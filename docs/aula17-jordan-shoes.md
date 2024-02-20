# Aula 17 - Jordan Shoes - Módulos JS + Detalhes do Carrinho

> Nesta aula vamos implementar a modularização da nossa aplicação e a exibição dos detalhes do carrinho.

## Modularizar

1. No arquivo `script.js`, selecione as funções `numberFormatBR` e `limparFormatoReal`, recorte (CTRL + X)

2. Na pasta `js` crie um novo arquivo `utils.js`

3. Dentro do arquivo `utils.js` cole (CTRL + V) o código das funções:

~~~javascript
// Formatar numeros para formato monetario brasileiro e exibir o simbolo R$
export const numberFormatBR = new Intl.NumberFormat('pt-BR', {
    style: 'currency',
    currency: 'BRL',
    minimumFractionDigits: 2,
    maximumFractionDigits: 2,
})

export const limparFormatoReal = (valor) => {
    return parseFloat(valor.replace('R$&nbsp;', '').replace('.', '').replace(',', '.'))
}

~~~

> Use a palavra reservada export antes da definição de cada função

4. Salve as alterações e feche o arquivo `utils.js`.

## Ajuste no HTML

1. No arquivo `index.html` na parte de baixo, onde está a tag script faça os ajuste e deixe o código da seguinte forma:

~~~html
<script src="js/utils.js" type="module"></script>
<script src="js/script.js" type="module"></script>
~~~

> Na tag de abertura adicione a propriedade type="module". E faça o import do arquivo utils.js

2. Salve as alterações.


## Como usar as funções do arquivo utils

1. Na parte de cima, na 1ª linha de código do script.js vamos fazer o import das funções:

~~~javascript
    import { numberFormatBR, limparFormatoReal } from './utils.js'
~~~

2. Salve as alterações e teste no navegador.

> Só podemos usar o import e export, recurso de Módulos do ES6 em diante, se declararmos lá na tag script que o nosso script é do tipo "module"

## Exibir detalhes do carrinho

> Agora para exibir detalhes do carrinho vamos fazer dois ajustes no nosso projeto, um no html e outro no css

1. No arquivo `index.html` dentro da `section .carrinho`, abaixo da table adicione as seguintes linhas de código:

~~~html
<!-- DETALHES DO CARRINHO -->
<div class="carrinho__detalhes">
    <div class="frete">
        <label for="cep2">Prazo de entrega</label>
        <div class="input">
            <input type="text" id="cep2" placeholder="00000-000" />
            <button type="button" class="btn_calcular">Calcular</button>
        </div>
        <p>Tempo previsto para entrega</p>
        <a href="https://buscacepinter.correios.com.br/app/endereco/index.php" target="_blank" rel="noopener noreferrer">Não sei meu CEP</a>
    </div>
    <div class="cupom_desconto">
        <label for="cupom">Cupom de Desconto</label>
        <div class="input">
            <input type="text" id="cupom" />
            <button type="button" class="btn_aplicar">Aplicar</button>
        </div>
        <span class="desconto_cupom"></span>
    </div>
    <div class="resumo">
        <h3>Resumo</h3>
        <ul>
            <li>
                <span>Valor dos produtos</span>
                <span class="sub_total"></span>
            </li>
            <li>
                <span>Frete</span>
                <span class="valor_frete"></span>
            </li>
            <li>
                <span>Desconto</span>
                <span class="valor_desconto"></span>
            </li>
            <li>
                <span>Total da compra</span>
                <span class="total_compra"></span>
            </li>
        </ul>
        <button type="button" class="btn_continuar">Continuar</button>
    </div>
</div>
~~~

> Este código html é dos detalhes do carrinho.

2. Salve as alterações.

3. No arquivo `style.css`, na parte final, adicione as seguintes linhas de código:

~~~css
/* DETALHES DO CARRINHO */
.carrinho__detalhes {
    width: 100%;
    margin-block: 20px;
    display: flex;
    justify-content: space-between;
}

.carrinho__detalhes label, .carrinho__detalhes h3 {
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 10px;
}

/* .carrinho__detalhes .frete */
.carrinho__detalhes .frete p {
    margin-bottom: 10px;
}

/* .carrinho__detalhes .cupom_desconto */
.cupom_desconto input {
    min-width: 320px;
}

/* .carrinho__detalhes .resumo */
.carrinho__detalhes .resumo {
    min-width: 300px;
    display: flex;
    flex-direction: column;
}

.resumo ul {
    margin-bottom: 20px;
}

.resumo li {
    font-size: 16px;
    line-height: 48px;
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #ccc;
}

.resumo li:first-child {
    border-top: 1px solid #ccc;
}

@media (max-width: 1024px) {
    .carrinho__detalhes {
        flex-direction: column;
        gap: 20px;
    }
    .carrinho__detalhes label, .carrinho__detalhes h3 {
        font-size: 18px;
    }
    .carrinho__detalhes p {
        font-size: 14px;
    }
}

.identificacao, .pagamento {
    margin-top: 50px;
    padding-inline: 20px;
    width: 100%;
}

.identificacao h2, .pagamento h2 {
    text-align: center;
}

~~~

> Mais um ajuste no CSS, para a formatação de campos de formulário, procure o seletor .input input e faça os seguintes ajustes e adições de código CSS:

~~~css
.input input, .input select {
    width: 100%;
    height: 50px;
    border-radius: 50px;
    border: 1px solid #ccc;
    font-size: 20px;
    padding-left: 20px;
}

.bloco {
    width: 100%;
    margin-block: 20px;
}

.input .checkbox {
    width: 20px;
}

.input select {
    background-image: url('../images/icon_expand_more.svg');
    background-repeat: no-repeat;
    background-position: right 20px center;
    background-size: 25px;
    padding-right: 20px;
    -webkit-appearance: none;
    -moz-appearance: none;
    -o-apparence: none;
    appearance: none;
}

~~~

4. Salve as alterações e feche o arquivo `style.css`.

5. Agora que já fizemos as adições do html e css de detalhes do carrinho, veja no navegador, após clicar no botão Carrinho, que abaixo da tabela, teremos 3 áreas de frete, cupom de desconto e resumo da compra.

> Nesta aula, vamos ver como fazer o preenchimento dos dados do resumo da compra.

## Preencher dados do resumo da compra no carrinho

1. No arquivo `script.js`, lá no final adicione as seguintes linhas de código:

~~~javascript
// aula 17
let valorFrete = 0
let valorDesconto = 0

const spanSubTotal = document.querySelector('.sub_total')
const spanFrete = document.querySelector('.valor_frete')
const spanDesconto = document.querySelector('.valor_desconto')
const spanTotalCompra = document.querySelector('.total_compra')

spanFrete.innerHTML = numberFormatBR.format(valorFrete)
spanDesconto.innerHTML = numberFormatBR.format(valorDesconto)

~~~

2. Para exibir o total do carrinho (subtotal) no resumo e calcular o total das compras, dentro da função `atualizarCarrinho`, após a linha `colunaTotal.innerHTML = numberFormatBR.format(total)`, adicione as seguintes linhas:

~~~javascript
// aula 17
spanSubTotal.innerHTML = numberFormatBR.format(total)
spanTotalCompra.innerHTML = numberFormatBR.format(total + valorFrete - valorDesconto)

~~~

3. Salve as alterações e teste no navegador.

## Considerações

> Esta aula vimos como trabalhar com módulos em JS e em seguinda como implementar a funcionalidade de detalhes do carrinho, com adição dos código html, css e js. Nas próximas aulas vamos implementar mais funcionalidades dessa nossa aplicação.

Salve Devs, até as próximas!
