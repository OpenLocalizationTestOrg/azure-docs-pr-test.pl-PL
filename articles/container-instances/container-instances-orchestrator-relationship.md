---
title: "aaaAzure wystąpień kontenera i aranżacji kontenera"
description: "Zrozumienie sposobu wystąpień kontenera Azure interakcji z orchestrators kontenera"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="d3e49-103">Wystąpień kontenera Azure i orchestrators kontenera</span><span class="sxs-lookup"><span data-stu-id="d3e49-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="d3e49-104">Ze względu na ich niewielki rozmiar i orientację aplikacji kontenerów dobrze nadają w środowiskach agile dostarczania i architektury mikrousługi systemem.</span><span class="sxs-lookup"><span data-stu-id="d3e49-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="d3e49-105">zadanie Hello automatyzacji i zarządzanie dużą liczbę kontenerów i sposób ich interakcji nosi nazwę *aranżacji*.</span><span class="sxs-lookup"><span data-stu-id="d3e49-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="d3e49-106">Kontener popularnych orchestrators obejmują Kubernetes DC/OS i Docker Swarm, które są dostępne w hello [usługi kontenera platformy Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="d3e49-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="d3e49-107">Wystąpień kontenera Azure zawiera niektóre z hello podstawowe planowanie możliwości platform aranżacji, ale nie obejmuje usług wyższa wartość hello czy tych platform zapewniają i w rzeczywistości może być uzupełniające się z nimi.</span><span class="sxs-lookup"><span data-stu-id="d3e49-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="d3e49-108">W tym artykule opisano zakres hello obsługuje wystąpień kontenera Azure i jakiego orchestrators kontener może korzystać z niego.</span><span class="sxs-lookup"><span data-stu-id="d3e49-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="d3e49-109">Tradycyjny aranżacji</span><span class="sxs-lookup"><span data-stu-id="d3e49-109">Traditional orchestration</span></span>

<span data-ttu-id="d3e49-110">Definicja standardowe Hello aranżacji obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d3e49-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="d3e49-111">**Planowanie**: danego obrazu kontenera i żądanie zasobu, Znajdź odpowiedniego komputera na powitania toorun kontenera.</span><span class="sxs-lookup"><span data-stu-id="d3e49-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="d3e49-112">**Koligacja/przeciwko-affinity**: określić, że zestaw kontenery powinien uruchomione w pobliżu innych (na wydajność) lub wystarczająco liniami (dostępności).</span><span class="sxs-lookup"><span data-stu-id="d3e49-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="d3e49-113">**Monitorowanie kondycji**: Obejrzyj niepowodzeń kontenera i automatycznie Zaplanuj je ponownie.</span><span class="sxs-lookup"><span data-stu-id="d3e49-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="d3e49-114">**Tryb failover**: Śledź co działa na każdym komputerze i ponowne planowanie kontenery z węzłów toohealthy maszyn nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="d3e49-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="d3e49-115">**Skalowanie**: Dodawanie lub usuwanie żądanie toomatch wystąpień kontenera, ręcznie lub automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d3e49-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="d3e49-116">**Sieć**: Podaj sieci nakładki koordynacji toocommunicate kontenery na wielu komputerach hosta.</span><span class="sxs-lookup"><span data-stu-id="d3e49-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="d3e49-117">**Odnajdowanie usługi**: toolocate kontenery wzajemnie automatycznie włączyć nawet podczas przenoszenia między komputerami hostów i zmiana adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d3e49-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="d3e49-118">**Koordynowane uaktualnień aplikacji**: Zarządzanie aplikacją tooavoid uaktualnień kontenera czas przestoju i włączyć wycofywanie, jeśli jakaś nieprawidłowość.</span><span class="sxs-lookup"><span data-stu-id="d3e49-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="d3e49-119">Orchestration z wystąpień kontenera platformy Azure: warstwowego podejścia</span><span class="sxs-lookup"><span data-stu-id="d3e49-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="d3e49-120">Wystąpień kontenera Azure umożliwia tooorchestration warstwowego podejścia, podając wszystkie hello planowania i możliwości zarządzania wymagane toorun jeden kontener, umożliwiając orchestrator platform toomanage kontenera wielu zadań na nim.</span><span class="sxs-lookup"><span data-stu-id="d3e49-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="d3e49-121">Ponieważ wszystkie hello podstawowej infrastruktury dla wystąpień kontenera jest zarządzane przez usługę Azure, platformy orchestrator nie jest konieczne tooconcern się z znajdowanie maszyny do odpowiedniego hosta, na które toorun jeden kontener.</span><span class="sxs-lookup"><span data-stu-id="d3e49-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="d3e49-122">elastyczność Hello chmury hello gwarantuje, że co jest zawsze dostępna.</span><span class="sxs-lookup"><span data-stu-id="d3e49-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="d3e49-123">Zamiast tego hello orchestrator można skoncentrować się na powitania zadania, które upraszczają programowanie hello architektury usługi kontenera, w tym skalowanie i skoordynowany sposób uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="d3e49-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="d3e49-124">Potencjalne scenariusze</span><span class="sxs-lookup"><span data-stu-id="d3e49-124">Potential scenarios</span></span>

