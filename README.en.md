# GPT Relay Codex Plugin

[Main README](./README.md) | [中文说明](./README.zh-Hant.md)

GPT Relay lets Codex delegate a task to ChatGPT through your existing Chrome session. It can request visible ChatGPT Intelligence combinations, wait for the final answer, and return the full result to Codex.

## Why This Exists

Codex is excellent for coding work, local files, and automation. ChatGPT may have account-specific UI features such as Pro mode, Deep Research, image generation, and visible model/mode/effort controls. GPT Relay bridges those workflows by letting Codex operate ChatGPT in Chrome when you explicitly ask it to.

## Installation

From the Codex UI:

| Field | Value |
| --- | --- |
| Source | `Toolsai/GPT-Relay-Codex-Plugin-` |
| Git ref | `main` |
| Sparse paths | Leave blank for normal install. Optional: `.agents/plugins` and `plugins/gpt-relay`. |

Or use the CLI:

```bash
codex plugin marketplace add Toolsai/GPT-Relay-Codex-Plugin-
codex plugin add gpt-relay@gpt-relay
```

Open a new Codex thread after installation.

The Add marketplace dialog installs this repository as a custom Codex marketplace source. It is not the same thing as publishing to an official built-in OpenAI marketplace.

## Repository Layout

```text
.agents/plugins/marketplace.json
plugins/gpt-relay/
  .codex-plugin/plugin.json
  skills/gpt-relay/SKILL.md
  scripts/chatgpt_relay.mjs
  assets/logo.png
media/
  plugin-install-screen.png
  gpt-relay-demo-thumbnail.png
  gpt-relay-demo.mp4
```

## Capabilities

- Visible ChatGPT Intelligence selection.
- Default behavior that preserves your current ChatGPT selection unless you request a change.
- Pro effort handling: Standard and Extended.
- Thinking effort handling: Light, Standard, Extended, and Heavy when visible.
- Clear unavailable-option errors instead of silent fallback.
- Prompt relay, file upload, image generation, web search, and Deep Research requests.
- Full delivery back to Codex with Markdown formatting, images, artifacts, and conversation URLs.
- Stored session metadata for continuation and polling.

## Limitations

- Requires Chrome automation and an active ChatGPT login.
- Availability depends on your ChatGPT account.
- The plugin operates the visible ChatGPT web UI, so ChatGPT UI changes may require plugin updates.
- Long-running tasks may need polling from Codex.

## Developer

Created by Prompt Case.
