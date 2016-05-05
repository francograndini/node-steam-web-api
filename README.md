# Steam Web API para Node.js e io.js

Isto é um compilado de node para Steam Web API extremamente simples. É completamente experimental e a API provavelmente mudará.

# Instalação

`npm install steam-web-api`

# Uso

O módulo exporta uma unica função `getInterface`.

```js
var getInterface = require('steam-web-api');
```

Chame isso com uma interface de nome Web API e uma API key opcional.

```js
var steamRemoteStorage = getInterface('ISteamRemoteStorage');
// or
var steamRemoteStorage = getInterface('ISteamRemoteStorage', 'API KEY');
```

Ele retorna um objeto com duas propriedades: `get` e `post`. Ambas são funçoes que aceitam os seguintes argumentos:

* Method name, e.g. `'GetCollectionDetails'`.
* Method version, e.g. `1`.
* Objetos com os parametros que serao serializados em uma rede de consulta. Multiplos valores (e.g. for "publishedfileids") podem passar várias ordens. Diferente de outros módulos de rede de consulta, esse suporta dados binarios (como buffers) usados em AuthenticateUser.
* Callback. O primeiro argumento no codigo de status, o segundo argumento é a resposta do JSON analisada se o codigo de status é 200.

`get` manda um pedido de GET, `post` manda um pedido de POST. Ele tenta de novo automaticamente em erros de conexao.

```js
steamRemoteStorage.get('GetUGCFileDetails', 1, {
  ugcid: '534000675759633498',
  appid: 767
}, function(statusCode, response) {
  if (statusCode == 200)
    console.log(response);
});

steamRemoteStorage.post('GetPublishedFileDetails', 1, {
  itemcount: 2,
  publishedfileids: ['406121458', '425876040']
}, function(statusCode, response) {
  if (statusCode == 200)
    console.log(response);
});
```
