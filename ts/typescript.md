## 什麼是TypeScript
1. 加強版JavaScript(JS是動態型語言)
2. 加強了"type"部分
3. 開發完後，還是需要編譯成JavaScript
4. 適用於開發前端與後端，例如：搭配React、Express框架
## 為什麼需要TypeScript
1. 開發時"type"類型檢查
2. 補強動態語言JS，run起來才出錯的缺點
3. 提高專案程式碼的維護性
## TypeScript優缺點比較
優點
1. 減少程式碼運行時bug
2. 提高專案的穩定性
3. 看懂一些function參數等等
缺點
1. 不是真正的類型檢查
2. 需要編譯，CI/CD部署速度慢
3. 花更多時間開發和學習
## 一定需要TypeScript嗎
1. 時間成本考量
2. 專案適合不適合
3. Trade-off(考慮cp值)
## 編譯流程
### 開發時: TS
檔案.ts
檔案.tsx
tsconfig.json
### 編譯工具: tsc
### 最後的產物: JS
前端: 給html引用
後端: 部署到node.js環境
## 安裝TS(資料夾或全局)
npm install typescript --save-dev
npm install typescript -g 
查看指令:
tsc -help
編譯ts:
tsc index.ts
創建config檔案(typescript.json):
tsc --init
"rootDir": "./src", 
"outDir": "./dist",   
"allowJs": true, 
"sourceMap": true, //chrome dev tools可直接debug。console旁邊顯示ts檔案
"module": "commonjs", 
"target": "es2016", 
"strict": true,   


## type any vs. unknown 的差別
any 和 unknown 都是表示「任意型別」的關鍵字，主要在於安全性與使用限制。
1. any
=> let value: any;

特性：
允許任意型別的值。
使用時幾乎沒有任何限制，可以任意操作該值。
不會進行型別檢查（TypeScript 的型別保護被完全繞過）。
適合用於逐步轉換或不確定型別的情況（但應謹慎使用）。
優點：
    靈活且快速，不需要處理型別檢查。
缺點：
    不安全，因為它讓 TypeScript 放棄型別檢查，可能導致執行期錯誤。

2. unknown
=> let value: unknown;

特性：
允許任意型別的值。
必須先進行型別檢查，才能對該值執行操作。
TypeScript 會強制開發者顯式處理型別保護（例如使用 typeof 或類型斷言）。
適合用於需要更安全的型別處理，但型別不確定的情況。
優點：
    安全，因為它會強制進行型別檢查，避免無意間的型別錯誤。
缺點：
    使用上需要更多的型別保護（相對於 any），稍微麻煩一些。

## type 跟 interface 的差別在哪？
1. 共通點
都可以用來定義物件的結構。
都可以定義類型的形狀（例如物件、函式、聯合型別等）。
都能被用於型別註記，讓 TypeScript 進行型別檢查。
=> 
interface User {
  name: string;
  age: number;
}

// 使用 type
type User = {
  name: string;
  age: number;
};
const user: User = {
  name: "Alice",
  age: 25,
};

2. 差異
(1) 擴展方式
interface 使用 extends
interface 可以使用 extends 來擴展其他介面。
type 使用交集（&）
type 可以使用交集運算符（&）來合併型別。
(2) 型別的靈活性
interface 主要用於描述物件結構。
它只能描述物件型別或類別的結構。
type 可以描述多種型別，不局限於物件。
可以用來定義原始型別、聯合型別、元組等。
(3) 重複定義的行為
interface 支援合併宣告（Declaration Merging）。
如果多次定義相同的介面，TypeScript 會自動將它們合併。
type 不支援重複定義。
如果多次定義相同名稱的 type，TypeScript 會報錯。
(4) 關於類別的實作
interface 可以用於類別的實作（implements）。
類別可以使用 implements 關鍵字來實作介面。
type 不能直接用於類別的 implements。
但可以透過間接方式使用。

使用建議
使用 interface 描述物件結構或類別實作。
它更直觀且可擴展，適合大多數面向物件的程式設計。
使用 type 定義聯合型別、元組、或複雜型別結合。
當需要更靈活或非物件型別時，type 是更好的選擇。
如果你預期需要重複定義或擴展型別，優先考慮使用 interface。

