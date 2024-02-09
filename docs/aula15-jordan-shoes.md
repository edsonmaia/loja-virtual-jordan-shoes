# Aula 15 - Refatoração

> Neste aula apresento para vocês algumas sugestões de refatoração, melhorias na organização do nosso código. Você pode fazer passo a passo ou simplesmente copiar o código JS completo e colar no seu arquivo script.js

## Refatoração

  1. Organizar as `constantes` de seleção dos elementos de tela

1.1 Colocar todas na parte superior do código para facilitar o uso delas

~~~javascript
const sectionHero = document.querySelector('.hero')
const sectionProdutos = document.querySelector('.produtos')
const botaoVoltar = document.querySelector('.voltar')
const sectionDetalhesProduto = document.querySelector('.produto__detalhes')
const sectionCarrinho = document.querySelector('.carrinho')

~~~

 2. Organizar as `funções` de navegação da aplicação

2.1 Renomear a função `ocultarBotaoEsecao` para `ocultarVoltarEsecaoDetalhes`, em todas ocorrências

2.2 Agrupar as funções de navegação da aplicação após as constantes

~~~javascript
// NAVEGACAO
const ocultarVoltarEsecaoDetalhes = () => {
    botaoVoltar.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
}
ocultarVoltarEsecaoDetalhes()

~~~

> Coloque também o escutador de eventos do botão Voltar perto dos códigos de navegação

2.3 Podemos criar outras funções para mostrar/ocultar `hero` e `produtos`

2.4 Renomear a função `numberFormat` para `numberFormatBR`, em todas ocorrências, só tome cuidado com o nome `NumberFormat` na declaração de uma nova (new) instância do `Intl.NumberFormat()`.

2.4 Comente a função

~~~javascript
// Formatar números para formato monetário brasileiro e exibir o símbolo R$
~~~

2.5 Se achar útil, podemos criar uma função para fazer a formatação para o padrão US internacional:

~~~javascript
const numberFormatUS = new Intl.NumberFormat('en-US', {
    style: 'decimal',
    useGrouping: false,
    minimumFractionDigits: 2,
    maximumFractionDigits: 2,
})

~~~

 3. Comentar as funções `getProducts` e `generateCard`, respectivamente:

~~~javascript
// PAGE HOME
// pegar dados dos produtos

// gerar dinamicamente os cards de cada produto
~~~

 4. Comentar a função `preencherDadosProduto`, com o seguinte:

~~~javascript
// PAGE DETALHES
// preencher dados do produto na pagina detalhes do produto
~~~

 5. Após a seleção de `details`, tem um escutador de eventos dele.

 6. Mova a definição da função `preencherCard`, coloque-a após a evocação da função `generateCard`.

> Como estamos usando arrow functions a posição da definição da função, não é um problema, como é nas funções 'comuns', porém, é importante, deixar os códigos próximo, para facilitar a leitura do código e sua manutenção, ou melhorias.

 7. As ações de mostrar/ocultar que estão no escutador de eventos do card da função `preencherCard` poderiam ser organizadas em funções externas, isto, é só uma sugestão, pois, a função tem 12 linhas, contando com os 3 comentários internos.

 8. As linhas de seleção do `btnCarrinho`, `btnHome` e seus escutadores de eventos, precisam ser movidos lá para a parte de navegação, que está na parte de cima do código:

~~~javascript
const btnCarrinho = document.querySelector('.btn__carrinho .icone')

btnCarrinho.addEventListener('click', () => {
    sectionCarrinho.style.display = 'block'
    sectionHero.style.display = 'none'
    sectionProdutos.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
})

const btnHome = document.querySelector('.link_home')
btnHome.addEventListener('click', (event) => {
    event.preventDefault()
    sectionCarrinho.style.display = 'none'
    sectionHero.style.display = 'flex'
    sectionProdutos.style.display = 'flex'
    ocultarVoltarEsecaoDetalhes() // ajuste aula 12
})

~~~

 9. Uma linha acima da criação do array `cart` coloque os seguintes comentários:

~~~javascript
// PAGE CARRINHO
// criar array do carrinho
const cart = []

~~~

10. Dentro do escutador de eventos do `btnAddCarrinho`, mude a forma que pegamos o preco:

~~~javascript
preco: document.querySelector('.detalhes h6').innerHTML.replace('R$&nbsp;', ''),
~~~

> usando o replace estamos tirando os textos do símbolo monetário e o espaço do preço.

