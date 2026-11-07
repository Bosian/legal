# Bosian / legal

公開法律文件（GitHub Pages）。給 Google Play 的 **Terms of Service** 欄位、以及之後各商店／各 app 共用。

**Pages URL**：`https://bosian.github.io/legal/`

| 用途 | URL |
|---|---|
| Play Console「服務條款」欄位（**兩支 app 都填這個**） | `https://bosian.github.io/legal/terms.html` |
| 英文版（同內容） | `https://bosian.github.io/legal/terms.en.html` |
| 退款／撤回權說明頁（可當退款政策連結） | `https://bosian.github.io/legal/refund.html` |
| 文件索引 | `https://bosian.github.io/legal/` |

## 檔案

```
index.html        文件索引（zh-Hant 為主，含英文連結）
terms.html        服務條款（zh-Hant）
terms.en.html     Terms of Service (English)
refund.html       退款與撤回權（zh-Hant）
refund.en.html    Refunds and right of withdrawal (English)
assets/style.css  共用樣式（含 prefers-color-scheme）
.nojekyll         跳過 Jekyll 建置
```

無建置步驟：純靜態 HTML，改檔 push 到 `main` 即上線（Pages 部署約 1 分鐘）。

## 涵蓋的產品

**通用條款**：主文不逐支列舉 app，而是按「**取得方式**」（付費下載／免費／應用程式內購買）定規。

**附錄表已刪除（2026-11-07）**：原本 15 列的「產品／套件識別碼／取得方式」表整個拿掉 —— package name 對使用者是無意義字串、產品身分由商店頁＋開發者名就已確定，而手寫清單反而會過期、且容易被讀成「只有列出的才適用」。現在改成指向**權威且會自己更新**的來源：`https://play.google.com/store/apps/developer?id=Bo-Sian+Liou`（實測 200，標題＝「Google Play 上『Bo-Sian Liou』的 Android 應用程式」）。

**2026-11-07 查證**：Google Play 上架 **15 支**，全部在同一個開發者帳號「**Bo-Sian Liou**」（交易商聲明是**帳號層**＋每 app 確認，所以一次聲明涵蓋全部）：

| 取得方式 | 支數 |
|---|---|
| 付費下載 | 8（countdownlife、militarycountdown、travelmap、whatsforlunch、lifecost、flashlight、photoeditor、humanalarm） |
| 免費 | 7（各 `*lite`／`.lite` 版） |

**新 app 上架完全不用動這個 repo 的任何檔案**（清單由商店頁自己生成，條款按取得方式定規）。

查證方法（可重跑）：`GET https://play.google.com/store/apps/details?id=<pkg>&hl=en&gl=US`，看 `<meta itemprop="price" content="$0.99">`（付費）與 `content="0"`（免費）；廣告看整份 HTML 的 `Contains ads`。**注意**：`In-App Purchases` 與 `Contains ads` 都出現在文件尾端的 `__INITIAL_STATE__`（約 1.0M 字元後），**不能只看頁首**，也會被「相關應用」carousel 污染 —— 判 IAP 要看該標章是否出現在 app 自己的 offer 區塊（與 `990000,"USD","$0.99"` 同段）。

## 設計決定（改之前先讀這段）

### 1. 聯絡方式不寫 email，指向商店頁

交易商的電話／地址由 Google Play 商店頁公開顯示（個人帳號＋交易商＝強制揭露），ToS 內不再重複列 email/地址，避免四處同步。代價：「可直接聯絡」這點稍弱，若之後要強化，在 `terms.html` 第 14 節與 `refund.html`「如何申請退款」補信箱。

### 2. 交易商名稱用 `Bo-Sian Liou`（以 Bosian 名義發行）

2027-03-01 起 EEA/UK 的「Offered by」會顯示 Play 上的開發者名，實測是 **`Bo-Sian Liou`**（不是 `Bosian`）→ ToS 寫 `Bo-Sian Liou`（publishing as Bosian）讓兩者對齊。若要改成法定姓名或純品牌名，改 `terms.html` 第 2 節、`index.html`、各頁 header/footer。

### 3. 撤回權：不能靠條款排除，所以改成「揭露 ＋ 自願 14 天退款」

這是本 repo 最重要的決定，不要隨意改回「概不退費」。要點：

