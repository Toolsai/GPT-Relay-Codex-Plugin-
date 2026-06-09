# GPT Relay Codex 插件

[English README](./README.md) | [English details](./README.en.md)

GPT Relay 是一個 Codex 插件，用你的 Chrome 登入狀態打開 ChatGPT，把 Codex 的問題轉交給 ChatGPT，等 ChatGPT 完成後，再把完整回覆、圖片、Deep Research 報告和對話連結帶回 Codex。

簡單講：你在 Codex 裡叫插件使用 GPT 5.5 Pro Extended、GPT 5.4 Thinking Light、Deep Research、圖片生成或附件分析，插件會去 Chrome 裡操作 ChatGPT，然後把結果帶回來。

> 這是 Prompt Case 製作的社群插件，不是 OpenAI 或 ChatGPT 官方產品。

## 示範

### Codex 安裝畫面

![GPT Relay 安裝畫面](./media/plugin-install-screen.png)

### Codex 和 ChatGPT 並排操作示範

下面示範展示 Codex 呼叫 GPT Relay，Chrome 同步打開 ChatGPT，選擇指定模型 / 思考模式 / 思考強度，送出 prompt，最後把結果帶回 Codex。

[![觀看 GPT Relay 示範影片](./media/gpt-relay-demo-thumbnail.png)](./media/gpt-relay-demo.mp4)

點擊上方預覽圖，或使用下面連結打開影片。

[打開示範影片](./media/gpt-relay-demo.mp4)

## 安裝方法

### 方法 A：用 Codex 介面安裝

在 Codex 打開 **Plugins** → **Manage** → **Create** → **Add marketplace**，然後填入：

| 欄位 | 填寫內容 |
| --- | --- |
| Source | `Toolsai/GPT-Relay-Codex-Plugin-` |
| Git ref | `main` |
| Sparse paths | 一般情況留空即可。如果你的 Codex 版本要求 sparse checkout，可以填 `.agents/plugins` 和 `plugins/gpt-relay`。 |

加入 marketplace 後，安裝 **GPT Relay**，然後開一個新的 Codex thread。

### 方法 B：用 CLI 安裝

在 Codex 環境執行：

```bash
codex plugin marketplace add Toolsai/GPT-Relay-Codex-Plugin-
codex plugin add gpt-relay@gpt-relay
```

安裝後請開一個新的 Codex thread，讓 Codex 載入新的插件 skill。

## 使用前需要

- Codex 支援插件功能。
- Codex 能使用 Chrome / Chrome automation。
- 你的 Chrome 已經登入 ChatGPT。
- 你的 ChatGPT 帳號本身要有你要求的模型或模式。比如 Pro 模式需要 ChatGPT Pro 帳號。

## Marketplace 需要什麼

這個 repo 已經整理成 Codex 可以加入的 plugin marketplace。Codex 需要看到：

- repo 根目錄有 `.agents/plugins/marketplace.json`
- 插件 manifest 在 `plugins/gpt-relay/.codex-plugin/plugin.json`
- 插件本體在 `plugins/gpt-relay`
- Git ref 通常填 `main`

你截圖裡的 **Add marketplace** 是把這個 GitHub repo 加成自訂 marketplace 來源；它和「提交到 OpenAI 官方內建商店」不是同一件事。

## 支援能力

- 如果你沒有指定更換模型，會保留你 ChatGPT 原本的模型設定。
- 如果你指定模型，會嘗試切換到可見的 ChatGPT Intelligence 選項，例如 `5.5 Pro Extended` 或 `5.4 Thinking Light`。
- 如果你的帳號看不到某個模型或模式，插件會明確告訴你，而不是偷偷改用其他模型。
- 可以把 prompt 和支援的附件傳給 ChatGPT。
- 回傳文字會盡量保留 ChatGPT 原本格式，包括標題、列表、表格、連結和程式碼。
- 圖片生成任務會回傳圖片 artifact。
- Deep Research 任務會匯出 Markdown 報告 artifact。
- 會保存 session 資料，方便繼續對話或輪詢長時間任務。

## 常用例子

```text
Use GPT 5.5 Pro Extended to analyze this question: ...
```

```text
Run Deep Research on this topic: ...
```

```text
Switch to GPT 5.4 Thinking Light and analyze this image.
```

## 更新插件

之後如果這個 GitHub repo 有更新，可以執行：

```bash
codex plugin marketplace upgrade gpt-relay
codex plugin add gpt-relay@gpt-relay
```

更新後同樣建議開一個新的 Codex thread。

## 注意事項

- GPT Relay 是透過 ChatGPT 網頁 UI 操作。如果 ChatGPT 改版，插件可能需要更新 selector。
- 插件只會報告 ChatGPT 畫面上可見和已選中的模型 / 模式 / 強度，不會聲稱知道背後隱藏狀態。
- 如果遇到登入、CAPTCHA、權限彈窗，或者帳號沒有相關模型，插件會停止並回報原因。
