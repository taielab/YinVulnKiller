# 🚀 YinVulKiller 快速入门指南

> **企业级漏洞扫描与资产测绘平台 - 5分钟快速上手**

## 🎯 核心能力

| 功能 | 数量 | 说明 |
|------|------|------|
| 🔍 **POC引擎** | 4个引擎 | Nuclei (11,581+) + Xray (911+) + GoPOC + YamlPOC (562+) |
| 📊 **总POC数量** | **13,054+** | 覆盖最新CVE和常见漏洞 |
| 🌐 **Web指纹** | 640+ | 精准识别框架、CMS、中间件 |
| 🔐 **弱口令模块** | 40+ | SSH/RDP/MySQL/Redis等主流服务 |
| 📂 **目录扫描** | 32,707条路径 | 默认字典31,094 + 高危字典1,613 |
| ⚡ **扫描性能** | 35-70倍提速 | Worker Pool并发架构 + 批量扫描优化 |

---

## ⚡ 3秒快速扫描

```bash
# 🔥 最常用：扫描单个网站（全引擎检测）
./yinvulkiller scan -u http://target.com --engines all

# 🌐 内网C段扫描（TOP100端口）
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --noping

# 🎯 高危端口快速探测
./yinvulkiller scan -i 192.168.1.0/24 --risk

# 📂 目录扫描（高危字典）
./yinvulkiller dirsearch -u http://target.com --dict-type high
```

---

## 📖 基础使用

### 1️⃣ 扫描单个目标

```bash
# 基础扫描（自动选择引擎）
./yinvulkiller scan -u https://example.com

# 指定引擎扫描
./yinvulkiller scan -u https://example.com --engines nuclei,xray,yamalpoc

# 使用所有引擎（推荐）
./yinvulkiller scan -u https://example.com --engines all
```

### 2️⃣ 批量扫描

```bash
# 扫描URL列表文件
./yinvulkiller scan --urlfile targets.txt --engines all

# 扫描IP段（TOP500端口）
./yinvulkiller scan -i 192.168.1.0/24 -p top500

# 扫描IP范围
./yinvulkiller scan -i 192.168.1.100-200 -p top100
```

### 3️⃣ POC引擎选择

```bash
# 🚀 Nuclei引擎（11,581+ POC，社区驱动，覆盖最新CVE）
./yinvulkiller scan -u http://target.com --engines nuclei --nuclei-severity critical,high

# ⚡ Xray引擎（911+ POC，高精度，适合生产环境）
./yinvulkiller scan -u http://target.com --engines xray

# 🎯 GoPOC引擎（基于指纹智能匹配）
./yinvulkiller scan -u http://target.com --engines gopoc

# 📝 YamlPOC引擎（562+ YAML POC，含110个自动转换旧格式）
./yinvulkiller scan -u http://target.com --engines yamalpoc

# 🔥 使用所有引擎（推荐，最全面）
./yinvulkiller scan -u http://target.com --engines all
```

### 4️⃣ 目录扫描

```bash
# 使用高危字典（1,613条，推荐）⭐
./yinvulkiller dirsearch -u http://target.com --dict-type high

# 使用默认字典（31,094条，全面扫描）
./yinvulkiller dirsearch -u http://target.com --dict-type default

# 指定并发数
./yinvulkiller dirsearch -u http://target.com --dict-type high -c 100

# 输出HTML报告（浏览器可视化）
./yinvulkiller dirsearch -u http://target.com --dict-type high -o html
```

---

## 🎨 扫描模式

### 资产探测模式（不检测漏洞）
```bash
# 快速探测存活主机和端口
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --nopoc --nocrack --noimg
```

### 仅Web扫描
```bash
# 只扫描Web端口（80/443/8080等）
./yinvulkiller scan -i 192.168.1.0/24 --web
```

### 仅数据库扫描
```bash
# 只扫描数据库端口 + 弱口令
./yinvulkiller scan -i 192.168.1.0/24 --dbs
```

### 高危端口扫描
```bash
# 仅扫描SSH/RDP/MySQL/Redis等高危服务
./yinvulkiller scan -i 192.168.1.0/24 --risk
```

### 深度扫描模式
```bash
# 启用Gonmap深度服务识别
./yinvulkiller scan -i 192.168.1.0/24 -p top500 --deep-scan
```

---

## 🔍 内网探测（Spy模式）

