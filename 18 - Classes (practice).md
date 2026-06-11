### (Practice) Classes

Below is a CodeSandbox link which has some TypeScript code. Your job is to define two classes. There are a set of tests that automatically run when you make changes to the classes. Follow the instructions in the test names to create the classes so the tests pass. Once you are done making the tests pass, make sure there are no TypeScript errors in the `classes.test.ts` file.

[Classes CodeSandbox](https://codesandbox.io/s/practice-classes-vrrkr?file=/src/classes.ts)

src/classes.test.ts
```ts
import { Apple, Fruit } from "./classes";

// This type declaration makes the test utilities
// not throw type errors.
declare global {
  function describe(name: string, implementation: Function): void;
  function it(name: string, implementation: Function): void;
  function expect(value: any): any;
}

describe("fruit class", () => {
  it("should instantiate with just a name", () => {
    const fruit = new Fruit("Apple");

    expect(fruit.name).toEqual("Apple");
  });
  it("should include a protected sweetness value that is 50 by default", () => {
    const fruit = new Fruit("Apple");

    expect(fruit.name).toEqual("Apple");
    // Since this value is protected, TypeScript will throw an error here
    // We want to read this value in our tests, so we will expect the error
    // @ts-expect-error
    expect(fruit.sweetness).toEqual(50);
  });
  it("should instantiate with a name and sweetness value", () => {
    const fruit = new Fruit("Fruit", 80);

    expect(fruit.name).toEqual("Fruit");
    // @ts-expect-error
    expect(fruit.sweetness).toEqual(80);
  });
  it("should include a get accessor called `tasty` that returns true if sweetness is greater than 60", () => {
    const fruit = new Fruit("Fruit", 80);
    expect(fruit.tasty).toEqual(true);

    const notTasty = new Fruit("Fruit", 40);
    expect(notTasty.tasty).toEqual(false);
  });
  it("should have a private 'isEdible' boolean property that is true.", () => {
    const fruit = new Fruit("Fruit");

    // @ts-expect-error
    expect(fruit.isEdible).toBe(true);
  });
  it('should have a static method called `cook` that cooks the fruit. It takes a fruit instance and returns a string that says "Cooked {fruit.name}"', () => {
    const fruit = new Fruit("Fruit", 80);

    expect(Fruit.cook(fruit)).toEqual("Cooked Fruit");
  });
});

describe("apple class", () => {
  it("should instantiate properly, and include a variety field", () => {
    const fiji = new Apple("fiji");
    expect(fiji instanceof Fruit).toBeTruthy();
    expect(fiji.name).toEqual("Apple");
    expect(fiji.variety).toEqual("fiji");
  });
});
```


src/classes.ts
```ts
export class Fruit {
  constructor() {}
}

export class Apple extends Fruit {}
```


src/index.ts
```ts
const app = document.getElementById("app");
if (app) {
  app.innerHTML = `
  <h1>Classes</h1>
  <p>This practice is a little different. Instead of just making sure TypeScript's 
  type checker passes, you also need to write your code to match some automated tests. 
  Switch the CodeSandbox tab from 'Browser' to 'Tests' to see the automated tests in action.
  Then, update the code in <code>/src/classes.ts</code> to make the tests pass. Finally, make
  sure you double check <code>/src/classes.test.ts</code> to make sure TypeScript's type checker is passing 
  in that file too.
  `;
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
  "name": "practice-classes",
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


types.d.ts
```ts
export {}

declare global
```
