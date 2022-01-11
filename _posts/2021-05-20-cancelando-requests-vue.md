---
layout: article
title: Como cancelar requests ao digitar na barra de pesquisa
date: 2021-05-20 16:15

tags:
  - Axios
  - Vuejs
  - Vuex
image: https://rochabianca.github.io/blog/assets/posts/cancelando-requests-vue/asset-1.png
author: 'Bianca Rocha'
description: "Quer saber como cancelar um request na sua barra de pesquisa quando o usuário digitar outro caractere? Pois cola aqui que talvez eu possa te ajudar"
---

![Parte de network do inspecionar do chrome mostrando vários requests 'search' cancelados e um com status 200]({{ site.baseurl }}/assets/posts/cancelando-requests-vue/asset-1.png)

Vamos lá, você está fazendo um input de pesquisa que vai atualizar a cada palavra digitada e quer cancelar o request anterior quando uma nova palavra for digitada, assim não sobrecarregando seu backend? Pois eu tenho a solução! (talvez não seja a melhooor solução, mas é o que achei)

<!--more-->

O código a seguir está em Vue, mas acho que se você trabalha com React não vai ser nada muito diferente (na verdade tem um artigo melhor que o meu explicando como fazer em react, então se você entende inglês da uma olhada [aqui](https://www.codingdeft.com/posts/axios-cancel-previous-request-react/){:target="\_blank"}. E se você trabalha com Angular aparentemente ele já tem uma solução pra isso chamada `switchMap`. Dito tudo isso, vamos ao código.

Primeiramente você vai precisar importar o axios no script do seu componente:

```
// Search.vue

import axios from 'axios'

export default {
...
}
```

Então vamos precisar criar uma variável `cancelToken` no  data, com o valor inicial `undefined` :

```
data() {
  return {
    cancelToken: undefined,
  }
}
```

Aí, na função onde você for fazer a chamada para a pesquisa, você vai adicionar as seguintes linhas:

```
methods: {
  search(query) {
    // Esse if serve para verificar se não existe nenhum request anterior pendente.
    // Caso exista ele vai cancela-lo (a mensagem é opcional)
    if (typeof this.cancelToken !== typeof undefined) {
      this.cancelToken.cancel("Operation canceled due to new request.")
    }

    // A seguir a gente salva o token de cancelamento do request atual
    this.cancelToken = axios.CancelToken.source()

    // E ai você vai mandar esse token no seu dispatch (assumindo que você esteja usando vuex)
    this.$store.dispatch('search_term', {
      query,
      cancel: this.cancelToken.token
    })
  }
}
```

Então, lá onde esta função vai estar na sua store, você vai adicionar o `cancelToken` na sua chamada para o axios:

```
// search.js

import axios from 'axios'

// ...
actions: {
  search_term({}, payload) {
    // Aqui eu estou fazendo um get, mas funciona em post também
    axios.get('search',
     { query: payload.query },
     { cancelToken: payload.cancel })
    .then(res => {
      // ...
    })
  }
}
// ...
```

E é basicamente isso! Eu deixei algumas coisas de fora para o código ficar o mais focado possivel, mas espero que tenha dado para entender. Qualquer coisa pode comentar que eu ajeito aqui e se você tiver uma solução melhor comenta aí tbm que estamos todos aqui pra aprender. Até a próxima aí galera!