```bash
# 探测所有内网段（10.x, 172.x, 192.168.x）
./yinvulkiller scan --spy all -p top100

# 仅探测10.x网段
./yinvulkiller scan --spy 10 -p top500

# 仅探测不扫描
./yinvulkiller scan --spy all --spy-only

# 探测后自动扫描发现的存活主机
./yinvulkiller scan --spy 192 -p top1000
```

---

## 🔐 弱口令检测

### 支持的服务（40+）

- **远程访问**: SSH, RDP, Telnet, VNC
- **数据库**: MySQL, PostgreSQL, Oracle, MSSQL, MongoDB, Redis, Memcached
- **Web服务**: Tomcat, WebLogic, JBoss, Zabbix, Grafana
- **其他**: FTP, SMB, SNMP, LDAP 等

### 使用示例

```bash
# 启用RDP弱口令扫描（注意账号锁定风险）
./yinvulkiller scan -i 192.168.1.0/24 --rdp

# 自定义字典
./yinvulkiller scan -i 192.168.1.0/24 \
  --userfile users.txt \
  --passwdfile passwords.txt

# 仅扫描数据库 + 弱口令
./yinvulkiller scan -i 192.168.1.0/24 --dbs
```

---

## 🎯 Nuclei引擎高级用法

### 按严重程度过滤
```bash
# 仅扫描严重和高危漏洞
./yinvulkiller scan -u http://target.com \
  --engines nuclei \
  --nuclei-severity critical,high
```

### 按标签过滤
```bash
# 仅扫描CVE、RCE、SQL注入
./yinvulkiller scan -u http://target.com \
  --engines nuclei \
  --nuclei-tags cve,rce,sqli
```

### 性能调优
```bash
# 调整并发参数（适合高性能服务器）
./yinvulkiller scan -u http://target.com \
  --engines nuclei \
  --nuclei-concurrency 50 \
  --nuclei-rate-limit 300
```

---

## 📊 扫描报告

扫描完成后自动生成：

```
ScanLog/
├── 202511101234-YinVulKiller.xlsx    # Excel详细报告
├── 202511101234-YinVulKiller.html    # HTML可视化报告
└── WebScreenshot/                    # Web截图目录
    └── 202511101234/
        ├── http_192.168.1.1_80.png
        └── https_example.com_443.png
```

### 报告内容

- ✅ **实时漏洞输出**：发现漏洞时立即显示在终端
- ✅ **存活主机列表**：IP、端口、服务、操作系统
- ✅ **漏洞详情**：CVE编号、严重程度、POC信息、HTTP请求/响应
- ✅ **弱口令列表**：服务、用户名、密码
- ✅ **指纹识别**：Web框架、CMS、中间件版本
- ✅ **Web截图**：自动截图存档

---

## 🛠️ 常用参数

### 并发控制
```bash
# 调整并发速率（默认0.8）
./yinvulkiller scan -i 192.168.1.0/24 -p top500 --chan 1.5

# Nuclei并发参数
./yinvulkiller scan -u http://target.com \
  --engines nuclei \
  --nuclei-concurrency 50 \
  --nuclei-rate-limit 300
```

### 超时控制
```bash
# 单次请求超时（默认5秒）
./yinvulkiller scan -i 192.168.1.1 -t 10

# 整体扫描最长时间（默认10分钟）
./yinvulkiller scan -i 192.168.1.0/24 --done 30
```

### 端口预设
```bash
# TOP100：最常见的100个端口（速度快）⚡
./yinvulkiller scan -i 192.168.1.0/24 -p top100

# TOP500：500个常用端口（平衡）✅
./yinvulkiller scan -i 192.168.1.0/24 -p top500

# TOP1000：1000个扩展端口（全面）🔍
./yinvulkiller scan -i 192.168.1.0/24 -p top1000

# Quick：精简的高危端口 🎯
./yinvulkiller scan -i 192.168.1.0/24 -p quick

# 自定义端口
./yinvulkiller scan -i 192.168.1.1 -p 80,443,8080,3306,3389
```

### 功能开关
```bash
# 禁用Ping检测（适合防火墙屏蔽ICMP的环境）
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --noping

# 禁用POC扫描（仅资产探测）
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --nopoc

# 禁用弱口令扫描
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --nocrack

# 禁用Web截图
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --noimg

# 禁用自动打开浏览器
./yinvulkiller scan -i 192.168.1.0/24 -p top100 --no-browser
```

---

## 💡 实战场景

