---
title: "Nuxt3 - CHEAT SHEET 01"
date: "2024-04-07"
categories: 
  - "code-learning"
  - "learn-open-source-project"
tags: 
  - "cheat-sheet"
  - "nuxt"
  - "open-source"
  - "typescript"
coverImage: "de30f211086d4dd99b2adae83bbbce4e-scaled.jpg"
---

# 0 - Project

- New project `npx nuxi@latest init`.
- Run development server `npm run dev`.

# 1 - Configuration files

## 1.1 - Private Configuration

- `nuxt.config.ts` - `runtimeConfig` Configuration required at runtime, not exposed to the outside world

```ts
export default defineNuxtConfig({
  runtimeConfig: {
    // The private keys which are only available server-side
    apiSecret: '123',
    // Keys within public are also exposed client-side
    public: {
      apiBase: '/api'
    }
  }
})
```

- `.env`

```ini
# This will override the value of apiSecret
NUXT_API_SECRET=api_secret_token
```

- `useRuntimeConfig` to use.

```html
<script setup lang="ts">
    const runtimeConfig = useRuntimeConfig()
</script>
```

## 1.2 - Public Configuration

- `app.config.ts` Application configuration file.

```ts
export default defineAppConfig({
  title: 'Hello Nuxt',
  theme: {
    dark: true,
    colors: {
      primary: '#ff0000'
    }
  }
})
```

- `useAppConfig` to use.

```html
<script setup lang="ts">
    const appConfig = useAppConfig()
</script>
```

## 1.3 - External Configuration Files

- Nitro: `nitro.config.ts` -> Use `nitro` key in `nuxt.config`
- PostCSS: `postcss.config.js` -> Use `postcss` key in `nuxt.config`
- Vite: `vite.config.ts` -> Use `vite` key in `nuxt.config`
- webpack: `webpack.config.ts` -> Use `webpack` key in `nuxt.config`

## 1.4 - Other common configuration files

- TypeScript `tsconfig.json`
- ESLint `.eslintrc.js`
- Prettier `.prettierrc.json`
- Stylelint `.stylelintrc.json`
- TailwindCSS `tailwind.config.js`
- Vitest `vitest.config.ts`

## 1.5 - Vue Configuration

```ts
export default defineNuxtConfig({
  vite: {
    vue: {
      customElement: true
    },
    vueJsx: {
      mergeProps: true
    }
  }
})
```

- with webpack

```ts
export default defineNuxtConfig({
  webpack: {
    loaders: {
      vue: {
        hotReload: true,
      }
    }
  }
})
```

# 2 - Views

## 2.1 - Entrypoint

- `app.vue` The first component loaded.

```
<template>
  <div>
   <h1>Welcome to the homepage</h1>
  </div>
</template>
```

## 2.2 - Components

- `~/components` Most components are reusable pieces of the user interface, like buttons and menus.

## 2.3 - Pages

- `~/pages` The page matched by the route.
- To use pages, create `pages/index.vue` file and add `<NuxtPage />` component to the app.vue.

## 2.4 - Layouts

- `~/layouts` Define multiple layouts.

# 3 - Assets

## 3.1 - public

- `~/public`
- content is served at the server root as-is.
- used as a public server for static assets publicly available at a defined URL of your application.

## 3.2 - assets

- `~/assets`
- asset that you want the build tool (Vite or webpack) to process.

# 4 - Style

## 4.1 - Local Stylesheets

- `@import` Import stylesheets directly into components.

```html
<script>
// Use a static import for server-side compatibility
import '~/assets/css/first.css'

// Caution: Dynamic imports are not server-side compatible
import('~/assets/css/first.css')
</script>

<style>
@import url("~/assets/css/second.css");
</style>
```

- `nuxt.config.ts` `css property` Define styles to include on all pages.

```ts
export default defineNuxtConfig({
  css: ['~/assets/css/main.css']
})
```

- `fonts` Use url to introduce font resources under public files to define fonts.

```css
@font-face {
  font-family: 'FarAwayGalaxy';
  src: url('/fonts/FarAwayGalaxy.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}
```

- reference your fonts by name in your stylesheets, pages or components

```css
<style>
h1 {
  font-family: 'FarAwayGalaxy', sans-serif;
}
</style>
```

- Stylesheets Distributed Through NPM

```html
<script>
import 'animate.css'
</script>

<style>
@import url("animate.css");
</style>
```

```ts
export default defineNuxtConfig({
  css: ['animate.css']
})
```

