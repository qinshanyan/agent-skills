# Smoke Test

## 测试 1：单功能架构分解

输入：

> 对“电动尾翼自动升降”做架构设计。车辆目前存在中央车控计算平台、左右区域控制器，尾翼带独立执行器控制器。不要直接沿用现有分配，请先做功能架构，再比较自动控制逻辑放中央车控、ZCU、尾翼 ECU 三种方案。关注车速信号、驾驶模式、手动操作、防夹/堵转、故障降级、休眠唤醒、诊断、OTA 和时序。未知参数不要编造。

期望：
- 先输出 system context / assumptions
- 场景覆盖正常、手动、故障、睡眠/唤醒
- 功能树不是 ECU 树
- 给出 functional chain
- 明确 architecture drivers
- 三种候选 allocation 有 hard-constraint 检查和 rationale
- 定义 semantic interfaces 后再谈 CAN/Ethernet
- 未知延时目标标 OPEN，不随意写数值
- 有 ADR、traceability、verification

## 测试 2：架构评审

输入：

> 当前方案把所有车身功能都迁移到中央 HPC，ZCU 只做 I/O。请按该 Skill 评审这个方案。重点看网络、故障传播、唤醒、低级闭环控制、诊断和 OTA 耦合。

期望：
- 不因为“中央化是趋势”直接判优
- 分析 raw data / control traffic / failure blast radius / wake dependency
- 区分适合中央化的跨域逻辑与应局部保留的低级实时/安全控制
- 输出 BLOCKER / MAJOR / MINOR / OPEN，而不是泛泛而谈
