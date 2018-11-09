---
title: 简单的企业集成体系结构模式 - Azure Integration Services
description: 本体系结构参考演示如何使用 Azure 逻辑应用和 Azure API 管理来实现一个简单的企业集成模式
services: logic-apps
author: mattfarm
ms.author: mattfarm
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.date: 10/25/2018
ms.openlocfilehash: 15349aad4e7bc1a13337259fc933e1e11e252747
ms.sourcegitcommit: 2ae794de13c45cf24ad60d4f4dbb193c25944eff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50003569"
---
# <a name="simple-enterprise-integration"></a><span data-ttu-id="30943-103">简单企业集成</span><span class="sxs-lookup"><span data-stu-id="30943-103">Simple enterprise integration</span></span>

<span data-ttu-id="30943-104">本引用体系结构使用 [Azure Integration Services][integration-services] 来协调对企业后端系统的调用。</span><span class="sxs-lookup"><span data-stu-id="30943-104">This reference architecture uses [Azure Integration Services][integration-services] to orchestrate calls to enterprise backend systems.</span></span> <span data-ttu-id="30943-105">后端系统可能包括软件即服务 (SaaS) 系统、Azure 服务以及企业中现有的 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="30943-105">The backend systems may include software as a service (SaaS) systems, Azure services, and existing web services in your enterprise.</span></span>

<span data-ttu-id="30943-106">Azure Integration Services 是用于集成应用程序和数据的服务的集合。</span><span class="sxs-lookup"><span data-stu-id="30943-106">Azure Integration Services is a collection of services for integrating applications and data.</span></span> <span data-ttu-id="30943-107">本体系结构使用这其中的两种服务：用于协调工作流的[逻辑应用][logic-apps]，以及用于创建 API 目录的 [API 管理][apim]。</span><span class="sxs-lookup"><span data-stu-id="30943-107">This architecture uses two of those services: [Logic Apps][logic-apps] to orchestrate workflows, and [API Management][apim] to create catalogs of APIs.</span></span>

![体系结构图 - 简单的企业集成](./_images/simple-enterprise-integration.png)

## <a name="architecture"></a><span data-ttu-id="30943-109">体系结构</span><span class="sxs-lookup"><span data-stu-id="30943-109">Architecture</span></span>

<span data-ttu-id="30943-110">此体系结构具有以下组件：</span><span class="sxs-lookup"><span data-stu-id="30943-110">The architecture has the following components:</span></span>

- <span data-ttu-id="30943-111">**后端系统**。</span><span class="sxs-lookup"><span data-stu-id="30943-111">**Backend systems**.</span></span> <span data-ttu-id="30943-112">在上图的右侧是企业部署的或依赖的各种后端系统。</span><span class="sxs-lookup"><span data-stu-id="30943-112">On the right-hand side of the diagram are the various backend systems that the enterprise has deployed or relies on.</span></span> <span data-ttu-id="30943-113">其中可能包括 SaaS 系统、其他 Azure 服务或公开 REST 或 SOAP 终结点的 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="30943-113">These might include SaaS systems, other Azure services, or web services that expose REST or SOAP endpoints.</span></span>

- <span data-ttu-id="30943-114">**Azure 逻辑应用**。</span><span class="sxs-lookup"><span data-stu-id="30943-114">**Azure Logic Apps**.</span></span> <span data-ttu-id="30943-115">[逻辑应用][logic-apps]是一种用于生成企业工作流的无服务器平台，企业工作流可集成应用程序、数据和服务。</span><span class="sxs-lookup"><span data-stu-id="30943-115">[Logic Apps][logic-apps] is a serverless platform for building enterprise workflows that integrate applications, data, and services.</span></span> <span data-ttu-id="30943-116">在本体系结构中，逻辑应用由 HTTP 请求触发。</span><span class="sxs-lookup"><span data-stu-id="30943-116">In this architecture, the logic apps are triggered by HTTP requests.</span></span> <span data-ttu-id="30943-117">也可嵌套工作流，以便实现更复杂的业务流程。</span><span class="sxs-lookup"><span data-stu-id="30943-117">You can also nest workflows for more complex orchestration.</span></span> <span data-ttu-id="30943-118">逻辑应用使用[连接器][logic-apps-connectors]与常用的服务集成。</span><span class="sxs-lookup"><span data-stu-id="30943-118">Logic Apps uses [connectors][logic-apps-connectors] to integrate with commonly used services.</span></span> <span data-ttu-id="30943-119">逻辑应用提供数百个连接器，但你可以创建自定义连接器。</span><span class="sxs-lookup"><span data-stu-id="30943-119">Logic Apps offers hundreds of connectors, and you can create custom connectors.</span></span>

