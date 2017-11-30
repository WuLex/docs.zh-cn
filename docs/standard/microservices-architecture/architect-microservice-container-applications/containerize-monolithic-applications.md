---
title: "Containerizing 整体应用程序"
description: "为容器化的.NET 应用程序的.NET 微服务体系结构 |Containerizing 整体应用程序"
keywords: "Docker, 微服务, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: 11e2c24403b9b61584e424696c844e00e5d34b03
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="containerizing-monolithic-applications"></a><span data-ttu-id="a56dc-104">Containerizing 整体应用程序</span><span class="sxs-lookup"><span data-stu-id="a56dc-104">Containerizing monolithic applications</span></span>

<span data-ttu-id="a56dc-105">你可能想要生成的单个、 monolithically 部署 web 应用程序或服务并将其部署为一个容器。</span><span class="sxs-lookup"><span data-stu-id="a56dc-105">You might want to build a single, monolithically deployed web application or service and deploy it as a container.</span></span> <span data-ttu-id="a56dc-106">应用程序本身可能不是内部整体，但结构化几个库、 组件或甚至层 （应用程序层、 域层、 数据访问层等）。</span><span class="sxs-lookup"><span data-stu-id="a56dc-106">The application itself might not be internally monolithic, but structured as several libraries, components, or even layers (application layer, domain layer, data-access layer, etc.).</span></span> <span data-ttu-id="a56dc-107">外部使用，但是，它是单个容器-单个进程、 单个 web 应用程序或单个服务。</span><span class="sxs-lookup"><span data-stu-id="a56dc-107">Externally, however, it is a single container—a single process, a single web application, or a single service.</span></span>

<span data-ttu-id="a56dc-108">若要管理此模型，你可以部署单个容器来表示应用程序。</span><span class="sxs-lookup"><span data-stu-id="a56dc-108">To manage this model, you deploy a single container to represent the application.</span></span> <span data-ttu-id="a56dc-109">若要向上扩展，只需添加对负载平衡器在前面的更多副本。</span><span class="sxs-lookup"><span data-stu-id="a56dc-109">To scale up, you just add more copies with a load balancer in front.</span></span> <span data-ttu-id="a56dc-110">为了简单起见来自于管理单个部署中的单个容器或 VM。</span><span class="sxs-lookup"><span data-stu-id="a56dc-110">The simplicity comes from managing a single deployment in a single container or VM.</span></span>

![](./media/image1.png)

<span data-ttu-id="a56dc-111">**图 4-1**。</span><span class="sxs-lookup"><span data-stu-id="a56dc-111">**Figure 4-1**.</span></span> <span data-ttu-id="a56dc-112">容器化的整体应用程序的体系结构示例</span><span class="sxs-lookup"><span data-stu-id="a56dc-112">Example of the architecture of a containerized monolithic application</span></span>

<span data-ttu-id="a56dc-113">图 4-1 中所示，可以在每个容器，包括多个组件、 库或内部的层。</span><span class="sxs-lookup"><span data-stu-id="a56dc-113">You can include multiple components, libraries, or internal layers in each container, as illustrated in Figure 4-1.</span></span> <span data-ttu-id="a56dc-114">但是，此整体模式可能与"容器做一件事，而不在一个进程中"，但可能容器原则冲突是某些情况下为确定。</span><span class="sxs-lookup"><span data-stu-id="a56dc-114">However, this monolithic pattern might conflict with the container principle “a container does one thing, and does it in one process”, but might be ok for some cases.</span></span>

<span data-ttu-id="a56dc-115">此方法的缺点中变得显而易见，如果应用程序的增长，需要进行调整。</span><span class="sxs-lookup"><span data-stu-id="a56dc-115">The downside of this approach becomes evident if the application grows, requiring it to scale.</span></span> <span data-ttu-id="a56dc-116">如果可以缩放整个应用程序，它不是真正的问题。</span><span class="sxs-lookup"><span data-stu-id="a56dc-116">If the entire application can scale, it is not really a problem.</span></span> <span data-ttu-id="a56dc-117">但是，在大多数情况下，应用程序只需几部分是，需要进行缩放外，其他组件时使用小于压点。</span><span class="sxs-lookup"><span data-stu-id="a56dc-117">However, in most cases, just a few parts of the application are the choke points that requiring scaling, while other components are used less.</span></span>