## 4.2 - External Stylesheets

- CDN

```ts
export default defineNuxtConfig({
  app: {
    head: {
      link: [{ rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css' }]
    }
}})
```

- Dynamically Adding Stylesheets

```ts
useHead({
  link: [{ rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css' }]
})
```

- Modifying The Rendered Head With A Nitro Plugin

```ts
// ~/server/plugins/my-plugin.ts
// intercept the rendered html with a hook and modify the head programmatically.
export default defineNitroPlugin((nitro) => {
  nitro.hooks.hook('render:html', (html) => {
    html.head.push('<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">')
  })
})
```

## 4.3 - Using Preprocessors

- To use a preprocessor like `SCSS`, `Sass`, `Less` or `Stylus`, install it first.

```html
<style lang="scss">
@use "~/assets/scss/main.scss";
</style>
```

```ts
export default defineNuxtConfig({
  css: ['~/assets/scss/main.scss']
})
```

## 4.4 - Single File Components (SFC) Styling

- ref

```html
<script setup lang="ts">
const isActive = ref(true)
const hasError = ref(false)
const classObject = reactive({
  active: true,
  'text-danger': false
})
</script>

<template>
  <div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>
  <div :class="classObject"></div>
</template>
```

- computed

```html
<script setup lang="ts">
const isActive = ref(true)
const error = ref(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error.value && error.value.type === 'fatal'
}))
</script>

<template>
  <div :class="classObject"></div>
</template>
```

- array

```html
<script setup lang="ts">
const isActive = ref(true)
const errorClass = ref('text-danger')
</script>

<template>
  <div :class="[{ active: isActive }, errorClass]"></div>
</template>
```

- style

```html
<script setup lang="ts">
const activeColor = ref('red')
const fontSize = ref(30)
const styleObject = reactive({ color: 'red', fontSize: '13px' })
</script>

<template>
  <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
  <div :style="[baseStyles, overridingStyles]"></div>
  <div :style="styleObject"></div>
</template>
```

- Scoped Styles: The scoped attribute allows you to style components in isolation.

```html
<template>
  <div class="example">hi</div>
</template>

<style scoped>
.example {
  color: red;
}
</style>
```

- Css Module: You can use CSS Modules with the module attribute. Access it with the injected $style variable.

```html
<template>
  <p :class="$style.red">This should be red</p>
</template>

<style module>
.red {
  color: red;
}
</style>
```

## 4.5 - Using PostCSS

```ts
export default defineNuxtConfig({
  postcss: {
    plugins: {
      'postcss-nested': {}
      "postcss-custom-media": {}
    }
  }
})
```

```html
<style lang="postcss">
  /* Write postcss here */
</style>
```

# 5 - Routing

## 5.1 - Pages

- Nuxt routing is based on vue-router and generates the routes from every component created in the pages/ directory, based on their filename.

```
// files

| pages/
---| about.vue
---| index.vue
---| posts/
-----| [id].vue

// genrate

{
  "routes": [
    {
      "path": "/about",
      "component": "pages/about.vue"
    },
    {
      "path": "/",
      "component": "pages/index.vue"
    },
    {
      "path": "/posts/:id",
      "component": "pages/posts/[id].vue"
    }
  ]
}
```

## 5.2 - Navigation

```html
<template>
  <header>
    <nav>
      <ul>
        <li><NuxtLink to="/about">About</NuxtLink></li>
        <li><NuxtLink to="/posts/1">Post 1</NuxtLink></li>
        <li><NuxtLink to="/posts/2">Post 2</NuxtLink></li>
      </ul>
    </nav>
  </header>
</template>
```

## 5.3 - Route Parameters

```ts
<script setup lang="ts">
const route = useRoute()

// When accessing /posts/1, route.params.id will be 1
console.log(route.params.id)
</script>
```

## 5.4 - Route Middleware

- Anonymous (or inline) route middleware

```html
<script setup>
definePageMeta({
  middleware: defineNuxtRouteMiddleware((to, from) => {
    console.log('to', to);
    console.log('from', from);
  }),
});
</script>
<template>
  …
</template>
```

- Named route middleware

```
// ~/middleware` create your middleware
export default defineNuxtRouteMiddleware(async (to, from) => {
  console.log('middleware/auth')
  console.log('to', to)
  console.log('from', from)
})

// .vue use middleware
<script setup>
  definePageMeta({
    middleware: ["auth"]
    // or middleware: 'auth'
  })
