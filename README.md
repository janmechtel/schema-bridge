# schema-bridge

This is an experiment (think home cooked meal) to help with building integrations between APIs.

When building integrations between APIs one is often faced with stichting those apis together and transforming the data.

- Situation: You have some source json, from some APIs/webhooks and some target json how I need to send it out
- Complication: I need to transform it and re-map the fields. Depending on the complexity of the objects that might require some fiddling
- Solution: I'd love a visual data mapper that allows me to
  - see the source and target spec
  - example values maybe even API descriptions
  - create simple transformation with Type/Javascript, JSONata, JQ, JMESpath or similar
  - connect the target and source values visually
  - documentation - the visual aspect is important to help readers, as this is easier to understand/digest the integration, not only "build" it. Also it serves as a kind of todo-list. It's easy to see if something isn't mapped yet

## Existing tools

- many are code first/only like [JOLT](https://jolt-demo.appspot.com/#incept)
- [Ballerina Data Mapper](https://ballerina.io/learn/vs-code-extension/implement-the-c) - Data Mapper is pretty spot on, but is ballerina, a language I'm not familiar with yet. Does this exist for Javascript?
- https://www.postman.com/product/flows/ - can this do object mapping or only "steps" of the flow? It seems to only work by exposing paramaters. I can't really map complicated json objects quickly

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```