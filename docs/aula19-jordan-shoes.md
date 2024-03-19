# Aula 19 - Jordan Shoes - Processar Formulário

> Nesta aula vamos implementar as seções Identificação, Pagamento e prover os recursos para navegação entre as seções.

## Seção identificao com o form_identificacao

1. No arquivo `index.html`, dentro da main, abaixo da section .carrinho adicione os seguintes códigos:

~~~html
<section class="identificacao">
    
    <h2>Identificação</h2>
    <p>* campos obrigatórios</p>

    <form class="form_identificacao">
        <div class="input">
            <label for="nome">Nome completo*</label>
            <input type="text" id="nome" class="" required />
        </div>
        <div class="input">
            <label for="email">E-mail*</label>
            <input type="email" id="email" class="" required />
        </div>
        <div class="input">
            <label for="tel">Telefone*</label>
            <input type="tel" id="tel" class="" required />
        </div>
        <div class="input">
            <label for="cep1">CEP*</label>
            <input type="text" id="cep1" class="" required />
        </div>
        <div class="input">
            <label for="endereco">Endereco*</label>
            <input type="text" id="endereco" class="" required />
        </div>
        <div class="input">
            <label for="numero">Número*</label>
            <input type="text" id="numero" class="" required />
        </div>
        <div class="input">
            <label for="bairro">Bairro*</label>
            <input type="text" id="bairro" class="" required />
        </div>
        <div class="input">
            <label for="complemento">Complemento</label>
            <input type="text" id="complemento" class="" />
        </div>
        <div class="input">
            <label for="cidade">Cidade*</label>
            <input type="text" id="cidade" class="" required />
        </div>
        <div class="input">
            <label for="estado">Estado*</label>
            <input type="text" id="estado" class="" required />
        </div>
        <div class="bloco">
            <input type="checkbox" id="concordo" class="checkbox" value="sim" required />
            <label for="concordo">Concordo com a Política de Privacidade e os Termos de Uso.*</label>
        </div>
        <div class="botao">
            <button type="submit" class="btn_finalizar_cadastro">Finalizar cadastro</button>
        </div>
    </form>
</section>

~~~

2. Salve as alterações e veja o resultado no navegador.

## Como processar dos dados do formulário

1. No escutador de eventos do btnFinalizarCadastro faça os seguintes códigos:

~~~javascript

const btnFinalizarCadastro = document.querySelector('.btn_finalizar_cadastro')
btnFinalizarCadastro.addEventListener('click', (event) => {
    // ocultarElemento(sectionIdentificacao)
    // mostrarElemento(sectionPagamento)
    event.preventDefault()
    
    const nome = document.querySelector('#nome').value
    const email = document.querySelector('#email').value
    const telefone = document.querySelector('#tel').value
    const cep = document.querySelector('#cep1').value
    const endereco = document.querySelector('#endereco').value
    const numero = document.querySelector('#numero').value
    const bairro = document.querySelector('#bairro').value
    const complemento = document.querySelector('#complemento').value
    const cidade = document.querySelector('#cidade').value
    const estado = document.querySelector('#estado').value
    const concordo = document.querySelector('#concordo').checked

    // validacoes

    const cadastro = {
        nome,
        email,
        telefone,
        cep,
        endereco,
        numero,
        bairro,
        complemento,
        cidade,
        estado,
        concordo
    }

    console.log(cadastro)

})

~~~

2. Salve as alterações e faça o teste no navegador.

> Fazendo ou não o preenchimento dos dados, iremos conseguir pegar os dados do formulário.

>> Vocês devem ter percebido que temos muito código repetido, são 27 linhas para pegar os dados e criar um objeto literal chamado cadastro. Na próxima aula vamos otimizar este nosso código.

## Considerações

> Esta aula vimos como processar os dados do formulário identificação, porém, como um código com várias repetições, que iremos otimizar nas próxima aula e fazer também as validações do formulário.

Salve Devs, até as próximas!