</script>
```

- Global route middleware

placed in the `~/middleware` directory (with a `.global suffix`) and will be `automatically run on every route change`.

## 5.5 - Route Validation

- Nuxt offers route validation via the `validate` property in `definePageMeta()` in each page you wish to validate.

```html
<script setup lang="ts">
definePageMeta({
  validate: async (route) => {
    // Check if the id is made up of digits
    return typeof route.params.id === 'string' && /^\d+$/.test(route.params.id)
  }
})
</script>
```

# 6 - SEO & META

## 6.1 - Default

```ts
export default defineNuxtConfig({
  app: {
    head: {
      charset: 'utf-8',
      viewport: 'width=device-width, initial-scale=1',
    }
  }
})
```

## 6.2 - useHead

```ts
<script setup lang="ts">
useHead({
  title: 'My App',
  meta: [
    { name: 'description', content: 'My amazing site.' }
  ],
  bodyAttrs: {
    class: 'test'
  },
  script: [ { innerHTML: 'console.log(\'Hello world\')' } ]
})
</script>
```

## 6.3 - useSeoMeta

```html
<script setup lang="ts">
useSeoMeta({
  title: 'My Amazing Site',
  ogTitle: 'My Amazing Site',
  description: 'This is my amazing site, let me tell you all about it.',
  ogDescription: 'This is my amazing site, let me tell you all about it.',
  ogImage: 'https://example.com/image.png',
  twitterCard: 'summary_large_image',
})
</script>
```

## 6.4 - Components

- `<Title>, <Base>, <NoScript>, <Style>, <Meta>, <Link>, <Body>, <Html> and <Head>`

```html
<script setup lang="ts">
const title = ref('Hello World')
</script>

<template>
  <div>
    <Head>
      <Title>{{ title }}</Title>
      <Meta name="description" :content="title" />
      <Style type="text/css" children="body { background-color: green; }" ></Style>
    </Head>

    <h1>{{ title }}</h1>
  </div>
</template>
```

# 7 - Transitions

## 7.1 - Page transitions

- automatic transition for all your pages.

```ts
export default defineNuxtConfig({
  app: {
    pageTransition: { name: 'page', mode: 'out-in' }
  },
})
```

- different transition for a page

```html
<script setup lang="ts">
definePageMeta({
  pageTransition: {
    name: 'rotate'
  }
})
</script>
```

## 7.2 - Layout transitions

- transition for all your layouts.

```ts
export default defineNuxtConfig({
  app: {
    layoutTransition: { name: 'layout', mode: 'out-in' }
  },
})
```

- different transition for a layout.

```html
<script setup lang="ts">
definePageMeta({
  layout: 'orange',
  layoutTransition: {
    name: 'slide-in'
  }
})
</script>
```

## 7.3 - Global settings

```ts
export default defineNuxtConfig({
  app: {
    pageTransition: {
      name: 'fade',
      mode: 'out-in' // default
    },
    layoutTransition: {
      name: 'slide',
      mode: 'out-in' // default
    }
  }
})
```

## 7.4 - Disable Transitions

- page

```html
<script setup lang="ts">
definePageMeta({
  pageTransition: false,
  layoutTransition: false
})
</script>
```

- global

```ts
export default defineNuxtConfig({
  app: {
    pageTransition: false,
    layoutTransition: false
  }
})
```

## 7.5 JavaScript Hooks

```ts
<script setup lang="ts">
definePageMeta({
  pageTransition: {
    name: 'custom-flip',
    mode: 'out-in',
    onBeforeEnter: (el) => {
      console.log('Before enter...')
    },
    onEnter: (el, done) => {},
    onAfterEnter: (el) => {}
  }
})
</script>
```

## 7.6 Dynamic Transitions

```html
<script setup lang="ts">
definePageMeta({
  pageTransition: {
    name: 'slide-right',
    mode: 'out-in'
  },
  middleware (to, from) {
    if (to.meta.pageTransition && typeof to.meta.pageTransition !== 'boolean')
      to.meta.pageTransition.name = +to.params.id > +from.params.id ? 'slide-left' : 'slide-right'
  }
})
</script>

<template>
  <h1>#{{ $route.params.id }}</h1>
</template>

<style>
.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: all 0.2s;
}
.slide-left-enter-from {
  opacity: 0;
  transform: translate(50px, 0);
}
.slide-left-leave-to {
  opacity: 0;
  transform: translate(-50px, 0);
}
.slide-right-enter-from {
  opacity: 0;
  transform: translate(-50px, 0);
}
.slide-right-leave-to {
  opacity: 0;
  transform: translate(50px, 0);
}
</style>
```

## 7.7 Transition with NuxtPage

```
<template>
  <div>
    <NuxtLayout>
      <NuxtPage :transition="{
        name: 'bounce',
        mode: 'out-in'
      }" />
    </NuxtLayout>
  </div>
