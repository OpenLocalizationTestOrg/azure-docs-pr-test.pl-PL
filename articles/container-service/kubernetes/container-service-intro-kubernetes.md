---
title: "tooAzure aaaIntroduction usługi kontenera dla Kubernetes | Dokumentacja firmy Microsoft"
description: "Usługa kontenera platformy Azure dla Kubernetes umożliwia proste toodeploy aplikacji i zarządzanie nimi na podstawie kontenera na platformie Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, Containers, Microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="cda2d-104">Wprowadzenie tooAzure usługi kontenera dla Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cda2d-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="cda2d-105">Usługa kontenera platformy Azure dla Kubernetes umożliwia proste toocreate, konfigurowanie i Zarządzanie klastrem maszyn wirtualnych, które są wstępnie skonfigurowane toorun konteneryzowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cda2d-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="cda2d-106">Umożliwia możesz toouse Twojego posiadane umiejętności lub sięgać duży i rosnącym treści doświadczenia społeczności, toodeploy i Zarządzaj aplikacjami w kontenerze w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cda2d-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="cda2d-107">Za pomocą usługi kontenera platformy Azure, można skorzystać z hello korporacyjnej funkcji platformy Azure, zachowując przenośność aplikacji za pośrednictwem Kubernetes i hello Docker format obrazu.</span><span class="sxs-lookup"><span data-stu-id="cda2d-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="cda2d-108">Używanie usługi Azure Container Service ma potrzeby rozwiązania Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cda2d-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="cda2d-109">Naszym celem z usługi kontenera platformy Azure jest tooprovide środowisko macierzyste kontenera za pomocą open source, narzędzia i technologie, które są obecnie popularnością wśród klientów.</span><span class="sxs-lookup"><span data-stu-id="cda2d-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="cda2d-110">końcowy toothis uwidaczniamy hello standardowe Kubernetes punkty końcowe interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="cda2d-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="cda2d-111">Za pomocą tych standardowych punktów końcowych, można wykorzystać dowolne oprogramowanie, które jest w stanie mówić tooa Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="cda2d-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="cda2d-112">Możesz wybrać narzędzie [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) lub [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="cda2d-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="cda2d-113">Tworzenie klastra Kubernetes przy użyciu usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cda2d-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="cda2d-114">toobegin przy użyciu usługi kontenera platformy Azure, wdrażanie klastra usługi kontenera platformy Azure z hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) lub za pośrednictwem portalu hello (hello wyszukiwania portalu Marketplace dla **usługi kontenera platformy Azure**).</span><span class="sxs-lookup"><span data-stu-id="cda2d-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="cda2d-115">Jeśli jesteś użytkownikiem zaawansowanym, który musi mieć większą kontrolę nad hello szablonów usługi Azure Resource Manager, można użyć typu open source hello [aparat acs](https://github.com/Azure/acs-engine) toobuild projektu własne niestandardowe Kubernetes klastra i wdróż je za pośrednictwem hello `az` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="cda2d-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="cda2d-116">Korzystanie z rozwiązania Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cda2d-116">Using Kubernetes</span></span>
<span data-ttu-id="cda2d-117">Narzędzie Kubernetes automatyzuje proces wdrażania i skalowania aplikacji konteneryzowanych oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="cda2d-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="cda2d-118">Narzędzie to obejmuje bogaty zestaw funkcji, m.in.:</span><span class="sxs-lookup"><span data-stu-id="cda2d-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="cda2d-119">automatyczne pakowanie pudełek,</span><span class="sxs-lookup"><span data-stu-id="cda2d-119">Automatic binpacking</span></span>
* <span data-ttu-id="cda2d-120">mechanizm samonaprawiania</span><span class="sxs-lookup"><span data-stu-id="cda2d-120">Self-healing</span></span>
* <span data-ttu-id="cda2d-121">skalowanie w poziomie,</span><span class="sxs-lookup"><span data-stu-id="cda2d-121">Horizontal scaling</span></span>
* <span data-ttu-id="cda2d-122">odnajdywanie usług i równoważenie obciążenia,</span><span class="sxs-lookup"><span data-stu-id="cda2d-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="cda2d-123">zautomatyzowane wprowadzanie i wycofywanie zmian,</span><span class="sxs-lookup"><span data-stu-id="cda2d-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="cda2d-124">zarządzanie kluczami tajnymi i konfiguracją,</span><span class="sxs-lookup"><span data-stu-id="cda2d-124">Secret and configuration management</span></span>
* <span data-ttu-id="cda2d-125">aranżacja magazynu,</span><span class="sxs-lookup"><span data-stu-id="cda2d-125">Storage orchestration</span></span>
* <span data-ttu-id="cda2d-126">wykonywanie partii zadań.</span><span class="sxs-lookup"><span data-stu-id="cda2d-126">Batch execution</span></span>

<span data-ttu-id="cda2d-127">Diagram architektury rozwiązania Kubernetes wdrażanej za pomocą usługi Azure Container Service:</span><span class="sxs-lookup"><span data-stu-id="cda2d-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Usługa kontenera platformy Azure skonfigurowane toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="cda2d-129">Filmy wideo</span><span class="sxs-lookup"><span data-stu-id="cda2d-129">Videos</span></span>

<span data-ttu-id="cda2d-130">Obsługa klastra Kubernetes w usłudze Azure Container Service (Azure Friday, styczeń 2017 r.):</span><span class="sxs-lookup"><span data-stu-id="cda2d-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="cda2d-131">Narzędzia do tworzenia i wdrażania aplikacji w systemie Kubernetes (Azure OpenDev, czerwiec 2017 r.):</span><span class="sxs-lookup"><span data-stu-id="cda2d-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="cda2d-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cda2d-132">Next steps</span></span>

<span data-ttu-id="cda2d-133">Eksploruj hello [szybkiego startu Kubernetes](container-service-kubernetes-walkthrough.md) toobegin dzisiaj Eksplorowanie usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cda2d-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
