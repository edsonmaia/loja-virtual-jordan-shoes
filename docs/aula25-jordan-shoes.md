# Aula 25 - Jordan Shoes - Controle de login do usuário

> Nesta aula fazer 

## Controle de login

> Vamos implementar uma funcionalidade que indicará se o usuário está logado ou não. Ajuste o código do arquivo index.html no trecho do menu que tem o ícone do usuário:

~~~html
<div class="btn__carrinho_user">
    <span id="btn_open_login" class="material-symbols-outlined icone">
        account_circle
    </span>
    <span id="nome_usuario"></span>
    <span id="btn_logout">Sair</span>
</div>

~~~

1. Apague o texto da 2ª tag span e use o id 'nome_usuario'
2. Adicione a 3ª tag span com o id "btn_logout" e o texto Sair
3. Salve as alterações

### Janela modal ou pop-up de login

> Dentro da main antes da seção 'identificacao' adicione o trecho de código para criação da janela modal ou pop-up de login:

~~~html
<!-- modal logar usuario -->
<section class="modal_login hidden">

    <h2>Entrar</h2>
    <span class="btn_close_login">X</span>

    <form class="form_logar">
        <div class="input">
            <label for="email_login">E-mail</label>
            <input type="email" id="email_login" autofocus required />
        </div>
        <div class="input">
            <label for="senha_login">Senha</label>
            <input type="password" id="senha_login" required />
        </div>
        <div class="botao">
            <button type="submit" class="btn_logar">Entrar</button>
        </div>
    </form>

</section>
<div class="modal_overlay hidden"></div>
<!-- /modal logar usuario -->
~~~

## CSS da janela modal e controle de login

1. Adicione no final do arquivo 'style.css' os seguintes códigos:

~~~css
.icone {
    user-select: none;
}

/* modal ou pop-up login */
.modal_login {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 300px;
    height: 300px;
    background-color: var(--white_soft);
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
    z-index: 10; /* Certifique-se de que o pop-up apareça acima de outro conteúdo */
}

.modal_login h2 {
    text-align: center;
}

.modal_overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 9; /* Posicione atrás do pop-up */
}

.modal_login.hidden, .modal_overlay.hidden {
    display: none;
}

.modal_login.show, .modal_overlay.show {
    display: block;
}

.btn_close_login {
    position: absolute;
    right: 16px;
    top: 20px;
    text-align: center;
    cursor: pointer;
    width: 24px;
    height: 24px;
    padding: 2px 5px;
    border-radius: 50%;
    border: 1px solid #ccc;
}

.btn_close_login:hover {
    font-weight: bold;
    color: #fff;
    background-color: #222;
}

.modal_login .botao {
    margin-top: 20px;
}

~~~

2. Salve as alterações.

## Controle de login usando o JS

> Nosso objetivo nesta aula é 'simular' o controle de login, não é a forma correta, é só uma simulação para que a gente mantenha um estado de 'conectado' do usuário para poder identificá-lo e dar prosseguimento em todas etapas da finalização da compra.

~~~javascript
// aula 25
const btnOpenLogin = document.querySelector('#btn_open_login')
const modalLogin = document.querySelector('.modal_login')
const overlayLogin = document.querySelector('.modal_overlay')
const btnCloseLogin = document.querySelector('.btn_close_login')

btnOpenLogin.addEventListener('click', () => {
    mostrarModal()
})

document.addEventListener('click', (event) => {
    if(event.target === overlayLogin || event.target === btnCloseLogin) {
        fecharModal()
    }
})

const mostrarModal = () => {
    modalLogin.classList.add('show')
    overlayLogin.classList.add('show')
    modalLogin.classList.remove('hidden')
    overlayLogin.classList.remove('hidden')
}

const fecharModal = () => {
    modalLogin.classList.remove('show')
    overlayLogin.classList.remove('show')
    modalLogin.classList.add('hidden')
    overlayLogin.classList.add('hidden')
}

// controle de login
const nomeUsuario = document.querySelector('#nome_usuario')
const btnLogout = document.querySelector('#btn_logout')
const formularioLogar = document.querySelector('.form_logar')
const emailLogin = document.querySelector('#email_login')
const senhaLogin = document.querySelector('#senha_login')

ocultarElemento(btnLogout) // esconder o botao Sair

formularioLogar.addEventListener('submit', (e) => {
    e.preventDefault()
    // pegar dados e validar para autorizar entrada
    console.log(emailLogin.value, senhaLogin.value)
    nomeUsuario.innerHTML = emailLogin.value
    mostrarElemento(btnLogout)
    formularioLogar.reset()
    fecharModal()
})

const logout = () => {
    ocultarElemento(btnLogout)
    nomeUsuario.innerHTML = ''
}

btnLogout.addEventListener('click', logout)

~~~

2. Salve as alterações e teste.

## Considerações

> Esta aula vimos como fazer um controle de login de usuário utilizando uma janela modal, armazenando os dados dela exibindo ao lado do botão do usuário. Também criamos a lógica de mostra/ocultar informações com base no fato do usuário estar ou não logado, porém, sem controle de sessão. Nas próximas aulas vamos aprimorar nossa aplicação.

Salve Devs, até as próximas!
