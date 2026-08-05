# Trade Journal Dashboard

MEXC 永續合約的手動交易紀錄，主帳號 + 子帳號合併顯示。

---

## 🌐 網址

**https://jackyyy8jack.github.io/trade-dashboard/**

手機、平板、任何裝置的瀏覽器直接開就好。

### ⚠️ 第一次要先啟用，不然是 404

1. 到這個 repo 的 **Settings**（上方齒輪）
2. 左側選單往下找 **Pages**
3. **Source** 選 `Deploy from a branch`
4. **Branch** 選 `main`，右邊資料夾選 `/ (root)`
5. 按 **Save**

按完等 1～2 分鐘，重新整理 Settings → Pages，
上方出現綠色的 `Your site is live at ...` 就成功了。

**這個設定只要做一次**，往後每次 push 都自動更新，不用再碰。

### 加到手機主畫面（像 App 一樣）

- **iPhone**：Safari 開啟 → 分享鈕 → 加入主畫面
- **Android**：Chrome 開啟 → 右上選單 → 新增至主畫面

---

## 📊 頁面說明

上方五個分頁：

| 分頁 | 內容 |
|---|---|
| **Overview** | 兩個帳號的權益、可用餘額、目前持倉、最近成交 |
| **Equity** | 資產曲線，可切 Trade / 1h / 4h / 1d / 1w / 1M |
| **Trades** | 交易明細，可篩選 全部 / 主帳號 / 子帳號 |
| **Errors** | 抓取失敗的紀錄（正常時是空的） |
| **About** | 已記錄的筆數與商品 |

右邊的酒保可以點。

網頁每 **5 秒**自動重抓資料，不用手動重新整理。

---

## 🔄 資料多久更新一次

```
MEXC API ──每60秒查詢──> 本機程式 ──git push──> GitHub Pages ──每5秒fetch──> 瀏覽器
```

MEXC 不會主動通知，只能定時去問，靠 `positionId` 比對出沒看過的紀錄。
一筆交易從平倉到出現在網頁上，**最慢約 65 秒**。

### 網頁沒更新？

1. 看 Overview 左上角的狀態燈與 `↻ 時間`，那是資料產生的時間
2. 時間停住 → 本機的 `journal/push.py --loop 60` 沒在跑
3. 顯示「金鑰過期」→ MEXC 合約 API key 效期 90 天到了，要重新申請

---

## 資料來源

MEXC 合約 API `position/list/history_positions`（已平倉的歷史倉位）。

- 損益取 `realised`（已含資金費）
- 報酬率取 MEXC 自己算的 `profitRatio`（對保證金的 ROI）
- 部位大小已用各商品的 `contractSize` 從「張數」換算成「幣數」

金鑰不在這個 repo 裡，也不會出現在任何 commit。
