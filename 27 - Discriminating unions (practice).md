### (Practice) Discriminating Unions

Below is a CodeSandbox link which has some TypeScript code. Your job is to add the appropriate properties and checks so all of the TypeScript warnings go away.

[Discriminating Unions CodeSandbox](https://codesandbox.io/s/practice-discriminating-unions-pm4tx?file=/src/discriminatingUnions.ts)


src/index.ts
```ts
const app = document.getElementById("app");
if (app) {
  app.innerHTML = `
  <h1>Discriminating Unions</h1>
  <p>This should hopefully be a simple practice. All you have to do is fix all
  of the type errors by creating a Discriminating Union. You will also have to
  add the necessary check to see which type the value has. The practice is in <code>/src/discriminatingUnions.ts</code>.</p>
  `;
}
```

src/discriminatingUnions.ts
```ts
/* eslint-disable @typescript-eslint/no-unused-vars */
interface MovingThing {
  speed: number;
}

// Add the necessary properties to allow for discriminating unions
interface Car extends MovingThing {
  wheels: number;
}
interface Boat extends MovingThing {
  drag: number;
}
interface Plane extends MovingThing {
  drag: number;
  engines: number;
}
interface Train extends MovingThing {
  cars: number;
  wheels: number;
}

type Vehicle = Car | Boat | Plane | Train;

// Without changing the parameter type, use discriminating unions
// to fix the type errors
function speed(vehicle: Vehicle) {
  console.log(vehicle.speed);
}
function wheelCount(vehicle: Vehicle) {
  console.log(vehicle.wheels);
}
function dragAmount(vehicle: Vehicle) {
  console.log(vehicle.drag);
}
function numberOfCars(vehicle: Vehicle) {
  console.log(vehicle.cars);
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
  "name": "practice-discriminating-unions",
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