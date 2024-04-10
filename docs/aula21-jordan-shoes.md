# Aula 21 - Jordan Shoes - Validar Formulário no envio

> Nesta aula vamos implementar as ações de validação do formulário Identificação, agora no envio, e fazer também o controle de fluxo para exibir ou não os dados se o formulário foi preenchido corretamente.

## Validar formulário no envio

> Dentro do escutador de eventos do btnFinalizarCadastro, adicione uma chamada para a função que iremos implementar:

~~~javascript

const btnFinalizarCadastro = document.querySelector('.btn_finalizar_cadastro')
btnFinalizarCadastro.addEventListener('click', (event) => {
    
    event.preventDefault()
    
    // validacoes
    validacaoDoFormulario()

    // pegar dados
    console.log(pegarDados())
    
})
	
~~~

## função validacaoDoFormulario com retorno

1. Acima do escutador de eventos vamos implementar a função 'validacaoDoFormulario'. Faça o seguinte código:

~~~javascript

const validacaoDoFormulario = () => {
    
    todosCamposObrigatorios.forEach( campoObrigatorio => {
        
        const isEmpty = campoObrigatorio.value.trim() === ''
        const isNotChecked = campoObrigatorio.type === 'checkbox' && !campoObrigatorio.checked
        
        if(isEmpty) {
            campoObrigatorio.classList.add('campo-invalido')
            campoObrigatorio.nextElementSibling.textContent = `${campoObrigatorio.id} obrigatorio`
        } else {
            campoObrigatorio.classList.add('campo-valido')
            campoObrigatorio.classList.remove('campo-invalido')
            campoObrigatorio.nextElementSibling.textContent = ''
        }

        if(isNotChecked) {
            campoObrigatorio.parentElement.classList.add('erro')
        } else {
            campoObrigatorio.parentElement.classList.remove('erro')
        }
  
    })

}

~~~

2. Salve as alterações e teste no navegador.

> Antes de digitar qualquer informação, clique no botão Finalizar Cadastro, veja como já irão aparecer as mensagens de validação.

>> Como temos duas funções que fazem a validação, precisamos tomar cuidado para que as ações de uma não atrapalhem nas da outra.


## Controle de fluxo do formulário

1. Vamos controlar o fluxo do nosso formulário, no seguinte sentido, só podemos pegar os dados se o formulário for preenchido corretamente. No escutador de eventos do btnFinalizar cadastro, faça os seguintes ajustes:

~~~javascript

const btnFinalizarCadastro = document.querySelector('.btn_finalizar_cadastro')
btnFinalizarCadastro.addEventListener('click', (event) => {
    
    event.preventDefault()
    
    // validacoes
    validacaoDoFormulario()

    // pegar dados
    if(validacaoDoFormulario()) {
        console.log(pegarDados())
    }
    
})
    
~~~

> Adicionamos um if para pegar o returno da função validacaoDoFormulario, se for true, vamos pegar os dados, senão, por enquanto não fazemos nada. Mas, poderíamos fazer o else para definir as ações em caso de erro no preenchimento do formulário.

2. Adicione a variável formularioValido dentro da função validacacaoDoFormulario, mude o estado dela para false, quando tivermos erros, e por fim, retorne ela.

~~~javascript

const validacaoDoFormulario = () => {
    
    let formularioValido = true

    todosCamposObrigatorios.forEach( campoObrigatorio => {
        
        const isEmpty = campoObrigatorio.value.trim() === ''
        const isNotChecked = campoObrigatorio.type === 'checkbox' && !campoObrigatorio.checked
        
        if(isEmpty) {
            campoObrigatorio.classList.add('campo-invalido')
            campoObrigatorio.nextElementSibling.textContent = `${campoObrigatorio.id} obrigatorio`
            formularioValido = false
        } else {
            campoObrigatorio.classList.add('campo-valido')
            campoObrigatorio.classList.remove('campo-invalido')
            campoObrigatorio.nextElementSibling.textContent = ''
        }

        if(isNotChecked) {
            campoObrigatorio.parentElement.classList.add('erro')
            formularioValido = false
        } else {
            campoObrigatorio.parentElement.classList.remove('erro')
        }
  
    })

    return formularioValido

}

~~~

3. Salve as alterações e teste.

> Perceba que só teremos os dados no console, se o formulário for preenchido corretamente.

## Considerações

> Esta aula vimos como implementar a outra forma de validação que é feita no evento 'submit', ou seja, no envio do formulário. Também fizermos o controle de fluxo para exibir ou não os dados se o formulário foi preenchido corretamente.

Salve Devs, até as próximas!
