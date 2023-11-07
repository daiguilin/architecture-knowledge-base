它的作用是仅对变更的文件执行相关操作，就是执行eslint检查这项操作，同时还能忽略我们所要忽略的文件。

1. 安装lint-staged

   ```javascript
   npm i lint-staged -D
   ```

2. 项目根目录创建.lintstagedrc.js文件

   ```javascript
   const { ESLint } = require ('eslint');
   const removeIgnoredFiles = async (files) => {
   const eslint =new ESLint（）;
   const ignoredFiles = await Promise.all (files.map ((file) => eslint.isPathIgnored(file)));
   const filteredriles = 1iles.filter((_,i)=> Iignoredriles[i]):
   return filteredFiles.join(' ');
   module.exports = {
   '*': async (files)=>{
     const filesTolint = await removeignoredFiles (files);
   return [`eslint ${filesToLint} --max-warnings=0`];
   }
   }
   ```

   我们在这里使用了js文件格式,是因为我们需要在配置文件中编写代码