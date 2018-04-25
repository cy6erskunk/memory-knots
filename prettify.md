- `npm i -D eslint prettier eslint-config-prettier eslint-plugin-prettier eslint-plugin-import babel-eslint babel-preset-env @jetbrains/eslint-config`
- create `.eslintrc`:
```
{
  "root": true,
  "parser": "babel-eslint",
  "extends": [
    "@jetbrains",
    "@jetbrains/eslint-config/node",
    "@jetbrains/eslint-config/es6",
    "prettier"
  ],
  "plugins": [
    "prettier"
  ],
  "rules": {
    "import/no-commonjs": "off",
    "prettier/prettier": [
      "error",
      {
        "printWidth": 100,
        "semi": false,
        "singleQuote": true,
        "trailingComma": "all",
        "bracketSpacing": false
      }
    ],
    "import/no-extraneous-dependencies": [
      "error",
      {
        "devDependencies": true,
        "optionalDependencies": false,
        "peerDependencies": false
      }
    ]
  }
}
```
- add `.eslintignore`, e.g.:
```
.idea
node_modules
dist
```
- add `lint` script to the `package.json`: `"lint": "eslint ."`
