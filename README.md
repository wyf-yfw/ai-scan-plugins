# AI Scan 插件市场

一个仓库同时供 Claude Code、Codex、WorkBuddy、Cursor 安装。插件本体在 `plugins/ai-scan`，四份市场清单只登记这一份。

仓库地址：`https://github.com/wyf-yfw/ai-scan-plugins`。这是私有仓库，客户的 GitHub 账号需要有读取权限。

## 客户安装

Claude Code：

```bash
claude plugin marketplace add https://github.com/wyf-yfw/ai-scan-plugins.git
claude plugin install ai-scan@ai-scan-plugins
```

Codex：

```bash
codex plugin marketplace add https://github.com/wyf-yfw/ai-scan-plugins.git
codex plugin add ai-scan@ai-scan-plugins
```

WorkBuddy：在插件页添加市场，输入下面的地址。也可以在对话里执行：

```text
/plugin marketplace add https://github.com/wyf-yfw/ai-scan-plugins.git
/plugin install ai-scan@ai-scan-plugins
```

Cursor：打开左侧 Customize，点 Add，选 GitHub 仓库，粘贴 `https://github.com/wyf-yfw/ai-scan-plugins`。列表里出现 AI Scan 后点 Add。

也可以在 Agent 对话里整句输入：

```text
/add-plugin ai-scan@https://github.com/wyf-yfw/ai-scan-plugins.git
```

装好后点插件页右上角的 Configure，填写 MCP 地址和 API Key，再点 Save。地址形如 `http://<设备>:8765/mcp`，本机默认是 `http://127.0.0.1:8765/mcp`。请求头名是 `X-Api-Key`。

## 安装时填写设备

插件带有 MCP 服务 `ai-scan`。仓库里没有具体地址和密钥，安装或启用时由使用者填写：

- 地址：`http://<设备>:8765/mcp`。Claude Code 的默认值是 `http://127.0.0.1:8765/mcp`，设备不在本机就改掉。
- API Key：产品里签发的密钥，请求头名是 `X-Api-Key`。
- Cursor：在插件页右上角点 Configure，填 MCP 地址和 API Key，再点 Save。

Codex 安装后 MCP 和技能都在，地址和密钥是空的。第一次使用，或 MCP 连不上时，执行技能 `ai-scan-init`。它会询问设备地址和 API Key，并写入本机 `%USERPROFILE%\.codex\config.toml` 的 `mcp_servers.ai-scan`。请求头名是 `X-Api-Key`。写完后新开一个对话再使用。

跑客户端的机器必须能访问设备的 `8765` 端口。更新市场后再安装一次，才会看到这个 MCP。

## 仓库里各家读哪份清单

| 客户端 | 清单 |
|---|---|
| Claude Code | `.claude-plugin/marketplace.json` |
| Codex | `.agents/plugins/marketplace.json` |
| WorkBuddy | `.codebuddy-plugin/marketplace.json` |
| Cursor | `.cursor-plugin/marketplace.json` |
