# lala-food-feed

從拉拉熊（[@zeke_6973](https://www.threads.com/@zeke_6973)）的 Threads 貼文與留言自動整理的店家資料，給 [lala-food](https://github.com/2xin15/lala-food) 使用。

- 說明頁：https://poterpan.github.io/lala-food-feed/
- 最後更新：2026-11-26 22:57（台灣時間）；更新頻率：每天 03:30、12:30、18:30、22:30（台灣時間）

## 端點

| 網址 | 內容 |
|---|---|
| [`venues.json`](https://poterpan.github.io/lala-food-feed/venues.json) | 主要產出。每家店的名稱、地址、座標、CID，加上拉拉熊吃過沒、推不推、Threads 原文連結 |
| [`meta.json`](https://poterpan.github.io/lala-food-feed/meta.json) | 這一版的產生時間、各檔案筆數、因條件不足沒收錄的店家數與原因 |
| [`lala/extra.json`](https://poterpan.github.io/lala-food-feed/lala/extra.json) | 與 lala-food 的 extra.json 同格式：visited_from_wish、visited_add |
| [`lala/notes.json`](https://poterpan.github.io/lala-food-feed/lala/notes.json) | 與 lala-food 的 notes.json 同格式：必點品項 items、拉拉熊原話心得 comment |
| [`lala/posts.json`](https://poterpan.github.io/lala-food-feed/lala/posts.json) | 與 lala-food 的 posts.js 同內容（純 JSON）：每家店（CID）對應的拉拉熊貼文 |
| [`lala/data.js`](https://poterpan.github.io/lala-food-feed/lala/data.js) | lala-food 目前公開的 data.js，已套用上面三個檔案，可直接替換 |
| [`lala/posts.js`](https://poterpan.github.io/lala-food-feed/lala/posts.js) | lala-food 目前公開的 posts.js，已併入找到的貼文，可直接替換 |

## `venues.json` 欄位

| 欄位 | 說明 |
|---|---|
| `cid` | Google 地點 CID（與 lala-food 同一套 ID） |
| `place_id` | Google Places place_id（只從收藏清單對到的店為 null） |
| `name / addr / city / lat / lng` | 店名、地址、縣市、座標 |
| `names_in_threads` | Threads 上出現過的寫法與次數，例如 {"烏弄": 10, "乌弄": 5} |
| `stance` | 誰說了什麼：author:* 是拉拉熊本人，other_user:* 是網友；recommend / negative / mixed / question / mention |
| `experience` | 拉拉熊吃過沒：visited / planned / not_yet / unknown |
| `author_recommends` | 拉拉熊本人的推薦是否多於負評 |
| `in_lala_visited / in_lala_wish` | 是否已在 lala-food 的已去過／愛心清單 |
| `first_seen / last_seen` | 在 Threads 上第一次、最後一次被提到的時間 |
| `sources` | 所有提到這家店的 Threads 原文連結 |
