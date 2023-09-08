# API Simples com NodeJs e Express
### Como criar uma API simples em NodeJs com Express 

> O **Nodejs** é uma plataforma que permite que você desenvolva aplicativos de rede escaláveis.  
 O **Express** é um framework muito popular para **Nodejs** que permite criar aplicativos da web com facilidade.   
 Neste tutorial, mostraremos como criar uma API simples em Nodejs com o Express. 


### 1 - Início do projeto, instalação das dependências e configurações iniciais.

Antes de começar, você precisa ter o Nodejs instalado em seu sistema. Você pode baixar o [Nodejs do site oficial](https://nodejs.org/en) e instalá-lo, seguindo as instruções do próprio site.   

Depois comece criando um novo diretório para o seu projeto e inicializando um novo projeto npm dentro dele. Em seguida, instale o Express usando npm (Node Package Manager), que é o gerenciador de pacotes padrão para o Nodejs. Os comandos são:

```bash
mkdir my-api
cd my-api
npm init
```
>O NPM Init, vai fazer perguntas:   
package name: (nodeexpressapi) **node_express_api**  
version: (1.0.0) **[de enter]**  
description: **Simple API with NodeJs and Express**  
entry point: (index.js) **[de enter]**    
test command: **[de enter]**   
git repository: **[de enter]**    
keywords: **[de enter]**    
author: **[caso queira entre com seu apelido]**  
license: (ISC) **MIT** [ou outra licença que achar adequado]

Confirme com **yes** e em seguida instale o **Express**:

```bash
npm install express
```

Crie um arquivo **index.js** na pasta do seu projeto. Este será o principal ponto de entrada para sua API.  

O comando **npm init** usado anteriormente gerou um aquivo chamado **package.json**.  
Edite ele, e adicione a a execução do **index.js** pelo Node na linha após de "test"..., não esquecendo de adicionar a vírgula no final da linha do test:  
Adicione: **"start": "node index.js"**
```json
"test": "echo \"Error: no test specified\" && exit 1",
"start": "node index.js"
```

O arquivo de configuração completo fica similar a:

```json
{
  "name": "node_express_api",
  "version": "1.0.0",
  "description": "Simple API with NodeJs and Express",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "rramires",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

No arquivo **index.js** adicione:

```js
console.log("Hello World!");
```

Execute o seu projeto, no terminal:  

```bash
npm start 
```

Se estiver tudo OK, vai imprimir na tela:  
**Hello World!**

### 2 - Iniciando a codificação
Apague a linha do **console.log** no arquivo **index.js** e importe o Express:

```js
const express = require('express');
```

Crie uma nova instância da aplicação **Express** chamando a função **express()**:

```js
const app = express();
```

O **Express** usa um sistema de roteamento para lidar com solicitações recebidas.  
Você pode definir suas rotas usando o método **app.get()**.  
Adicione:

```js
app.get('/', (req, res) => {
    res.send('Hello World!');
});
```

Por fim, inicie o servidor chamando o método **app.listen()** e passando o número da porta que deseja que ele fique escutando:

```js
app.listen(3000, () => {
    console.log('Server listening on port 3000');
});
```

O arquivo **index.js** fica assim, até agora:

```js
const express = require('express');

const app = express();

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(3000, () => {
    console.log('Server listening on port 3000');
});
```

Salve o arquivo e inicie o servidor executando o comando em seu terminal:

```bash
npm start
```

Você deverá ver a mensagem **"Server listening on port 3000"**.  

Abra um navegador da web e navegue até http://localhost:3000 para ver a mensagem **"Hello, world!"** impressa na página do seu navegador.

De um **control+c** no terminal para parar o servidor:
```bash
...
Server listening on port 3000
^C
volta para o prompt normal:
>
```

>O cógigo fonte desse projeto encontra-se em: 
[https://github.com/rramires/articles/tree/master/NodeExpressAPI](https://github.com/rramires/articles/tree/master/NodeExpressAPI)  
Até essa parte, o comit é: **API NodeExpress parte 1**  
Hash: 9df61de0e2e3a82f18829de850fed5c4554ae588

### 3 - Melhorando o projeto com o pacote **CORS** para restringir a origem, **Morgan** para "fatiar" as solicitações no console e **Helmet** para segurança.

Instale os pacotes **Cors, Morgan e Helmet**:

```bash
npm install cors morgan helmet
```

Atualize index.js: Em seu arquivo index.js, comece importando os novos pacotes necessários:

```js
const express = require('express'); 
const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');
```

> Por padrão, o Express permite que qualquer origem acesse sua API. No entanto, em um ambiente de produção, você geralmente deseja restringir o acesso a origens específicas por razões de segurança. Você pode fazer isso usando o pacote CORS.

Em seguida, adicione o middleware **CORS** ao seu código index.js:

```js
const app = express();

// middlewares
app.use(cors());

// Restante do código
});
```

** Nota: Este código adiciona o middleware **CORS** à sua aplicação, sem nenhum parâmetro, no modo default **All**, ou seja permitindo acesso de qualeur lugar.  
Para restringir num projeto real, adicione um objeto ao cors e passe a origem como parâmetro:

```js
app.use(cors({
  origin: 'http://example.com',
  optionsSuccessStatus: 200 // some legacy browsers (IE11, various SmartTVs) choke on 204
}));
```

Para saber mais vá a página do pacote: [https://www.npmjs.com/package/cors](https://www.npmjs.com/package/cors)  

> Às vezes, é útil registrar todas as solicitações recebidas pela sua API em um arquivo de log ou no console. O pacote Morgan é uma opção popular para isso.  

Adicione o middleware **Morgan** ao seu código index.js:

```js
const app = express();

