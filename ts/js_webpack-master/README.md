## JS webpack BruceFE
- 初始空專案
- 此專案將js專案轉成ts+webpack
- 報錯Error: error:0308010C:digital envelope routines::unsupported
升級相關依賴:
有些依賴（如 Webpack 等）已經針對 OpenSSL 3.0 進行了更新，檢查是否有新版並進行升級
npm update
-裝ts loader
npm install --save-dev typescript ts-loader
- js專案變更成ts
1. 新增tsconfig.json
2. src底下新增index.ts
3. tsconfig.json依照官網範例配置
4. webpack.config.js底下的entry: './src/index.js', 改成".ts"
5. src index.js改成index.ts
6. babel-loader改成ts-loader
7. webpack只會解析js檔案，加上resolve配置，讓webpack解析ts
官方文檔:
https://webpack.js.org/guides/typescript/