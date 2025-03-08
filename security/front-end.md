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

source:
1. https://ithelp.ithome.com.tw/m/articles/10363951
2. https://ithelp.ithome.com.tw/m/articles/10253715