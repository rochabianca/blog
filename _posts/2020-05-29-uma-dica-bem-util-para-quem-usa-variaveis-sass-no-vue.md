---
layout: article
title: 'Usa variáveis sass no Vue? Posso ter uma dica bem útil pra você'
date: 2020-05-29 12:15
author:
tags:
  - Dicas
  - VueJS
  - Sass
image: 'assets/posts/uma-dica-bem-util-para-quem-usa-variaveis-sass-no-vue/asset-1.jpg'
description: "Nesse post eu falo sobre como importar um arquivo de variáveis sass em todos os componentes de um aplicativo Vue, sem ter que importar manualmente"
---

![imagem de várias linhas de código CSS]({{ site.baseurl }}/assets/posts/uma-dica-bem-util-para-quem-usa-variaveis-sass-no-vue/asset-1.jpg)

Faz um bom tempo que, na empresa onde trabalho, utilizamos um arquivo geral de variáveis sass para definir as cores do sistema. Desde então, o que fazíamos era importar manualmente o arquivo de variáveis para cada componente, cheguei até a criar um snippet no vue para fazer isso por mim toda vez que eu criava um componente. Só que isso está longe de ser uma solução ideal.

<!--more-->

O primeiro que essa abordagem gerava era que ela dependia que todos os meus colegas lembrassem de importar as variáveis, ou usassem meu snippet. E o segundo problema era que tudo bem, enquanto fossem apenas variáveis no arquivo esse tipo de abordagem não complicaria muito o tamanho do bundle final, uma vez que, ao ser compilado, a única coisa que aconteceria é que as variáveis seriam substituídas por seus respectivos valores e nenhum código css seria adicionado. Mas e se alguém adicionasse um código css ali por engano? Dependendo do código isso poderia impactar seriamente o bundle final da aplicação. Por conta disso, eu estava procurando uma solução mais aceitável para esse problema, e acabei topando com [essa pergunta no Stack Overflow](https://stackoverflow.com/questions/35580710/using-sass-variables-in-a-vuejs-component){:target="\_blank"}.

E qual a solução que eu achei nessa pergunta? Bem simples, na real a única coisa que você precisa fazer é adicionar o código abaixo ao seu `vue.config.js`:

```
module.exports = {
  css: {
    loaderOptions: {
      sass: {
        data: '@import "@/pathto/variables.scss";'
      }
    }
  }
};
```

Alguns pontos importantes:
- Se você está usando o `sass-loader 8`, substitua o `data` por `prependData`;
- É necessário reiniciar seu servidor para que essas mudanças se apliquem;
- Essas mudanças não irão funcionar se você não colocar `lang="scss"` (ou qualquer outro pré processador que esteja usando) na tag style do seu componente Vue.

<br/>

E prontinho! Agora você pode usar suas variáveis sass em qualquer componente sem ter que importar! Abaixo você vai encontrar um [exemplo feito pela @sdras desse código funcionando e mudando a cor primária do texto para roxo](https://codesandbox.io/s/936omxkqro?from-embed){:target="\_blank"}:

<iframe
  src="https://codesandbox.io/embed/936omxkqro?autoresize=1&fontsize=14&moduleview=1&theme=dark"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="Import Syle Variables in every Vue Component"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-autoplay allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
>
</iframe>

<br/>

E é isso, eu espero que essa dica tenha te sido útil para você. Até a próxima! :D

<br>

Links que foram essenciais para a criação desse texto:
- [O texto do CSS Tricks sobre como importar um arquivo Sass em todos componentes Vue de um app](https://css-tricks.com/how-to-import-a-sass-file-into-every-vue-component-in-an-app/){:target="\_blank"}
- [O exemplo criado pela @sdras no CodeSandbox](https://codesandbox.io/s/936omxkqro?from-embed=&file=/src/App.vue){:target="\_blank"}