10.1 Apague os `console.log` que estão nesse código, apague comentários e linhas em branco, deixe da seguinte forma:

~~~javascript
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
    sectionHero.style.display = 'none' // ocultar hero
    sectionCarrinho.style.display = 'block' // mostrar carrinho
    atualizarCarrinho(cart)
    atualizarNumeroItens()
})
~~~

> Depois, recolha a função

10.2 A criação da const `corpoTabela` e da função `atualizarCarrinho` estão bem organizadas, mas, vamos criar uma função externa para sanitizar os nossos valores monetários que estão formatados pelo numberFormatBR.

Crie o seguinte código abaixo da função `numberFormatBR`

~~~javascript
const limparFormatoReal = (valor) => {
    return parseFloat(valor.replace('R$&nbsp;', '').replace('.', '').replace(',', '.'))
}

~~~

> Veja que encapsulamos na função aqueles códigos de parseFloat e os três replaces, que limpam o número formatado, e deixam ele no formato internacional, apto para ser usado em cálculos

10.3 Agora dentro do return do `reduce` onde fazemos a somatória, vamos chamar a função `limparFormatoReal`:

~~~javascript
const total = cart.reduce( (valorAcumulado, item) => {
    return valorAcumulado + limparFormatoReal(item.preco)
}, 0)

~~~

> O restante do código permanece, a seleção da .coluna_total parece um pouco estranha, muito 'verbosa', porém, isso só seria resolvido se criássemos uma const, fora da função atualizarCarrinho, poderia ser abaixo de corpoTabela, e só chamar ela dentro da função, definindo o innerHTML ou textContent, já que só vamos exibir o resultado total (ou subtotal) da somatória do nosso carrinho.

11. Os trechos de código de seleção de `numeroItens` e a função `atualizarNumeroItens`, temos que mover, para colocar na parte de cima do nosso código, abaixo das seleções e escutadores dos `btnCarrinho` e `btnHome`, mude o comentário também e simpliquei a condicional ternária:

~~~javascript
// NUMERO DE ITENS do CARRINHO
const numeroItens = document.querySelector('.numero_itens')
numeroItens.style.display = 'none' // ocultar o numero_itens

const atualizarNumeroItens = () => {
    numeroItens.style.display = cart.length ? 'block' : 'none';
    numeroItens.innerHTML = cart.length
}

~~~

12. Mova também as linhas do `spanId` e da ocultação dele e coloque abaixo da função `preencherDadosProduto`, pois, ela é conteúdo da página detalhes:

~~~javascript
// selecionar o span do id e ocultar ele
const spanId = document.querySelector('.detalhes span')
spanId.style.display = 'none'

~~~

13. Por fim, dentro da função `acaoBotaoApagar`, apague os console.log, e as linhas em branco.

> Salve as alterações e teste.

## Código JS após as organizações

~~~javascript
const sectionHero = document.querySelector('.hero')
const sectionProdutos = document.querySelector('.produtos')
const botaoVoltar = document.querySelector('.voltar')
const sectionDetalhesProduto = document.querySelector('.produto__detalhes')
const sectionCarrinho = document.querySelector('.carrinho')

// NAVEGACAO
const ocultarVoltarEsecaoDetalhes = () => {
    botaoVoltar.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
}
ocultarVoltarEsecaoDetalhes()

botaoVoltar.addEventListener('click', () => {
    sectionProdutos.style.display = 'flex'
    ocultarVoltarEsecaoDetalhes()
    resetarSelecao(radios)
})

const btnCarrinho = document.querySelector('.btn__carrinho .icone')

btnCarrinho.addEventListener('click', () => {
    sectionCarrinho.style.display = 'block'
    sectionHero.style.display = 'none'
    sectionProdutos.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
})

const btnHome = document.querySelector('.link_home')
btnHome.addEventListener('click', (event) => {
    event.preventDefault()
    sectionCarrinho.style.display = 'none'
    sectionHero.style.display = 'flex'
    sectionProdutos.style.display = 'flex'
    ocultarVoltarEsecaoDetalhes() // ajuste aula 12
})

// NUMERO DE ITENS do CARRINHO
const numeroItens = document.querySelector('.numero_itens')
numeroItens.style.display = 'none' // ocultar o numero_itens

const atualizarNumeroItens = () => {
    (cart.length > 0) ? numeroItens.style.display = 'block' : numeroItens.style.display = 'none'
    numeroItens.innerHTML = cart.length
}

