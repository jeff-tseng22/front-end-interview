## 前端安全性-防範常見的安全威脅
1. 跨站腳本攻擊(XSS):
是最常見的前端安全威脅之一。攻擊者藉由在網頁中注入惡意腳本，使得當使用者訪問其頁面時，這些腳本會在使用者的瀏覽器中執行，進而竊取使用者的敏感資訊（如登入憑證）或操縱頁面行為。
防範措施:
輸入驗證與輸出編碼
對使用者輸入的資料進行嚴格驗證和清理，防止攻擊者透過輸入惡意腳本。對動態內容進行 HTML 編碼，確保特殊字符（如 < 和 >）不會被誤解為 HTML 標籤或 JavaScript 代碼。
使用 Content Security Policy（CSP）
CSP 是一種安全機制，能夠限制網頁上可以執行的內容類型。通過配置 CSP，開發者可以禁止在網頁中執行未授權的腳本，進一步防止 XSS 攻擊。
避免直接插入使用者輸入到 DOM
如果必須插入使用者輸入到頁面，使用安全的 DOM 操作方法（如 textContent 或 innerText） 而不是直接插入 HTML 片段。

2. 跨站請求偽造（CSRF）:
跨站請求偽造（CSRF，Cross-Site Request Forgery） 是一種透過誘騙使用者執行未授權操作的攻擊方式。攻擊者會建立惡意連結或表單，一旦使用者點擊或提交，這些請求將以使用者的身份發送到受信任的網站，導致使用者帳戶被盜或被篡改。
使用 CSRF 令牌
防範措施:
CSRF 防禦的最佳方法之一是使用 CSRF 令牌。服務器可以生成一個唯一的 CSRF 令牌並將其嵌入到表單或請求中，只有持有正確令牌的請求才能被服務器接受。服務器在接收請求時會驗證該令牌，確保請求是從合法來源發出的，而不是透過偽造的連結發送的。
設置 SameSite Cookie 屬性
SameSite Cookie 是一種瀏覽器機制，透過限制跨站點 Cookie 的發送行為，可以減少 CSRF 攻擊的發生。將 Cookie 的 SameSite 屬性設置為 Strict 或 Lax，可以確保 Cookie 只能在同站點的請求中發送，可以防止 Cookie 在跨站請求中被自動發送，從而有效阻止 CSRF 攻擊。
驗證請求來源
檢查請求的 Referer 或 Origin 標頭內容，確保請求來源是合法的。如果請求來源與預期不符，可以拒絕處理請求。

3. 點擊劫持（Clickjacking）:
點擊劫持（Clickjacking） 是一種使用 iframe 覆蓋使用者介面的攻擊。攻擊者誘使用者點擊一個看似無害的按鈕或連結，但實際上使用者點擊的是隱藏的惡意元素，導致使用者無意間執行了攻擊者設計的操作。
防範措施:
**使用 X-Frame-Options HTTP Header **
設置 X-Frame-Options 為 DENY 或 SAMEORIGIN，可以防止網頁被嵌入到 iframe 中，從而避免點擊劫持攻擊。
配置 Content Security Policy（CSP）中的 frame-ancestors
CSP 中的 frame-ancestors 指令可以指定網頁允許被哪些來源嵌入。透過限制 frame-ancestors 的來源，可以防止頁面被惡意嵌入。

source:
1. https://ithelp.ithome.com.tw/m/articles/10363951
2. https://ithelp.ithome.com.tw/m/articles/10253715