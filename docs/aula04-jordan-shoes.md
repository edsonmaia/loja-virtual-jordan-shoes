# Aula 04 - Jordan Shoes - HTML e CSS

## Responsividade

Ajuste o seguinte trecho de css do `.card__produto`

~~~css
.card__produto {
    width: 336px; /* era 384px */
    height: 326px;
    flex-basis: 336px;
}

~~~

Ajuste também a propriedade width do `.heading__produtos` defina como max-width
~~~css

.heading__produtos {
    max-width: 590px;
    height: 100%;
    margin-bottom: 72px;
}

~~~

> Mudamos a medida de referência de largura para 336px e adicionamos ela como flex-basis, tamanho base do nosso flex. Também ajustamos o width do .heading__produtos para max-width.
Em seguida aplique as formatações css de responsividade para os displays de 768px e 375px.


### Resolução de 768px e 375px

~~~css

/* Responsividade */
@media (max-width: 768px) {
    
    .top_fixed {
        height: 41px;
        font-size: 16px;
    }

    .hero {
        height: 350px;
    }

    .hero__content h1 {
        font-size: 18px;
    }

    .hero__content h2 {
        font-size: 24px;
    }

    .hero__content p {
        font-size: 18px;
        line-height: 28px;
    }

    .heading__produtos {
        padding-inline: 20px;
    }

    .heading__produtos h3 {
        font-size: 24px;
    }

    .heading__produtos p {
        font-size: 16px;
        line-height: 26px;
    }

    .lista__produtos {
        margin-block: 32px;
        gap: 32px;
    }

    .card__produto_detalhes h4 {
        font-size: 18px;
    }

    .card__produto_detalhes h5 {
        font-size: 16px;
    }

    .card__produto h6 {
        font-size: 20px;
    }

}

@media (max-width: 375px) {

    .top_fixed {
        height: 39px;
    }

    .hero__content p {
        font-size: 16px;
        line-height: 26px;
    }

    .heading__produtos h3 {
        font-size: 20px;
    }

    .heading__produtos p {
        font-size: 14px;
        line-height: 24px;
    }

    .lista__produtos {
        margin-block: 24px;
        gap: 24px;
    }

    .card__produto_detalhes h4 {
        font-size: 16px;
    }

}

~~~

Salve as alterações e veja o resultado no browser.

## Considerações

Nesta aula vimos como trabalhar a responsividade no nosso projeto para os displays de telas menores, como 768px e 375px, com base nas especificações do projeto no Figma. Na próxima aula já podemos fazer o deploy da nossa aplicação, aliás, já poderíamos ter feito ele.

Salve Devs, até as próximas!
