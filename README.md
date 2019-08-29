# Teste CI

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



# github

git init  
git add README.md  
git commit -m "first commit"  
git remote add origin https://github.com/ricardorodrigooliveira/lab2tinr.git  
git push -u origin master  