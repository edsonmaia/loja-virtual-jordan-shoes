# Aula 07 - Jordan Shoes - Página de Detalhes do Produto

## SPA - Single Page Application

> Vamos criar a página de detalhes do produto utilizando o conceito de SPA, ou seja, tudo estará na página index.html, vamos utilizar o JS para exibir e ocultar o que deve ser apresentado ou não.

1. No arquivo `index.html`, uma linha abaixo da `section de produtos` crie o seguinte código:

~~~html
<section class="produto__detalhes">

    <div class="produto__detalhes_imagens">
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
        <figure>
            <img src="./images/air-jordan-1-mid-dutch-green-1-400.png" alt="" />
        </figure>
    </div>

    <div class="produto__detalhes_info">

        <div class="detalhes">
            <h4>Nome do produto</h4>
            <h5>Descrição</h5>
            <h6>R$ preço</h6>
        </div>

        <div class="tamanho">
            Tamanho
        </div>

        <div class="botao">
            <button type="button">Adicionar ao carrinho</button>
        </div>

        <div class="descricao">
            <p>Inspirado no AJ1 original, essa edição cano médio mantém o visual icônico que você ama, enquanto a escolha de cores e o couro conferem uma identidade distinta.</p>

            <p>Benefícios</p>
            
            <ul>
                <li>Cabedal em material genuíno, sintético e tecido para sensação de suporte.
                <li>Entressola de espuma e amortecimento Nike Air proporcionam conforto e leveza.
                <li>Solado de borracha com ponto de giro cria tração duradoura.
            </ul>
        </div>

        <details class="frete">

            <summary>Calcular frete e entrega</summary>

            <p>Calcule o frete e o prazo de entrega estimados para sua região.</p>

            <label for="">Insira o seu cep</label>
            <input type="text" placeholder="00000-000" />
            <button type="button">Calcular</button>

            <a href="">Não sei meu CEP</a>

        </details>

    </div>

</section>

~~~

2. Salve as alterações.
3. Abra o arquivo `style.css` e faça os seguintes ajustes e acréscimos:

~~~css

/* ajustes */
main {
    width: 100%;
    height: 100%;

    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column; /* ajuste */
}

/* reutilização de formatação */
.card__produto figure, .produto__detalhes_imagens figure {
    width: 100%;
    height: 200px;
    background-color: var(--white_soft);

    display: flex;
    align-items: center;
    justify-content: center;
}

/* continua */

.card__produto_detalhes h4, .detalhes h4 {
    font-size: 18px;
    line-height: 28px;
}

.card__produto_detalhes h5, .detalhes h5 {
    font-size: 16px;
    line-height: 26px;
    color: var(--brand_color);
}

/* preco */
.card__produto h6, .detalhes h6 {
    font-size: 18px;
    line-height: 28px;
    font-family: "Space Grotesk", sans-serif;
}

/* código css novo da aula para formatar detalhes do produto  */
/* aula 07 detalhes do produto */
.produto__detalhes {
    /* border: 1px solid red; */
    width: 100%;
    height: 100%;
    padding: 20px;
    
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 32px;
    justify-content: center;
}

.produto__detalhes_imagens {
    /* border: 1px solid green; */
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
}

.detalhes, .tamanho, .botao, .descricao {
    margin-bottom: 20px;
}

.botao {
    width: 100%;
}

.botao button {
    width: 100%;
    height: 50px;
    border-radius: 50px;
    background-color: var(--dark);
    color: var(--white);
    border: 0;
    cursor: pointer;
    font-size: 16px;
}

~~~

4. Salve as alterações e teste no navegador.

## Links utilizado nesta aula

> https://www.nike.com.br/tenis-air-jordan-1-mid-masculino-024331.html?cor=15

## Considerações

Nesta aula vimos como criar a página de detalhes do produto utilizando o conceito de SPA, fizemos também parte da formatação css, porém, ainda temos mais trabalho a ser feito nesta página e iremos concluir nas próximas aulas.

Salve Devs, até as próximas!