- <span data-ttu-id="30943-120">**Azure API 管理**。</span><span class="sxs-lookup"><span data-stu-id="30943-120">**Azure API Management**.</span></span> <span data-ttu-id="30943-121">[API 管理][apim]是用于发布 HTTP API 目录的托管服务，可以促进重复使用和可发现性。</span><span class="sxs-lookup"><span data-stu-id="30943-121">[API Management][apim] is a managed service for publishing catalogs of HTTP APIs, to promote re-use and discoverability.</span></span> <span data-ttu-id="30943-122">API 管理包含两个相关的组件：</span><span class="sxs-lookup"><span data-stu-id="30943-122">API Management consists of two related components:</span></span>

    - <span data-ttu-id="30943-123">**API 网关**。</span><span class="sxs-lookup"><span data-stu-id="30943-123">**API gateway**.</span></span> <span data-ttu-id="30943-124">API 网关接受 HTTP 调用并将其路由到后端。</span><span class="sxs-lookup"><span data-stu-id="30943-124">The API gateway accepts HTTP calls and routes them to the backend.</span></span> 

    - <span data-ttu-id="30943-125">**开发人员门户**。</span><span class="sxs-lookup"><span data-stu-id="30943-125">**Developer portal**.</span></span> <span data-ttu-id="30943-126">Azure API 管理的每个实例都可以访问[开发人员门户][apim-dev-portal]。</span><span class="sxs-lookup"><span data-stu-id="30943-126">Each instance of Azure API Management provides access to a [developer portal][apim-dev-portal].</span></span> <span data-ttu-id="30943-127">开发人员可以通过此门户访问有关 API 调用的文档和代码示例。</span><span class="sxs-lookup"><span data-stu-id="30943-127">This portal gives your developers access to documentation and code samples for calling the APIs.</span></span> <span data-ttu-id="30943-128">还可以在开发人员门户中测试 API。</span><span class="sxs-lookup"><span data-stu-id="30943-128">You can also test APIs in the developer portal.</span></span>

    <span data-ttu-id="30943-129">在本体系结构中，可以通过[导入逻辑应用][apim-logic-app]作为 API 来生成复合 API。</span><span class="sxs-lookup"><span data-stu-id="30943-129">In this architecture, composite APIs are built by [importing logic apps][apim-logic-app] as APIs.</span></span> <span data-ttu-id="30943-130">也可导入现有的 Web 服务，方法是[导入 OpenAPI][apim-openapi] (Swagger) 规范或从 WSDL 规范[导入 SOAP API][apim-soap]。</span><span class="sxs-lookup"><span data-stu-id="30943-130">You can also import existing web services by [importing OpenAPI][apim-openapi] (Swagger) specifications or [importing SOAP APIs][apim-soap] from WSDL specifications.</span></span> 

    <span data-ttu-id="30943-131">API 网关用于将前端客户端与后端分离。</span><span class="sxs-lookup"><span data-stu-id="30943-131">The API gateway helps to decouple front-end clients from the back end.</span></span> <span data-ttu-id="30943-132">例如，它可以重新编写 URL 或在请求抵达后端之前转换请求。</span><span class="sxs-lookup"><span data-stu-id="30943-132">For example, it can rewrite URLs, or transform requests before they reach the backend.</span></span> <span data-ttu-id="30943-133">它还处理许多跨领域问题，例如身份验证、跨域资源共享 (CORS) 支持以及响应缓存。</span><span class="sxs-lookup"><span data-stu-id="30943-133">It also handles many cross-cutting concerns such as authentication, cross-origin resource sharing (CORS) support, and response caching.</span></span>

- <span data-ttu-id="30943-134">**Azure DNS**。</span><span class="sxs-lookup"><span data-stu-id="30943-134">**Azure DNS**.</span></span> <span data-ttu-id="30943-135">[Azure DNS][dns] 是 DNS 域的托管服务。</span><span class="sxs-lookup"><span data-stu-id="30943-135">[Azure DNS][dns] is a hosting service for DNS domains.</span></span> <span data-ttu-id="30943-136">Azure DNS 使用 Microsoft Azure 基础结构提供名称解析。</span><span class="sxs-lookup"><span data-stu-id="30943-136">Azure DNS provides name resolution by using the Microsoft Azure infrastructure.</span></span> <span data-ttu-id="30943-137">通过在 Azure 中托管域，可以使用与其他 Azure 服务相同的凭据、API、工具和计费来管理 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="30943-137">By hosting your domains in Azure, you can manage your DNS records by using the same credentials, APIs, tools, and billing that you use for your other Azure services.</span></span> <span data-ttu-id="30943-138">若要使用自定义域名（例如 contoso.com），请创建可将自定义域名映射到 IP 地址的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="30943-138">To use a custom domain name, such as contoso.com, create DNS records that map the custom domain name to the IP address.</span></span> <span data-ttu-id="30943-139">有关详细信息，请参阅[在 API 管理中配置自定义域名][apim-domain]。</span><span class="sxs-lookup"><span data-stu-id="30943-139">For more information, see [Configure a custom domain name in API Management][apim-domain].</span></span>

- <span data-ttu-id="30943-140">**Azure Active Directory (Azure AD)**。</span><span class="sxs-lookup"><span data-stu-id="30943-140">**Azure Active Directory (Azure AD)**.</span></span> <span data-ttu-id="30943-141">使用 [Azure AD][aad] 对调用 API 网关的客户端进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="30943-141">Use [Azure AD][aad] to authenticate clients that call the API gateway.</span></span> <span data-ttu-id="30943-142">Azure AD 支持 OpenID Connect (OIDC) 协议。</span><span class="sxs-lookup"><span data-stu-id="30943-142">Azure AD supports the OpenID Connect (OIDC) protocol.</span></span> <span data-ttu-id="30943-143">客户端从 Azure AD 获取访问令牌，API 网关在[验证令牌][apim-jwt]后对请求授权。</span><span class="sxs-lookup"><span data-stu-id="30943-143">Clients obtain an access token from Azure AD, and API Gateway [validates the token][apim-jwt] to authorize the request.</span></span> <span data-ttu-id="30943-144">使用标准层或高级层 API 管理时，Azure AD 也可确保开发人员门户的访问安全性。</span><span class="sxs-lookup"><span data-stu-id="30943-144">When using the Standard or Premium tier of API Management, Azure AD can also secure access to the developer portal.</span></span>

## <a name="recommendations"></a><span data-ttu-id="30943-145">建议</span><span class="sxs-lookup"><span data-stu-id="30943-145">Recommendations</span></span>

<span data-ttu-id="30943-146">你的具体要求可能与此处显示的通用体系结构不同。</span><span class="sxs-lookup"><span data-stu-id="30943-146">Your specific requirements might differ from the generic architecture shown here.</span></span> <span data-ttu-id="30943-147">请使用本部分中的建议作为入手点。</span><span class="sxs-lookup"><span data-stu-id="30943-147">Use the recommendations in this section as a starting point.</span></span>

