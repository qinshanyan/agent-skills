# Automotive E/E Architecture Expert Skill

面向汽车整车/系统电子电器架构工作的跨 Agent AI Skill。

它不是一个“汽车架构师角色 Prompt”，而是一套带流程、分层、功能分配规则、质量门禁、追溯和验证要求的工程 Skill。

## 适合处理

- 整车功能的架构化分解
- 功能架构 / 逻辑架构 / 物理 E/E 架构
- HPC / ZCU / 域控 / ECU / Sensor / Actuator 功能分配
- 中央计算、域架构、区域架构的方案比较
- 接口、信号/服务、网络路径设计
- 架构评审与变更影响分析
- 从 PRD / Vehicle Feature 连接到系统/控制器需求

## 核心工作链

`Need/Feature → Scenario → System Function → Functional Chain → Logical Element → Physical E/E Element → Interface/Communication → Derived Requirement → Verification`

## 仓库位置

本 Skill 发布在：

`qinshanyan/agent-skills/skills/automotive-ee-architecture-expert/`

## 给不同 Agent 使用

### Claude Code

如果已经安装/克隆 `qinshanyan/agent-skills`，让 Claude Code 加载整个插件/skills 目录即可。也可以只复制：

```text
skills/automotive-ee-architecture-expert/
```

到你的 Claude skills 目录中。主入口是 `SKILL.md`，references 按需加载。

### Gemini CLI

安装整个 skills 仓库后，指向 `skills` 目录；或者只复制本 Skill 目录到 Gemini 的 native skills 目录。Agent 应读取 `SKILL.md` 作为入口。

### Cursor

可将 `SKILL.md` 复制/链接到项目的 `.cursor/rules/`，并保持 `references/` 相对目录可访问；或在项目规则中明确要求读取本 Skill 的 `SKILL.md`。

### Codex / OpenCode / Windsurf / Copilot / 其他 Agent

任何支持 instruction file、system prompt、AGENTS.md 或项目规则文件的 Agent 都可以使用：

1. 把 `SKILL.md` 作为主指令加载；
2. 保持 `references/` 目录可读取；
3. 当 `SKILL.md` 指示时加载相应 reference；
4. 不要把 reference 全部无脑塞进上下文，按需加载即可。

### 最通用的用法

如果目标 Agent 没有原生 Skill 机制，把下面这句话放到项目级规则中：

> For automotive E/E architecture tasks, read and follow `skills/automotive-ee-architecture-expert/SKILL.md`. Load its referenced files on demand and treat its workflow and quality gates as mandatory unless the user explicitly overrides them.

## 文件

- `SKILL.md`：主技能与完整工作流
- `references/method.md`：架构分层与功能分解方法
- `references/allocation-rules.md`：HPC / ZCU / ECU 等功能分配规则
- `references/output-contract.md`：Architecture Pack 输出契约
- `references/quality-gates.md`：架构质量门禁
- `examples/smoke-test.md`：建议试跑用例
- `SOURCES.md`：方法来源
- `VALIDATION.md`：本包结构检查结果

## 推荐试用提示

> 按 automotive-ee-architecture-expert 分析“无框车门玻璃微降”。先不要假定一定由 BDC 实现，请从用户场景、功能分解、功能链、逻辑架构开始，然后比较 BDC / ZCU / 门模块等分配方案，给出接口和关键时序开放项。

也可以直接说：

> Use the automotive-ee-architecture-expert skill to review this architecture. Do not accept the current ECU allocation as a given; reconstruct the functional and logical architecture first, then evaluate the physical allocation and interfaces.

## 设计目标

它不是“自动替代架构师”，而是强制架构工作具备：

- 分层：Need / Function / Logical / Physical 不混为一谈
- 追溯：上游需求到下游 E/E 元素可双向追踪
- 决策依据：关键分配必须有备选方案和 ADR
- 假设透明：未知数据标 `OPEN/ASSUMPTION`，不编造数值
- 动态行为：不仅画静态框图，也分析状态、时序和故障降级
- 工程约束：考虑 timing/safety/security/power/network/OTA/diagnostics 等
- 可评审：有明确质量门禁与 verification 计划

## 方法基础

该 Skill 是原创综合，主要吸收公开的 Arcadia/Capella 分层思想、Automotive SPICE SYS.3 的系统架构实践、工业 E/E 功能分配方法、AUTOSAR/现代中央计算与区域架构思路。详见 `SOURCES.md`。
