---
name: mimo-fix
description: 诊断和修复小米 MiMo 模型报错问题。当用户遇到 MiMo 模型 401 错误、model not found、或微信小月无响应时触发。也用于开启/关闭 1M 上下文模式。
---

# MiMo 模型修复工具

## 诊断步骤

按顺序执行以下检查：

### 1. 检测 API Key 是否有效

```bash
curl -s -o /dev/null -w "%{http_code}" -X POST "https://api.xiaomimimo.com/anthropic/v1/messages" \
  -H "Content-Type: application/json" \
  -H "x-api-key: <当前key>" \
  -H "anthropic-version: 2023-06-01" \
  -d '{"model":"mimo-v2.5-pro","max_tokens":10,"messages":[{"role":"user","content":"hi"}]}'
```

- 返回 200 = 有效
- 返回 401 = key 失效，需要更换

### 2. 检查配置一致性

读取三个文件，对比模型名是否一致（注意 `[1m]` 后缀）：
- `~/.cc-connect/config.toml` — 找 `[[providers]]` 中 `name = "mimo-v2.5-pro"` 的 `model` 字段
- `~/.claude/settings.json` — 对比所有 `ANTHROPIC_*_MODEL` 字段
- `~/.claude/profiles/mimopro.json` — **profile 会覆盖 settings.json，必须检查**

用 grep 一次性搜索所有残留：
```bash
grep -rn "\[1m\]\|\[1M\]" ~/.claude/settings.json ~/.claude/profiles/ ~/.cc-connect/config.toml
```

### 3. 检查 session 是否有旧错误

```bash
grep -i "issue with the selected model\|401\|Invalid API Key" ~/.cc-connect/sessions/*.json
```

如果找到匹配，说明 session 缓存了旧错误，需要清除。

## 修复方案

### 方案 A：API Key 失效

用户需要提供新的 key，然后同时更新两个文件：

1. 更新 `~/.cc-connect/config.toml` 中所有 `api_key = "新key"`
2. 更新 `~/.claude/settings.json` 中 `ANTHROPIC_AUTH_TOKEN` 为新 key
3. 清除 session：删除 `~/.cc-connect/sessions/*.json`
4. 重启 cc-connect

### 方案 B：Session 有旧错误

1. 清除 session：删除 `~/.cc-connect/sessions/*.json`
2. 重启 cc-connect

### 方案 C：开启/关闭 1M 上下文

**开启 1M：**
- `config.toml` 中 `model = "mimo-v2.5-pro[1m]"`
- `settings.json` 中所有模型名改为 `mimo-v2.5-pro[1m]`

**关闭 1M（恢复默认）：**
- `config.toml` 中 `model = "mimo-v2.5-pro"`
- `settings.json` 中所有模型名改为 `mimo-v2.5-pro`

修改后需清除 session 并重启。

## 重启命令

```powershell
# 杀进程（不要 kill 所有 node.exe，会误杀 MCP server）
Stop-Process -Name cc-connect -Force
Get-CimInstance Win32_Process | Where-Object { $_.CommandLine -match "typing-companion" } | ForEach-Object { Stop-Process -Id $_.ProcessId -Force }

# 清除 session（模型/配置变更时必须）
Remove-Item ~/.cc-connect/sessions/*.json

# 启动 cc-connect（必须用 RedirectStandardOutput，否则日志会缓冲）
Start-Process -FilePath "D:\npm-global\cc-connect.cmd" `
  -ArgumentList "--config","C:\Users\Lenovo\.cc-connect\config.toml" `
  -RedirectStandardOutput "C:\Users\Lenovo\.cc-connect\cc-connect.log" `
  -RedirectStandardError "C:\Users\Lenovo\.cc-connect\cc-connect.err" `
  -WindowStyle Hidden

# 等待 cc-connect 就绪
Start-Sleep -Seconds 5

# 启动 typing-companion
Start-Process node `
  -ArgumentList "D:\cc-switch\weixin-claude-bridge\typing-companion.js" `
  -RedirectStandardOutput "C:\Users\Lenovo\.cc-connect\typing-companion.log" `
  -RedirectStandardError "C:\Users\Lenovo\.cc-connect\typing-companion.err" `
  -WindowStyle Hidden
```

## 配置文件位置

| 文件 | 路径 | 用途 |
|------|------|------|
| cc-connect 配置 | `~/.cc-connect/config.toml` | 模型、API key、平台配置 |
| Claude Code 配置 | `~/.claude/settings.json` | 环境变量、模型名 |
| Claude Code Profile | `~/.claude/profiles/mimopro.json` | **会覆盖 settings.json** |
| Session 文件 | `~/.cc-connect/sessions/*.json` | 对话历史 |
| 日志 | `~/.cc-connect/cc-connect.log` | 运行日志 |
| typing-companion | `D:\cc-switch\weixin-claude-bridge\typing-companion.js` | 消息监控 |
