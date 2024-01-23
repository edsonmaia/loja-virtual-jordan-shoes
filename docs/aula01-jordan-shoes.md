# Aula 01 - Jordan Shoes - HTML

## Criar o projeto web

1. Dentro de uma unidade C: ou D: crie a pasta `jordan-shoes`
2. Clique na pasta jordan-shoes com o botão direito e escolha `Abrir com Code`
3. Dentro da pasta raiz do projeto crie as pastas `css`, `images` e `js`
4. Na raiz do projeto crie o arquivo `index.html`
5. Faça os seguinte código:

~~~html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Jordan Shoes</title>
    <link rel="icon" href="images/favicon.png" />
    <link rel="stylesheet" href="css/style.css" />
</head>
<body>

    <section>
        Frete grátis para todo o Brasil
    </section>

    <section>
        <span>
            <img src="images/logo-jordan.svg" alt="Logo Jordan">
            Jordan Shoes
        </span>

        <h2>A melhor loja de Jordan</h2>
        <p>O tênis Jordan é fruto de uma velha e forte parceria entre a Nike e o jogador Michael Jordan.</p>
    </section>

    <section>
        <h3>Os melhores em só lugar</h3>
        <p>A marca Jordan na JordanShoes é a escolha certa para os amantes de sneakers que buscam estilo e conforto.</p>

        <section>
            <div>
                <img src="images/air-jordan-1-high-zoom-cmft-tropical-twist-1-400.png" alt="Tênis" />
                <h4>Air Jordan 1 High Zoom CMFT Tropical Twist</h4>
                <h5>Tênis Air Jordan</h5>
                <h6>R$ 1.049,00</h6>
            </div>
        </section>

    </section>
    
    <script src="js/script.js"></script>
</body>
</html>

~~~

## CSS inicial

1. Dentro da pasta `css` crie o arquivo `style.css`
2. Faça o seguinte código:

~~~css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

~~~

3. Salve as alterações e feche o arquivo.

## JS inicial

1. Dentro da pasta `js` crie o arquivo `script.js`
2. Faça o seguinte código:

~~~javascript
console.log('Jordan Shoes')

~~~

3. Salve as alterações e feche o arquivo.

## Copiar as images para a pasta images

1. Baixe o arquivo zip com as imagens

[ZIP das imagens](https://drive.google.com/file/d/17yl5V9cJGOtKoGsQOiAX_dQ4KjlWQHpy/view?usp=sharing)

2. Extrai os arquivos do zip
3. Copie e cole eles para dentro da pasta `images` do seu projeto

## Abrir a página no browser

1. Na bairra de status do VSCode, na parte inferior direita
2. Clique na opção Open Live Server
3. Ele irá abrir a sua página web no navegador.

## Considerações

Nesta aula vimos detalhes sobre o Projeto, Figma do Projeto e fizemos a estrutura básica dele, com os 3 arquivos essenciais. Na próxima aula vamos fazer as formatações CSS.

Salve Devs, até as próximas!