</template>
```

# 8 - Data fetching

## 8.1 - useFetch

```html
<script setup lang="ts">
const { data: count } = await useFetch('/api/count')
</script>

<template>
  <p>Page visits: {{ count }}</p>
</template>
```

## 8.2 - $fetch

```html
<script setup lang="ts">
async function addTodo() {
  const todo = await $fetch('/api/todos', {
    method: 'POST',
    body: {
      // My todo data
    }
  })
}
</script>
```

## 8.3 - useAsyncData

```html
<script setup lang="ts">
const { data, error } = await useAsyncData('users', () => myGetFunction('users'))

// This is also possible:
const { data, error } = await useAsyncData(() => myGetFunction('users'))
</script>
```

```html
<script setup lang="ts">
const { id } = useRoute().params

const { data, error } = await useAsyncData(`user:${id}`, () => {
  return myGetFunction('users', { id })
})
</script>
```

```html
<script setup lang="ts">
const { data: discounts, pending } = await useAsyncData('cart-discount', async () => {
  const [coupons, offers] = await Promise.all([
    $fetch('/cart/coupons'),
    $fetch('/cart/offers')
  ])

  return { coupons, offers }
})
// discounts.value.coupons
// discounts.value.offers
</script>
```

## 8.4 - Return Values

- useFetch and useAsyncData have the same return values listed below.
    - `data`: the result of the asynchronous function that is passed in.
    - `pending`: a boolean indicating whether the data is still being fetched.
    - `refresh/execute`: a function that can be used to refresh the data returned by the handler function.
    - `clear`: a function that can be used to set data to undefined, set error to null, set pending to false, set status to idle, and mark any currently pending requests as cancelled.
    - `error`: an error object if the data fetching failed.
    - `status`: a string indicating the status of the data request ("idle", "pending", "success", "error").

## 8.5 - Options

- Lazy

```html
<script setup lang="ts">
const { pending, data: posts } = useFetch('/api/posts', {
  lazy: true
})
</script>

<template>
  <!-- you will need to handle a loading state -->
  <div v-if="pending">
    Loading ...
  </div>
  <div v-else>
    <div v-for="post in posts">
      <!-- do something -->
    </div>
  </div>
</template>
```

- Minimize payload size

```html
<script setup lang="ts">
/* only pick the fields used in your template */
const { data: mountain } = await useFetch('/api/mountains/everest', {
  pick: ['title', 'description']
})
</script>

<template>
  <h1>{{ mountain.title }}</h1>
  <p>{{ mountain.description }}</p>
</template>
```

- Caching and refetching

```html
<script setup lang="ts">
const { data, error, execute, refresh } = await useFetch('/api/users')
</script>

<template>
  <div>
    <p>{{ data }}</p>
    <button @click="refresh">Refresh data</button>
  </div>
</template>
```

- Clear

```html
<script setup lang="ts">
const { data, clear } = await useFetch('/api/users')

const route = useRoute()
watch(() => route.path, (path) => {
  if (path === '/') clear()
})
</script>
```

- Watch

```html
<script setup lang="ts">
const id = ref(1)

const { data, error, refresh } = await useFetch('/api/users', {
  /* Changing the id will trigger a refetch */
  watch: [id]
})
</script>
```

- Computed URL

```html
<script setup lang="ts">
const id = ref(null)

const { data, pending } = useLazyFetch('/api/user', {
  query: {
    user_id: id
  }
})
</script>
```

- Not immediate

```html
<script setup lang="ts">
const { data, error, execute, pending, status } = await useLazyFetch('/api/comments', {
  immediate: false
})
</script>

<template>
  <div v-if="status === 'idle'">
    <button @click="execute">Get data</button>
  </div>

  <div v-else-if="pending">
    Loading comments...
  </div>

  <div v-else>
    {{ data }}
  </div>
</template>
```

- Passing Headers and cookies

```html
<script setup lang="ts">
const headers = useRequestHeaders(['cookie'])

const { data } = await useFetch('/api/me', { headers })
</script>
```

- Pass Cookies From Server-side API Calls on SSR Response

```ts
import { appendResponseHeader, H3Event } from 'h3'

