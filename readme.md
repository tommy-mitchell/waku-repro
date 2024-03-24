# waku `vite-plugin-checker` repro

Initialized with `create waku` and added `vite-plugin-checker` to the project:

```sh
npm create waku@next
cd waku-repro
npm i vite-plugin-checker -D # and add to vite.config.ts
npm run dev
```

## To Replicate

1. Clone repo
2. Run `npm install`
3. Run `npm run dev`

## Error Message

```
$ npm run dev
ready: Listening on http://localhost:3000/

node:internal/event_target:1100
  process.nextTick(() => { throw err; });
                           ^
TypeError [Error]: Cannot read properties of undefined (reading 'env')
    at Object.workerScript (…/node_modules/vite-plugin-checker/dist/esm/worker.js:43:34)
    at TscChecker.initWorkerThread (…/node_modules/vite-plugin-checker/dist/esm/Checker.js:38:19)
    at TscChecker.init (…/node_modules/vite-plugin-checker/dist/esm/checkers/typescript/main.js:137:11)
    at …/node_modules/vite-plugin-checker/dist/esm/checkers/typescript/main.js:142:12
    at ModuleJob.run (node:internal/modules/esm/module_job:218:25)
    at async ModuleLoader.import (node:internal/modules/esm/loader:329:24)
    at async createCheckers (…/node_modules/vite-plugin-checker/dist/esm/main.js:30:37)
    at async config (…/node_modules/vite-plugin-checker/dist/esm/main.js:63:18)
    at async runConfigHook (…/node_modules/waku/node_modules/vite/dist/node/chunks/dep-jvB8WLp9.js:68303:25)
    at async resolveConfig (…/node_modules/waku/node_modules/vite/dist/node/chunks/dep-jvB8WLp9.js:67760:14)
Emitted 'error' event on Worker instance at:
    at [kOnErrorMessage] (node:internal/worker:326:10)
    at [kOnMessage] (node:internal/worker:337:37)
    at MessagePort.<anonymous> (node:internal/worker:232:57)
    at [nodejs.internal.kHybridDispatch] (node:internal/event_target:826:20)
    at exports.emitMessage (node:internal/per_context/messageport:23:28)

Node.js v20.11.0
```

This is the line that fails:

```js
const isBuild = workerData.env.command === "build";
```
