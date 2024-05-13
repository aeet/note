---
title: "Nuxt3 - CHEAT SHEET 02"
date: "2024-04-07"
categories: 
  - "code-learning"
  - "learn-open-source-project"
tags: 
  - "cheat-sheet"
  - "nuxt"
  - "open-source"
  - "typescript"
coverImage: "8cd4dc708c6c493b8948a6f6673762cc.jpg"
---

# Directory Structure

# 1 - .nuxt

- Nuxt uses the .nuxt/ directory in development to generate your Vue application.

# 2 - .output

- Use this directory to deploy your Nuxt application to production.

# 3 - assets

- all the website's assets that the build tool will process.
    - Stylesheets (CSS, SASS, etc.)
    - Fonts
    - Images that won't be served from the public/ directory.

# 4 - components

- all your Vue components.

* * *

```
| components/
--| base/
----| foo/
------| Button.vue
```

- component Names: `<BaseFooButton />`

* * *

```ts
export default defineNuxtConfig({
  components: [
    {
      path: '~/components',
      pathPrefix: false,
    },
  ],
});
```

- auto-import components based only on its name, not path.

* * *

- dynamic Components

```html
<script setup lang="ts">
import { SomeComponent } from '#components'

const MyButton = resolveComponent('MyButton')
</script>

<template>
  <component :is="clickable ? MyButton : 'div'" />
  <component :is="SomeComponent" />
</template>
```

* * *

- register some components globally by placing them in a ~/components/global directory, or by using a .global.vue suffix in the filename.
    
- other function
    

```ts
  export default defineNuxtConfig({
    components: {
+     global: true,
+     dirs: ['~/components']
    },
  })
```

* * *

- Dynamic Imports
    - add the Lazy prefix to the component's name.

```html
<script setup lang="ts">
const show = ref(false)
</script>

<template>
  <div>
    <h1>Mountains</h1>
    <!-- Lazy -->
    <LazyMountainsList v-if="show" />
    <button v-if="!show" @click="show = true">Show List</button>
  </div>
</template>
```

* * *

- Direct Imports
    - import components from #components

```html
<script setup lang="ts">
import { NuxtLink, LazyMountainsList } from '#components'

const show = ref(false)
</script>

<template>
  <div>
    <h1>Mountains</h1>
    <LazyMountainsList v-if="show" />
    <button v-if="!show" @click="show = true">Show List</button>
    <NuxtLink to="/">Home</NuxtLink>
  </div>
</template>
```

* * *

- Custom Directories

```ts
export default defineNuxtConfig({
  components: [
    // ~/calendar-module/components/event/Update.vue => <EventUpdate />
    { path: '~/calendar-module/components' },

    // ~/user-module/components/account/UserDeleteDialog.vue => <UserDeleteDialog />
    { path: '~/user-module/components', pathPrefix: false },

    // ~/components/special-components/Btn.vue => <SpecialBtn />
    { path: '~/components/special-components', prefix: 'Special' },

    // It's important that this comes last if you have overrides you wish to apply
    // to sub-directories of `~/components`.
    //
    // ~/components/Btn.vue => <Btn />
    // ~/components/base/Btn.vue => <BaseBtn />
    '~/components'
  ]
})
```

* * *

- Npm Packages

```ts
import { addComponent, defineNuxtModule } from '@nuxt/kit'

export default defineNuxtModule({
  setup() {
    // import { MyComponent as MyAutoImportedComponent } from 'my-npm-package'
    addComponent({
      name: 'MyAutoImportedComponent',
      export: 'MyComponent',
      filePath: 'my-npm-package',
    })
  },
})
```

* * *

- Component Extensions

```ts
export default defineNuxtConfig({
  components: [
    {
      path: '~/components',
      extensions: ['.vue'],
    }
  ]
})
```

* * *

- Client Components
    - If a component is meant to be rendered only client-side, you can add the .client suffix to your component.

