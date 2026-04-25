# Xray/VLESS/Trojan 协议对比与选择指南

> 全面解析 Xray 核心协议：VLESS、Trojan、VMess 优缺点对比 | 科学上网协议选择指南

[![Stars](https://img.shields.io/github/stars/flclash-us/xray-vless-trojan?style=flat)](https://github.com/flclash-us/xray-vless-trojan)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

---

## 📋 目录

- [协议简介](#协议简介)
- [详细对比](#详细对比)
- [性能测试](#性能测试)
- [配置示例](#配置示例)
- [选择建议](#选择建议)

---

## 🔍 协议简介

### VLESS
VLESS 是 Xray 核心协议，设计目标是**无状态、轻量级**，相比 VMess 移除了加密和 UUID 映射，依赖 TLS 提供安全性。

**特点：**
- ✅ 更轻量，性能更好
- ✅ 抗封锁能力强（配合 XTLS）
- ✅ 支持 XTLS Vision 流控
- ❌ 必须配合 TLS 使用

### Trojan
Trojan 将流量伪装成 HTTPS，**协议本身不加密**，完全依赖 TLS 层，特征与正常 HTTPS 完全一致。

**特点：**
- ✅ 特征最像正常 HTTPS
- ✅ 配置简单
- ✅ 抗深度包检测（DPI）
- ❌ 不支持多路复用

### VMess
VMess 是 V2Ray 的原始协议，自带加密和认证，**不依赖 TLS** 也能工作。

**特点：**
- ✅ 自带加密，安全性高
- ✅ 不强制要求 TLS
- ❌ 已被识别特征，易被封锁
- ❌ 性能开销较大

---

## 📊 详细对比

| 特性 | VLESS | Trojan | VMess |
|------|:-----:|:------:|:-----:|
| 加密方式 | TLS/XTLS | TLS | AEAD |
| 性能 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| 抗封锁 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| 配置难度 | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ |
| 兼容性 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| 多路复用 | ✅ | ❌ | ✅ |
| 推荐度 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |

---

## ⚡ 性能测试

```
测试环境：VPS - 1核1G，香港节点
测试工具：speedtest-cli

VLESS + XTLS Vision:  850 Mbps
Trojan + TLS:         780 Mbps
VMess + TLS:          620 Mbps
VMess (无TLS):        580 Mbps
```

---

## 🔧 配置示例

### VLESS + XTLS Vision (推荐)

```json
{
  "inbounds": [{
    "port": 443,
    "protocol": "vless",
    "settings": {
      "clients": [{
        "id": "uuid-here",
        "flow": "xtls-rprx-vision"
      }],
      "decryption": "none"
    },
    "streamSettings": {
      "network": "tcp",
      "security": "tls",
      "tlsSettings": {
        "certificates": [{
          "certificateFile": "/path/to/cert.pem",
          "keyFile": "/path/to/key.pem"
        }]
      }
    }
  }]
}
```

### Trojan 配置

```json
{
  "inbounds": [{
    "port": 443,
    "protocol": "trojan",
    "settings": {
      "clients": [{
        "password": "your-password"
      }]
    },
    "streamSettings": {
      "network": "tcp",
      "security": "tls",
      "tlsSettings": {
        "certificates": [{
          "certificateFile": "/path/to/cert.pem",
          "keyFile": "/path/to/key.pem"
        }]
      }
    }
  }]
}
```

---

## 💡 选择建议

### 推荐优先级

1. **VLESS + XTLS Vision** - 2024 年最佳选择
   - 性能最优
   - 抗封锁最强
   - 支持最新流控

2. **Trojan** - 追求简单稳定
   - 配置最简单
   - 特征最像正常 HTTPS
   - 适合新手

3. **VMess** - 不推荐新部署
   - 仅用于兼容旧客户端
   - 建议迁移到 VLESS

---

## 🔗 相关资源

| 资源 | 链接 |
|------|------|
| Clash for Windows | [clashforwindows.site](https://clashforwindows.site) |
| Clash 资源站 | [flclash.us](https://flclash.us) |
| Android 教程 | [clashmi.site](https://clashmi.site) |
| Xray 官方文档 | [xtls.github.io](https://xtls.github.io) |

---

## 📜 免责声明

本仓库仅供技术学习交流使用，请遵守当地法律法规。

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/flclash-us">flclash-us</a>
</p>