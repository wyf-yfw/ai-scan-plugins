# AI Scan 插件市场

一个仓库同时供 Claude Code、Codex、WorkBuddy、Cursor 安装。插件本体在 `plugins/ai-scan`，四份市场清单只登记这一份。

仓库地址：`https://gitlab.inone.nsfocus.com/wvss/ai-scan/ai-scan-plugins`。这是私有仓库，客户的账号需要有读取权限。

## 客户安装

Claude Code：

```bash
claude plugin marketplace add https://gitlab.inone.nsfocus.com/wvss/ai-scan/ai-scan-plugins.git
claude plugin install ai-scan@ai-scan-plugins
```

Codex：

```bash
codex plugin marketplace add https://gitlab.inone.nsfocus.com/wvss/ai-scan/ai-scan-plugins.git
codex plugin add ai-scan@ai-scan-plugins
```

WorkBuddy：在插件页添加市场，输入下面的地址。也可以在对话里执行：

```text
/plugin marketplace add https://gitlab.inone.nsfocus.com/wvss/ai-scan/ai-scan-plugins.git
/plugin install ai-scan@ai-scan-plugins
```

Cursor 2.5 及以上，在 Agent 对话里整句输入：

```text
/add-plugin ai-scan@https://gitlab.inone.nsfocus.com/wvss/ai-scan/ai-scan-plugins.git
```

## 装完后填写设备

每台 AI Scan 的地址和密钥不同，仓库里不写这两项。安装后在对应客户端添加远程 MCP：

- 地址：`http://<设备>:8765/mcp`
- 请求头：`X-Api-Key: <产品里签发的密钥>`

运行 IDE 的机器必须能访问设备的 `8765` 端口。产品里的 MCP 服务需要监听该地址，默认端口是 `8765`。

## 仓库里各家读哪份清单

| 客户端 | 清单 |
|---|---|
| Claude Code | `.claude-plugin/marketplace.json` |
| Codex | `.agents/plugins/marketplace.json` |
| WorkBuddy | `.codebuddy-plugin/marketplace.json` |
| Cursor | `.cursor-plugin/marketplace.json` |
