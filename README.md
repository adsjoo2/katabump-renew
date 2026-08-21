## 🚀 katabump 自动续期（GitHub Actions）

这是一个基于 GitHub Actions 的自动化脚本，用于定时登录自动续期 [katabump](https://dashboard.katabump.com) 应用。

🌐 网络走 **Cloudflare WARP**（与 Wispbyte 相同：`fscarmen/warp-on-actions` + `warp-cli`），不再使用 sing-box / `NODE_LINK` 代理。系统级 WARP 出口有助于通过 Cloudflare 盾。

━━━━━━━━━━━━━━━━━━━━━━

🔐 Secrets 配置说明

| Secret 名称        | 是否必填 | 说明                                 |
|--------------------|----------|--------------------------------------|
| KATABUMP_EMAIL     | ✅ 必填  | katabump 登录邮箱                    |
| KATABUMP_PASSWORD  | ✅ 必填  | katabump 登录密码                    |
| TG_BOT_TOKEN       | ❌ 可选  | Telegram Bot Token（用于发送通知）   |
| TG_CHAT_ID         | ❌ 可选  | Telegram Chat ID（接收通知的用户或群组 ID） |

━━━━━━━━━━━━━━━━━━━━━━
### 网络说明

工作流会在运行脚本前启用 Cloudflare WARP：

- Action：`fscarmen/warp-on-actions@v1.4`
- `mode: client`（安装官方 `warp-cli`，便于更换 IP）
- `stack: dual`（IPv4 + IPv6）

浏览器不需要再挂 `vless://` / `vmess://` / SOCKS 等节点。登录若被 Cloudflare 拦截，脚本会自动重启 WARP 更换 IP 并重试（最多 3 次）。

若仓库里还留着旧的 `NODE_LINK` Secret，可以删掉，已经不再使用。

### 注意事项
- cron 时间根据自己的服务到期时间的前一天来修改
