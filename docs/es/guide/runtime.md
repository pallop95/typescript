
# Tiempo de Ejecución (opcional)

TypeScript en tiempo de ejecución es requerido para archivos que no son compilados por Webpack como lo es el archivo **nuxt.config**, **modules** locales y **serverMiddlewares**

Nuxt.js ha creado un envolvente de TypeScript en tiempo de ejecución bajo un paquete dedicado **`@nuxt/typescript-runtime`**. El envolventes es un binario llamado **nuxt-ts** que registra [**ts-node**](https://github.com/TypeStrong/ts-node) detrás de escena antes de correrlo.

## Instalación

```sh
yarn add @nuxt/typescript-runtime
# o tambien
npm install @nuxt/typescript-runtime
```

::: tip
Nota este paquete es instalado como `dependency` y no como `devDependency` igual a `@nuxt/typescript-build`, porque `@nuxt/typescript-runtime` es necesario en producción.
:::

## Uso

Todo lo que necesitas es actualizar tu archivo **package.json**:

```json{2-5}
"scripts": {
  "dev": "nuxt-ts",
  "build": "nuxt-ts build",
  "generate": "nuxt-ts generate",
  "start": "nuxt-ts start"
},
"dependencies": {
  "@nuxt/typescript-runtime": "latest",
  "nuxt": "latest",
},
"devDependencies": {
  "@nuxt/types": "latest",
  "@nuxt/typescript-build": "latest"
}
```

::: tip
**nuxt-ts** tambien funciona si usted esta usando la version edge de Nuxt.js (**nuxt-edge**).
:::

Usted puede ahora usar TypeScript para el archivo **nuxt.config**, **modulos** locales y **serverMiddlewares**.

::: warning

`@nuxt/typescript-runtime` no soporta uso programado (como esto extiende de `@nuxt/cli`).

Los usuarios avanzados pueden intentar agregar el siguiente código al punto de entrada de su servidor (ver [fuente](https://github.com/nuxt/typescript/blob/master/packages/typescript-runtime/src/index.ts)):

```js
import { register } from 'ts-node'

register({
  project: 'tsconfig.json',
  compilerOptions: {
    module: 'commonjs'
  },
  transpileOnly: true
})
```

Igualmente, esto es **no recomendado o soportado**.
:::
