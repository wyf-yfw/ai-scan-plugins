---
name: ai-scan-init
description: 第一次使用 AI Scan，或 AI Scan 的 MCP 缺少地址、缺少 API Key、连不上、鉴权失败、工具列表为空时必须先执行。向用户询问设备 URL 和 API Key，写入当前客户端的本机 MCP 配置。用户提到配置 AI Scan、填写地址、填写密钥、MCP 失效时使用。
---

# 初始化 AI Scan

插件安装后只有 MCP 和技能，地址和密钥是空的。本技能负责问用户并写到本机配置。密钥只放在用户自己的客户端配置里，不要写入插件仓库，不要提交 git，不要在回复里重复密钥全文。

## 何时执行

下面任一情况先做完本技能，再调用 AI Scan 工具：

- 还没有可用的 `ai-scan` MCP，或配置里没有地址、没有 `X-Api-Key`
- 连接失败、超时、401、403，或工具列表为空
- 用户要改地址或密钥

已经连上并且工具调用正常时，不要重新询问。

## 询问

一次问齐这两项。用户没给齐就停下来等，不要猜，也不要用仓库或示例里的值。

1. 设备地址。必须是绝对地址，形如 `http://<设备>:8765/mcp`。本机扫描器才用 `http://127.0.0.1:8765/mcp`。
2. API Key。这是产品里签发的密钥，请求头名固定为 `X-Api-Key`。

收到后只复述地址，并说明密钥已收到。用户确认后再写入。

## 写入 Codex

配置文件是 Codex 主目录下的 `config.toml`。Windows 上是 `%USERPROFILE%\.codex\config.toml`，设置了 `CODEX_HOME` 时用 `$CODEX_HOME/config.toml`。

只改 `ai-scan` 这两组，其它表原样保留：

```toml
[mcp_servers.ai-scan]
enabled = true
url = "用户给的地址"

[mcp_servers.ai-scan.http_headers]
X-Api-Key = "用户给的密钥"
```

插件里带的那条 MCP 没有密钥，不能用来连接。把它关掉，避免和上面这条抢同一个名字：

```toml
[plugins."ai-scan@ai-scan-plugins".mcp_servers.ai-scan]
enabled = false
```

写完告诉用户新开一个 Codex 对话，让 MCP 重新加载。然后用一个只读工具确认连接，例如列出任务或查看系统状态。还是失败，就说明失败原因，并再问一次地址和密钥。

## 写入其它客户端

按当前客户端写，仍然只改 `ai-scan` 这一条。

Claude Code：写当前项目在 `~/.claude.json` 里的 `mcpServers.ai-scan`。

```json
{
  "type": "http",
  "url": "用户给的地址",
  "headers": {
    "X-Api-Key": "用户给的密钥"
  }
}
```

Cursor：不要改 `mcp.json`。让用户打开已安装的 AI Scan 插件，点右上角 Configure，填写 MCP 地址和 API Key，再点 Save。地址形如 `http://<设备>:8765/mcp`。

WorkBuddy：插件用 `user_config.scan_url` 和 `user_config.api_key`。本机若已有 MCP 配置文件，按 Claude Code 的结构写入 `ai-scan`。没有可写文件时，把这两项交给用户填进插件的配置项。
