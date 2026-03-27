# Shortlink v101

這個資料夾是 shortlink 的第一版資料維護區。

版本：

- `v101`
- 意義：`v1.01`

主檔：

- [falo-shortlink-json-editor-v101.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v101.html)
- [falo-shortlink-guide-v101.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-guide-v101.html)

## 這是什麼工具

這一版不是 router，不是 redirect 頁，也不是 GAS 後台。

它的角色很單純：

- `falo-shortlink-json-editor-v101.html`
  - `links.json` 維護器
- `falo-shortlink-guide-v101.html`
  - 給人看的說明頁

用途：

- 自動讀取預設 `links.json`
- 手動上傳既有 `links.json`
- 顯示 slug 與 target URL 列表
- 新增 / 修改 / 刪除 shortlink
- 匯出新的 `links.json`

## links.json 格式

v1 先固定使用最簡字串對字串格式：

```json
{
  "123": "https://www.google.com/",
  "demo": "https://force.formosa-ai.com",
  "force": "https://force.formosa-ai.com/about/",
  "qrcode": "https://falo-taiwan.github.io/tools/qrcode/falo-qrcode-v102.html",
  "shortlink": "https://falo-taiwan.github.io/tools/shortlink/falo-shortlink-json-editor-v101.html"
}
```

規則：

- key = slug
- value = target URL
- 先只支援字串對字串
- 不做 `title / note / status / tags`

這個格式的好處：

- 好懂
- 好教
- 好維護
- 最好接 `404.html`
- 後續升級成 GAS / JSON fallback 也容易

## 如何使用

### 1. 自動讀取預設 JSON

打開 [falo-shortlink-json-editor-v101.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v101.html) 後，頁面會先嘗試讀取 repo root 的 `links.json`。

如果成功：

- 會顯示資料來源是「預設 `links.json`」
- 直接列出目前 slug / target URL

如果失敗：

- 會顯示提示訊息
- 仍可使用手動上傳或內建 sample 繼續編輯

補充：

- 在 `file://` 本機模式下，瀏覽器常會擋掉自動讀檔
- 這是瀏覽器安全限制，不是工具壞掉
- 所以 v1 預設就保留手動上傳流程

### 2. 手動上傳 JSON

如果自動讀取失敗，或你要改另一份資料：

1. 點選檔案欄位
2. 上傳既有 `links.json`
3. 工具會驗證格式是否為最簡 object

### 3. 編輯 / 新增 / 刪除

- 每筆資料都包含：
  - `slug`
  - `target URL`
- 上方有「新增一筆」欄位，可直接輸入新的 `slug` 與 `target URL`
- 按下新增後，會直接加入清單，並立即下載一份新的 JSON
- 可直接修改既有資料
- 可刪除單筆資料

驗證規則：

- `slug` 不可空白
- `slug` 只接受英數、底線 `_`、連字號 `-`
- `slug` 不可重複
- URL 必須是完整的 `http` 或 `https`

### 4. 下載新的 JSON

有兩種下載方式：

1. 在上方新增一筆時，按 `新增一筆並下載 JSON`
2. 完成整體修改後，按 `匯出 links.json`

新增一筆時，檔名會自動帶時間戳到「分」，例如：

- `links-20260327-1530.json`

這一版不會自動寫回 GitHub。

## 建議放置位置

主站 repo：

- `falo-taiwan.github.io`

建議結構：

```text
/
├─ 404.html
├─ links.json
├─ /go/
│   └─ （未來 shortlink 入口路徑）
├─ /tools/
│   ├─ /qrcode/
│   │   ├─ falo-qrcode-v102.html
│   │   └─ README.md
│   └─ /shortlink/
│       ├─ falo-shortlink-json-editor-v101.html
│       ├─ falo-shortlink-guide-v101.html
│       └─ README.md
```

重點：

- `links.json` 放在 repo root
- `404.html` 也放在 repo root
- `404.html` 後續可直接吃 root 的 `links.json`
- `tools/shortlink/` 放維護工具與說明文件

## 如何人工覆蓋到主站 root

建議流程：

1. 打開 shortlink editor
2. 讀取目前 `links.json`
3. 完成新增 / 修改 / 刪除
4. 匯出新的 `links.json`
5. 把下載好的檔案，手動覆蓋主站 repo root 的 `/links.json`
6. 提交並部署主站

如果你是人工維護 GitHub Pages，這個流程是最直覺也最穩的。

## 後續如何接到 404.html

目前 `404.html` 已驗證能接管 `/go/<slug>`。

下一步建議是：

1. `404.html` 只處理 `/go/<slug>`
2. 在命中 `/go/<slug>` 時，fetch root 的 `links.json`
3. 成功後用 `slug -> target URL` 查表
4. 有命中就 redirect
5. 沒命中就顯示 `Shortlink not found`

這樣可以保留：

- GitHub Pages static hosting
- shortlink routing
- 簡單可教的資料結構

## 後續 v2：GAS / JSON fallback

v2 再升級成：

- GAS 作為正式維護來源
- `links.json` 作為 fallback

也就是：

1. `404.html` 先嘗試拿 GAS 指令
2. 若 GAS timeout、格式錯、沒有 target，就 fallback 改吃 root 的 `links.json`

這樣 v1 做好的資料面不會浪費，而是會成為 v2 的保底層。
