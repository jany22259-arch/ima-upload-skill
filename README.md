# ima-upload — IMA 知识库上传技能

腾讯 IMA（ima.qq.com）知识库自动化上传技能，封装网页导入、文件上传、HTML 转 PDF 全流程。基于 WorkBuddy 技能生态。

## 安装

1. 在 WorkBuddy 市场搜索安装「腾讯ima」技能（前置依赖）
2. 配置 IMA API 凭证：https://ima.qq.com/agent-interface
3. 在 WorkBuddy 技能管理中导入 `ima-upload.skill`

## 功能

| 功能 | 说明 |
|------|------|
| 网页 URL 导入 | 一句话把网页添加到知识库 |
| 文件上传 | PDF/Word/PPT/Excel/图片等，自动走 create_media → COS → add_knowledge |
| HTML 转 PDF | Playwright 自动渲染，完美保留样式 |

## 触发词

上传到ima、放入ima知识库、添加到ima、ima导入、ima上传

## 依赖

- WorkBuddy（codebuddy.cn）
- 「腾讯ima」技能（skill_2053082144792322048）
- IMA OpenAPI 凭证

## 避坑经验

本技能沉淀了以下实战中发现的关键坑位：

- kb_id 必须用 encoded 格式（base64），不能用 MCP 返回的数字 ID
- 导入到根目录时**不要传 folder_id**，否则报 222000
- PowerShell 5.1 处理中文 JSON 会乱码，用 Python subprocess
- Windows 上 weasyprint 缺少 GTK 库，用 Playwright