<span data-ttu-id="a56dc-118">例如，在典型的电子商务应用程序中，你可能需要缩放产品信息子系统，因为许多更多的客户浏览产品不是购买必需的许可证。</span><span class="sxs-lookup"><span data-stu-id="a56dc-118">For example, in a typical e-commerce application, you likely need to scale the product information subsystem, because many more customers browse products than purchase them.</span></span> <span data-ttu-id="a56dc-119">更多的客户使用他们的购物篮不是使用付款管道。</span><span class="sxs-lookup"><span data-stu-id="a56dc-119">More customers use their basket than use the payment pipeline.</span></span> <span data-ttu-id="a56dc-120">更少的客户添加注释，或查看其购买历史记录。</span><span class="sxs-lookup"><span data-stu-id="a56dc-120">Fewer customers add comments or view their purchase history.</span></span> <span data-ttu-id="a56dc-121">并且你可能有只有少量的员工组，需要管理内容和市场营销活动。</span><span class="sxs-lookup"><span data-stu-id="a56dc-121">And you might have only a handful of employees, that need to manage the content and marketing campaigns.</span></span> <span data-ttu-id="a56dc-122">如果缩放单一式设计，这些不同的任务的所有代码是部署多个时间，并且扩展在同一级。</span><span class="sxs-lookup"><span data-stu-id="a56dc-122">If you scale the monolithic design, all the code for these different tasks is deployed multiple times and scaled at the same grade.</span></span>

<span data-ttu-id="a56dc-123">有多种方法来缩放应用程序-水平重复，拆分的应用程序和分区的业务概念相似或数据的不同区域。</span><span class="sxs-lookup"><span data-stu-id="a56dc-123">There are multiple ways to scale an application—horizontal duplication, splitting different areas of the application, and partitioning similar business concepts or data.</span></span> <span data-ttu-id="a56dc-124">但是，除了缩放所有组件的问题，对单个组件的更改需要完成重新测试整个应用程序，以及完成重新部署的所有实例。</span><span class="sxs-lookup"><span data-stu-id="a56dc-124">But, in addition to the problem of scaling all components, changes to a single component require complete retesting of the entire application, and a complete redeployment of all the instances.</span></span>

<span data-ttu-id="a56dc-125">但是，整体方法非常常见，，因为应用程序的开发是更容易微服务方法最初。</span><span class="sxs-lookup"><span data-stu-id="a56dc-125">However, the monolithic approach is common, because the development of the application is initially easier than for microservices approaches.</span></span> <span data-ttu-id="a56dc-126">因此，许多组织开发使用此体系结构的方法。</span><span class="sxs-lookup"><span data-stu-id="a56dc-126">Thus, many organizations develop using this architectural approach.</span></span> <span data-ttu-id="a56dc-127">某些组织有不会有什么足够结果，而其他人已达到限制。</span><span class="sxs-lookup"><span data-stu-id="a56dc-127">While some organizations have had good enough results, others are hitting limits.</span></span> <span data-ttu-id="a56dc-128">许多组织设计使用此模型，因为工具和基础结构变得太困难生成服务面向体系结构 (SOA) 几年前，及它们看不到需要其应用程序，直到应用程序增长。</span><span class="sxs-lookup"><span data-stu-id="a56dc-128">Many organizations designed their applications using this model because tools and infrastructure made it too difficult to build service oriented architectures (SOA) years ago, and they did not see the need—until the application grew.</span></span>

