# 订阅链接转换器 s8mr2u

[中文版] 支持 Clash / Surge / V2Ray / QuanX / ShadowRocket 格式互转，自动去重、测速筛选。

## 功能特性

- 多格式互转：Clash / Surge / V2Ray / Quantumult / ShadowRocket
- 节点去重和过滤（按国家/地区、协议、标签）
- 自动测速筛选（可选）
- Web 界面 + API 接口

## 快速开始

pip install -r requirements.txt
python subconverter.py &
默认监听 25500 端口
Web 界面: http://localhost:25500

## API 使用

GET /api/v1/subscribe?target=clash&url=https://your-subscription-url

### 进阶参数
?target=clash&url=订阅URL&exclude=广告节点,测试&include=美国,香港&emoji=true&sort=true

## Python SDK

import requests
params = {
    "target": "clash",
    "url": "你的订阅URL",
    "emoji": True,
    "include": "美国,香港,日本"
}
clash_config = requests.get("http://localhost:25500/api/v1/subscribe", params=params).text

## 配置文件

bind: 0.0.0.0:25500
remove-emoji: false
sort: true

## 许可证

MIT License

推荐工具

- [Clash for Windows](https://clashforwindows.site/) - Windows 最流行的 Clash 图形化客户端
- [ClashMI](https://clashmi.site/) - 轻量级 Clash 客户端，支持多平台
- [FlClash](https://flclash.us/) - 现代代理工具，支持多种协议