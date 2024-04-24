# Aula 26 - Jordan Shoes - Cadastro de usuário

> Nesta aula fazer o fluxo de cadastro 'rápido' do usuário com e-mail e senha para permitir a autenticação (login).

## Cadastrar usuário

1. Dentro do form_login, após a div do botão adicione o seguinte código:

~~~html
<div class="centralizar">
    <a class="link_cadastrar" href="">Cadastrar usuário</a>
</div>

~~~

2. Vamos implementar funcionalidade para 'Cadastrar Usuário'. No código html após a modal de login adicione as seguintes linhas:

~~~html
<!-- modal cadastrar usuario -->
<section class="modal_cadastrar_usuario hidden">

    <h2>Cadastrar</h2>
    <span class="btn_close_cadastrar">X</span>

    <form class="form_cadastrar_usuario">
        <div class="input">
            <label for="email_usuario">E-mail</label>
            <input type="email" placeholder="user@mail.com" id="email_usuario" autofocus required />
        </div>
        <div class="input">
            <label for="senha_login">Senha</label>
            <input type="password" placeholder="mínimo 5 caracteres" id="senha_usuario" required />
        </div>
        <div class="input">
            <label for="confirma_senha_login">Confirme a Senha</label>
            <input type="password" id="confirma_senha_usuario" required />
        </div>
        <div class="botao">
            <button type="submit" class="btn_cadastrar">Cadastrar</button>
        </div>
        <div class="centralizar">
            <span class="form_aviso"></span>
        </div>
    </form>

</section>
<div class="modal_overlay_cadastrar hidden"></div>
<!-- /modal cadastrar usuario -->
~~~

3. Salve as alterações.

## Ajustes no CSS

1. No arquivo 'style.css' faça os ajustes nas seguintes linha de código:

~~~css
/* modal ou pop-up login */
.modal_login, .modal_cadastrar_usuario {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 300px;
    height: auto; /* 300px */
    background-color: var(--white_soft);
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
    z-index: 10; /* Certifique-se de que o pop-up apareça acima de outro conteúdo */
}

.modal_login h2, .modal_cadastrar_usuario h2 {
    text-align: center;
}

.modal_overlay, .modal_overlay_cadastrar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 9; /* Posicione atrás do pop-up */
}

.modal_login.hidden, .modal_overlay.hidden, .hidden {
    display: none;
}

.modal_login.show, .modal_overlay.show, .show {
    display: block;
}

.btn_close_login, .btn_close_cadastrar {
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

.btn_close_login:hover, .btn_close_cadastrar:hover {
    font-weight: bold;
    color: #fff;
    background-color: #222;
}

.modal_login .botao, .botao {
    margin-top: 20px;
}

/* modal cadastrar usuario */
.centralizar {
    text-align: center;
}

.link_cadastrar {
    color: var(--dark);
    cursor: pointer;
    text-decoration: none;
}

.link_cadastrar:hover {
    text-decoration: underline;
}

~~~

2. Observe que fizemos a adição das classes .modal_cadastrar_usuario, .overlay_cadastrar_usuario e .btn_close_cadastrar
3. Criamos também algumas poucas formatações para ajustes da nova janela modal. Salve as alterações.

## Controlar a janela modal ou pop-up de cadastro de usuário

> Vamos controlar o cadastro de novos usuários usando apenas as informações de e-mail e senha.

1. No final do arquivo 'script.js' adicione o seguinte código:

~~~javascript
// aula 26
const modalCadastrarUsuario = document.querySelector('.modal_cadastrar_usuario')
const modalOverlayCadastrar = document.querySelector('.modal_overlay_cadastrar')
const btnCloseCadastro = document.querySelector('.btn_close_cadastrar')
const linkCadastrar = document.querySelector('.link_cadastrar')

linkCadastrar.addEventListener('click', (e) => {
    e.preventDefault()
    fecharModal()
    modalCadastrarUsuario.classList.add('show')
    modalOverlayCadastrar.classList.add('show')
})

btnCloseCadastro.addEventListener('click', () => {
    modalCadastrarUsuario.classList.remove('show')
    modalOverlayCadastrar.classList.remove('show')
})

const formularioCadastrarUsuario = document.querySelector('.form_cadastrar_usuario')
const formAviso = document.querySelector('.form_aviso')

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
})

~~~

2. Salve as alterações e teste.

### Ajustes no JS

As funções mostrarModal e fecharModal está com 4 linhas cada, mas, não há necessidade de todas as linhas, pois, por padrão a janela modal já vem com a class 'hidden'. Portanto, os códigos podem ficar com menos linhas conforme vemos abaixo:

~~~javascript
const mostrarModal = () => {
    modalLogin.classList.add('show')
    overlayLogin.classList.add('show')
    // modalLogin.classList.remove('hidden')
    // overlayLogin.classList.remove('hidden')
}

const fecharModal = () => {
    modalLogin.classList.remove('show')
    overlayLogin.classList.remove('show')
    // modalLogin.classList.add('hidden')
    // overlayLogin.classList.add('hidden')
}
~~~

> Podemos apagar as linhas que estão comentadas. Salvar as alterações.

## Considerações

> Esta aula vimos como fazer um controle do processo de autenticação e autorização, pois, criamos o fluxo de cadastro de novos usuários usando e-mail e senha. Isto, possibilita o processo de login.

>> Você deve ter pensando. "E aquele formulário Identificação?". Ele serve para fazer o cadastro completo do usuário. Mas, nele não temos o campo de senha e confirmação de senha. Poderíamos ter adicionado nele? Sim, mas, ele iria ficar muito grande, demorado para ser preenchido. O objetido do cadastro inicial é ser "rápido e fácil" por isso fizemos um cadastro de usuário inicial separado, pegando apenas e-mail e senha como informações.

Salve Devs, até as próximas!