## 請說明泛型（generics）是什麼？
泛型（Generics）是一種工具，讓我們可以建立靈活且可重複使用的程式碼。它允許我們定義可接受多種型別的函式、類別或介面，同時仍保有型別檢查的能力。
泛型允許我們在函式、類別或介面中，使用一個**占位符型別（type parameter）**來表示不確定的型別，這樣可以保留型別檢查並提高靈活性。
=>
function identity<T>(value: T): T {
  return value;
}
const num = identity<number>(42);   // 泛型參數為 number
const str = identity<string>("Hi"); // 泛型參數為 string
<T> 是一個型別參數，像是一個占位符，代表傳入的型別。
value: T 和 return T 表示該函式的輸入與輸出型別相同。
當呼叫函式時，我們可以明確指定型別（例如 <number> 或 <string>），也可以讓 TypeScript 自動推導型別。

1. 泛型函式
function wrapInArray<T>(value: T): T[] {
  return [value];
}
const numArray = wrapInArray(42);      // 推導型別為 number[]
const strArray = wrapInArray("hello"); // 推導型別為 string[]
2. 泛型介面
interface Box<T> {
  content: T;
}
const stringBox: Box<string> = { content: "Hello" }; // T 是 string
const numberBox: Box<number> = { content: 123 };     // T 是 number
3. 泛型類別
class KeyValuePair<K, V> {
  constructor(public key: K, public value: V) {}
}
const pair = new KeyValuePair<string, number>("id", 123);
// key 是 string, value 是 number
4. 泛型約束
function getLength<T extends { length: number }>(value: T): number {
  return value.length;
}
getLength("Hello"); // ✅ 字串有 length 屬性
getLength([1, 2, 3]); // ✅ 陣列有 length 屬性
// getLength(42); // ❌ 錯誤：數字沒有 length 屬性
5. 泛型與預設型別
function logValue<T = string>(value: T): void {
  console.log(value);
}
logValue("Hello"); // ✅ T 推導為 string
logValue(123);     // ✅ T 被顯式指定為 number

### 泛型的優勢
型別安全：
泛型允許我們在型別不明時仍保留型別檢查，避免運行時錯誤。
可重複使用性：
泛型提升了函式、類別和介面的適用範圍，減少重複程式碼。
靈活性：
泛型提供了高靈活性，適合處理不同型別的情境。

泛型是 TypeScript 提供的功能，用於在靈活性與型別安全之間取得平衡。它非常適合用於處理多種型別的程式碼情境，如：
函式庫設計、資料結構（如陣列、樹、圖等）、API 的型別處理

## extend 在泛型中的用途？
extends 在泛型中用來約束泛型的類型，確保泛型符合指定的型別或介面，這樣可以限制泛型的範圍並讓程式更型別安全。
用途
限制泛型的範圍：確保泛型只能是特定型別或其子類型。
使用特定屬性或方法：當泛型被約束時，可以安全地訪問該型別的屬性或方法。
範例
1. 約束泛型型別
=>
function printLength<T extends { length: number }>(value: T): number {
  return value.length;
}
// 正確
console.log(printLength("Hello")); // 字串有 length 屬性 => 5
console.log(printLength([1, 2, 3])); // 陣列有 length 屬性 => 3
// 錯誤
// console.log(printLength(123)); // ❌ 錯誤：數字沒有 length 屬性
2. 限制為某個類別或介面的子類型
=>
interface Person {
  name: string;
}
function greet<T extends Person>(person: T): string {
  return `Hello, ${person.name}`;
}
// 正確
console.log(greet({ name: "Alice" }));
// 錯誤
// console.log(greet({ age: 30 })); // ❌ 錯誤：物件缺少 name 屬性
3. 泛型與聯合型別
function getId<T extends string | number>(id: T): T {
  return id;
}
// 正確
console.log(getId(123)); // 123
console.log(getId("ABC")); // "ABC"
// 錯誤
// console.log(getId(true)); // ❌ 錯誤：boolean 不在約束範圍內

小結
extends 的作用是限制泛型的型別，使其必須滿足特定條件。
可以用來提高程式的型別安全性，防止使用不符合預期的型別。

