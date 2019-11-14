---
layout: article
title: Slots em Vue - Como eles podem mudar (para melhor) seu modo de programar
date: 2019-11-14 09:56
tags:
  - Vue js
  - Slots
description: "Uma história de como a ideia desse blog surgiu, seus motivos e suas dificuldades."
image: "assets/posts/slots-em-vue/asset-1.jpg"
---

![um monitor com várias linhas de código](assets/posts/slots-em-vue/asset-1.jpg)

Para quem não sabe, quando entrei na minha atual empresa, a Beliive, eu pouco ou nada sabia sobre Vue js, que é o framework utilizado na empresa. Minhas informações sobre ele podiam ser resumidas em:
<br/>

- É um dos 3 grandes frameworks, junto com React e Angular
- É o mais novo dos 3
- por ser o mais novo dos 3, não havia tantas vagas de emprego para ele, na época pelo menos.

<!--more-->
<br/>
Mas bem, como eu iria precisar aprende-lo para fazer meu trabalho, mergulhei em vários cursos rápidos para poder pegar o máximo possível antes de começar no emprego. E quem diria, eu gostei **pacas** desse framework, por sua simplicidade, sua documentação extremamente bem documentada e a elegância com a qual ele abordava muitos problemas. E uma das coisas que explodiu minha mente com todas essas qualidades foi justamente os slots em Vue.

Na época, já um ou dois meses depois da minha entrada no novo emprego, eu estava tendo uma dificuldade absurda para modificar um componente. Porque, veja bem, eu componetizei muito bem a página em que estava trabalhando, pode-se dizer até que eu componetizei **demais** e agora estava tendo dificuldades com um componente específico, que antes era apenas uma imagem e um texto e agora teria que ser modificado para suportar, não apenas um texto, mas também uma lista.

Parece um problema simples, mas o componente em si tinha muitas instâncias, que mudavam não só a imagem e o texto, mas também a posição dos mesmos, o background e a cor do texto. Em resumo, colocar uma lista ali parecia uma tarefa impossível para a jovem Bianca que mal tinha começado a engatinhar no Vue e que, depois de passar uma tarde inteira batendo a cabeça, foi para a alternativa mais fácil e cretina, que foi criar outro componente praticamente igual somente para inserir uma lista naquele local específico.

Acelera para mais ou menos um mês depois disso e , enquanto investigava o código para fazer alguma outra tarefa e me deparei com um negócio meio esquisito:

```
  <componente-que-claramente-era-nosso>
      <h1>Vários html</h1>
      <p>Uns texto muito loco</p>
      <p>etc</p>
  </componente-que-claramente-era-nosso>
```

Eu olhei para aquilo e fiquei ** ue????** e resolvi dar uma investigada no ComponenteQueClaramenteEraNosso. Foi aí que eu vi.

˜pausa dramática˜

```
<!-- ComponenteQueClaramenteEraNosso.vue -->

<template>
    <section>
        <!-- vários blocos de código -->
        <slot></slot>
    </section>
</template>
```

<span class="article__muted">// Fim historinha</span>

<br/>

