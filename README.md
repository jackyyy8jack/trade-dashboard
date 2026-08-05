# Trade Journal Dashboard

MEXC 永續合約的手動交易紀錄，主帳號 + 子帳號合併顯示。

資料由本機程式每隔一段時間抓 MEXC API、寫成 `state.json` 後推上來，
網頁每 5 秒自動 refresh。

## 顯示內容

- 🏦 兩個帳號的權益、可用餘額、目前持倉
- 📈 資產曲線（可切 Trade / 1h / 4h / 1d / 1w / 1M）
- 📜 交易明細：時間 / 帳號 / 商品 / 方向 / 進出場價 / 損益 / ROI
- 📊 總筆數、勝率、平均賺賠、最大賺賠（可依帳號篩選）
- ⚠️ 抓取錯誤紀錄

## 資料來源

MEXC 合約 API `position/list/history_positions`（已平倉的歷史倉位）。
損益取 `realised`（已含資金費），報酬率取 MEXC 自己算的 `profitRatio`。

金鑰不在這個 repo 裡，也不會出現在任何 commit。
