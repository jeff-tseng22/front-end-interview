## JS webpack BruceFE
- 初始空專案
- 此專案將js專案轉成ts+webpack
- 報錯Error: error:0308010C:digital envelope routines::unsupported
升級相關依賴:
有些依賴（如 Webpack 等）已經針對 OpenSSL 3.0 進行了更新，檢查是否有新版並進行升級
npm update
-裝ts loader
npm install --save-dev typescript ts-loader