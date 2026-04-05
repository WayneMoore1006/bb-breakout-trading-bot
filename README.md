# BB Breakout 交易機器人(中文版本)

## 🎯 專案目標

本專案使用 Pine Script v6，在 TradingView 上實作一套**布林通道突破反轉策略（Bollinger Band Breakout Reversal Strategy）**。
其目標是在價格突破統計波動區間（上下軌）時捕捉動能行情，並透過自動反向平倉機制，確保部位管理的清晰與一致性。

---

## 📈 專案概述

本策略設計用於 TradingView 環境中的**量化交易與回測分析**。
系統透過移動平均與標準差自行計算布林通道，並依據突破條件進行交易：

* **做多（Long）** → 當價格收盤高於上軌
* **做空（Short）** → 當價格收盤低於下軌

此外，系統會在開立新倉位前自動平掉反向部位，以避免多空衝突，並確保任一時間僅持有單一方向部位。

---

## 🧠 策略邏輯

* 當 `close > 上軌` 時做多
* 當 `close < 下軌` 時做空
* 在建立新倉位前，自動平掉反向持倉
* 採用**反轉型策略（Reversal Strategy）**，在訊號出現時持續處於市場中

---

## 🖼️ 視覺化

策略內建圖表視覺化功能：

* 布林通道（上軌 / 下軌 / 中線）
* 通道區間填色（顯示波動範圍）
* 訊號標記：

  * 🟢 多單（L）
  * 🔴 空單（S）

---

## 🔧 核心特色

### 獨立指標實作

* 使用 `ta.sma` 與 `ta.stdev` 自行計算布林通道
* 不依賴外部或內建指標模板

### 反轉式部位管理

* 確保不會同時持有多單與空單
* 進場前自動平掉反向倉位

### 支援回測

* 使用 `strategy()` 建立，可直接於 TradingView 進行回測
* 可在圖表中查看策略績效

### 清晰且可解釋的邏輯

* 採用規則式交易（非黑箱模型）
* 易於修改與擴展

---

## 📁 專案結構

.

```
├── bb_breakout_strategy.pine   # Pine Script v6 交易策略
├── .gitignore
└── README.md
```

---

## 🚀 快速開始

### 1️⃣ 開啟 TradingView

進入 TradingView → Pine Editor

### 2️⃣ 貼上程式碼

將 `bb_breakout_strategy.pine` 的內容貼到編輯器中

### 3️⃣ 加入圖表

點擊 **"Add to Chart"** 執行策略

### 4️⃣ 執行回測

開啟 **Strategy Tester** 查看績效指標

---

## 📊 輸出結果

* 交易進出場點會直接顯示於圖表上
* 可於 TradingView 查看策略績效（報酬、最大回撤、勝率等）

以下圖表為使用 TradingView 產生之示意圖，僅供展示與說明用途。  
所有圖表影像之版權皆屬其原平台或相關權利人所有。

<img width="1131" height="591" alt="image" src="https://github.com/user-attachments/assets/7c24de3d-dbb3-4103-a154-be9a7b652a15" />
<img width="1116" height="697" alt="image" src="https://github.com/user-attachments/assets/52ecafd4-1944-4dc5-ab46-5299e0a832cd" />
<img width="1083" height="735" alt="image" src="https://github.com/user-attachments/assets/1f5f72c1-9f52-4094-b97c-fe96eff4725e" />

> ⚠️ **績效免責聲明**
>
> 圖中所顯示之績效、利潤與相關數據皆為模擬交易（回測）結果，並非實際交易成果。
>
> 實際結果可能因市場狀況、交易延遲及其他因素而有所差異。
>
> 請自行承擔投資風險，所有投資決策均由使用者自行負責。

---

## 🧠 設計說明

* 本策略基於**波動突破（Volatility Breakout）概念**
* 使用統計區間（平均值 ± 標準差）判斷異常價格變動
* 強調簡潔性與可重現性，而非複雜模型
* 可延伸應用：

  * 停損 / 停利（Stop Loss / Take Profit）
  * 成交量濾網（Volume Filter）
  * 機器學習訊號整合

---

## 📌 注意事項

本專案僅供**教學、研究與作品集展示用途**。
主要展示**量化交易邏輯、Pine Script 實作能力與系統化策略設計**，並非用於實際交易部署。

---

## ⚠️ 免責聲明

本專案為獨立實作，與 TradingView 無任何關聯或背書。  
TradingView 為其各自擁有者之商標。

本專案部分內容參考公開可取得之 TradingView 腳本，並經過重新設計與獨立實作，加入自訂邏輯與功能強化。

