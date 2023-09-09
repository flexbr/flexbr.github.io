# API Simples com NodeJs e Express
### Como criar uma API simples em NodeJs com Express 

> O **Nodejs** é uma plataforma que permite que você desenvolva aplicativos de rede escaláveis.  
 O **Express** é um framework muito popular para **Nodejs** que permite criar aplicativos da web com facilidade.   
 Neste tutorial, mostraremos como criar uma API simples em Nodejs com o Express. 


### 1 - Início do projeto, instalação das dependências e configurações iniciais.

Antes de começar, você precisa ter o **Nodejs** instalado em seu sistema. Você pode baixar o [Nodejs do site oficial](https://nodejs.org/en) e instalá-lo, seguindo as instruções do próprio site.   

Depois comece criando um novo diretório para o seu projeto e inicializando um novo projeto com o **npm**(Node Package Manager, gerenciador de pacotes padrão para o Nodejs) dentro dele. Em seguida, instale o Express usando **npm**. Os comandos são:

```bash
mkdir my-api
cd my-api
npm init
```
>**O NPM Init, vai fazer perguntas:**  
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

Se estiver usando o **Git**, crie um aquivo chamado **.gitignore** (inicia com ponto + gitignore) na raiz do seu projeto e nele adicione o nome da pasta onde os módulos do **Nodejs** foram instalados.  
Isso faz com que eles sejam ignorados pelo **Git** e consequentemente não subam para o **GitHub**.  
Adicione:
```bash
node_modules
```

Crie um arquivo **index.js** na pasta do seu projeto. Este será o principal ponto de entrada para sua **API**.  

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
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
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
Apague a linha do **console.log** no arquivo **index.js** e importe o **Express**:

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

Por fim, inicie o servidor chamando o método **app.listen()** e passando o número da porta que deseja que ele fique escutando. No nosso caso, usaremos a **3000**:

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

Você deverá ver a mensagem no terminal: **"Server listening on port 3000"**.  

Abra um navegador da web e navegue até **http://localhost:3000**  
A mensagem **"Hello, world!"** deverá ser impressa na página do seu navegador.


>Parabéns! Objetivos atingidos até aqui:
> * Criamos um novo projeto em **NodeJs**
> * Concluímos as configurações iniciais
> * Adicionamos o **Express** e iniciamos um servidor na porta **3000**
> * Criamos e testamos a primeira rota que responde a chamadas via URL: **http://localhost:3000**


De um **control+c** no terminal para parar a execução do servidor:
```bash
...
Server listening on port 3000
^C
volta para o prompt normal:
>
```
>O cógigo fonte desse projeto encontra-se em: 
[https://github.com/rramires/articles/tree/master/NodeExpressAPI](https://github.com/rramires/articles/tree/master/NodeExpressAPI)  
Até essa parte, o commit é: **API NodeExpress parte 1 fix 2**  
Hash: acf3352524a416dd7598d4e2b915d8cdf5648aab

### 3 - Melhorando o projeto com o pacote **CORS** para restringir a origem, **Morgan** para "fatiar" as solicitações no console e **Helmet** para segurança.

Instale os pacotes **Cors, Morgan e Helmet**:

```bash
npm install cors morgan helmet
```

No início do seu arquivo **index.js**, importe os novos pacotes necessários:

```js
const express = require('express'); 
const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');
```

> Por padrão, o Express permite que de qualquer origem acesse sua API. No entanto, em um ambiente de produção, você geralmente deseja restringir o acesso a origens específicas por razões de segurança. Você pode fazer isso usando o pacote CORS.

Em seguida, adicione o middleware **CORS** ao seu código index.js:

```js
const app = express();

// middlewares
app.use(cors());

// Restante do código
});
```

**Nota**: Este código adiciona o middleware **CORS** à sua aplicação, sem nenhum parâmetro, no modo default **All**, ou seja permitindo acesso de qualeur lugar.  
Para restringir num projeto real, adicione um objeto ao cors e passe a origem como parâmetro:

```js
app.use(cors({
  origin: 'http://example.com',
  optionsSuccessStatus: 200 // some legacy browsers (IE11, various SmartTVs) choke on 204
}));
```

Para saber mais vá a página do pacote: [https://www.npmjs.com/package/cors](https://www.npmjs.com/package/cors)  

> Às vezes, é útil registrar todas as solicitações recebidas pela sua API em um arquivo de log ou no console. O pacote Morgan é uma opção muito popular para isso.  

Adicione o middleware **Morgan** ao seu código index.js:

```js
const app = express();

// middlewares
app.use(cors());
app.use(morgan('dev'));

// Restante do código
});
```
Este código adiciona o middleware Morgan à sua aplicação, registrando todas as solicitações no console. Isso ajuda na etapa de desenvolvimento na visualização das chamadas ao servidor. 
Para saber mais vá a página do pacote: [https://www.npmjs.com/package/morgan](https://www.npmjs.com/package/morgan)

> O pacote Helmet é uma coleção de middlewares, para ajudar a proteger sua aplicação Express de várias vulnerabilidades da web. Ele ajuda a definir vários cabeçalhos HTTP para aumentar a segurança da sua aplicação.  

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

// middlewares
app.use(cors(/* 
              { origin: 'http://example.com',
                optionsSuccessStatus: 200 } 
             */));
app.use(morgan('dev'));
app.use(helmet());

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

Salve o arquivo e inicie o servidor executando **"npm start"** em seu terminal. Você deverá ver a mensagem **"Server listening on port 3000".**  
Abra um navegador da web e navegue até **http://localhost:3000** para ver a mensagem **"Hello, world!".**  

>**O que mudou:**  
> * Observe que com o middleware **Morgan**, você deverá ver os logs das solicitações feitas ao seu servidor em seu console. Onde está a opção **dev**, experimente trocar por **combined** ou outras opções que você acha na página do pacote
> * Apesar de não ver nenhuma indicação visual com o middleware **Helmet**, você terá cabeçalhos de segurança adicionais adicionados às suas respostas para melhor proteção contra vulnerabilidades comuns da web. Sua aplicação agora está mais segura!  
> * E com o middleware **CORS**, você poderá restringir as origens que podem acessar sua API. Descomentando o objeto onde está **(origin: 'http://seusite.abc')** e configurando com as únicas origens corretas, quando estiver em produção.

>Até essa parte, o commit é: **API NodeExpress add Cors, Morgan e Helmet**  
Hash: 15dc1a42b3a7459f2b68bd1415850e205acfe03f


### 4 - Adicionando operações CRUD

>Agora que você criou uma API básica, vamos incrementar adicionando operações CRUD (Criar, Ler, Atualizar, Excluir) para manipular dados.  
Nesse exemplo para ficar mais simples(sem envolver um banco de dados), vamos criar um array de produtos e criar rotas para consultar, inserir, atualizar e excluir produtos.

Adicione o array de produtos no início do seu arquivo **index.js**, logo após a importação dos pacotes:

```js
/**
 * Products array
 */
const products = [
  { id: 1, name: 'Product 1', price: 10.99 },
  { id: 2, name: 'Product 2', price: 9.99 },
  { id: 3, name: 'Product 3', price: 12.99 }
];
```

Adicione um novo middleware para fazer o parser de conteúdo JSON, logo após o **Helmet**:

```js
app.use(express.json());
```

Apague a rota do **Hello world** e em seu lugar, e defina uma rota que todo o array de produtos quando uma requisição **GET** for feita ao endpoint **/products**.

```js
/**
 * Return all products
 */
app.get('/products', (req, res) => {
  // return 200 OK + products array
  res.json(products);
});
```

Inicie a aplicação, abra o navegador e vá até **http://localhost:3000/products** para ver o array de produtos, retornando em formato **JSON**.

Depois defina uma rota para retornar um produto pelo **id** quando uma requisição **GET** for feita ao endpoint **/products/:id**

```js
/**
 * Return product by id
 */
app.get('/products/:id', (req, res) => {
  // get param
  const id = parseInt(req.params.id);
  // find
  const product = products.find(p => p.id === id);
  // if found
  if(product){
    // return 200 OK + product
    res.json(product);
  } 
  else{ 
    // return 404 Not Found + message
    res.status(404).json({ message: 'Product not found.' });
  }
});
```

Inicie a aplicação novamente, vá até **http://localhost:3000/products/1** para ver um produto específico. Troque o número final **1** por 2 ou três e observe que o produto mudou. Coloque um número que não existe, ex: **4** e perceba que retorna o erro **404**, com a mensagem **Product not found**.


Antes de fazermos as rotas de inserção e exclusão, perceba que fica chato ficar iniciando a aplicação com o **npm start** e parando com o "ctrl+c" toda vez que faz uma modificação.
Para melhorar isso, vamos instalar mais um pacote, o **Nodemon**(Node Monitor) e configurá-lo. Com isso, iniciando o projeto com ele, cada vez que for salvo qualquer arquivo na aplicação, ela reinicia automaticamente.
Instale o **Nodemon**, no modo desenvolvedor:

```bash
npm install --save-dev nodemon
```

Após a instalação adicione o novo comando de execução no arquivo de configuração **package.json** depois da linha do **"start"**, não esquecendo da vírgula no final da linha anterior:

```json
"dev": "nodemon index.js" 

// Fica assim essa parte:
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "start": "node index.js", 
  "dev": "nodemon index.js" 
}
```
>A partir de agora, inicie sua aplicação no terminal com o comando:  
**npm run dev**  
Quando salvar o arquivo, **index.js** perceba que a aplicação reinicia automaticamente, executando a versão mais nova do código. Experimente dar **ctrl+s** para salvar mesmo sem modificar nada, e perceba na janela do terminal a cada vez:  

```bash  
[nodemon] restarting due to changes...  
[nodemon] starting `node index.js`  
Server listening on port 3000  
```

Continuando com as rotas. Vamos precisar de uma variável auxiliar para servir de auto-incremento para o id dos produtos. Para isso adicione logo após o array de produtos:

```js
/**
 * Aux to create incremental product ID
 */
let idCounter = products.length; 
```

Defina uma rota que adicione um novo produto ao array de produtos quando uma requisição **POST** for feita ao endpoint **/products**

```js
/**
 * Insert new product
 */
app.post('/products', (req, res) => {
  // create a new product 
  const newProduct = { id: ++idCounter, ...req.body };
  // add to array
  products.push(newProduct);
  // return 201 Created + product 
  res.status(201).json(newProduct);
});
```

Defina uma rota que atualize um produto existente no array de produtos quando uma requisição **PUT** for feita para o endpoint **/products/:id** 

```js
/**
 * Update product
 */
app.put('/products/:id', (req, res) => {
  // get params
  const productId = parseInt(req.params.id);
  const updatedProduct = req.body;
  // find product index
  const index = products.findIndex(product => product.id === productId);
  // if not found
  if(index === -1){
    // return 404 Not Found + message
    res.status(404).json({ message: 'Product not found.' });
  }
  else{
    // updates the product using destructuring assignment
    products[index] = { ...products[index], ...updatedProduct };
    // return 200 OK + product
    res.json(products[index]);
  }
});
```

Defina uma rota que exclua um produto existente no array de produtos quando uma requisição **DELETE** for feita para **/products/:id**

```js
/**
 * Delete product
 */
app.delete('/products/:id', (req, res) => {
  // get param
  const productId = parseInt(req.params.id);
  // find product index
  const index = products.findIndex(product => product.id === productId);
  if(index === -1){
    // return 404 Not Found + message
    res.status(404).json({ message: 'Product not found.' });
  }
  else{
    // delete
    products.splice(index, 1);
    // return 200 OK + product ID
    res.json({ id: productId });
  }
});
```

Fica assim arquivo **index.js** completo, até agora:

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
 * Aux to create incremental product ID
 */
let idCounter = products.length; // starts with value 3 

/**
 * Express App instance
 */
const app = express();


/* --------- Middlewares --------- */

app.use(cors(/* 
              { origin: 'http://site.abc',
                optionsSuccessStatus: 200 } 
             */));
app.use(morgan('dev'));
app.use(helmet());
app.use(express.json());


/* --------- Routes --------- */

/**
 * Return all products
 */
app.get('/products', (req, res) => {
  // return 200 OK + products array
  res.json(products);
});

/**
 * Return product by id
 */
app.get('/products/:id', (req, res) => {
  // get param
  const id = parseInt(req.params.id);
  // find
  const product = products.find(p => p.id === id);
  // if found
  if(product){
    // return 200 OK + product
    res.json(product);
  } 
  else{ 
    // return 404 Not Found + message
    res.status(404).json({ message: 'Product not found.' });
  }
});

/**
 * Insert new product
 */
app.post('/products', (req, res) => {
  // create a new product (++ before, first increments then recovers the value)
  const newProduct = { id: ++idCounter, ...req.body };
  // add to array
  products.push(newProduct);
  // return 201 Created + product 
  res.status(201).json(newProduct);
});

/**
 * Update product
 */
app.put('/products/:id', (req, res) => {
  // get params
  const productId = parseInt(req.params.id);
  const updatedProduct = req.body;
  // find product index
  const index = products.findIndex(product => product.id === productId);
  // if not found
  if(index === -1){
    // return 404 Not Found + message
    res.status(404).json({ message: 'Product not found.' });
  }
  else{
    // updates the product using destructuring assignment
    products[index] = { ...products[index], ...updatedProduct };
    // return 200 OK + product
    res.json(products[index]);
  }
});

/**
 * Delete product
 */
app.delete('/products/:id', (req, res) => {
  // get param
  const productId = parseInt(req.params.id);
  // find product index
  const index = products.findIndex(product => product.id === productId);
  if(index === -1){
    // return 404 Not Found + message
    res.status(404).json({ message: 'Product not found.' });
  }
  else{
    // delete
    products.splice(index, 1);
    // return 200 OK + product ID
    res.json({ id: productId });
  }
});


/* --------- App start --------- */

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

#### Com esse código, agora você poderá recuperar, inserir, atualizar e excluir produtos usando os seguintes endpoints:

* **GET /products:** Retorna a lista de produtos.
* **GET /products/:id:** Retorna o produto por id. 
* **POST /products:** Adiciona um novo produto à lista.
* **PUT /products/:id:** Atualiza um produto existente na lista.
* **DELETE /products/:id:** Exclui um produto existente da lista.

Para testar as rotas **POST, PUT e DELETE** utilize a coleção desse artigo no Postman:
[https://www.postman.com/rramires/workspace/rramires-public/request/6767252-f4c683e9-c939-4e47-87b4-85d619bce6b1](https://www.postman.com/https://www.postman.com/rramires/workspace/rramires-public/request/6767252-f4c683e9-c939-4e47-87b4-85d619bce6b1)  
Caso não tenha, basta criar uma conta gratuíta.

>Esse foi um exemplo simples para inicar. Agora você tem uma API Nodejs em funcionamento com o Express. A partir daqui, você pode adicionar mais rotas, manipular solicitações POST, integrar bancos de dados e expandir sua API conforme necessário. 
O **Express** oferece uma variedade de recursos poderosos para desenvolvimento web, e você pode explorar mais recursos na documentação oficial: [https://expressjs.com](https://expressjs.com/)
Até essa parte, o commit é: **API NodeExpress final**  
Hash: fe1fd04c46b2b928261d2a3c454024f467e8b614