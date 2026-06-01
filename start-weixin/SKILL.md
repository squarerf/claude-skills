---
name: start-weixin
description: 后台启动微信 Claude Bridge（cc-connect + typing-companion）
---

# 启动微信 Claude Bridge

当用户说"启动微信"、"开启微信"、"打开微信"、"start weixin"时，执行以下步骤。

## 前置条件

- cc-connect 安装路径：`D:\npm-global\cc-connect.cmd`
- typing-companion 路径：`D:\cc-switch\weixin-claude-bridge\typing-companion.js`
- 配置文件：`C:\Users\Lenovo\.cc-connect\config.toml`
- 日志目录：`C:\Users\Lenovo\.cc-connect\`

## 执行步骤

### 第一步：停止旧进程

```powershell
taskkill /F /IM cc-connect.exe 2>$null
# 注意：不要 kill 所有 node.exe，只 kill typing-companion 相关的
```

用 PowerShell 查找并停止 typing-companion 进程：
```powershell
Get-CimInstance Win32_Process | Where-Object { $_.CommandLine -match "typing-companion" } | ForEach-Object { Stop-Process -Id $_.ProcessId -Force }
```

### 第二步：后台启动 cc-connect

使用 PowerShell 的 `Start-Process`，必须重定向日志输出（否则日志会缓冲，typing-companion 无法实时监控）：

```powershell
Start-Process -FilePath "D:\npm-global\cc-connect.cmd" `
  -ArgumentList "--config","C:\Users\Lenovo\.cc-connect\config.toml" `
  -RedirectStandardOutput "C:\Users\Lenovo\.cc-connect\cc-connect.log" `
  -RedirectStandardError "C:\Users\Lenovo\.cc-connect\cc-connect.err" `
  -WindowStyle Hidden
```

### 第三步：等待 cc-connect 就绪

等待 5 秒，确保 cc-connect 完成初始化并写入日志：

```powershell
Start-Sleep -Seconds 5
```

验证启动成功：
```bash
tail -3 "$USERPROFILE/.cc-connect/cc-connect.log"
# 应看到 "cc-connect is running"
```

### 第四步：后台启动 typing-companion

同样使用 PowerShell 重定向日志：

```powershell
Start-Process node `
  -ArgumentList "D:\cc-switch\weixin-claude-bridge\typing-companion.js" `
  -RedirectStandardOutput "C:\Users\Lenovo\.cc-connect\typing-companion.log" `
  -RedirectStandardError "C:\Users\Lenovo\.cc-connect\typing-companion.err" `
  -WindowStyle Hidden
```

验证启动成功：
```bash
cat "$USERPROFILE/.cc-connect/typing-companion.log"
# 应看到 "已启动" 和 "监控日志中..."
```

## 关键注意事项

1. **启动顺序**：必须先 cc-connect，后 typing-companion（companion 需要监控 cc-connect 的日志文件）
2. **日志重定向**：必须用 `-RedirectStandardOutput` 重定向，否则 PowerShell 的 `Start-Process` 会导致日志缓冲，typing-companion 无法实时检测消息
3. **不要用 `cmd /c start /B`**：从 bash 调用时行为不可靠
4. **不要 kill 所有 node.exe**：会误杀 MCP server 等其他 node 进程

## 日志文件说明

| 文件 | 用途 |
|------|------|
| `cc-connect.log` | cc-connect 主日志，typing-companion 监控此文件 |
| `cc-connect.err` | cc-connect 错误日志 |
| `typing-companion.log` | typing-companion 运行日志 |
| `typing-companion.err` | typing-companion 错误日志 |
