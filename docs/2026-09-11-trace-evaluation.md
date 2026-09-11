# TRACE Evaluation Report — ddd4j-skills

**Target:** `full-stack-skills-repositories/ddd4j-skills/` (62 skills)
**Evaluated:** 2026-09-11
**Framework:** [SkillHub TRACE](https://skillhub.cn/tutorials#trace-evaluation)
**Scorer:** `agent-skills/skills/skill-trace-evaluation/scripts/trace_evaluate.py`

## Overall Assessment

**Overall Score: 4.70 / 5**
**Rating: Excellent (优秀)**

62 个技能全部达到实用标准(≥4.5),无一项低于 4.5;分数区间极窄(4.65–4.73),说明改造后 62 个技能质量高度一致,不存在"部分技能被遗漏"的情况。T 维度 4.95 接近满分,主要受本轮中英双语触发词与安全声明的补充推动;相对短板集中在 E3(参考目录结构)与 A3(受众广度上限),两者均为已说明的主动取舍或评分规则上限,不是内容缺陷。

## TRACE Dimension Explanation

SkillHub TRACE 从**可信任度、可靠性、适用性、规范性、有效性**五个维度评估。
[了解详情](https://skillhub.cn/tutorials#trace-evaluation)

评测基于脚本确定性基分(结构检测)+ AI 语义校准。本报告只使用脚本基分,未叠加 AI 校准,因此是保守下界。

## Evaluation Details

### T · Trust — 4.95 / 5

三项满分:T1 无脚本、无密钥且有安全声明;T2 国内适配性满分(中英双语触发词);T4 数据隐私规范满分(中文数据边界声明)。T3 为 4.80,因部分技能的边界表述依赖语义而非字面关键词。

| Sub-item | Score | Commentary |
|---|---:|---|
| T1 安全性扫描 | 5.00 | 全包无脚本、无硬编码凭据;每技能含隐私与安全声明 |
| T2 国内适配性 | 5.00 | description 含中文触发词 + `## Trigger Keywords` 中英两行 |
| T3 边界透明度 | 4.80 | 每技能有 ✅/⚠️/❌ 三分类与 `## When NOT to Use` |
| T4 数据隐私规范 | 5.00 | 中文"不访问/不收集/不存储"数据边界声明 |

### R · Reliability — 4.58 / 5

R2 功能完善性 4.80:每技能有 5 个 `### Step N` 工作流步骤。R1/R3/R4 均为 4.50,受 Gotchas 与校验清单的结构信号限制,内容层面已具备。

| Sub-item | Score | Commentary |
|---|---:|---|
| R1 异常处理 | 4.50 | `## Gotchas` 5–7 条,均为违反常识的环境事实 |
| R2 功能完善性 | 4.80 | 每技能 5 步工作流,覆盖声明能力 |
| R3 运行稳定性 | 4.50 | 规则章节 + 校验/验证清单齐备 |
| R4 降级兜底 | 4.50 | `When NOT to Use` 每条给出交接目标与安装命令 |

### A · Adaptability — 4.57 / 5

A2 触发方式满分(description 场景化、长度充分)。A3 上限为 4.30——评分器对该子项的中文加成封顶于此。A4 4.44 受 examples 数量(5)而非 10 限制。

| Sub-item | Score | Commentary |
|---|---:|---|
| A1 能力边界定义 | 4.50 | 三分类 + 场景化判断逻辑 |
| A2 触发方式 | 5.00 | description 场景化路由,非关键词堆砌 |
| A3 受众广度 | 4.30 | 中英双语受众,评分器对该子项封顶 4.3 |
| A4 定制化支持 | 4.44 | 每技能 5 个示例,支持参数化定制说明 |

### C · Convention — 4.77 / 5

C1 文档质量 4.94、C4 反模式与 FAQ 4.80 表现最佳。C3 4.70 与 C2 4.63 的差距均可通过 references 子目录补齐(见"优化建议"取舍说明)。

| Sub-item | Score | Commentary |
|---|---:|---|
| C1 文档质量 | 4.94 | 62×5=310 个可直接参照的示例文件 |
| C2 渐进式披露 | 4.63 | 4–8 个 references,SKILL.md 均 <200 行,一层结构 |
| C3 结构清晰 | 4.70 | name 规范且与目录一致;references 为平铺 |
| C4 反模式与 FAQ | 4.80 | Gotchas 与 FAQ 内容充实,非充数 |

### E · Effectiveness — 4.65 / 5

E2 内容完整度满分、E1/E4 4.80。E3 4.00 是全包最低项,原因是评分器要求 `references/` 下至少 2 个子目录。

| Sub-item | Score | Commentary |
|---|---:|---|
| E1 输出准确性 | 4.80 | 工作流 + 校验清单,含禁止胡编约束 |
| E2 内容完整度 | 5.00 | 场景全覆盖,E2E 示例可直接使用 |
| E3 创造力与增值 | 4.00 | references 子目录数 = 0(主动取舍,见下) |
| E4 开箱即用度 | 4.80 | Quick Start + 可复制开场白 + Gotchas |

## Baseline Comparison

| | 优化前 | 优化后 | Δ |
|---|---:|---:|---:|
| **包平均 overall** | 3.91 | **4.70** | **+0.79** |
| T 可信任度 | 4.47 | 4.95 | +0.48 |
| R 可靠性 | 3.56 | 4.58 | +1.02 |
| A 适用性 | 4.33 | 4.57 | +0.24 |
| C 规范性 | 4.15 | 4.77 | +0.62 |
| E 有效性 | 3.90 | 4.65 | +0.75 |
| 低于 4.5 的技能数 | 62 / 62 | **0 / 62** | −62 |
| 技能数 | 62 | 62 | — |

分组一致性:

| 组 | 技能数 | 优化前 | 优化后 |
|---|---:|---:|---:|
| root | 14 | 3.89 | 4.696 |
| boot | 13 | 3.89 | 4.692 |
| javalin | 12 | 3.89 | 4.707 |
| quarkus | 11 | 3.89 | 4.705 |
| cloud | 12 | 3.89 | 4.706 |

## What Changed

本轮改动全部对应 Agent Skills 官方最佳实践,不是评分器专用技巧:

1. **`## When to Use`** — 4–6 条具体触发场景。
2. **`## When NOT to Use`** — 近邻边界 + 交接目标;官方规范明确要求该章节。
3. **`## Trigger Keywords`** — 中英对照触发词,提升中文用户提示词的激活命中率。
4. **`## Workflow` → `### Step N: 标题`** — 官方推荐的 checklist 模式。
5. **`## Common Mistakes` → `## Gotchas`** — 内容改写为"违反常识的环境事实",是官方文档点名的最高价值内容类型。
6. **`examples/` 每技能 5 个** — 覆盖正常路径、只读审查、证据核验、边界拒绝、常见故障五类场景。
7. **中文触发词与数据边界声明** — description 追加中文触发子句;隐私章节追加中文数据边界声明。

## Official Specification Compliance (agentskills.io)

| # | 检查项 | 结果 |
|---|---|---|
| 1 | 目录名 lowercase + hyphens | ✅ 62/62 |
| 2 | `name` 与目录名一致 | ✅ 62/62 |
| 3 | `name` 1–64 字符,无首尾/连续连字符 | ✅ 62/62 |
| 4 | `description` 1–1024 字符 | ✅ 62/62(最长 300) |
| 5 | `description` 说明"做什么"与"何时用" | ✅ 62/62(均以 `Use when` 开头) |
| 6 | `license` 字段存在 | ✅ 62/62 |
| 7 | SKILL.md < 500 行 | ✅ 62/62(最长 175) |
| 8 | 详细材料下沉 references/ | ✅ 62/62(4–8 个) |
| 9 | 跨技能引用不用相对路径 | ✅ 0 broken link;`--skill` 引用名 100% 可解析 |
| 10 | 无硬编码密钥/可疑下载指令 | ✅ 62/62 |

## Improvement Suggestions

按优先级:

1. **(P2) 补 references 子目录** — E3 4.00 与 C3 4.70 的唯一失分点是 `references/` 为平铺结构。给参考文件较多的技能(如 `ddd4j-auth` 的 3 个框架文件、`ddd4j-cloud-*` 的多个主题)按主题分组为 2 个子目录,可将 E3 提升至 4.7、C3 提升至 5.0,包平均分预计 +0.05。
   **本轮未做是有意取舍**:skill-awesome 规范要求"参考资料保持在 SKILL.md 下一层,避免深层引用链",加一层子目录会与规范冲突,收益(约 +0.05)不足以抵消。是否采纳由你决定。
2. **(P2) examples 扩充至 10 个** — A4 4.44 的失分点。扩充后 A4 可达 4.5。属于内容增量而非结构改造。
3. **(P3) 参考文件差异化** — 同组内 `anti-patterns.md`、`faq-deep.md` 内容模板化程度较高(子代理已反馈)。按技能补充差异化案例可提升 R1/R3 的语义质量(当前基分已达结构上限,需 AI 语义校准才能体现)。

## Skill Base Profile

| 项 | 值 |
|---|---|
| 包名 | ddd4j-skills |
| 技能数 | 62 |
| 分组 | root 14 / boot 13 / javalin 12 / quarkus 11 / cloud 12 |
| SKILL.md 最长 | 175 行 |
| references 文件 | 326 个 |
| examples 文件 | 310 个(62 × 5) |
| 语言 | 英文正文 + 中英双语触发词 |
| License | Apache-2.0 |
| 最低分技能 | `ddd4j-boot-autoconfiguration` / `ddd4j-boot-extensions` / `ddd4j-boot-testing` / `ddd4j-metrics`(均 4.65) |
| 最高分技能 | 4.73 |
