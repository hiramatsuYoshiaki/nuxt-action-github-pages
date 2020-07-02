# nuxt-univ-github-action

develop-github\nuxt-github-action\nuxt-univ-github-action

### アプリケーションの概要

1.Github Action により自動で GitHub Pages へデプロイする。

### nuxt-univ-starter(clone)

develop-github\nuxt(node12.18.0)\nuxt-start  
node:v12.18.0  
npm v6.14.4

### アプリケーションの初期設定

スターターテンプレート nuxt.config.js setting  
1.pug  
2.sass  
3.sass 変数  
4.autoprefixer  
5.eslintrc.js console.log  
6.eslint error

css setting  
1.styles.scss(import)  
2.style-guode.scss(sass 変数)  
3.foundation  
4.layout  
5.component  
6.project  
7.utilitty

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

## nuxt install setting

```
create-nuxt-app v2.15.0
✨  Generating Nuxt.js project in nuxt-univ-starter
? Project name nuxt-univ-starter
? Project description My stylish Nuxt.js project
? Author name hiramatsu
? Choose programming language JavaScript
? Choose the package manager Npm
? Choose UI framework None
? Choose custom server framework None (Recommended)
? Choose Nuxt.js modules Axios
? Choose linting tools ESLint, Prettier
? Choose test framework None
? Choose rendering mode Universal (SSR)
? Choose development tools jsconfig.json (Recommended for VS Code)

```

# nuxt.config.js setting

> nuxt.config.js での導入時の設定

## 1.pug

https://qiita.com/amishiro/items/38fe1b102d7e91a93ada

```
// pug
$ npm i pug pug-loader pug-plain-loader

```

## 2.css プロパティ

sass を利用したい場合は node-sass および sass-loader パッケージをインストールしてください。

1. install

```
npm install --save-dev node-sass sass-loader
```

2. nuxt.config 　 setting

```
export default {
  css: [
    // プロジェクト内の SCSS ファイル
    '@/assets/sass/styles.scss'
  ]
}
```

3. component style setting

```
    <style scoped lang="scss">
    </style>
```

## 3.SASS 変数を vue ファイルで使う

import の記述なしで使う。

1. install

```
npm install --save @nuxtjs/style-resources
```

`注意`
--save-dev にすると google app engine へデプロイ時に not found でエラーになる。package.json の devDependencies ではエラー

2. nuxt.config setting

```
modules: [
    '@nuxtjs/style-resources',
  ],
styleResources: {
  scss: [
    '@/assets/sass/style-guide.scss',
  ],
},
```

3. usage

```
<style scoped lang="scss">
//@import "../../../assets/scss/common/data/thema.scss";
.container {
    color: $text-color
}
</style>
```

## 4.autoprefixer の設定をカスタマイズする

Nuxt.js で CSS(Sass) をコンパイルすると、 autoprefixer がベンダープレフィクスを自動で適用してくれます。

1. nuxt.config setting

```
build: {
  postcss: [
    require('autoprefixer')({
      browsers: ['IE 11', 'last 2 versions' ],
      grid: true
    })
  ]
}

```

2. autoprefixer デフォルト設定

```
1%, last 2 versions, Firefox ESR
```

1%:1%以上のシェアがあるブラウザ
last 2 versions:最後の 2 バージョンのブラウザ
Firefox ESR:最新の Firefox ESR 版  
3.対応ブラウザの確認
https://browserl.ist/?q=%3E+1%25%2C+last+2+versions%2C+Firefox+ESR

参考ページ:https://parashuto.com/rriver/tools/using-custom-data-for-autoprefixer

## 5.eslintrc.js

## console.log の使用

`eslintrc.js`

```
    rules: {
        'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
        'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
    }
```

## 6.eslint

フォーマットエラー対応
✖ 7 problems (7 errors, 0 warnings)
7 errors, 0 warnings potentially fixable with the `--fix` option.

Solved adding fix option in nuxt.config.jsfile:

```
extend(config, ctx) {
    if (ctx.dev && ctx.isClient) {
        config.module.rules.push({
            enforce : 'pre',
            test    : /\.(js|vue)$/,
            loader  : 'eslint-loader',
            exclude : /(node_modules)/,
            options : {
                fix : true
            }
        });
    }
}
```

ex.https://github.com/nuxt/nuxt.js/issues/1628

```
options: {
fix: true
       }
```

```
<template >
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxt-univ-starter
      </h1>
      <h2 class="subtitle">
        My stylish Nuxt.js project
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

```

# GitHub

## GitHub リポジトリの作成

1. GitHub ログイン後のトップページから、Repositories の New ボタンをクリックします。
2. Create a new repository の画面に遷移するので、リポジトリ名、ライセンス等を入力。Initialize this repository with a README はチェックせず画面下のほうにある Create repository ボタンをクリックします。

## プロジェクトを GitHub に Push する

1. git add -A
2. git commit -m "first commit"
3. git remote add origin https://github.com/hiramatsuYoshiaki/プロジェクト名
4. git push -u origin master

## 現在のブランチから派生ブランチを作成して GitHub へ Push する。

1. git branch new-branch
2. git checkout new-branch
3. git branch
   - new-branch
     master
4. git add -A
5. git commit -m 'new branch commit'
6. git push --set-upstream origin new-branch
   (もしくは、　 git push -u origin new-branch)

## GitHub リポジトリを clone してローカルプロジェクト作る

1. リモートリポジトリを clone する。

```
    git clone https://github.com/hiramatsuYoshiaki/nuxt-univ-create-gae-hosting.git
```

2. インストールする

```
    npm install
```

3. サーバーを立ち上げて確認

```
   npm run dev
```

4. ローカルサーバーへアクセス

```
   http://localhost:3000/で確認する。
```

## ローカルプロジェクトを GitHub へ push する。

```
1. 現在のブランチを確認する。
   git branch
   * master
```

2. master から新しい branch を作る

```
　　git branch new-branch
```

3. 新しい branch に移動し開発を行う。

```
   git checkout new-branch
```

4. clone したリポジトリから別のリモートリポジトリの URL を変更する場合

```
    git remote -v
    origin  https://github.com/hiramatsuYoshiaki/vue-cli3-unit.git (fetch)
    origin  https://github.com/hiramatsuYoshiaki/vue-cli3-unit.git (push)
    git remote rm originで現在のリモートリポジトリを削除する
    git remote add originで新しいリモートリポジトリを追加する
    git remote add origin https://github.com/hiramatsuYoshiaki/vue-cli3-unit-alprime.git
```

5. コミットして GitHub に push する

```
   git add　-A
   git commit -m "コメント"
   git push -u origin new-branch
```
