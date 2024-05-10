# Aula 28 - Jordan Shoes - Está logado ou não

> Nesta aula fazer ajustes dos fluxos de identificação do usuário, se está logado para finalização de compra.

## Controle de usuário logado ou não

Não estamos trabalhando com controle de sessão, autenticação utilizando cookies, tokens, nada do tipo, estamos "simulando" o que pode ser feito nos casos do usuário estar logado ou não, quando ele for continuar a compra para finalizar.

Adicione as seguintes linhas de código, a partir da linha 8, para a variável ficar na parte de cima do código:

~~~javascript
// aula 28
let usuarioLogado = false
console.log('usuario logado ', usuarioLogado)

~~~

1. A variável 'usuarioLogado' serve para controlarmos o estado, ou seja, a situação, se o usuário está logado ou não. Ela começa como 'false', mas, o valor dela deve mudar, caso o usuário fizer o login. E voltar para 'false' quando fizer logout.
2. O console.log serve para debugarmos o nosso código enquanto estamos fazendo os testes de uso.

## Criar função que vai para página Home

Abaixo do comentário // NAVEGAÇÃO crie a seguinte função:

~~~javascript
const irParaHome = () => {
    ocultarElemento(sectionPagamento)
    ocultarElemento(sectionIdentificacao)
    ocultarElemento(sectionIdentifiquese)
    ocultarElemento(sectionCarrinho)
    ocultarElemento(botaoVoltar)
    ocultarElemento(sectionDetalhesProduto)
    mostrarElemento(sectionHero, 'flex')
    mostrarElemento(sectionProdutos, 'flex')
}

~~~

## Ajustes no botão Home

1. No 'btnHome' vamos ajustar o código:

~~~javascript
const btnHome = document.querySelector('.link_home')
btnHome.addEventListener('click', (event) => {
    event.preventDefault()
    irParaHome()
})

~~~

## O que fazer após logar

1. Após fazer o login temos que definir o fluxo, para onde vamos, o que vai aparecer, o que deve sumir da tela.
2. A mesma linha de raciocínio deve ser seguida em caso de logout.
3. No 'formularioLogar' vamos refatorar o código para usar uma condição para exibir a 'sectionIdentifiquese':

> Vamos garantir também que as sessões 'sectionIdentifiquese' e 'sectionCarrinho' ficarão ocultas:

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
    console.log('usuario logado ', usuarioLogado)
    // aula 27
    ocultarElemento(sectionIdentifiquese)
    // aula 28
    ocultarElemento(sectionCarrinho)
    if(numeroItens.innerHTML > 0) {
        ocultarElemento(sectionHero)
        ocultarElemento(sectionProdutos)
        ocultarVoltarEsecaoDetalhes()      // IMPORTANTE
        ocultarElemento(sectionCarrinho)   // IMPORTANTE
        mostrarElemento(sectionPagamento)
    }
})

const logout = () => {
    ocultarElemento(btnLogout)
    nomeUsuario.innerHTML = ''
    // aula 28
    usuarioLogado = false
    console.log('Usuário logado ', usuarioLogado)
    irParaHome()
}

~~~

> No 'logout' temos que mudar o estado da variável 'usuarioLogado', controlar a exibição e ocultação das seções após sair, ou seja, após fazer a desconexão.

## Ajuste no botão Apagar item do carrinho

No botão 'acaoBotaoApagar' vamos garantir que as 'sectionIdentifiquese' e 'sectionPagamento' fiquem ocultas, e que o usuário seja redirecionado para a 'Home', se o carrinho estiver vazio:

~~~javascript
const acaoBotaoApagar = () => {
    const botaoApagar = document.querySelectorAll('.coluna_apagar span')
    botaoApagar.forEach( botao => {
        botao.addEventListener('click', () => {
            const id = botao.getAttribute('data-id')
            const posicao = cart.findIndex( item => item.id == id )
            cart.splice(posicao, 1)
            atualizarCarrinho(cart)
        })        
    })
    atualizarNumeroItens()
    // aula 28
    if (numeroItens.innerHTML <= 0) {
        irParaHome()
    }
}

~~~

## Restringir o fluxo do botão Continuar

No 'btnContinuar' criar as regras
- Só pode Continuar se no carrinho tiver pelo menos 1 item
- Se estiver logador, mostrar 'sectionPagamento', senão, mostrar 'sectionIdentifiquese'

~~~javascript
const btnContinuarCarrinho = document.querySelector('.btn_continuar')
btnContinuarCarrinho.addEventListener('click', () => {
    ocultarElemento(sectionCarrinho)
    // mostrarElemento(sectionIdentificacao)
    // aula 27
    // mostrarElemento(sectionIdentifiquese, 'flex')
    // aula 28
    if (usuarioLogado) {
        mostrarElemento(sectionPagamento)
        return
    }
    mostrarElemento(sectionIdentifiquese, 'flex')
})

~~~

## Ajustes no botão Carrinho

No 'btnCarrinho' vamos ajustar o código:

~~~javascript
const btnCarrinho = document.querySelector('.btn__carrinho .icone')
btnCarrinho.addEventListener('click', () => {
    if(numeroItens.innerHTML > 0) {
        mostrarElemento(sectionCarrinho)
        ocultarElemento(sectionHero)
        ocultarElemento(sectionProdutos)
        ocultarElemento(sectionDetalhesProduto)
        ocultarElemento(sectionIdentificacao)
        ocultarElemento(sectionPagamento)
    }
    // aula 28
    ocultarElemento(sectionIdentifiquese)
    if(usuarioLogado) {
        ocultarElemento(sectionIdentifiquese)
        ocultarElemento(sectionPagamento)
    }
})

~~~

## O que fazer após criar nova conta

No final do escutador de eventos do 'formularioCadastraUsuario' faça os ajustes:

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
    // aula 27
    ocultarElemento(sectionIdentifiquese)
    //mostrarElemento(sectionPagamento)
    // aula 28
    if(numeroItens.innerHTML > 0) {
        ocultarElemento(sectionHero)
        ocultarElemento(sectionProdutos)
        ocultarVoltarEsecaoDetalhes()      // IMPORTANTE
        ocultarElemento(sectionCarrinho)   // IMPORTANTE
        mostrarElemento(sectionPagamento)
    }

})

~~~

## Restringir o acesso às janelas modais de login e cadastro

No escutador de eventos de click em 'btnOpenLogin' ou 'btnFazerLogin' criar a restrição. Só permitir abrir mostraModal() se não estiver logado:

~~~javascript
document.addEventListener('click', (e) => {
    if(e.target === btnOpenLogin || e.target === btnFazerLogin) {
        (!usuarioLogado) && mostrarModal() // ajuste aula 28
    }
})

~~~

## Considerações

> Esta aula vimos como fazer os ajustes necessários para controlar a identificação do usuário. Se estiver logado e com item no carrinho, pode prosseguir para a seção de Pagamento para finalizar a compra.

Vocês devem ter percebido que o código está complexo, e não está fácil de manutenção, nem de extensão. É um grande indicativo de que precisa ser refatorado.

Salve Devs, até as próximas!
