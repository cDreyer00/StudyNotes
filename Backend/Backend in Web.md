operador de dados de um software

## Overview

uma conexão na internet acontece através de 2 computadores, um que envia uma mensagem (request) chamado de "client" e o que recebe a mensagem chamado de "server", que pode levar uma mensagem de volta pro client (response).
Computadores não podem ser servidores por padrão, então para isso acontecer eles precisam ser configurados atráves de uma linguagem de programação backend.

## Frameworks e Package Manager

Pra transformar um computador em um servidor usando apenas uma lingaugem backend requer muito código e trabalho, ai entram os frameworks pra facilitar o trabalho. Além dos frameworks, é comum utilizar código feito por outras pessoas com features que podem ser usadas nos sistemas produzidos, esses códigos são chamados de __"packages"__ e são importados no programa através de um __"package manager"__, como "pip" para Python, "npm" pra JavaScript...

## Request-Response Cyle

Ao enviar uma mensagem pra um servidor, é necessário saber o __tipo__ de mensagem e o __endereço__ do servidor.
- Endereço:
	Composto pelo "Dominio" e a "URL path"
- Tipos
	POST - cria algo
	GET - pega uma resposta do servidor
	DELETE - cancela pedido enviado
	PUT
	PATCH
	HEAD

Todos esses tipos que o servidor permite são chamados de "API" (Application Programming Interface), caso o client envia um request não permitido pela API, o servidor vai responder um uma mensagem de erro.

REST (Representational State Transfer), convenções de nomes para os tipos utilizados no servidor

## Infraestrutura

Ao invés das empresas usarem seus próprios computadores como servidor, é mais comum alugar um computador para isso através de um "cloud computing company", como __AWS__ (Amazon Web Services, __Google Cloud Plataform__, __Microsoft Azure__...


## Microservices

Pratica de separar uma sequencia de ações de um servidores em diferentes backends, como por exemplo fazer um pedido em um site de compras, pagar pelo pedido e receber um email de confirmação.
Geralmente cada uma dessas 3 ações (fazer o pedido, pagar e receber o email) são dividias em diferentes backends, isso deixa o código menor e mais focado no objetivo que ele tem que cumprir.
Os Microserviçõs não precisam utilizar o mesmo framework e nem a mesma linguagem de programação