### <a name="api-management"></a><span data-ttu-id="30943-148">API 管理</span><span class="sxs-lookup"><span data-stu-id="30943-148">API Management</span></span>

<span data-ttu-id="30943-149">使用 API 管理基本层、标准层或高级层。</span><span class="sxs-lookup"><span data-stu-id="30943-149">Use the API Management Basic, Standard, or Premium tiers.</span></span> <span data-ttu-id="30943-150">这些层提供生产服务级别协议 (SLA)，并支持 Azure 区域中的横向扩展。</span><span class="sxs-lookup"><span data-stu-id="30943-150">These tiers offer a production service level agreement (SLA) and support scale out within the Azure region.</span></span> <span data-ttu-id="30943-151">API 管理的吞吐量容量以单位来度量。</span><span class="sxs-lookup"><span data-stu-id="30943-151">Throughput capacity for API Management is measured in *units*.</span></span> <span data-ttu-id="30943-152">每个定价层的横向扩展存在上限。高级层还支持跨多个 Azure 区域横向扩展。</span><span class="sxs-lookup"><span data-stu-id="30943-152">Each pricing tier has a maximum scale out. The Premium tier also supports scale out across multiple Azure regions.</span></span> <span data-ttu-id="30943-153">请根据功能集和所需的吞吐量级别选择层。</span><span class="sxs-lookup"><span data-stu-id="30943-153">Choose your tier based on your feature set and the level of required throughput.</span></span> <span data-ttu-id="30943-154">有关详细信息，请参阅 [API 管理定价][apim-pricing]和 [Azure API 管理实例的容量][apim-capacity]。</span><span class="sxs-lookup"><span data-stu-id="30943-154">For more information, see [API Management pricing][apim-pricing] and [Capacity of an Azure API Management instance][apim-capacity].</span></span>

<span data-ttu-id="30943-155">每个 Azure API 管理实例都有一个默认的域名，它是 `azure-api.net` 的子域，例如 `contoso.azure-api.net`。</span><span class="sxs-lookup"><span data-stu-id="30943-155">Each Azure API Management instance has a default domain name, which is a subdomain of `azure-api.net` &mdash for example, `contoso.azure-api.net`.</span></span> <span data-ttu-id="30943-156">考虑为组织配置[自定义域][apim-domain]。</span><span class="sxs-lookup"><span data-stu-id="30943-156">Consider configuring a [custom domain][apim-domain] for your organization.</span></span>

### <a name="logic-apps"></a><span data-ttu-id="30943-157">逻辑应用</span><span class="sxs-lookup"><span data-stu-id="30943-157">Logic Apps</span></span> 

<span data-ttu-id="30943-158">逻辑应用最适合不需要低延迟的场景。</span><span class="sxs-lookup"><span data-stu-id="30943-158">Logic Apps works best in scenarios that don't require low latency.</span></span> <span data-ttu-id="30943-159">例如，逻辑应用最适合异步或运行时间适中的 API 调用。</span><span class="sxs-lookup"><span data-stu-id="30943-159">For example, Logic Apps works best for asynchronous or semi long-running API calls.</span></span> <span data-ttu-id="30943-160">如果需要保证低延迟（例如，某个调用会导致用户界面停滞），请使用其他技术来实现 API 或操作。</span><span class="sxs-lookup"><span data-stu-id="30943-160">If low latency is required, for example, a call that blocks a user interface, implement your API or operation by using a different technology.</span></span> <span data-ttu-id="30943-161">例如，使用 Azure Functions 或通过 Azure 应用服务部署的 Web API。</span><span class="sxs-lookup"><span data-stu-id="30943-161">For example, use Azure Functions or a Web API that you deploy by using Azure App Service.</span></span> <span data-ttu-id="30943-162">对于 API 使用者，请优先 API 管理而不是 API。</span><span class="sxs-lookup"><span data-stu-id="30943-162">Use API Management to front the API to your API consumers.</span></span>

### <a name="region"></a><span data-ttu-id="30943-163">区域</span><span class="sxs-lookup"><span data-stu-id="30943-163">Region</span></span>

<span data-ttu-id="30943-164">若要尽量降低网络延迟，可将 API 管理和逻辑应用置于同一区域。</span><span class="sxs-lookup"><span data-stu-id="30943-164">To minimize network latency, put API Management and Logic Apps in the same region.</span></span> <span data-ttu-id="30943-165">一般情况下，请选择离用户最近（或离后端服务最近）的区域。</span><span class="sxs-lookup"><span data-stu-id="30943-165">In general, choose the region that's closest to your users (or closest to your backend services).</span></span>

<span data-ttu-id="30943-166">资源组也有一个区域。</span><span class="sxs-lookup"><span data-stu-id="30943-166">The resource group also has a region.</span></span> <span data-ttu-id="30943-167">此区域指定了部署元数据的存储位置，以及执行部署模板的位置。</span><span class="sxs-lookup"><span data-stu-id="30943-167">This region specifies where to store deployment metadata and where to execute the deployment template.</span></span> <span data-ttu-id="30943-168">为了提高部署期间的可用性，请将资源组和资源放在同一区域。</span><span class="sxs-lookup"><span data-stu-id="30943-168">To improve availability during deployment, put the resource group and resources in the same region.</span></span>

## <a name="scalability-considerations"></a><span data-ttu-id="30943-169">可伸缩性注意事项</span><span class="sxs-lookup"><span data-stu-id="30943-169">Scalability considerations</span></span>

