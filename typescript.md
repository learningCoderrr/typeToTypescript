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
    "outDir": "dist", // The directory for the JavaScript files after compiling into JS.
    "sourceMap": true //If true => it creates a standalone sourceMap file for the linking for minified and ugly code and original source code.
  },
  "include": [],
  // A list of file names or folder paths (can use wildcards like *.ts)
  // telling TypeScript WHICH files to compile/convert into working code.

  "exclude": []
  // A list of file names or folder paths (can use wildcards like *.ts)
  // telling TypeScript WHICH files to SKIP — these won't be compiled
  // or included in the final output.
}
```

## Source Maps

## The Problem

When we ship JavaScript to production, we usually **minify** and **uglify** it first:

> **Minify** = code-optimize,remove all extra spaces, line breaks, and comments to make the file smaller.
> **Uglify** = also shorten variable/function names (like `getUserData` becomes `a`) to make it even smaller.

The result: your whole file might turn into one giant, unreadable line of code.

**The problem:** if something breaks in production and you open DevTools to debug it, all you see is this messy, unreadable code. You can't tell what's actually going wrong.

## The Solution: Source Maps

Think of a source map like a **translator** sitting between your messy production code and your original clean code.

It's a separate file that says: _"this position in the ugly code = this position in the original code."_

So when you open DevTools, instead of seeing the ugly file, you see your **original, clean source code** — even though the browser is really running the ugly version behind the scenes.

Under the hood, source maps store all these position-mappings using something called **VLQ (Variable-Length Quantity)** — just a compact way of encoding numbers so the map file itself doesn't become huge.

## How a Source Map Gets Loaded

**Option 1 — Manually:**

1. Open DevTools
2. Go to the Sources panel
3. Right-click the ugly file
4. Point it to the `.map` file's URL

**Option 2 — Automatically (the common way):**

Add this comment as the very last line of your minified file:

```js
//# sourceMappingURL=urlOfSourceMap.map
```

If DevTools is open, it sees this comment and automatically loads the map + original files for you. If DevTools is closed, nothing happens — the map is simply never fetched.

## ⚠️ Important Warning

**Never expose source maps in public production apps.** Only use them:

- Behind a login/auth wall, or
- In development only before shipping.

Why? Because a source map can let anyone see your original code.

## How Someone Could Steal Your Code Using a Public Source Map

1. Someone finds your `.map` file (either through the comment, or by guessing the URL).
2. Inside that file (it's just JSON), there's a `sources` field — this lists paths to your original files. There's also often a `sourcesContent` field that contains your **actual original code**, just sitting there in plain text.
3. DevTools reads this and rebuilds your original files right there in the Sources tab.

**Result:** your real, readable source code is now visible to anyone —

## `any` vs `unknown`

### 🔓 `any` — No Safety Net

The `any` type turns off TypeScript's type checking completely. A value can be a `number`, `string`, `object`, `array`, or anything else — and you can call **any method or property** on it, even if it doesn't exist. TypeScript won't warn you.

```ts
const value: any = 5;

value.toUpperCase(); // ❌ No error shown in your IDE...
// but it WILL crash at runtime! 💥
```

> ⚠️ **Danger:** `any` basically tells TypeScript "trust me, don't check this." That defeats the whole purpose of using TypeScript.

---

### 🔒 `unknown` — Safe Alternative

The `unknown` type can also hold any value, **but** you can't use it directly. You must first **narrow down** the type (check what it actually is) before accessing its properties or methods.

```ts
const value: unknown = 5;

// value.toUpperCase(); ❌ Error: Object is of type 'unknown'

// ✅ Narrow it down first, then use it safely:
if (typeof value === "string") {
  console.log(value.toUpperCase());
} else if (typeof value === "number") {
  console.log(value.toFixed(2));
}
```

> ✅ **Safe:** TypeScript forces you to check the type first, preventing runtime crashes.

---

### 🆚 Quick Comparison

| Feature                       | `any`               | `unknown`                 |
| ----------------------------- | ------------------- | ------------------------- |
| Can hold any value            | ✅ Yes              | ✅ Yes                    |
| Type checking                 | ❌ Disabled         | ✅ Enabled                |
| Direct method/property access | ✅ Allowed (unsafe) | ❌ Blocked until narrowed |
| Runtime safety                | ❌ Risky            | ✅ Safe                   |

**💡 Golden Rule:** Prefer `unknown` over `any` whenever possible — it gives you flexibility _without_ sacrificing safety.

## 📦 Arrays in TypeScript

TypeScript lets you define array types in **two ways** — both work the same, just different syntax styles.

---

### 1️⃣ Using Generics — `Array<Type>`

```ts
const lists: Array<number> = []; // ✅ only numbers allowed

// Multiple types allowed using union (|)
const lists: Array<number | string> = []; // ✅ numbers AND strings
```

---

### 2️⃣ Using Shorthand — `Type[]`

```ts
const lists: number[] = []; // ✅ only numbers allowed

// Multiple types allowed using union (|)
const lists: (number | string)[] = []; // ✅ numbers AND strings
```

> ⚠️ **Note:** When mixing types with `[]` shorthand, wrap them in parentheses `()` — otherwise TypeScript misreads the union.

---

### 🆚 Quick Comparison

| Style     | Syntax        | Example         |
| --------- | ------------- | --------------- |
| Generic   | `Array<Type>` | `Array<number>` |
| Shorthand | `Type[]`      | `number[]`      |

**💡 Tip:** Both are functionally identical — pick whichever is more readable for your team. The shorthand (`Type[]`) is more commonly used in everyday code.

## 🎯 Tuples

A tuple is basically an **array with fixed types at fixed positions**. Unlike a regular array (where every item can be the same type freely), a tuple **forces you to declare the exact type for each index** — 1st position must be this type, 2nd position must be that type, and so on.

You can also **name each position** — similar to how you name properties in an `interface` or `type`.

---

### 🔹 Basic Tuple

```ts
const userInfo: [string, number] = ["Prabhu", 18];
// index 0 → must be string
// index 1 → must be number
```

---

### 🔹 Named Tuple

```ts
const coordinate: [x: number, y: number] = [343.334, 232.3];
// Just like naming properties in an interface/type,
// but here it's for tuple positions — improves readability
```

---

### 🆚 Array vs Tuple

| Feature            | Array                   | Tuple                      |
| ------------------ | ----------------------- | -------------------------- |
| Length             | Flexible (any size)     | Fixed (exact size)         |
| Type per index     | ❌ Same type throughout | ✅ Specific type per index |
| Order matters      | ❌ No                   | ✅ Yes                     |
| Can name positions | ❌ No                   | ✅ Yes                     |

> 💡 **Tip:** Use tuples when the **position** of a value carries meaning — like `[x, y]` coordinates, or `[key, value]` pairs. Use arrays when you just have a list of similar items.
