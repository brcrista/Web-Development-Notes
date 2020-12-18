# JavaScript Modules

I've always been confused by JavaScript's module system.
When I had been learning about it about 3 years ago, the ES6 module spec was defined, but no browsers actually implemented it, and Node didn't implement it either.
And then there was the competing standards of CommonJS and AMD.

Meanwhile, TypeScript has supported ES6 modules, but I wasn't clear on how to do it in pure JavaScript.

## CommonJS vs. ES6 modules

Today (July 2020), browsers do support ES6 modules.
You import a module script like this:

```html
<script type="module" src="script.js"></script>
```

But, you get CORS errors if you try to run this locally, so it's not that useful in my opinion.
Seems like Webpack is still the way to go here.

Also, Node still doesn't support ES6 modules.
As of Node 14, it's still in experimental status.
Node's module system, using `require`, still uses a CommonJS-ish convention:

```js
'use strict';

function hello() {
    return "hello";
}

exports.hello = hello;
```

When I looked at how TypeScript compiled my modules, it was using the CommonJS convention.
This is because of the `module` setting in the `tsconfig.json`.

## Packaging Modules as NPM packages

NPM packages are separate from the concept of modules.
An NPM package must either have a `package.json` or a file named `index.js`.
To package your code with `npm`, run `npm pack`.
This will produce a `.tgz` file of your package.
You can also use an `.npmignore` file to exclude certain files or directories from the package.

When you use `require` to load a module in Node, `node_modules` is included in the search path.
So, you just pass the path to the module relative to the `node_modules` directory.

When you just import a package by its name (so, the name of the directory, not a specific file), it will import the module designated by the `"main"` field in the `package.json`.

### NPM and build output (`dist/`)

This works fine if your package is just the source tree, but usually this isn't the case.
You might use tools such as Webpack, Babel, or TypeScript to produce the actual code you want to distribute.
(It's conventional in JavaScript for this output to go in a directory named `dist`.)

This poses a couple of problems:
- If you pack your project like this, you'll have to add `/dist` to the path in `require`.
- If you're consuming the package from a TypeScript project, TypeScript won't find the type declarations for the file.


The way to get around this is to use the `main` file of the package (specified in the `package.json`, see above).

### NPM and TypeScript

There are a couple of TypeScript compiler settings that affect loading modules:
- `module`
- `moduleResolution`

When working with NPM packages, make sure `module` is set to `commonjs`.
`moduleResolution` should default to the correct value.

If you get a compiler error like

```
Cannot find module 'your-package-name' or its corresponding type declarations.ts(2307)
```

then TypeScript isn't able to find the type declarations for your package.

While the actual module loading is handled by Node, TypeScript needs to find the `.d.ts` files for the module.
If you've published `.d.ts` files along with your package (usually when the package is written in TypeScript), then the modified `package.json` produced by `npm pack` should include a `"types"` property for the `.d.ts` file.
If types are published separately through a `@types` package, then TypeScript will look there.

You can debug module loading by passing the `--traceResolution` compiler flag.
This will tell you exactly which paths the TypeScript compiler is looking in for the declaration files.
