# 安全策略 / Security Policy

## 报告安全问题

如发现本仓库的安全问题（例如四件套 JSON 被注入恶意规则、MCP 契约泄露真实运单或人员证件号、隐私声明字段被弱化），请**私下**联系维护者：

- 邮箱：zhaoxinghua09@gmail.com
- 请在邮件中说明：问题描述、复现步骤、影响范围、建议修复方式。

**不要在公开 issue / PR 中披露未修复的安全问题。**

## 范围

本仓为声明式域骨架（4 个 JSON + 文档），无可执行代码、无网络服务、不采集运行时数据。

- `checker.io.json` 仅定义 MCP 工具契约；真正的核验端点由认领的运营方实现（`checker_endpoint` 现为 `mcp://pending-claim/log-checker`）。
- `privacy.json` 默认数据类目为 off、sharing disabled、cross_border disabled。

## 我们的承诺

- 收到有效报告后，我们会在合理时间内确认并评估。
- 修复后会在对应文件中记录（按需脱敏）。

## 使用者须知

- 请从**本仓库官方地址**获取，警惕第三方二次打包。
- 认领方实现 checker 端点时，不得输出 `checker.io.json` 的 `_forbidden_outputs` 列出的任何结论性表述。
- 任何密钥 / 令牌 / 真实运单或人员证件号都不应提交进仓库。

---

许可：代码与配置 MIT（© 2026 SynomosAI）｜文档知识版权 All Rights Reserved ｜ 联系：zhaoxinghua09@gmail.com ｜ ORCID 0009-0001-0512-1237
