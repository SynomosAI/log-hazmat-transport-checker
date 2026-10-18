# AGENTS.md — 给 AI Agent 的工作指引

人类读者请看 [README.md](README.md)。

## 这个仓库是什么

`log-hazmat-transport-checker` 是 SynomosAI 平台的**声明式域 Profile 骨架**（domain/1.0），不是可运行 SDK，也不是已上线产品。当前状态 RESERVED：四件套已建好，等待有资质的运营方认领并填注 `operator` / `checker_endpoint`。

核心资产：`domain.manifest.json`（声明）、`gate-map.json`（摩擦五级）、`privacy.json`（隐私）、`checker.io.json`（MCP 契约）。

## 可用的工作命令

```bash
git clone https://github.com/SynomosAI/log-hazmat-transport-checker.git
cd log-hazmat-transport-checker
cat domain.manifest.json                  # 通读声明
python -m json.tool domain.manifest.json  # 校验 JSON 合法
```

本仓无运行时依赖；**不要尝试「运行」本仓**。

## 约定（Do）

- 修改属性或红线后，必须同步 `gate-map.json`（每条红线都要有对应规则），并重新跑平台校验器自测。
- 新增属性时同步更新 `privacy.json` 的 `data_categories[].attr_keys`。
- 保持 `checker.io.json` 的输出状态词表（shown / missing / expired / unverifiable）不变。

## 禁止（Don't）

- 不要输出「可承运 / 可放行 / 已合规」类结论——核验器只出示出处链。
- 不要改动 `LICENSE` / `LICENSE-CONTENT` 的版权主体，不要改 `CODEOWNERS`。
- 不要提交任何密钥、真实运单或人员证件号；示例证据用占位指纹。
- 不要建议匿报、夹带、普货混装、拆分申报等方式规避危货监管。

## 边界

本域只覆盖道路危货类别、运输经营许可、车辆罐体资质、驾押人员证件与应急预案属性的出示与核验；不替代企业安全管理人员与交通运输主管部门的承运放行决定，不构成法律意见。
