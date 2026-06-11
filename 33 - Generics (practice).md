### (Practice) Generics

Below is a CodeSandbox link which has some TypeScript code. Your job is to implement a few generic functions and types so all of the TypeScript warnings go away.

[Generics CodeSandbox](https://codesandbox.io/s/practice-generics-z32hw?file=/src/generics.ts)


src/index.ts
```ts
const app = document.getElementById("app");
if (app) {
  app.innerHTML = `
  <h1>Generics</h1>
  <p>This practice is focused with creating and using generic functions and generic types. You'll be tasked with converting existing functions into generic versions. The practice is in <code>/src/generics.ts</code>.</p>
  `;
}
```


src/generics.ts
```ts
/* eslint-disable @typescript-eslint/no-unused-vars */
// Change these functions into generic functions by altering the
// type signatures. There should be no `unknown` types when you are done
function randomFromList(list: unknown[]) {
  const length = list.length;
  const index = Math.floor(Math.random() * length);
  return list[index];
}
function duplicateList(list: unknown[], count: number = 1) {
  let output: unknown[] = [];
  for (let i = 0; i < count; i++) {
    output = output.concat(list);
  }
  return output;
}
function createTuple(item1: unknown, item2: unknown) {
  return [item1, item2];
}

// Use the following interface to constrain the generic in the next function
interface Length {
  length: number;
}
function getLength(item: unknown): number {
  return item.length;
}
```


tsconfig.json
```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "module": "commonjs",
    "jsx": "preserve",
    "esModuleInterop": true,
    "sourceMap": true,
    "allowJs": true,
    "lib": [
      "ESNext",
      "DOM"
    ],
    "target": "ESNext",
    "rootDir": "src",
    "moduleResolution": "node",
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```


package.json
```json
{
  "name": "practice-generics",
  "version": "1.0.0",
  "description": "",
  "main": "index.html",
  "scripts": {
    "start": "parcel index.html --open",
    "build": "parcel build index.html"
  },
  "dependencies": {},
  "devDependencies": {
    "parcel-bundler": "^1.6.1"
  },
  "keywords": []
}
```


index.html
```html
<html>
  <head>
    <title>ui.dev's TypeScript Course</title>
    <meta charset="UTF-8" />
    <link rel="stylesheet" type="text/css" href="theme.css">
  </head>

  <body>
    <ul class='border-container'>
      <li class='border-item red' />
      <li class='border-item blue' />
      <li class='border-item pink' />
      <li class='border-item yellow' />
      <li class='border-item aqua' />
    </ul>
    <div class='container'>
      <div id="app"></div>
    </div>

    <script src="src/index.ts">
    </script>
  </body>
</html>
```


theme.css
```css
/* Ignore this file. You can put your CSS in the styles.css file */

@import url("https://ui.dev/font");

:root {
  --black: #000;
  --white: #fff;
  --red: #f32827;
  --purple: #a42ce9;
  --blue: #2d7fea;
  --yellow: #f4f73e;
  --pink: #eb30c1;
  --gold: #ffd500;
  --aqua: #2febd2;
  --gray: #282c35;
}

*,
*:before,
*:after {
  box-sizing: inherit;
}

html {
  font-family: proxima-nova, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen-Sans, Ubuntu, Cantarell, Helvetica Neue, sans-serif;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  font-size: 18px;
}

body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  background: var(--black);
  color: var(--white);
}

.container {
  margin: 0 auto;
  max-width: 1100px;
  padding: 50px;
}

.border-container {
  padding: 0;
  margin: 0;
  display: flex;
}

.border-item {
  width: 20vw;
  height: 12px;
  list-style-type: none;
}

a {
  color: var(--gold);
  font-weight: 600;
}

.red {
    background: var(--red);
}

.blue {
    background: var(--blue);
}

.pink {
    background: var(--pink);
}

.yellow {
    background: var(--yellow);
}

.aqua {
    background: var(--aqua);
}
```