// middlewares
app.use(cors());
app.use(morgan('dev'));

// Restante do código
});
```
Este código adiciona o middleware Morgan à sua aplicação, registrando todas as solicitações no console.
Para saber mais vá a página do pacote: [https://www.npmjs.com/package/morgan](https://www.npmjs.com/package/morgan)

> O pacote Helmet é uma coleção de pequenos middleware para ajudar a proteger sua aplicação Express de várias vulnerabilidades da web. Ele ajuda a definir vários cabeçalhos HTTP para aumentar a segurança da sua aplicação.  

Adicione o middleware **Helmet** ao seu código index.js:

```js
const app = express();

// middlewares
app.use(cors());
app.use(morgan('dev'));
app.use(helmet());

// Restante do código
});
```

Este código adiciona o middleware Helmet à sua aplicação, protegendo-a de várias vulnerabilidades da web.
Para saber mais vá a página do pacote: [https://www.npmjs.com/package/helmet](https://www.npmjs.com/package/helmet)

Aqui está o arquivo index.js completo, até agora:

```js
const express = require('express');
const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');

const app = express();

app.use(cors(/* 
              { origin: 'http://example.com',
                optionsSuccessStatus: 200 } 
             */));
app.use(morgan('combined'));
app.use(helmet());

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

Salve o arquivo e inicie o servidor executando node index.js em seu terminal. Você deverá ver a mensagem "Server listening on port 3000".  
Abra um navegador da web e navegue até http://localhost:3000 para ver a mensagem "Hello, world!".  

Observe que com o middleware **Morgan**, você deverá ver os logs das solicitações feitas ao seu servidor em seu console.  
Com o middleware do **Helmet**, você terá cabeçalhos de segurança adicionais adicionados às suas respostas para melhor proteção contra vulnerabilidades comuns da web.  
E com o middleware **CORS**, você poderá restringir as origens que podem acessar sua API.


### 4 - Adicionando operações CRUD

>Agora que você criou uma API básica, vamos incrementar adicionando operações CRUD (Criar, Ler, Atualizar, Excluir) para manipular dados.  
Nesse exemplo para ficar mais simples(sem envolver um banco de dados), vamos criar um array de produtos e criar rotas para consultar, inserir, atualizar e excluir produtos.

Adicione o seguinte código no topo do seu arquivo index.js para definir o array de produtos:

```js
const products = [
  { id: 1, name: 'Product 1', price: 10.99 },
  { id: 2, name: 'Product 2', price: 9.99 },
  { id: 3, name: 'Product 3', price: 12.99 }
];
```

Defina uma rota que retorne a matriz de produtos quando uma solicitação **GET** for feita ao endpoint **/products**

```js
/**
 * Return all products
 */
app.get('/products', (req, res) => {
  // return
  res.json(products);
});
```

Defina uma rota que retorne um produto quando uma solicitação **GET** for feita ao endpoint **/products/:id**

