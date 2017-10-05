---
title: "Pule agenta DC/OS usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak działają pule publiczny i prywatny agenta z klastrem usługi kontenera platformy Azure DC/OS"
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
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="ea8f1-104">Pule agenta DC/OS usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ea8f1-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="ea8f1-105">Klastry DC/OS usługi kontenera platformy Azure zawierają węzły agenta w dwie pule, puli publicznych i prywatnych puli.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="ea8f1-106">Aplikację można wdrożyć do jednej puli wpływu na dostępność między komputerami w usłudze kontenera.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="ea8f1-107">Maszyny można połączenie z Internetem (publicznej) lub przechowywane wewnętrzny (prywatny).</span><span class="sxs-lookup"><span data-stu-id="ea8f1-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="ea8f1-108">Ten artykuł zawiera krótki przegląd, dlatego są pule publiczne i prywatne.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="ea8f1-109">**Agenci prywatnej**: węźle prywatnego agent uruchomiony za pośrednictwem sieci bez obsługi routingu.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="ea8f1-110">Ta sieć jest dostępny tylko ze strefy administratora lub za pośrednictwem routera brzegowego publicznego strefy.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="ea8f1-111">Domyślnie DC/OS uruchamia aplikacje na węzłach prywatny agenta.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="ea8f1-112">**Agentów publicznych**: węzłów agenta publicznego Uruchom aplikacje DC/OS i usługi za pośrednictwem publicznie dostępnej sieci.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="ea8f1-113">Aby uzyskać więcej informacji o zabezpieczeniach sieci DC/OS, zobacz [dokumentacji DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="ea8f1-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="ea8f1-114">Wdrażanie pul agenta</span><span class="sxs-lookup"><span data-stu-id="ea8f1-114">Deploy agent pools</span></span>

<span data-ttu-id="ea8f1-115">Pule agenta DC/OS w usłudze kontenera platformy Azure są tworzone w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ea8f1-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="ea8f1-116">**Prywatnej puli** zawiera liczbę węzłów agenta, że możesz określić, kiedy użytkownik [wdrożyć klaster DC/OS](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ea8f1-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="ea8f1-117">**Puli publicznych** początkowo zawiera wstępnie określoną liczbę węzłów agenta.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="ea8f1-118">Ta pula jest automatycznie dodawane po zainicjowaniu obsługi klastra DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="ea8f1-119">Pula prywatnych i publicznych puli są zestawy skalowania maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="ea8f1-120">Po wdrożeniu mogą zmieniać rozmiar te pule.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="ea8f1-121">Pule agenta</span><span class="sxs-lookup"><span data-stu-id="ea8f1-121">Use agent pools</span></span>
<span data-ttu-id="ea8f1-122">Domyślnie **Marathon** wdraża każdej nowej aplikacji *prywatnej* węzłów agenta.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="ea8f1-123">Należy jawnie wdrożenia aplikacji na *publicznego* węzłów podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="ea8f1-124">Wybierz **opcjonalnie** i wprowadzić **slave_public** dla **zaakceptowane role zasobów** wartość.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="ea8f1-125">Ten proces jest udokumentowany [tutaj](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) i [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea8f1-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ea8f1-126">Next steps</span></span>
* <span data-ttu-id="ea8f1-127">Przeczytaj więcej na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="ea8f1-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="ea8f1-128">Dowiedz się, jak [otwórz Zaporę](container-service-enable-public-access.md) dostarczany przez platformę Azure, aby zezwolić na publiczny dostęp do kontenerów DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ea8f1-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