### 场景1：外网单点渗透测试
```bash
# 使用所有引擎全面扫描
./yinvulkiller scan -u https://target.com --engines all

# Nuclei高危漏洞扫描
./yinvulkiller scan -u https://target.com \
  --engines nuclei \
  --nuclei-severity critical,high \
  --nuclei-tags cve,rce,sqli,xss
```

### 场景2：内网资产发现
```bash
# Spy探测所有内网段
./yinvulkiller scan --spy all -p top100 --nopoc --nocrack

# 扫描发现的C段
./yinvulkiller scan -i 192.168.1.0/24 -p top500 --noping
```

### 场景3：数据库渗透测试
```bash
# 扫描数据库端口 + 弱口令爆破
./yinvulkiller scan -i 192.168.1.0/24 --dbs \
  --userfile users.txt \
  --passwdfile passwords.txt
```

### 场景4：Web应用安全评估
```bash
# POC漏洞扫描 + 目录扫描
./yinvulkiller scan -u https://target.com --engines all
./yinvulkiller dirsearch -u https://target.com --dict-type high -o html
```

### 场景5：快速C段探测
```bash
# 仅端口扫描和服务识别
./yinvulkiller scan -i 192.168.1.0/24 -p top100 \
  --noping --nopoc --nocrack --deep-scan
```

### 场景6：代理扫描
```bash
# 通过SOCKS5代理扫描
./yinvulkiller scan -i target.com -p top500 \
  --proxy socks5://127.0.0.1:1080

# 通过HTTP代理扫描
./yinvulkiller scan -i target.com -p top500 \
  --proxy http://127.0.0.1:8080
```

---

## 🔥 性能优化亮点

### ⚡ 35-70倍扫描速度提升

**优化前**：88个目标串行扫描需要 **176-352分钟**

**优化后**：并发批量扫描仅需 **5-10分钟**

### 🚀 核心优化技术

1. **Worker Pool并发架构**
   - 多个目标同时扫描
   - 智能任务调度
   - 资源高效利用

2. **指纹分组批量扫描**
   - 相同指纹的目标合并扫描
   - 避免重复初始化
   - 大幅减少开销

3. **引擎并行执行**
   - 4个POC引擎同时运行
   - 独立上下文管理
   - 线程安全设计

4. **实时漏洞输出**
   - 发现漏洞立即显示
   - 无需等待扫描完成
   - 提升用户体验

---

## 🐛 故障排查

### 问题1：POC规则未加载
```bash
# 解决方案：检查pocs目录是否存在
ls -la pocs/

# 重新部署POC规则
./deploy_pocs.sh
```

### 问题2：扫描卡住不动
```bash
# 可能原因：目标防火墙或WAF拦截
# 解决方案：降低并发，增加超时

./yinvulkiller scan -i target.com -p top100 \
  --chan 0.5 \
  -t 10 \
  --nuclei-rate-limit 50
```

### 问题3：弱口令扫描导致账号锁定
```bash
# 解决方案：禁用RDP扫描或使用自定义字典
./yinvulkiller scan -i 192.168.1.0/24 --nocrack

# 使用精简字典
./yinvulkiller scan -i 192.168.1.0/24 \
  --userfile short-users.txt \
  --passwdfile short-passwords.txt
```

### 问题5：SMB扫描卡住
```bash
# 已修复：单任务超时控制（15秒）
# 如果仍然卡住，禁用SMB扫描
./yinvulkiller scan -i 192.168.1.0/24 -p top100 -e 445
```

---

## 📚 进一步学习

- 📖 **完整文档**: [README.md](README.md)
- 🎯 **POC管理**: 参考README.md的"POC管理"章节

---

## ⚠️ 注意事项

1. ⚡ **性能影响**：扫描会产生大量网络请求，注意服务器负载
2. 🔐 **弱口令风险**：RDP扫描可能导致账号锁定，生产环境慎用
3. 🌐 **网络合规**：仅在授权范围内使用，遵守法律法规
4. 📊 **日志审计**：所有扫描活动都会记录，保留证据

---

## 🤝 获取帮助

- **GitHub Issues**: [https://github.com/taielab/YinVulnKiller/issues](https://github.com/taielab/YinVulKiller/issues)
- **微信公众号**: AI安全工坊
- **完整文档**: [README.md](README.md)

---

<div align="center">

**⭐ 如果这个项目对你有帮助，请给个 Star！⭐**

Made with ❤️ by [AI安全工坊](https://github.com/taielab)

</div>
