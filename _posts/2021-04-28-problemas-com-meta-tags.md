---
layout: article
title: Problemas com meta tags? Vem cá que eu te ajudo
date: 2021-04-28 10:11
tags:
  - Dicas
  - SEO
  - Meta tags
image: https://rochabianca.github.io/blog/assets/posts/problemas-com-meta-tags/asset-1.jpeg
author: 'Bianca Rocha'
description: "Pode não resolver todos os seus problemas, mas vai facilitar BASTANTE"
---

![Eu juro pra vocês que eu tento botar outra imagem que não seja de código, mas é difícil]({{ site.baseurl }}/assets/posts/problemas-com-meta-tags/asset-1.jpeg)

Eu passei algum tempo das ultimas semanas desenvolvendo uma landing page para a empresa que estou trabalhando. QA vai QA vem, finalmente chegou a hora de mandar o negócio para a produção. Só que ai me veio meu primeiro problema. Durante todos esses anos eu só sabia fazer um tipo de meta tag, que é esse tipo aqui:

<!--more-->

![imagem mostrando um preview consistente de um texto e uma imagem pequena ao lado]({{ site.baseurl }}/assets/posts/problemas-com-meta-tags/asset-2.png)

Enquanto isso quebra um galho obviamente não é tão bonito quanto aqueles previews com uma imagem gigante. E era exatamente isso que a minha empresa queria para a nova landing page.  Algo mais nesse estilo aqui:

![imagem mostrando um preview mais em formato de post, com uma imagem maior em cima e o titulo e texto embaixo, além do endereço do website]({{ site.baseurl }}/assets/posts/problemas-com-meta-tags/asset-3.png)

Pois bem, como faz um negócio desses? Eu passei um dia inteiro procurando mas, além de não ter muita informação online de como fazer esse card específico a cada teste eu tinha que fazer o deploy do site para então ver os resultados. Até que eu achei [Esse site aqui](https://www.heymeta.com/){:target="\_blank"}

Com ele você pode inserir o endereço do seu website e ele vai detectar as meta tags e mostrar o que ele identificou e aí você pode corrigir essas informações lá na hora. Um exemplo, ao por o meu último post, isso é o que ele detecta:

![as informações detectadas pelo website sobre o meu blog, incluindo titulo, descrição e imagem]({{ site.baseurl }}/assets/posts/problemas-com-meta-tags/asset-4.png)

Se algo estiver errado eu posso editar essas informações, ai lá embaixo o site me dá a opção para gerar as meta tags, e assim obter o resultado que eu queria:

![Parte do site onde você pode gerar as meta tags do seu site com as informações da imagem anterior]({{ site.baseurl }}/assets/posts/problemas-com-meta-tags/asset-5.png)

Aí é só copiar esse código no seu `<head>` e ser feliz 😄

Agora só falta eu achar um tempo pra implementar isso aqui...