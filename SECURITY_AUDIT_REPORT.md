# ArgoX 安全净化版审计说明

本包基于用户上传的 `ArgoX-main.zip` 修改，仅对脚本做安全加固，未改变项目许可证。

## 已处理的主要风险

1. 禁用第三方 GitHub 反代
   - 原脚本包含 `hub.glowp.xyz`、`proxy.vvvv.ee` 作为 GitHub 下载代理。
   - 安全版将 `GITHUB_PROXY=()`，强制不经第三方反代下载。

2. 禁用运行统计上报
   - 原脚本会请求 `stat.cloudflare.now.cc/updateStats?...`。
   - 安全版将 `statistics_of_run-times()` 改为空函数，不再上报运行统计。

3. 禁用 OpenAI / ChatGPT 解锁检测
   - 原脚本会请求 `api.openai.com` 和 `ios.chat.openai.com`。
   - 安全版将 `check_chatgpt()` 改成本地返回，不再发起这些检测请求。

4. 禁用 Reality 私钥远程换公钥 API
   - 原脚本在本地推导失败时，会把 Reality privateKey 发送到 `realitykey.cloudflare.now.cc`。
   - 安全版删除该远程 fallback，避免私钥外传。

5. 删除 `--no-check-certificate`
   - 原脚本大量使用 `wget --no-check-certificate`。
   - 安全版删除这些参数，恢复 HTTPS 证书校验。

6. 禁用菜单里的远程脚本二次执行
   - 原脚本菜单会直接执行 TCP 优化、sing-box、sba 等第三方远程脚本。
   - 安全版将这些动作改成提示并退出。

7. 禁用旧版远程降级桥接
   - 原脚本在旧安装检测场景下可能跳转执行历史版本远程脚本。
   - 安全版改为报错退出，避免远程执行旧代码。

8. 修改提示文案
   - 删除/替换推荐通过第三方网站获取 Cloudflare Json 的提示。
   - 建议只从 Cloudflare 官方后台生成 Token/Json。

## 仍然保留的必要联网行为

这个脚本仍然是安装器，因此无法完全离线运行。安全版仍会访问：

- GitHub / GitHub Releases：下载 cloudflared、Xray、jq、订阅模板等。
- Cloudflare API：当用户使用 Cloudflare API 创建隧道/DNS 时。
- `ip.cloudflare.now.cc`：用于识别 VPS 公网 IP 信息。
- 本机 `localhost` 端口：用于读取 cloudflared metrics。

如果你需要更严格的“完全离线版”，应提前下载 cloudflared/Xray/jq/qrencode 并在脚本内改成本地文件路径，同时为每个文件加 SHA256 校验。

## 使用方式

```bash
unzip ArgoX-main-safe.zip
cd ArgoX-main
bash -n argox.sh
sudo bash argox.sh
```

不要再使用：

```bash
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/argox/main/argox.sh)
```

## 校验结果

已执行：

```bash
bash -n argox.sh
```

结果：语法检查通过。

## 重要提醒

安全版降低了明显的隐私泄漏和供应链风险，但不代表“绝对安全”。任何 VPS 一键安装器都会修改系统服务、防火墙、Nginx、Xray、Cloudflared 等配置。建议先在空白 VPS 或虚拟机测试。
