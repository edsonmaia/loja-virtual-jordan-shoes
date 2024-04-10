# Aula 22 - Jordan Shoes - Preencher endereço usando API de CEP

> Nesta aula vamos implementar as ações de preenchimento automático dos dados do endereço, bairro, cidade e estado no formulário de identificação

## Preencher dados do endereço usando API ViaCEP

> No final do código do arquivo 'script.js' adicione as seguintes linhas de código:

~~~javascript
// aula 22
const buscarCep = async (cep) => {
    const url = `https://viacep.com.br/ws/${cep}/json/`
    const response = await fetch(url)
    const data = await response.json()
    return data
}

document.querySelector('#cep1').addEventListener('blur', async (e) => {
    const cep = e.target.value
    if(cep) {
        let resposta = await buscarCep(cep)
        console.log(resposta)
        if(!resposta.erro) {
            document.querySelector('#endereco').value = resposta.logradouro
            document.querySelector('#bairro').value = resposta.bairro
            document.querySelector('#cidade').value = resposta.localidade
            document.querySelector('#estado').value = resposta.uf
        } else {
            document.querySelector('#endereco').value = ''
            document.querySelector('#bairro').value = ''
            document.querySelector('#cidade').value = ''
            document.querySelector('#estado').value = ''
        }
    } else {
        document.querySelector('#endereco').value = ''
        document.querySelector('#bairro').value = ''
        document.querySelector('#cidade').value = ''
        document.querySelector('#estado').value = ''
    }
})

~~~

Salve as alterações e faça os testes no browser.

## Desafio da aula

> Nesta aula vimos que após informar o CEP, pressionar TAB ou passar para outro campo, os dados do endereço são preenchidos se o CEP estiver correto. Eu sugiro que após o preenchimento do CEP, "mude o foco para o campo número".

## Considerações

> Esta aula vimos como implementar a funcionalidade de preenchimento automático do endereço, bairro, cidade e estado com base na informação do CEP que foi usado para fazer uma requisição que busca os dados na API ViaCEP.

Porém, temos uma estrutura if else com várias repetições de código. Sugiro que vocês façam a refatoração.

Salve Devs, até as próximas!
