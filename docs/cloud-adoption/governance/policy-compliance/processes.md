---
title: CAF：监视和强制执行策略遵循
description: 如何确保符合既定的策略？
author: BrianBlanchard
ms.date: 1/4/2019
ms.openlocfilehash: 9066f33c8baa183476a9632e82d6eb960d03752c
ms.sourcegitcommit: 273e690c0cfabbc3822089c7d8bc743ef41d2b6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55900470"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-processes-can-help-ensure-policy-adherence"></a>哪些流程可帮助确保策略遵循？

<!---
I've defined policies, I've provided an architecture guide. Now how do I monitor adherence to policy? If there is a violation, how do I enforce the policy?
--->

在建立云策略声明并起草设计指南之后，你需要创建一个策略，确保云部署符合策略要求。 此策略需包含云治理团队的持续审查和沟通流程，为何时需要对策略违反行为采取行动建立标准，以及定义检测违规和触发补救措施的自动监控和符合性系统的要求。

有关策略遵循流程如何适应云治理计划的示例，请参阅[可操作的治理过程](../journeys/overview.md)中的公司策略部分。

## <a name="prioritize-policy-adherence-processes"></a>设置策略遵循流程的优先级

开发流程需要多少投资来支持策略目标？ 根据云部署的规模和成熟度，建立支持符合性的流程所需的工作和与此工作相关的成本可能千差万别。

对于只包括开发和测试资源的小型部署来说，策略要求可能很简单，并且只需要很少的专用资源来处理。 另一方面，对于一个成熟的任务关键型云部署，其具有高优先级安全性和性能需求，这就可能需要一组人员、全面的内部流程和自定义监控工具来支持策略目标。

作为定义策略遵循规划的第一步，请评估下面讨论的流程如何支持策略要求。 确定在这些流程中值得投入多少工作量，然后使用这些信息来建立切合实际的预算和人员配置计划，以满足这些需求。

## <a name="establish-cloud-governance-team-processes"></a>建立云治理团队流程

在定义策略符合性修正的触发器之前，需要建立团队将使用的整个流程，以及如何在 IT 人员和云治理团队之间共享和升级信息。

### <a name="assign-cloud-governance-team-members"></a>分配云治理团队成员

谁将提供关于策略符合性的持续指导，并处理在部署和运营云资产时出现的与策略相关的问题？ 云治理团队的规模和人员构成将取决于策略需求的复杂性，以及与策略符合性相关的预算和人员优先级。

请选择在你所定义的策略声明所涉及领域具有专业知识的团队成员。 对于初始测试部署，这可以仅限于少数几个负责建立治理基础的系统管理员。 随着部署的成熟和策略复杂性的增加，以及与更广泛的公司策略需求更密切地整合，云治理团队需要随之变化，以支持日益复杂的策略需求。

随着治理流程的成熟，定期检查云指导团队的成员资格，以确保能够正确处理最新的策略需求。 确定 IT 人员中具有特定治理领域的相关经验或对该领域感兴趣的成员，并根据需要将他们永久或临时纳入团队。

### <a name="reviews-and-policy-iteration"></a>审查和策略迭代

部署其他资源时，云治理团队需要确保新的工作负载或资产符合策略需求。 计划与负责部署任何新资源的团队会面，讨论与设计指南的一致性。

随着整体部署的扩大，定期评估新的潜在风险，并根据需要更新策略声明和设计指南。 定期安排五个治理规则的评审周期，确保策略最新且满足其需求。

### <a name="education"></a>教育

策略符合性要求 IT 人员和开发者理解影响其职责范围的策略需求。 计划投入资源来记录决策和需求，并就支持策略需求的设计指南对所有相关团队进行培训。

随着策略的变化，定期更新文档和培训材料，并确保培训工作传达最新要求及指导给相关 IT 人员。  

### <a name="establish-escalation-paths"></a>建立升级路径

如果资源不合规，谁将获得通知？ 如果 IT 人员检测到一个策略符合性问题，他们应联系谁？ 确保对云治理团队的升级流程进行明确定义。 确保这些沟通渠道保持更新，以反映员工和组织的变化。

## <a name="violation-triggers-and-actions"></a>违规触发器和操作

在定义云治理团队及其流程之后，需要明确定义哪些符合性违规行为将会触发操作，以及对应的操作应是什么。

### <a name="define-triggers"></a>定义触发器

对于每个策略声明，查看各项要求，确定哪些行为将导致违反策略。 使用策略定义流程中已经建立的信息生成触发器。

* 风险容忍度 - 根据在[风险容忍度分析](risk-tolerance.md)中建立的度量值和风险指标创建违规触发器。
* 已定义的策略需求 - 策略声明可能提供服务级别协议 (SLA)、业务连续性和灾难恢复 (BRCD)，或者应用作符合性触发器基础的性能要求。

### <a name="define-actions"></a>定义操作

每个违规触发器都应具有相应的操作。 触发的操作应始终在出现违规情况时通知适当的 IT 人员或云治理团队成员。 根据此通知，可能会对符合性问题进行手动审查，或根据检测到的违反行为的类型和严重程度启动预先建立的修正流程。

违规触发器和操作的一些示例：

| 云治理规则 | 示例触发器 | 示例操作 |
|-----------------------------|----------------|---------------|
| 成本管理 | 每月云支出比预期高出 20% 以上。 | 通知计费部门负责人，他们将开始审查资源使用情况。 |
| 安全基线 | 检测到可疑的用户登录活动。 | 通知 IT 安全团队，并禁用可疑的用户帐户。 |
| 资源一致性 | 工作负载的 CPU 使用率大于 90%。 | 通知 IT 运维团队并横向扩展要处理负载的其他资源。 |

## <a name="monitoring-and-compliance-automation"></a>监视和符合性自动化

在定义符合性违规触发器和操作之后，可以开始计划如何最大程度地使用云平台的日志记录和报告工具，以及其他功能来帮助自动化监视和策略符合性策略。

请参阅 CAF [日志记录和报告决策指南](../../decision-guides/log-and-report/overview.md)主题，获得关于为部署选择最佳监视模式的指导。
