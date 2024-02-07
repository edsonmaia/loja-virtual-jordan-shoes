# Aula 13 - Jordan Shoes - Atualizar Carrinho

> Nesta aula vamos implementar duas funcionalidades de atualização do carrinho, e fazer ajustes no nosso projeto.

## Atualizar Carrinho

1. Dentro do escutador de eventos do botão Adicionar ao carrinho no final dele, adicione as seguintes linhas:

~~~javascript
    atualizarCarrinho(cart)
    atualizarNumeroItens()
~~~

2. No final do código js, fora do escutador de eventos implemente as duas funções:

> Antes crie as constantes para selecionar o corpo da tabela onde serão adicionadas as linhas de cada produto do carrinho e selecione também o span numero_itens para colocar o número de itens do carrinho

~~~javascript
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
}

const numeroItens = document.querySelector('.numero_itens')
const atualizarNumeroItens = () => {
    numeroItens.innerHTML = cart.length
}

~~~

3. Salve as alterações e teste no navegador.

> Veja que ao adicionar um novo item no carrinho, além de criarmos uma linha e exibir na section carrinho, também mostramos o número 1 no span do botão carrinho que fica na header do topo.

## Ajuste no HTML

> Durante a edição do vídeo, percebi um erro semântico na nossa tabela no arquivo index.html. As células - th, td - não estavam dentro de tags tr.

1. Ajuste o código da `table` dentro da `section .carrinho` para ficar conforme o trecho abaixo:

~~~html
<section class="carrinho">
    <h2>Carrinho</h2>
    <table>
        <thead>
            <tr>
                <th>id</th>
                <th>Produto</th>
                <th>Tamanho</th>
                <th>Preço</th>
                <th class="coluna_apagar">Apagar</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>-</td>
                <td>-</td>
                <td>-</td>
                <td>-</td>
                <td class="coluna_apagar">-</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3"><strong>TOTAL</strong></td>
                <td class="coluna_total">-</td>
                <td></td>
            </tr>
        </tfoot>
    </table>
</section>

~~~

> Adicionamos tr, e dentro delas colocamos as tags th e td, de cada thread, tbody e tfoot

2. Salve as alterações.

## Considerações

> Na próxima aula vamos implementar as funcionalidades para apagar itens do carrinho e exibir total do carrinho. E fazer ajustes se for necessário.

Salve Devs, até as próximas!