<span data-ttu-id="a56dc-129">从基础结构的角度看，每个服务器可以运行在同一主机内的很多应用程序和在图 4-2 中所示在资源用法中，具有到可接受的比率的效率。</span><span class="sxs-lookup"><span data-stu-id="a56dc-129">From an infrastructure perspective, each server can run many applications within the same host and have an acceptable ratio of efficiency in resources usage, as shown in Figure 4-2.</span></span>

![](./media/image2.png)

<span data-ttu-id="a56dc-130">**图 4-2**。</span><span class="sxs-lookup"><span data-stu-id="a56dc-130">**Figure 4-2**.</span></span> <span data-ttu-id="a56dc-131">整体方法： 托管运行多个应用作为容器运行每个应用程序</span><span class="sxs-lookup"><span data-stu-id="a56dc-131">Monolithic approach: Host running multiple apps, each app running as a container</span></span>

<span data-ttu-id="a56dc-132">可以为每个实例使用专用的虚拟机部署在 Microsoft Azure 中的单一应用程序。</span><span class="sxs-lookup"><span data-stu-id="a56dc-132">Monolithic applications in Microsoft Azure can be deployed using dedicated VMs for each instance.</span></span> <span data-ttu-id="a56dc-133">此外，使用[Azure VM 缩放集](https://docs.microsoft.com/azure/virtual-machine-scale-sets/)，你可以轻松地缩放 Vm。</span><span class="sxs-lookup"><span data-stu-id="a56dc-133">Additionally, using [Azure VM Scale Sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/), you can easily scale the VMs.</span></span> <span data-ttu-id="a56dc-134">[Azure App Service](https://azure.microsoft.com/services/app-service/)可以还运行的单一应用程序并轻松缩放而无需管理虚拟机的实例。</span><span class="sxs-lookup"><span data-stu-id="a56dc-134">[Azure App Service](https://azure.microsoft.com/services/app-service/) can also run monolithic applications and easily scale instances without requiring you to manage the VMs.</span></span> <span data-ttu-id="a56dc-135">自 2016，Azure 应用程序服务就可以运行单一实例的 Docker 容器都一样，从而简化部署。</span><span class="sxs-lookup"><span data-stu-id="a56dc-135">Since 2016, Azure App Services can run single instances of Docker containers as well, simplifying deployment.</span></span>

<span data-ttu-id="a56dc-136">作为 QA 环境或有限的生成环境，可部署多个 Docker 主机 Vm 和平衡它们使用 Azure 平衡器，如图 4-3 中所示。</span><span class="sxs-lookup"><span data-stu-id="a56dc-136">As a QA environment or a limited production environment, you can deploy multiple Docker host VMs and balance them using the Azure balancer, as shown in Figure 4-3.</span></span> <span data-ttu-id="a56dc-137">这允许你管理使用粗粒度方法时，缩放，因为整个应用程序存在于单个容器中。</span><span class="sxs-lookup"><span data-stu-id="a56dc-137">This lets you manage scaling with a coarse-grain approach, because the whole application lives within a single container.</span></span>

![](./media/image3.png)

<span data-ttu-id="a56dc-138">**图 4-3**。</span><span class="sxs-lookup"><span data-stu-id="a56dc-138">**Figure 4-3**.</span></span> <span data-ttu-id="a56dc-139">纵向扩展单个容器应用程序的多个主机的示例</span><span class="sxs-lookup"><span data-stu-id="a56dc-139">Example of multiple hosts scaling up a single container application</span></span>

<span data-ttu-id="a56dc-140">部署到各种主机可通过传统部署技术。</span><span class="sxs-lookup"><span data-stu-id="a56dc-140">Deployment to the various hosts can be managed with traditional deployment techniques.</span></span> <span data-ttu-id="a56dc-141">可以使用类似的命令管理 docker 主机`docker run`或`docker-compose`执行手动或通过如持续交付 (CD) 管道的自动化。</span><span class="sxs-lookup"><span data-stu-id="a56dc-141">Docker hosts can be managed with commands like `docker run` or `docker-compose` performed manually, or through automation such as continuous delivery (CD) pipelines.</span></span>

## <a name="deploying-a-monolithic-application-as-a-container"></a><span data-ttu-id="a56dc-142">部署容器作为一个整体应用程序</span><span class="sxs-lookup"><span data-stu-id="a56dc-142">Deploying a monolithic application as a container</span></span>

<span data-ttu-id="a56dc-143">没有为使用容器来管理整体应用程序部署的好处。</span><span class="sxs-lookup"><span data-stu-id="a56dc-143">There are benefits to using containers to manage monolithic application deployments.</span></span> <span data-ttu-id="a56dc-144">缩放容器实例是得更快比更容易地部署其他虚拟机。</span><span class="sxs-lookup"><span data-stu-id="a56dc-144">Scaling container instances is far faster and easier than deploying additional VMs.</span></span> <span data-ttu-id="a56dc-145">即使你使用 VM 缩放集，Vm 将花时间才能启动。</span><span class="sxs-lookup"><span data-stu-id="a56dc-145">Even if you use VM Scale Sets, VMs take time to start.</span></span> <span data-ttu-id="a56dc-146">在部署为而不是容器的传统应用程序实例，应用程序配置作为一部分进行管理的虚拟机，这并不理想。</span><span class="sxs-lookup"><span data-stu-id="a56dc-146">When deployed as traditional application instances instead of containers, the configuration of the application is managed as part of the VM, which is not ideal.</span></span>

<span data-ttu-id="a56dc-147">部署更新，因为 Docker 映像是得相当快和高效的网络。</span><span class="sxs-lookup"><span data-stu-id="a56dc-147">Deploying updates as Docker images is far faster and network efficient.</span></span> <span data-ttu-id="a56dc-148">Docker 映像通常将启动以秒为单位，― 加快了首次推出。</span><span class="sxs-lookup"><span data-stu-id="a56dc-148">Docker images typically start in seconds, which speeds rollouts.</span></span> <span data-ttu-id="a56dc-149">关闭的 Docker 映像实例非常简单，只需为颁发`docker stop`命令，并完成此过程通常少于一秒。</span><span class="sxs-lookup"><span data-stu-id="a56dc-149">Tearing down a Docker image instance is as easy as issuing a `docker stop` command, and typically completes in less than a second.</span></span>

<span data-ttu-id="a56dc-150">容器是设计使然不可变，因为无需担心如何损坏的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a56dc-150">Because containers are immutable by design, you never need to worry about corrupted VMs.</span></span> <span data-ttu-id="a56dc-151">与此相反，为 VM 的更新脚本可能会忘记某些特定配置或磁盘上剩余的文件的帐户。</span><span class="sxs-lookup"><span data-stu-id="a56dc-151">In contrast, update scripts for a VM might forget to account for some specific configuration or file left on disk.</span></span>

<span data-ttu-id="a56dc-152">尽管单一应用程序可以受益于 Docker，我们相互接触仅在好处上。</span><span class="sxs-lookup"><span data-stu-id="a56dc-152">While monolithic applications can benefit from Docker, we are touching only on the benefits.</span></span> <span data-ttu-id="a56dc-153">使用管理各种实例和每个容器实例的生命周期的容器 orchestrators 部署来自管理容器的其他好处。</span><span class="sxs-lookup"><span data-stu-id="a56dc-153">Additional benefits of managing containers come from deploying with container orchestrators, which manage the various instances and lifecycle of each container instance.</span></span> <span data-ttu-id="a56dc-154">中断此整体应用程序分解可以缩放、 开发和部署单独的子系统是微服务的领域你入口点。</span><span class="sxs-lookup"><span data-stu-id="a56dc-154">Breaking up the monolithic application into subsystems that can be scaled, developed, and deployed individually is your entry point into the realm of microservices.</span></span>

## <a name="publishing-a-single-container-based-application-to-azure-app-service"></a><span data-ttu-id="a56dc-155">单容器基于应用程序发布到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a56dc-155">Publishing a single-container-based application to Azure App Service</span></span>

<span data-ttu-id="a56dc-156">你是否想要进行验证的部署到 Azure 的容器或应用程序只需单个容器应用程序时，Azure App Service 提供了提供可缩放的单容器基于服务的好办法。</span><span class="sxs-lookup"><span data-stu-id="a56dc-156">Whether you want to get validation of a container deployed to Azure or when an application is simply a single-container application, Azure App Service provides a great way to provide scalable single-container-based services.</span></span> <span data-ttu-id="a56dc-157">使用 Azure App Service 是简单的。</span><span class="sxs-lookup"><span data-stu-id="a56dc-157">Using Azure App Service is simple.</span></span> <span data-ttu-id="a56dc-158">它提供了使用 Git，以便可以方便地获取你的代码，生成它在 Visual Studio 中，并将其部署到 Azure 直接极好的集成。</span><span class="sxs-lookup"><span data-stu-id="a56dc-158">It provides great integration with Git to make it easy to take your code, build it in Visual Studio, and deploy it directly to Azure.</span></span>

![](./media/image4.png)

<span data-ttu-id="a56dc-159">**图 4-4**。</span><span class="sxs-lookup"><span data-stu-id="a56dc-159">**Figure 4-4**.</span></span> <span data-ttu-id="a56dc-160">单容器应用程序发布到 Azure App Service 从 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a56dc-160">Publishing a single-container application to Azure App Service from Visual Studio</span></span>

<span data-ttu-id="a56dc-161">而无需 Docker，如果需要其他功能，框架或不支持在 Azure App Service 中的依赖项必须等待，直到 Azure 团队更新在 App Service 中的这些依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a56dc-161">Without Docker, if you needed other capabilities, frameworks, or dependencies that are not supported in Azure App Service, you had to wait until the Azure team updated those dependencies in App Service.</span></span> <span data-ttu-id="a56dc-162">或者，你必须切换到 Azure Service Fabric、 Azure 云服务或甚至虚拟机，其中进一步控件并且你无法安装所需的组件或 framework 应用程序等其他服务。</span><span class="sxs-lookup"><span data-stu-id="a56dc-162">Or you had to switch to other services like Azure Service Fabric, Azure Cloud Services, or even VMs, where you had further control and you could install a required component or framework for your application.</span></span>

<span data-ttu-id="a56dc-163">在 Visual Studio 2017 容器支持使你能够包括任何你想在应用程序环境中，在图 4-4 中所示。</span><span class="sxs-lookup"><span data-stu-id="a56dc-163">Container support in Visual Studio 2017 gives you the ability to include whatever you want in your application environment, as shown in Figure 4-4.</span></span> <span data-ttu-id="a56dc-164">由于你已经运行在容器中，如果将一个依赖项添加到你的应用程序，你可以在 Dockerfile 或 Docker 映像中包括依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a56dc-164">Since you are running it in a container, if you add a dependency to your application, you can include the dependency in your Dockerfile or Docker image.</span></span>

<span data-ttu-id="a56dc-165">此外显示在图 4-4 中，发布流将映像推送通过容器注册表中。</span><span class="sxs-lookup"><span data-stu-id="a56dc-165">As also shown in Figure 4-4, the publish flow pushes an image through a container registry.</span></span> <span data-ttu-id="a56dc-166">这可以是 Azure 容器注册表 （注册表关闭你在 Azure 中的部署和保护的 Azure Active Directory 组和帐户） 或任何其他 Docker 注册表，如 Docker Hub 或在本地注册表。</span><span class="sxs-lookup"><span data-stu-id="a56dc-166">This can be the Azure Container Registry (a registry close to your deployments in Azure and secured by Azure Active Directory groups and accounts), or any other Docker registry, like Docker Hub or an on-premises registry.</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="a56dc-167">[以前](index.md) [下一步] (docker-应用程序的状态-data.md)</span><span class="sxs-lookup"><span data-stu-id="a56dc-167">[Previous] (index.md) [Next] (docker-application-state-data.md)</span></span>