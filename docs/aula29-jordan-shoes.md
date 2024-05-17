# Aula 29 - Jordan Shoes - Pagamento

> Nesta aula vamos fazer ajustes dos fluxos para finalização de compra.

## Ajuste criar a função de navegação irParaPagamento

1. Abaixo da função `irParaHome` crie a função `irParaPagamento`:

~~~javascript
const irParaPagamento = () => {
    // aula 27
    ocultarElemento(sectionIdentifiquese)
    // aula 28
    if(numeroItens.innerHTML > 0) {
        ocultarElemento(sectionHero)
        ocultarElemento(sectionProdutos)
        ocultarVoltarEsecaoDetalhes()      // IMPORTANTE
        ocultarElemento(sectionCarrinho)   // IMPORTANTE
        mostrarElemento(sectionPagamento)
    }
}

~~~

> Ajuste os códigos nos escutadores de eventos dos dois formulários - `formularioLogar` e `formularioCadastrarUsuario`, as 10 linhas finais substitua pela chamada da função `irParaPagamento()`

## Como guardar o usuário logado

1. Guardar o nome do usuário logado.
2. Guardar informações sobre a compra.
3. Finalizar a compra.

Após fazer o login seja pelo `formularioLogin` ou `formularioCadastrarUsuario`, vamos adicionar as linhas necessárias para guardar o usuário de uma forma 'mais persistente':

