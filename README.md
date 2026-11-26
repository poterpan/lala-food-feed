# lala-food-feed

從拉拉熊（[@zeke_6973](https://www.threads.com/@zeke_6973)）的 Threads 貼文、留言與收藏清單自動整理的店家資料。

- 說明頁：https://poterpan.github.io/lala-food-feed/
- 最後更新：2026-11-27 04:52（台灣時間）；更新頻率：每天 03:30、12:30、18:30、22:30（台灣時間）

## v1：標準格式（推薦）

| 網址 | 內容 |
|---|---|
| [`v1/venues.json`](https://poterpan.github.io/lala-food-feed/v1/venues.json) | 所有店家：Threads 上有證據的，加上拉拉熊收藏清單裡的。每家都標明依據（吃過、推薦、收藏） |
| [`v1/recommendations.json`](https://poterpan.github.io/lala-food-feed/v1/recommendations.json) | 社群推薦：網友推薦給拉拉熊、他還沒吃過的店，依推薦人數與他的反應（想去、記下來）排序 |
| [`v1/brands.json`](https://poterpan.github.io/lala-food-feed/v1/brands.json) | 連鎖品牌層級的推薦（拉拉熊推了某品牌但沒說哪間分店），附必點、原話、已知分店 |
| [`v1/evidence.json`](https://poterpan.github.io/lala-food-feed/v1/evidence.json) | 每一條證據：哪家店或品牌、拉拉熊或網友、立場、拉拉熊原話（逐字）、原文連結、日期 |
| [`v1/posts.json`](https://poterpan.github.io/lala-food-feed/v1/posts.json) | 拉拉熊提到店家的每篇貼文與回覆，以及各自連到哪些店（venue_ids；正式介紹的店在 about_venue_ids） |
| [`v1/meta.json`](https://poterpan.github.io/lala-food-feed/v1/meta.json) | 產生時間、各項數量、因條件不足沒收錄的店與原因 |
| [`v1/schema/`](https://poterpan.github.io/lala-food-feed/v1/schema/) | 以上檔案的 JSON Schema |

## lala/：lala-food 相容格式（由 v1 產生）

| 網址 | 內容 |
|---|---|
| [`lala/data.js`](https://poterpan.github.io/lala-food-feed/lala/data.js) | 只用 v1 產生的完整版：已去過＝拉拉熊吃過，愛心＝他的收藏清單 |
| [`lala/posts.js`](https://poterpan.github.io/lala-food-feed/lala/posts.js) | 只用 v1 產生：每家店（CID）對應的拉拉熊貼文 |
| [`lala/extra.json`](https://poterpan.github.io/lala-food-feed/lala/extra.json) | 相對於 lala-food 目前資料的差異，格式同其 extra.json |
| [`lala/notes.json`](https://poterpan.github.io/lala-food-feed/lala/notes.json) | 必點品項與拉拉熊原話心得，格式同其 notes.json |
| [`lala/posts.json`](https://poterpan.github.io/lala-food-feed/lala/posts.json) | 相對於 lala-food 目前資料的貼文對應（純 JSON） |
| [`lala/merged/data.js`](https://poterpan.github.io/lala-food-feed/lala/merged/data.js) | lala-food 目前的 data.js 套用上面差異後的結果（保留其手動修改） |
| [`lala/merged/posts.js`](https://poterpan.github.io/lala-food-feed/lala/merged/posts.js) | lala-food 目前的 posts.js 併入新找到的貼文 |

## `v1/venues.json` 主要欄位

| 欄位 | 說明 |
|---|---|
| `id / cid` | Google 地點 CID（與 lala-food 同一套 ID） |
| `place_id` | Google Places place_id；只來自收藏清單的店為 null |
| `name / address / city / lat / lng / category` | 店名、地址、縣市、座標、分類 |
| `brand` | 所屬連鎖品牌（不是連鎖則為 null） |
| `author.visited` | 拉拉熊說過或照片顯示他吃過 |
| `author.recommends` | 拉拉熊本人的推薦多於負評為 true，相反為 false，沒表態為 null |
| `author.saved / saved_at / saved_note` | 是否在拉拉熊分享的任一 Google 地圖清單、加入時間（Unix 秒）、他在清單上的備註 |
| `author.lists` | 在哪幾份清單：id、title、meaning（saved＝收藏；recommended＝他說平常會去吃，算吃過且推薦） |
| `basis` | 依據：threads（Threads 上有提到）、saved_list（在收藏清單） |
| `tier` | 分級：author_visited 拉拉熊吃過 › author_endorsed 拉拉熊推薦 › community_recommended 網友推薦（推薦多於差評）› author_saved 只在他的清單 › mentioned 只被提到 |
| `community` | 網友推薦：推薦次數、推薦人數（不同網友，不公開帳號）、拉拉熊的反應（visited/planned/not_yet/unknown）、是否他自己發問、網友推薦的品項、差評次數（negative）。拉拉熊沒提過、只有網友差評的店不收錄 |
| `names_in_threads` | Threads 上出現過的寫法與次數 |
| `stance` | 誰說了什麼：author:* 是拉拉熊，other_user:* 是網友 |
| `items / quotes` | 必點品項、拉拉熊原話（逐字、已對照原文，附連結） |
| `post_urls` | 拉拉熊正式介紹這家店的貼文（lala/posts.js 用這個） |
| `related_post_urls` | 所有跟這家店有關的拉拉熊貼文／回覆，包含只有網友在他串底下提到的情況 |
| `first_seen / last_seen / sources` | Threads 上第一次與最後一次提到的時間、所有原文連結 |
