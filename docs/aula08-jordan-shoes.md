# Aula 08 - Jordan Shoes - Navegação entre páginas SPA

> Vamos aprender como fazer a navegação entre páginas de uma aplicação que utiliza os conceitos de SPA - Single Page Application.

## Ajustes na Página HTML

1. Abra o arquivo `index.html`
2. Dentro da `main` abaixo da `section .produtos` crie a div para o botão Voltar:

~~~html
<div class="voltar">Voltar</div>
~~~

3. Na parte do código da `div .tamanho` ajuste o conteúdo interno:

~~~html
<div class="tamanho">
    <h5>Tamanho</h5>
    <div class="tamanhos">
        38 até 51
    </div>
</div>
~~~

4. Na parte de `details .frete` faça os seguintes ajustes:
4.1 Defina a class `icone-expandir` para summary
4.2 Crie a `div .input` para envolver o `input` e o `button`
4.3 Atualize `href` do link, defina o `target` e `rel`

~~~html
<details class="frete">

    <summary class="icone-expandir">Calcular frete e entrega</summary>

    <p>Calcule o frete e o prazo de entrega estimados para sua região.</p>

    <label for="">Insira o seu cep</label>
    <div class="input">
        <input type="text" placeholder="00000-000" />
        <button type="button">Calcular</button>
    </div>

    <a href="https://buscacepinter.correios.com.br/app/endereco/index.php" target="_blank" rel="noopener noreferrer">Não sei meu CEP</a>

</details>
~~~

5. Salve as alterações.

> Para indicar que os nossos cards são elementos clicáveis que irão ser usados para abrir a página de detalhes, faça os ajustes no css e depois vamos fazer os códigos javascript.

## Ajustes no código CSS

1. Abra o arquivo `style.css`
2. Abaixo do seletor `.card__produto` adicione o seguinte código:

~~~css
/* aula 08 */
.card__produto figure:hover {
    border: 1px solid var(--brand_color);
    cursor: pointer;
}

~~~

3. Agora lá no final do código css faça a adição dos seguintes códigos:

~~~css
/* aula 08 */

/* detalhes do produto - nome, descricao e preco */
.detalhes {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.detalhes h4 {
    font-size: 24px;
}

.detalhes h5 {
    font-size: 16px;
    color: var(--brand_color);
}

.detalhes h6 {
    font-size: 24px;
    font-family: "Space Grotesk", sans-serif;
}

/* tamanho */
.tamanho h5 {
    font-size: 18px;
    margin-bottom: 10px;
}

.tamanhos {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
}

.numeros {
    height: 40px;
    border: 1px solid #ccc;
}

/* descricao - texto descrito */
.descricao {
    font-size: 16px;
    line-height: 26px;
    font-weight: 400;
}

.descricao p {
    margin-bottom: 10px;
}

.descricao ul {
    margin-left: 20px;
}

/* frete */
details::marker,
summary::marker {
  content: "";
}

summary {
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    height: 24px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
}

.icone-expandir::after,
.icone-recolher::after {
    content: "";
    display: inline-flex;
    width: 16px;
    height: 16px;
    background-image: url('../images/icon_expand_more.svg');
    background-size: contain;
    background-repeat: no-repeat;
    margin-left: 5px;
}

.icone-recolher::after {
    background-image: url('../images/icon_expand_less.svg');
}

details {
    font-size: 16px;
}

details p {
    margin-bottom: 15px;
}

label {
    margin-bottom: 5px;
}

.input {
    margin-block: 10px;
    display: flex;
    flex-direction: column;
    position: relative;
}

.input input {
    width: 100%;
    height: 50px;
    border-radius: 50px;
    border: 1px solid #ccc;
    font-size: 20px;
    padding-left: 20px;
}

.input button {
    font-size: 16px;
    font-weight: 500;
    width: 120px;
    height: 40px;
    background-color: var(--white);
    border-radius: 50px;
    border: 1px solid #ccc;
    font-size: 20px;
    cursor: pointer;
    position: absolute;
    bottom: 5px;
    right: 0px;
    margin-right: 5px;
}

.input button:hover {
    border-color: #222;
}

details a {
    color: var(--dark);
    font-weight: bold;
    margin-top: 20px;
}

.voltar {
    margin-top: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 10px;
}

.voltar:hover {
    cursor: pointer;
    border: 1px solid var(--brand_color);
}

~~~

4. Salve as alterações, antes de testar, copie os arquivos de ícones para a sua pasta images:

> Link dos ícones: https://drive.google.com/file/d/1DOGr4AXvVVlE1Qp6xenz9-clfii0R5lP/view?usp=sharing

5. Salve as alterações e teste no navegador.

> Nesta aula vamos fazer os códigos javascript para criar a navegação entre telas, ou seja, entre a página inicial que tem a lista dos cards de produtos e quando clicarmos em um card vamos exibir a página de detalhes do produto, porém, esconder a página de cards, mostrar o botão voltar e a página de detalhes.

> Quando clicarmos no botão voltar, precisamos mostrar os cards da página inicial, esconder o botão voltar e a página de detalhes.

## Ajustes em script.js

1. Abra o arquivo `script.js`
2. Nas primeiras linhas do script acrescente os seguintes códigos:

~~~javascript
const botaoVoltar = document.querySelector('.voltar')
const sectionDetalhesProduto = document.querySelector('.produto__detalhes')
const sectionProdutos = document.querySelector('.produtos')
// ocultar botao voltar e secao de detalhos do produto
botaoVoltar.style.display = 'none'
sectionDetalhesProduto.style.display = 'none'

~~~

3. Dentro da função `generateCard`, após a linha do appendChild adicione os códigos do escutador de eventos para o clique no card:

~~~javascript
card.addEventListener('click', () => {
    sectionProdutos.style.display = 'none'
    // mostrar o botão e página de detalhes do produto
    botaoVoltar.style.display = 'block'
    sectionDetalhesProduto.style.display = 'grid'

})

~~~

4. Após a linha da evocação da função generateCard() faça o escutador de eventos para o botão Voltar:

~~~javascript

botaoVoltar.addEventListener('click', () => {
    sectionProdutos.style.display = 'flex'
    botaoVoltar.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
})

~~~

5. Salve as alterações e teste no navegador.

## Links utilizado nesta aula

> https://fonts.google.com/icons?selected=Material+Symbols+Outlined:expand_more:FILL@0;wght@400;GRAD@0;opsz@24&icon.query=down

## Considerações

Nesta aula vimos como criar a navegação entre as páginas index que tem os cards e a página de detalhes do produto utilizando o conceito de SPA, vimos também parte da formatação css, porém, ainda temos mais trabalho a ser feito, iremos concluir nas próximas aulas.

Salve Devs, até as próximas!