- CRD **Art 16(m)** 的例外需要消費者在履行開始前做**獨立的明示同意＋確認喪失撤回權**（歐盟執委會指引：pre-ticked box 或「已同意一般條款」**不足**，要 positive action 如勾選框）。
- 付費下載的結帳 UI **完全在 Google 手裡**，開發者拿不到那個勾選框 → **單靠 ToS 文字無法有效成立例外**。
- 未滿足 Art 8(7)(b) 確認義務時，**Art 14(4)(b)** 的救濟照樣適用（最壞情況＝白送＋退款）。所以把「14 天退款」主動寫成自己的政策，是把最壞結果收編，同時消除被追責的資訊義務缺口。
- 因此條款寫成：承認原則上下載開始即喪失撤回權 → 但交易商**自願**給 14 天退款 → 且不排除瑕疵救濟與強制性消費者權利。
- **絕對不要**寫「所有銷售均為最終／概不退費」：與 Art 14(4)(b) 衝突，且容易被認定為不公平條款。

### 4. 其他條款要點

- 第 9 節明確講「倒數顯示僅供參考、不保證提醒必然送達」—— 這是倒數/提醒類 app 最實際的争議來源。
- 第 12 節：付費購買適用**購買當時**的條款（修訂不得對已購買者為不利變更）。
- 第 13 節：準據法中華民國，但明文不排除歐盟/英國消費者慣常居住地的強制規定。
- 免費版（Lite）無買賣契約 → 撤回權章節明文「不適用」，但 Lite 仍是交易商（廣告營收）→ 仍要交易商揭露＋ToS。

## 更新流程

1. 改 HTML（zh 與 en **務必同步改**，兩份是一一對應）。
2. 更新該頁 header 與 footer 的「發布日期／生效日期」（`Published` / `Effective`）。
3. `git commit` + `push` → 等約 1 分鐘。
4. 驗證：`curl -sI https://bosian.github.io/legal/terms.html`（200）＋ 開瀏覽器看排版。

## 法源與來源（查證於 2026-11-07）

- CRD Art 9 / 16(m) / 8(7) / 14(4)：<https://www.legislation.gov.uk/eudr/2011/83/adopted>
- 執委會 CRD 指引與總覽（2021 Notice CELEX 52021XC1229(04)）：<https://commission.europa.eu/law/law-topic/consumer-protection-law/consumer-contract-law/consumer-rights-directive_en>
- 執委會「立即提供數位內容要放勾選框」建議文字：<https://commission.europa.eu/system/files/2019-07/sr_information_presentation.pdf>
- UK CCR 2013 reg 30 / reg 37：<https://www.legislation.gov.uk/uksi/2013/3134/contents/made>
- DMCCA 2024（執法權給 CMA，上限全球營業額 10%；2025-11 首批罰單已落地）；訂閱新制只管訂閱，一次性買斷不適用。
- Google Play 交易商聲明（截止 2027-02-01；marketplace model 2027-03-01）：<https://support.google.com/googleplay/android-developer/answer/17594752>
- Google Play 現行 EEA/UK ToS 的 withdrawal waiver（Google 自己當賣方時的寫法，2027 後不適用於開發者）：<https://play.google.com/about/play-terms/eea/index.html>
- DDA §3.8（Google 得依其退款政策退款並從收入扣款）、§10.3/§11.4（聲明不實可停權）：<https://play.google/developer-distribution-agreement.html>

**文件缺口**：Google 到 2026-11 為止**沒有**說明 2027-03-01 後退款／撤回的責任歸屬（trader 聲明頁只要求 ToS 連結＋聯絡資訊＋自證）。本 repo 的自願退款策略同時覆蓋「Google 機制」與「法定撤回權」兩邊，所以這個缺口不阻擋上線。

## 待辦

- [ ] **PhotoEditor 的商店頁掛著 `In-App Purchases` 標章，但實際上沒有 IAP**（2026-11-07 實測：該標章出現在 app 自己的 offer 區塊、出 2 次，不是相關應用污染）。應去 Play Console 確認並清掉（IAP 產品清單／內容設定），否則標章與實際不符。ToS 已按「沒有 IAP」寫產品表，且第 5 節用「以商店頁面標示為準」包住這個不一致。
- [ ] 之後真的接 IAP 時要複查：訂閱／消耗型商品的條款（訂閱另有 EU 訂閱契約新制與 UK *Consumer Subscription Contracts (Cancellation and Information) Regulations 2026*）。
- [ ] iOS 端若要同一份，App Store 的 EULA 欄位可指同一 URL。
- [ ] `urgebrake` 的 Android 尚未上架（`com.bosian.urgebrake`／`...lite` 回 404）→ 上架後自動進入開發者清單，**不用改條款**。
