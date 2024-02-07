# Aula 11 - Jordan Shoes - Carrinho

> Vamos fazer nesta aula alguns ajustes na nossa aplicação, inicialmente vamos criar o header .topo que ficará acima do hero. Em seguida vamos ocultar o top_fixed

## Ajuste no HTML

1. Para funcionar os ícones do Material Icons do Google fonts, adicione a seguinte linha no head, acima da tag meta viewport:

~~~html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />
~~~

2. No body acima da section `.top_fixed` coloque o seguinte código do header:

~~~html
    <header class="topo">
        <div class="topo__marca">
            <a href="" class="link_home">
                <img src="images/icon_jordan.svg" alt="Logo Jordan">
                <h1>Jordan Shoes</h1>
            </a>
        </div>
        <div class="btn__carrinho">
            <span class="material-symbols-outlined icone">
                shopping_cart
            </span>
            <span class="numero_itens">0</span>
        </div>
    </header>

~~~

> Na section .top_fixed mude o display: flex; para display: none;

3. Aproveite que está no `index.html` e lá no final abaixo da section `.detalhes__produto` coloque os códigos da section `.carrinho`:

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

> Só depois percebi que não tinha colocado o th e td dentro das tags tr.

4. Salve as alterações.

## Ajustes no CSS

1. Para formatar o header `.topo`, abaixo do seletor `body` e acima do seletor `.top_fixed` coloque o seguinte código:

~~~css
/* topo */
.topo {
    position: fixed;
    top: 0;
    width: 100%;
    height: 50px;
    background-color: var(--white_soft);
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.topo__marca a {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 20px;
    text-decoration: none;
    color: var(--dark);
}

.topo__marca img {
    margin-right: 5px;
}

.topo__marca h1 {
    font-size: 24px;
}

.btn__carrinho {
    position: relative;
    display: inline-block;
}

.btn__carrinho span {
    margin-right: 10px;
    cursor: pointer;
}

.btn__carrinho .icone {
    font-size: 28px;
}

.btn__carrinho .icone:hover {
    filter: invert(0.5);
}

.btn__carrinho .numero_itens {
    position: absolute;
    top: -5px;
    right: -5px;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background-color: #f44336;
    color: #f1f1f1;
    font-size: 14px;
    text-align: center;
    line-height: 18px;
}

~~~

> No selector .hero adicione a linha: margin-top: 50px;
> Com isso você, irá deixar o espaço acima do hero para poder ser visualizado, já que o .topo tem position: fixed; e ele fica por cima de todos elementos.

2. Lá no final do arquivo css adicione os códigos de formatação da section `.carrinho`:

~~~css
/* carrinho */
.carrinho {
    display: none; /* block */
    padding-top: 30px;
    width: 100%;
    height: 100%;
    margin-block: 20px;
    padding-inline: 20px;
}

.carrinho h2 {
    margin-bottom: 10px;
}

table {
    width: 100%;
    border-collapse: collapse;
}

table tr, th, td {
    border: 1px solid #ccc;
    height: 40px;
}

table td {
    padding-inline: 10px;
}

.coluna_tamanho, .coluna_preco {
    text-align: right;
}

.coluna_apagar {
    width: 65px;
    text-align: center;
}

.coluna_apagar span:hover {
    cursor: pointer;
    color: red;
}

tfoot {
    text-align: right;
}

~~~

3. Salve as alterações.

## Para testar

1. No css do `.carrinho` mude o `display: none;` para `display: block;`
2. Salve as alterações e veja o resultado no navegador.

> Perceba que abaixo da section .produtos aparecerá a section .carrinho

3. Volte o display do `.carrinho` para `display: none;`
4. Salve as alterações e vamos controlar o fluxo de navegação.

## Controlar o fluxo de navegação

> Para controlar o fluxo de navegação temos que entender a lógica da nossa SPA.

1. A página `home` é formada pelo `.hero` e `.produtos`
2. A página `detalhes` é formada pelo `.hero` e `.detalhes__produto`, com o botão `Voltar`
3. A página `carrinho` é formada só pela section `.carrinho`
4. A `logo no header` serve para voltar para a página `Home`
5. O `ícone do carrinho` serve para exibir a página `carrinho`

> Temos que controlar o fluxo de exibição e ocultação de sections e botões para criar a navegação na nossa SPA.

## Controlar botão e link home

1. Abra o arquivo `script.js`
2. Nas primeiras linhas do script já tem const das sections Produtos e DetalhesProduto, crie a const da sectionHero na linha 4 do código:

`const sectionHero = document.querySelector('.hero')`

3. No final do script adicione as seguintes linhas de código:

~~~javascript
// aula 11
const btnCarrinho = document.querySelector('.btn__carrinho .icone')
const sectionCarrinho = document.querySelector('.carrinho')

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
    /* ajuste */
    ocultarBotaoEsecao()
})

~~~

2. Salve as alterações e teste.

## Ajuste para exibir o id do produto na página detalhes

1. No arquivo index.html

2. Dentro da div .detalhes da div .produto__detalhes_info adicione o span para exibir o id

~~~html
<div class="detalhes">
    <span>id</span>
    <h4>Nome do produto</h4>
    <h5>Descrição</h5>
    <h6>R$ preço</h6>
</div>

~~~

3. Salve as alterações.

4. No arquivo `script.js`

5. Na função `preencherDadosProduto`, adicione a linha:

`document.querySelector('.detalhes span').innerHTML = product.id // ajust a11`

~~~javascript
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
    document.querySelector('.detalhes h6').innerHTML = numberFormat.format(product.price)

}

~~~

> Com esta linha você irá prencher o span de .detalhes com o id do produto na página detalhes.

6. Salve as alterações e teste no navegador.

> Após clicar em um produto na lista, na página detalhes irá aparecer o id do produto selecionado.
Esta informação será usada para buscar produto por id, filtrar dados, etc.

## Considerações

Nesta aula vimos como criar o topo para nossa página, com link para home e botão para o carrinho de compras, criamos também a seção do carrinho, que representa a página dele, e controlamos o fluxo de navegação entre os elementos. Aproveitamos o tempo e fizemos a adição do id do produto na página detalhes, informação que é essencial para buscar dados do produtos selecionado, filtrar, etc.
Nas próximas aulas vamos trabalhar as funcionalidades de adição de produto no carrinho, pode parecer pouco, mas, temos muito trabalho a ser feito.

Salve Devs, até as próximas!
