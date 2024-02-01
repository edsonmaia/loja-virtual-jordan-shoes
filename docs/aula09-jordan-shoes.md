# Aula 09 - Jordan Shoes - Exibir detalhes do produto

> Vamos aprender como exibir os detalhes do produto de acordo com o card que foi clicado.

## Ajustes no JS

1. Abra o arquivo `script.js`
2. Faça os seguintes acréscimos:
2.1 Abaixo da linha de criação do card adicione a definição do id para o card:

~~~javascript
    card.id = product.id // 1º passo na aula 09
~~~

2.2 Dentro do escutador de eventos de click no card adicione as seguintes linhas, abaixo das instruções de mostrar/ocultar:

~~~javascript
    // identificar qual card foi clicado
    const cardClicado = e.currentTarget
    const idProduto = cardClicado.id
    const produtoClicado = products.find( product => product.id == idProduto )
    // console.log(produtoClicado)
    // preencher os dados de detalhes do produto
    preencherDadosProduto(produtoClicado)
~~~

2.3 Fora do escutador de eventos, lá no final do código adicione a definição da função `preencherDadosProduto`:

~~~javascript
const preencherDadosProduto = (product) => {
    // preencher imagens
    const images = document.querySelectorAll('.produto__detalhes_imagens figure img')
    const imagesArray = Array.from(images)
    imagesArray.map( image => {
        image.src = `./images/${product.image}`
    })

    // preencher nome, modelo e preco
    document.querySelector('.detalhes h4').innerHTML = product.product_name
    document.querySelector('.detalhes h5').innerHTML = product.product_model
    document.querySelector('.detalhes h6').innerHTML = numberFormat.format(product.price)
}

~~~

## Código JS completo

~~~javascript

const botaoVoltar = document.querySelector('.voltar')
const sectionDetalhesProduto = document.querySelector('.produto__detalhes')
const sectionProdutos = document.querySelector('.produtos')
// ocultar botao voltar e secao de detalhos do produto
botaoVoltar.style.display = 'none'
sectionDetalhesProduto.style.display = 'none'

const numberFormat = new Intl.NumberFormat('pt-BR', {
    style: 'currency',
    currency: 'BRL',
    minimumFractionDigits: 2,
    maximumFractionDigits: 2,
})

const getProducts = async () => {
    const response = await fetch('js/products.json')
    const data = await response.json()
    return data
}

const generateCard = async () => {
    const products = await getProducts()
    products.map(product => {
        let card = document.createElement('div')
        card.id = product.id // 1o passo da aula 09
        card.classList.add('card__produto')
        card.innerHTML = `
        <figure>
            <img src="images/${product.image}" alt="${product.product_name}" />
        </figure>
        <div class="card__produto_detalhes">
            <h4>${product.product_name}</h4>
            <h5>${product.product_model}</h5>
        </div>
        <h6>${numberFormat.format(product.price)}</h6>
        `
        const listaProdutos = document.querySelector('.lista__produtos')
        listaProdutos.appendChild(card)

        card.addEventListener('click', (e) => {
            // ocultar produtos e mostrar o botão e página de detalhes do produto
            sectionProdutos.style.display = 'none'
            botaoVoltar.style.display = 'block'
            sectionDetalhesProduto.style.display = 'grid'

            // identificar qual card foi clicado
            const cardClicado = e.currentTarget
            const idProduto = cardClicado.id
            const produtoClicado = products.find( product => product.id == idProduto )
            // console.log(produtoClicado)
            // preencher os dados de detalhes do produto
            preencherDadosProduto(produtoClicado)
        })

    })
}

generateCard()

botaoVoltar.addEventListener('click', () => {
    sectionProdutos.style.display = 'flex'
    botaoVoltar.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
})

const preencherDadosProduto = (product) => {
    // preencher imagens
    const images = document.querySelectorAll('.produto__detalhes_imagens figure img')
    const imagesArray = Array.from(images)
    imagesArray.map( image => {
        image.src = `./images/${product.image}`
    })

    // preencher nome, modelo e preco
    document.querySelector('.detalhes h4').innerHTML = product.product_name
    document.querySelector('.detalhes h5').innerHTML = product.product_model
    document.querySelector('.detalhes h6').innerHTML = numberFormat.format(product.price)
}

~~~

## EXTRA - Ajustes no HTML

> Só para otimizar a melhoria da página de detalhes, vamos substituir no html aquele caminho que estávamos usando por um de uma imagem genérica, pode ser do placehold.co. Usamos o link

https://placehold.co/300x200

1. Selecione só o conteúdo de `src` da tag `img` das nossas `figures`
2. Use o `CTRL + H` para localizar e substituir
3. Cole a url https://placehold.co/300x200
4. Clique no botão Substituir tudo
5. Salve as alterações e teste no navegador.

~~~html
<div class="produto__detalhes_imagens">
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
    <figure>
        <img src="https://placehold.co/300x200" alt="" />
    </figure>
</div>

~~~

## EXTRA - Ajuste no CSS

1. No seletor da tag h4 que é o título do produto no card adicione as seguintes linha de código:

~~~css

.card__produto_detalhes h4 {
    font-size: 18px;
    line-height: 28px;
    /* ajuste feito na aula 09 */
    white-space: nowrap;
    width: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
}

~~~

2. Lembre-se que já tinha tamanho e altura de fonte.
3. Salve as alterações e teste no navegador.

> Veja que nos cards, os títulos que são muito extensos, se, não couberem no espaço, não vão quebrar, e no final aparecerá ...

## Links utilizado nesta aula

> https://placehold.co/300x200

## Considerações

Nesta aula vimos como identificar o card clicado, e a partir disto, filtramos as informações do produto clicado, e em seguida usamos essas informações para preencher os dados da página de detalhes do produto. Por fim, com extras vimos como utilizar o placehold.co para gerar uma imagem genérica a ser usada na página de detalhes e também vimos como fazer o uso do text-ellipsis para exibir reticências em títulos muito extensos, para que eles não quebrem a linha, nem baguncem a exibição dos dados do card. Nas próximas aulas iremos resolver outros desafios desta nossa aplicação.

Salve Devs, até as próximas!
