# Aula 16 - Jordan Shoes - Funções Úteis

> Nesta aula vamos implementar duas funcionalidades de otimizar nosso código evitando repetições.

## Função ocultarElemento

1. Abaixo das declarações das constantes implemente a seguinte função:

~~~javascript
const ocultarElemento = (elemento) => {
    elemento.style.display = 'none'
}
~~~

> Ela será usada nas linhas onde selecionávamos o elemento e definiamos o style.display = 'none' para ocultar o elemento selecionado.

## Função mostrarElemento

1. Abaixo da definição da função ocultarElemento implemente a seguinte função:

~~~javascript
const mostrarElemento = (elemento, display='block') => {
    elemento.style.display = display
}
~~~

> Ela será usada nas linhas onde selecionávamos o elemento e definiamos o style.display = 'block', 'flex' ou 'grid' para mostrar o elemento selecionado.

## Refatorando

1. Em cada linha onde usamos a seleção do elemento com a propriedade style.display, substituia pela função `ocultarElemento` ou `mostrarElemento`, abaixo temos só os trechos de código que foram modificados:

~~~javascript
// trecho de codigo ...

// NAVEGACAO
const ocultarVoltarEsecaoDetalhes = () => {
    ocultarElemento(botaoVoltar)
    ocultarElemento(sectionDetalhesProduto)
}
ocultarVoltarEsecaoDetalhes()

botaoVoltar.addEventListener('click', () => {
    mostrarElemento(sectionProdutos, 'flex')
    ocultarVoltarEsecaoDetalhes()
    // resetarSelecao(radios)
})

const btnCarrinho = document.querySelector('.btn__carrinho .icone')
btnCarrinho.addEventListener('click', () => {
    mostrarElemento(sectionCarrinho)
    ocultarElemento(sectionHero)
    ocultarElemento(sectionProdutos)
    ocultarElemento(sectionDetalhesProduto)
})

const btnHome = document.querySelector('.link_home')
btnHome.addEventListener('click', (event) => {
    event.preventDefault()
    ocultarElemento(sectionCarrinho)
    mostrarElemento(sectionHero, 'flex')
    mostrarElemento(sectionProdutos, 'flex')
    ocultarVoltarEsecaoDetalhes()
})

// NUMERO DE ITENS do CARRINHO
const numeroItens = document.querySelector('.numero_itens')
ocultarElemento(numeroItens)

const atualizarNumeroItens = () => {
    numeroItens.style.display = cart.length ? 'block' : 'none'
    numeroItens.innerHTML = cart.length
}

// trecho de codigo ...

// preencher card
const preencherCard = (card, products) => {
    card.addEventListener('click', (e) => {
        // ocultar produtos e mostrar o botão e página de detalhes do produto
        ocultarElemento(sectionProdutos)
        mostrarElemento(botaoVoltar)
        mostrarElemento(sectionDetalhesProduto, 'grid')

        // identificar qual card foi clicado
        const cardClicado = e.currentTarget
        const idProduto = cardClicado.id
        const produtoClicado = products.find( product => product.id == idProduto )
        // preencher os dados de detalhes do produto
        preencherDadosProduto(produtoClicado)
    })
}

// trecho de codigo ...

// selecionar o span do id e ocultar ele
const spanId = document.querySelector('.detalhes span')
ocultarElemento(spanId)

// trecho de codigo ...

// PAGE carrinho
// pegar dados dos produtos
const cart = []

const btnAddCarrinho = document.querySelector('.btn__add_cart')
btnAddCarrinho.addEventListener('click', () => {
    // pegar dados do produto adicionado
    const produto = {
        id: document.querySelector('.detalhes span').innerHTML,
        nome: document.querySelector('.detalhes h4').innerHTML,
        modelo: document.querySelector('.detalhes h5').innerHTML,
        preco: document.querySelector('.detalhes h6').innerHTML.replace('R$&nbsp;', ''),
        tamanho: document.querySelector('input[type="radio"][name="size"]:checked').value
    }
    cart.push(produto) // adicionar o produto ao array cart -> carrinho
    ocultarVoltarEsecaoDetalhes()
    ocultarElemento(sectionHero)
    mostrarElemento(sectionCarrinho)
    atualizarCarrinho(cart)
    atualizarNumeroItens()
})

// trecho de codigo ...

~~~

Salve as alterações e teste no navegador.

## Considerações

> Esta aula rápida vimos como refatorar duas funcinalidades para evitar repetição de códigos, melhorar a legibilidade, manutebilidade e extensão da nossa aplicação, aplicando conceitos do Clean Code.

Salve Devs, até as próximas!
