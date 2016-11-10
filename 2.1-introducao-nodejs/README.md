# Introdução ao node.js

- 60 minutos
- pra não esquecer, criar desde agora o repositório e dar checkout local pra praticar
  - hello-nodejs-v2-aula2
  - ver as instruções do github sobre como realizar um **git clone** do seu repositório

## Definição

- interpretador + plataforma baseada em javascript
- derivado da engine javascript do chrome
- filho da "guerra dos browsers"
- commons.js trouxe a modularização
  - módulos em javascript só foram formalizados no es6
  - implementação nula ou parcial nos browsers
- npm
  - gestão das dependências do projeto
  - SemVer (Semantical Version)

## Aplicação

- aplicativos de rápida configuração
- microservices
  - enxame de pequenos serviços em vez de um monolito complexo
- do embarcado ao enterprise
- camada de serviço (a.k.a. webservices)

## Exemplo

- vamos praticar? pratiquem. cada script deve ser salvo na pasta do projeto de aula 2
- não esquecer de comitar e fazer push após cada script

```bash

git add .
git commit -m "exercicio"
git push -u origin master

```

### 1 - Hello world

- para executar alguma coisa no node, você só precisa do interpretador instalado e de um script

```bash
touch hello1.js
geany hello1.js
```

- crie seu hello world

```javascript
// hello1.js
console.log("Hello, friend! %s",process.argv[0])
```

- execute via linha de comando

```bash
node hello1.js
```

- o [process](https://nodejs.org/api/process.html) tem vários atributos notáveis
  - o **argv** com a lista de argumentos
  - o **env** com as variáveis de ambiente relacionadas ao processo

### 2 - Verificando variáveis de ambiente

- uma forma comum de customizar a execução do seu projeto node é definir variáveis de ambiente para ele

```bash
touch hello2.js
geany hello2.js
```

```javascript
// hello2.js
console.log("Estamos no ambiente de [%s]", process.env.NODE_ENV)
```

- definir uma variável de ambiente agora

```bash
NODE_ENV="producao" node hello2.js
```

- ou ainda

```bash
export NODE_ENV="producao"
node hello2.js
```

### 3 - Ler a partir do prompt (readline)

```javascript
// hello3.js
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('Digite um número\n', (num) => {
  if(isNaN(num))
    console.log('%s não é um número válido', num);
  else
    console.log("Você digitou o número %s", num);
  rl.close();
});
```

- pode parecer estranho, mas está [documentado](https://nodejs.org/api/readline.html#readline_rl_question_query_callback) então não tem desculpa pra não aprender, firmeza?
- o **require()** vai ser melhor detalhado adiante

### 4 - Escrever em arquivo

```javascript
// hello4.js
const fs = require("fs");
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

var nomes = [];

function leianome(count){
  if(count--){
    rl.question("Digite um nome:\n",function(line){
      nomes.push(line);
      leianome(count);
    });
  }else gravaarquivo();
}

function gravaarquivo(){

  for(var i in nomes)
    fs.appendFile("nomes.txt",nomes[i]+"\n");

  rl.close();
  console.log("Arquivo nomes.txt salvo!");
}

// chamar a função
leianome(3);
```

- o node é de natureza assíncrona
  - em miúdos, isso de função que vem como parâmetro é praticamente regra
- se você chamar este exemplo mais de uma vez, os nomes não são sobrescritos

## Exercício

- crie um script (*hello5.js*) no seu repositório desta aula
- peça via linha de comando o nome do arquivo a ser criado
- salve neste arquivo 5 linhas que devem representar o nome de países
