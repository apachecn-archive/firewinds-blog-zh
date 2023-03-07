# Kubernetes: 10 个技术改造步骤

> 原文：<https://www.fairwinds.com/blog/kubernetes-10-technical-transformation-steps>

 Fairwinds 发布了 [Kubernetes 成熟度模型](https://www.fairwinds.com/kubernetes-maturity-model)工具，帮助人们通过 Kubernetes 自我识别他们的成熟度，了解他们环境中的差距，并深入了解如何增强和改善他们的 Kubernetes 堆栈。

Kubernetes 成熟度模型的第二阶段[侧重于转型](https://www.fairwinds.com/kubernetes-maturity-model/phase-2-transform)。在这一阶段，您的重点是将工作负载转移到 Kubernetes 中，包括将您的应用程序容器化(如果它们还没有在容器中运行)。要成功完成这一技术转型，您需要采取 10 个主要步骤。这代表了对每个步骤的高度概括，请记住，您应该准备在此过程的每个步骤上花费大量时间。

1.  **深入研究和项目计划** -无论您是在本地、数据中心还是已经迁移到云，您的第一步都是深入研究您的现有堆栈。您需要调查堆栈的所有方面，从底层网络、基础架构、配置、机密管理到您如何部署应用程序及其依赖关系。当您迁移到 Kubernetes 时，您需要确定您的技术需求。这一步可以帮助你避免错过一个重要的需求。基于这种深入研究，您可以制定一个项目计划，作为您的迁移路线图。
2.  **应用程序容器化**——你的应用程序可能已经被容器化了，在这种情况下，你可以进入第三步。如果不是，你需要根据十二因素应用程序方法来分解你的应用程序。这是至关重要的，因为您将需要您的应用程序经历破坏(您的容器可能随时被杀死)。您需要能够干净地备份您的应用程序和容器。在这一步中，我们建议您从构建工件中提取您的秘密和配置。Kubernetes 是短暂的，因此通过这样做，您将维护您的标准和安全性，并在容器运行时简单地注入秘密和配置。
3.  **构建云基础设施** -您需要确定您的云提供商:AWS、GCP、Azure 或托管的 Kubernetes 服务，如 EKS、GKS 或 AKS。如果您选择了托管 Kubernetes 服务，那么在构建 Kubernetes 基础设施时，您的工作量会更少。您需要设置底层的云配置、VPC、安全组、认证和授权等。作为这一步的一部分。
4.  **构建 Kubernetes 基础设施** -在第四步中，需要考虑设计因素，以避免做出可能需要耗时的集群重建或网络和成本影响的选择。一些考虑事项包括:在什么区域应该有多少个集群，有多少个可用性区域(az)？需要多少独立的环境、集群和名称空间？服务应该如何相互通信或发现？安全性是在 VPC、集群还是单元级别？你的重点应该是重复性。您将希望利用基础设施即代码(IaC ),以便能够以一种重复的方式构建您的集群。在这一步中，使用第一步中的深入研究/项目计划时，请注意您的配置选项，以确保您不会错过应用程序要求。
5.  **写 YAML 或舵图**——在 Fairwinds，我们称这一步应用为 Kubernating。这是您定义 Kubernetes 资源的地方，以便将它们加入您的集群。在这里，您可以编写 Kubernetes 资源 YAML 文件，但是现在大多数都使用舵图来将应用程序部署到 Kubernetes 中。你将写 YAML 或舵图表专门为您的集装箱图像，模板配置图，秘密或任何特殊的应用要求。
6.  **探测外部云依赖关系** -您的应用程序将具有外部依赖关系，如其密钥库、库、数据库或其他资产。Kubernetes 并不是这些依赖者生活的好地方。您将希望在 Kubernetes 之外管理您的有状态依赖。例如，你可以在 Amazon RDS 这样的工具中建立数据库，然后将其导入 Kubernetes。然后，您的应用程序可以在 Kubernetes 的 pod 中运行，并与这些依赖项对话。
7.  定义 Git 工作流程——Kubernetes 的一个主要优势是能够以可重复的方式部署代码，无需人工干预。您通常通过 Git 将代码提交给源代码，Git 将启动事件并与将这些更改转移到非生产集群的分支合并。然后，您将测试和 QA 您的代码，并将其合并到主文件中。这将把您的代码部署到登台或生产环境中。在这个阶段，你只是简单地定义你的 Git 工作流看起来像什么，也就是说，当开发者推送代码时，Kubernetes 中会发生什么？
8.  **建立你的 CI/CD 管道** -一旦你定义了你的 Git 工作流程，你将使用像 Jenkins 或 CircleCI 这样的自动化工具建立你的 CI/CD 平台。这将把您定义的工作流变成一个实际的构建管道。
9.  **非生产测试** -在您完成整体应用或微服务架构的步骤 1-8 后，您将部署到非生产环境。在这里，您将使用应用程序来确保它运行，有足够的资源和限制，测试您的秘密是否正确进入，人们是否可以访问该应用程序。你将测试如果你杀死你的豆荚会发生什么。实际上，在进入生产阶段之前，你会踢踢轮胎。如果你正在运行一个 monolith 应用程序，你会更快地通过这个阶段。如果您正在部署微服务应用程序架构，您将为每个服务完成步骤 1-8，并部署到非生产环境。一旦所有的服务都准备好了，您就可以看到它们是如何协同工作的，以确保一旦投入生产，您的应用程序就能正常工作。
10.  **生产推广** -最后，一旦您在非生产环境中彻底测试了您的应用程序，并对此感到满意，只要您的生产环境与您的试运行环境相同，您就可以部署应用程序并向其发送流量。在这里，您只需更改您的负载平衡器或 DNS。使用 DNS，如果需要，您可以回切。

在第二阶段，您还将着眼于清理技术债务，围绕工具制定决策，调查生产率的收益与损失，并开始着眼于灵活性与控制。

进一步了解 [Kubernetes 成熟度模型](https://www.fairwinds.com/kubernetes-maturity-model)的转型阶段，并研究该模型的所有阶段。