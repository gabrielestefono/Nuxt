# Assets

Nuxt oferece 2 opções para os seus assets

Nuxt usa dois diretórios para lidar com assets como CSS, fontes ou imagens

* A pasta `public` é servida no servidor como deve ser.
* A pasta `assets` contém por convenção todo asset que você quer que a ferramenta (Vite, webpack) processe.

## Pasta Public

O diretório `public/` é usado como um servidor público para ativos estáticos disponíveis publicamente em uma URL definida da sua aplicação. Você pode obter um arquivo no diretório `public/` a partir do código da sua aplicação ou de um navegador pela URL raiz `/`. Por exemplo, referenciando um arquivo de imagem no diretório `public/img/`, disponível na URL estática `/img/nuxt.png`.

```js
<template>
  <img src="/img/nuxt.png" alt="Discover Nuxt 3" />
</template>
```

## Pasta Assets

O Nuxt usa **Vite** (padrão) ou **webpack** para construir e empacotar sua aplicação. A função principal dessas ferramentas de construção é processar arquivos JavaScript, mas elas podem ser estendidas por meio de **plugins** (para o Vite) ou **loaders** (para o webpack) para processar outros tipos de ativos, como folhas de estilo, fontes ou SVG. Esta etapa transforma o arquivo original principalmente para fins de desempenho ou de cache (como minificação de folhas de estilo ou invalidação de cache do navegador).

Por convenção, o Nuxt usa o diretório `assets/` para armazenar esses arquivos, mas não há funcionalidade de varredura automática para este diretório, e você pode usar qualquer outro nome para ele.

No código da sua aplicação, você pode referenciar um arquivo localizado no diretório `assets/` usando o caminho `~/assets/`.

### Exemplo

Por exemplo, referenciando um arquivo de imagem que será processado se uma ferramenta de construção estiver configurada para lidar com essa extensão de arquivo.

```js
<template>
  <img src="~/assets/img/nuxt.png" alt="Discover Nuxt 3" />
</template>
```

## Global Styles Imports

Para inserir globalmente declarações nos estilos dos seus componentes Nuxt, você pode usar a opção `Vite` no arquivo `nuxt.config`.

### Example

Neste exemplo, há um arquivo **sass parcial** contendo variáveis de cor a serem usadas pelas suas **páginas** e **componentes** Nuxt.

```scss
// assets/_colors.scss
$primary: #49240F;
$secondary: #E4A79D;
```

```scss
// assets/_colors.sass
$primary: #49240F
$secondary: #E4A79D
```
In your `nuxt.config`

```js
export default defineNuxtConfig({
  vite: {
    css: {
      preprocessorOptions: {
        scss: {
          additionalData: '@use "~/assets/_colors.scss" as *;'
        }
      }
    }
  }
})
```

```js
export default defineNuxtConfig({
  vite: {
    css: {
      preprocessorOptions: {
        sass: {
          additionalData: '@use "~/assets/_colors.sass" as *\n'
        }
      }
    }
  }
})
```