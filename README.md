# LEARN TO USE ESLINT AND PRETTIER
This project is use to learn eslint and prettier in javascript projects

All steps will be listed here to rework later

### Step 1: Init the project by using vitejs to create
> yarn create vite example1 -- --template vanilla-ts

### Step 2: Add eslint
> yarn create @eslint/config
Select: 
- No framework
- Use typescript
- Run on browser

Add it will install eslint@9.x, globals, @eslint/js, typescript-eslint

A eslint.config.js file is added with below content:
```
import globals from "globals";
import pluginJs from "@eslint/js";
import tseslint from "typescript-eslint";


export default [
  {files: ["**/*.{js,mjs,cjs,ts}"]},
  {languageOptions: { globals: globals.browser }},
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
];
```

### Step 3: Update eslint config file, run lint and check the result
- Add a rule for console.log to eslint.config.js
```
{
  rules: { 'no-console': 'warn' }
}
```
- Add a script to run lint to package.json `"lint": "eslint"`
- Add console.log to a ts file
- Run `yarn lint`
- Result
![alt text](./readme-files/eslint-console.png)

### Step 4: Add prettier to format code
- Install required package: prettier
- Add `prettier.config.js` and fill some simple rule:
```
export default {
  arrowParens: 'avoid',
  printWidth: 120,
  semi: false,
  singleQuote: true,
  trailingComma: 'es5',
  tabWidth: 2,
}
```
- Add script to run prettier: `"format": "prettier --write \"**/*.{js,ts}\""`
- Run `yarn format` to format all js and ts files in the project

### Step 5: Combine eslint and prettier together
This will help eslint to use prettier rules while linting \
It will be helpful when using eslint extension that does highlight for unformatted text

We will:
- Install some packages: `yarn add -D eslint-config-prettier eslint-plugin-prettier`
- Use plugins in eslint config\
By default, all unformatted code will be `error` when running lint.
And we can change it to `warning` for some rules by add `prettier/prettier` rule
> import prettierRecommended from 'eslint-plugin-prettier/recommended'
```
export default [
  ...
  js.configs.recommended,
  prettierRecommended,
  {
    rules: {
      ...
      'prettier/prettier': [
        'warn',
        {
          semi: false,
          singleQuote: true,
        }
      ]
    }
  }
]
```
- Should use `eslint-config-prettier` to disable all formatting-related ESLint rules that may conflict with prettier rules
- Should put `eslint-config-prettier` after other plugins to override
> import eslintConfigPrettier from 'eslint-config-prettier'
```
export default [
  ...
  pluginJs.configs.recommended,
  prettierRecommended,
  eslintConfigPrettier,
  {
    rules: {
      ...
    }
  },
]
```