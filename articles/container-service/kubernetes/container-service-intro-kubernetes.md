---
title: "Wprowadzenie do usługi Azure Container Service dla rozwiązania Kubernetes | Microsoft Docs"
description: "Usługa Azure Container Service dla rozwiązania Kubernetes ułatwia wdrażanie aplikacji opartych na kontenerach i zarządzanie nimi na platformie Azure."
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
ms.openlocfilehash: 92cdbe20e7a2974a734dfed5294c547866050290
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-azure-container-service-for-kubernetes"></a><span data-ttu-id="6dc00-104">Wprowadzenie do usługi Azure Container Service dla rozwiązania Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6dc00-104">Introduction to Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="6dc00-105">Usługa Azure Container Service dla rozwiązania Kubernetes upraszcza tworzenie i konfigurację klastra maszyn wirtualnych, które są wstępnie skonfigurowane do uruchamiania konteneryzowanych aplikacji, oraz zarządzanie nim.</span><span class="sxs-lookup"><span data-stu-id="6dc00-105">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="6dc00-106">Umożliwia to używanie posiadanych umiejętności lub sięganie po duży i rosnący zasób wiedzy społeczności w celu wdrażania opartych na kontenerze aplikacji platformy Microsoft Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="6dc00-106">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="6dc00-107">Za pomocą usługi Azure Container Service możesz korzystać z funkcji klasy korporacyjnej platformy Azure, zachowując jednocześnie przenośność aplikacji dzięki usłudze Kubernetes i formatowi obrazów Docker.</span><span class="sxs-lookup"><span data-stu-id="6dc00-107">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="6dc00-108">Używanie usługi Azure Container Service ma potrzeby rozwiązania Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6dc00-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="6dc00-109">Za pomocą usługi Azure Container Service chcemy zapewnić środowisko hostingu kontenerów za pomocą narzędzi i technologii typu open source, które już dziś są popularne wśród naszych klientów.</span><span class="sxs-lookup"><span data-stu-id="6dc00-109">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="6dc00-110">W tym celu uwidaczniamy standardowe punkty końcowe interfejsu API rozwiązania Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6dc00-110">To this end, we expose the standard Kubernetes API endpoints.</span></span> <span data-ttu-id="6dc00-111">Za pomocą tych standardowych punktów końcowych można wykorzystać dowolne oprogramowanie, które jest w stanie komunikować się z klastrem usługi Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6dc00-111">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span></span> <span data-ttu-id="6dc00-112">Możesz wybrać narzędzie [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) lub [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="6dc00-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="6dc00-113">Tworzenie klastra Kubernetes przy użyciu usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="6dc00-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="6dc00-114">Aby rozpocząć korzystanie z usługi Azure Container Service, musisz wdrożyć klaster usługi Azure Container Service przy użyciu [interfejsu wiersza polecenia platformy Azure 2.0](container-service-kubernetes-walkthrough.md) lub za pośrednictwem portalu (wyszukaj w witrynie Marketplace termin **Azure Container Service**).</span><span class="sxs-lookup"><span data-stu-id="6dc00-114">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="6dc00-115">Jeśli jesteś użytkownikiem zaawansowanym, który musi mieć większą kontrolę nad szablonami usługi Azure Resource Manager, możesz użyć projektu [acs-engine](https://github.com/Azure/acs-engine) typu open source do kompilowania własnego niestandardowego klastra Kubernetes i wdrażania go za pomocą interfejsu wiersza polecenia `az`.</span><span class="sxs-lookup"><span data-stu-id="6dc00-115">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="6dc00-116">Korzystanie z rozwiązania Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6dc00-116">Using Kubernetes</span></span>
<span data-ttu-id="6dc00-117">Narzędzie Kubernetes automatyzuje proces wdrażania i skalowania aplikacji konteneryzowanych oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="6dc00-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="6dc00-118">Narzędzie to obejmuje bogaty zestaw funkcji, m.in.:</span><span class="sxs-lookup"><span data-stu-id="6dc00-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="6dc00-119">automatyczne pakowanie pudełek,</span><span class="sxs-lookup"><span data-stu-id="6dc00-119">Automatic binpacking</span></span>
* <span data-ttu-id="6dc00-120">mechanizm samonaprawiania</span><span class="sxs-lookup"><span data-stu-id="6dc00-120">Self-healing</span></span>
* <span data-ttu-id="6dc00-121">skalowanie w poziomie,</span><span class="sxs-lookup"><span data-stu-id="6dc00-121">Horizontal scaling</span></span>
* <span data-ttu-id="6dc00-122">odnajdywanie usług i równoważenie obciążenia,</span><span class="sxs-lookup"><span data-stu-id="6dc00-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="6dc00-123">zautomatyzowane wprowadzanie i wycofywanie zmian,</span><span class="sxs-lookup"><span data-stu-id="6dc00-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="6dc00-124">zarządzanie kluczami tajnymi i konfiguracją,</span><span class="sxs-lookup"><span data-stu-id="6dc00-124">Secret and configuration management</span></span>
* <span data-ttu-id="6dc00-125">aranżacja magazynu,</span><span class="sxs-lookup"><span data-stu-id="6dc00-125">Storage orchestration</span></span>
* <span data-ttu-id="6dc00-126">wykonywanie partii zadań.</span><span class="sxs-lookup"><span data-stu-id="6dc00-126">Batch execution</span></span>

<span data-ttu-id="6dc00-127">Diagram architektury rozwiązania Kubernetes wdrażanej za pomocą usługi Azure Container Service:</span><span class="sxs-lookup"><span data-stu-id="6dc00-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Usługa Azure Container Service skoordynowana do użycia narzędzia Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="6dc00-129">Filmy wideo</span><span class="sxs-lookup"><span data-stu-id="6dc00-129">Videos</span></span>

<span data-ttu-id="6dc00-130">Obsługa klastra Kubernetes w usłudze Azure Container Service (Azure Friday, styczeń 2017 r.):</span><span class="sxs-lookup"><span data-stu-id="6dc00-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="6dc00-131">Narzędzia do tworzenia i wdrażania aplikacji w systemie Kubernetes (Azure OpenDev, czerwiec 2017 r.):</span><span class="sxs-lookup"><span data-stu-id="6dc00-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="6dc00-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6dc00-132">Next steps</span></span>

<span data-ttu-id="6dc00-133">Zapoznaj się z [przewodnikiem Szybki start dotyczącym rozwiązania Kubernetes](container-service-kubernetes-walkthrough.md), aby rozpocząć eksplorowanie usługi Azure Container Service już dziś.</span><span class="sxs-lookup"><span data-stu-id="6dc00-133">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span></span>