---
title: "Nuxt3 – CHEAT SHEET 03"
date: "2024-04-08"
categories: 
  - "code-learning"
  - "learn-open-source-project"
tags: 
  - "cheat-sheet"
  - "nuxt"
  - "open-source"
  - "typescript"
coverImage: "e2f5a847dcf94fd0b34423f4b9f16bb9.jpg"
---

# Components

## ClientOnly

- Render components only in client-side with the `<ClientOnly>` component.
    
- props
    
    - `placeholderTag | fallbackTag`: specify a tag to be rendered server-side.
    - `placeholder | fallback`: specify a content to be rendered server-side.

## DevOnly

- Render components only during development with the `<DevOnly>` component.
- slots
    - `#fallback`: if you ever require to have a replacement during production.

## NuxtClientFallback

- Nuxt provides the `<NuxtClientFallback>` component to render its content on the client if any of its children trigger an error in SSR
- events
    - `@ssr-error`: Event emitted when a child triggers an error in SSR. Note that this will only be triggered on the server.
- props
    - `placeholderTag | fallbackTag`: Specify a fallback tag to be rendered if the slot fails to render on the server.
    - `placeholder | fallback`: Specify fallback content to be rendered if the slot fails to render
    - `keepFallback`: Keep the fallback content if it failed to render server-side.
- slots
    - `#fallback`: specify content to be displayed server-side if the slot fails to render.

## NuxtPage

- The `<NuxtPage>` component is required to display pages located in the pages/ directory.
- props
    - `name`: tells RouterView to render the component with the corresponding name in the matched route record's components option.
    - `route`: route location that has all of its components resolved.
    - `pageKey`: control when the NuxtPage component is re-rendered.
    - `transition`: define global transitions for all pages rendered with the NuxtPage component.
    - `keepalive`: control state preservation of pages rendered with the NuxtPage component

## NuxtLayout

- Nuxt provides the `<NuxtLayout>` component to show layouts on pages and error pages.
- props
    - `name`: Specify a layout name to be rendered, can be a string, reactive reference or a computed property. It must match the name of the corresponding layout file in the `layouts/` directory.

## NuxtLink

- Nuxt provides `<NuxtLink>` component to handle any kind of links within your application.
- props
    - RouterLink
        - `to`: Any URL or a route location object from Vue Router.
        - `custom`: Whether `<NuxtLink>` should wrap its content in an `<a>` element. It allows taking full control of how a link is rendered and how navigation works when it is clicked. Works the same as Vue Router's custom prop.
        - `exactActiveClass`: A class to apply on exact active links. Works the same as Vue Router's exact-active-class prop on internal links. Defaults to Vue Router's default "router-link-exact-active").
        - `replace`: Works the same as Vue Router's replace prop on internal links.
        - `ariaCurrentValue`: An aria-current attribute value to apply on exact active links. Works the same as Vue Router's aria-current-value prop on internal links.
        - `activeClass`: A class to apply on active links. Works the same as Vue Router's active-class prop on internal links. Defaults to Vue Router's default ("router-link-active")
    - NuxtLink
        - `href`: An alias for to. If used with to, href will be ignored.
        - `noRel`: If set to true, no rel attribute will be added to the link.
        - `external`: Forces the link to be rendered as an a tag instead of a Vue Router RouterLink.
        - `prefetch`: When enabled will prefetch middleware, layouts and payloads (when using payloadExtraction) of links in the viewport. Used by the experimental crossOriginPrefetch config.
        - `noPrefetch`: Disables prefetching.
        - `prefetchedClass`: A class to apply to links that have been prefetched.
    - Anchor
        - `target`: A target attribute value to apply on the link.
        - `rel`: A rel attribute value to apply on the link. Defaults to "noopener noreferrer" for external links.

## NuxtLoadingIndicator

- Display a progress bar between page navigations.
- props
    - `color`: The color of the loading bar. It can be set to false to turn off explicit color styling. height: Height of the loading bar, in pixels (default 3).
    - `duration`: Duration of the loading bar, in milliseconds (default 2000).
    - `throttle`: Throttle the appearing and hiding, in milliseconds (default 200).
    - `estimatedProgress`: By default Nuxt will back off as it approaches 100%. You can provide a custom function to customize the progress estimation, which is a function that receives the duration of the loading bar (above) and the elapsed time. It should return a value between 0 and 100.

