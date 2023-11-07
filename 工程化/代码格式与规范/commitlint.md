对于我们的commit信息，也是有统一规范的，不能随便写，要让每个人都按照统一的标准来执行，我们可以利用commitlint来实现。

1. 安装包

```sh
pnpm add @commitlint/config-conventional @commitlint/cli -D
```

2. 添加配置文件，新建 commitlint.config.cjs （注意是cjs），然后添加下面的代码：

```javascript
module. exports = {
  extends: ['@commitlint/config-conventional'],
  // 校验规则
  rules: {
    "type-enum': [
      2，
      'always',
      ［
      'feat',
      'fix',
      "docs',
      'style',
      'refactor',
      'perf',
      'test',
      "chore',
      'revert',
      'build',
      ］，
    'type-case': [0],
    'type-empty': [0],
    'scope-empty': [0],
    'scope-case': [0],
    'subject-full-stop': [0, 'never'],
    'subject-case': [0, 'never'],
    'header-max-length':[0,'always',72],
  }
}
```

3. 在package.json 中配置scripts命令

```javascript
# 在scrips中添加下面的代码
{
  "scripts": {
  	"commitlint": "commitlint --config commitlint.config.cjs -e -V"
  ｝
}
```

4. 配置结束，现在当我们填写commit 信息的时候，前面就需要带着下面的 subject

```javascript
'feat',//新特性、新功能
'fix',//修改bug
'docs',//文档修改
'style',//代码格式修改，注意不是 css 修改
'refactor',//代码重构
'perf',//优化相关，比如提升性能，体验
'test',//测试用例修改
'chore',//其他修改，比如改变构建流程，或者增加依赖库，工具等
'revert',//回滚到上一个版本
'build',//编译相关的修改，例如发布版本、对项目构建或者依赖的改动
```

5. 配置husky

```javascript
npx husky add .husky/commit-msg
```

在生成的commit-msg文件中添加下面的命令

```javascript
#!/usr/bin/env sh
 "$(dirname -- "$0")/_/husky.sh"

pnpm commitlint
```

当我们commit提交信息时，就不能再随意写了，必须是 git commit-m fix:xxx符合类型的才可以，需要注意的是类型的后面需要用英文的：，并且冒号后面是需要空一格的，这个是不能省略的