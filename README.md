# ReactPHP

## PHP assíncrono e reativo

Algumas alternativas

## O que é o ReactPHP?

ReactPHP é uma biblioteca de baixo nível para programação orientada a eventos em PHP.

No seu núcleo está um loop de eventos, em cima do qual fornece utilitários de baixo nível, tais como: abstração de fluxos, resolução DNS assíncrona, cliente/servidor de rede, cliente/servidor http, interação com processos.

Bibliotecas de terceiros podem usar esses componentes para criar clientes/servidores de rede assíncrona e muito mais.

A palavra chave em React é assíncrono. Esta é a maior ideia por trás da coleção de bibliotecas que vemos consigo. PHP, por natureza, é dito "bloqueante". Isto significa que cada procedimento só virá a ser executado após o anterior.

Exemplo:

```php
echo 'Obtendo o arquivo...';
// Executa somente após a linha 3
$conteudo = file_get_contents('umArquivoPesado.txt');
// Executa somente após a linha 5, e assim por diante...
if ($conteudo) {
    echo 'Arquivo obtido com sucesso! :)';
}
```
Estamos de fato acostumados com este cenário. Porém isto passa a ser problemático quando umArquivoPesado.txt leva alguns segundos para ser carregado à memória.

O ponto é: PHP bloqueia a cada comando executado e os comandos que fazem entrada/saída (acesso a disco, acesso a rede...) de dados tendem a ser mais demorados que comandos internos de processamento (um echo, um if, um cálculo...).

React PHP vem com o intuito, justamente, de permitir que executemos pedaços de lógica em paralelo. Nada que não pudesse ser feito com PHP antes, mas React traz uma interface orientada a objetos muito bem organizada e que nos facilita esta utilização.

Mais detalhes em:
- https://phpsp.org.br/artigos/react-php-conceitos-basicos-eventloop/
- https://www.treinaweb.com.br/blog/introducao-a-programacao-assincrona-em-php-usando-o-reactphp


## Pequeno Hello World em ReactPHP

Crie uma pasta e a acesse

Então execute:
```php
composer require react/http react/socket
```
Criar um index.php contendo:
```php
<?php
require 'vendor/autoload.php';

require __DIR__ . '/vendor/autoload.php';

$http = new React\Http\HttpServer(function (Psr\Http\Message\ServerRequestInterface $request) {
    return React\Http\Message\Response::plaintext(
        "Hello World!\n"
    );
});

$socket = new React\Socket\SocketServer('127.0.0.1:8080');
$http->listen($socket);

echo "Server running at http://127.0.0.1:8080" . PHP_EOL;
```
Executar
```php
php index.php
```

## Exemplo semelhante com NodeJS:

Crie uma papsta e a acesse
```php
npm init -y

npm install
```
Criar index.js
```php
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
Executar
```php
node index
```

## Exemplo criado com o FrameworkX

Criar uma pasta e acessá-la

Executar
```php
composer require clue/framework-x:dev-main
```
Criar a pasta public e acessá-la

Criar o index.php contendo:
```php
<?php

require __DIR__ . '/../vendor/autoload.php';

$app = new FrameworkX\App();

$app->get('/', function () {
    return React\Http\Message\Response::plaintext(
        "Hello wörld!\n"
    );
});

$app->get('/users/{name}', function (Psr\Http\Message\ServerRequestInterface $request) {
    return React\Http\Message\Response::plaintext(
        "Hello " . $request->getAttribute('name') . "!\n"
    );
});

$app->run();
```
No raiz executar
```php
php public/index.php

http://127.0.0.1:8080/

http://127.0.0.1:8080/users/RibaFS
```

## Node.js vs ReactPHP

Os desenvolvedores descrevem o Node.js como "uma plataforma construída no tempo de execução JavaScript do Chrome para criar facilmente aplicativos de rede rápidos e escaláveis". O Node.js usa um modelo de E/S sem bloqueio e orientado a eventos que o torna leve e eficiente, perfeito para aplicativos em tempo real com uso intenso de dados executados em dispositivos distribuídos. 

Por outro lado, o ReactPHP é detalhado como "E/S não bloqueante e orientada a eventos com PHP". Uma biblioteca de baixo nível para programação orientada a eventos em PHP. Em seu núcleo está um loop de eventos, no topo do qual fornece utilitários de baixo nível.

O Node.js pode ser classificado como uma ferramenta na categoria "Frameworks (Full Stack)", enquanto o ReactPHP é agrupado em "Servidores Web".


## Pequeno CRUD em ReactPHP na linha de comando

https://github.com/ribafs/reactphp-simple-crud

## Alternativas para o ReactPHP

- https://github.com/ReactiveX/RxPHP
- https://framework-x.org/
- https://github.com/clue/framework-x
- https://github.com/ratchetphp/Ratchet
- https://github.com/amphp/amp
- https://github.com/thephpleague/event
- https://github.com/igorw/evenement
- https://github.com/recoilphp/recoil


## Referências

- http://reactphp.org/
- https://github.com/reactphp/reactphp
- https://phpsp.org.br/artigos/react-php-conceitos-basicos-eventloop/
- https://www.treinaweb.com.br/blog/introducao-a-programacao-assincrona-em-php-usando-o-reactphp
