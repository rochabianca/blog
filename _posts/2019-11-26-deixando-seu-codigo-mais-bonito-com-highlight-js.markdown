---
layout: article
title: Deixando seu código mais bonito com highlight.js
date: 2019-11-26 14:03
tags:
  - Highlight.js
  - Utilidades
  - Tutoriais
image: "assets/posts/highlight-js/asset-1.jpg"
description: 'Tenho adotado uma maneira bem prática para ir adicionando as novas funções neste blog: o famigerado "quando eu precisar eu vejo" o que funciona bastante para evitar ter dor de cabeça antes da hora, mas infelizmente também quer dizer que eu vou ter que sair implementando coisa antes de fazer um post'
---

![um monitor com o código a mostra](assets/posts/highlight-js/asset-1.jpg)

Tenho adotado uma maneira bem prática para ir adicionando as novas funções neste blog: o famigerado "quando eu precisar eu vejo" o que funciona bastante para evitar ter dor de cabeça antes da hora, mas infelizmente também quer dizer que eu vou ter que sair implementando coisa antes de fazer um post, [o que foi o caso do último post](https://rochabianca.github.io/blog/slots-em-vue){:target="\_blank"} onde eu vi pela primeira vez o padrão das tags `<code>` e de cara não agradou nada a minha vista.

<!--more-->

Até então eu nunca tinha mexido com esse tipo de tag e achei que era automático o highlight dos códigos, o que obviamente não era o caso. Como estava olhando a documentação do vue na hora e eles tinham uma tag code muito bonitinha, fui lá inspecionar pra ver qual era. Então achei essas tags aqui:

![print da documentação do Vue js sobre a parte de slots, com a aba inspencionar aberta, mostrando o código da tag 'code' e suas classes](assets/posts/highlight-js/asset-2.png)

Uma rápida pesquisa no google por esse hljs me deu o nome do que eles estavam usando: uma lib chamada Highlight.js. E pesquisando mais um pouco eu descobri que ela é muito simples de usar, como irei explicar agora.

## Usando o Highlight.js

O processo para usar o highlight.js é bem simples, mas primeiramente é bom que você saiba onde exatamente você quer colocá-lo. Se você está fazendo um blog como eu, provavelmente vale mais a pena colocar o css e js dele no template do seus posts, em vez de no index.html, visto que ele muito provavelmente só irá aparecer lá. Aí você cola o link do cnd dele, tanto o css quanto o js

```
<!-- Esse é o css do estilo, nesse caso o do github -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/styles/github.min.css">

<!-- E aqui o js, que é onde a mágica acontece -->
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```

E, essencialmente é isso, você já pode ter uma tag code funcional com o estilo selecionado, assim ó:

![print do estilo 'github' no highlight.js](assets/posts/highlight-js/asset-3.png)

[Para ver os estilos disponíveis basta clicar aqui](https://highlightjs.org/static/demo/){:target="\_blank"} e escolher o que você achar que mais combina com o seu site. Então você pode procurar o link do cnd, [procurando pelo nome do estilo que você escolheu neste site](https://cdnjs.com/libraries/highlight.js/){:target="\_blank"} aí é só alterar a tag link mostrada mais cedo.

## Mas e se eu quiser um estilo personalizado?

Se você é como eu e não conseguiu se dar por satisfeito com os mais de 150 temas disponíveis calma, que temos solução pra isso também. Nesse caso, você pode alterar o css das tags, fazendo um estilo personalizado. Aqui estão as classes que eu alterei para fazer esse estilo aqui:

```
.hljs {
  background: #f2f2fd;
  color: #0c080b;
}
.hljs-tag,
.hljs-name,
.hljs-attribute {
  color: #4d12a1;
}
.hljs-string,
.hljs-doctag {
  color: #cd50af;
}
.hljs-number,
.hljs-literal,
.hljs-variable,
.hljs-template-variable,
.hljs-tag .hljs-attr {
  color: #5eb59a;
}
.hljs-comment,
.hljs-quote {
  color: #9c92aa;
}
```

E o resultado você pode ver acima. E aí, curtiu?

#### Os seguintes links foram essenciais para a criação desse post:

- [Site do Highlight.js](https://highlightjs.org/){:target="\_blank"}
- [Code highlighting in Jekyll blog using highlight.js](http://www.vishalsinha.in/2017/04/23/highlight-code-jekyll.html){:target="\_blank"}
