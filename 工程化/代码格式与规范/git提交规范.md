### husky

1. 项目中安装husky 

   ```javascript
   npm i husky -D
   ```

2. 通过npx执行husky install命令启用git hook

   ```javascript
   npx husky install
   ```

   注意：在根目录生成一个.husky目录

3. Package.json中的script的命令中增加一条命令，使得当其他人克隆该项目并安装依赖时，会自动通过husky启用git hook

   ```javascript
   scripts:{
     prepare:"husky install"
   }
   ```

4. 代码提交前对代码进行质量与格式检查,执行如下命令

   ```javascript
   npx husky add .husky/pre-commit "npm run lint“
   ```

   注意：.husky 文件夹下已经有了pre-commit 这个git hook

5. commit代码之前会执行`npm run lint`当不符合eslint规则时，会报错，执行`npm  run format`对代码格式化之后，在从新提交就不会报错了
