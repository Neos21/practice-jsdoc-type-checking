# Practice JSDoc Type Checking

JSDoc をちゃんと書けば TypeScript をイチイチインストールしなくても型チェックしてくれるんじゃね？と思い、試行錯誤してみる。


## VSCode 上で JSDoc が正しく書けているかチェック・エラー表示させる手順

1. VSCode 拡張機能の「ESLint」(`dbaeumer.vscode-eslint`) をインストールしておく
2. VSCode のユーザ設定 (`settings.json`) にて以下の設定をしておき ESLint による警告を表示できるようにしておく
  ```json
  {
    "eslint.enable": true,
    "eslint.quiet": false
  }
  ```
3. `$ npm install --save-dev eslint eslint-plugin-jsdoc` でプラグインをインストールする
4. `.eslintrc.js` にて次のように設定しプラグインを有効にする
  ```javascript
  module.exports = {
    env: {
      browser: true,
      node: true,
      es2022: true  // 最低限コレがあれば良さそう
    },
    plugins: [
      'jsdoc'
    ],
    rules: {
      // `eslint-plugin-jsdoc` の各種ルールは `0` = 無効、`1` = 警告 (Warning)、`2` = エラー (Error) で指定する
    }
  };
  ```
5. エディタ上で下線が表示され、「問題」タブに表示されるようになる他、`$ npx eslint ./` で ESLint としても実行可能

**FIXME** : VSCode のユーザ設定 (`settings.json`) で `eslint` 関連の設定をしている時、`.vscode/settings.json` で設定を上書きできない。そういう仕様なのか、自分の環境でのみ発生しているモノなのか不明。


## VSCode 上で型チェックエラーを表示させる手順

1. JS ファイルの1行目に以下のコメントを書く (ファイル個別に有効化・無効化を設定する)
  ```javascript
  // @ts-check
  ```
2. もしくは `jsconfig.json` を作り以下のように書く (プロジェクト全体で有効化・無効化を設定する)
  ```json
    {
    "compilerOptions": {
      "checkJs": true
    }
  }
  ```
3. エディタ上で赤下線が表示される他、「問題」タブに表示されるようになる


## Links

- [Neo's World](https://neos21.net/)