<span data-ttu-id="30943-170">为了提高 API 管理的可伸缩性，请添加[缓存策略][apim-caching]（如果适用）。</span><span class="sxs-lookup"><span data-stu-id="30943-170">To increase the scalability of API Management, add [caching policies][apim-caching] where appropriate.</span></span> <span data-ttu-id="30943-171">缓存还有助于减少后端服务的负载。</span><span class="sxs-lookup"><span data-stu-id="30943-171">Caching also helps reduce the load on back-end services.</span></span>

<span data-ttu-id="30943-172">若要提高容量，可在 Azure 区域中横向扩展 Azure API 管理基本层、标准层和高级层。</span><span class="sxs-lookup"><span data-stu-id="30943-172">To offer greater capacity, you can scale out Azure API Management Basic, Standard, and Premium tiers in an Azure region.</span></span> <span data-ttu-id="30943-173">若要分析服务的使用情况，请在“指标”菜单中选择“容量指标”选项，然后相应地纵向扩展或缩减。</span><span class="sxs-lookup"><span data-stu-id="30943-173">To analyze the usage for your service, on the **Metrics** menu, select the **Capacity Metric** option and then scale up or scale down as appropriate.</span></span> <span data-ttu-id="30943-174">升级或缩放过程可能需要 15 到 45 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="30943-174">The upgrade or scale process can take from 15 to 45 minutes to apply.</span></span>

<span data-ttu-id="30943-175">有关缩放 API 管理服务的建议：</span><span class="sxs-lookup"><span data-stu-id="30943-175">Recommendations for scaling an API Management service:</span></span>

- <span data-ttu-id="30943-176">缩放时请考虑流量模式。</span><span class="sxs-lookup"><span data-stu-id="30943-176">Consider traffic patterns when scaling.</span></span> <span data-ttu-id="30943-177">采用较高易失性流量模式的客户需要更多的容量。</span><span class="sxs-lookup"><span data-stu-id="30943-177">Customers with more volatile traffic patterns need more capacity.</span></span>

- <span data-ttu-id="30943-178">如果容量一贯超过 66%，则可能表示需要纵向扩展。</span><span class="sxs-lookup"><span data-stu-id="30943-178">Consistent capacity that's greater than 66% might indicate a need to scale up.</span></span>

- <span data-ttu-id="30943-179">如果容量一贯低于 20%，则可能表示能够缩减。</span><span class="sxs-lookup"><span data-stu-id="30943-179">Consistent capacity that's under 20% might indicate an opportunity to scale down.</span></span>

- <span data-ttu-id="30943-180">在生产环境中启用负载之前，请始终使用有代表性的负载对 API 管理服务进行负载测试。</span><span class="sxs-lookup"><span data-stu-id="30943-180">Before you enable the load in production, always load-test your API Management service with a representative load.</span></span>

<span data-ttu-id="30943-181">使用高级层时，可以跨多个 Azure 区域缩放 API 管理实例。</span><span class="sxs-lookup"><span data-stu-id="30943-181">With the Premium tier, you can scale an API Management instance across multiple Azure regions.</span></span> <span data-ttu-id="30943-182">这样可以让 API 管理有资格获得更高的 SLA，让你可以在多个区域靠近用户的位置预配服务。</span><span class="sxs-lookup"><span data-stu-id="30943-182">This makes API Management eligible for a higher SLA, and lets you provision services near users in multiple regions.</span></span>


<span data-ttu-id="30943-183">逻辑应用的无服务器模型意味着管理员无需规划服务可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="30943-183">The Logic Apps serverless model means administrators don't have to plan for service scalability.</span></span> <span data-ttu-id="30943-184">服务会根据需求自动缩放。</span><span class="sxs-lookup"><span data-stu-id="30943-184">The service automatically scales to meet demand.</span></span>

## <a name="availability-considerations"></a><span data-ttu-id="30943-185">可用性注意事项</span><span class="sxs-lookup"><span data-stu-id="30943-185">Availability considerations</span></span>

<span data-ttu-id="30943-186">查看每个服务的 SLA：</span><span class="sxs-lookup"><span data-stu-id="30943-186">Review the SLA for each service:</span></span>

- <span data-ttu-id="30943-187">[API 管理 SLA][apim-sla]</span><span class="sxs-lookup"><span data-stu-id="30943-187">[API Management SLA][apim-sla]</span></span>
- <span data-ttu-id="30943-188">[逻辑应用 SLA][logic-apps-sla]</span><span class="sxs-lookup"><span data-stu-id="30943-188">[Logic Apps SLA][logic-apps-sla]</span></span>

<span data-ttu-id="30943-189">如果在使用高级层时跨至少两个区域来部署 API 管理，则有资格获得更高的 SLA。</span><span class="sxs-lookup"><span data-stu-id="30943-189">If deploy API Management across two or more regions with Premium tier, it is eligible for a higher SLA.</span></span> <span data-ttu-id="30943-190">请参阅 [API 管理定价][apim-pricing]。</span><span class="sxs-lookup"><span data-stu-id="30943-190">See [API Management pricing][apim-pricing].</span></span>

### <a name="backups"></a><span data-ttu-id="30943-191">备份</span><span class="sxs-lookup"><span data-stu-id="30943-191">Backups</span></span>

<span data-ttu-id="30943-192">定期[备份][apim-backup] API 管理配置。</span><span class="sxs-lookup"><span data-stu-id="30943-192">Regularly [back up][apim-backup] your API Management configuration.</span></span> <span data-ttu-id="30943-193">将备份文件存储在不同于服务部署区域的某个位置或 Azure 区域。</span><span class="sxs-lookup"><span data-stu-id="30943-193">Store your backup files in a location or Azure region that differs from the region where the service is deployed.</span></span> <span data-ttu-id="30943-194">根据 [RTO][rto] 选择灾难恢复策略：</span><span class="sxs-lookup"><span data-stu-id="30943-194">Based on your [RTO][rto], choose a disaster recovery strategy:</span></span>