export const fetchWithCookie = async (event: H3Event, url: string) => {
  /* Get the response from the server endpoint */
  const res = await $fetch.raw(url)
  /* Get the cookies from the response */
  const cookies = (res.headers.get('set-cookie') || '').split(',')
  /* Attach each cookie to our incoming Request */
  for (const cookie of cookies) {
    appendResponseHeader(event, 'set-cookie', cookie)
  }
  /* Return the data of the response */
  return res._data
}
```

```html
<script setup lang="ts">
// This composable will automatically pass cookies to the client
const event = useRequestEvent()

const { data: result } = await useAsyncData(() => fetchWithCookie(event!, '/api/with-cookie'))

onMounted(() => console.log(document.cookie))
</script>
```

# 9 - State Management

- useState

```html
<script setup lang="ts">
const counter = useState('counter', () => Math.round(Math.random() * 1000))
</script>
```

- Pinia

```ts
export const useWebsiteStore = defineStore('websiteStore', {
  state: () => ({
    name: '',
    description: ''
  }),
  actions: {
    async fetch() {
      const infos = await $fetch('https://api.nuxt.com/modules/pinia')

      this.name = infos.name
      this.description = infos.description
    }
  }
})
```

# 10 -Error Handling

## 10.1 - Vue Errors

- `~/plugins/error-handler.ts` use hook `vue:error`

```ts
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.config.errorHandler = (error, instance, info) => {
    // handle error, e.g. report to a service
  }

  // Also possible
  nuxtApp.hook('vue:error', (error, instance, info) => {
    // handle error, e.g. report to a service
  })
})
```

## 10.2 - Startup Errors

- Nuxt will call the `app:error` hook if there are any errors in starting your Nuxt application.
- This includes:
    - running Nuxt plugins
    - processing `app:created` and `app:beforeMount` hooks
    - `rendering` your Vue app to HTML (during SSR)
    - `mounting the app (on client-side)`, though you should handle this case with `onErrorCaptured` or with `vue:error`
    - processing the `app:mounted` hook

## 10.3 - Error Page

- Customize the default error page by adding `~/error.vue` in the source directory of your application, alongside `app.vue`.

```html
<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: Object as () => NuxtError
})

const handleError = () => clearError({ redirect: '/' })
</script>

<template>
  <div>
    <h2>{{ error.statusCode }}</h2>
    <button @click="handleError">Clear errors</button>
  </div>
</template>
```

## 10.4 - Error Utils

- `useError` - This function will return the global Nuxt error that is being handled.
- `createError` - Create an error object with additional metadata. It is usable in both the Vue and Server portions of your app, and is meant to be thrown.
- `showError` - You can call this function at any point on client-side, or (on server side) directly within middleware, plugins or setup() functions. It will trigger a full-screen error page which you can clear with clearError.
- `clearError` - This function will clear the currently handled Nuxt error. It also takes an optional path to redirect to (for example, if you want to navigate to a 'safe' page).

## 10.5 - Render Error in Component

```html
<template>
  <!-- some content -->
  <NuxtErrorBoundary @error="someErrorLogger">
    <!-- You use the default slot to render your content -->
    <template #error="{ error, clearError }">
      You can display the error locally here: {{ error }}
      <button @click="clearError">
        This will clear the error.
      </button>
    </template>
  </NuxtErrorBoundary>
</template>
```

# 11 - Testing

## 11.1 - Installation

`npm i --save-dev @nuxt/test-utils vitest @vue/test-utils happy-dom playwright-core`

## 11.2 - Unit Testing

- Setup
    
    - Add module.
        
        ```ts
        export default defineNuxtConfig({
        modules: [
            '@nuxt/test-utils/module'
        ]
        })
        ```
        
    - Create a `vitest.config.ts`
        

```ts
    import { defineVitestConfig } from '@nuxt/test-utils/config'
    export default defineVitestConfig({
    // any custom Vitest config you require
    })
```

- Using a Nuxt Runtime Environment

adding `@vitest-environment` nuxt as a comment directly in the test file.

```ts
    // @vitest-environment nuxt
    import { test } from 'vitest'
    test('my test', () => {
     // ... test with Nuxt environment!
    })
