# 【ArgoX】 = Argo + Xray

中文 | [English](README_EN.md)

## 交互式运行脚本

```
bash <(wget -qO- https://raw.githubusercontent.com/hkzping999/ArgoX/main/argox.sh)
```
```
wget https://raw.githubusercontent.com/hkzping999/ArgoX/main/argox.sh -O argox.sh
bash -n argox.sh
sudo bash argox.sh
 ```
/etc/argox                    # 项目主体目录
├── subscribe                 # 订阅文件目录
│   ├── base64                # V2rayN / Nekobox 订阅文件
│   ├── clash                 # Clash 订阅文件
│   ├── proxies               # Clash proxy provider 订阅文件
│   ├── shadowrocket          # Shadowrocket 订阅文件
│   └── sing-box              # SFI / SFA / SFM 订阅文件
├── cert                      # 自签证书目录
│   ├── cert.pem              # 证书文件
│   └── private.key           # 私钥文件
├── cloudflared               # argo tunnel 主程序
├── custom                    # 用户自定义持久化配置文件（serverIp / cdn / language 等）
├── geoip.dat                 # 用于根据 IP 地址来进行地理位置策略或访问控制
├── geosite.dat               # 用于基于域名或网站分类来进行访问控制、内容过滤或安全策略
├── inbound.json              # 按已选协议动态生成的入站配置文件
├── list                      # 节点信息列表
├── nginx.conf                # Nginx 配置文件（安装 WS/XHTTP 协议或启用订阅功能时生成）
├── outbound.json             # 出站和路由配置文件，chatGPT 使用 warp ipv6 链式代理出站
├── xray                      # xray 主程序
├── ax.sh                     # 快捷方式脚本文件
├── jq                        # 命令行 JSON 处理器
└── qrencode                  # QR 码编码二进制文件
```




## 免责声明:
* 本程序仅供学习了解, 非盈利目的，请于下载后 24 小时内删除, 不得用作任何商业用途, 文字、数据及图片均有所属版权, 如转载须注明来源。
* 使用本程序必循遵守部署免责声明。使用本程序必循遵守部署服务器所在地、所在国家和用户所在国家的法律法规, 程序作者不对使用者任何不当行为负责。