* <span data-ttu-id="30943-195">在灾难恢复事件中，预配新的 API 管理实例，将备份还原到新实例，并重新指向 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="30943-195">In a disaster recovery event, provision a new API Management instance, restore the backup to the new instance, and repoint the DNS records.</span></span>

* <span data-ttu-id="30943-196">在另一 Azure 区域中保留 API 管理服务的被动实例。</span><span class="sxs-lookup"><span data-stu-id="30943-196">Keep a passive instance of the API Management service in another Azure region.</span></span> <span data-ttu-id="30943-197">定期将备份还原到该实例，使之与主动服务同步。</span><span class="sxs-lookup"><span data-stu-id="30943-197">Regularly restore backups to that instance, to keep it in sync with the active service.</span></span> <span data-ttu-id="30943-198">若要在发生灾难恢复事件期间还原服务，只需重新指向 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="30943-198">To restore the service during a disaster recovery event, you need only repoint the DNS records.</span></span> <span data-ttu-id="30943-199">此方法会产生额外的成本，因为需为被动实例付费，但会缩短恢复时间。</span><span class="sxs-lookup"><span data-stu-id="30943-199">This approach incurs additional cost because you are paying for the passive instance, but reduces the time to recover.</span></span> 

<span data-ttu-id="30943-200">对于逻辑应用，建议使用配置即代码方法进行备份和还原。</span><span class="sxs-lookup"><span data-stu-id="30943-200">For logic apps, we recommend a configuration-as-code approach to backup and restoring.</span></span> <span data-ttu-id="30943-201">由于逻辑应用无服务器，因此可以通过 Azure 资源管理器模板快速地重新创建它们。</span><span class="sxs-lookup"><span data-stu-id="30943-201">Because logic apps are serverless, you can quickly recreate them from Azure Resource Manager templates.</span></span> <span data-ttu-id="30943-202">请将模板保存在源代码管理中，并将模板与持续集成/持续部署 (CI/CD) 过程相集成。</span><span class="sxs-lookup"><span data-stu-id="30943-202">Save the templates in source control, integrate the templates with your continuous integration/continuous deployment (CI/CD) process.</span></span> <span data-ttu-id="30943-203">在灾难恢复事件中，请将模板部署到新区域。</span><span class="sxs-lookup"><span data-stu-id="30943-203">In a disaster recovery event, deploy the template to a new region.</span></span>

<span data-ttu-id="30943-204">如果将逻辑应用部署到另一区域，请在 API 管理中更新配置。</span><span class="sxs-lookup"><span data-stu-id="30943-204">If you deploy a logic app to a different region, update the configuration in API Management.</span></span> <span data-ttu-id="30943-205">可以使用一个基本的 PowerShell 脚本来更新 API 的**后端**属性。</span><span class="sxs-lookup"><span data-stu-id="30943-205">You can update the API's **Backend** property by using a basic PowerShell script.</span></span>

## <a name="manageability-considerations"></a><span data-ttu-id="30943-206">可管理性注意事项</span><span class="sxs-lookup"><span data-stu-id="30943-206">Manageability considerations</span></span>

<span data-ttu-id="30943-207">为生产、开发和测试环境创建单独的资源组。</span><span class="sxs-lookup"><span data-stu-id="30943-207">Create separate resource groups for production, development, and test environments.</span></span> <span data-ttu-id="30943-208">使用单独的资源组可以更方便地管理部署、删除测试部署，以及分配访问权限。</span><span class="sxs-lookup"><span data-stu-id="30943-208">Separate resource groups make it easier to manage deployments, delete test deployments, and assign access rights.</span></span>

<span data-ttu-id="30943-209">将资源分配到资源组时，请考虑以下因素：</span><span class="sxs-lookup"><span data-stu-id="30943-209">When you assign resources to resource groups, consider these factors:</span></span>

* <span data-ttu-id="30943-210">**生命周期**。</span><span class="sxs-lookup"><span data-stu-id="30943-210">**Lifecycle**.</span></span> <span data-ttu-id="30943-211">一般情况下，应将具有相同生命周期的资源放入同一个资源组。</span><span class="sxs-lookup"><span data-stu-id="30943-211">In general, put resources that have the same lifecycle in the same resource group.</span></span>

