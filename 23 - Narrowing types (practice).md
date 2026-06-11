### (Practice) Narrowing Types

Below is a CodeSandbox link which has some TypeScript code. Your job is to narrow all of the types so the TypeScript warnings go away. Don't change the type annotations unless the instructions tell you to - instead, use type narrowing to determine what the type actually is.

[Narrowing Types CodeSandbox](https://codesandbox.io/s/practice-type-guards-neqko?file=/src/typeGuards.ts)

src/index.ts
```ts
const app = document.getElementById("app");
if (app) {
  app.innerHTML = `
  <h1>Type Guards</h1>
  <p>As you work through fixing the type errors in this section, it might be tempting to change the parameter or return types for these
  functions. <strong>Don't</strong>. The purpose of this exercise is to practice type guards. It's possible to fix the
  type errors without making any changes. You'll find the practice functions in the <code>/src/typeGuards.ts</code> folder.
  `;
}
```


src/styles.css
```css
/* Your CSS goes here */
```


src/typeGuards.ts
```ts
/* eslint-disable @typescript-eslint/no-unused-vars */
// Without changing the input or return types of the functions, fix all of the TypeScript errors with type narrowing
// If the input is an invalid type, feel free to throw an error in your function.
function doubleIfNumber(input: unknown) {
  return input * 2;
}

function combineValues(input1: unknown, input2: unknown): string | number {
  return input1 + input2;
}

function appendToArray(list: unknown, input: unknown): string[] {
  return list.concat(input);
}

function sumArray(list: unknown) {
  return list.reduce((accumulator: number, item: number) => {
    return accumulator + item;
  }, 0);
}

// The type of "sum" should not be "any"
const sum = sumArray([1, 2, 3]);

interface Fruit {
  name: string;
  color?: string;
  eat?: () => void;
}
function shoutFruitName(fruit: object | Fruit) {
  console.log(fruit.name.toUpperCase());
}

function shoutFruitColor(fruit: Fruit) {
  console.log(fruit.color.toUpperCase());
}

function eatFruit(fruit: Fruit) {
  fruit.eat();
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


package.json
```json
{
  "name": "practice-type-guards",
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


tsconfig.json
```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "alwaysStrict": true,
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
