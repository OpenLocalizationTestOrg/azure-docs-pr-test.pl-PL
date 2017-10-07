---
title: "aaaAzure grupy kontenerów wystąpień kontenera"
description: "Zrozumienie, jak działają grupy kontenerów w wystąpień kontenera platformy Azure"
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
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="16efe-103">Kontener grupy wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="16efe-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="16efe-104">Witaj zasobu najwyższego poziomu w wystąpień kontenera Azure to grupa kontenera.</span><span class="sxs-lookup"><span data-stu-id="16efe-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="16efe-105">W tym artykule opisano, co to są grupy kontenerów i jakie typy scenariuszy umożliwiają one.</span><span class="sxs-lookup"><span data-stu-id="16efe-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="16efe-106">Jak działa grupa kontenera</span><span class="sxs-lookup"><span data-stu-id="16efe-106">How a container group works</span></span>

<span data-ttu-id="16efe-107">Grupy kontenerów jest kolekcją kontenerów, które są planowane na powitania sam host maszyny i udostępniać cykl, sieci lokalnej i woluminy magazynu.</span><span class="sxs-lookup"><span data-stu-id="16efe-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="16efe-108">Jest podobne koncepcji toohello *pod* w [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) i [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="16efe-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="16efe-109">Witaj poniższym diagramie przedstawiono przykład grupy kontenera, który zawiera wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="16efe-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Przykład grupy kontenera][container-groups-example]

<span data-ttu-id="16efe-111">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="16efe-111">Note that:</span></span>

- <span data-ttu-id="16efe-112">grupy Hello jest zaplanowane na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="16efe-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="16efe-113">grupy Hello udostępnia jeden publiczny adres IP, z jedną dostępnego portu.</span><span class="sxs-lookup"><span data-stu-id="16efe-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="16efe-114">Grupa Hello składa się z dwóch kontenerów.</span><span class="sxs-lookup"><span data-stu-id="16efe-114">hello group is made up of two containers.</span></span> <span data-ttu-id="16efe-115">Jeden kontener nasłuchuje na porcie 80, podczas gdy inne hello nasłuchuje na porcie 5000.</span><span class="sxs-lookup"><span data-stu-id="16efe-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="16efe-116">Grupa Hello obejmuje dwa udziały plików platformy Azure jako instalacji woluminu i każdego kontenera instaluje jeden udziałów hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="16efe-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="16efe-117">Sieć</span><span class="sxs-lookup"><span data-stu-id="16efe-117">Networking</span></span>

<span data-ttu-id="16efe-118">Kontener grupy mają adres IP i port przestrzeni nazw na ten adres IP.</span><span class="sxs-lookup"><span data-stu-id="16efe-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="16efe-119">tooreach klientów zewnętrznych tooenable kontenera w obrębie grupy hello, musi ujawniać portu hello hello adresu IP i z hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="16efe-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="16efe-120">Ponieważ kontenery w ramach grupy hello udział portu przestrzeni nazw, mapowanie portów nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="16efe-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="16efe-121">Kontenery w obrębie grupy może nawiązać połączenie wzajemnie za pośrednictwem hosta lokalnego na powitania porty, które mają one dostępne, nawet jeśli te porty nie są widoczne zewnętrznie na adres IP hello grupy.</span><span class="sxs-lookup"><span data-stu-id="16efe-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="16efe-122">Magazyn</span><span class="sxs-lookup"><span data-stu-id="16efe-122">Storage</span></span>

<span data-ttu-id="16efe-123">Można określić toomount zewnętrznych woluminy w grupie kontenera.</span><span class="sxs-lookup"><span data-stu-id="16efe-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="16efe-124">Woluminy można mapować do określonej ścieżki w poszczególnych kontenerach hello w grupie.</span><span class="sxs-lookup"><span data-stu-id="16efe-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="16efe-125">Typowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="16efe-125">Common scenarios</span></span>

<span data-ttu-id="16efe-126">Kontener wielu grup są przydatne w sytuacjach, kiedy konieczne toodivide się pojedyncze zadanie funkcjonalności do niewielkiej liczby kontener obrazów, które mogą być dostarczane przez różnych zespołów i mają wymagania dotyczące zasobów oddzielne.</span><span class="sxs-lookup"><span data-stu-id="16efe-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="16efe-127">Przykład użycia mogą obejmować:</span><span class="sxs-lookup"><span data-stu-id="16efe-127">Example usage could include:</span></span>

- <span data-ttu-id="16efe-128">Kontener aplikacji i kontener rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="16efe-128">An application container and a logging container.</span></span> <span data-ttu-id="16efe-129">kontener rejestrowania Hello zbiera dzienniki hello i metryki danych wyjściowych przez głównej aplikacji hello i zapisuje je magazynu długoterminowego toolong.</span><span class="sxs-lookup"><span data-stu-id="16efe-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="16efe-130">Aplikacja i monitorowania kontenera.</span><span class="sxs-lookup"><span data-stu-id="16efe-130">An application and a monitoring container.</span></span> <span data-ttu-id="16efe-131">Witaj okresowo monitorowania kontenera sprawia, że żądanie toohello aplikacji tooensure jest uruchomiona i odpowiada prawidłowo i zgłasza alert, jeśli nie jest.</span><span class="sxs-lookup"><span data-stu-id="16efe-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="16efe-132">Kontener obsługująca aplikacji sieci web i kontener ściąganie hello najnowsza zawartość z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="16efe-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16efe-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16efe-133">Next steps</span></span>

<span data-ttu-id="16efe-134">Dowiedz się, jak za[wdrożenie grupy kontenera wielu](container-instances-multi-container-group.md) z szablonem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16efe-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png