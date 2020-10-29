---
layout: article
title: Leia esse post e dê adeus ao "nvm use"
date: 2020-10-29 18:22
tags:
  - Dicas
  - Nvm
  - Nodejs
  - zsh
  - MacOs
image: 'assets/posts/leia-esse-post-e-de-adeus-ao-nvm-use/asset-1.jpg'
description: "Uma dica valiosa para todos que mexem com muitos projetos com várias versões de node"
---
![imagem de várias linhas de código]({{ site.baseurl }}/assets/posts/leia-esse-post-e-de-adeus-ao-nvm-use/asset-1.jpg)

Comecei recentemente a trabalhar em uma nova empresa, e pela primeira vez estou tendo que trabalhar com muitos projetos com versões diferentes do node e isso estava começando a perturbar meu juízo, uma vez era uma festa de `nvm use x`, `nvm use y` e vários servidores iniciados apenas para dar erro depois pois você errou a versão node desse repositório. Bom, agora não mais.

<!--more-->

Resolvi dar uma pesquisada na doc do nvm porque não era possível que não houvesse um jeito mais simples de fazer isso. E você sabe que se está lendo esse post é porque eu encontrei.

Devo avisar, porém, que o tutorial a seguir é para a implementação utilizando zsh no MacOs,  então se você usa bash ou Windows o passo inicial pode ser um pouco diferente, mas [você pode ler mais sobre e ver as diferentes opções de implementação aqui](https://github.com/nvm-sh/nvm#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file){:target="\_blank"}.

Primeiramente, você vai ter que modificar o seu `$HOME/.zshrc` e para isso basta executar o seguinte código:

```
nano $HOME/.zshrc
```

Então, logo abaixo de onde você inicia o nvm, você vai colocar esse código aqui:

```
# place this after nvm initialization!
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

Salve, saia e vá para o diretório que você precisa mudar a versão do node , crie um arquivo chamado `.nvmrc` e coloque lá a versão de node compatível com o projeto. Um exemplo:

```
v9.9.0
```

Reinicie o terminal e pronto! Agora quando você entrar no diretório ele vai automaticamente mudar para a versão compatível daquele projeto!