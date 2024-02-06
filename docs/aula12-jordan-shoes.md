# Aula 12 - Jordan Shoes - Adicionar ao Carrinho

> Vamos fazer nesta aula um ajuste e as ações para adicionar o produto ao carrinho.

## Ajuste no btnHome

> Na aula anterior eu fiz a ocultação da sectionDetalhesProduto, porém, esqueci de ocultar o botaoVoltar, para fazer isso, já temos uma função chamada ocultarBotaoEsecao()

1. No escutador de eventos de btnHome faça o seguinte ajuste:

~~~javascript
const btnHome = document.querySelector('.link_home')
btnHome.addEventListener('click', (event) => {
    event.preventDefault()
    sectionCarrinho.style.display = 'none'
    sectionHero.style.display = 'flex'
    sectionProdutos.style.display = 'flex'
    ocultarBotaoEsecao() // ajuste aula 12
})

~~~

## Adicionar produto ao carrinho

1. No final do arquivo `script.js` adicione o seguinte código:

~~~javascript
// aula 12
// controlar seleção dos inputs radio
const radios = document.querySelectorAll('input[type="radio"]')
radios.forEach(radio => {
  radio.addEventListener('change', () => {
    const label = document.querySelector(`label[for="${radio.id}"]`)
    label.classList.add('selecionado')
    console.log(label)
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

const cart = []

const btnAddCarrinho = document.querySelector('.btn__add_cart')
btnAddCarrinho.addEventListener('click', () => {
    // pegar dados do produto adicionado
    const produto = {
        id: document.querySelector('.detalhes span').innerHTML,
        nome: document.querySelector('.detalhes h4').innerHTML,
        modelo: document.querySelector('.detalhes h5').innerHTML,
        preco: document.querySelector('.detalhes h6').innerHTML,
        tamanho: document.querySelector('input[type="radio"][name="size"]:checked').value
    }
    console.log(produto)
    cart.push(produto) // adicionar o produto ao array cart -> carrinho
    console.log(cart)
    // ocultar botao voltar, secao detalhes_produto e hero, e exibir a secao carrinho
    ocultarBotaoEsecao()
    sectionHero.style.display = 'none'
    sectionCarrinho.style.display = 'block'
})

~~~

2. Salve as alterações e teste.

## Faça os testes

1. No navegador, abra as ferramentas de desenvolvedor 'F12'

2. Acesse um produto, escolha o tamanho, depois clique no botão Adicionar ao carrinho

3. No console irá aparecer o produto adicionado e o array do carrinho.

> Agora falta fazer a exibição dos produtos que estão no array cart, lá na section carrinho, que é a página do nosso carrinho. Mas, isto vamos fazer na próxima aula.

Salve Devs, até as próximas!