<span data-ttu-id="d3e49-125">Podczas integracji programu orchestrator z wystąpień kontenera Azure jest nadal rodzącego, przewidujemy, że mogą pojawić się w kilku różnych środowiskach:</span><span class="sxs-lookup"><span data-stu-id="d3e49-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="d3e49-126">Orchestration wystąpień kontenera wyłącznie</span><span class="sxs-lookup"><span data-stu-id="d3e49-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="d3e49-127">Ponieważ szybkie rozpoczęcie i naliczać opłaty za hello drugie, środowisko wyłącznie na podstawie wystąpień kontenera Azure oferuje hello najszybszy sposób tooget uruchomiona i toodeal z obciążeniami wysokiej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="d3e49-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="d3e49-128">Kombinacja wystąpień kontenera i kontenerów na maszynach wirtualnych</span><span class="sxs-lookup"><span data-stu-id="d3e49-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="d3e49-129">Dla długotrwałe, obciążeń stabilny, organizowanie kontenery w klastrze dedykowanych maszyn wirtualnych zwykle będzie tańsze niż uruchomienie tego samego kontenery hello z wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="d3e49-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="d3e49-130">Jednak wystąpień kontenera oferuje doskonałe rozwiązanie do szybkiego rozszerzania i instytucje toodeal Twojego ogólną pojemność z nieoczekiwany lub krótkim okresie wzrostów użycia.</span><span class="sxs-lookup"><span data-stu-id="d3e49-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="d3e49-131">Zamiast skalowania hello liczbę maszyn wirtualnych w klastrze, a następnie wdrażanie dodatkowych kontenerów na tych komputerach, hello orchestrator można po prostu zaplanować dodatkowe kontenery hello za pomocą wystąpień kontenera i usunąć je, gdy są one nie już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d3e49-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="d3e49-132">Przykładowe zastosowanie: Azure łącznik wystąpień kontenera dla Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d3e49-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="d3e49-133">toodemonstrate jak kontenera platformy orchestration można zintegrować z wystąpień kontenera platformy Azure, możemy uruchomić budynku [łącznik próbki dla Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="d3e49-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="d3e49-134">Witaj łącznika dla Kubernetes naśladuje hello [kubelet] [ kubelet-doc] przez zarejestrowanie jako węzeł o nieograniczonej pojemności i wysyła tworzenie hello [stanowiskami] [ pod-doc] jako kontenera grupy wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d3e49-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="d3e49-135">Łączniki dla innych orchestrators mogą być zbudowane analogicznie zintegrowaną z platformy podstawowych toocombine hello zasilania programu orchestrator hello interfejsu API za pomocą hello szybkość i łatwość zarządzania kontenerami w wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d3e49-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="d3e49-136">Witaj ACI łącznika jest Kubernetes *eksperymentalne* i nie powinna być używana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d3e49-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3e49-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3e49-137">Next steps</span></span>

<span data-ttu-id="d3e49-138">Tworzenie Twojego pierwszego kontenera z wystąpień kontenera Azure za pomocą hello [Przewodnik Szybki start dotyczący](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="d3e49-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/