// Formatar numeros para formato monetario brasileiro e exibir o simbolo R$
const numberFormatBR = new Intl.NumberFormat('pt-BR', {
    style: 'currency',
    currency: 'BRL',
    minimumFractionDigits: 2,
    maximumFractionDigits: 2,
})

const limparFormatoReal = (valor) => {
    return parseFloat(valor.replace('R$&nbsp;', '').replace('.', '').replace(',', '.'))
}

// PAGE HOME
// pegar dados dos produtos
const getProducts = async () => {
    const response = await fetch('js/products.json')
    const data = await response.json()
    return data
}

// gerar dinamicamente os cards de cada produto
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
        <h6>${numberFormatBR.format(product.price)}</h6>
        `
        const listaProdutos = document.querySelector('.lista__produtos')
        listaProdutos.appendChild(card)
        preencherCard(card, products)
    })
}

generateCard()

// preencher card
const preencherCard = (card, products) => {
    card.addEventListener('click', (e) => {
        // ocultar produtos e mostrar o botão e página de detalhes do produto
        sectionProdutos.style.display = 'none'
        botaoVoltar.style.display = 'block'
        sectionDetalhesProduto.style.display = 'grid'

        // identificar qual card foi clicado
        const cardClicado = e.currentTarget
        const idProduto = cardClicado.id
        const produtoClicado = products.find( product => product.id == idProduto )
        // preencher os dados de detalhes do produto
        preencherDadosProduto(produtoClicado)
    })
}

// PAGE DETALHES
// preencher dados do produto na pagina detalhes do produto
const preencherDadosProduto = (product) => {
    // preencher imagens
    const images = document.querySelectorAll('.produto__detalhes_imagens figure img')
    const imagesArray = Array.from(images)
    imagesArray.map( image => {
        image.src = `./images/${product.image}`
    })

    // preencher nome, modelo e preco
    document.querySelector('.detalhes span').innerHTML = product.id // ajust a11
    document.querySelector('.detalhes h4').innerHTML = product.product_name
    document.querySelector('.detalhes h5').innerHTML = product.product_model
    document.querySelector('.detalhes h6').innerHTML = numberFormatBR.format(product.price)

}

// selecionar o span do id e ocultar ele
const spanId = document.querySelector('.detalhes span')
spanId.style.display = 'none'

// mudar icone do details frete
const details = document.querySelector('details')
details.addEventListener('toggle', () => {
    const summary = document.querySelector('summary')
    summary.classList.toggle('icone-expandir')
    summary.classList.toggle('icone-recolher')
})

// aula 12
// controlar seleção dos inputs radio
const radios = document.querySelectorAll('input[type="radio"]')
radios.forEach(radio => {
  radio.addEventListener('change', () => {
    const label = document.querySelector(`label[for="${radio.id}"]`)
    label.classList.add('selecionado')
    // console.log(label)
    radios.forEach(radioAtual => {
      if (radioAtual !== radio) {
        const outroLabel = document.querySelector(`label[for="${radioAtual.id}"]`)
        outroLabel.classList.remove('selecionado')
      }
    })
  })
})

const resetarSelecao = (radios) => {
    radios.forEach(radio => {
        radios.forEach(radioAtual => {
            if (radioAtual !== radio) {
                const outroLabel = document.querySelector(`label[for="${radioAtual.id}"]`)
                outroLabel.classList.remove('selecionado')
            }
        })
    })
}

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
    sectionHero.style.display = 'none' // ocultar hero
    sectionCarrinho.style.display = 'block' // mostrar carrinho
    atualizarCarrinho(cart)
    atualizarNumeroItens()
})

const corpoTabela = document.querySelector('.carrinho tbody')

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

    // aula 14 - R$&nbsp;1.123,45 -> 1123.45
    const total = cart.reduce( (valorAcumulado, item) => {
        return valorAcumulado + limparFormatoReal(item.preco)
    }, 0)
    document.querySelector('.coluna_total').innerHTML = numberFormatBR.format(total) // 1123.45

    acaoBotaoApagar()
}

// aula 14
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
}

~~~

## Considerações

> Estas ações de renomear, mudar a posição de trechos de códigos, reecrever, organizar ações dentro de funções, são tarefas frequentes na refatoração. Após testes e code reviews, é comum fazermos essas mudanças, para facilitar a leitura, entendimento do código, a manutenção e permitir a extensão ou aumento dele.

Salve Devs, até as próximas aulas.
