1. 減少 HTTP 請求數量
合併文件：將多個 CSS 或 JavaScript 文件合併為一個文件。
CSS Sprite：將多張小圖片合併為一張大圖片，使用 background-position 顯示所需部分。
使用 Base64 編碼：對小圖標（如 10KB 以下的圖片）進行 Base64 編碼，嵌入到 CSS 或 HTML 中，減少請求數。

2. 資源壓縮
Gzip/Brotli 壓縮：配置伺服器（如 Nginx、Apache）啟用 Gzip 或 Brotli 壓縮，縮小文件大小。
壓縮圖片：使用工具（如 TinyPNG 或 Squoosh）壓縮圖片，選擇合適的格式（如 WebP）。
移除不必要的空格與注釋：對 HTML、CSS 和 JS 文件進行壓縮（Minification），移除空格、換行和注釋。
工具：UglifyJS、Terser、cssnano。

3. 縮短首屏渲染時間
優化關鍵渲染路徑：將 CSS、JavaScript、圖片等資源盡量減少並優化加載順序。
CSS 放頭部（Head）：避免影響頁面渲染。
JavaScript 放底部（Body 末尾）：避免阻塞 DOM 解析。
Critical CSS：提取關鍵 CSS，將其內聯到 HTML 中，縮短渲染時間。
延遲加載非關鍵資源：使用 async 或 defer 屬性延遲加載 JS 文件。

4. 使用瀏覽器快取
設置緩存頭（Cache-Control）：配置靜態資源的緩存時間，例如：
=>
Cache-Control: max-age=31536000
使用版本號（Cache Busting）：在文件名中添加哈希值（如 style.a1b2c3.css），方便文件更新後自動刷新緩存。

5. 圖片優化
選擇合適的圖片格式：
WebP：比 PNG 和 JPEG 更小，支持壓縮且質量高。
SVG：適合圖標和簡單圖形，支持無損縮放。
Lazy Loading：
對圖片使用懶加載技術，僅當圖片進入可視範圍時才加載。
使用 <img loading="lazy" /> 或 Intersection Observer 實現。
使用響應式圖片：使用 <picture> 元素根據屏幕大小加載不同分辨率的圖片：
<picture>
    <source srcset="image-large.jpg" media="(min-width: 800px)">
    <source srcset="image-small.jpg" media="(max-width: 799px)">
    <img src="image-default.jpg" alt="描述">
</picture>

6. 代碼拆分與按需加載
代碼分割（Code Splitting）：
將應用的代碼拆分成多個小模塊，按需加載，減少首屏的代碼體積。
使用工具如 Webpack 的 splitChunks。
動態加載（Dynamic Import）：
使用 ES6 的 import() 語法按需加載模塊：
=>
import('./module.js').then(module => {
    module.default();
});

