# Aula 20 - Jordan Shoes - Validar Formulário

> Nesta aula vamos implementar as ações de validação do formulário Identificação, também otimizar as ações de pegar dados do formulário.

## Revisão do form_identificacao

1. No arquivo `index.html`, dentro da section identificacao:

~~~html
<section class="identificacao">
    
    <h2>Identificação</h2>
    <p>* campos obrigatórios</p>

    <form class="form_identificacao">
        <div class="input">
            <label for="nome">Nome completo*</label>
            <input type="text" id="nome" class="" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="email">E-mail*</label>
            <input type="email" id="email" class="" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="tel">Telefone*</label>
            <input type="tel" id="tel" class="" placeholder="99 99999-9999" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="cep1">CEP*</label>
            <input type="text" id="cep1" class="" maxlength="9" placeholder="99999-999" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="endereco">Endereco*</label>
            <input type="text" id="endereco" class="" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="numero">Número*</label>
            <input type="text" id="numero" class="" maxlength="10" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="bairro">Bairro*</label>
            <input type="text" id="bairro" class="" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="complemento">Complemento</label>
            <input type="text" id="complemento" class="" />
            <!-- <span class="erro-complemento"></span> -->
        </div>
        <div class="input">
            <label for="cidade">Cidade*</label>
            <input type="text" id="cidade" class="" required />
            <span class="erro"></span>
        </div>
        <div class="input">
            <label for="estado">Estado*</label>
            <input type="text" id="estado" class="" maxlength="2" required />
            <span class="erro"></span>
        </div>
        <div class="bloco">
            <input type="checkbox" id="concordo" class="checkbox" value="sim" />
            <span class="erro"></span>
            <label for="concordo">Concordo com a Política de Privacidade e os Termos de Uso.*</label>
        </div>
        <div class="botao">
            <button type="submit" class="btn_finalizar_cadastro">Finalizar cadastro</button>
        </div>
    </form>

</section>

~~~

> Dentro das divs de 'input' e 'bloco', abaixo dos inputs adicionei uma tag 'span' com a class 'erro'.
Elas servirão para colocarmos as mensagens de erro.

## CSS para validação do formulário

1. Adicione o seguinte código no final do arquivo style.css:

~~~css

/* validacoes do form */
.campo-invalido {
    border-color: red !important;
}

.campo-valido {
    border-color: green !important;
}

.erro {
    color: red;
    margin-left: 5px;
}

~~~

> Salve as alterações.

## Pegar dados do formulário identificacao

> Dentro do escutador de eventos do btnFinalizarCadastro, deixe conforme o código abaixo:

~~~javascript

const btnFinalizarCadastro = document.querySelector('.btn_finalizar_cadastro')
btnFinalizarCadastro.addEventListener('click', (event) => {
    
    event.preventDefault()
    
    // validacoes

    // pegar dados
    console.log(pegarDados())
    
})
	
~~~

1. Apagamos as duas linhas comentadas.
2. Apagamos todos os códigos que foram feitos na aula 19.
3. Adicionamos os comentários
4. Colocamos o console.log para exibir o retorn da função pegarDados.
5. Salve as alterações.

## função pegarDados

1. Acima do escutador de eventos vamos implementar a função pegarDados, mas antes fazer algumas seleções importantes. Faça o seguinte código:

~~~javascript
// aula 20 validacoes
const formularioIdentificacao = document.querySelector('.form_identificacao')
const todosCamposObrigatorios = formularioIdentificacao.querySelectorAll('[required]')
const todosCampos = formularioIdentificacao.querySelectorAll('input')

const pegarDados = () => {
    const dados = {}
    todosCampos.forEach( campo => {
        dados[campo.id] = campo.value.trim()
    })
    return dados
}

~~~

> Criamos as seleções do formularioIdentificacao, todosCamposObrigatorios e todosCampos. E abaixo a definição da função pegarDados.

2. Salve as alterações e teste no navegador.

## Validar formulário no evento onBlur

1. Abaixo do escutador de eventos do btnFinalizar cadastro adicione o seguinte código:

~~~javascript
// validacao onBlur
todosCamposObrigatorios.forEach( campo => {

    const emailRegex = /\S+@\S+\.\S+/

    campo.addEventListener('blur', (e) => {

        if(campo.value !== "" && e.target.type !== "email") {
            campo.classList.add('campo-valido')
            campo.classList.remove('campo-invalido')
            campo.nextElementSibling.textContent = ''
        } else {
            campo.classList.add('campo-invalido')
            campo.classList.remove('campo-valido')
            campo.nextElementSibling.textContent = `${campo.id} é obrigatório`
        }

        if(emailRegex.test(e.target.value)) {
            campo.classList.add('campo-valido')
            campo.classList.remove('campo-invalido')
            campo.nextElementSibling.textContent = ''
        }

        if(e.target.type === "checkbox" && !e.target.checked) {
            campo.parentElement.classList.add('erro')
        } else {
            campo.parentElement.classList.remove('erro')
        }

    })

})

~~~

2. Salve as alterações e teste no navegador.

> Perceba que só estamos validando por enquanto evento 'blur', ou seja, após sair do campo, é feita a validação.

## Considerações

> Esta aula vimos, os ajustes do html e css necessários para implementar as validações. Em seguida vimos como melhorar a forma de pegar os dados do formulário. E por fim implementamos a validação do formulário identificação com base no evento 'blur' ou 'onBlur'. Nas próximas aulas vamos implementar a outra forma de validação que é feita no evento 'submit', ou seja, no envio do formulário.

Salve Devs, até as próximas!
