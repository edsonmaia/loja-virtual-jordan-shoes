# Aula 24 - Jordan Shoes - Ajustes na interface e uso do localStorage

> Nesta aula fazer ajustes na interface para permitir o acesso aos dados do usuário. Mas, antes vamos limitar o acesso ao carrinho de compras, somente, se tiver pelo menos um item adicionado.

## Ajustes no acesso ao carrinho

> Para limitar o acesso ao carrinho usando o botão só se tiver 1 item ou mais. No arquivo 'script.js' mude o código do escutador de eventos, na linha 30 do nosso código em diante:

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
})

~~~

> Dentro do escutador organizamos as ações mostrar e ocultar dentro de uma estrutura if simples que avalia se o numeroItens for maior do que zero.

Salve as alterações e faça os testes no browser. Veja que só teremos acesso ao carrinho pelo botão se tiver pelo menos 1 item adicionado ao carrinho.

>> Poderiamos ter usado uma outra estratégia, exibir a página do carrinho, porém, indicando textualmente nela que o carrinho está vazio. E utilizar links ou botões sugerindo a adição de produto no carrinho.

## Ajuste no fluxo da ação finalizar cadastro

No escutador de eventos do 'btnFinalizarCadastro', vamos ajustar as ações a serem feitas após o formulário ser considerado válido:

~~~javascript
// aula 24 - ajustes do fluxo
const btnFinalizarCadastro = document.querySelector('.btn_finalizar_cadastro')
btnFinalizarCadastro.addEventListener('click', (event) => {
    
    event.preventDefault()
    
    // validacoes
    validacaoDoFormulario()

    // pegar dados
    if(validacaoDoFormulario()) {
        console.log(pegarDados())
        localStorage.setItem('dados', JSON.stringify(pegarDados()))
        // console.log(JSON.parse(localStorage.getItem('dados')))
        formularioIdentificacao.reset()
        ocultarElemento(sectionIdentificacao)
        mostrarElemento(sectionPagamento)
    }
    
})

~~~

Dentro do if que avalia se o formulário é válido, se for válido:

1. Vamos fazer um 'mock' dos dados usando 'localStorage' para armazenar os dados do cliente em um objeto
2. Só depois vamos limpar o 'formularioIdentificacao' e depois ocultá-lo
3. E por fim mostrar a 'sectionPagamento'.

Salve as alterações e teste no navegador.

## Ajustes no HTML

Precisamos adicionar um ícone para identificar o usuário. Ajuste o código do 'header .topo' das linhas 23 a 27:

~~~html
<div class="btn__carrinho">
    <div class="btn__carrinho_icone">
        <span class="material-symbols-outlined icone">
            shopping_cart
        </span>
        <span class="numero_itens">0</span>
    </div>

    <div class="btn__carrinho_user">
        <span class="material-symbols-outlined icone">
            account_circle
        </span>
        <span>User</span>
    </div>
</div>

~~~

> Colocamos os spans dos ícones e textos dentro de divs para facilitar as formatações css.

## Ajustes no CSS

No arquivo 'style.css' a partir da linha 50 ajuste o código para ficar conforme o exemplo abaixo, nas linhas 50 até 63:

~~~css
.btn__carrinho {
    position: relative;
    display: flex;
}

.btn__carrinho_icone {
    position: relative;
}

.btn__carrinho_user {
    display: flex;
    align-items: center;
}

~~~

Salve as alterações e teste no navegador.

## Considerações

> Esta aula vimos como fazer ajustes no projeto para exibir o ícone de usuário, organizar a posição dos ícones na barra. Também ajustamos o controle de acesso ao carrinho de compras pelo botão, somente se tiver item adicionado. E finalizamos com o armazenamento dos dados de identificação utilizando localStorage e definimos a passagem do fluxo para a seção de pagamento.

Salve Devs, até as próximas!
