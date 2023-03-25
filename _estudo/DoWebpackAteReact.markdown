---
title: Do Webpack até o React
layout: estudo
---

# Do Webpack até o React

## Porque webpack existe

Criar aplicações webs com muitos scripts pode ser complexo. As tags `<scrpt src>` não são mais suficientes, essa técnica não escala. Muitas requisições HTTP seriam necessárias e o app ficaria lento.

Por isso, com o **webpack**, cada arquivo `.js` torna-se um módulo e o Webpack insere todos os módulos e suas dependências em grande arquivo, esse grande arquivo é conhecido como **bundle**.

Com o webpack também é possível utilizar **ES6** e também **JSX**.

O webpack transpila o código para uma versão que o navegador entenda, para isso, é utilizado um plugin conhecido como **Babel**.

Ainda, para que os arquivos fiquem mais compactos usamos **minify** e também o **uglify**. Então, variáveis com nomes longos serão encurtadas e espaços vazios serão removidos.

## Meu primeiro Webpack

Se você já tentou usar `react` possívelmente ja se deparou com inúmeros arquivos. É muito fácil se perder. Ainda mais se ainda não sabe o que o `babel` `react` fazem e como isso é organizado dentro do diretorio.

Antes de continuar com essas incríveis biblitecas, vamos fazer o projeto mais simples possível.

A primeira coisa que precisamos é do gerenciador de pacotes do Node, o NPM.

```
mkdir my-first-webpack
cd my-first-webpack
npm init -y
```

Será gerado um arquivo assim:

```
{
    "name": "my-first-webpack",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"
}
```

Dentre as informações do projeto ( nome, versão e descrição ) o que realmente importa são as dependencias, iremos passar por isso mais tarde.

Em seguida, crie uma pasta `src` onde teremos nosso `index.js` contendo apenas um `console.log("ola mundo")`.Também, instale os pacotes `webpack` `webpack-cli`. Por fim, adicione o trecho abaixo à configuração. Isso permitirá rodar o script de build, no qual o webpack será utilizado.

```
"scripts":
{
    "build": "webpack --mode development"
}
```

Note que o arquivo `package.json` já está atualizado com os pacotes instalados.

Finalmente, você pode rodar o comando `node run build`. O modo escolhido foi de `development`, porém também poderia ser `production`, daí o código seria otimizado para performance. O código gerado estará na pasta `/dist`. É nessa pasta que está o arquivo javascript a ser **dist**ribuido.

## O tal do webpack.config.js

```
const webpack = require('webpack');
const path = require('path');
const config = {
entry: './src/index.js',
output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
}
module.exports = config;
```

Para o nosso projeto, basta essa configuração.

As 2 primeiras linhas servem para importar os pacotes **webpack** e **path**. **Path** servirá para lidarmos com o caminho dos arquivos.

No arquivo de configuração, temos aquilo que é esperado para a entrada, enquanto para a saida temos a pasta destino e o nome do arquivo. Se quiser, pode rodar o mesmo comando anterior para ver o novo arquivo gerado com o nome atualizado.

Por fim, além do código em javascript podemos também querer empacotar outros arquivos (.png .css). Para isso, usaremos `loaders` que irão converter arquivos em módulos válidos.

Aqui, iremos utilizar os seguintes pacotes:

```
babel-loader
@babel/core
@babel/preset-env
```

*Transpiling* babel-loader Loads ES2015+ code and transpiles to ES5 using Babel

Agora, para a configuração, **criaremos um novo arquivo** chamado `.babelrc` na pasta raiz com o seguinte conteúdo:

```
{
    presets: ['@babel/preset-env']
}
```

Isso irá transpilar o código para uma versão onde o navegador entende. Por fim, também mudaremos o arquivo `webpack.config.js`.

Para definir uma regra precisamos de duas chaves: *test* e *use*. Também queremos excluir a pasta *node_modules*, pois dentro dela não há arquivos interessantes para o `Babel`.

```
module: {
    rules:[{
            test: /\.(js)$/,
            exclude: /node_modules/,
            use: 'babel-loader'
        }]
}
```

Para vermos funcionando, mudaremos um pouco o código do `index.js` e por fim usaremos o comando `npm run build` novamente.

```
const hello = () => {
    console.log("hello world!");
} hello()
```

Assim, você consegue ver como o resultado. Dois códigos que fazem a mesma função escritos de maneiras diferentes. Uma delas é aquela entendida pelo navegador.

## Criando uma aplicação em react

Instale o pacote `react react-dom`

Insira o trecho de código abaixo no `index.js`

```
import React from "react";
import ReactDOM from "react-dom";

class App extends React.Component {
render(){
    return <div> Ola Mundo! {this.props.name}</div>
}
}

var mountNode = document.getElementById("app");
ReactDOM.render(<App name="Analise Real"/>, mountNode);
```

Em sequencia, adicione o arquivo `index.html` à pasta `dist/` ( note que é a mesma pasta da saída do javascprit pós transpilação)

Em sequencia, vamos configurar o `Babel` para transpilar JSX ( React ). Por isso iremos adicionar ao arquivo `.babelrc` o seguinte:

```
{
    presets: [
        '@babel/preset-env',
        '@babel/preset-react'
    ]
}
```

Agora o Babel entende .jsx.

Além disso, precisamos alterar o regex que cuida das extensões dos arquivos, já que agora teremos arquivos `.jsx`. Isso fica no arquivo `webpack.config.js`

```
test: /\.(js|jsx)$/,
```

O webpack cuida disso automaticamente para .js, porém também teremos que inserir o seguinte código:

```
resolve: {
    extensions: [
    '.js',
    '.jsx'
    ]
}
```

Por fim, para ver o resultado basta acessar a pasta `dist` onde teremos o arquivo de saída, daí basta editar o código html (e ironicamente usar a tag de scripts que tanto criticamos).

```
<!DOCTYPE html>
<html>
    <head>
        <title>React starter app</title>
    </head>
    <body>
        <div id="app"></div>
        <script src="bundle.js"></script>
    </body>
</html>
```

É possível ver o texto no console, conforme o esperado.