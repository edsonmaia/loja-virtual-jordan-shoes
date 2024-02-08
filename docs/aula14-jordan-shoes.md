# Aula 14 - Jordan Shoes - Exibir Total e Apagar itens do carrinho

> Nesta aula vamos implementar duas funcionalidades de atualização do carrinho, e fazer ajustes no nosso projeto.

## Calcular e exibir total do carrinho

1. Dentro da função `AtualizarCarrinho` no final dela, após o map adicione as seguintes linhas:

~~~javascript
// aula 14 - R$&nbsp;1.123,45 -> 1123.45
const total = cart.reduce( (valorAcumulado, item) => {
    return valorAcumulado + parseFloat(item.preco.replace('R$&nbsp;', '').replace('.', '').replace(',', '.'))
}, 0)
document.querySelector('.coluna_total').innerHTML = numberFormat.format(total) // 1123.45

~~~

> A const total irá armazenar a somatória ou subtotal dos preços dos produtos que estão no carrinho.

> Como preco que vem do nosso objeto produto que é adicionado ao nosso array cart está formatado para o padrão brasileiro, ele vem no formato de textos, por exemplo `R$&nbsp;1.123,45`
> Por isto, temos que usar o replace para tirar os textos, tirar o ponto (sepador de milhares) e por fim, substituir a vírgula por ponto, para deixar o preco no formato internacional.
> Temos que fazer o parseFloat para que o número seja convertido para um formato numérico com casas decimais.
> Depois, selecionamos a .coluna_total e colocamos dentro dela o total que recebemos, porém, a gente vai usar a função numberFormat.format(valorAserFormatado) para formatar o número do total.

2. Salve as alterações e teste no navegador.

3. Escolha um produto, escolha o tamanho, adicione ao carrinho, veja como irá aparecer o valor total. Se você adicionar mais itens, ele irá somar.

## Apagar itens do carrinho

1. Dentro da função `AtualizarCarrinho` no final dela, após as ações para calcular e exibir o total adicione a seguinte linha:

~~~javascript

acaoBotaoApagar()

~~~

> Esta é uma chamada para a função acaoBotaoApagar que iremos implementar no final do script.

2. Use CTRL + END, lá no final adicione as seguintes linhas de código:

~~~javascript
// aula 14
const acaoBotaoApagar = () => {
    const botaoApagar = document.querySelectorAll('.coluna_apagar span')
    botaoApagar.forEach( botao => {
        botao.addEventListener('click', () => {
            console.log('Apagar')
            const id = botao.getAttribute('data-id')
            console.log(id)
            const posicao = cart.findIndex( item => item.id == id )
            cart.splice(posicao, 1)
            atualizarCarrinho(cart)
        })        
    })
    atualizarNumeroItens()
}

~~~

> Vamos selecionar todos botões Apagar, usar um forEach para iterar nosso node list, que o resultado do querySelectorAll, e colocar um escutador de eventos de click para cada botão Apagar, as ações serão, pegar o id da linha, do produto clicado, usar esse id para pegar a posição do produto no array carrinho, depois usar o splice para apagar o produto no array usando a posição dele, e por fim atualizarCarrinho passando o cart atualizado e atualizarNumeroItens para exibir o número de itens atual.

3. Salve as alterações e teste no navegador.

4. Adicione um item, dois itens, depois clique no botão Apagar.

> Perceba que está funcionando perfeitamente a nossa função que definiu as ações necessárias para apagar item do array, e fazer as atualizações visuais na tabela e no botão do carrinho que mostra o número de itens.

## EXTRA 1 - Ajuste para não mostrar o span com o id do produto na página detalhes

1. No final do nosso código adicione as seguintes linhas:

~~~javascript
// selecionar o span do id e ocultar ele
const spanId = document.querySelector('.detalhes span')
spanId.style.display = 'none'

~~~

> Só estávamos deixando esse id visível para que pudéssemos ver o número do id durante os testes.

2. Salve as alterações.

## EXTRA 2 - Ajuste para não mostrar o span com o número de itens se o carrinho estiver vazio

1. Acima da função acaoBotaoApagar, na aula 13 fizemos a seleção do span numeroItens e definimos uma função para atualizarNumeroItens, vamos refatorar esse trecho de códigos, deixe da seguinte forma:

~~~javascript
// aula 13 e 14
const numeroItens = document.querySelector('.numero_itens')
numeroItens.style.display = 'none' // ocultar o numero_itens

const atualizarNumeroItens = () => {
    (cart.length > 0) ? numeroItens.style.display = 'block' : numeroItens.style.display = 'none'
    numeroItens.innerHTML = cart.length
}

~~~

> Adicionamos um display none para numeroItens, com isso o estado inicial dele, será não mostrar, porque inicialmente o carrinho está vazio.
> Dentro da função atualizarNumeroItens adicionamos uma condição ternária para ver o número de itens no carrinho, se for maior que zero, então, tem 1 ou mais, com isso, mudamos o display para block, senão, display none.

2. Salve as alterações e teste no navegador.

3. Veja que inicialmente o ícone do carrinho não tem a `bola vermelha` com o número de itens, mas, se você adicionar um ou mais itens, irá aparecer, e se você excluir, ao ponto de zerar, ela irá sumir.

> Enfim, conseguimos melhorar a experiência do usuário com a nossa interface, o famoso trabalho de UI/UX.

## Considerações

> Na próxima aula vamos implementar as funcionalidades outras funcionalidades para a nossa aplicação, e fazer qualquer ajustes que seja necessário.

Salve Devs, até as próximas!
