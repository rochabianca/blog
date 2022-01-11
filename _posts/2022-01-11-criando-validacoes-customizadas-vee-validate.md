---
layout: article
title: Criando Validações customizadas no Vee-Validate
date: 2022-01-11 14:51

tags:
  - Dicas
  - Vuejs
  - VeeValidate
image: https://rochabianca.github.io/blog/assets/posts/criando-validacoes-customizadas-vee-validate/asset-1.jpeg
author: 'Bianca Rocha'
description: "Para você que usa o VeeValidate, mas precisa de validações mais específicas do que as disponíveis pelo framework (cof cof.... validação com moedas.... cof cof)."
---

![Uma pessoa digitando em um macbook]({{ site.baseurl }}/assets/posts/criando-validacoes-customizadas-vee-validate/asset-1.jpeg)

Para você que usa o VeeValidate, mas precisa de validações mais específicas do que as disponíveis pelo framework (cof cof.... validação com moedas.... cof cof).

<!--more-->

A primeira coisa que deve ser feita é criar uma nova pasta em src.Inicialmente essa pasta vai ter 2 arquivos:

```
- src
  - validadoresCustomizados
    - index.js
    - validacaoCustom.js
```

Por enquanto vamos ignorar o index.js e focar no segundo arquivo, `validacaoCustom.js` é nele que iremos criar nossa primeira validação. Começaremos criando uma validação que verifica se certo valor, no formato `R$ XX,XX` é positivo ou não:

```
// src/validadoresCustomizados/validacaoCustom.js

const ehPositivo = {
    getMessage: field => 'O campo ' + field + 'deve ser positivo',
    validate (value) {
        const valorFormatado = value.replace('R$ ', '').replace(',', '.')
        const validacao = +valorFormatado > 0
        return validacao
    }
}

export default ehPositivo
```

Okay, mas o que exatamente faz esse código funcionar?

Basicamente, para que o VeeValidate reconheça sua regra, ela precisa seguir um certo padrão. O padrão que estou mostrando é a forma em objeto, que pode ser vista [aqui](https://vee-validate.logaretm.com/v2/guide/custom-rules.html#function-form){:target="\_blank"} mas que consiste em um objeto com 2 funções dentro:
- `getMessage` , que retorna a mensagem que será exibida caso a validação falhe
- `validate` que é onde a validação ocorre e obrigatoriamente deve retornar um booleano ou uma promessa que resulta em um booleano.

Caso você queira utilizar um parâmetro para fazer sua validação, como por exemplo, saber se um valor é menor ou maior que um certo número, basta utilizar os args:

```
// src/validadoresCustomizados/ehMaiorQue.js

const ehMaiorQue = {
    getMessage: (field, args) => 'O campo ' + field + 'deve ser maior que' + args,
    validate (value, args) {
        const validacao = value > args
        return validacao
    }
}

export default ehMaiorQue
```

Beleza, mas como eu vou importar esse código nas minhas regras?

Bom, antes disso vamos voltar ao index.js e fazer lá a importação do nosso objeto, para manter nosso código mais organizado e facilitar a adição de novas regras no futuro:

```
// src/validadoresCustomizados/index.js

import { Validator } from 'vee-validate'
import ehPositivo from './validacaoCustom'
import ehMaiorQue from './ehMaiorQue'

Validator.extend('eh_positivo', ehPositivo)
Validator.extend('eh_maior_que', ehMaiorQue)
```

No código acima a função `Validator.extend` é a responsável por adicionar a regra que criamos as regras disponíveis por padrão. Agora sim, está tudo pronto para importarmos.

A importação é feita no local onde você adiciona o vee-validate no vue. Pode ser no main.js, ou em um arquivo específico apenas para plugins. Lá você precisa apenas importar o index.js que acabamos de criar que a validação já deve estar disponível para você:

```
// src/main.js

import VeeValidate from 'vee-validate'
import '@/validadoresCustomizados/index.js'

...

export default (Vue) => {
    Vue.use(VeeValidate),
    ...
}
```

Por fim, a validação estará disponível e pode ser utilizada assim como quaisquer outras validações no vee-validate:

```
// ComponenteQualquer.vue

<div class="form-group" :class="{ 'has-error': errors.has('eh_positivo') }">
  <label class="control-label" for="total">Total</label>

  <!-- Input com a nossa validação customizada -->
  <input
    name="total"
    type="text"
    mask="R$ XX,XX"
    class="form-control"
    id="total"
    placeholder="Total"
    v-validate
    data-rules="required|eh_positivo"
   />
  <!-- Fim do input com a nossa validação customizada -->

  <span v-show="errors.has('eh_positivo')" class="help-block">
    {{ errors.first('eh_positivo') }}
  </span>
</div>

<!-- Validação com parametros -->
<div class="form-group" :class="{ 'has-error': errors.has('eh_maior_que') }">
  <label class="control-label" for="total">Total</label>

  <!-- Input com a nossa validação customizada -->
  <input
    name="total"
    type="number"
    class="form-control"
    id="total"
    placeholder="Total"
    v-validate
    data-rules="required|eh_maior_que:1"
   />
  <!-- Fim do input com a nossa validação customizada -->

  <span v-show="errors.has('eh_maior_que')" class="help-block">
    {{ errors.first('eh_maior_que') }}
  </span>
</div>
```

No mais acho que é isso, espero que tenham achado esse post útil, até a próxima :D

Fontes que me ajudaram a produzir esse texto:
- [Esse vídeo do canal Poorgramer que mostra um exemplo prático de como fazer uma regra customizada](https://www.youtube.com/watch?v=zz7d0XLsl08&t=65s&ab_channel=Poorgrammer){:target="\_blank"}
- [A documentação do Vee Validate para custom rules](https://vee-validate.logaretm.com/v2/guide/custom-rules.html){:target="\_blank"}