Mas bem, o que são os slots no Vue e por que eles são tão importantes, você deve estar se perguntando. Bom, na [documentação do Vue](https://br.vuejs.org/v2/guide/components-slots.html){:target="\_blank"} temos a seguinte explicação:

> Vue implementa uma API de distribuição de conteúdo que é modelada após o atual detalhamento da especificação dos componentes da Web, usando o elemento <slot> para servir como saída de distribuição de conteúdos.

O que isso quer dizer na prática? Que usando slots, você pode inserir um conteúdo personalizado em seu componente, sem alterar o mesmo.

```
<navigation-link url="/link">
  Conteúdo totalmente personalizado e modificável
</navigation-link>

<!-- NavigationLink.vue -->

<template>
    <a
      v-bind:href="url"
      class="nav-link"
    >
      <slot></slot>
    </a>
</template>
```

Se você leu a historinha acima, percebe que isso era exatamente o que eu estava procurando esse tempo todo e, sem saber que existia, passei uma tarde batendo a cabeça no teclado. Hoje não mais (só as vezes).

Dentro dos slots você pode por todo e qualquer tipo de html, texto e aparentemente até componentes (essa info eu acabei de descobrir lendo a documentação e vou já testar, nesse momento estava fazendo um html imenso dentro de um slot porque achava que não dava para por componentes dentro de slots - Vivendo e aprendendo).

Mas é importante informar: não é porque o slot está dentro do seu componente filho que você vai ter acesso às informações desse componente no html do componente pai. Em resumo, o código abaixo **não vai funcionar**.

```
<navigation-link url="/profile">

  <p>Clicando aqui te enviará para: {{ url }}</p>

  <!-- O `url` será undefined, porque esse conteúdo é passado
    para <navigation-link>, em vez de definido dentro do
    componente <navigation-link>. -->

</navigation-link>
```

Outras coisas que você pode fazer com slots:

### Definir um conteúdo de Fallback

Conteúdo de fallback nada mais é do que um conteúdo que será exibido caso nenhum seja, por exemplo, temos aqui um componente que é um botão que enviará um formulário:

```
<!-- SendForm.vue -->

<template>
    <button type="submit">
        <slot></slot>
    </button>
</template>
```

Podemos colocar qualquer texto dentro desse slot, mas vamos ser realistas, 99,9% das vezes o texto será um "Enviar".  Temos que colocar então em todo canto um enviar? Temos que criar uma prop para texto e, caso não tenha, colocar o texto enviar? Não, pois o Vue pensou nisso. Tudo que precisamos fazer é:

```
<!-- SendForm.vue -->

<template>
    <button type="submit">
        <slot>Enviar</slot>
    </button>
</template>
```

E pronto, caso nenhum texto seja colocado ele vai automaticamente por o conteúdo de fallback, que é o "Enviar":

```
<!-- UmOutroComponenteQualquer.vue -->

<template>
    <div>
        <send-form></send-form> <!-- um botão de submit com o texto enviar -->
        <send-form>Outro texto</send-form> <!-- o mesmo botão acima, mas agora
        com "Outro Texto" como texto -->
    </div>
</template>
```

### Slots Nomeados

Imagine que você está criando um componente de modal e gostaria que ele fosse completamente personalizado com slots. Mas você também quer manter as coisas organizadas, além de definir um estilo padrão para o header, conteúdo e footer do seu modal. Bom, com slots **você pode**! Foi para isso que foi criado um atributo especial chamado `name` que pode ser usado para definir slots adicionais:

```
<!-- Modal.vue -->

<template>
  <div>
    <div class="container">
      <header>
        <slot name="header"></slot>
      </header>

      <main>
        <slot></slot>
      </main>

      <footer>
        <slot name="footer"></slot>
      </footer>
    </div>
  </div>
</template>
```

Um `<slot>` sem o atributo name tem implicitamente o nome de "default".

E como adicionar o conteúdo a esses slots específicos? Você pode fazer isso usando a diretiva `v-slot` em um `<template>`, usando o nome como argumento, assim:

```
<modal>
  <template v-slot:header>
      <h1>Aqui pode estar um título do modal</h1>
  </template>

  <p>Aqui temos o conteúdo.</p>
  <p>Não é necessário criar um template com v-slot:default para ele
  pois qualquer conteúdo não envolvido em um '<template>' usando
  v-slot é considerado como sendo o slot default.</p>

  <small>
  Mas nada te impede de criar um template com v-slot:default,
  inclusive funciona também
  </small>

  <template v-slot:footer>
      <p>Aqui temos uma chamada e alguns botões</p>
      <button>Cancelar</button>
      <button>OK</button>
  </template>
</modal>
```

E por fim, o html renderizado desse componente ficará assim:

```
<div>
  <div class="container">
    <header>
      <h1>Aqui pode estar um título do modal</h1>
    </header>

    <main>
      <p>Aqui temos o conteúdo.</p>
      <p>
      Não é necessário criar um template com v-slot:default para ele
      pois qualquer conteúdo não envolvido em um '<template>' usando
      v-slot é considerado como sendo o slot default.
      </p>

      <small>
      Mas nada te impede de criar um template com v-slot:default,
      inclusive funciona também
      </small>
    </main>

    <footer>
      <p>Aqui temos uma chamada e alguns botões</p>
      <button>Cancelar</button>
      <button>OK</button>
    </footer>
  </div>
</div>
```

<br/>
E é isto, eu ia escrever sobre cada uma das propriedades dos slots em vue, porém olhei a documentação e, bem, são muitas, [ mas muitas propriedades](https://br.vuejs.org/v2/guide/components-slots.html){:target="\_blank"}.

Bom, espero que tenham curtido o textinho e até o próximo! :D

**OBS**: Este blog agora é open source! Então se você achou algum errinho, quer acrescentar alguma informação, qualquer coisa mesmo, [sinta-se livre para contribuir!](https://github.com/rochabianca/blog){:target="\_blank"}
