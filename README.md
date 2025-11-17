<div align="center">

# 🛡️ YinVulKiller

**企业级漏洞扫描与资产测绘平台**

[![Version](https://img.shields.io/badge/version-1.3.0-blue.svg)](https://github.com/taielab/YinVulKiller)
[![Go Version](https://img.shields.io/badge/Go-1.19+-00ADD8.svg)](https://golang.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/taielab/YinVulKiller?style=social)](https://github.com/taielab/YinVulKiller/stargazers)

**开发者**: [AI安全工坊](https://github.com/taielab) | **微信公众号**: AI安全工坊

<img src="https://img.shields.io/badge/POC库-12492+-red.svg" alt="POC Count"/>
<img src="https://img.shields.io/badge/指纹库-6400+-orange.svg" alt="Fingerprint Count"/>
<img src="https://img.shields.io/badge/弱口令-40+-yellow.svg" alt="Weak Password"/>

</div>

---

## 📖 简介

**YinVulKiller** 是一款功能强大的企业级漏洞扫描与资产测绘工具，集成了主机存活探测、端口扫描、服务识别、指纹识别、漏洞检测、弱口令爆破等多种功能。

### 🎯 核心特性

- 🚀 **三引擎 POC 检测**：集成 Xray + Nuclei + GoPOC 三大引擎，12,492+ POC 规则
- 🔍 **深度服务识别**：基于 Gonmap/Nmap 探针库，6000+ 服务指纹
- 🌐 **全面资产扫描**：支持 IP/CIDR/URL 多种目标格式，智能并发调度
- 📂 **目录扫描模块**：内置双字典（31,094 + 1,613 条路径），快速发现隐藏目录
- 🎨 **多格式报告**：Excel/HTML 双格式报告，自动截图，可视化展示
- 🔐 **40+ 弱口令模块**：覆盖 SSH、RDP、MySQL、PostgreSQL 等主流服务
- 🧩 **640+ 指纹规则**：精准识别 Web 框架、中间件、CMS 系统
- 🌍 **内网穿透**：Spy 网段探测 + 代理支持，适配复杂网络环境
- 📦 **POC 外部化管理**：支持自定义 POC 规则，无需重新编译

---

## ✨ 核心优势

### 1. 🎯 强大的 POC 检测能力

| 引擎 | POC 数量 | 特点 |
|------|----------|------|
| **Xray** | 911+ | 高精度漏洞检测，支持自定义 YAML 规则 |
| **Nuclei** | 11,581+ | 社区驱动，覆盖最新 CVE |
| **GoPOC** | 基于指纹 | 自动匹配指纹执行相应 POC |

**总计**: **12,492+ POC 规则** 🔥

### 2. 🔍 精准的服务识别

- **Gonmap 深度识别**：基于 Nmap 探针库，6000+ 服务指纹
- **Web 指纹识别**：27000+ Web 组件指纹（框架、CMS、中间件）
- **协议自动识别**：自动判断 HTTP/HTTPS/SSH/RDP/MySQL 等协议
- **📌 新增协议支持**：Cassandra、Kafka、Neo4j、Elasticsearch、Memcached、LDAP（11个端口映射）

### 3. 🚀 高性能并发架构

- **智能并发调度**：根据 CPU 核心数和目标规模动态调整
- **分布式引擎**：Nuclei 引擎支持分布式任务，避免资源冲突
- **上下文超时控制**：防止扫描卡死，自动超时清理

### 4. 🌍 复杂网络支持

- **Spy 网段探测**：极速 B 段扫描，发现内网存活网段
- **代理支持**：HTTP/SOCKS5 代理，穿透防火墙
- **内网穿透**：支持内网到外网的扫描场景

---

## 🚀 快速开始

### 基础扫描示例

```bash
# 1. 快速扫描单个主机（TOP100 端口）
./yinvulkiller scan -i 192.168.1.1 -p top100

# 2. 扫描整个 C 段（TOP500 端口）
./yinvulkiller scan -i 192.168.1.0/24 -p top500 --noping

# 3. 扫描指定 URL
./yinvulkiller scan -u https://example.com

# 4. 批量扫描 URL 文件
./yinvulkiller scan --urlfile urls.txt

# 5. 使用 Nuclei 引擎深度扫描
./yinvulkiller scan -u http://target.com --engine nuclei

# 6. 使用代理扫描
./yinvulkiller scan -i 8.8.8.8 -p top100 --proxy http://127.0.0.1:8080
```

---

## 📚 功能详解

### 🔍 扫描模式

#### 1. 资产扫描模式
```bash
# 快速资产探测（不进行漏洞和弱口令扫描）
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --nopoc --nocrack --noimg
```

#### 2. 全面漏洞扫描
```bash
# 启用所有检测模块
./yinvulkiller scan -i 192.168.1.0/24 -p top500 --deep-scan
```

#### 3. 数据库专项扫描
```bash
# 仅扫描数据库端口 + 弱口令爆破
./yinvulkiller scan -i 192.168.1.0/24 --dbs
```

#### 4. Web 应用扫描
```bash
# 仅扫描 Web 端口 + POC 检测 + 截图
./yinvulkiller scan -i 192.168.1.0/24 --web
```

#### 5. 高危端口扫描
```bash
# 仅扫描高危端口（SSH/RDP/MySQL/Redis等）
./yinvulkiller scan -i 192.168.1.0/24 --risk
```

#### 6. 目录扫描模式

YinVulKiller 内置专业目录扫描功能，支持双字典选择：

```bash
# 使用默认字典（31,094 条路径）
./yinvulkiller dirsearch -u http://example.com

# 使用高危字典（1,613 条高风险路径）⭐ 推荐
./yinvulkiller dirsearch -u http://example.com --dict-type high

# 自定义字典
./yinvulkiller dirsearch -u http://example.com -f custom.txt

# 高级参数：并发、状态码过滤、代理
./yinvulkiller dirsearch -u http://example.com --dict-type high \
  -c 100 --code "200,403,500" \
  -p socks5://127.0.0.1:1080

# 指定输出格式（默认: txt,json）
./yinvulkiller dirsearch -u http://example.com -o html         # HTML 可视化报告
./yinvulkiller dirsearch -u http://example.com -o txt,csv,html # 多格式输出
./yinvulkiller dirsearch -u http://example.com -o all          # 所有格式
```

**输出格式**：
- 📄 **TXT** - 表格形式纯文本（推荐日常查看）
- 📊 **JSON** - 机器可读（API/脚本集成）
- 📑 **CSV** - Excel/WPS 打开（数据分析）
- 🌐 **HTML** - 浏览器查看（带样式、搜索、高亮）

**字典对比**：

| 字典类型                    | 路径数量     | 适用场景               |
| --------------------------- | ------------ | ---------------------- |
| 默认字典 (url.txt)          | 31,094 条    | 全面目录审计           |
| **高危字典 (url-high.txt)** | **1,613 条** | **快速发现高危路径** 🔥 |

### 🌍 内网探测（Spy 模式）

```bash
# 1. 探测所有内网段（10.x, 172.x, 192.168.x）
./yinvulkiller scan --spy all -p top100

# 2. 探测指定内网段
./yinvulkiller scan --spy 10 -p top500

# 3. 仅探测不扫描
./yinvulkiller scan --spy all --spy-only

# 4. 探测后自动扫描发现的主机
./yinvulkiller scan --spy 192 -p top1000
```

### 🎯 POC 引擎选择

```bash
# 1. 仅使用 Xray 引擎（速度快）
./yinvulkiller scan -u http://target.com --engine xray

# 2. 仅使用 Nuclei 引擎（规则全）
./yinvulkiller scan -u http://target.com --engine nuclei

# 3. 同时使用两个引擎（默认）
./yinvulkiller scan -u http://target.com --engine both

# 4. Nuclei 高级参数
./yinvulkiller scan -u http://target.com \
  --engine nuclei \
  --nuclei-tags cve,rce,sqli \
  --nuclei-severity critical,high \
  --nuclei-concurrency 50
```

### 🔐 弱口令检测

支持 **40+ 种服务** 的弱口令检测：

```bash
# 启用 RDP 弱口令扫描（注意账号锁定风险）
./yinvulkiller scan -i 192.168.1.0/24 --rdp

# 自定义字典
./yinvulkiller scan -i 192.168.1.0/24 \
  --userfile users.txt \
  --passwdfile passwords.txt
```

**⚠️ 智能去重保障**：最新版本已实现账户级去重机制，每个账户只记录首个成功密码，避免重复结果！

**支持的服务**：
- **远程访问**: SSH, RDP, Telnet, VNC
- **数据库**: MySQL, PostgreSQL, Oracle, MSSQL, MongoDB, Redis, Memcached, **Cassandra**, **Neo4j**, **Elasticsearch**
- **SMB 协议**: SMB v1 (445), SMB 2.0/2.1/3.0/3.1.1 (445) - **智能双版本认证**
- **消息队列**: **RabbitMQ**, **Kafka**, **ActiveMQ**
- **Web 服务**: Tomcat, WebLogic, JBoss, Zabbix, Grafana
- **邮件协议**: SMTP, IMAP, POP3
- **其他**: FTP, SNMP, **LDAP**, Rsync, Modbus

---

## 📊 POC 管理

### POC 外部化架构

YinVulKiller 支持 **POC 外部化管理**，允许用户自由添加/删除/修改 POC 规则，**无需重新编译**！

```
pocs/
├── xray/          # 911+ Xray POC 规则（YAML 格式）
│   ├── CVE-2021-44228-log4j.yaml
│   ├── Shiro-550.yaml
│   └── ...
└── nuclei/        # 11,581+ Nuclei 模板
    ├── http/
    │   ├── cves/
    │   ├── vulnerabilities/
    │   └── ...
    ├── dns/
    ├── network/
    └── ...
```

### 自定义 POC

#### 1. 添加 Xray POC
```bash
# 添加自定义 POC 到 Xray 引擎
cp my-custom-poc.yaml pocs/xray/

# 重启扫描即可生效
./yinvulkiller scan -u http://target.com
```

#### 2. 添加 Nuclei 模板
```bash
# 添加 Nuclei 模板
cp my-nuclei-template.yaml pocs/nuclei/http/vulnerabilities/

# 使用特定标签过滤
./yinvulkiller scan -u http://target.com --nuclei-tags custom
```

#### 3. 删除不需要的 POC
```bash
# 删除单个 POC
rm pocs/xray/unwanted-poc.yaml

# 删除整个类别（例如移除 headless 模板）
rm -rf pocs/nuclei/headless/
```

---

## 🎨 报告输出

扫描完成后自动生成以下报告：

```
ScanLog/
├── 202511081000-YinVulKiller.xlsx    # Excel 格式详细报告
├── 202511081000-YinVulKiller.html    # HTML 格式可视化报告
└── WebScreenshot/
    └── 202511081000/                 # Web 截图目录
        ├── http_192.168.1.1_80.png
        └── https_example.com_443.png
```

### 报告内容

- ✅ **存活主机列表**：IP、端口、服务、操作系统
- ✅ **漏洞详情**：CVE 编号、严重程度、POC 信息、HTTP 请求/响应
- ✅ **弱口令列表**：服务、用户名、密码
- ✅ **指纹识别**：Web 框架、CMS、中间件版本
- ✅ **Web 截图**：自动截图存档

---

## 🛠️ 高级参数

### 并发控制

```bash
# 调整并发速率（默认 0.8）
./yinvulkiller scan -i 192.168.1.0/24 -p top500 --chan 1.5

# Nuclei 并发参数
./yinvulkiller scan -u http://target.com \
  --nuclei-concurrency 50 \          # 模板并发数
  --nuclei-host-concurrency 10 \     # 主机并发数
  --nuclei-rate-limit 300            # 速率限制（请求/秒）
```

### 超时控制

```bash
# 设置单次请求超时（默认 5 秒）
./yinvulkiller scan -i 192.168.1.1 -t 10

# 设置整体扫描最长时间（默认 10 分钟）
./yinvulkiller scan -i 192.168.1.0/24 --done 30

# Gonmap 服务识别超时
./yinvulkiller scan -i 192.168.1.1 --gonmap-timeout 3
```

### 端口预设

```bash
# TOP100：最常见的 100 个端口（速度快）
./yinvulkiller scan -i 192.168.1.0/24 -p top100

# TOP500：500 个常用端口（平衡）
./yinvulkiller scan -i 192.168.1.0/24 -p top500

# TOP1000：1000 个扩展端口（全面）
./yinvulkiller scan -i 192.168.1.0/24 -p top1000

# 快速扫描：精简的高危端口
./yinvulkiller scan -i 192.168.1.0/24 -p quick

# 自定义端口
./yinvulkiller scan -i 192.168.1.1 -p 80,443,8080,3306,3389
```

### 排除目标

```bash
# 排除指定端口
./yinvulkiller scan -i 192.168.1.0/24 -p top500 -e 80,443

# 排除指定 IP（通过文件）
echo "192.168.1.254" > exclude.txt
./yinvulkiller scan -i 192.168.1.0/24 --excludeip exclude.txt
```

---

## 📝 完整参数列表

### 扫描参数

| 参数 | 说明 | 示例 |
|------|------|------|
| `-i, --ip` | 扫描 IP/CIDR/范围 | `-i 192.168.1.1-100` |
| `-p, --port` | 端口（支持预设） | `-p top500` |
| `-u, --url` | 单个 URL | `-u https://example.com` |
| `--urlfile` | URL 文件 | `--urlfile urls.txt` |
| `--ipfile` | IP 文件 | `--ipfile targets.txt` |
| `-x, --proxy` | HTTP/SOCKS 代理 | `-x http://127.0.0.1:8080` |
| `-t, --time` | 超时时间（秒） | `-t 10` |

### 扫描模式

| 参数 | 说明 |
|------|------|
| `--web` | 仅扫描 Web 端口 |
| `--dbs` | 仅扫描数据库端口 |
| `--risk` | 仅扫描高危端口 |
| `--deep-scan` | 启用 Gonmap 深度识别 |

### 功能开关

| 参数 | 说明 |
|------|------|
| `--noping` | 禁用 Ping 检测 |
| `--nopoc` | 禁用 POC 扫描 |
| `--nocrack` | 禁用弱口令扫描 |
| `--noimg` | 禁用 Web 截图 |
| `--no-browser` | 禁止自动打开浏览器 |

### POC 引擎参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--engine` | 引擎选择（xray/nuclei/both） | both |
| `--xray-poc-name` | Xray POC 名称过滤 | - |
| `--xray-concurrency` | Xray POC 并发数 | 10 |
| `--nuclei-tags` | Nuclei 标签过滤 | - |
| `--nuclei-severity` | Nuclei 严重程度 | - |
| `--nuclei-exclude-tags` | Nuclei 排除标签 | - |
| `--nuclei-exclude-severity` | Nuclei 排除严重程度 | - |
| `--nuclei-concurrency` | Nuclei 模板并发数 | 25 |
| `--nuclei-rate-limit` | Nuclei 速率限制 | 150 |

### Spy 探测参数

| 参数 | 说明 |
|------|------|
| `--spy` | 网段探测（all/10/172/192/IP） |
| `--spy-only` | 仅探测不扫描 |

### 其他参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--chan` | 并发增长速率 | 0.8 |
| `--done` | 整体扫描最长时间（分钟） | 10 |
| `--random` | 打乱主机顺序 | - |
| `--rdp` | 启用 RDP 弱口令扫描 | - |
| `--outname` | 指定输出报告名称 | 时间戳 |
| `--userfile` | 自定义用户字典 | - |
| `--passwdfile` | 自定义密码字典 | - |

---

## 💡 实战场景

### 场景 1：内网资产发现
```bash
# 使用 Spy 探测所有内网段，发现存活主机
./yinvulkiller scan --spy all -p top100 --nopoc --nocrack
```

### 场景 2：Web 应用漏洞挖掘
```bash
# 使用 Nuclei 引擎深度扫描 Web 应用
./yinvulkiller scan -u https://target.com \
  --engine nuclei \
  --nuclei-tags cve,rce,sqli,xss \
  --nuclei-severity critical,high
```

### 场景 3：数据库渗透测试
```bash
# 扫描数据库端口 + 弱口令爆破
./yinvulkiller scan -i 192.168.1.0/24 --dbs \
  --userfile users.txt \
  --passwdfile passwords.txt
```

### 场景 4：外网代理扫描
```bash
# 通过代理扫描外网目标
./yinvulkiller scan -i target.com -p top500 \
  --proxy socks5://127.0.0.1:1080
```

### 场景 5：快速 C 段探测
```bash
# 仅进行端口扫描和服务识别，不进行漏洞检测
./yinvulkiller scan -i 192.168.1.0/24 -p top100 \
  --noping --nopoc --nocrack --deep-scan
```

### 场景 6：FOFA 联动扫描
```bash
# 调用 FOFA API 获取目标并扫描
./yinvulkiller scan --fofa 'title="login"' --fofasize 500 -p top100
```

### 场景 7：Web 目录扫描
```bash
# 快速高危检测（推荐）
./yinvulkiller dirsearch -u https://target.com --dict-type high -c 100

# 全面目录审计
./yinvulkiller dirsearch -u https://target.com --dict-type default -c 50

# 低调扫描避免 WAF
./yinvulkiller dirsearch -u https://target.com --dict-type high \
  -c 10 --wait 2 -t 10

# 输出 HTML 报告（浏览器可视化查看）
./yinvulkiller dirsearch -u https://target.com --dict-type high -o html

# 输出所有格式（TXT/JSON/CSV/HTML）
./yinvulkiller dirsearch -u https://target.com --dict-type high -o all
```

**查看结果**：
```bash
cat dirScan.txt        # 纯文本查看
open dirScan.html      # 浏览器可视化（推荐）
open dirScan.csv       # Excel 分析
```

**适用于**：
- 敏感文件/目录发现
- 配置文件泄露检测
- 备份文件探测
- 管理后台发现

---

## 🔥 技术亮点

### 1. 多引擎协同架构
- **Xray**：高精度、低误报，适合生产环境
- **Nuclei**：社区驱动、覆盖最新 CVE
- **GoPOC**：基于指纹智能匹配

### 2. 分布式引擎管理
- 每个任务独立引擎，避免资源冲突
- 上下文超时控制，自动清理
- 线程安全设计，支持高并发

### 3. POC 外部化管理
- YAML 格式 POC，易于编写和维护
- 无需重新编译，即时生效
- 支持社区规则导入

### 4. 智能并发调度
- 根据 CPU 核心数动态调整
- 速率限制防止 DDoS 误触发
- 分阶段并发：端口扫描 → 服务识别 → POC 检测

### 5. 全面报告系统
- Excel + HTML 双格式
- 自动截图存档
- 可视化漏洞统计

---

## ⚠️ 免责声明

**本工具仅用于经授权的安全测试！**

- ✅ 允许用于：企业授权的渗透测试、安全加固、合规检查
- ❌ 禁止用于：未授权的漏洞扫描、网络攻击、数据窃取

**使用本工具造成的任何法律责任，均由使用者自行承担，与软件作者无关。**

---

## 🔄 最近更新

### Version 2.0.0 (2025-11)

**🚀 重大更新**：
- 🔥 **新增 SMB2/SMB3 协议支持** - 完整支持 SMB 2.0/2.1/3.0/3.1.1 协议弱口令扫描
  - 使用 `projectdiscovery/go-smb2` 库实现
  - 智能双版本认证：自动尝试 SMB v1 和 SMB2/SMB3
  - 管理员权限验证（C$ 共享挂载测试）
  - 账户锁定检测与保护机制
  - 共享枚举功能
- 🛡️ **新增 SMBGhost (CVE-2020-0796) 漏洞检测** - 自动检测 Windows 10 1903/1909 远程代码执行漏洞
  - 被动检测，不触发漏洞利用
  - 445 端口自动检测
  - 精准协议协商分析

**💡 技术亮点**：
- ✅ SMB v1 和 SMB2/SMB3 双版本并行认证，兼容所有 Windows 版本
- ✅ Windows 10 1709+ 默认禁用 SMBv1，SMB2/SMB3 成为主流
- ✅ 去重机制确保每个账户只记录首个成功密码

**🐛 Bug修复**：

- ✅ 修复弱口令扫描去重问题 - 每个账户只记录首个成功密码
- ✅ 修复Rsync服务弱口令扫描未生效的问题
- ✅ 优化服务识别逻辑，提升准确性

**✨ 新增功能**：
- 📌 新增 6 种协议支持：Cassandra、Kafka、Neo4j、Elasticsearch、Memcached、LDAP
- 📌 新增 11 个端口映射，提升协议识别覆盖率
- 📖 新增快速开始指南（QUICKSTART.md）- 5分钟快速上手

**🔧 优化改进**：
- ⚡ 优化弱口令扫描性能和稳定性
- ⚡ 完善服务协议识别机制
- 📝 完善项目文档和使用说明

---

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

### 如何贡献

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

### 贡献方向

- 🐛 Bug 修复
- ✨ 新功能开发
- 📝 文档完善
- 🎯 POC 规则贡献
- 🔍 指纹规则补充

---

## 📞 联系我们

- **GitHub**: [https://github.com/taielab](https://github.com/taielab)
- **微信公众号**: AI安全工坊

![wxgzh](./images/wxgzh.png)

---

## 📄 开源许可

本项目采用 **MIT License** 开源协议。

---

## 🎉 致谢

感谢以下开源项目的支持：

- [Nuclei](https://github.com/projectdiscovery/nuclei) - 强大的漏洞扫描引擎
- [Xray](https://github.com/chaitin/xray) - 长亭科技的安全评估工具
- [Gonmap](https://github.com/lair-framework/go-nmap) - Go 语言 Nmap 扫描器
- [Fscan](https://github.com/shadow1ng/fscan) - 内网综合扫描工具
- [Golin](https://github.com/selinuxG/Golin) - 内网综合扫描工具

---

<div align="center">

**⭐ 如果这个项目对你有帮助，请给个 Star！⭐**

Made with ❤️ by [AI安全工坊](https://github.com/taielab)

</div>
