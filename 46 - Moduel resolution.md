### Module Resolution

When TypeScript is compiling your project, it will start with the files in your `files` or `includes` list, but as we've found, it doesn't stop there. If one of the TypeScript files imports any other modules, TypeScript will load in that file as well. If it can't find the file, it will throw an error and the compilation will fail.

TypeScript knows how to find files based what you put in your `import` statement using a process called Module Resolution. TypeScript is configured to use a module resolution strategy that is very similar to the one Node.js uses, so if you've used Node.js, Webpack, or something similar, it should be familiar. If you want more information you can read about it in [the TypeScript docs](https://www.typescriptlang.org/docs/handbook/module-resolution.html#node).

TypeScript lets you configure the module resolution strategy, which can be useful depending on the size of your project and how you've structured it. There are a number of settings which affect module resolution, so we'll go through each of them and how you can use them to make your project easier to work with.


#### Relative vs. Non-Relative Imports

Before we move on, it's important to note the difference between relative and non-relative imports.

A non-relative import is anything that just references a file or a module that is not relative to the current file. This includes any file in `node_modules`. For example, `import * as THREE from 'threejs';` will have TypeScript look in the closest `node_modules` directory for a file called `threejs.js`, and then the `threejs` folder that has an `index.js` file inside it. If it can't find a matching file in the current directory, it will jump up one level and search again. If it can't go up any more levels, it fails and throws an error.

Relative imports are entirely based on where the file that is doing the importing is located. These imports start with `./` or `../` and tell TypeScript to look around the importing file to find the file we're looking for. For example, if I was in `/src/FruitBasket/index.ts` and had `import Apple from '../Fruit/apple';`, TypeScript would first look for the `/src/Fruit/apple.ts` file, then a `/src/Fruit/apple/index.ts` file.

One important thing to remember is that you can write TypeScript code that is not completely compliant with ES Modules syntax. In ES Modules, you have to specify the extension of the file you are importing, and you can't import a folder. If you want to take advantage of TypeScript's nuanced module resolution system, you can leave the extension off files that you are imported. However, if you are targeting ES Modules, you'll want to include the `.js` extension, even if you are pointing to a `.ts` file in your imports. Don't worry, TypeScript will know what file you are referencing, and when the code compiles, it will come out with the correct path to your module file.


#### Important Note

These next settings alter the way that you write your `import` statements. Before I go any further, it's **very important** to note that these settings have some pretty big implications.

First, this affects the way your code is written, since we are changing how our `import` statements are written. The TypeScript type checker will be able to tell whether you've written your code correctly, and it will be able to compile your code correctly. But other tools, like Webpack, might get confused as they traverse your dependency tree.

Second, this affects the output of the TypeScript compiler. If you change the way module resolution works and adjust the imports in your code accordingly, those adjustments to your code will transfer into the output. Loading the compiled code in a browser or Node.js will make those environments look for modules exactly where the import statement says they are. If the browser or Node.js can't find the files because the files aren't in the right place, there will be an error.

All of this means you'll need to make adjustments to how your code is consumed to match the changes you make to these settings. Most bundlers, like Webpack, support adjusting module resolution, as does Node.js with the correct packages. If we're working with ES Modules in a browser environment, we have to rearrange our directory structure on our static file server to match the import statements. We'll talk about how to handle module resolution in the sections on configuring TypeScript to work in different environments.

In short, if you change these settings, make sure everything else is configured to consume your TypeScript code properly.


#### `baseUrl`

`baseUrl` is a setting that changes where non-relative imports are resolved from. They don't affect relative modules at all.

Suppose we have a directory structure that looks something like this.

```text
FruityApp
├── src
│   ├── index.ts
│   ├── fruit
│   │   ├── apple.ts
│   │   ├── banana.ts
│   │   ├── fruit.ts
│   │   └── pear.ts
│   └── fruitBasket
│       └── index.ts
└── tsconfig.json
```

If we were to use a relative import to access `apple.ts` from the `fruitBasket/index.ts` file, we would have to do something like this.

```ts
import Apple from "../fruit/apple";
```

Going back just one level in our directory structure is fine, but it can get a little tedious if we are importing a file from even deeper within our project's directory structure.