本專案僅供教學、研究與作品集展示用途，並不構成任何投資建議或交易推薦。

請自行承擔使用風險，交易具有高度財務風險，過去績效不代表未來表現。


# BB Breakout Trading Bot(English version)

## 🎯 Project Objective

This project implements a **Bollinger Band breakout reversal strategy** using Pine Script v6 on TradingView.
The goal is to capture momentum-driven price movements when the market breaks above or below statistical volatility bands, while ensuring clean position management through automatic position reversal.

---

## 📈 Project Overview

This strategy is designed for **algorithmic trading and backtesting** within TradingView.
It independently calculates Bollinger Bands using moving average and standard deviation, and executes trades based on breakout conditions:

* **Long Position** → When price closes above the upper band
* **Short Position** → When price closes below the lower band

The system ensures that opposing positions are closed before opening new ones, avoiding conflicting trades and maintaining a single directional exposure at all times.

---

## 🧠 Strategy Logic

* Long when `close > upper band`
* Short when `close < lower band`
* Automatically closes opposite positions before entering a new trade
* Designed as a **reversal strategy** (always in market when signals occur)

---

## 🖼️ Visualization

The strategy includes built-in chart visualization:

* Bollinger Band (Upper / Lower / Basis)
* Filled band area for volatility visualization
* Signal markers:

  * 🟢 Long (L)
  * 🔴 Short (S)

---

## 🔧 Key Features

### Independent Indicator Implementation

* Uses `ta.sma` and `ta.stdev` to compute Bollinger Bands
* No reliance on external or built-in indicator templates

### Reversal-Based Position Management

* Ensures no simultaneous long/short positions
* Automatically closes opposite positions before entering new trades

### Backtesting Ready

* Built with `strategy()` for TradingView backtesting
* Enables performance evaluation directly on charts

### Clear and Interpretable Logic

* Rule-based trading (no black-box model)
* Easy to modify and extend for further experimentation

---

## 📁 Project Structure

.

```
├── bb-breakout-trading-bot.pine   # Pine Script v6 trading strategy
├── .gitignore
└── README.md
```

---

## 🚀 Quick Start

### 1️⃣ Open TradingView

Go to TradingView → Pine Editor

### 2️⃣ Paste the Script

Copy the contents of `bb-breakout-trading-bot.pine` into the editor

### 3️⃣ Add to Chart

Click **"Add to Chart"** to run the strategy

### 4️⃣ Run Backtest

Open the **Strategy Tester** tab to view performance metrics

---

## 📊 Output

* Trade entries and exits plotted directly on chart
* Strategy performance metrics (profit, drawdown, win rate, etc.) available in TradingView

The following charts are generated using TradingView for demonstration purposes only.  
All chart images are the property of their respective owners.

<img width="1131" height="591" alt="image" src="https://github.com/user-attachments/assets/7c24de3d-dbb3-4103-a154-be9a7b652a15" />
<img width="1116" height="697" alt="image" src="https://github.com/user-attachments/assets/52ecafd4-1944-4dc5-ab46-5299e0a832cd" />
<img width="1083" height="735" alt="image" src="https://github.com/user-attachments/assets/1f5f72c1-9f52-4094-b97c-fe96eff4725e" />

> ⚠️ **Performance Disclaimer**
>
> The performance metrics, profits, and results shown in the charts are based on simulated trading (backtesting) and do not represent actual trading performance.
>
> Actual results may vary due to market conditions, execution latency, and other real-world factors.
>
> Please trade at your own risk. All investment decisions are solely your responsibility.

---

## 🧠 Design Notes

* The strategy is based on **volatility breakout principles**
* Uses statistical bands (mean ± standard deviation) to detect abnormal price movement
* Designed for clarity and reproducibility rather than complexity
* Easily extendable with:

  * Stop loss / take profit
  * Volume filters
  * Machine learning signals

---

## 📌 Notes

This project is intended for **educational, research, and portfolio purposes**.
It demonstrates **algorithmic trading logic, Pine Script implementation, and systematic strategy design**, rather than production-level trading deployment.

---

## ⚠️ Disclaimer

This project is an independent implementation and is not affiliated with or endorsed by TradingView.  
TradingView is a trademark of its respective owners.

This project is inspired by publicly available TradingView scripts and has been modified and implemented independently with custom logic and enhancements.

This project is provided for educational, research, and portfolio purposes only. It does not constitute financial advice or a recommendation to trade.

Use at your own risk. Trading involves significant financial risk, and past performance does not guarantee future results.
