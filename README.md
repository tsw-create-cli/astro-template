# 项目配置

## 配置eslint和prettier

### eslint

https://github.com/ota-meshi/eslint-plugin-astro

安装

```shell
npm install --save-dev eslint eslint-plugin-astro
```

配置文件

```shell
npm init @eslint/config
```

然后添加

```js
module.exports = {
  extends: [
    // ...
    "plugin:astro/recommended",
  ],
  overrides: [
    {
      // Define the configuration for `.astro` file.
      files: ["*.astro"],
      // Allows Astro components to be parsed.
      parser: "astro-eslint-parser",
      // Parse the script in `.astro` as TypeScript by adding the following configuration.
      // It's the setting you need when using TypeScript.
      parserOptions: {
        parser: "@typescript-eslint/parser",
        extraFileExtensions: [".astro"],
      },
      rules: {
        // override/add rules settings here, such as:
        // "astro/no-set-html-directive": "error"
      },
    },
    // ...
  ],
};
```

### prettier

https://github.com/withastro/prettier-plugin-astro

安装

```shell
npm i --save-dev prettier prettier-plugin-astro
```

配置文件

创建`.prettierrc.mjs`

```js
/** @type {import("prettier").Config} */
export default {
  plugins: ["prettier-plugin-astro"],
  overrides: [
    {
      files: "*.astro",
      options: {
        parser: "astro",
      },
    },
  ],
};
```

## 配置husky和line-staged

### 预准备

```shell
git init
```

### 配置husky

初始化husky

```shell
npx husky-init
```

安装husky

```shell
npm i
```

### 集成lint-staged

```shell
npm install --save-dev lint-staged
```

配置（`package.json`）

```json
"lint-staged": {
    "*.{js,ts,astro,vue,jsx,tsx,mjs,cjs}": [
      "eslint",
      "prettier --write"
    ],
    "*.{html,css,md,mdx,json}": "npx prettier --write"
  },
```

添加命令（.husky/pre-commit）

```
npx lint-staged
```

### 集成commitlint

```shell
npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
```

安装

```shell
npm install --save-dev @commitlint/cli
```

配置（`package.json`）

```json
"commitlint": {
  "extends": [
    "@commitlint/config-conventional"
  ]
}
```