```
| components/
--| Comments.client.vue
```

* * *

- Server Components
    - Server components allow server-rendering individual components within your client-side apps

* * *

- Standalone server components
    - Standalone server components will always be rendered on the server, also known as Islands components.

```ts
export default defineNuxtConfig({
  experimental: {
    componentIslands: true
  }
})
```

```
| components/
--| HighlightedMarkdown.server.vue
```

* * *

- Built-In Nuxt Components
    - ## components: `<ClientOnly>` ,`<DevOnly>` and more....
        
- Library Authors

```
| node_modules/
---| awesome-ui/
------| components/
---------| Alert.vue
---------| Button.vue
------| nuxt.js
| pages/
---| index.vue
| nuxt.config.js
```

```ts
import { defineNuxtModule, createResolver } from '@nuxt/kit'

export default defineNuxtModule({
  hooks: {
    'components:dirs': (dirs) => {
      const { resolve } = createResolver(import.meta.url)
      // Add ./components dir to the list
      dirs.push({
        path: resolve('./components'),
        prefix: 'awesome'
      })
    }
  }
})
```

- you can import your UI library as a Nuxt module in your nuxt.config file:

```ts
export default defineNuxtConfig({
  modules: ['awesome-ui/nuxt']
})
```

# 5 - composables

- auto-import your Vue composables into your application.

```ts
// composables/useFoo.ts
export const useFoo = () => {
  return useState('foo', () => 'bar')
}

// composables/use-foo.ts or composables/useFoo.ts 
// It will be available as useFoo() (camelCase of file name without extension)
export default function () {
  return useState('foo', () => 'bar')
}
```

* * *

- How Files Are Scanned

```
| composables/
---| index.ts     // scanned
---| useFoo.ts    // scanned
-----| nested/
-------| utils.ts // not scanned
```

* * *

- config scan

```ts
export default defineNuxtConfig({
  imports: {
    dirs: [
      // Scan top-level modules
      'composables',
      // ... or scan modules nested one level deep with a specific name and file extension
      'composables/*/index.{ts,js,mjs,mts}',
      // ... or scan all modules within given directory
      'composables/**'
    ]
  }
})
```

# 6 - content

- Use the content/ directory to create a file-based CMS for your application.
- `npx nuxi module add content`

```html
<!-- pages/[...slug].vue -->
<template>
  <main>
    <!-- ContentDoc returns content for `$route.path` by default or you can pass a `path` prop -->
    <ContentDoc />
  </main>
</template>
```

# 7 - layouts

- Nuxt provides a layouts framework to extract common UI patterns into reusable layouts.

* * *

- Enable Layouts

```html
<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
```

* * *

- To use a layout
    - Set a layout property in your page with `definePageMeta`.
    - Set the `name` prop of `<NuxtLayout>`.

* * *

- Default Layout
    - Add a `~/layouts/default.vue`
        
        ```
        
        <template>
        <div>
        <p>Some default layout content shared across all pages</p>
        <slot />
        </div>
        </template>
        ```
        

```
---
- Named Layout
```

\-| layouts/ ---| default.vue ---| custom.vue

````

```html
<script setup lang="ts">
definePageMeta({
  layout: 'custom'
})
</script>
````

```html
<script setup lang="ts">
// You might choose this based on an API call or logged-in status
const layout = "custom";
</script>

<template>
  <NuxtLayout :name="layout">
    <NuxtPage />
  </NuxtLayout>
</template>
```

* * *

## `~/layouts/desktop/default.vue`: desktop-default `~/layouts/desktop-base/base.vue`: desktop-base `~/layouts/desktop/index.vue`: desktop

- Changing the Layout Dynamically

```html
<script setup lang="ts">
function enableCustomLayout () {
  setPageLayout('custom')
}
definePageMeta({
  layout: false,
});
</script>

<template>
  <div>
    <button @click="enableCustomLayout">Update layout</button>
  </div>
