---
title: CAF：什么是云安全基线
titleSuffix: Microsoft Cloud Adoption Framework for Azure
ms.service: architecture-center
ms.subservice: enterprise-cloud-adoption
ms.custom: governance
ms.date: 10/10/2018
description: 什么是云安全基线？
author: BrianBlanchard
ms.openlocfilehash: cb6e3372fd76486e5c4467ef822163eac0499573
ms.sourcegitcommit: 273e690c0cfabbc3822089c7d8bc743ef41d2b6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55900549"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-the-cloud-security-baseline"></a><span data-ttu-id="6ce5a-103">什么是云安全基线？</span><span class="sxs-lookup"><span data-stu-id="6ce5a-103">What is the Cloud Security Baseline?</span></span>

<span data-ttu-id="6ce5a-104">这是有关云安全基线一般主题的介绍性文章，云安全基线以[云治理的五项规则](../governance-disciplines.md)为基础而构建，来建立治理框架。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-104">This is an introductory article on the general topic of Cloud Security Baseline which builds on the [Five Disciplines of Cloud Governance](../governance-disciplines.md) to establish a governance framework.</span></span> <span data-ttu-id="6ce5a-105">[Azure 的受信任云](https://azure.microsoft.com/overview/trusted-cloud/)提供了有关云安全的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-105">More detailed information about Cloud Security is available from [Azure's Trusted Cloud](https://azure.microsoft.com/overview/trusted-cloud/).</span></span> <span data-ttu-id="6ce5a-106">改进组织安全状况的方法可以在[云安全服务目录](https://www.microsoft.com/security/information-protection)中找到</span><span class="sxs-lookup"><span data-stu-id="6ce5a-106">Approaches to improving your organizations security posture can be found in the [Cloud Security Service Catalog](https://www.microsoft.com/security/information-protection)</span></span>

> [!NOTE]
> <span data-ttu-id="6ce5a-107">本文并非旨在提供足够的上下文以使读者可以实现安全策略。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-107">This article is not expected to provide enough context to allow the reader to implement a security strategy.</span></span> <span data-ttu-id="6ce5a-108">它仅用于进行一般了解。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-108">It is for general awareness only.</span></span>

## <a name="cloud-security"></a><span data-ttu-id="6ce5a-109">云安全</span><span class="sxs-lookup"><span data-stu-id="6ce5a-109">Cloud security</span></span>

<span data-ttu-id="6ce5a-110">云安全是传统信息安全做法的扩展。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-110">Cloud security is an extension of traditional information security practices.</span></span> <span data-ttu-id="6ce5a-111">传统 IT 安全包括用于治理计算机安全、网络安全、数据保护、信息使用情况等的策略和控制。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-111">Traditional IT security would include policies and controls governing computer security, network security, data protection, information usage, and so forth.</span></span> <span data-ttu-id="6ce5a-112">云中需要这些相同的策略和控制。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-112">These same policies and controls are needed in the cloud.</span></span> <span data-ttu-id="6ce5a-113">在任何云转换过程中，CISO 都必须主动参与并了解云环境，以确保旧 IT 策略映射到云中的适当控制级别。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-113">During any Cloud Transformation, it is imperative that the CISO be actively involved and understand the cloud landscape, to ensure legacy IT policies map to proper levels of control in the cloud.</span></span>

<span data-ttu-id="6ce5a-114">任何云安全策略都应至少考虑以下主题：</span><span class="sxs-lookup"><span data-stu-id="6ce5a-114">At minimum, any cloud security strategy should consider the following topics:</span></span>

* <span data-ttu-id="6ce5a-115">对数据进行分类：进行正确的数据分类，以了解任何专用、受保护或高度机密的数据源。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-115">Classify data: Proper data classification to understand any data sources that are private, protected, or highly confidential.</span></span> <span data-ttu-id="6ce5a-116">这将有助于在规划过程中管理风险。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-116">This will help manage risk during planning.</span></span>
* <span data-ttu-id="6ce5a-117">规划混合云方案：了解旧的本地网络如何连接到云将有助于 CISO 确定和缓解风险。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-117">Plan for a hybrid cloud scenario: Understanding how legacy, on-premise networks will connect to the cloud will help the CISO identify and mitigate risks.</span></span>
* <span data-ttu-id="6ce5a-118">规划攻击和错误：在转换的头几个月中，团队会在学习过程中犯错。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-118">Plan for attacks and mistakes: In the first few months of a transformation, mistakes will be made as the team learns.</span></span> <span data-ttu-id="6ce5a-119">从低风险和高度受限的部署开始，以便安全地学习。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-119">Start with low risk and highly restricted deployments to learn securely.</span></span>
* <span data-ttu-id="6ce5a-120">确定隐私优先级：在任何转换的整个过程中，整个团队都应该将客户和员工隐私放在首位。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-120">Prioritize privacy: Throughout any transformation, the entire team should keep customer and employee privacy top of mind.</span></span> <span data-ttu-id="6ce5a-121">数据在云中是安全的，但是团队应在处理敏感数据时保持注意并格外谨慎。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-121">Your data is safe in the cloud, but the team should be aware and extra cautious when dealing with sensitive data.</span></span>

## <a name="protecting-data-and-privacy"></a><span data-ttu-id="6ce5a-122">保护数据和隐私</span><span class="sxs-lookup"><span data-stu-id="6ce5a-122">Protecting data and privacy</span></span>

<span data-ttu-id="6ce5a-123">对于世界各地的组织 &mdash; 无论是政府机构、非营利组织还是企业 &mdash;，云计算已成为其正在进行的 IT 策略的关键部分。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-123">For organizations throughout the world &mdash; whether governments, nonprofits, or businesses &mdash; cloud computing has become a key part of their ongoing IT strategy.</span></span> <span data-ttu-id="6ce5a-124">云服务使所有规模的组织都可以访问几乎无限的数据存储，同时使它们无需购买、维护和更新自己的网络和计算机系统。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-124">Cloud services give organizations of all sizes access to virtually unlimited data storage while freeing them from the need to purchase, maintain, and update their own networks and computer systems.</span></span> <span data-ttu-id="6ce5a-125">Microsoft 和其他云提供商可提供 IT 基础结构、平台和软件即服务 (SaaS)，从而使客户可以根据需要快速向上向上或向下扩展，并且仅为所使用的计算能力和存储付费。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-125">Microsoft and other cloud providers offer IT infrastructure, platform, and software as a service (SaaS), enabling customers to quickly scale up or down as needed and only paying for the computing power and storage they use.</span></span>

<span data-ttu-id="6ce5a-126">但是，随着组织不断利用云服务的好处（如增加选择、敏捷性和灵活性，同时提高效率并降低 IT 成本），它们必须考虑云服务的引入会如何影响其隐私、安全性和符合性状态。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-126">However, as organizations continue to take advantage of the benefits of cloud services, such as increased choice, agility, and flexibility while boosting efficiency and lowering IT cost, they must consider how the introduction of cloud services affects their privacy, security, and compliance posture.</span></span> <span data-ttu-id="6ce5a-127">Microsoft 努力使其云产品/服务不仅可缩放、可靠且可管理，而且可确保客户数据受保护并以透明方式进行使用。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-127">Microsoft has worked to make their cloud offerings not only scalable, reliable, and manageable, but also to ensure our customers data is protected and used in a transparent manner.</span></span>

<span data-ttu-id="6ce5a-128">安全性是所有联机计算环境中强大数据安全措施的必要组件。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-128">Security is an essential component of strong data safeguards in all online computing environments.</span></span> <span data-ttu-id="6ce5a-129">但仅仅只有安全性并不够。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-129">But security alone is not sufficient.</span></span> <span data-ttu-id="6ce5a-130">消费者和企业使用特定云计算产品的意愿还取决于其是否能够信任其信息隐私会受到保护，以及其数据仅采用与客户期望一致的方式进行使用。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-130">Consumers’ and businesses’ willingness to use a particular cloud computing product also depends on their ability to trust that the privacy of their information will be protected, and that their data will only be used in a manner consistent with customer expectations.</span></span> <span data-ttu-id="6ce5a-131">详细了解 Microsoft 用于[在云中保护数据和隐私](https://go.microsoft.com/fwlink/?LinkId=808242&clcid=0x409)的方法</span><span class="sxs-lookup"><span data-stu-id="6ce5a-131">Learn more about Microsoft's approach to [Protecting data and privacy in the cloud](https://go.microsoft.com/fwlink/?LinkId=808242&clcid=0x409)</span></span>

## <a name="risk-mitigation"></a><span data-ttu-id="6ce5a-132">风险缓解</span><span class="sxs-lookup"><span data-stu-id="6ce5a-132">Risk mitigation</span></span>

<span data-ttu-id="6ce5a-133">任何数据中心内的两个最大风险可以分成两个来源：老化系统和人为错误。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-133">The two greatest risks in any datacenter can be grouped into two sources: Aging systems and Human error.</span></span> <span data-ttu-id="6ce5a-134">防范这两种风险是定义 IT 安全策略的最低限度。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-134">Protecting against these two risks is a minimum when defining an IT security strategy.</span></span> <span data-ttu-id="6ce5a-135">这同样适用云中的情况。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-135">The same is true in the cloud.</span></span> <span data-ttu-id="6ce5a-136">以下是为缓解风险并增强云安全策略而可以实施的控制的一些示例。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-136">The following are a few examples of controls that can be put in place to mitigate risks and strengthen your Cloud Security strategy.</span></span>

* <span data-ttu-id="6ce5a-137">旧系统：本地数据中心解决方案中的许多组件由早于当前安全风险的软件、硬件和流程组成。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-137">Legacy Systems: Many components in on-premises datacenter solutions consist of software, hardware, and processes that predate current security risks.</span></span> <span data-ttu-id="6ce5a-138">如果可能，请在云转换过程中修正、替换或停用这些系统。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-138">When possible, remediate, replace, or retire these systems during a Cloud Transformation.</span></span> <span data-ttu-id="6ce5a-139">当然，这并不总是可行。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-139">Of course, that's not always feasible.</span></span> <span data-ttu-id="6ce5a-140">如果有任何旧系统将保留在混合解决方案中的生产中，请务必在虚拟数据中心设计过程中对这些系统列出清单并进行了解。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-140">If any legacy systems will remain in production in a hybrid solution, it is important that those systems have been inventoried and understood during Virtual Datacenter design.</span></span> <span data-ttu-id="6ce5a-141">这样做可使设计团队能够消除或控制从云中对这些系统进行的访问。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-141">Doing so allows the design team to eliminate or control access to those systems from the cloud.</span></span>
* <span data-ttu-id="6ce5a-142">IT 安全流程和控制：云设计团队至少应对现有 IT 安全流程和控制进行更新，以便可转移到云中。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-142">IT Security processes and controls: At minimum, Cloud design teams should be refreshed on existing IT security processes and controls to carry those forward into the cloud.</span></span> <span data-ttu-id="6ce5a-143">在理想方案中，IT 安全团队的成员会在网络安全方面接受培训，并专门充当设计和实现团队的成员。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-143">In an ideal scenario, a member of the IT security team would be trained in cybersecurity and dedicated as a member of the design and implementation teams.</span></span>
* <span data-ttu-id="6ce5a-144">监视和审核：设计治理流程和工具时，请确保监视和审核解决方案包括安全风险或违规。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-144">Monitoring and Auditing: When designing governance processes and tooling, ensure that monitoring and auditing solutions include security risks or violations.</span></span>

> [!NOTE]
> <span data-ttu-id="6ce5a-145">技术债务泄露：本主题缺少可操作的后续步骤。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-145">Technical Debt disclosure: This topic lacks actionable next steps.</span></span> <span data-ttu-id="6ce5a-146">随着时间的推移，附加文章将扩展此主题。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-146">Addition articles will expand on this topic over time.</span></span> <span data-ttu-id="6ce5a-147">[Azure 的受信任云](https://azure.microsoft.com/overview/trusted-cloud/)提供了有关云安全的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="6ce5a-147">More detailed information about Cloud Security is available from [Azure's Trusted Cloud](https://azure.microsoft.com/overview/trusted-cloud/).</span></span> <span data-ttu-id="6ce5a-148">改进组织安全状况的方法可以在[云安全服务目录](https://www.microsoft.com/security/information-protection)中找到</span><span class="sxs-lookup"><span data-stu-id="6ce5a-148">Approaches to improving your organizations security posture can be found in the [Cloud Security Service Catalog](https://www.microsoft.com/security/information-protection)</span></span>