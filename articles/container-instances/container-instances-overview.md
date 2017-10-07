---
title: "Omówienie wystąpień kontenera aaaAzure | Dokumentacja platformy Azure"
description: "Informacje dotyczące usługi Azure Container Instances"
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="8d007-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="8d007-103">Azure Container Instances</span></span>

<span data-ttu-id="8d007-104">Kontenery staje się szybko hello preferowany sposób toopackage, wdrażanie i zarządzanie aplikacjami w chmurze.</span><span class="sxs-lookup"><span data-stu-id="8d007-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="8d007-105">Wystąpień kontenera Azure oferuje hello najszybszym i Najprostszym sposobem toorun kontenera na platformie Azure, bez konieczności tooprovision wszystkie maszyny wirtualne i bez konieczności tooadopt wyższego poziomu usługi.</span><span class="sxs-lookup"><span data-stu-id="8d007-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="8d007-106">Usługa Azure Container Instances to doskonałe rozwiązanie dla wszystkich scenariuszy, które może działać w kontenerach izolowanych, w tym w przypadku prostych aplikacji, automatyzacji zadań i zadań kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8d007-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="8d007-107">W scenariuszach, w którym musisz mieć pełne aranżacji kontenera, w wielu kontenerów, automatyczne skalowanie i uaktualnień aplikacji w skoordynowany sposób, w tym odnajdywania usługi zalecamy hello [usługi kontenera platformy Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="8d007-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="8d007-108">Krótki czas uruchamiania</span><span class="sxs-lookup"><span data-stu-id="8d007-108">Fast startup times</span></span>

<span data-ttu-id="8d007-109">Kontenery oferują znaczące korzyści związane z uruchamianiem w porównaniu do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8d007-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="8d007-110">Wystąpień kontenera platformy Azure możesz uruchomić kontenera na platformie Azure w sekundach bez tooprovision potrzeby hello i zarządzenie maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="8d007-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="8d007-111">Zabezpieczenia na poziomie funkcji hypervisor</span><span class="sxs-lookup"><span data-stu-id="8d007-111">Hypervisor-level security</span></span>

<span data-ttu-id="8d007-112">W przeszłości kontenery oferowały zarządzanie zasobami i izolację zależności aplikacji, ale nie były wystarczająco odporne na użycie wielu obcych dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="8d007-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="8d007-113">Dzięki usłudze Azure Container Instances aplikacja jest izolowana w kontenerze w takim samym stopniu, w jakim byłaby w maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8d007-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="8d007-114">Rozmiary niestandardowe</span><span class="sxs-lookup"><span data-stu-id="8d007-114">Custom sizes</span></span>

<span data-ttu-id="8d007-115">Kontenery są zwykle zoptymalizowane toorun, który tylko jedną aplikację, ale hello musi dokładnie te aplikacje mogą się znacznie różnić.</span><span class="sxs-lookup"><span data-stu-id="8d007-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="8d007-116">W usłudze Azure Container Instances możesz zażądać dokładnie tylu rdzeni i pamięci, ile potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="8d007-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="8d007-117">Płacisz oparte na możesz poprosić, rozliczony przez hello drugie, tak aby precyzyjne zoptymalizować wydatki na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="8d007-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="8d007-118">Łączność przy użyciu publicznych adresów IP</span><span class="sxs-lookup"><span data-stu-id="8d007-118">Public IP connectivity</span></span>

<span data-ttu-id="8d007-119">Wystąpieniami kontenera Azure mogą uwidaczniać kontenerów bezpośrednio toohello internet z publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="8d007-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="8d007-120">W przyszłości hello firma Microsoft będzie rozwiń naszych sieci możliwości integracji tooinclude z sieciami wirtualnymi, obciążenia równoważenia i innych części core hello Azure infrastruktura sieci.</span><span class="sxs-lookup"><span data-stu-id="8d007-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="8d007-121">Magazyn trwały</span><span class="sxs-lookup"><span data-stu-id="8d007-121">Persistent storage</span></span>

<span data-ttu-id="8d007-122">tooretrieve i utrwalić stanu z wystąpień kontenera platformy Azure, firma Microsoft oferuje udziały plików bezpośrednie instalowanie Azure.</span><span class="sxs-lookup"><span data-stu-id="8d007-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="8d007-123">Kontenery systemów Linux i Windows</span><span class="sxs-lookup"><span data-stu-id="8d007-123">Linux and Windows containers</span></span>

<span data-ttu-id="8d007-124">Z wystąpień kontenera platformy Azure można zaplanować zarówno systemu Windows i Linux kontenerów hello tego samego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8d007-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="8d007-125">Wystarczy wskazać hello podstawowy typ systemu operacyjnego i wszystkich innych urządzeń jest identyczny.</span><span class="sxs-lookup"><span data-stu-id="8d007-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="8d007-126">Grupy planowane wspólnie</span><span class="sxs-lookup"><span data-stu-id="8d007-126">Co-scheduled groups</span></span>

<span data-ttu-id="8d007-127">Usługa Azure Container Instances obsługuje planowanie grup wielu kontenerów, które współużytkują maszynę hosta, sieć lokalną, magazyn i cykl życia.</span><span class="sxs-lookup"><span data-stu-id="8d007-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="8d007-128">Dzięki temu można toocombine głównej aplikacji z innymi działającą w roli pomocniczych, takich jak rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="8d007-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d007-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8d007-129">Next steps</span></span>

<span data-ttu-id="8d007-130">Spróbuj przeprowadzić wdrożenie tooAzure kontenera, z jednego polecenia za pomocą naszych [Przewodnik Szybki Start](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="8d007-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
