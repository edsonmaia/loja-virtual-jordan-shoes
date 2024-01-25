# Aula 03 - Jordan Shoes - JS

## Criar cards dinâmicos

>> Vamos criar os cards de produtos dinamicamente utilizando o JavaScript.

## Preparação

1. Copie o arquivo `products.json` para dentro da sua pasta `js`.
2. Apague os espaços em branco de dois arquivos de imagens, e apague também o 1 do final do nome deles.
3. No `index.html`, deixe o código de 'apenas um card' para usarmos como referência, depois vamos apagá-lo também.

## Código em JS

1. Abra o arquivo `script.js`
2. Faça o seguinte código:

~~~javascript

console.log('Jordan Shoes')

const getProducts = async () => {
    const response = await fetch('js/products.json')
    const data = await response.json()
    return data
}

const generateCard = async () => {

    const products = await getProducts()

    products.map(product => {
        let card = document.createElement('div')
        card.classList.add('card__produto')
        
        card.innerHTML = `
        <figure>
            <img src="images/${product.image}" alt="${product.product_name}" />
        </figure>

        <div class="card__produto_detalhes">
            <h4>${product.product_name}</h4>
            <h5>${product.product_model}</h5>
        </div>

        <h6>R$ ${product.price}</h6>
        `

        const listaProdutos = document.querySelector('.lista__produtos')
        listaProdutos.appendChild(card)

    })
   
}

generateCard()

~~~

3. Salve as alterações e veja o resultado no browser.

## Considerações

Nesta aula vimos como ler dados de um arquivo json para fazer a geração de cards dinâmicos utilizando o JavaScript. Nas próximas aulas vamos fazer alguns ajustes no projeto, trabalhar a responsividade.

Salve Devs, até as próximas!
