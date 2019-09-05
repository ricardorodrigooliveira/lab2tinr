# Teste CI

## Aula 1

## Criação do diretório

### Inicie um terminal e digite
```node.js
mkdir lab2tinr
```
### Navegue para o novo diretório
```node.js
cd lab2tinr
```

## Instalação de pacotes necessários
```node.js
npm init  

npm install express request --save

npm install moch chai --save-dev
```

## Criação de arquivo
Crie o arquivo index.js dentro do diretório principal e inclua o texto abaixo;
```node.js
var express = require('express')
var app = express()

app.set('port', 5000)
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
          response.send(
              'Continuous Integration (CI) is a development practice that requires developers to integrate code into a sh    ared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early.'
          )
})

app.listen(app.get('port'), function() {
    console.log("Node app is running at localhost:" + app.get('port'))
})

```

## Criação de diretório
Crie o diretório test dentro do diretório principal e crie o arquivo index-spec.js dentro de test e insira o script abaixo;
```node.js
var app = require('../index')

var http = require('http'),
    assert = require('assert'),
    express = require('express'),
    app = express();
    
app.set('port', 5000)

var baseurl = 'http://127.0.0.1:' + app.get('port') + '/';
console.log('Testing with URL', baseurl);

var request = require('request');
var assert = require('chai').assert;

describe('/', function () {
  it('should return 200', function (done) {
    request(baseurl, {json:true}, function(err, response, body) {
      assert.equal(200, response.statusCode);
      done();
    });
  });
});
```

## Package.json
Altere o package.json da seguinte forma;
```node.js
"scripts": {
    "test": "mocha --exit"
```
Isto será chamado na hora do build da aplicação

# Aultomatização
https://travis-ci.org

## Diretório novo
Criar novo diretório na raiz chamado .travis.yml e o conteudo é;
```yml
language: node_js
node_js:
  - "10"
```

# Teste
Facha o push para o git

Acesse o sitehttps://travis-ci.org e faça login com o usuário do git  
O travis já irá exibir os repositórios do git e basta ligar a chave para os repositórios que deseje testar.


### Notas gerais
* build Scripts
    1. Linguagem de integração entre CI e o repositório (Como deve se comportar caso seja feito uma alteração no repositório)


## Aula 2

* Criação de uma conta no HEROKU https://heroku.com  

Documentação referente a execução de node usando PAAS (Heroku)
https://devcenter.heroku.com/articles/getting-started-with-nodejs?singlepage=true

1. Academicamente vamos utilizar uma maquina virtual com uma linha de comando no cmd  
2. ssh -l ricardo cicd.fiapdev.com -p 80  
Senha: fiap_1234  
3. Clona o diretório git para a maquina  
4. Conecta no heroku com o comando...  
  heroku login -i (Informe usuário e senha)  
5. Cria o app com o comando  
  heroku create -a <nome do repositírio>  

### 1º teste
Fazer um push para o repositório, porém do Heroku...  
git push heroku master

O HEROCU vai instalar todas as dependencias de acordo com o que está declarado no packge.json

A partir dai a aplicação já está no HEROKU e em settings já foi criada uma url para acesso. No caso do nosso teste...  
https://lab2tinr-80438.herokuapp.com/  

Com o comando abaixo é possivel ver a execução
```dos
heroku logs --tail
```
Para teste direto no terminal, instale as dependencias abaixo  
```node
npm install request express --save
```

### 2º teste
Alterações
```dos
nano package.json
```
E edita o arquivo incluindo na tag script...  
```json
"start": "node index.js",
```

para sair...  
CTRL+O  
ENTER  
CTRL+X  

Alteração no index.js  

Alterar a linha onde está declarada a porta...  
```node.js
app.set('port', (process.env.PORT || 5000))
```

Fazemos novamente o push seguindo os comandos
git add -A  
git config --global user.email "seu email do git"
git config --global user.name "seu nome do git"
git push heroku master




# github

git init  
git add README.md  
git commit -m "first commit"  
git remote add origin https://github.com/ricardorodrigooliveira/lab2tinr.git  
git push -u origin master  