## NuxtErrorBoundary

- The `<NuxtErrorBoundary>` component handles client-side errors happening in its default slot.
- events
    - `@error`: Event emitted when the default slot of the component throws an error.
- slots
    - `#error`: Specify a fallback content to display in case of error.

## NuxtIsland

- Nuxt provides the `<NuxtIsland>` component to render a non-interactive component without any client JS.
    
- props
    
    - `name` : Name of the component to render.
    - `lazy`: Make the component non-blocking.
    - `props`: Props to send to the component to render.
    - `source`: Remote source to call the island to render.
    - `dangerouslyLoadClientComponents`: Required to load components from a remote source.
- slots
    
    - `#fallback`: Specify the content to be rendered before the island loads (if the component is lazy) or if NuxtIsland fails to fetch the component.
- ref
    
    - `refresh()`: force refetch the server component by refetching it.
- events
    
    - error: emitted when when NuxtIsland fails to fetch the new island.

## NuxtImg

- Nuxt provides a `<NuxtImg>` component to handle automatic image optimization.
- `npx nuxi@latest module add image`

```html
<NuxtImg src="/nuxt-icon.png" />
```

## NuxtPicture

- Nuxt provides a `<NuxtPicture>` component to handle automatic image optimization.
- `npx nuxi@latest module add image`

## Teleport

- The `<Teleport>` component teleports a component to a different location in the DOM.

```html
<template>
  <button @click="open = true">
    Open Modal
  </button>
  <Teleport to="body">
    <div v-if="open" class="modal">
      <p>Hello from the modal!</p>
      <button @click="open = false">
        Close
      </button>
    </div>
  </Teleport>
</template>
```

# Composables

- useAppConfig
- useAsyncData
- useCookie
- useError
- useFetch
- useHead
- useHeadSafe
- useHydration
- useId
- useLazyAsyncData
- useLazyFetch
- useLoadingIndicator
- useNuxtApp
- useNuxtData
- usePreviewMode
- useRequestEvent
- useRequestHeader
- useRequestHeaders
- useRequestURL
- useRoute
- useRouter
- useRuntimeConfig
- useSeoMeta
- useServerSeoMeta
- useState

# Utils

- $fetch
- abortNavigation
- addRouteMiddleware
- callOnce
- clearError
- clearNuxtData
- clearNuxtState
- createError
- defineNuxtComponent
- defineNuxtRouteMiddleware
- definePageMeta
- defineRouteRules
- navigateTo
- onBeforeRouteLeave
- onBeforeRouteUpdate
- onNuxtReady
- prefetchComponents
- preloadComponents
- preloadRouteComponents
- prerenderRoutes
- refreshCookie
- refreshNuxtData
- reloadNuxtApp
- setPageLayout
- setResponseStatus
- showError
- updateAppConfig

# Commands

- nuxi add
- nuxi analyze
- nuxi build
- nuxi build-module
- nuxi cleanup
- nuxi dev
- nuxi devtools
- nuxi generate
- nuxi info
- nuxi init
- nuxi module
- nuxi prepare
- nuxi preview
- nuxi typecheck
- nuxi upgrade

# hooks

## App Hooks (runtime)

