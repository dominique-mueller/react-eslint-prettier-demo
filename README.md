<div align="center">

# react-eslint-prettier-demo

Demo for a **[React](https://reactjs.org/)** project using **[ESLint](https://eslint.org/)** and **[Prettier](https://prettier.io/)**, using
GitHub actions as CI

</div>

<br><br>

## 1. Setup React application

Using **[Create React App](https://create-react-app.dev)**

``` bash
npx create-react-app react-eslint-prettier-demo --template typescript
```

> Due to an incompatibility issue, this demo uses a downgraded version of TypeScript (`4.0.x` instead of `4.1.x`), which also requires the
> `compilerOptions.jsx` value to be changed from `react-jsx` to `react`.

<br><br><br>

## 2. Setup ESLint w/ TypeScript support

Using **[ESLint](https://eslint.org/docs/user-guide/getting-started)**,
**[TypeScript ESLint](https://github.com/typescript-eslint/typescript-eslint/blob/master/docs/getting-started/linting/README.md )**

<br>

### Install dependencies

`package.json`

``` diff
  {
    "devDependencies": {
+     "eslint": "x.x.x",
+     "@typescript-eslint/parser": "x.x.x",
+     "@typescript-eslint/eslint-plugin": "x.x.x"
    }
  }
```

``` bash
npm install
```

<br>

### Configure ESLint

`.eslintrc`

``` diff
+ {
+   "extends": [
+     "eslint:recommended",
+     "plugin:@typescript-eslint/eslint-recommended",
+     "plugin:@typescript-eslint/recommended"
+    ],
+   "parser": "@typescript-eslint/parser",
+   "parserOptions": {
+     "ecmaVersion": 2018,
+     "sourceType": "module",
+     "ecmaFeatures": {
+       "jsx": true
+     }
+   },
+   "plugins": [
+     "@typescript-eslint"
+   ]
+ }
```

<br>

### Setup scripts

`package.json`

``` diff
  {
    "scripts": {
+     "lint": "eslint src/**/*.{ts,tsx} --max-warnings 0",
+     "lint:fix": "eslint src/**/*.{ts,tsx} --max-warnings 0 --fix"
    }
  }
```

<br>

### Bonus: Remove ESLint from build steps

`package.json`

``` diff
  {
    "devDependencies": {
+     "cross-env": "x.x.x"
    }
  }
```

```
npm install
```

`package.json`

``` diff
  {
    "scripts": {
-     "start": "react-scripts start",
+     "start": "cross-env DISABLE_ESLINT_PLUGIN=true react-scripts start",
-     "build": "react-scripts build",
+     "build": "cross-env DISABLE_ESLINT_PLUGIN=true react-scripts build",
    }
  }
```

<br><br><br>

## 3. Add ESLint React support

Using **[eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)**,
**[eslint-plugin-react-hooks](https://github.com/facebook/react/tree/master/packages/eslint-plugin-react-hooks)**

<br>

## Install dependencies

`package.json`

``` diff
  {
    "devDependencies": {
+     "eslint-plugin-react": "x.x.x",
+     "eslint-plugin-react-hooks": "x.x.x",
    }
  }
```

```
npm install
```

<br>

## Configure ESLint

`.eslintrc`

``` diff
  {
    "extends": [
+     "react-app",
+     "plugin:react/recommended",
+     "plugin:react-hooks/recommended"
    ],

    "plugins": [
+     "react",
+     "react-hooks"
    ],

+   "settings": {
+     "react": {
+       "version": "detect"
+     }
+   },
  }
```

<br><br><br>

## 4. Setup Prettier w/ ESLint integration

Using, **[Prettier](https://prettier.io/)**, **[eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)**,
**[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)**

<br>

### Install dependencies

`package.json`

``` diff
  {
    "devDependencies": {
+     "eslint-config-prettier": "x.x.x",
+     "eslint-plugin-prettier": "x.x.x",
+     "prettier": "x.x.x",
    }
  }
```

```
npm install
```

<br>

### Configure Prettier

`.prettierrc`

``` diff
+ {
+   "endOfLine": "auto",
+   "jsxBracketSameLine": false,
+   "printWidth": 140,
+   "singleQuote": true,
+   "trailingComma": "all"
+ }
```

<br>

## Configure ESLint

`.eslintrc`

``` diff
  {
    "extends": [
+     "prettier/@typescript-eslint",
+     "plugin:prettier/recommended",
+     "prettier/react"
    ],

    "plugins": [
+     "prettier"
    ]
  }
```

<br><br><br>

## Visual Studio Code integration

<br>

### Extensions

- ESLint<br />https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint
- Prettier<br />https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

<br>

### Autofix on save

`settings.json`

``` diff
+ "editor.codeActionsOnSave": {
+   "source.fixAll.eslint": true
+ }
```
