---
layout: article
title: Um jeito simples de simular erro de requests
date: 2022-05-05 15:00

tags:
  - Dicas
  - Google Webtools
image: https://rochabianca.github.io/blog/assets/posts/um-jeito-simples-de-simular-erro-requests/asset-1.jpeg
author: 'Bianca Rocha'
description: "Uma dica muito simples mas super útil para fluxos de erro"
---

![Uma página mostrando um aviso de erro de autenticação com um link embaixo para tentar logar novamente]({{ site.baseurl }}/assets/posts/um-jeito-simples-de-simular-erro-requests/asset-1.jpeg)

Esses dias estava quebrando a cabeça em como simular um request falho em uma feature que já havia implementado e acabei topando com uma dica bem legal: Você sabia que dá para bloquear requests no Inspect do Chrome (versão 63 para cima)? Achei esse recurso muito útil, e queria mostrar pra vocês. Vem aqui que te explico como fazer.

<!--more-->

Existem 2 modos de iniciar, no primeiro você vai:
- abrir o inspect
- ir para a aba de network
- selecionar um request que você quer bloquear
- clicar com o botão direito neste request
- selecionar `block request url`

e pronto, seu request estará bloqueado e a aba `network request blocking`  será aberta, mostrando todos os requests bloqueados da página.

![tela do Inspect mostrando a aba Network e a opção "Block request URL" selecionada em um dos requests]({{ site.baseurl }}/assets/posts/um-jeito-simples-de-simular-erro-requests/asset-2.png)


![Nova aba Network request blocking]({{ site.baseurl }}/assets/posts/um-jeito-simples-de-simular-erro-requests/asset-3.png)

Um outro modo de chegar nesta aba é, também na aba Network, na barra de opções, ao lado da opção "no trottling" você verá um ícone de wifi, que vai te levar as opções avançadas de wifi, ai é só selecionar a aba "Network request blocking" e lá adicionar o request que deseja bloquear.

![Aba network, barra de opções mostrando o ícone de wifi levemente mais brilhante]({{ site.baseurl }}/assets/posts/um-jeito-simples-de-simular-erro-requests/asset-4.png)

E é isso, quis fazer um post mais rápido com uma dica que achei deveras interessante, com certeza vou utiliza-la para testar fluxos de erro sem precisar mockar requisições ou ficar devolvendo promise.reject. Como você vai utilizar essa dica?