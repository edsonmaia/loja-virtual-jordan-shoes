# Aula 10 - Jordan Shoes - Refatoração

> Vamos fazer nesta aula alguns ajustes na nossa aplicação, preparando para as próximas aulas e outras funcionalidades.

## Ajuste no HTML

> Acrescente apenas as linhas de input e label dentro da tag div .tamanhos

~~~html
<div class="tamanho">
    <h5>Tamanho</h5>
    <div class="tamanhos">
        <!-- 38 até 51 -->
        <input class="radio" type="radio" name="size" id="size38" value="38">
        <label for="size38" class="numeros">38</label>
        
        <input class="radio" type="radio" name="size" id="size39" value="39">
        <label for="size39" class="numeros">39</label>
        
        <input class="radio" type="radio" name="size" id="size39p5" value="39,5">
        <label for="size39p5" class="numeros">39,5</label>
        
        <input class="radio" type="radio" name="size" id="size40" value="40">
        <label for="size40" class="numeros">40</label>
        
        <input class="radio" type="radio" name="size" id="size40p5" value="40,5">
        <label for="size40p5" class="numeros">40,5</label>

        <input class="radio" type="radio" name="size" id="size41" value="41">
        <label for="size41" class="numeros">41</label>

        <input class="radio" type="radio" name="size" id="size42" value="42">
        <label for="size42" class="numeros">42</label>

        <input class="radio" type="radio" name="size" id="size42p5" value="42,5">
        <label for="size42p5" class="numeros">42,5</label>

        <input class="radio" type="radio" name="size" id="size43" value="43">
        <label for="size43" class="numeros">43</label>

        <input class="radio" type="radio" name="size" id="size43p5" value="43,5">
        <label for="size43p5" class="numeros">43,5</label>

        <input class="radio" type="radio" name="size" id="size44" value="44">
        <label for="size44" class="numeros">44</label>

        <input class="radio" type="radio" name="size" id="size45" value="45">
        <label for="size45" class="numeros">45</label>

        <input class="radio" type="radio" name="size" id="size46" value="46">
        <label for="size46" class="numeros">46</label>

        <input class="radio" type="radio" name="size" id="size47" value="47">
        <label for="size47" class="numeros">47</label>

        <input class="radio" type="radio" name="size" id="size48" value="48">
        <label for="size48" class="numeros">48</label>

        <input class="radio" type="radio" name="size" id="size49" value="49">
        <label for="size49" class="numeros">49</label>

        <input class="radio" type="radio" name="size" id="size50" value="50">
        <label for="size50" class="numeros">50</label>

        <input class="radio" type="radio" name="size" id="size51" value="51">
        <label for="size51" class="numeros">51</label>
    </div>
</div>

~~~

Salve as alterações.

## Ajustes no CSS

> Adicione as propriedades no seletor .numeros e acrescente os seletores abaixo:

~~~css
.numeros {
    height: 40px;
    border: 1px solid #ccc;
    /* aula 10 */
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
}

/* aula 10 */
.numeros:hover {
    border-color: var(--dark);
    cursor: pointer;
}

.radio {
    display: none;
}

.selecionado {
    border-color: var(--dark);
}

~~~

> Salve as alterações e teste no browser, agora teremos na página de detalhes os tamanhos dos produtos. A programação de seleção deles será feita nas próximas aulas.

## Ajustes no JS

> Vamos ajustar a troca do ícone de details .frete e depois refatarar algumas funcionalidades

1. No final do código adicione:

~~~javascript
// mudar icone do details
const details = document.querySelector('details')

details.addEventListener('toggle', () => {
    const summary = details.querySelector('summary')
    summary.classList.toggle('icone-expandir')
    summary.classList.toggle('icone-recolher')
})

~~~

2. Encapsular as funcionalidades de ocultar botão voltar e seção detalhes, na parte de cima do script, coloque as duas linhas dentro de uma função e evoque ela em seguida:

~~~javascript
const ocultarBotaoEsecao = () => {
    botaoVoltar.style.display = 'none'
    sectionDetalhesProduto.style.display = 'none'
}

ocultarBotaoEsecao()

~~~

3. No escutador de eventosdo botão voltar, substitua as duas linhas pela chamada da função:

~~~javascript

botaoVoltar.addEventListener('click', () => {
    sectionProdutos.style.display = 'flex'
    ocultarBotaoEsecao()
})

~~~

4. Dentro da função generateCard, recorte as linhas finais que tratam do escutador de eventos em card, faça a chamada de uma função preencherCard(card, products):

~~~javascript
// continua o codigo
        const listaProdutos = document.querySelector('.lista__produtos')
        listaProdutos.appendChild(card)
        preencherCard(card, products)
    })
}

~~~

4.1.  Faça a definição da função lá no final do script:

~~~javascript
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

~~~

5. Salve as alterações e teste no navegador.

## Considerações

Nesta aula vimos como organizar melhor nosso código JS, fizemos algumas definições de funções para refatorar nosso código. Nas próximas aulas iremos resolver outros desafios desta nossa aplicação.

Salve Devs, até as próximas!