* <span data-ttu-id="30943-212">**访问**。</span><span class="sxs-lookup"><span data-stu-id="30943-212">**Access**.</span></span> <span data-ttu-id="30943-213">若要对组中的资源应用访问策略，可以使用[基于角色的访问控制][rbac] (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="30943-213">To apply access policies to the resources in a group, you can use [role-based access control][rbac] (RBAC).</span></span>

* <span data-ttu-id="30943-214">**计费**。</span><span class="sxs-lookup"><span data-stu-id="30943-214">**Billing**.</span></span> <span data-ttu-id="30943-215">可以查看资源组的累计成本。</span><span class="sxs-lookup"><span data-stu-id="30943-215">You can view rollup costs for the resource group.</span></span>

* <span data-ttu-id="30943-216">**API 管理的定价层**。</span><span class="sxs-lookup"><span data-stu-id="30943-216">**Pricing tier for API Management**.</span></span> <span data-ttu-id="30943-217">对开发和测试环境使用开发人员层。</span><span class="sxs-lookup"><span data-stu-id="30943-217">Use the Developer tier for development and test environments.</span></span> <span data-ttu-id="30943-218">为了尽量降低预生产期间的成本，请部署生产环境的副本、运行测试，然后关闭。</span><span class="sxs-lookup"><span data-stu-id="30943-218">To minimize costs during preproduction, deploy a replica of your production environment, run your tests, and then shut down.</span></span>

### <a name="deployment"></a><span data-ttu-id="30943-219">部署</span><span class="sxs-lookup"><span data-stu-id="30943-219">Deployment</span></span>

<span data-ttu-id="30943-220">使用 [Azure 资源管理器模板][arm]部署 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="30943-220">Use [Azure Resource Manager templates][arm] to deploy the Azure resources.</span></span> <span data-ttu-id="30943-221">使用模板可以通过 PowerShell 或 Azure CLI 更轻松地自动完成部署。</span><span class="sxs-lookup"><span data-stu-id="30943-221">Templates make it easier to automate deployments using PowerShell or the Azure CLI.</span></span>

<span data-ttu-id="30943-222">将 API 管理和任何单个逻辑应用放在其自身独立的资源管理器模板中。</span><span class="sxs-lookup"><span data-stu-id="30943-222">Put API Management and any individual logic apps in their own separate Resource Manager templates.</span></span> <span data-ttu-id="30943-223">使用独立的模板可将资源存储在源代码管理系统中。</span><span class="sxs-lookup"><span data-stu-id="30943-223">By using separate templates, you can store the resources in source control systems.</span></span> <span data-ttu-id="30943-224">然后，可以在持续集成/持续部署 (CI/CD) 过程中统一或者逐个部署这些模板。</span><span class="sxs-lookup"><span data-stu-id="30943-224">You can then deploy these templates together or individually as part of a continuous integration/continuous deployment (CI/CD) process.</span></span>

### <a name="versions"></a><span data-ttu-id="30943-225">版本</span><span class="sxs-lookup"><span data-stu-id="30943-225">Versions</span></span>

<span data-ttu-id="30943-226">每当更改逻辑应用的配置或者通过资源管理器模板部署更新时，Azure 都会保留该版本的副本，并保留具有运行历史记录的所有版本。</span><span class="sxs-lookup"><span data-stu-id="30943-226">Each time you change a logic app's configuration or deploy an update through a Resource Manager template, Azure keeps a copy of that version and keeps all versions that have a run history.</span></span> <span data-ttu-id="30943-227">可以使用这些版本来跟踪历史更改，或者将某个版本提升为逻辑应用的当前配置。</span><span class="sxs-lookup"><span data-stu-id="30943-227">You can use these versions to track historical changes or promote a version as the logic app's current configuration.</span></span> <span data-ttu-id="30943-228">例如，可以将逻辑应用回退到以前的版本。</span><span class="sxs-lookup"><span data-stu-id="30943-228">For example, you can roll back a logic app to a previous version.</span></span>

<span data-ttu-id="30943-229">API 管理支持两个不同但互补的版本控制概念：</span><span class="sxs-lookup"><span data-stu-id="30943-229">API Management supports two distinct but complementary versioning concepts:</span></span>

* <span data-ttu-id="30943-230">版本：API 使用者可以根据需要选择 API 版本（例如 v1、v2、beta 或 production）。</span><span class="sxs-lookup"><span data-stu-id="30943-230">*Versions* allow API consumers to choose an API version based on their needs, for example, v1, v2, beta, or production.</span></span>

* <span data-ttu-id="30943-231">修订版：API 管理员可以在 API 中进行非重大更改并部署这些更改。另外还可以提供更改日志，将所做的更改告知 API 使用者。</span><span class="sxs-lookup"><span data-stu-id="30943-231">*Revisions* allow API administrators to make non-breaking changes in an API and deploy those changes, along with a change log to inform API consumers about the changes.</span></span>

<span data-ttu-id="30943-232">可在开发环境中创建修订版，并使用资源管理器模板在其他环境中部署此项更改。</span><span class="sxs-lookup"><span data-stu-id="30943-232">You can make a revision in a development environment and deploy that change in other environments by using Resource Manager templates.</span></span> <span data-ttu-id="30943-233">有关详细信息，请参阅[发布 API 的多个版本][apim-versions]</span><span class="sxs-lookup"><span data-stu-id="30943-233">For more information, see [Publish multiple versions of your API][apim-versions]</span></span>

<span data-ttu-id="30943-234">也可在将某个 API 指定为“当前”版本并提供给用户访问之前，使用修订版来测试该 API。</span><span class="sxs-lookup"><span data-stu-id="30943-234">You can also use revisions to test an API before making the changes current and accessible to users.</span></span> <span data-ttu-id="30943-235">但是，建议不要使用此方法进行负载测试或集成测试。</span><span class="sxs-lookup"><span data-stu-id="30943-235">However, this method isn't recommended for load testing or integration testing.</span></span> <span data-ttu-id="30943-236">应改用独立的测试环境或预生产环境。</span><span class="sxs-lookup"><span data-stu-id="30943-236">Instead, use separate test or preproduction environments.</span></span>

## <a name="diagnostics-and-monitoring"></a><span data-ttu-id="30943-237">诊断和监控</span><span class="sxs-lookup"><span data-stu-id="30943-237">Diagnostics and monitoring</span></span>

<span data-ttu-id="30943-238">在 API 管理和逻辑应用中使用 [Azure Monitor][monitor] 进行操作监视。</span><span class="sxs-lookup"><span data-stu-id="30943-238">Use [Azure Monitor][monitor] for operational monitoring in both API Management and Logic Apps.</span></span> <span data-ttu-id="30943-239">Azure Monitor 根据为每个服务配置的指标提供信息，默认已启用。</span><span class="sxs-lookup"><span data-stu-id="30943-239">Azure Monitor provides information based on the metrics configured for each service and is enabled by default.</span></span> <span data-ttu-id="30943-240">有关详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="30943-240">For more information, see:</span></span>

- <span data-ttu-id="30943-241">[监视已发布的 API][apim-monitor]</span><span class="sxs-lookup"><span data-stu-id="30943-241">[Monitor published APIs][apim-monitor]</span></span>
- <span data-ttu-id="30943-242">[针对 Azure 逻辑应用监视状态、设置诊断日志记录，并启用警报][logic-apps-monitor]</span><span class="sxs-lookup"><span data-stu-id="30943-242">[Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps][logic-apps-monitor]</span></span>

<span data-ttu-id="30943-243">每个服务还提供以下选项：</span><span class="sxs-lookup"><span data-stu-id="30943-243">Each service also has these options:</span></span>

* <span data-ttu-id="30943-244">若要进行更深入的分析和仪表板显示，请将逻辑应用日志发送到 [Azure Log Analytics][logic-apps-log-analytics]。</span><span class="sxs-lookup"><span data-stu-id="30943-244">For deeper analysis and dashboarding, send Logic Apps logs to [Azure Log Analytics][logic-apps-log-analytics].</span></span>

* <span data-ttu-id="30943-245">若要进行 DevOps 监视，请为 API 管理配置 Azure Application Insights。</span><span class="sxs-lookup"><span data-stu-id="30943-245">For DevOps monitoring, configure Azure Application Insights for API Management.</span></span>

* <span data-ttu-id="30943-246">API 管理支持[使用 Power BI 解决方案模板进行自定义 API 分析][apim-pbi]。</span><span class="sxs-lookup"><span data-stu-id="30943-246">API Management supports the [Power BI solution template for custom API analytics][apim-pbi].</span></span> <span data-ttu-id="30943-247">可以使用此解决方案模板来创建自己的分析解决方案。</span><span class="sxs-lookup"><span data-stu-id="30943-247">You can use this solution template for creating your own analytics solution.</span></span> <span data-ttu-id="30943-248">业务用户可在 Power BI 中查看报表。</span><span class="sxs-lookup"><span data-stu-id="30943-248">For business users, Power BI makes reports available.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="30943-249">安全注意事项</span><span class="sxs-lookup"><span data-stu-id="30943-249">Security considerations</span></span>

<span data-ttu-id="30943-250">下面是一些针对本体系结构的安全注意事项，虽然此列表并未完整描述所有的安全最佳做法：</span><span class="sxs-lookup"><span data-stu-id="30943-250">Although this list doesn't completely describe all security best practices, here are some security considerations that apply specifically to this architecture:</span></span>

* <span data-ttu-id="30943-251">Azure API 管理服务具有固定的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="30943-251">The Azure API Management service has a fixed public IP address.</span></span> <span data-ttu-id="30943-252">只有 API 管理的 IP 地址能调用逻辑应用终结点。</span><span class="sxs-lookup"><span data-stu-id="30943-252">Restrict access for calling Logic Apps endpoints to only the IP address of API Management.</span></span> <span data-ttu-id="30943-253">有关详细信息，请参阅[限制传入 IP 地址][logic-apps-restrict-ip]。</span><span class="sxs-lookup"><span data-stu-id="30943-253">For more information, see [Restrict incoming IP addresses][logic-apps-restrict-ip].</span></span>

* <span data-ttu-id="30943-254">为确保用户拥有适当的访问级别，请使用基于角色的访问控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="30943-254">To make sure users have appropriate access levels, use role-based access control (RBAC).</span></span>

* <span data-ttu-id="30943-255">使用 OAuth 或 OpenID Connect 保护 API 管理中的公共 API 终结点。</span><span class="sxs-lookup"><span data-stu-id="30943-255">Secure public API endpoints in API Management by using OAuth or OpenID Connect.</span></span> <span data-ttu-id="30943-256">若要保护公共 API 终结点，请配置标识提供者并添加 JSON Web 令牌 (JWT) 验证策略。</span><span class="sxs-lookup"><span data-stu-id="30943-256">To secure public API endpoints, configure an identity provider, and add a JSON Web Token (JWT) validation policy.</span></span> <span data-ttu-id="30943-257">有关详细信息，请参阅[结合 Azure Active Directory 和 API 管理使用 OAuth 2.0 保护 API][apim-oauth]。</span><span class="sxs-lookup"><span data-stu-id="30943-257">For more information, see [Protect an API by using OAuth 2.0 with Azure Active Directory and API Management][apim-oauth].</span></span>

* <span data-ttu-id="30943-258">使用相互身份验证证书从 API 管理连接到后端服务。</span><span class="sxs-lookup"><span data-stu-id="30943-258">Connect to back-end services from API Management by using mutual certificates.</span></span>

* <span data-ttu-id="30943-259">在 API 管理 API 上强制实施 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="30943-259">Enforce HTTPS on the API Management APIs.</span></span>

### <a name="storing-secrets"></a><span data-ttu-id="30943-260">存储机密</span><span class="sxs-lookup"><span data-stu-id="30943-260">Storing secrets</span></span>

<span data-ttu-id="30943-261">切勿将密码、访问密钥或连接字符串签入源代码管理。</span><span class="sxs-lookup"><span data-stu-id="30943-261">Never check passwords, access keys, or connection strings into source control.</span></span> <span data-ttu-id="30943-262">如果需要这些值，请使用适当的技术保护和部署这些值。</span><span class="sxs-lookup"><span data-stu-id="30943-262">If these values are required, secure and deploy these values by using the appropriate techniques.</span></span> 

<span data-ttu-id="30943-263">如果逻辑应用所需的任何敏感值不能在连接器中创建，请将这些值存储在 Azure Key Vault 中，并从资源管理器模板引用它们。</span><span class="sxs-lookup"><span data-stu-id="30943-263">If a logic app requires any sensitive values that you can't create within a connector, store those values in Azure Key Vault and reference them from a Resource Manager template.</span></span> <span data-ttu-id="30943-264">请为每个环境使用部署模板参数和参数文件。</span><span class="sxs-lookup"><span data-stu-id="30943-264">Use deployment template parameters and parameter files for each environment.</span></span> <span data-ttu-id="30943-265">有关详细信息，请参阅[保护工作流中的参数和输入][logic-apps-secure]。</span><span class="sxs-lookup"><span data-stu-id="30943-265">For more information, see [Secure parameters and inputs within a workflow][logic-apps-secure].</span></span>

<span data-ttu-id="30943-266">API 管理使用称作“命名值”或“属性”的对象管理机密。</span><span class="sxs-lookup"><span data-stu-id="30943-266">API Management manages secrets by using objects called *named values* or *properties*.</span></span> <span data-ttu-id="30943-267">这些对象安全地存储可通过 API 管理策略访问的值。</span><span class="sxs-lookup"><span data-stu-id="30943-267">These objects securely store values that you can access through API Management policies.</span></span> <span data-ttu-id="30943-268">有关详细信息，请参阅[如何在 Azure API 管理策略中使用命名值][apim-properties]。</span><span class="sxs-lookup"><span data-stu-id="30943-268">For more information, see [How to use Named Values in Azure API Management policies][apim-properties].</span></span>

## <a name="cost-considerations"></a><span data-ttu-id="30943-269">成本注意事项</span><span class="sxs-lookup"><span data-stu-id="30943-269">Cost considerations</span></span>

<span data-ttu-id="30943-270">需要对所有运行的 API 管理实例付费。</span><span class="sxs-lookup"><span data-stu-id="30943-270">You are charged for all API Management instances when they are running.</span></span> <span data-ttu-id="30943-271">如果已纵向扩展，但始终不需要该性能级别，请手动进行纵向缩减，或者配置[自动缩放][apim-autoscale]。</span><span class="sxs-lookup"><span data-stu-id="30943-271">If you have scaled up and don't need that level of performance all the time, manually scale down or configure [autoscaling][apim-autoscale].</span></span>

<span data-ttu-id="30943-272">逻辑应用使用[无服务器](/azure/logic-apps/logic-apps-serverless-overview)模型。</span><span class="sxs-lookup"><span data-stu-id="30943-272">Logic Apps uses a [serverless](/azure/logic-apps/logic-apps-serverless-overview) model.</span></span> <span data-ttu-id="30943-273">根据操作和连接器执行计算费用。</span><span class="sxs-lookup"><span data-stu-id="30943-273">Billing is calculated based on action and connector execution.</span></span> <span data-ttu-id="30943-274">有关详细信息，请参阅[逻辑应用定价](https://azure.microsoft.com/pricing/details/logic-apps/)。</span><span class="sxs-lookup"><span data-stu-id="30943-274">For more information, see [Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/).</span></span> <span data-ttu-id="30943-275">目前，逻辑应用没有层方面的注意事项。</span><span class="sxs-lookup"><span data-stu-id="30943-275">Currently, there are no tier considerations for Logic Apps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30943-276">后续步骤</span><span class="sxs-lookup"><span data-stu-id="30943-276">Next steps</span></span>

* <span data-ttu-id="30943-277">了解[企业集成与队列和事件](/azure/logic-apps/logic-apps-architectures-enterprise-integration-with-queues-events)</span><span class="sxs-lookup"><span data-stu-id="30943-277">Learn about [enterprise integration with queues and events](/azure/logic-apps/logic-apps-architectures-enterprise-integration-with-queues-events)</span></span>

<!-- links -->

[aad]: /azure/active-directory
[apim]: /azure/api-management
[apim-autoscale]: /azure/api-management/api-management-howto-autoscale
[apim-backup]: /azure/api-management/api-management-howto-disaster-recovery-backup-restore
[apim-caching]: /azure/api-management/api-management-howto-cache
[apim-capacity]: /azure/api-management/api-management-capacity
[apim-dev-portal]: /azure/api-management/api-management-key-concepts#a-namedeveloper-portal-a-developer-portal
[apim-domain]: /azure/api-management/configure-custom-domain
[apim-jwt]: /azure/api-management/policies/authorize-request-based-on-jwt-claims
[apim-logic-app]: /azure/api-management/import-logic-app-as-api
[apim-monitor]: /azure/api-management/api-management-howto-use-azure-monitor
[apim-oauth]: /azure/api-management/api-management-howto-protect-backend-with-aad
[apim-openapi]: /azure/api-management/import-api-from-oas
[apim-pbi]: http://aka.ms/apimpbi
[apim-pricing]: https://azure.microsoft.com/pricing/details/api-management/
[apim-properties]: /azure/api-management/api-management-howto-properties
[apim-sla]: https://azure.microsoft.com/support/legal/sla/api-management/
[apim-soap]: /azure/api-management/import-soap-api
[apim-versions]: /azure/api-management/api-management-get-started-publish-versions
[arm]: /azure/azure-resource-manager/resource-group-authoring-templates
[dns]: /azure/dns/
[integration-services]: https://azure.microsoft.com/product-categories/integration/
[logic-apps]: /azure/logic-apps/logic-apps-overview
[logic-apps-connectors]: /azure/connectors/apis-list
[logic-apps-log-analytics]: /azure/logic-apps/logic-apps-monitor-your-logic-apps-oms
[logic-apps-monitor]: /azure/logic-apps/logic-apps-monitor-your-logic-apps
[logic-apps-restrict-ip]: /azure/logic-apps/logic-apps-securing-a-logic-app#restrict-incoming-ip-addresses
[logic-apps-secure]: /azure/logic-apps/logic-apps-securing-a-logic-app#secure-parameters-and-inputs-within-a-workflow
[logic-apps-sla]: https://azure.microsoft.com/support/legal/sla/logic-apps
[monitor]: /azure/azure-monitor/overview
[rbac]: /azure/role-based-access-control/overview
[rto]: ../../resiliency/index.md#rto-and-rpo