---
layout: article
title: Facilite sua vida, crie Snippets
date: 2022-03-21 16:27

tags:
  - Dicas
  - Vscode
image: https://rochabianca.github.io/blog/assets/posts/facilite-sua-vida-com-snippets/asset-1.jpeg
author: 'Bianca Rocha'
description: "O que são Snippets, o que fazem, como podem facilitar minha vida? Aqui mesmo no Bianca Reporter"
---

![Um computador sobre uma mesa de madeira em que um pé está apoiado]({{ site.baseurl }}/assets/posts/facilite-sua-vida-com-snippets/asset-1.jpeg)

No decorrer da sua carreira você eventualmente vai encontrar com pedaços de códigos que são repetidos várias e várias vezes, mas que são específicos a sua empresa ou seu projeto.

Um exemplo disso seria um componente de ícones, onde você teria o componente base, com as tags svg iniciais além de algumas propriedades e o componente que definirá qual ícone o componente base vai compilar. O componente de ícone tem um template, com seu html, propriedades e estilo, mas o conteúdo dele será sempre diferente. A questão que fica é: como fazer com que a criação de novos componentes seguindo esse template não se torne um tedioso copia e cola?

É aqui que entram os snippets.

<!--more-->

Snippets são blocos de códigos que podem ser acessados por um atalho no seu editor de código. Por um exemplo, quando você digita `!`  no seu arquivo html e vê um atalho para criar toda uma estrutura html no seu arquivo, aquilo é um snippet

![Um arquivo em html no vscode com ! digitado, mostrando os atalhos do mencionado acima]({{ site.baseurl }}/assets/posts/facilite-sua-vida-com-snippets/asset-2.png)

Você também pode criar snippets customizados, para isso basta ir (no vscode) em `Preferences > User Snippets` e então selecionar a linguagem que você quer criar seus snippets

![Tela de snippets, mostrando todas as linguagens disponíveis para a criação de snippets]({{ site.baseurl }}/assets/posts/facilite-sua-vida-com-snippets/asset-3.png)

A partir daí é só seguir o template que vai aparecer nos comentários do arquivo e criar seus próprios snippets. Um exemplo disso é [um snippet que criei a um tempo atrás](https://gist.github.com/rochabianca/2c39f611b28dfb51f0fb3ff483afbf51){:target="\_blank"} para trazer de volta o scaffold nos arquivos vue, uma vez que o mesmo havia sido retirado (renomeado na verdade) do Vetur:

```
{
	"bring back the scaffold to vue files": {
		"prefix": "scaffold",
		"body": [
			"<template>",
			"  <div>$TM_FILENAME_BASE</div>",
			"</template>",
			"",
			"<script>",
			"export default {",
			"  name: '$TM_FILENAME_BASE',",
			"};",
			"</script>",
			"",
			"<style>",
			"</style>",
			""
		],
		"description": "bring back the scaffold to vue files"
	}
}
```

Para utilizar esse atalho agora você só precisa digitar ``scaffold`` no seu arquivo vue que ele deve aparecer.

O ``$TM_FILENAME_BASE``  é uma variável do Vscode que me devolve o nome do arquivo sem sua extensão, por exemplo, se o nome do componente é "Exemplo.vue" ele me retorna apenas "Exemplo". Você pode ver a lista de variáveis do vscode [aqui](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variables){:target="\_blank"}.

O ideal é que você crie um snippet sempre que notar que está copiando e colando muito um trecho de código. Uma outra dica muito boa é que você pode criar snippets específicos para o projeto em que está trabalhando, assim tanto você quanto seus colegas podem ter acesso aos atalhos.

Para isso, você precisa criar, dentro da sua pasta ``.vscode`` (se ela não existir você pode cria-la) um arquivo com o nome dos arquivos nos quais o snippet vai aparecer com a extensão ``.code-snippets``  (por exemplo arquivos vue seriam nomeados ``vue.code-snippets`` , arquivos javascript ``javascript.code-snippets``  e por ai vai). Lá você pode criar seu snippet como demostrado acima e ele vai funcionar para todas as pessoas que forem mexer no projeto e estiverem utilizando o vscode, facilitando a sua vida e a de quem mais trabalhar com você 😀

Agora, para fechar com chave de ouro, é bom documentar os atalhos do projeto e avisar seus colegas sobre os novos atalhos, assim eles também tem a vida facilitada e vocês tem um código mais padrão e documentado.