~~~javascript
formularioLogar.addEventListener('submit', (e) => {
    e.preventDefault()
    // pegar dados e validar para autorizar entrada
    console.log(emailLogin.value, senhaLogin.value)
    nomeUsuario.innerHTML = emailLogin.value
    mostrarElemento(btnLogout)
    formularioLogar.reset()
    fecharModal()
    // aula 28
    usuarioLogado = true
    console.log('Usuário logado ', usuarioLogado)
    // aula 29
    localStorage.setItem('nomeUsuario', nomeUsuario.innerHTML)
    console.log(localStorage.getItem('nomeUsuario')
    irParaPagamento()
})

const logout = () => {
    ocultarElemento(btnLogout)
    nomeUsuario.innerHTML = ''
    // aula 28
    usuarioLogado = false
    console.log('Usuário logado ', usuarioLogado)
    irParaHome()
    // aula 29
    localStorage.removeItem('nomeUsuario')
    localStorage.removeItem('carrinho')
}

~~~

> Na função `logout` estamos removendo os itens do localStoragem, simulando a 'desconexão'.

## Na 'funcaoCadastrarUsuario' como guardar o usuario

> No final adicione as linhas para armazenarmos os dados do usuário usando o `localStorage`:

~~~javascript
formularioCadastrarUsuario.addEventListener('submit', (e) => {
    e.preventDefault()
    // pegar dados, validar e autenticar
    const email = document.querySelector('#email_usuario').value
    const senha = document.querySelector('#senha_usuario').value
    const confirmaSenha = document.querySelector('#confirma_senha_usuario').value

    // validação
    const mensagemSenhaInvalida = senha.length < 5 ? 'Digite uma senha com no mínimo 5 caracteres' : 'Senha e confirmação SÃO diferentes'
    if(senha.length < 5 || senha !== confirmaSenha) {
        formAviso.innerHTML = mensagemSenhaInvalida
        return
    }

    // armazenar e autenticar - login
    formularioCadastrarUsuario.reset()
    formAviso.innerHTML = ''
    modalCadastrarUsuario.classList.remove('show')
    overlayCadastrarUsuario.classList.remove('show')

    const usuario = {
        email,
        senha
    }
    console.log(usuario)
    nomeUsuario.innerHTML = usuario.email
    mostrarElemento(btnLogout)
    // aula 28
    usuarioLogado = true
    console.log('Usuário logado ', usuarioLogado)
    // aula 29
    localStorage.setItem('nomeUsuario', nomeUsuario.innerHTML)
    console.log(localStorage.getItem('nomeUsuario')
    irParaPagamento()
})

~~~

## Como fazer o pagamento

Para fazer o pagamento precisamos coletar e organizar as seguintes informações:

1. Dados do Usuário logado
2. Carrinho - produto, id, descrição, tamanho, preço + Total do carrinho
3. Dados de pagamento

Todas essas informações em conjunto formam um 'pedido' ou 'compra', na função `atualizarCarrinho` vamos adicionar a chamada à função `criarCompra`:

~~~javascript
const atualizarCarrinho = (cart) => {
    corpoTabela.innerHTML = "" // limpar linhas da tabela

    cart.map( produto => {
        corpoTabela.innerHTML += `
            <tr>
                <td>${produto.id}</td>
                <td>${produto.nome}</td>
                <td class='coluna_tamanho'>${produto.tamanho}</td>
                <td class='coluna_preco'>${produto.preco}</td>
                <td class='coluna_apagar'>
                    <span class="material-symbols-outlined" data-id="${produto.id}">
                        delete
                    </span>
                </td>
            </tr>
        `
    })

    const total = cart.reduce( (valorAcumulado, item) => {
        return valorAcumulado + limparFormatoReal(item.preco)
    }, 0)
    colunaTotal.innerHTML = numberFormatBR.format(total)
    // aula 17
    spanSubTotal.innerHTML = numberFormatBR.format(total)
    spanTotalCompra.innerHTML = numberFormatBR.format(total + valorFrete - valorDesconto)
    
    acaoBotaoApagar()
    criarCompra() // aula 29
}

~~~

## Função criarCompra

Abaixo da função `atualizarCarrinho` vamos implementar a função `criarCompra`:

~~~javascript
// aula 29
let compra = {}

const criarCompra = () => {
    console.log(cart)
    const dataAtual = new Date().toLocaleString()

    compra = {
        dataCompra: dataAtual,
        carrinho: cart,
        totalCompra: limparFormatoReal(spanTotalCompra.innerHTML)
    }
    localStorage.setItem('carrinho', JSON.stringify(compra))
    console.log(JSON.parse(localStorage.getItem('carrinho')))
}

~~~

> Na função `criarCompra` criamos um objeto literal que é formado pelos dados da compra - usuário, data, produtos no carrinho e total da compra. Com base nisto, podemos ir para o Pagamento.

Criamos a variável em `localStoragem` para 'persistir' os dados, simulando como seria armazenar em um banco de dados.

## Ajuste da const cart

Antes vamos fazer um ajuste na `const cart`, mude ela para `let`, por volta da linha 170 ou 180:

~~~javascript
// PAGE carrinho
// pegar dados dos produtos
let cart = [] // aula 29

~~~

## Comentar as linhas do btnFinalizarCompra

> Antes vamos comentar as linhas 395 até 401 que tem a seleção e o escutar de eventos do `btnFinalizarCompra`:

~~~javascript
// aula 29
// const btnFinalizarCompra = document.querySelector('.btn_finalizar_compra')
// btnFinalizarCompra.addEventListener('click', () => {
//     ocultarElemento(sectionPagamento)
//     mostrarElemento(sectionHero, 'flex')
//     mostrarElemento(sectionProdutos, 'flex')
// })
~~~

> Se quiser apagar essas linhas não tem problema.

## Processar formulário de Pagamento

Podemos digitar os códigos lá no final do nosso script. Para pegar os dados do pagamento e gerar um pedido, digite abaixo da função `criarCompra` os seguintes códigos:

~~~javascript
// pegar os dados do pagamento
const formularioPagamento = document.querySelector('.form_pagamento')
const numeroCartao = document.querySelector('#numero_cartao')
const nomeImpresso = document.querySelector('#nome_impresso')
const validade = document.querySelector('#validade')
const codigoSeguranca = document.querySelector('#codigo_seguranca')
const numeroParcelas = document.querySelector('#numero_parcelas')

formularioPagamento.addEventListener('submit', (e) => {
    e.preventDefault()
    let cartao = {
        numeroCartao: numeroCartao.value,
        nomeImpresso: nomeImpresso.value,
        validade: validade.value,
        codigoSeguranca: codigoSeguranca.value,
        numeroParcelas: numeroParcelas.value
    }
    console.log(cartao)

    // pedido
    const pedido = {
        id: 1,
        usurio: localStorage.getItem('nomeUsuario'),
        carrinho: JSON.parse(localStorage.getItem('carrinho')),
        cartao: cartao
    }
    localStorage.setItem('pedido', JSON.stringify(pedido))
    // limpar formulario e ir para home
    formularioPagamento.reset()
    irParaHome()
    cart = []
    atualizarCarrinho(cart)
    atualizarNumeroItens()
    console.log(pedido)
    console.log(localStorage.getItem('pedido'))
})
// /aula 29

~~~

> Salve as alterações e teste.

## Considerações

> Esta aula vimos como fazer para finalizar a compra, mas, antes fizemos alguns ajustes no código.

Vocês devem ter percebido que o código está complexo, e não está fácil de manutenção, nem de extensão. É um grande indicativo de que precisa ser refatorado.

Salve Devs, até as próximas!
