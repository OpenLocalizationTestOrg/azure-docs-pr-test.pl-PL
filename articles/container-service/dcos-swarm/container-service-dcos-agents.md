---
title: "pule agenta aaaDC/OS usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak działają hello agenta publicznego i prywatnego pule z klastrem usługi kontenera platformy Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="fe027-104">Pule agenta DC/OS usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fe027-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="fe027-105">Klastry DC/OS usługi kontenera platformy Azure zawierają węzły agenta w dwie pule, puli publicznych i prywatnych puli.</span><span class="sxs-lookup"><span data-stu-id="fe027-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="fe027-106">Aplikację można wdrożyć puli tooeither wpływu na dostępność między komputerami w usłudze kontenera.</span><span class="sxs-lookup"><span data-stu-id="fe027-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="fe027-107">Hello maszyny mogą być narażone toohello internet (publicznej) lub wewnętrzny (prywatny).</span><span class="sxs-lookup"><span data-stu-id="fe027-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="fe027-108">Ten artykuł zawiera krótki przegląd, dlatego są pule publiczne i prywatne.</span><span class="sxs-lookup"><span data-stu-id="fe027-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="fe027-109">**Agenci prywatnej**: węźle prywatnego agent uruchomiony za pośrednictwem sieci bez obsługi routingu.</span><span class="sxs-lookup"><span data-stu-id="fe027-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="fe027-110">Ta sieć jest dostępny tylko ze strefy admin hello lub za pośrednictwem routera brzegowego publicznego strefy hello.</span><span class="sxs-lookup"><span data-stu-id="fe027-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="fe027-111">Domyślnie DC/OS uruchamia aplikacje na węzłach prywatny agenta.</span><span class="sxs-lookup"><span data-stu-id="fe027-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="fe027-112">**Agentów publicznych**: węzłów agenta publicznego Uruchom aplikacje DC/OS i usługi za pośrednictwem publicznie dostępnej sieci.</span><span class="sxs-lookup"><span data-stu-id="fe027-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="fe027-113">Aby uzyskać więcej informacji o zabezpieczeniach sieci DC/OS, zobacz hello [dokumentacji DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="fe027-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="fe027-114">Wdrażanie pul agenta</span><span class="sxs-lookup"><span data-stu-id="fe027-114">Deploy agent pools</span></span>

<span data-ttu-id="fe027-115">pule agenta DC/OS Hello w usłudze kontenera platformy Azure są tworzone w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fe027-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="fe027-116">Hello **prywatnej puli** zawiera hello liczbę węzłów agenta, że możesz określić, kiedy użytkownik [wdrożyć klaster DC/OS hello](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fe027-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="fe027-117">Witaj **puli publicznych** początkowo zawiera wstępnie określoną liczbę węzłów agenta.</span><span class="sxs-lookup"><span data-stu-id="fe027-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="fe027-118">Ta pula jest automatycznie dodawane po zainicjowaniu obsługi klastra DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="fe027-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="fe027-119">Hello puli prywatnych i puli publicznych hello są zestawy skalowania maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe027-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="fe027-120">Po wdrożeniu mogą zmieniać rozmiar te pule.</span><span class="sxs-lookup"><span data-stu-id="fe027-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="fe027-121">Pule agenta</span><span class="sxs-lookup"><span data-stu-id="fe027-121">Use agent pools</span></span>
<span data-ttu-id="fe027-122">Domyślnie **Marathon** wdraża żadnych nowych aplikacji toohello *prywatnej* węzłów agenta.</span><span class="sxs-lookup"><span data-stu-id="fe027-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="fe027-123">Należy wdrożyć toohello aplikacji hello tooexplicitly *publicznego* węzłów podczas tworzenia aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe027-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="fe027-124">Wybierz hello **opcjonalnie** i wprowadzić **slave_public** dla hello **zaakceptowane role zasobów** wartość.</span><span class="sxs-lookup"><span data-stu-id="fe027-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="fe027-125">Ten proces jest udokumentowany [tutaj](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) w hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="fe027-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe027-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe027-126">Next steps</span></span>
* <span data-ttu-id="fe027-127">Przeczytaj więcej na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="fe027-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="fe027-128">Dowiedz się, jak za[Otwórz zaporę Windows hello](container-service-enable-public-access.md) podał Azure tooallow dostępu publicznego tooyour DC/OS kontenerów.</span><span class="sxs-lookup"><span data-stu-id="fe027-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