```ts
import Banana from "../../../../fruit/pear";
```

What `baseUrl` does is tells TypeScript to treat whatever folder we specify as the root of our project and allow us to use it for accessing modules with a non-relative import. It basically treats that root folder the same as our `node_modules` folder. If we were to change it to the `src` directory, we would be able to import anything in `src` without having to navigate up our directory structure.

```ts
import Pear from 'fruit/pear`
```

It can be helpful to think about this in terms of websites. Suppose our app is hosted at `https://fruityapp.ui.dev`. Using relative imports would work exactly the same, regardless of our `baseUrl` setting. But our non-relative import would be resolved relative to the base of our app. If we adjusted our `Pear` import to support ES Modules, our browser would look for that file at `https://fruityapp.ui.dev/fruit/pear.js`.

This setting is helpful in two ways. First, it lets us clean up our code when working with deeply nested relative imports. Second, it lets us change what the import root for our project is in our compiled code when we're using the TypeScript compiler. If we were using a bundler like Webpack, the bundler would take care of the import root for us anyway.


#### `paths`

TypeScript gives us one more tool we can use control our non-relative imports. The `paths` setting lets us specify specific patterns to match specific modules. These patterns accept wildcard (`*`) characters, so they can be pretty flexible.

Let's use the same folder directory again. This time, instead of changing our `baseUrl`, we'll create a special path for our `fruit` folder that can be non-relative imported from anywhere in our project. When using the paths setting, we need to specify a `baseUrl`, since all of the `paths` we list will be relative to the `baseUrl`.

The `paths` setting is a map of the import pattern with a list of directory patterns that it matches. In our case, it looks like this:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@fruit/*": ["src/fruit/*"]
    }
  }
}
```

I'm using `@fruit/*` as my path alias to hopefully avoid any name collisions. Now we can use our non-relative import in `fruitBasket/index.ts`.

```ts
import Apple from "@fruit/apple";
```

Notice how we wrote the path. In the property name, we wrote the shorthand followed by `*`. In the value list, we wrote the directory path followed by `*`. In our import, TypeScript replaced the shorthand with the full directory path, so we could import our file correctly.

As you might guess, we can add multiple items to each `paths` entry to serve as fallback locations. For example, if our directory structure looked more like this:

```text
FruityApp
├── src
│   ├── fruit
│   │   ├── apple.ts
│   │   ├── banana.ts
│   │   ├── fruit.ts
│   │   └── pear.ts
│   └── fruitBasket
│       └── index.ts
├── generated
│   └── fruit
│       ├── strawberry.ts
│       └── lime.ts
└── tsconfig.json
```

We could change our `paths` setting to first look in the `src/fruit` folder and then look in the `generated/fruit` folder.

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@fruit/*": ["src/fruit/*", "generated/fruit/*"]
    }
  }
}
```


#### `paths` and ES Modules

The `paths` setting can really upset the way ES Modules work in browsers. For one thing, all ES Module imports have to begin with a `/`, `./` or `../`. Fortunately we can simulate that behavior with `paths`.

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "/*": ["src/*"]
    }
  }
}
```

What if we are using ES Modules to import modules from a CDN, like `unpkg.com`? This is fairly common when working with small libraries like Preact. With ES Modules, we can import directly from a url.

```ts
import { h } from "https://unpkg.com/preact@10.5.2/dist/preact.min.js";
```

The only problem with this is type checking. TypeScript doesn't download and install files that our project imports from CDNs or external URLs. That means we can't access the type declaration files which are bundled with Preact, so TypeScript can't type check our code.

Using `paths`, we can create a direct connection between this external URL import and a file in our `node_modules` directory. First, we need to install Preact locally. This will put an `index.d.ts` inside our `node_modules` directory. Then, in our `paths` setting, we can connect our import to that declaration file.

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "/*": ["src/*"],
      "https://unpkg.com/preact@10.5.2/dist/preact.min.js": [
        "node_modules/preact/src/index.d.ts"
      ]
    }
  }
}
```

Now Typescript will be able to properly check the types, but we'll still be loading the module from the CDN when our code runs in a browser environment.