Check the [app source code](https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/nuxt.ts#L27) for all available hooks.

| Hook | Arguments | Environment | Description |
| --- | --- | --- | --- |
| `app:created` | `vueApp` | Server & Client | Called when initial `vueApp` instance is created. |
| `app:error` | `err` | Server & Client | Called when a fatal error occurs. |
| `app:error:cleared` | `redirect?` | Server & Client | Called when a fatal error occurs. |
| `app:data:refresh` | `keys?` | Server & Client | (internal) |
| `vue:setup` | \- | Server & Client | (internal) |
| `vue:error` | `err, target, info` | Server & Client | Called when a vue error propagates to the root component. [Learn More](https://vuejs.org/api/composition-api-lifecycle.html#onerrorcaptured). |
| `app:rendered` | `renderContext` | Server | Called when SSR rendering is done. |
| `app:redirected` | \- | Server | Called before SSR redirection. |
| `app:beforeMount` | `vueApp` | Client | Called before mounting the app, called only on client side. |
| `app:mounted` | `vueApp` | Client | Called when Vue app is initialized and mounted in browser. |
| `app:suspense:resolve` | `appComponent` | Client | On [Suspense](https://vuejs.org/guide/built-ins/suspense.html#suspense) resolved event. |
| `app:manifest:update` | `id, timestamp` | Client | Called when there is a newer version of your app detected. |
| `link:prefetch` | `to` | Client | Called when a `<NuxtLink>` is observed to be prefetched. |
| `page:start` | `pageComponent?` | Client | Called on [Suspense](https://vuejs.org/guide/built-ins/suspense.html#suspense) pending event. |
| `page:finish` | `pageComponent?` | Client | Called on [Suspense](https://vuejs.org/guide/built-ins/suspense.html#suspense) resolved event. |
| `page:loading:start` | \- | Client | Called when the `setup()` of the new page is running. |
| `page:loading:end` | \- | Client | Called after `page:finish` |
| `page:transition:finish` | `pageComponent?` | Client | After page transition [onAfterLeave](https://vuejs.org/guide/built-ins/transition.html#javascript-hooks) event. |
| `dev:ssr-logs` | `logs` | Client | Called with an array of server-side logs that have been passed to the client (if `features.devLogs` is enabled). |
| `page:view-transition:start` | `transition` | Client | Called after `document.startViewTransition` is called when [experimental viewTransition support is enabled](https://nuxt.com/docs/getting-started/transitions#view-transitions-api-experimental). |

## Nuxt Hooks (build time)

Check the [schema source code](https://github.com/nuxt/nuxt/blob/main/packages/schema/src/types/hooks.ts#L53) for all available hooks.

| Hook | Arguments | Description |
| --- | --- | --- |
| `kit:compatibility` | `compatibility, issues` | Allows extending compatibility checks. |
| `ready` | `nuxt` | Called after Nuxt initialization, when the Nuxt instance is ready to work. |
| `close` | `nuxt` | Called when Nuxt instance is gracefully closing. |
| `restart` | `hard?: boolean` | To be called to restart the current Nuxt instance. |
| `modules:before` | \- | Called during Nuxt initialization, before installing user modules. |
| `modules:done` | \- | Called during Nuxt initialization, after installing user modules. |
| `app:resolve` | `app` | Called after resolving the `app` instance. |
| `app:templates` | `app` | Called during `NuxtApp` generation, to allow customizing, modifying or adding new files to the build directory (either virtually or to written to `.nuxt`). |
| `app:templatesGenerated` | `app` | Called after templates are compiled into the [virtual file system](/docs/guide/directory-structure/nuxt#virtual-file-system) (vfs). |
| `build:before` | \- | Called before Nuxt bundle builder. |
| `build:done` | \- | Called after Nuxt bundle builder is complete. |
| `build:manifest` | `manifest` | Called during the manifest build by Vite and webpack. This allows customizing the manifest that Nitro will use to render `<script>` and `<link>` tags in the final HTML. |
| `builder:generateApp` | `options` | Called before generating the app. |
| `builder:watch` | `event, path` | Called at build time in development when the watcher spots a change to a file or directory in the project. |
| `pages:extend` | `pages` | Called after pages routes are resolved. |
| `pages:routerOptions` | `files: Array<{ path: string, optional?: boolean }>` | Called when resolving `router.options` files. Later items in the array override earlier ones. |
| `server:devHandler` | `handler` | Called when the dev middleware is being registered on the Nitro dev server. |
| `imports:sources` | `presets` | Called at setup allowing modules to extend sources. |
| `imports:extend` | `imports` | Called at setup allowing modules to extend imports. |
| `imports:context` | `context` | Called when the [unimport](https://github.com/unjs/unimport) context is created. |
| `imports:dirs` | `dirs` | Allows extending import directories. |
| `components:dirs` | `dirs` | Called within `app:resolve` allowing to extend the directories that are scanned for auto-importable components. |
| `components:extend` | `components` | Allows extending new components. |
| `nitro:config` | `nitroConfig` | Called before initializing Nitro, allowing customization of Nitro's configuration. |
| `nitro:init` | `nitro` | Called after Nitro is initialized, which allows registering Nitro hooks and interacting directly with Nitro. |
| `nitro:build:before` | `nitro` | Called before building the Nitro instance. |
| `nitro:build:public-assets` | `nitro` | Called after copying public assets. Allows modifying public assets before Nitro server is built. |
| `prerender:routes` | `ctx` | Allows extending the routes to be pre-rendered. |
| `build:error` | `error` | Called when an error occurs at build time. |
| `prepare:types` | `options` | Called before Nuxi writes `.nuxt/tsconfig.json` and `.nuxt/nuxt.d.ts`, allowing addition of custom references and declarations in `nuxt.d.ts`, or directly modifying the options in `tsconfig.json` |
| `listen` | `listenerServer, listener` | Called when the dev server is loading. |
| `schema:extend` | `schemas` | Allows extending default schemas. |
| `schema:resolved` | `schema` | Allows extending resolved schema. |
| `schema:beforeWrite` | `schema` | Called before writing the given schema. |
| `schema:written` | \- | Called after the schema is written. |
| `vite:extend` | `viteBuildContext` | Allows to extend Vite default context. |
| `vite:extendConfig` | `viteInlineConfig, env` | Allows to extend Vite default config. |
| `vite:configResolved` | `viteInlineConfig, env` | Allows to read the resolved Vite config. |
| `vite:serverCreated` | `viteServer, env` | Called when the Vite server is created. |
| `vite:compiled` | \- | Called after Vite server is compiled. |
| `webpack:config` | `webpackConfigs` | Called before configuring the webpack compiler. |
| `webpack:configResolved` | `webpackConfigs` | Allows to read the resolved webpack config. |
| `webpack:compile` | `options` | Called right before compilation. |
| `webpack:compiled` | `options` | Called after resources are loaded. |
| `webpack:change` | `shortPath` | Called on `change` on WebpackBar. |
| `webpack:error` | \- | Called on `done` if has errors on WebpackBar. |
| `webpack:done` | \- | Called on `allDone` on WebpackBar. |
| `webpack:progress` | `statesArray` | Called on `progress` on WebpackBar. |

## Nitro App Hooks (runtime, server-side)

See [Nitro](https://nitro.unjs.io/guide/plugins#available-hooks) for all available hooks.

| Hook | Arguments | Description | Types |
| --- | --- | --- | --- |
| `dev:ssr-logs` | `path, logs` | Server | Called at the end of a request cycle with an array of server-side logs. |
| `render:response` | `response, { event }` | Called before sending the response. | [response](https://github.com/nuxt/nuxt/blob/71ef8bd3ff207fd51c2ca18d5a8c7140476780c7/packages/nuxt/src/core/runtime/nitro/renderer.ts#L24), [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38) |
| `render:html` | `html, { event }` | Called before constructing the HTML. | [html](https://github.com/nuxt/nuxt/blob/71ef8bd3ff207fd51c2ca18d5a8c7140476780c7/packages/nuxt/src/core/runtime/nitro/renderer.ts#L15), [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38) |
| `render:island` | `islandResponse, { event, islandContext }` | Called before constructing the island HTML. | [islandResponse](https://github.com/nuxt/nuxt/blob/e50cabfed1984c341af0d0c056a325a8aec26980/packages/nuxt/src/core/runtime/nitro/renderer.ts#L28), [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38), [islandContext](https://github.com/nuxt/nuxt/blob/e50cabfed1984c341af0d0c056a325a8aec26980/packages/nuxt/src/core/runtime/nitro/renderer.ts#L38) |
| `close` | \- | Called when Nitro is closed. | \- |
| `error` | `error, { event? }` | Called when an error occurs. | [error](https://github.com/unjs/nitro/blob/main/src/runtime/types.ts#L24), [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38) |
| `request` | `event` | Called when a request is received. | [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38) |
| `beforeResponse` | `event, { body }` | Called before sending the response. | [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38), unknown |
| `afterResponse` | `event, { body }` | Called after sending the response. | [event](https://github.com/unjs/h3/blob/f6ceb5581043dc4d8b6eab91e9be4531e0c30f8e/src/types.ts#L38), unknown |
