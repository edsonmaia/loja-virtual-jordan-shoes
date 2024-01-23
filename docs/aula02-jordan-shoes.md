# Aula 02 - Jordan Shoes - CSS

## Refatorar o html para fazer o CSS

Precisamos organizar melhor o nosso html com tags semânticas e definição de classes para facilitar a formatação CSS.

Faça os seguintes ajustes no código:

1. Cole as linhas do link das fontes do Google Fonts, abaixo da tag meta charset:

~~~html
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600&family=Space+Grotesk:wght@400;500;600&display=swap" rel="stylesheet">
~~~

2. Dentro do body faça os ajustes definindo classes e organizando melhor os conteúdos dentro de outras tags semânticas:

~~~html
<section class="top_fixed">
        Frete grátis para todo o Brasil
    </section>

    <section class="hero">
        <div class="hero__content">
            <h1>
                <img src="images/logo-jordan.svg" alt="Logo Jordan">
                Jordan Shoes
            </h1>
    
            <h2>A melhor loja de Jordan</h2>
            <p>O tênis Jordan é fruto de uma velha e forte <br> parceria entre a Nike e o jogador Michael Jordan.</p>
        </div>
    </section>

    <main>
        <section class="produtos">

            <div class="heading__produtos">
                <h3>Os melhores em só lugar</h3>
                <p>A marca Jordan na JordanShoes é a escolha certa para os amantes de sneakers que buscam estilo e conforto.</p>
            </div>
    
            <section class="lista__produtos">

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

            </section>
    
        </section>
    </main>
~~~

# Código HTML completo

~~~html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600&family=Space+Grotesk:wght@400;500;600&display=swap" rel="stylesheet">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Jordan Shoes</title>
    <link rel="icon" href="images/favicon.png" />
    <link rel="stylesheet" href="css/style.css" />
</head>
<body>

    <section class="top_fixed">
        Frete grátis para todo o Brasil
    </section>

    <section class="hero">
        <div class="hero__content">
            <h1>
                <img src="images/logo-jordan.svg" alt="Logo Jordan">
                Jordan Shoes
            </h1>
    
            <h2>A melhor loja de Jordan</h2>
            <p>O tênis Jordan é fruto de uma velha e forte <br> parceria entre a Nike e o jogador Michael Jordan.</p>
        </div>
    </section>

    <main>
        <section class="produtos">

            <div class="heading__produtos">
                <h3>Os melhores em só lugar</h3>
                <p>A marca Jordan na JordanShoes é a escolha certa para os amantes de sneakers que buscam estilo e conforto.</p>
            </div>
    
            <section class="lista__produtos">

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

                <div class="card__produto">

                    <figure>
                        <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                    </figure>

                    <div class="card__produto_detalhes">
                        <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                        <h5>Tênis Air Jordan</h5>
                    </div>

                    <h6>R$ 1.049,00</h6>

                </div>

            </section>
    
        </section>
    </main>
    
    <script src="js/script.js"></script>
</body>
</html>

~~~

## CSS do projeto

1. No arquivo CSS adicione o seletor :root com as cores do projeto, acima do seletor *
2. Abaixo do seletor * faça as formatações do body e das classes do projeto
3. Veja o código CSS completo abaixo:

~~~css

:root {
    --brand_color: #7CA2F4;
    --dark: #121214;
    --white_soft: #F3F7FF;
    --white: #FFFFFF;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    width: 100%;
    height: 100%;
    font-family: Archivo, sans-serif;
}

.top_fixed {
    width: 100%;
    height: 64px;
    background-color: var(--white_soft);
    font-weight: 500;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px; /* ajuste */
}

.hero {
    width: 100%;
    height: 400px;
    background-image: url('../images/image-michael-jordan.png');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center bottom;

    display: flex;
    align-items: center;
    justify-content: center;
}

.hero__content {
    width: 80%;
    height: auto;
    color: var(--white);

}

.hero__content h1, .hero__content p {
    font-size: 24px;
    margin-bottom: 20px;
}

.hero__content h2 {
    font-size: 32px;
    margin-bottom: 20px;
}

.hero__content p {
    line-height: 34px;
}

main {
    width: 100%;
    height: 100%;

    display: flex;
    align-items: center;
    justify-content: center;

}

.produtos {
    width: 100%;
    height: 100%;
    margin-block: 80px;

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

}

.heading__produtos {
    width: 590px;
    height: 100%;
    margin-bottom: 72px;
}

.heading__produtos h3 {
    text-align: center;
    font-size: 32px;
    margin-bottom: 20px;
}

.heading__produtos p {
    font-size: 24px;
}

.lista__produtos {
    width: 100%;
    height: 100%;

    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 32px;

}

.card__produto {
    width: 384px;
    height: 326px;

}

.card__produto figure {
    width: 100%;
    height: 200px;
    background-color: var(--white_soft);

    display: flex;
    align-items: center;
    justify-content: center;
}

.card__produto_detalhes {
    margin-block: 24px;

}

.card__produto_detalhes h4 {
    font-size: 18px;
    line-height: 28px;
}

.card__produto_detalhes h5 {
    font-size: 16px;
    line-height: 26px;
    color: var(--brand_color);
}

/* preco */
.card__produto h6 {
    font-size: 20px; /* estava 18  */
    line-height: 30px; /* estava 28 */
    font-family: "Space Grotesk", sans-serif;
}

~~~

4. Salve as alterações e teste no navegador.

## Considerações

Nesta aula vimos como fazer a organização do código html para trabalhar o css de forma semântica.
Na próxima aula vamos trabalhar o código js para automatizar a geração dos cards.

Salve Devs, até as próximas!
