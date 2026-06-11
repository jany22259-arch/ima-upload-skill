# ima-upload-skill

> 在 WorkBuddy 里一句话把网页、PDF、HTML 上传到腾讯 IMA 知识库。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform: WorkBuddy](https://img.shields.io/badge/Platform-WorkBuddy-6c5ce7)](https://workbuddy.ai)
[![Skills Standard](https://img.shields.io/badge/Skills-Agent%20Skills%20Standard-00b894)](https://agentskills.io)

---

## Quick Start · 快速开始

### 安装 · Install

在 WorkBuddy 里说一句话：

```
帮我安装这个 skill：https://github.com/jany22259-arch/ima-upload-skill
```

或从 [Releases](https://github.com/jany22259-arch/ima-upload-skill/releases) 下载 `ima-upload.skill` 手动导入。

**前置依赖：**

1. 在 WorkBuddy 市场搜索安装「腾讯ima」技能
2. 配置 IMA API 凭证：[https://ima.qq.com/agent-interface](https://ima.qq.com/agent-interface)

### 使用 · Use

配置完直接说：

```
上传到ima https://example.com/article
```

```
把这个PDF放入ima知识库
```

---

## Why This Exists · 为什么做这个

IMA API 有两个硬限制：**不支持创建文件夹**、**不支持直接上传 HTML 文件**。

每次上传资料需要手动走 `create_media → COS 上传 → add_knowledge` 三步，HTML 还得先渲染成 PDF。

这个 skill 把上述流程封装成一句话。踩过的坑都沉淀在「避坑经验」里，不重复踩。

---

## Features · 功能

| 功能 | 说明 |
|---|---|
| 网页 URL 导入 | 一句话把网页添加到知识库 |
| 文件上传 | PDF / Word / PPT / Excel / 图片，自动走完整上传链路 |
| HTML 转 PDF | Playwright 自动渲染，完美保留样式 |
| 坑位沉淀 | 实战验证的 4 个关键踩坑经验 |

---

## Trigger Phrases · 触发词

| 中文触发 | 示例 |
|---|---|
| 上传到ima | 上传到ima 这篇文章 https://... |
| 放入ima知识库 | 把这个PDF放入ima知识库 |
| 添加到ima | 添加到ima 这个HTML文档 |
| ima导入 | ima导入 这页微信文章 |
| ima上传 | ima上传 这份报告 |
| 把文件存到ima | 把这个Excel存到ima |

---

## Use Cases · 使用场景

### 网页存档

```
上传到ima https://mp.weixin.qq.com/s/xxxxx
```

### PDF 入库

```
把这份CAIE考纲解析放入ima知识库
```

### HTML 转 PDF 上传

```
把这个HTML学习页面添加到ima
```

### 批量文件导入

```
把这三个Excel报表ima导入到「财务数据」文件夹
```

---

## Installation · 安装方式

### 方式一：一句安装（推荐）

在 WorkBuddy 中说：

```
帮我安装这个 skill：https://github.com/jany22259-arch/ima-upload-skill
```

### 方式二：.skill 下载

从 [GitHub Releases](https://github.com/jany22259-arch/ima-upload-skill/releases) 下载最新 `.skill` 文件导入。

### 方式三：手动安装

```bash
git clone https://github.com/jany22259-arch/ima-upload-skill.git ~/.workbuddy/skills/ima-upload-skill
```

---

## Dependencies · 依赖

| 依赖 | 说明 |
|---|---|
| WorkBuddy | codebuddy.cn 平台 |
| 腾讯ima 技能 | skill_2053082144792322048（WorkBuddy 市场安装） |
| IMA OpenAPI 凭证 | 在 [ima.qq.com/agent-interface](https://ima.qq.com/agent-interface) 配置 |
| Playwright | HTML 转 PDF 功能需要 |

---

## Known Pitfalls · 避坑经验

在实践中发现并解决的关键问题，沉淀于此避免重复踩坑：

| 问题 | 解决方案 |
|---|---|
| kb_id 必须用 base64 encoded 格式 | MCP 返回的数字 ID 不能直接用于 REST API |
| 根目录导入省略 folder_id | 传了 folder_id 会报 222000 错误 |
| PowerShell 5.1 中文 JSON 乱码 | 改用 Python subprocess 处理 |
| Windows 上 weasyprint 缺 GTK 库 | HTML→PDF 改用 Playwright + Python |

---

## Troubleshooting · 排障

| 错误 | 原因 | 解决 |
|---|---|---|
| 上传失败 222000 | 传了 folder_id 到根目录 | 去掉 folder_id 参数 |
| kb_id 无效 | 用了数字 ID | 改用 base64 encoded kb_id |
| 中文文件名乱码 | PowerShell 5.1 编码问题 | 用 Python subprocess 调用 API |
| HTML 上传渲染异常 | weasyprint 缺 GTK | 改用 Playwright 渲染 |
| 前置依赖未安装 | 缺少腾讯ima 技能 | WorkBuddy 市场搜索安装 |

---

## Compatible Platforms · 兼容

| 平台 | 状态 |
|---|---|
| WorkBuddy | ✅ 原生支持 |
| Claude Code | ✅ 兼容 |
| 其他支持 Agent Skills 的平台 | ✅ 理论兼容 |

---

## Project Structure · 项目结构

```
ima-upload-skill/
├── README.md
├── LICENSE
└── ima-upload.skill
```

---

## License · 许可证

MIT — 详见 [LICENSE](LICENSE)。

---

问题或建议 → [GitHub Issues](https://github.com/jany22259-arch/ima-upload-skill/issues)
