---
layout: article
title: Um jeito simples de manipular a altura de um textarea (autosize.js)
date: 2020-01-20 16:58
tags:
  - Utilidades
  - Tutoriais

description: "Nesse mini tutorial explico um jeito bem simples de fazer uma textarea que se adequa ao texto do usuário, usando o script autosize.js"
image: "assets/posts/um-jeito-simples-de-manipular-a-altura-do-textarea/asset-1.jpg"
---
![um print do codepen abaixo dizendo: textarea com auto resize; escreva e veja as linhas do textarea se formando de acordo com o tamanho do seu texto (Enter tbm funciona); e no textarea escrito "um texto em uma textarea com resize (vale para textos muito longos que quebram a linha também viu?)", cada palavra separada por enter]({{ site.baseurl }}/assets/posts/um-jeito-simples-de-manipular-a-altura-do-textarea/asset-1.jpg)

Uma coisa bem simples, mas que tenho julgado cada vez mais padrão na web, é a capacidade de fazer os inputs (textareas na verdade) de texto se adequarem ao texto em que o usuário digita, a medida que o mesmo vai digitando. Afinal nessa época em que textões e threads estão se tornando cada vez mais comuns, seria um estresse a mais para o usuário revisar esse texto quando ele está contido em uma única linha gigante.

<!--more-->

Bom, recentemente eu precisei implementar esta funcionalidade em uma das features em que estou trabalhando, porém não lembrava de jeito nenhum qual era o nome da bendita. Depois de algumas várias pesquisas, descobri como se chama: autosize. E agora vou ensinar para vocês um jeito simples de implementá-la.

Em resumo, existe um pequeno script (pequeno mesmo, a build tem apenas 3.5kb) chamado [autosize](https://github.com/jackmoore/autosize){:target="\_blank"} que torna o processo todo incrivelmente simples. Você pode usar o npm para instalá-lo no seu projeto:

```
npm install autosize
```

Depois disso o processo todo é bem simples, e aqui vou usar o Vue como framework, mas é possível adaptar esse código para qualquer framework do seu gosto

```
<template>
  <textarea
    rows="1"
    placeholder="Escreva aqui"
    class="resized-textarea"
  />
</template>

<script>
import autosize from 'autosize';

export default {
  mounted() {
    autosize(document.querySelector('.post__comment__input'));
  },
};
</script>
```

<br/>

E o resultado final é esse:


<p class="codepen" data-height="364" data-theme-id="dark" data-default-tab="js,result" data-user="rochabianca" data-slug-hash="BayGOwV" style="height: 364px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Textarea com autoresize (Vuejs)">
  <span>See the Pen <a href="https://codepen.io/rochabianca/pen/BayGOwV">
  Textarea com autoresize (Vuejs)</a> by Bianca (<a href="https://codepen.io/rochabianca">@rochabianca</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<br/>

Você também pode ver mais opções e configurações no [github do script](https://github.com/jackmoore/autosize){:target="\_blank"}.

<br/>

No mais é isso, espero que tenham curtido o mini tutorial, e até a próxima :D