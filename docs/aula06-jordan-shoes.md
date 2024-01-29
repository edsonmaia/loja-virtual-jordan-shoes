# Aula 06 - Jordan Shoes - Extra

## Formatação de valores numéricos no estilo monetário

~~~javascript
console.log('Jordan Shoes')

const formatCurrency = (number) => {
  return number.toLocaleString('pt-BR', {
            style: 'currency',
            currency: 'BRL',
    })
}

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

        <h6>${formatCurrency(product.price)}</h6>
        `

        const listaProdutos = document.querySelector('.lista__produtos')
        listaProdutos.appendChild(card)

    })
   
}

generateCard()

~~~

## Outra forma é utilizando o Intl.

~~~javascript

// valor é a variável ou constante a ser formatada.
// No nosso exemplo é product.price

const numberFormat = new Intl.NumberFormat('pt-BR', {
  style: 'currency',
  currency: 'BRL',
  minimumFractionDigits: 2,
  maximumFractionDigits: 2,
})

numberFormat.format(valor)

~~~

## Links da Documentação

> https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString
> https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat

## Considerações

Nesta aula extra vimos como fazer a formatação de valores numéricos no estilo monetário utilizando toLocaleString e Intl.NumberFormat

Salve Devs, até as próximas!
