# Aula 18 - Jordan Shoes - Identificação, Pagamento e Navegação

> Nesta aula vamos implementar as seções Identificação, Pagamento e prover os recursos para navegação entre as seções.

## Novas seções

1. No arquivo `index.html`, dentro da main, abaixo da section .carrinho adicione os seguintes códigos:

~~~html
<section class="identificacao">
    
    <h2>Identificação</h2>
    <p>* campos obrigatórios</p>

    <form class="form_identificacao">
        <div class="input">
            <label for="nome">Nome completo*</label>
            <input type="text" id="nome" class="input" required />
        </div>
        <div class="input">
            <label for="email">E-mail*</label>
            <input type="email" id="email" class="input" required />
        </div>
        <div class="input">
            <label for="tel">Telefone*</label>
            <input type="tel" id="tel" class="input" required />
        </div>
        <div class="input">
            <label for="cep1">CEP*</label>
            <input type="text" id="cep1" class="input" maxlength="9" placeholder="99999-999" required />
        </div>
        <div class="input">
            <label for="endereco">Endereco*</label>
            <input type="text" id="endereco" class="input" required />
        </div>
        <div class="input">
            <label for="numero">Número*</label>
            <input type="text" id="endereco" class="input" maxlength="10" required />
        </div>
        <div class="input">
            <label for="bairro">Bairro*</label>
            <input type="text" id="bairro" class="input" required />
        </div>
        <div class="input">
            <label for="complemento">Complemento</label>
            <input type="text" id="complemento" class="input" />
        </div>
        <div class="input">
            <label for="cidade">Cidade*</label>
            <input type="text" id="cidade" class="input" required />
        </div>
        <div class="input">
            <label for="estado">Estado*</label>
            <input type="text" id="estado" class="input" maxlength="2" required />
        </div>
        <div class="bloco">
            <input type="checkbox" id="concordo" class="checkbox" required />
            <label for="concordo">Concordo com a Política de Privacidade e os Termos de Uso.*</label>
        </div>
        <div class="botao">
            <button type="button" class="btn_finalizar_cadastro">Finalizar cadastro</button>
        </div>
    </form>
</section>

<section class="pagamento">
    <h2>Pagamento</h2>
    <p>* campos obrigatórios</p>
    
    <h3>Dados do cartão</h3>

    <form class="form_pagamento">
        <div class="input">
            <label for="numero_cartao">Número do cartão*</label>
            <input type="text" id="numero_cartao" class="input" maxlength="16" required />
        </div>
        <div class="input">
            <label for="nome_impresso">Nome impresso*</label>
            <input type="text" id="nome_impresso" class="input" required />
        </div>
        <div class="input">
            <label for="validade">Validade*</label>
            <input type="text" id="validade" class="input" maxlength="5" placeholder="MM/AA" required />
        </div>
        <div class="input">
            <label for="codigo_seguranca">Código de Seguranca*</label>
            <input type="text" id="codigo_seguranca" class="input" maxlength="3" placeholder="CVV" required />
        </div>
        <div class="input">
            <label for="numero_parcelas">Número de parcelas</label>
            <select id="numero_parcelas" required >
                <option value="1">À vista</option>
                <option value="2">2</option>
                <option value="3">3</option>
            </select>
        </div>
        <div class="bloco">
            <input type="checkbox" id="salvar_cartao" class="checkbox" />
            <label for="salvar_cartao">Salvar cartão para minhas próximas compras.*</label>
        </div>
        <div class="botao">
            <button type="button" class="btn_finalizar_compra">Finalizar compra</button>
        </div>
        <div class="bloco">
            <p>Ao finalizar a sua compra, você concorda com a nossa Política de trocas e devoluções.</p>
        </div>
    </form>
    
</section>

~~~

2. Salve as alterações e veja o resultado no navegador.

> Os códigos CSS para formatação dessas áreas foram colocados na aula anterior.

> Perceba que abaixo da listagem de produtos, agora estão aparecendo duas seções de identificação e de pagamento. Vamos utilizar o JS para controlar a exibição dessas seções.

## Controlar o fluxo de exibição das seções novas

~~~javascript
// aula 18
const sectionIdentificacao = document.querySelector('.identificacao')
const sectionPagamento = document.querySelector('.pagamento')

ocultarElemento(sectionIdentificacao)
ocultarElemento(sectionPagamento)

const btnContinuarCarrinho = document.querySelector('.btn_continuar')
btnContinuarCarrinho.addEventListener('click', () => {
    ocultarElemento(sectionCarrinho)
    mostrarElemento(sectionIdentificacao)

})

const btnFinalizarCadastro = document.querySelector('.btn_finalizar_cadastro')
btnFinalizarCadastro.addEventListener('click', () => {
    ocultarElemento(sectionIdentificacao)
    mostrarElemento(sectionPagamento)

})

const btnFinalizarCompra = document.querySelector('.btn_finalizar_compra')
btnFinalizarCompra.addEventListener('click', () => {
    ocultarElemento(sectionPagamento)
    mostrarElemento(sectionHero, 'flex')
    mostrarElemento(sectionProdutos, 'flex')

})

~~~

2. Salve as alterações, mas antes faça os seguintes ajustes

## Ajustes no btnCarrinho e btnHome

> Ocultar os elementos sectionIdentificacao e sectionPagamento

~~~javascript
const btnCarrinho = document.querySelector('.btn__carrinho .icone')
btnCarrinho.addEventListener('click', () => {
    mostrarElemento(sectionCarrinho)
    ocultarElemento(sectionHero)
    ocultarElemento(sectionProdutos)
    ocultarElemento(sectionDetalhesProduto)
    ocultarElemento(sectionIdentificacao)
    ocultarElemento(sectionPagamento)
})

const btnHome = document.querySelector('.link_home')
btnHome.addEventListener('click', (event) => {
    event.preventDefault()
    ocultarElemento(sectionCarrinho)
    mostrarElemento(sectionHero, 'flex')
    mostrarElemento(sectionProdutos, 'flex')
    ocultarVoltarEsecaoDetalhes()
    ocultarElemento(sectionIdentificacao)
    ocultarElemento(sectionPagamento)
})

~~~

3. Salve as alterações e teste no navegador.

## Considerações

> Esta aula vimos como criar as novas seções Identificação e Pagamento, e também como fazer os fluxos de navegação entre as seções a partir da continuação do carrinho. Nas próximas aulas vamos implementar mais funcionalidades dessa nossa aplicação.

Salve Devs, até as próximas!
