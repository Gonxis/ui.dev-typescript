### (Practice) User Defined Type Guards

Below is a CodeSandbox link which has some TypeScript code. Your job is to implement some user defined type guards with type predicates and assertion functions so all of the TypeScript warnings go away.

[User Defined Type Guards CodeSandbox](https://codesandbox.io/s/practice-user-defined-type-guards-2b6d0?file=/src/userDefinedGuard.ts)


src/index.ts
```ts
const app = document.getElementById("app");
if (app) {
  app.innerHTML = `
  <h1>User Defined Type Guards</h1>
  <p>Use the templates provided to create some user-defined type guards, including assertion functions. The templates are in the <code>/src/userDefinedGuard.ts</code> file</p>
  `;
}
```


src/userDefinedGuards.ts
```ts
/* eslint-disable @typescript-eslint/no-unused-vars */
interface Fruit {
  name: string;
  sweetness: number;
  color: unknown;
}

// Add the necessary return types and implementation for these
// user-defined type guards
function isString(maybeString: unknown) {}
function isFruit(maybeFruit: unknown) {}
function assertIsFruit(maybeFruit: unknown) {}

// Don't change anything in this function
function checkFruit(fruit: unknown) {
  if (isFruit(fruit)) {
    if (isString(fruit.color)) {
      console.log(fruit.color.toUpperCase());
    }
  }
  assertIsFruit(fruit);

  console.log(`This fruit is ${fruit.name}`);
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
  "name": "practice-user-defined-type-guards",
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