```

enable the Nuxt environment for all tests.

```ts
    // vitest.config.ts
    import { fileURLToPath } from 'node:url'
    import { defineVitestConfig } from '@nuxt/test-utils/config'

    export default defineVitestConfig({
    test: {
        environment: 'nuxt',
     // you can optionally set Nuxt-specific environment options
    // environmentOptions: {
    //   nuxt: {
    //     rootDir: fileURLToPath(new URL('./playground', import.meta.url)),
    //     domEnvironment: 'happy-dom', // 'happy-dom' (default) or 'jsdom'
    //     overrides: {
    //       // other Nuxt config you want to pass
    //     }
    //   }
    // }
    }
    })
```

## 11.3 - Built-In Mocks

```ts
import { defineVitestConfig } from '@nuxt/test-utils/config'

export default defineVitestConfig({
  test: {
    environmentOptions: {
      nuxt: {
        mock: {
          intersectionObserver: true,
          indexedDb: true,
        }
      }
    }
  }
})
```

## 11.4 - Helpers

- mountSuspended: allows you to mount any Vue component within the Nuxt environment

```ts
import type { Component } from 'vue'
import { it, expect } from 'vitest'
declare const SomeComponent: Component
declare const App: Component
// ---cut---
// tests/components/SomeComponents.nuxt.spec.ts
import { mountSuspended } from '@nuxt/test-utils/runtime'

it('can mount some component', async () => {
    const component = await mountSuspended(SomeComponent)
    expect(component.text()).toMatchInlineSnapshot(
        'This is an auto-imported component'
    )
})

// tests/App.nuxt.spec.ts
it('can also mount an app', async () => {
    const component = await mountSuspended(App, { route: '/test' })
    expect(component.html()).toMatchInlineSnapshot(`
      "<div>This is an auto-imported component</div>
      <div> I am a global component </div>
      <div>/</div>
      <a href="/test"> Test link </a>"
    `)
})
```

- renderSuspended: allows you to render any Vue component within the Nuxt environment using @testing-library/vue

```ts
import type { Component } from 'vue'
import { it, expect } from 'vitest'
declare const SomeComponent: Component
declare const App: Component
// ---cut---
// tests/components/SomeComponents.nuxt.spec.ts
import { renderSuspended } from '@nuxt/test-utils/runtime'
import { screen } from '@testing-library/vue'

it('can render some component', async () => {
  await renderSuspended(SomeComponent)
  expect(screen.getByText('This is an auto-imported component')).toBeDefined()
})
```

```ts
import type { Component } from 'vue'
import { it, expect } from 'vitest'
declare const SomeComponent: Component
declare const App: Component
// ---cut---
// tests/App.nuxt.spec.ts
import { renderSuspended } from '@nuxt/test-utils/runtime'

it('can also render an app', async () => {
  const html = await renderSuspended(App, { route: '/test' })
  expect(html).toMatchInlineSnapshot(`
    "<div id="test-wrapper">
      <div>This is an auto-imported component</div>
      <div> I am a global component </div>
      <div>Index page</div><a href="/test"> Test link </a>
    </div>"
  `)
})
```

- mockNuxtImport: allows you to mock Nuxt's auto import functionality

```ts
import { mockNuxtImport } from '@nuxt/test-utils/runtime'

mockNuxtImport('useStorage', () => {
  return () => {
    return { value: 'mocked storage' }
  }
})

// your tests here
```

- mockComponent: allows you to mock Nuxt's component.

```ts
import { mockComponent } from '@nuxt/test-utils/runtime'

mockComponent('MyComponent', {
  props: {
    value: String
  },
  setup(props) {
    // ...
  }
})

// relative path or alias also works
mockComponent('~/components/my-component.vue', async () => {
  // or a factory function
  return defineComponent({
    setup(props) {
      // ...
    }
  })
})

// or you can use SFC for redirecting to a mock component
mockComponent('MyComponent', () => import('./MockComponent.vue'))

// your tests here
```

- registerEndpoint: allows you create Nitro endpoint that returns mocked data

```ts
import { registerEndpoint } from '@nuxt/test-utils/runtime'

registerEndpoint("/test/", () => ({
  test: "test-field"
}))

registerEndpoint("/test/", {
  method: "POST",
  handler: () => ({ test: "test-field" })
})
```

## 11.3 - End-To-End Testing

For end-to-end testing, we support Vitest, Jest, Cucumber and Playwright as test runners.

```ts
import { describe, test } from 'vitest'
import { setup, $fetch } from '@nuxt/test-utils/e2e'

describe('My test', async () => {
  await setup({
    // test context options
  })

  test('my test', () => {
    // ...
  })
})
```

- [https://nuxt.com/docs/getting-started/testing#end-to-end-testing](https://nuxt.com/docs/getting-started/testing#end-to-end-testing)
