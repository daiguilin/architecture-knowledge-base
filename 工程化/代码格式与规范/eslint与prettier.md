### Eslint

1. 项目中安装eslint

```javascript
npm i eslint  @typescript-eslint/eslint-plugin @typescript-eslint/parser -D
```

2. 创建配置文件.eslintrc，.eslintignore

   .eslintrc

```javascript
{
  // 该配置项主要用于指示此.eslintrc文件是Eslint在项目内使用的根级别文件，并且 ESLint 不应在该目录之外搜索配置文件
  "root": true,
  // 默认情况下，Eslint使用其内置的 Espree 解析器，该解析器与标准 Javaseript运行时和版本兼容，而我们需要将ts
  // 代码解析为eslint兼容的AST，所以此处我们使用 @typescript-eslint/parser
  "parser": "@typescript-eslint/parser",
  // 该配置项告诉eslint我们拓展了哪些指定的配置集，其中
  // eslint:recommended：该配置集是 ESiint 内置的“推荐”，它打开一组小的、合理的规则，用于检查众所周知的最佳实践
  // @typescript-eslint/recommended：该配置集是typescript-eslint的推荐，它与eslint:recommended相似，但它启用了特定于ts的规则
  // @typescript-eslint/eslint-recommended：该配置集禁用 eslint:recommended 配置集中已经由typeSeript 处理的规则，防止eslint和typescript之间的冲突。
  // 这样它有机会覆盖其他配置
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/eslint-recommended",
  ],
  // 该配置项指示要加载的插件，这里
  // @typescript-eslint 插件使得我们能够在我们的存储库中使開typescript-eslint包定义的规则集。
  "plugins": ["@typescript-eslint" ],
}

```

.eslintignore

```javascript
node_modules/
package-lock.json
```

3.在package.json中配置命令

```javascript
"lint": "eslint ./ --ext .ts,.tsx,.js --max-warnings=0"
```

4.提交代码之前对代码进行eslint检测

```javascript
npm run lint
```

注意：此方式使用需要执行eslint命令才能对文件进行检测，控制台输出错误，比较麻烦，可以安装对应的vscode插件，读取配置文件，对代码错误进行及时提示,不再需要执行命令检查代码错误

### 为什么有eslint，还要还用用prettier？

eslint只是对代码质量和少量的代码格式进行检查，所以需要用prettier插件对代码进行格式化，但是二者规则也会有冲突，后面我们会进行解决

### prettier

1. 安装prettier

```
npm i prettier -D
```

2. 创建.prettierrc,  .prettierignore

   .prettierrc

   ```javascript
   {
     "semi": true,
     "singleQuote": true,
     "tabWidth": 2,
     "printWidth": 120
   }
   ```

   .prettierignore

   ```javascript
   node_modules/
   package-lock.json
   ```

3. 在package.json中配置命令

   ```javascript
    "format": "prettier --config .prettierrc '.' --write"
   ```

4. 每次编写完代码执行命令进行代码格式化

   ```javascript
   npm run format
   ```

注意：此处也可以在vscode中安装prettier插件，读取项目中的配置文件，对代码进行实时监测，保存的时候进行格式化

### Vscode

要想启用prettier进行保存格式化，需要settings.json中设置如下命令

```json
"editor.formatOnSave": true,//保存格式化代码
"editor.defaultFormatter": "esbenp.prettier-vscode",//把prettier设置成默认的代码格式化工具
"[javascript]": { //自定义不同的语言，使用prettier作为默认的格式化工具， 
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

### eslint与prettier规则冲突解决

1. 项目中安装解决冲突的插件

   ```javascript
   npm i eslint-config-prettier eslint-plugin-prettier -D
   ```

2. 配置.eslintrc

   ```javascript
   {
     "root": true,
     "parser": "@typescript-eslint/parser",
     // prettier（eslint-config-prettier）关闭所有可能干扰Prettier 规则的 ESLint 规则，确保将其放在最后
     // 这样它有机会覆盖其他配置
     "extends": [
       "eslint:recommended",
       "plugin:@typescript-eslint/recommended",
       "plugin:@typescript-eslint/eslint-recommended",
       "prettier"
     ],
     // prettier插件（即eslint-plugin-prettier） 将 Prettier 规则转换为 ESLint 规则
     "plugins": ["@typescript-eslint", "prettier"],
     "rules": {
       "prettier/prettier": "error", // 打开prettier插件提供的规则，该插件从 ESLint 内运行 Prettier
       //关闭这两个 ESLint 核心规则，这两个规则和prettier插件一起使用会出现问题，具体可参阅
       //https://github.com/prettier/eslint-plugin-prettier/blob/master/README.
       //md#arrow-body-style-and-prefer-arrow-callback-issue
       "arrow-body-style": "off",
       "prefer-arrow-callback": "off"
     }
   }
   ```

   
