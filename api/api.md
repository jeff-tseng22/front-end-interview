在開發中，選擇合適的迴圈方法來處理非同步 API 請求至關重要，以下幫大家整理了幾種常見的方法及其特性：
​
1. forEach：
同步執行，無法等待非同步操作完成，可能導致程式碼提前執行。
2. map + Promise.all：
可以等待所有請求完成，但無法控制請求執行的順序。
3. for...of：
可以按順序執行每個請求，確保每次迭代都等待前一次完成，非常適合需要順序處理的情境。
4. reduce：
也能實現按順序執行，適合將多個請求合併成單一結果。

https://muki.tw/foreach-map-for-of/?fbclid=IwY2xjawI1Ti1leHRuA2FlbQIxMAABHfwgDiNNdULJmaX85FEpG5SFDyt5WgoQunn9EjnpIVFCz_t33MwYnyKG9w_aem_5uW2KKpNO6bx41mVUEjFPQ