</template>
```

* * *

- Overriding a Layout on a Per-page Basis
    - If you are using pages, you can take full control by setting layout: false and then using the `<NuxtLayout>` component within the page.

```html
<script setup lang="ts">
definePageMeta({
  layout: false,
})
</script>

<template>
  <div>
    <NuxtLayout name="custom">
      <template #header> Some header template content. </template>

      The rest of the page
    </NuxtLayout>
  </div>
</template>
```

# 8 - middleware

- Nuxt provides middleware to run code before navigating to a particular route.

* * *

- kinds
    - Anonymous
    - Named route middleware
    - Global route middleware

* * *

- order
    - Global Middleware
    - Page defined middleware order (if there are multiple middleware declared with the array syntax)

* * *

- Ordering Global Middleware

```
middleware/
--| 01.setup.global.ts
--| 02.analytics.global.ts
--| auth.ts
```

* * *

- When Middleware Runs

```ts
export default defineNuxtRouteMiddleware(to => {
  // skip middleware on server
  if (import.meta.server) return
  // skip middleware on client side entirely
  if (import.meta.client) return
  // or only skip middleware on initial client load
  const nuxtApp = useNuxtApp()
  if (import.meta.client && nuxtApp.isHydrating && nuxtApp.payload.serverRendered) return
})
```

* * *

- Adding Middleware Dynamically

```ts
export default defineNuxtPlugin(() => {
  addRouteMiddleware('global-test', () => {
    console.log('this global middleware was added in a plugin and will be run on every route change')
  }, { global: true })

  addRouteMiddleware('named-test', () => {
    console.log('this named middleware was added in a plugin and would override any existing middleware of the same name')
  })
})
```

- Setting Middleware At Build Time

```ts
import type { NuxtPage } from 'nuxt/schema'

export default defineNuxtConfig({
  hooks: {
    'pages:extend' (pages) {
      function setMiddleware (pages: NuxtPage[]) {
        for (const page of pages) {
          if (/* some condition */ true) {
            page.meta ||= {}
            // Note that this will override any middleware set in `definePageMeta` in the page
            page.meta.middleware = ['named']
          }
          if (page.children) {
            setMiddleware(page.children)
          }
        }
      }
      setMiddleware(pages)
    }
  }
})
```

# 9 - modules

You don't need to add those local modules to your nuxt.config.ts separately.

```ts
// `nuxt/kit` is a helper subpath import you can use when defining local modules
// that means you do not need to add `@nuxt/kit` to your project's dependencies
import { createResolver, defineNuxtModule, addServerHandler } from 'nuxt/kit'

export default defineNuxtModule({
  meta: {
    name: 'hello'
  },
  setup () {
    const { resolve } = createResolver(import.meta.url)

    // Add an API route
    addServerHandler({
      route: '/api/hello',
      handler: resolve('./runtime/api-route')
    })
  }
})
```

- When starting Nuxt, the hello module will be registered and the /api/hello route will be available.

# 10 - pages

- Dynamic Routes

```
-| pages/
---| index.vue
---| users-[group]/
-----| [id].vue
```

```html
<template>
  <p>{{ $route.params.group }} - {{ $route.params.id }}</p>
</template>
```

```html
<script setup lang="ts">
const route = useRoute()

if (route.params.group === 'admins' && !route.params.id) {
  console.log('Warning! Make sure user is authenticated!')
}
</script>
```

* * *

- Catch-all Route

`pages/[...slug].vue`

* * *

- Nested Routes

```
-| pages/
---| parent/
------| child.vue
---| parent.vue
```

```
[
  {
    path: '/parent',
    component: '~/pages/parent.vue',
    name: 'parent',
    children: [
      {
        path: 'child',
        component: '~/pages/parent/child.vue',
        name: 'parent-child'
      }
    ]
  }
]
```

* * *

- Child Route Keys
    - control over when the component is re-rendered

```html
<template>
  <div>
    <h1>I am the parent view</h1>
    <NuxtPage :page-key="route => route.fullPath" />
  </div>
