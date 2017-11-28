---
title: aaaGetting Started with Foundry chmury w systemie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Uruchom OSS lub Foundry kluczową chmurze na platformie Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="6aef4-103">Usługa Cloud Foundry na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6aef4-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="6aef4-104">Foundry chmury jest open source platformy jako — usługa (PaaS) dotyczące tworzenia, wdrażania i obsługi 12-factor aplikacji utworzonych w różnych języków i struktur.</span><span class="sxs-lookup"><span data-stu-id="6aef4-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="6aef4-105">W tym dokumencie opisano opcje hello masz zasilany Foundry chmury Azure i jak możesz rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="6aef4-105">This document describes hello options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="6aef4-106">Foundry oferty usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="6aef4-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="6aef4-107">Istnieją dwie formy toorun dostępne Foundry chmurze na platformie Azure: chmury Foundry (OSS CF) i kluczową chmury Foundry (PCF) open source.</span><span class="sxs-lookup"><span data-stu-id="6aef4-107">There are two forms of Cloud Foundry available toorun on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="6aef4-108">OSS CF jest całkowicie [open source](https://github.com/cloudfoundry) wersji Foundry chmury zarządza hello Foundation Foundry chmury.</span><span class="sxs-lookup"><span data-stu-id="6aef4-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by hello Cloud Foundry Foundation.</span></span> <span data-ttu-id="6aef4-109">Kluczową Foundry chmury jest dystrybucja enterprise Foundry chmury z kluczową Inc. oprogramowania Przyjrzymy się niektóre hello różnice między Witaj dwie oferty.</span><span class="sxs-lookup"><span data-stu-id="6aef4-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of hello differences between hello two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="6aef4-110">Chmura open source Foundry</span><span class="sxs-lookup"><span data-stu-id="6aef4-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="6aef4-111">Można wdrożyć OSS Foundry chmury Azure najpierw wdrażanie Dyrektor BOSH, a następnie wdrażanie Foundry chmury, za pomocą hello [instrukcje podane w serwisie GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span><span class="sxs-lookup"><span data-stu-id="6aef4-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using hello [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="6aef4-112">toolearn więcej informacji o użyciu CF systemów operacyjnych, zobacz hello [dokumentacji](https://docs.cloudfoundry.org/) podał hello Foundation Foundry chmury.</span><span class="sxs-lookup"><span data-stu-id="6aef4-112">toolearn more about using OSS CF, see hello [documentation](https://docs.cloudfoundry.org/) provided by hello Cloud Foundry Foundation.</span></span>

<span data-ttu-id="6aef4-113">Firma Microsoft udostępnia optymalnych obsługę OSS CF za pośrednictwem następujących kanałów społeczności hello:</span><span class="sxs-lookup"><span data-stu-id="6aef4-113">Microsoft provides best-effort support for OSS CF through hello following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="6aef4-114">kanał bosh-azure-cpi na [Slack Foundry chmury](https://slack.cloudfoundry.org/)</span><span class="sxs-lookup"><span data-stu-id="6aef4-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="6aef4-115">listy adresowej CF bosh</span><span class="sxs-lookup"><span data-stu-id="6aef4-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="6aef4-116">Problemy z usługi GitHub hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) i [programu service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span><span class="sxs-lookup"><span data-stu-id="6aef4-116">GitHub issues for hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="6aef4-117">Witaj poziom obsługi zasobów platformy Azure, takich jak maszyny wirtualne hello realizującym Foundry chmury opiera się na umowie pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6aef4-117">hello level of support for your Azure resources, such as hello virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="6aef4-118">Obsługa społeczności optymalnych dotyczy tylko składniki toohello Foundry specyficzne dla chmury.</span><span class="sxs-lookup"><span data-stu-id="6aef4-118">Best-effort community support only applies toohello Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="6aef4-119">Kluczową chmury Foundry</span><span class="sxs-lookup"><span data-stu-id="6aef4-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="6aef4-120">Kluczową Foundry chmury obejmuje hello tej samej podstawowej platformy jako dystrybucji hello OSS, wraz z zestawem narzędzi do zarządzania zastrzeżonych i pomocy technicznej enterprise.</span><span class="sxs-lookup"><span data-stu-id="6aef4-120">Pivotal Cloud Foundry includes hello same core platform as hello OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="6aef4-121">toorun PCF na platformie Azure, w przypadku uzyskania licencji z Pivotal.</span><span class="sxs-lookup"><span data-stu-id="6aef4-121">toorun PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="6aef4-122">Oferta PCF Hello z hello Azure marketplace zawiera 90-dniowy licencja próbna.</span><span class="sxs-lookup"><span data-stu-id="6aef4-122">hello PCF offer from hello Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="6aef4-123">narzędzia Hello obejmują [kluczową programu Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), aplikacji sieci web, które upraszcza wdrażanie i zarządzanie foundation Foundry chmury, a [kluczową Menedżera aplikacji](https://docs.pivotal.io/pivotalcf/console/), aplikacji sieci web do zarządzania Użytkownicy i aplikacje.</span><span class="sxs-lookup"><span data-stu-id="6aef4-123">hello tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="6aef4-124">Ponadto wymienione powyżej CF OSS kanałów pomocy technicznej toohello, licencji PCF uprawnia możesz toocontact Pivotal pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="6aef4-124">In addition toohello support channels listed for OSS CF above, a PCF license entitles you toocontact Pivotal for support.</span></span> <span data-ttu-id="6aef4-125">Microsoft Pivotal również włączono obsługę przepływy pracy, które pozwalają toocontact każdą stronę pomocy i mieć Twojego zapytania kierowane odpowiednio w zależności od tego, gdzie znajduje się problem hello.</span><span class="sxs-lookup"><span data-stu-id="6aef4-125">Microsoft and Pivotal have also enabled support workflows that allow you toocontact either party for assistance and have your inquiry routed appropriately depending on where hello issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="6aef4-126">Broker usług Azure</span><span class="sxs-lookup"><span data-stu-id="6aef4-126">Azure Service Broker</span></span>

<span data-ttu-id="6aef4-127">Chmura Foundry zachęca hello ["12 factor aplikacja"](https://12factor.net/) metodologii, która wspiera czyste rozdzielenie procesów aplikacji bezstanowych i stateful kopii usług.</span><span class="sxs-lookup"><span data-stu-id="6aef4-127">Cloud Foundry encourages hello ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="6aef4-128">[Usługa brokerzy](https://docs.cloudfoundry.org/services/api.html) oferować tooprovision spójny sposób i powiązać tooapplications usługi tworzenia kopii.</span><span class="sxs-lookup"><span data-stu-id="6aef4-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way tooprovision and bind backing services tooapplications.</span></span> <span data-ttu-id="6aef4-129">Witaj [brokera usług Azure](https://github.com/Azure/meta-azure-service-broker) zawiera niektóre z hello klucza usługi Azure za pośrednictwem tego kanału, w tym magazynu Azure i Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6aef4-129">hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of hello key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="6aef4-130">Jeśli używasz kluczową Foundry chmury programu service broker hello jest również [dostępne jako Kafelek](https://docs.pivotal.io/azure-sb/installing.html) z hello kluczową sieci.</span><span class="sxs-lookup"><span data-stu-id="6aef4-130">If you are using Pivotal Cloud Foundry, hello service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from hello Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="6aef4-131">Powiązane zasoby</span><span class="sxs-lookup"><span data-stu-id="6aef4-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="6aef4-132">Visual Studio Team Services wtyczki</span><span class="sxs-lookup"><span data-stu-id="6aef4-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="6aef4-133">Foundry chmury jest rozwoju oprogramowania dobrze nadają się tooagile, włączając stosowania hello ciągłej integracji (CI) i ciągłego dostarczania (CD).</span><span class="sxs-lookup"><span data-stu-id="6aef4-133">Cloud Foundry is well suited tooagile software development, including hello use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="6aef4-134">Jeśli używasz programu Visual Studio Team Services (VSTS) toomanage swoje projekty i chcesz tooset się potoku CI/CD przeznaczonych dla Foundry chmury, można użyć hello [rozszerzenie kompilacji programu VSTS chmury Foundry](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span><span class="sxs-lookup"><span data-stu-id="6aef4-134">If you use Visual Studio Team Services (VSTS) toomanage your projects and would like tooset up a CI/CD pipeline targeting Cloud Foundry, you can use hello [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="6aef4-135">Hello wtyczki powoduje tooconfigure proste i zautomatyzować wdrożeń tooCloud Foundry, czy uruchomione w Azure lub w innym środowisku.</span><span class="sxs-lookup"><span data-stu-id="6aef4-135">hello plugin makes it simple tooconfigure and automate deployments tooCloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aef4-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6aef4-136">Next steps</span></span>

- [<span data-ttu-id="6aef4-137">Wdrażanie kluczową Foundry chmury z hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6aef4-137">Deploy Pivotal Cloud Foundry from hello Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="6aef4-138">Wdrażanie aplikacji tooCloud Foundry na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6aef4-138">Deploy an app tooCloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)
