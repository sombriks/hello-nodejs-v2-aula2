# Entendendo module.exports / require()

- 30 minutos light
- debater a importância de modularizar o código do projeto direitinho

## Definição

- TL;DR module.exports "publica" código, require "solicita" código
- no episódio anterior falamos que existe uma coisa chamada commons.js
- ele serve pra modularizar seu projeto
- certas peças de código merecem reuso
- não faz sentido fazer um script de 150 mil linhas
- não faz sentido reinventar a roda
- separação lógica e semântica
- caminho de busca de módulos
  - pasta local
  - pasta node_modules local
  - pasta node_modules global
- um módulo em memória não é carregado novamente

## Aplicação

- usar no script principal arquivos adiconais
- diminuir o tamanho de arquivos individuais
- separar as responsabilidades do projeto em pedaços distintos
- facilitar o rastreio de problemas
- centrarlizar objetos comuns ao aplicativo todo num só lugar
- organizar!

## Exemplo

```javascript
// matematica.js
const mat = {
  soma : (a,b) => a + b,
  subtracao : (a,b) => a - b
};
// aqui estamos publicando o conteúdo (ou parte do conteúdo) deste módulo
module.exports = mat;
```

- na mesma pasta criamos outro script

```javascript
// hello6.js
var libm = require("./matematica");
console.log(libm.soma(2,2)); // prints 4
```

- a extensão do arquivo não deve ser informada
- o es6 tem uma [sintaxe alternativa](http://es6-features.org/#ValueExportImport) para módulos
  - ainda maturando no node e nos browsers

## Exercício

- use seus conhecimentos de input/output
  - crie um script que peça 3 nomes via linha de comando
  - salve-os num arquivo
  - a parte de salvamento em arquivo deve vir de um módulo dedicado
  - o módulo deve publicar pelo menos uma função que receba o nome do arquivo e a lista de nomes pra salvar
