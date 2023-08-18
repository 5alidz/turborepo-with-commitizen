### installing husky and lint staged

```sh
yarn add -D -W husky lint-staged
```

### ensure that husky in not installed in CI environments

in your package.json

```json
{
  "scripts": {
    "prepare": "node -e \"try { !(process.env.CI !== undefined) && require('husky').install() } catch (e) {if (e.code !== 'MODULE_NOT_FOUND') throw e}\""
  }
}
```

### now run husky prepare

```sh
yarn prepare
```

### add lint-staged config

```json
{
  "lint-staged": {
    "apps/**/*.{js,ts,jsx,tsx}": ["./node_modules/eslint/bin/eslint.js --fix"],
    "packages/ui/**/*.{js,ts,jsx,tsx}": [
      "./node_modules/eslint/bin/eslint.js --fix"
    ],
    "*.json": ["prettier --write"]
  }
}
```

### create the hooks

```sh
npx husky add .husky/pre-commit "npm run test && npx lint-staged"
```
