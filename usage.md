# 安装

```
# 通过cnpm安装
cnpm install eslint-vue-js-fixer

# 通过yarn安装 (推荐)
yarn add git+https://github.com/virtoolswebplayer/eslint-vue-js-fixer.git
```

# 用法

```
Usage: vuefix [options]

Options:
  -d, --dir     源目录                      [string] [required] [default: "src"]
  -e, --exlude  排除                                     [array] [default: [""]]
  -b, --babel   <script lang="babel" type="text/babel">         [default: false]
  -s, --style   <style lang="less" rel="stylesheet/less">
                                                       [string] [default: false]
  -h, --help    Show help                                              [boolean]

Examples:
  vuefix -d src                    修复src目录下的所有 .vue 和 .js文件
  vuefix -d src -e a.js b.js c.js  修复所有除了 a.js b.js c.js
  vuefix -d src -s less            修复所有, style lang=less
  vuefix -d src -s sass            修复所有, style lang=sass
  vuefix -d src -b                 修复所有, script lang=babel

```

# 在vue项目中配置

### 安装依赖包

```
yarn add eslint-plugin-vue eslint-config-elemefe -D
```

### 配置package.json

```
// 添加新命令
...
"scripts": {
    ...
    "lint:fix": "vuefix -s src"
  },
...
```

### 配置eslintrc.js

```
// eslintrc.js  eslint规则配置文件

module.exports = {
  root: true,
  parser: 'babel-eslint',
  parserOptions: {
    sourceType: 'module'
  },
  extends: 'eslint-config-elemefe',
  // required to lint *.vue files
  plugins: [
    'vue'
  ],
  'globals': {
    'Promise': true   // Promise 允许 Promise
  },
  // check if imports actually resolve
  'settings': {
    'import/resolver': {
      'webpack': {
        'config': 'build/webpack.base.conf.js'
      }
    }
  },
  // add your custom rules here
  'rules': {
    // don't require .vue extension when importing
    // 'import/extensions': ['error', 'never', {
    //   'js': 'never',
    //   'vue': 'never'
    // }],
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 2 : 0,
    'semi': ['error', 'never'], // 必须使用 ';' 号结尾
    'one-var': ['error', 'never'],
    'comma-dangle': ['error', { // 结尾逗号 ','
      'arrays': 'only-multiline',
      'objects': 'only-multiline', //多行结尾 必须加 ','
      'imports': 'never',
      'exports': 'never',
      'functions': 'never',
    }]
  }
}
```

### 在项目中运行修复命令

```
npm run lint:fix
```

