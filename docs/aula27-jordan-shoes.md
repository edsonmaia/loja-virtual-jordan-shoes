# Aula 27 - Jordan Shoes - Identifique-se

> Nesta aula fazer o fluxo de identificação do usuário para finalização de compra.

## Tela identifique-se

1. No arquivo 'index.html' vamos adicionar o seguinte código, acima da 'section .modal_login':

~~~html

<section class="identifique-se">
    <h2>Identifique-se</h2>
    <div class="criar_conta">
        <span class="btn btn_criar_conta">Criar conta</span>
    </div>
    ou
    <div class="entrar">
        <button class="btn_fazer_login">Fazer login</button>
    </div>
</section>

~~~ 

## Ajustes no CSS

1. Ajuste o código css, por volta da linha 350:

~~~css
/* ajuste aula 27 */
.botao button, .btn_continuar, .btn_fazer_login, .btn_criar_conta { 
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

> Adicionamos as classes 'btn_fazer_login' e 'btn_criar_conta' no seletor para fazer a formatação dos botões

2. Adicione no final do arquivo 'style.css' o seguinte código:

~~~css
/* aula 27 */
.identifique-se {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-top: 70px;
    gap: 20px;
}

.identifique-se span {
    text-align: center;
}

.identifique-se h2, .identifique-se h3 {
    margin-bottom: 20px;
}

.criar_conta, .entrar {
    width: 50%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.btn {
    width: 100%;
    height: 50px;
    border-radius: 50px;
    background-color: #ccc;
    color: #222;
    display: flex;
    align-items: center;
    justify-content: center;
}

~~~

## Refatorar a função que abre a modal de cadastro

1. Usar o objeto document
2. Criar outro seletor para o botão Criar cadastro
3. Utilizar uma estrutura if para indicar que a modal deve abrir se clicarmos no link ou no botão

~~~javascript
const linkCadastrar = document.querySelector('.link_cadastrar')

linkCadastrar.addEventListener('click', (e) => {
    e.preventDefault()
    fecharModal()
    modalCadastrarUsuario.classList.add('show')
    overlayCadastrarUsuario.classList.add('show')
})

~~~

Ajuste o código pelo seguinte:

~~~javascript
const linkCadastrar = document.querySelector('.link_cadastrar')
const btnCriarConta = document.querySelector('.btn_criar_conta')

document.addEventListener('click', (e) => {
    if(e.target === linkCadastrar || e.target === btnCriarConta) {
        e.preventDefault()
        fecharModal()
        modalCadastrarUsuario.classList.add('show')
        overlayCadastrarUsuario.classList.add('show')
    }
})

~~~

## Refatorar a função que abre a modal de login

~~~javascript
// aula 27
const btnFazerLogin = document.querySelector('.btn_fazer_login')
document.addEventListener('click', (event) => {
    if(event.target === btnOpenLogin || event.target === btnFazerLogin) {
        mostrarModal()
    }
})

~~~

## O que fazer após fazer login ou criar conta

> Ao invés de ir para a tela de identificação, que tem aquele cadastro longo, podemos direcionar o usuário para escolher, criar conta ou logar, e se ele já estiver logado já redirecionar para a página de Pagamento.

1. Ajuste do que fazer após login feito durante o Continuar carrinho:

~~~javascript
formularioLogar.addEventListener('submit', (e) => {
    e.preventDefault()
    // pegar dados e validar para autorizar entrada
    console.log(emailLogin.value, senhaLogin.value)
    nomeUsuario.innerHTML = emailLogin.value
    mostrarElemento(btnLogout)
    formularioLogar.reset()
    fecharModal()
    // aula 27
    ocultarElemento(sectionIdentifiquese)
    mostrarElemento(sectionPagamento)

})

~~~

2. Ajustes do que fazer após o cadastro de nova conta

~~~javascript
formularioCadastrarUsuario.addEventListener('submit', (e) => {
    e.preventDefault()
    // pegar dados, validar e autenticar
    const email = document.querySelector('#email_usuario').value
    const senha = document.querySelector('#senha_usuario').value
    const confirmaSenha = document.querySelector('#confirma_senha_usuario').value

    // validação
    const mensagemSenhaInvalida = senha.length < 5 ? 'Digite uma senha com no mínimo 5 caracteres' : 'Senha e confirmação SÃO diferentes'
    if(senha.length < 5 || senha !== confirmaSenha) {
        formAviso.innerHTML = mensagemSenhaInvalida
        return
    }

    // armazenar e autenticar - login
    formularioCadastrarUsuario.reset()
    formAviso.innerHTML = ''
    modalCadastrarUsuario.classList.remove('show')
    overlayCadastrarUsuario.classList.remove('show')

    const usuario = {
        email,
        senha
    }
    console.log(usuario)
    nomeUsuario.innerHTML = usuario.email
    mostrarElemento(btnLogout)

    // aula 27
    ocultarElemento(sectionIdentifiquese)
    mostrarElemento(sectionPagamento)
    
})

~~~

## Considerações

> Esta aula vimos como fazer o controle das ações necessárias para identificação do usuário antes de finalizar a compra na seção Pagamento.

Vocês devem ter percebido que o código está complexo, e não está fácil de manutenção, nem de extensão. É um grande indicativo de que precisa ser refatorado.

Salve Devs, até as próximas!
