# CVE漏洞信息自动化拉取与筛选脚本

## 功能简介

这是一个Python脚本，用于自动从美国国家漏洞数据库(NVD)获取最新的CVE漏洞信息，并根据自定义条件进行筛选和格式化输出。

### 主要功能：
1. **自动获取CVE数据**：从NVD API获取指定时间范围内的CVE漏洞信息
2. **智能筛选**：根据CVSS评分和关键词对漏洞进行筛选
3. **格式化输出**：以清晰易读的格式在控制台显示结果
4. **结果导出**：支持将筛选结果导出为JSON文件
5. **自定义配置**：支持自定义查询天数、CVSS阈值和关键词

## 环境要求

### Python版本
- Python 3.6 或更高版本

### 依赖库
```bash
pip install requests
安装与使用
1. 安装依赖
bash
pip install -r requirements.txt
如果使用基本安装：

bash
pip install requests
2. 运行脚本
基本用法（默认查询过去7天，CVSS≥7.0）：
bash
python cve_fetcher.py
自定义查询天数：
bash
# 查询过去30天的CVE数据
python cve_fetcher.py --days 30
自定义CVSS评分阈值：
bash
# 只显示CVSS≥8.0的漏洞
python cve_fetcher.py --min-cvss 8.0
导出结果为JSON文件：
bash
# 查询并将结果导出为JSON文件
python cve_fetcher.py --export-json
自定义关键词：
bash
# 添加自定义关键词
python cve_fetcher.py --keywords "zeroday,heap overflow,use after free"
组合参数：
bash
# 查询过去14天，CVSS≥7.5，并导出结果
python cve_fetcher.py --days 14 --min-cvss 7.5 --export-json
脚本配置
默认关键词列表
脚本内置了常见的高危漏洞关键词，包括：

Remote Code Execution / RCE

SQL Injection

Privilege Escalation

Buffer Overflow

Cross-Site Scripting / XSS

Command Injection

Authentication Bypass

输出格式
脚本会以不同颜色显示不同风险等级的漏洞：

红色：严重漏洞（CVSS ≥ 9.0）

黄色：高危漏洞（CVSS 7.0-8.9）

绿色：中危漏洞（CVSS < 7.0）

输出示例
text
===============================================================================
[高危漏洞] CVE-2023-XXXXX | CVSS v3.1: 8.8 | 发布日期: 2023-10-15
匹配关键词: remote code execution
漏洞类型: CWE-78: Improper Neutralization of Special Elements used in an OS Command
描述: A remote code execution vulnerability exists in...
-------------------------------------------------------------------------------

[严重漏洞] CVE-2023-YYYYY | CVSS v3.1: 9.8 | 发布日期: 2023-10-14
匹配关键词: sql injection
描述: A SQL injection vulnerability allows attackers to...
注意事项
API限制：NVD API有速率限制（建议每分钟不超过10次请求），脚本已内置延时处理

网络要求：需要能够访问NVD API（https://services.nvd.nist.gov）

数据更新：NVD数据库通常每天更新一次

关键词匹配：关键词匹配不区分大小写

错误处理：脚本包含基本的错误处理和重试机制

故障排除
常见问题：
连接超时：

检查网络连接

尝试增加超时时间（修改脚本中的timeout参数）

API限制错误：

脚本会自动等待并重试

如果需要更频繁的查询，可以考虑申请NVD API密钥

无结果显示：

可能是该时间段内没有符合条件的漏洞

尝试增加查询天数或降低CVSS阈值

检查关键词是否匹配

文件结构
text
cve-automation-script/
├── cve_fetcher.py    # 主脚本文件
├── README.md         # 说明文档
└── requirements.txt  # 依赖库列表（可选）
许可证
本项目仅供学习和安全研究使用，请遵守相关法律法规。

更新日志
v1.0 (2024-01) - 初始版本

实现基本CVE数据获取功能

添加CVSS评分和关键词筛选

支持结果导出为JSON

添加命令行参数支持

text

### 3. `requirements.txt`（可选）

```txt
requests>=2.28.0
使用说明
快速开始：
创建一个新文件夹，将上述三个文件放入其中

安装依赖：

bash
pip install requests
运行脚本：

bash
python cve_fetcher.py
主要特性：
自动化获取：自动从NVD API获取最新CVE数据

智能筛选：

基于CVSS评分（默认≥7.0）

基于关键词匹配（可自定义）

美观输出：

彩色终端输出

风险等级分类

详细统计信息

灵活配置：

可调整查询天数

可修改CVSS阈值

可自定义关键词

数据导出：支持JSON格式导出

高级用法：
bash
# 完整示例：查询过去30天CVSS≥8.0的漏洞，添加自定义关键词，并导出结果
python cve_fetcher.py --days 30 --min-cvss 8.0 --keywords "zeroday,memory corruption" --export-json# CVE
