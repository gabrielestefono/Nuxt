# Views

Nuxt provém várias camadas de componentes para implementar a interface do usuário da sua aplicação.

## app.vue

Por padrão, Nuxt vai tratar esse arquivo como o ponto de entrada e renderizar seu conteúdo em cada rota da sua aplicação.

```js
<template>
  <div>
   <h1>Welcome to the homepage</h1>
  </div>
</template>
```

A maioria dos componentes são pedaços reutilizável da interface do usuário, como botões em menus. No Nuxt, você pode criar esses componentes na pasta `/components`, e assim, eles estarão disponíveis em toda a sua aplicação sem precisar importá-los.

```js
<template>
  <div>
    <h1>Welcome to the homepage</h1>
    <AppAlert>
      This is an auto-imported component.
    </AppAlert>
  </div>
</template>
```

```js
<template>
  <span>
    <slot />
  </span>
</template>
```

## Páginas

Páginas representam views para cada rota. Todo arquivo dentro da pasta `/pages` representa uma rota diferente mostrando o seu conteúdo.

Para usar páginas, crie o arquivo `pages/index.vue` e adicione o componente `<NuxtPage/>` ao app.vue. Agora você pode mais páginas adicionando seus respectivos arquivos à pasta pages.

```js
<template>
  <div>
    <h1>Welcome to the homepage</h1>
    <AppAlert>
      This is an auto-imported component
    </AppAlert>
  </div>
</template>
```

## Layouts

Layouts são envoltórios ao redor das páginas que contêm uma Interface de Usuário comum para várias páginas, como a exibição de cabeçalho e rodapé. Os layouts são arquivos Vue que usam componentes `<slot/>` para exibir o conteúdo da página. O arquivo `layouts/default.vue` será utilizado por padrão. Layouts personalizados podem ser definidos como parte dos metadados da sua página.

```js
<template>
  <div>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>
```

```js
<template>
  <div>
    <AppHeader />
    <slot />
    <AppFooter />
  </div>
</template>
```

```js
<template>
  <div>
    <h1>Welcome to the homepage</h1>
    <AppAlert>
      This is an auto-imported component
    </AppAlert>
  </div>
</template>
```

```js
<template>
  <section>
    <p>This page will be displayed at the /about route.</p>
  </section>
</template>
```

## Avançado: Extendendo o template HTML

Você pode ter controle absoluto sobre o template HTML adicionando um pluggin nitro que registra os hooks. A função callback de render:html te permite mudar o HTML antes de ser enviado ao cliente.

```js
export default defineNitroPlugin((nitroApp) => {
  nitroApp.hooks.hook('render:html', (html, { event }) => {
    // This will be an object representation of the html template.
    console.log(html)
    html.head.push(`<meta name="description" content="My custom description" />`)
  })
  // You can also intercept the response here.
  nitroApp.hooks.hook('render:response', (response, { event }) => { console.log(response) })
})
```