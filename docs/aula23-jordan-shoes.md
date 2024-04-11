# Aula 23 - Jordan Shoes - Refatoração e ajustes

> Nesta aula vamos refatorar as ações de preenchimento automático do endereço e ajustar o formulário de identificação mudando o campo estado para o type select.

## Refatorar as ações de preenchimento dos dados do CEP

> No arquivo 'script.js' mude o código do escutador de eventos:

~~~javascript
document.querySelector('#cep1').addEventListener('blur', async (e) => {
    const cep = e.target.value
    if (!cep) {
        limparCampos()
        return
    }
    const resposta = await buscarCep(cep)
    if (resposta.erro) {
        limparCampos()
        return
    }
    preencherCampos(resposta)
    document.querySelector('#numero').focus()
})
  
const limparCampos = () => {
    document.querySelector('#endereco').value = ''
    document.querySelector('#bairro').value = ''
    document.querySelector('#cidade').value = ''
    document.querySelector('#estado').value = ''
}
  
const preencherCampos = (resposta) => {
    document.querySelector('#endereco').value = resposta.logradouro
    document.querySelector('#bairro').value = resposta.bairro
    document.querySelector('#cidade').value = resposta.localidade
    document.querySelector('#estado').value = resposta.uf
}


~~~

Salve as alterações e faça os testes no browser.

## Ajustes no HTML

No arquivo 'index.html' vamos mudar o campo estado para um select, comente o código do input e deixe o código o trecho abaixo:

~~~html
<div class="input">
    <label for="estado">Estado*</label>
    <!-- <input type="text" id="estado" class="" maxlength="2" required /> -->
    <select id='estado' name='estado' required>
        <option value=''>Selecione um estado</option>
        <option value='AC'>Acre</option>
        <option value='AL'>Alagoas</option>
        <option value='AP'>Amapá</option>
        <option value='AM'>Amazonas</option>
        <option value='BA'>Bahia</option>
        <option value='CE'>Ceará</option>
        <option value='DF'>Distrito Federal</option>
        <option value='ES'>Espírito Santo</option>
        <option value='GO'>Goiás</option>
        <option value='MA'>Maranhão</option>
        <option value='MT'>Mato Grosso</option>
        <option value='MS'>Mato Grosso do Sul</option>
        <option value='MG'>Minas Gerais</option>
        <option value='PA'>Pará</option>
        <option value='PB'>Paraíba</option>
        <option value='PR'>Paraná</option>
        <option value='PE'>Pernambuco</option>
        <option value='PI'>Piauí</option>
        <option value='RJ'>Rio de Janeiro</option>
        <option value='RN'>Rio Grande do Norte</option>
        <option value='RS'>Rio Grande do Sul</option>
        <option value='RO'>Rondônia</option>
        <option value='RR'>Roraima</option>
        <option value='SC'>Santa Catarina</option>
        <option value='SP'>São Paulo</option>
        <option value='SE'>Sergipe</option>
        <option value='TO'>Tocantins</option>
    </select>
    <span class="erro"></span>
</div>

~~~

Salve as alterações e teste no navegador.

## Considerações

> Esta aula vimos como refatorar a funcionalidade de preenchimento automático do endereço, bairro, cidade e estado com base na informação do CEP que foi usado para fazer uma requisição que busca os dados na API ViaCEP. Também mudamos o campo estado para o type select.

Salve Devs, até as próximas!
