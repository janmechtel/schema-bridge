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

## Existing tools / alternatives / inspiration

- [Ballerina Data Mapper](https://ballerina.io/learn/vs-code-extension/implement-the-c) - Data Mapper is pretty spot on, but is ballerina, a language I'm not familiar with yet. Does this exist for Javascript?
- many are code first/only like [JOLT](https://jolt-demo.appspot.com/#incept)
- https://www.postman.com/product/flows/ - can this do object mapping or only "steps" of the flow? It seems to only work by exposing paramaters. I can't really map complicated json objects quickly
- [JSONCrack](https://jsoncrack.com/) great visualization, but i don't understand how the "compare data" works and whether it would help with mapping/transforming

## Roadmap

- [X] make the transformation editable
- [X] Apply the transformation live
- [X] Deploy to github pages https://janmechtel.github.io/schema-bridge/
- [X] test it with easy stuff recreate the [sample from Ballerina data mapper](https://ballerina.io/learn/vs-code-extension/implement-the-code/data-mapper/)
- [X] add a new component "editor" that for now only contains the textarea, the content should be 2-way bound from the app.vue

- [X] add a target area
- [X] better editor (json syntax highlighting etc. using Monaco)

- [X] show a diff between transformation output and target
- [X] refactor the diff editor into it's own component
- [ ] easy way to import & export everything

- Test with something real

- [ ] visual mapping (without editing) 
    - [X] show a list of source & target fields
    - [X] show a list of transformation fields
    - show a table with 3 columns "source" "target" "transformation"
    - selecting a row highlights back to the code edit areas? can everything stay in one line?

- [ ] register [jsonata as language](https://github.com/jsonata-js/jsonata-exerciser/blob/master/src/jsonataMode.js)

- [ ] filtering (only show fields that are mapped or not mapped)
- [ ] test/support arrays - How to deal with their type?
- [ ] work with OpenAPI spec 
- [ ] support for descriptions types and required fields
- [ ] enable editing in the visual part
- [ ] UI collapse, resize the editors more freely

# Recommended IDE Setup

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

### Deploy to GitHub pages

```sh
npm run deploy
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
