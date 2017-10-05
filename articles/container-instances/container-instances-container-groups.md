---
title: "Kontener grupy wystąpień kontenera platformy Azure"
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
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="61586-103">Kontener grupy wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="61586-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="61586-104">Zasób najwyższego poziomu w wystąpień kontenera Azure jest grupy kontenerów.</span><span class="sxs-lookup"><span data-stu-id="61586-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="61586-105">W tym artykule opisano, co to są grupy kontenerów i jakie typy scenariuszy umożliwiają one.</span><span class="sxs-lookup"><span data-stu-id="61586-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="61586-106">Jak działa grupa kontenera</span><span class="sxs-lookup"><span data-stu-id="61586-106">How a container group works</span></span>

<span data-ttu-id="61586-107">Grupy kontenerów jest kolekcją kontenerów, które są planowane na tym samym komputerze-hoście i udostępniać cykl, sieci lokalnej i woluminy magazynu.</span><span class="sxs-lookup"><span data-stu-id="61586-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="61586-108">Jest on podobny do koncepcji *pod* w [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) i [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="61586-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="61586-109">Na poniższym diagramie przedstawiono przykład grupy kontenera, który zawiera wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="61586-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![Przykład grupy kontenera][container-groups-example]

<span data-ttu-id="61586-111">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="61586-111">Note that:</span></span>

- <span data-ttu-id="61586-112">Grupa jest zaplanowane na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="61586-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="61586-113">Grupa przedstawia jeden publiczny adres IP, z jedną dostępnego portu.</span><span class="sxs-lookup"><span data-stu-id="61586-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="61586-114">Grupa składa się z dwóch kontenerów.</span><span class="sxs-lookup"><span data-stu-id="61586-114">The group is made up of two containers.</span></span> <span data-ttu-id="61586-115">Jeden kontener nasłuchuje na porcie 80, podczas innych wykrywa port 5000.</span><span class="sxs-lookup"><span data-stu-id="61586-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="61586-116">Grupa zawiera dwa udziały plików platformy Azure jako instalacji woluminu i każdego kontenera instaluje jednej akcji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="61586-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="61586-117">Sieć</span><span class="sxs-lookup"><span data-stu-id="61586-117">Networking</span></span>

<span data-ttu-id="61586-118">Kontener grupy mają adres IP i port przestrzeni nazw na ten adres IP.</span><span class="sxs-lookup"><span data-stu-id="61586-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="61586-119">Aby umożliwić klientom zewnętrznych do kontenera w obrębie grupy, musi ujawniać port, na adres IP i z kontenera.</span><span class="sxs-lookup"><span data-stu-id="61586-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="61586-120">Ponieważ kontenery w ramach grupy używają portu przestrzeni nazw, mapowanie portów nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="61586-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="61586-121">Kontenery w obrębie grupy może nawiązać połączenie wzajemnie za pośrednictwem hosta lokalnego na portach, które mają one dostępne, nawet jeśli te porty nie są widoczne zewnętrznie na adres IP grupy.</span><span class="sxs-lookup"><span data-stu-id="61586-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="61586-122">Magazyn</span><span class="sxs-lookup"><span data-stu-id="61586-122">Storage</span></span>

<span data-ttu-id="61586-123">Można określić zewnętrzne woluminów należy zainstalować w grupie kontenera.</span><span class="sxs-lookup"><span data-stu-id="61586-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="61586-124">Woluminy można mapować do określonej ścieżki w ramach poszczególnych kontenerów w grupie.</span><span class="sxs-lookup"><span data-stu-id="61586-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="61586-125">Typowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="61586-125">Common scenarios</span></span>

<span data-ttu-id="61586-126">Kontener wielu grupy są przydatne w sytuacjach, w miejsce podział pojedyncze zadanie funkcjonalności do niewielkiej liczby kontener obrazów, które mogą być dostarczane przez różnych zespołów i mieć zasobów oddzielne wymagania.</span><span class="sxs-lookup"><span data-stu-id="61586-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="61586-127">Przykład użycia mogą obejmować:</span><span class="sxs-lookup"><span data-stu-id="61586-127">Example usage could include:</span></span>

- <span data-ttu-id="61586-128">Kontener aplikacji i kontener rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="61586-128">An application container and a logging container.</span></span> <span data-ttu-id="61586-129">Kontener rejestrowania zbiera dane wyjściowe dzienników i metryk przechowywanych w ramach aplikacji głównej i zapisuje je do magazynu długoterminowego.</span><span class="sxs-lookup"><span data-stu-id="61586-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="61586-130">Aplikacja i monitorowania kontenera.</span><span class="sxs-lookup"><span data-stu-id="61586-130">An application and a monitoring container.</span></span> <span data-ttu-id="61586-131">Kontener monitorowania okresowo wysyła żądanie do aplikacji, aby upewnić się, że jest uruchomiona i odpowiada prawidłowo i zgłasza alert, jeśli nie jest.</span><span class="sxs-lookup"><span data-stu-id="61586-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="61586-132">Kontener obsługująca aplikacji sieci web i kontener ściąganie najnowsza zawartość z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="61586-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61586-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61586-133">Next steps</span></span>

<span data-ttu-id="61586-134">Dowiedz się, jak [wdrożenie grupy kontenera wielu](container-instances-multi-container-group.md) z szablonem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61586-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png