## enum 和 const 的差別是什麼？
enum 和 const 是兩種用於管理值的方式，但它們的用途和特性不同。
1. enum（列舉）
enum 是 TypeScript 提供的一個特性，用來定義一組有名字的常數值集合。這些值可以是數字或字串，並且在編譯階段會被轉換為物件。
特性
支援自動遞增數字值（數字列舉）。
支援指定具名字串值（字串列舉）。
可以用鍵值對的形式進行雙向映射（僅數字列舉）。
編譯後仍然會保留在 JavaScript 中（有額外的開銷）。
=>
enum Direction {
  Up,    // 預設值為 0
  Down,  // 自動遞增為 1
  Left,  // 2
  Right, // 3
}
console.log(Direction.Up);    // 0
console.log(Direction[0]);    // 'Up'（雙向映射）
=>
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE",
}
console.log(Color.Red); // "RED"
// console.log(Color["RED"]); // ❌ 字串列舉不支援雙向映射

選擇建議
使用 enum：
需要雙向映射（尤其是數字列舉）。
定義大量具名的常量並希望利用其結構。
需要較高可讀性和型別安全的情境。
使用 const：
更追求效能（無額外開銷）。
僅需定義少量的常量集合。
不需要 enum 的雙向映射功能。

## 什麼是 function overload？
Function Overload（函式多載）是一種讓函式可以根據不同的參數組合，執行不同邏輯或返回不同型別的特性。這對於設計靈活且型別安全的函式非常有用。

Function Overload 的核心概念
定義多個函式簽名（overload signatures）：
每個簽名描述函式可以接受的參數和返回的型別。
使用一個實際的函式實現（implementation signature）：
實際的函式實現負責根據參數處理邏輯。
注意：實現的簽名通常更寬鬆，必須覆蓋所有可能的情況。
=>
// 定義多載簽名
function add(a: number, b: number): number;
function add(a: string, b: string): string;
// 實際函式實現
function add(a: any, b: any): any {
  return a + b;
}
// 使用函式
const result1 = add(10, 20);      // result1: number => 30
const result2 = add("Hello, ", "World!"); // result2: string => "Hello, World!"
// const result3 = add(10, "20"); // ❌ 錯誤：不符合多載簽名

Overload 的組成
Overload Signatures（多載簽名）：
定義函式的可能參數和返回型別。
僅描述函式的「介面」，不包含實現。
Implementation Signature（實現簽名）：
真正執行函式的邏輯。
通常使用 any 或更廣泛的型別來涵蓋所有可能情況。
使用 Function Overload 的情境
1. 根據參數型別處理不同邏輯
例如：計算長度，根據輸入的型別不同，返回不同結果。
=>
function getLength(value: string): number;
function getLength(value: any[]): number;
function getLength(value: any): number {
  return value.length;
}
// 使用範例
console.log(getLength("Hello")); // 5
console.log(getLength([1, 2, 3])); // 3
// console.log(getLength(123));   // ❌ 錯誤：不符合多載簽名
2. 返回型別根據輸入改變
例如：根據參數型別，返回數字或字串。
function toArray(value: string): string[];
function toArray(value: number): number[];
=>
function toArray(value: any): any[] {
  return [value];
}
// 使用範例
const strArray = toArray("hello"); // string[] => ['hello']
const numArray = toArray(123);     // number[] => [123]
3. 可變參數數量
例如：根據參數數量返回不同的結果。
=>
function sum(a: number, b: number): number;
function sum(a: number, b: number, c: number): number;
function sum(a: number, b: number, c?: number): number {
  return c ? a + b + c : a + b;
}
// 使用範例
console.log(sum(10, 20));       // 30
console.log(sum(10, 20, 30));   // 60

用 Function Overload 的好處
提高靈活性與可讀性：
函式可以根據不同的參數處理不同的需求。
型別安全：
編譯器會根據多載簽名進行型別檢查，避免潛在的錯誤。
清晰的 API 設計：
開發者可以明確知道函式支援哪些參數組合與返回值。

### source
布魯斯的 TypeScript 入門教學｜用TypeScript輕鬆打造實時聊天室
https://www.youtube.com/watch?v=GinkGJZBHIY
https://www.typescriptlang.org
https://hackmd.io/@mingjunlu/front-end-interview-questions