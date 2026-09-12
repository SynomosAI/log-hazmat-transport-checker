# log-hazmat-transport-checker

> **状态：RESERVED（占位 · 开放认领）** — 本仓已按平台协议规范建好行业接入四件套骨架，
> 等待具备本域资质的运营方认领并填充真实规则。

把「这批货能不能运、谁有资格运」拆成可核验的属性，让 AI 只做要件提示，不做承运放行结论。

## 这个域管什么

道路危险货物运输资质与承运条件核验

危险货物按类别有专门的包装、车辆、人员与应急预案要求，匿报夹带是主要事故成因。AI 能做的是把资质与条件摆清楚，承运放行权在企业安全管理人员与交通运输主管部门。

## 域标识

| 项 | 值 |
|---|---|
| 域 ID | `log`（全局唯一，一经分配不复用） |
| 域名称 | 物流 · 道路危险货物运输资质 |
| Profile 版本 | `domain/1.0` |
| 当前状态 | `RESERVED` |
| 占位时间 | 2026-09-12 |

## 属性清单

| 属性键 | 类型 | 说明 |
|---|---|---|
| `log.cargo_class` | enum | 按 JT/T 617 划分的危险货物类别；是否为危货须以鉴定结论为准 · 取值 explosives/gases/flammable_liquid/flammable_solid/oxidizing/toxic/radioactive/corrosive/miscellaneous/not_hazmat/undetermined |
| `log.transport_permit` | enum | 道路危险货物运输经营许可（含经营范围） · 取值 valid/expired/none/not_required |
| `log.vehicle_qualification` | enum | 车辆、罐体与安全技术状况是否符合所运类别要求 · 取值 qualified/unqualified/unknown/not_required |
| `log.personnel_cert` | enum | 驾驶员、押运员从业资格证与当前有效性 · 取值 valid/expired/none/unknown |
| `log.emergency_plan` | enum | 应急预案备案与演练记录 · 取值 filed/missing/not_required |

## 本域红线（不可逾越，机器可读）

1. 不得输出「可承运」「可放行」结论，以交通运输主管部门许可为唯一依据
2. 人员资质失效、车辆不合格或类别不明时不得给出可运输表述
3. 不得建议匿报、夹带、普货混装、拆分申报等方式规避危货监管

> 红线在 `gate-map.json` 中均有对应阻断规则。平台校验器会检查「每条红线都有规则覆盖」，
> 缺失即校验失败——**制度与系统不允许不同步**。

## 行业接入四件套

| 文件 | 作用 |
|---|---|
| `domain.manifest.json` | 本域声明：属性清单、签发方要求、有效期、红线 |
| `gate-map.json` | 本域「什么动作要多少摩擦」：silent / warn / confirm / block / require-owner |
| `privacy.json` | 本域隐私声明：默认关闭、最小必要、可撤回、可删除 |
| `checker` | 本域核验器（MCP 工具，**只出示核验，不下判定**） |

## 核心原则

**平台只当擂台，不当货架。** 本域的核验器只回答「这条声明是否可核验、缺什么要件」，
不回答「这件事是否合规、该不该做」。判定权在本域的资质方、监管方与人。

**隐私是准入条件，不是整改事项。** 缺失 `privacy.json` 或任一必填字段不符，
符合性校验直接失败——不是警告，是拒绝接入。

## 参考依据

- 危险化学品安全管理条例
- 中华人民共和国道路运输条例
- 道路危险货物运输管理规定
- JT/T 617 危险货物道路运输规则
- 中华人民共和国安全生产法

> 上列依据仅用于说明本域属性的来源与口径，不构成法律意见。具体适用以现行有效文本与主管部门解释为准。

## 认领方式

本域面向具备相应资质的机构开放。认领后请：

1. Fork 本仓，填注 `operator` 与 `checker_endpoint`
2. 按本域现行有效规则校准属性取值与红线表述
3. 跑平台侧校验器自测（五项判据全过方可提交）
4. 提 PR，附资质证明与规则依据

## 许可与署名

代码与配置按 MIT 许可使用。文档的知识版权归 SynomosAI 所有。

© 2026 SynomosAI. All rights reserved.
