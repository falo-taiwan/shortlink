# Shortlink

這個資料夾現在不只是維護工具集合，也是一個完整的 shortlink 小專案。

核心定位：

- `Google Sheets + GAS`
  - 主資料源
- `網站 root /links.json`
  - published snapshot / fallback
- `tools/shortlink/404.html`
  - shortlink 專案內唯一維護的 router 原始檔

一句話理解：

- shortlink 專案內維護
- 網站 root 手動部署

## 專案邊界

現在這個 shortlink 專案包含三條線：

1. 維護頁
- `falo-shortlink-json-editor-v101.html`
- `falo-shortlink-json-editor-v102.html`
- `falo-shortlink-json-editor-v103.html`
- `falo-shortlink-json-editor-v104.html`
- `falo-shortlink-json-editor-v105.html`
- `falo-shortlink-json-editor-v106.html`
- `falo-shortlink-json-editor-v201.html`

2. router
- [404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
- 這是 shortlink 專案內唯一維護的 router 原始檔
- GitHub Pages 真正部署時，再手動放到網站 root 的 `/404.html`
- [404_gas_first_v101.htm](/Users/force/AI-CodeX/tools/shortlink/404_gas_first_v101.htm)
  - 保留的 GAS-first 對照版
- [404_js_first_v101.htm](/Users/force/AI-CodeX/tools/shortlink/404_js_first_v101.htm)
  - 保留的 JSON-first 版本檔

3. GAS 範本
- [gas-v2/README.md](/Users/force/AI-CodeX/tools/shortlink/gas-v2/README.md)
- [gas-v2/main.gs](/Users/force/AI-CodeX/tools/shortlink/gas-v2/main.gs)

4. 404 router 專用文件
- [404-readme.md](/Users/force/AI-CodeX/tools/shortlink/404-readme.md)

## Source Of Truth

對 shortlink 這個專案來說，建議的 source of truth 是：

- router source：
  - [tools/shortlink/404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
- data source：
  - Google Sheets + GAS
- fallback snapshot：
  - 網站 root 的 `links.json`

版本：

- `v101`
- 意義：`v1.01`
- `v102`
- 意義：`v1.02`
- `v103`
- 意義：`v1.03`
- `v104`
- 意義：`v1.04`
- `v105`
- 意義：`v1.05`
- `v106`
- 意義：`v1.06`
- `v201`
- 意義：外部測試版 `v2.01`

主檔：

- [falo-shortlink-json-editor-v101.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v101.html)
- [falo-shortlink-json-editor-v102.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v102.html)
- [falo-shortlink-json-editor-v103.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v103.html)
- [falo-shortlink-json-editor-v104.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v104.html)
- [falo-shortlink-json-editor-v105.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v105.html)
- [falo-shortlink-json-editor-v106.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v106.html)
- [falo-shortlink-json-editor-v201.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v201.html)
- [404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
- [404_gas_first_v101.htm](/Users/force/AI-CodeX/tools/shortlink/404_gas_first_v101.htm)
- [404_js_first_v101.htm](/Users/force/AI-CodeX/tools/shortlink/404_js_first_v101.htm)
- [404-readme.md](/Users/force/AI-CodeX/tools/shortlink/404-readme.md)
- [falo-shortlink-guide-v101.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-guide-v101.html)
- [falo-shortlink-guide-v102.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-guide-v102.html)
- [gas-v2/README.md](/Users/force/AI-CodeX/tools/shortlink/gas-v2/README.md)

## 這是什麼工具

這一區現在有三種角色：

- `falo-shortlink-json-editor-v101.html`
  - JSON 視角維護器
- `falo-shortlink-json-editor-v102.html`
  - 表格視角維護器
- `falo-shortlink-json-editor-v103.html`
  - 防呆一致性維護器
- `falo-shortlink-json-editor-v104.html`
  - 操作優化維護器
- `falo-shortlink-guide-v101.html`
  - v101 給人看的說明頁
- `falo-shortlink-guide-v102.html`
  - v102 給人看的說明頁
- `falo-shortlink-json-editor-v105.html`
  - Google Sheet 直連維護器
  - 透過 GAS 讀取與更新主資料源
- `falo-shortlink-json-editor-v106.html`
  - v105 的延伸版
  - 把這次 timeout 是關鍵因素的發現正式寫進版本
  - 適合拿來當「GAS 主資料源不等於一定即時成功」的教材版
- `falo-shortlink-json-editor-v201.html`
  - 給外部使用者測試的版本
  - 把網站用途直接寫給使用者看
  - 密碼欄改成明碼顯示，並預填測試期間密碼 `123`
- `404.html`
  - shortlink router 維護來源
  - 用來接管 `/go/<slug>`
  - 目前主線策略改成：
    - `links.json` first
    - GAS JSONP lookup
    - GAS fetch lookup
    - 中轉頁版本時間顯示
- `404_gas_first_v101.htm`
  - 保留舊版 router
  - 策略是先查 GAS，再 fallback JSON
- `404_js_first_v101.htm`
  - 保留新版 router 版本檔
  - 策略是先查 JSON，再查 GAS
- `gas-v2/`
  - Google Sheets + Apps Script 版最小可用範本
  - 先收成單一 `main.gs` 版
  - 檔內用模組區塊註解分功能
  - 提供公開 lookup、簡單密碼 admin、snapshot 匯出與 backup

## v101 / v102 / v103 / v104 / v105 / v106 / v201 的差異

- `v101`
  - 比較像工程底稿 / JSON 對照版
  - 適合教學、理解資料格式、直接對照輸出結果
- `v102`
  - 比較像日常維護頁 / 表格操作版
  - 使用者不必直接看 raw JSON
  - 主要改用表格做排序、分頁、編輯、新增、刪除
- `v103`
  - 比較像防錯優先的資料層版本
  - 重點不在多功能，而在資料一致性
  - 補上操作者欄位、URL 自動補全、archive / delete 狀態、舊格式轉換與統一小寫
- `v104`
  - 延續 v103 的防呆規則
  - 時間改成台北時間
  - `archived` / `deleted` 後可直接按 `active` 恢復
  - 把操作按鈕移到表格最左邊
- `v105`
  - 把維護頁正式接上 GAS
  - 可直接讀取 Google Sheet
  - 可直接送 `create / update / archive / restore / delete / export_snapshot / backup_now`
  - 主資料源從本地 JSON 維護，升級成 GAS / Sheet 維護
  - 密碼欄位改為遮罩顯示，可手動切換顯示 / 隱藏
  - 預設改成依 `updated_at` 降冪排序
  - 補上關鍵字搜尋欄，主要用於搜尋網址
- `v106`
  - 延續 `v105` 的 GAS 直連維護流程
  - 額外把這次 shortlink 成敗與 timeout 之間的關係正式寫進版本註解
  - 用來提醒：資料存在，不代表查詢一定能在短時間內成功
- `v201`
  - 給外部測試者使用
  - 文字改成更偏使用者導向，不是內部工程維護口吻
  - 密碼欄改成明碼輸入框，並預填 `123`

一句話理解：

- `v101` = JSON 視角
- `v102` = 表格視角
- `v103` = 防呆一致性視角
- `v104` = 操作優化視角
- `v105` = GAS 直連維護視角
- `v106` = GAS 直連 + timeout 教學視角
- `v201` = GAS 外部測試視角
- `gas-v2` = GAS 主資料源視角

用途：

- 自動讀取預設 `links.json`
- 手動上傳既有 `links.json`
- 顯示 slug 與 target URL
- 新增 / 修改 / 刪除 shortlink
- 匯出新的 `links.json`

## links.json 格式

`v101` / `v102` 主要操作的基礎格式：

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

`v103` / `v104` 匯出格式：

```json
{
  "demo": {
    "target_url": "https://force.formosa-ai.com",
    "status": "active",
    "created_at": "2026-03-28t00:00:00.000z",
    "created_by": "force",
    "updated_at": "2026-03-28t00:00:00.000z",
    "updated_by": "force"
  }
}
```

規則：

- `slug` 一律作為外層 key
- `target_url / created_by / updated_by / status` 一律轉小寫
- `status` 只接受：
  - `active`
  - `archived`
  - `deleted`
- 若匯入舊格式：
  - `{ "123": "https://xxx" }`
  - 會自動轉成新格式
- `404.html` 已同步升級成可吃舊格式與 `v103` 新格式
- `v104` 的 `created_at / updated_at` 改用台北時間（`Asia/Taipei`）

補充：

- `v103` 會連 `target_url` 一起轉小寫
- 這是為了優先降低錯誤率
- 某些區分大小寫的 URL path 可能會有 edge case
- 這一版先接受這個取捨，README 明確記錄規則

## 如何使用

### 1. 自動讀取預設 JSON

打開 [falo-shortlink-json-editor-v101.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v101.html) 後，頁面會先嘗試讀取網站 root 的 `links.json`。

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
- `v101`
  - 上方有新增欄位
  - 可直接修改列表中的資料
- `v102`
  - 上方有新增表單
  - 中間主畫面是表格
  - 可依 `slug` 或 `target URL` 做前端排序
  - 內建分頁，每頁固定 10 筆
  - 點選某列的「編輯」後，在右側編輯表單修改
  - 刪除前會有確認提示
- `v103`
  - 上方先設定操作者，可選 `force / goma / terra`，也可手動輸入
  - 一律轉小寫後存入
  - 若 URL 未填 `http://` 或 `https://`，會自動補 `http://`
  - `archive` 與 `delete` 不做真刪除，只改 `status`
  - 匯入舊格式時會自動轉成新格式
  - 所有資料欄位都統一轉小寫後匯出
- `v104`
  - 延續 `v103` 的所有防呆規則
  - 表格左邊就是操作按鈕
  - `active / archive / delete` 都能直接點
  - 時間欄位改成台北時間

驗證規則：

- `slug` 不可空白
- `slug` 只接受英數、底線 `_`、連字號 `-`
- `slug` 不可重複
- URL 必須是完整的 `http` 或 `https`
- `status` 只接受 `active / archived / deleted`

### 4. 下載新的 JSON

有兩種下載方式：

1. `v101`
   - 在上方新增一筆時，可直接下載 JSON
   - 或按 `匯出 links.json`
2. `v102`
   - 完成表格操作後，按 `匯出新的 links.json`
3. `v103`
   - 完成表格操作後，按 `匯出新的 links.json`
   - 匯出的會是新 object 格式
4. `v104`
   - 完成表格操作後，按 `匯出新的 links.json`
   - 匯出的會是新 object 格式
   - `created_at / updated_at` 一律使用台北時間

匯出檔名會自動帶時間戳到「分」，例如：

- `links-20260327-1530.json`

這一版不會自動寫回 GitHub。

## 建議目錄

主站網站：

- `https://falo-taiwan.github.io`

建議結構：

```text
/
├─ 404.html
├─ links.json
├─ /tools/
│   ├─ /qrcode/
│   │   ├─ falo-qrcode-v102.html
│   │   └─ README.md
│   └─ /shortlink/
│       ├─ 404.html
│       ├─ falo-shortlink-json-editor-v101.html
│       ├─ falo-shortlink-json-editor-v102.html
│       ├─ falo-shortlink-json-editor-v103.html
│       ├─ falo-shortlink-json-editor-v104.html
│       ├─ falo-shortlink-json-editor-v105.html
│       ├─ falo-shortlink-guide-v101.html
│       ├─ falo-shortlink-guide-v102.html
│       ├─ /gas-v2/
│       │   ├─ main.gs
│       │   ├─ appsscript.json
│       │   └─ README.md
│       └─ README.md
```

重點：

- `links.json` 放在網站 root
- shortlink 專案內唯一維護的是 `tools/shortlink/404.html`
- 每次調整 router 時，只改 `tools/shortlink/404.html`
- 確認沒問題後，再手動部署到網站 root 的 `/404.html`
- `tools/shortlink/` 放維護工具、router source 與說明文件

## Router 同步流程

建議流程：

1. 先改 [tools/shortlink/404.html](/Users/force/AI-CodeX/tools/shortlink/404.html)
2. 確認中轉頁版本時間有更新
3. 再手動部署到網站 root 的 `/404.html`
4. 重新整理後測主站
5. 線上測：
   - `/go/demo`
   - `/go/g1`
   - `/go/pch3`
   - `/go/notfound`

如果線上中轉頁看不到最新時間，例如：

- `Router Updated: YYYY-MM-DD HH:MM TPE`

就代表網站上的 `/404.html` 還不是最新部署版。

## 如何人工覆蓋到主站 root

建議流程：

1. 打開 shortlink editor
2. 讀取目前 `links.json`
3. 若你想看資料契約與 JSON 對照，用 `v101`
4. 若你想直接維護表格，用 `v102`
5. 若你想優先降低錯誤率與統一格式，用 `v103`
6. 若你想在窄畫面下也更穩定操作，用 `v104`
7. 完成新增 / 修改 / active / archive / delete
8. 匯出新的 `links.json`
9. 確認匯出內容沒問題
10. 把下載好的檔案，手動覆蓋網站 root 的 `links.json`
11. 若 router 也有更新，再手動部署網站 root 的 `/404.html`
12. 重新整理後測主站

如果你平常真的要維護，建議順序是：

1. 先打開 [falo-shortlink-json-editor-v102.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v102.html)
2. 在表格中排序、找資料、編輯、新增、刪除
3. 匯出新的 `links.json`
4. 再人工覆蓋網站 root 的 `links.json`

如果你現在要優先防錯，我更建議：

1. 先打開 [falo-shortlink-json-editor-v104.html](/Users/force/AI-CodeX/tools/shortlink/falo-shortlink-json-editor-v104.html)
2. 先設定操作者
3. 再做新增、編輯、active、archive、delete
4. 匯出新的 `links.json`
5. 再人工覆蓋網站 root 的 `links.json`

如果你要做教學或查資料格式，再回頭看 `v101`。

如果你是人工維護 GitHub Pages，這個流程是最直覺也最穩的。

## Router 工作方式

目前 router 的工作方式是：

1. 使用者打 `/go/<slug>`
2. 網站 root 的 `/404.html` 接管
3. 先問 GAS
   - 先走 JSONP
   - 若 JSONP 沒有 usable result，再退回 fetch
4. 若 GAS 成功
   - 直接 redirect
5. 若 GAS 失敗
   - fallback 到網站 root 的 `links.json`
6. 若都沒有
   - 顯示 `Shortlink not found`

## 後續如何接到 404.html

目前 `404.html` 已驗證能接管 `/go/<slug>`。

下一步建議是：

1. `404.html` 只處理 `/go/<slug>`
2. 在命中 `/go/<slug>` 時，fetch root 的 `links.json`
3. 成功後支援兩種資料格式：
   - 舊格式：`slug -> url`
   - 新格式：`slug -> { target_url, status, ... }`
4. 有命中就 redirect
5. `status !== active` 視為不可用
6. 沒命中就顯示 `Shortlink not found`

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
