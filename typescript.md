# Typescript

## What is Typescript

Typescript is a `tooling` as well as programming language.It is a `Superset` of javascript adding some features into it for maintainability,scalability,easy to understand and many more ...

## Some info about Vs code editor how it uses ts internally and other language services.

Vs code editor uses TS,HTML,CSS etc... language services internally which is preinstalled on it.If wanted a different `language service` then we install it to use those language service for c,c++,java,php etc...

When ever we hover or type the syntax then according to the service it starts the service for suggestion and brief info or docs links.

When ever new service started then a new process will started by the code editor .

## Use typescript features on js without ts compiler.

By using this comment we can use those features on js file on development
`//@ts-check`

```js
//@ts-check
let isNight = true;
isNight = 45; // this line starts to show error because of there is @ts-check comment is on so TS starts to check it using TS language service.
console.log(isNight);
```

## Running TS file in nodejs

We can run `typescript file` on nodejs interpreter on latest update of nodejs.

> Nodejs `strip out` the additional keywords which is present in TS to make it `vanilla JS to run`.

## Adding types in TS

We can provide a specific types in the TS code to store only a specific value.

```ts
let userFullName: string = "Mohan Lal";
console.log(userFullName);
```

> The `string keyword` used after colon that's we call `types` in TS.
> The way where we adding types is know as `type annotation`.
> `Explicitly` giving types is known as `type annotation`.

![code infer](image.png)

> The pic is showing the term know as `types infer`. TS automatically infer(implicitly) acquire the type and set the type to the variable according to the value datatype.

## Compiling TS to JS with TS compiler

To convert TS code to JS code we need `tsc` compiler.

### Installing `TSC` compiler

There so many ways to install it on various location in our workplace(**System**).

##### Global Package

To run ts compiler use `tsc` after installing compiler .

```bash
npm install -g typescript
```

##### Local Package

To start compiler use `npx tsc` after installation of typescript compiler.

There is two way's to install the local package:-

1. Using Dev dependency

- ```bash
    npm install --save-dev typescript
  ```

- ```bash
    npm install -D typescript
  ```

2. Without Dev dependency

```bash
npm install typescript
```

### How to use `tsc`

> To compile a `TS` to `JS` we use a cmd which known as `tsc`.`tsc cmd` needs file path to compile those file into JS.

```bash
tsc script.ts app.mts server.cts
```

To compile all files at once we needs `tsconfig.json` file .It's not matter the `file empty or having configuration` file is needed.

#### If wanted to create `tsconfig.json` using `tsc cmd` (Optional)

For global binary package

```bash
tsc --init
```

For local binary package

```bash
npx tsc --init
```

## Configuring tsconfig.json for Compiling TypeScript to JavaScript

When compiling TypeScript into JavaScript, we can configure the `tsconfig.json` file, and both `tsc` and the TypeScript language service will use it — the compilation will behave according to the configuration we set.

```json
{
  "compiler-option": {
    "target": "es2017", // Sets the version of JavaScript the TypeScript code is compiled into.
    "onEmitOnError": true, // If true => when the TypeScript code has some error, it will not output JavaScript.
    "removeComments": true, // If true => when TypeScript has some comments and it is compiled into JavaScript, all comments will be removed.
    "rootDir": "./src", // The directory containing all TS files.
    "outDir": "dist" // The directory for the JavaScript files after compiling into JS.
  }
}
```