```js
app.get('products/:id', (req, res) => {
  // get param
  const id = parseInt(req.params.id);
  // find
  const product = products.find(p => p.id === id);
  // if found
  if(product){
    res.json(product);
  } 
  else{ // if not found
    res.status(404).json({ message: 'Product not found.' });
  }
});
```

Defina uma rota que adicione um novo produto à matriz de produtos quando uma solicitação **POST** for feita ao endpoint **/products**

```js
/**
 * Insert new product
 */
app.post('/products', (req, res) => {
  // define new product
  const newProduct = { id: products.length + 1, ...req.body };
  // add to array
  products.push(newProduct);
  // return
  res.json(newProduct);
});
```

Defina uma rota que atualize um produto existente no array de produtos quando uma solicitação **PUT** for feita para o endpoint **/products/:id** 

```js
/**
 * Update product
 */
app.put('/products/:id', (req, res) => {
  // get params
  const productId = parseInt(req.params.id);
  const updatedProduct = req.body;
  // find and update
  products = products.map(product => {
    if(product.id === productId) {
      return { ...product, ...updatedProduct };
    }
    return product;
  });
  // return
  res.json(products.find(product => product.id === productId));
});
```

Defina uma rota que exclua um produto existente no array de produtos quando uma solicitação **DELETE** for feita para **/products/:id**

```js
/**
 * Delete product
 */
app.delete('/products/:id', (req, res) => {
  // get param
  const productId = parseInt(req.params.id);
  // find
  const deletedProduct = products.find(product => product.id === productId);
  // delete
  products = products.filter(product => product.id !== productId);
  // return
  res.json(deletedProduct);
});
```

Fica assim arquivo index.js completo, até agora:

```js
const express = require('express');
const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');

/**
 * Products array
 */
const products = [
  { id: 1, name: 'Product 1', price: 10.99 },
  { id: 2, name: 'Product 2', price: 9.99 },
  { id: 3, name: 'Product 3', price: 12.99 }
];

/**
 * Express App instance
 */
const app = express();


/* --------- Middlewares --------- */

app.use(cors());
app.use(morgan('combined'));
app.use(helmet());
app.use(express.json());


/* --------- Routes --------- */

/**
 * Return all products
 */
app.get('/products', (req, res) => {
  // return
  res.json(products);
});

/**
 * Return product by id
 */
app.get('products/:id', (req, res) => {
  // get param
  const id = parseInt(req.params.id);
  // find
  const product = products.find(p => p.id === id);
  // if found
  if(product){
    res.json(product);
  } 
  else{ // if not found
    res.status(404).json({ message: 'Product not found.' });
  }
});

/**
 * Insert new product
 */
app.post('/products', (req, res) => {
  // define new product
  const newProduct = { id: products.length + 1, ...req.body };
  // add to array
  products.push(newProduct);
  // return
  res.json(newProduct);
});

/**
 * Update product
 */
app.put('/products/:id', (req, res) => {
  // get params
  const productId = parseInt(req.params.id);
  const updatedProduct = req.body;
  // find and update
  products = products.map(product => {
    if(product.id === productId) {
      return { ...product, ...updatedProduct };
    }
    return product;
  });
  // return
  res.json(products.find(product => product.id === productId));
});

/**
 * Delete product
 */
app.delete('/products/:id', (req, res) => {
  // get param
  const productId = parseInt(req.params.id);
  // find
  const deletedProduct = products.find(product => product.id === productId);
  // delete
  products = products.filter(product => product.id !== productId);
  // return
  res.json(deletedProduct);
});


/* --------- App start --------- */

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

#### Com esse código, agora você poderá recuperar, inserir, atualizar e excluir produtos usando os seguintes endpoints:

* **GET /products:** Retorna a lista de produtos.
* **GET /products/:id:** Retorna o produto por id. 
* **POST /products:** Adiciona um novo produto à lista.
* **PUT /products/:id:** Atualiza um produto existente na lista.
* **DELETE /products/:id:** Exclui um produto existente da lista.

>Agora você tem uma API Nodejs simples em funcionamento com o Express. A partir daqui, você pode adicionar mais rotas, manipular solicitações POST, integrar bancos de dados e expandir sua API conforme necessário. 
O Express oferece uma variedade de recursos poderosos para desenvolvimento web, e você pode explorar mais recursos na documentação oficial: [https://expressjs.com](https://expressjs.com/)