</template>
```

```html
<script setup lang="ts">
definePageMeta({
  key: route => route.fullPath
})
</script>
```

* * *

- Page Metadata

```html
<script setup lang="ts">
definePageMeta({
  title: 'My home page'
})
const route = useRoute()
console.log(route.meta.title) // My home page
</script>
```

* * *

- Special Metadata
    - alias
    - keepalive
    - key
    - layout
    - layoutTransition and pageTransition
    - middleware
    - name
    - path

* * *

- Typing Custom Metadata

```ts
declare module '#app' {
  interface PageMeta {
    pageType?: string
  }
}
// It is always important to ensure you import/export something when augmenting a type
export {}
```

* * *

- Navigation

```html
<template>
  <NuxtLink to="/">Home page</NuxtLink>
</template>
```

- Programmatic Navigation

```html
<script setup lang="ts">
const name = ref('');
const type = ref(1);

function navigate(){
  return navigateTo({
    path: '/search',
    query: {
      name: name.value,
      type: type.value
    }
  })
}
</script>
```

# 11 - plugins

```ts
export default defineNuxtPlugin({
  name: 'my-plugin',
  enforce: 'pre', // or 'post'
  async setup (nuxtApp) {
    // this is the equivalent of a normal functional plugin
  },
  hooks: {
    // You can directly register Nuxt app runtime hooks here
    'app:created'() {
      const nuxtApp = useNuxtApp()
      // do something in the hook
    }
  },
  env: {
    // Set this value to `false` if you don't want the plugin to run when rendering server-only or island components.
    islands: true
  }
})
```

```ts
export default defineNuxtConfig({
  plugins: [
    '~/plugins/bar/baz',
    '~/plugins/bar/foz'
  ]
})
```

* * *

- Parallel Plugins

```ts
export default defineNuxtPlugin({
  name: 'my-plugin',
  parallel: true,
  async setup (nuxtApp) {
    // the next plugin will be executed immediately
  }
})
```

* * *

- Plugins With Dependencies

```ts
export default defineNuxtPlugin({
  name: 'depends-on-my-plugin',
  dependsOn: ['my-plugin'],
  async setup (nuxtApp) {
    // this plugin will wait for the end of `my-plugin`'s execution before it runs
  }
})
```

* * *

- Providing Helpers

```ts
export default defineNuxtPlugin(() => {
  return {
    provide: {
      hello: (msg: string) => `Hello ${msg}!`
    }
  }
})
```

```ts
export default defineNuxtPlugin({
  name: 'hello',
  setup () {
    return {
      provide: {
        hello: (msg: string) => `Hello ${msg}!`
      }
    }
  }
})
```

```ts
<script setup lang="ts">
// alternatively, you can also use it here
const { $hello } = useNuxtApp()
</script>

<template>
  <div>
    {{ $hello('world') }}
  </div>
</template>
```

* * *

- vue plugins

```ts
import VueGtag, { trackRouter } from 'vue-gtag-next'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(VueGtag, {
    property: {
      id: 'GA_MEASUREMENT_ID'
    }
  })
  trackRouter(useRouter())
})
```

* * *

- Vue Directives

```ts
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.directive('focus', {
    mounted (el) {
      el.focus()
    },
    getSSRProps (binding, vnode) {
      // you can provide SSR-specific props here
      return {}
    }
  })
})
```

# 12 - public

- Files contained within the public/ directory are served at the root and are not modified by the build process. This is suitable for files that have to keep their names (e.g. robots.txt) or likely won't change (e.g. favicon.ico).

# 13 - server

pass

# 14 - .env

- A .env file specifies your build/dev-time environment variables.

* * *

- Custom File

```
npx nuxi dev --dotenv .env.local
```
