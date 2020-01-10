---
layout: article
title: Um pouco de porquê esse blog existe
date: 2019-10-08 09:31
tags:
  - Happy Hour
description: 'Uma história de como a ideia desse blog surgiu, seus motivos e suas dificuldades.'
image: 'assets/posts/porque-esse-blog-existe/asset-1.jpg'
---

![Um computador com um caderno e caneta a sua frente, ao lado uma caneca com chá e um vaso de flores]({{ site.baseurl }}/assets/posts/porque-esse-blog-existe/asset-1.jpg)

Faz um tempinho que migrei para cá e admito que tem muita coisa que não sei ainda, ou que não faço direito. Por exemplo, eu estou criando esse texto na branch gh-pages, o que quer dizer que eu não posso commita-lo até terminar, e não posso mudar para a master porque não commitei nada (fora que nem sei como tá a master). Vivendo e aprendendo, não é mesmo?

<!--more-->

Mas por que se dar a todo um trabalho de criar um blog, o medium já não estava bom o bastante? Bem, estava. Na real eu sou uma pessoa bem preguiçosa quando se trata de projetos pessoais, em parte porque (lá vem aquela frase bem brega de entrevista) eu sou muito perfecionista com meus projetos. Eu quero fazer isso, fazer aquilo, integrar com o firebase, usar a escala musical para definir os espaços, fazer um editor igual o do medium, usar vuejs e bem, eu já falei que também sou bem preguiçosa né? O resultado dessa combinação era que eu tinha planos muito bons e zero saco para bota-los em prática.

Mas aí aconteceram duas coisas. A primeira foi a [briga do Medium com o FreeCodeCamp](https://wptavern.com/freecodecamp-moves-off-of-medium-after-being-pressured-to-put-articles-behind-paywalls){:target="\_blank"}. Nas palavras do fundador do FreeCodeCamp, Quincy Larson e em tradução livre:

> "No ano passado, o Medium se tornou mais agressivo conosco. Eles nos pressionaram a colocar nossos artigos atrás de suas paywalls. Nós recusamos. Então eles tentaram nos comprar. (O que não faz nenhum sentido. Somos uma instituição de caridade pública.) Recusamos. Então eles começaram a nos ameaçar com um advogado.

Isso para mim é um exemplo de como o capitalismo pode deixar as pessoas meio loucas. O [FreeCodeCamp](https://www.freecodecamp.org/){:target="\_blank"} é um projeto incrível para quem quer aprender, eles explicam muito bem as coisas e existem inúmeros exemplos de prática, vai mais fundo até que alguns cursos que eu paguei para fazer. Mas por ser tão lido no médium (na época dessa briga, o FreeCodeCamp sozinho era responsável por 5% do trafego do Medium), o médium viu isso nada mais do que como uma boa oportunidade de lucrar mais. Uma oportunidade pelo qual valeria a pena subornar e ameaçar uma instituição de caridade.

E não me leve a mal, lucro é importante. Nenhuma empresa, por melhor que seja, vai durar muito sem ter lucro o bastante para se sustentar. Mas pisar em cima de instituições de caridade ou mesmo nos direitos e na dignidade dos seus trabalhadores a meu ver é um jeito mesquinho de se lidar com isso.

Dito isso, claro, existem situações e situações. Eu não vou te falar aqui que você deve abolir o medium da sua vida e criar seu próprio blog do zero. Para você, pode ser mil vezes mais complicado fazer isso, você pode estar começando agora a escrever e querer testar coisas antes de dar um passo tão grande, pode escrever para a sua empresa e <b>ta tudo bem</b>. O objetivo desse texto não é te dizer para criar seu próprio blog (por mais que eu esteja planejando fazer um mini tutorial disso no futuro) sou só eu falando os motivos que me levaram a criar este blog em específico. Meus próprios textos no médium vão continuar lá, porque eu também penso que meus textos podem ter ajudado alguém em algum momento e seria um saco para essa pessoa voltar lá e encontrar uma página 404 sem ter ideia do que raios aconteceu.

Bom, depois de decidir montar um blog faltava só o como. Como eu disse, sendo eu uma pessoa perfeccionista E preguiçosa eu queria um jeito simples, prático e rapido, mas que fosse de fácil de personalizar. Foi aí que eu achei [esse repositorio](https://github.com/mathieudutour/medium-to-own-blog){:target="\_blank"} que propunha exatamente isso. Basicamente ele criava um site estático com Gatsby onde você escrevia usando markdown (ou MDX) e era isso. Simples, não?

### foi um completo desastre

Pra começar eu não manjo **nada** de Gatsby. Até esse momento eu não sei nem escrever direito o nome desse negócio sem olhar na internet antes porque minha cabeça lê Gastsby e eu sempre escrevo isso se não prestar atenção, ai eu vou pesquisar como fazer algo em **gastsby** e não encontro nada, pq nem o Google entende meu retardo mental.

E o fato que lembra (acho que é feito, não sei) React não me ajuda também, uma vez que eu não vejo React desde que estava procurando um trabalho em React, ou seja, **a muito tempo**.

Em resumo, eu consegui fazer algumas mudanças e elas me custaram um pouco da minha sanidade, pois sendo uma pessoa preguiçosa eu tentei fazer as coisas na marra, mesmo sabendo que estudar Gatsby seria um caminho mais rápido (não façam isso em casa, crianças) e até que o layout estava aceitável, só tinha alguns problemas:

- Eu queria publicar no github pages
- Alguns espaçamentos estavam malucos **e eu não tinha ideia do porquê**
- Não tinha como o leitor interagir ainda.

Mas por que o Github Pages você deve estar se perguntando. É por ser gratuito? Não caro developer, era por um motivo muito mais fútil, mas na minha cabeça essencial: **eu acho o dominio .github.io muito bonito**. Muito mais bonitinho que qualquer outro domínio gratuito. E ai começou minha odisseia. No fim, eu consegui, a muito custo, colocar o código no Github pages e ajeitar os espaçamentos, porém eu também consegui **sumir com as imagens de todos os posts**, aliais, eu consegui o grande feito de **sumir com os posts também**. Foi nessa hora que começou a passar pela minha cabeça que talvez fosse melhor construir meu blog de outro modo, antes que eu tenha um ataque de estresse, de preferência. Foi então que, depois de tentar fazer aquele super projeto com vue/firebase/editor do medium/etc e desistir, eu dei de cara com a segunda coisa que me fez criar esse blog.

E a segunda coisa foi [o curso do Willian Justen sobre como fazer um blog com Jekyll](https://www.udemy.com/course/criando-sites-estaticos-com-jekyll/){:target="\_blank"} (não é ad, eu juro). Era um curso curto, gratuito e que o projeto era justamente fazer um blog, com sessão de comentários e tudo. E, além disso, era feito usando Ruby e Sass, duas ferramentas com as quais eu já tinha experiência.

E no fim foi muito mais fácil e, o melhor de tudo, **muito mais divertido**. Aprendi um monte, fiz um negócio bonito e funcional de modo simples e consegui transferir meus textos para lá sem muita dor de cabeça, o que me deu muito orgulho. Claro que tem um monte de coisas que eu ainda preciso melhorar e um monte que eu não faço ideia de como fazer, mas isso vai ficar para os próximos capítulos.

E esse texto na verdade era para ter sido uma introdução ao tutorial de como fazer seu próprio blog nesse estilo, mas eu acabei enrolando tanto que virou um texto por si só e acabou sendo bem legal de fazer. Me digam ai nos comentários se curtiram, quem sabe eu não trago mais uns devaneios assim.

Muito obrigada se você leu até aqui e até o próximo texto :D
