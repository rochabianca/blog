---
layout: article
title: Como monitorar graphql requests no Cypress quando o request é um GET
date: 2022-05-24 11:48

tags:
  - Dicas
  - Cypress
  - GraphQL
  - GET
image: https://rochabianca.github.io/blog/assets/posts/como-monitorar-graphql-requests-no-cypress-quando-request-get/asset-1.jpeg
author: 'Bianca Rocha'
description: "Um modo de monitorar requests no cypress quando sua chamada graphql não é o convencional POST"
---

![Uma IDLE mostrando códigos de testes]({{ site.baseurl }}/assets/posts/como-monitorar-graphql-requests-no-cypress-quando-request-get/asset-1.jpeg)

Recentemente aprendi uma ferramenta muito útil no Cypress, que é o `cy.intercept` . Ele me permite, entre outras coisas interceptar requests feitas, e esperar por elas antes de fazer uma ação. É bem mais sofisticado que usar um cy.wait(1000) e ajuda bastante quando você tem uma request em particular que demora muito para terminar.

<!--more-->

````
cy.intercept('POST', `${Cypress.env('api')}/login`).as('auth')
cy.wait('@auth')
// Ações que só podem ser executadas depois da request auth
````

Só que quando você usa GraphQL as coisas ficam um pouco mais complicadas. Felizmente o próprio Cypress tem um guia muito bom sobre como implementar o intercept em GraphQL quando a request é um POST, que vou deixar [aqui](https://docs.cypress.io/guides/testing-strategies/working-with-graphql).

Só que, para meu azar, o modo que as requests eram feitas no projeto que estava trabalhando utilizava GET em vez de POST e isso fazia com que o guia acima não me ajudasse muito. Então, após alguns dias de tudo dando errado, fui obrigada a tomar medidas desesperadas, porém efetivas: Usar regex.

A lógica era simples: minha api graphql era sempre `https://site-da-api.com.br/graphql` e como o request era um GET, o nome da query iria sempre aparecer em algum lugar do request. Então utilizei o regex para detectar as ocorrências de `graphql` e o nome da minha query (armazenada em uma variável) e, por fim, era só dar um alias para o comando, assim como é feito em chamadas rest, e criar um comando personalizado para facilitar o uso. Ficou assim no final:

````
Cypress.Commands.add('interceptGraphqlGET', (query) => {
	const regex = new RegExp(
    '\\bgraphql\\b.*\\b' + query + '\\b' // Equivalente à /\bgraphql\b.*\bQueryExemplo\b/
  )
  cy.intercept(regex).as(`gql${query}`)
})
````

Aí se eu quiser interceptar e esperar uma chamada GET em qualquer local dos meus testes vai ser só chamar:

````
cy.interceptGraphqlGET('QueryExemplo')
cy.wait('@gqlQueryExemplo')
// faça alguma coisa
````

E aí, curtiu a solução? Ou tem uma muito melhor para mostrar? Comenta aí o que achou e até a próxima :D