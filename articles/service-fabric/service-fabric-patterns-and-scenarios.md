---
title: "aaaAzure sieci szkieletowej usług wzorców i scenariusze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, najlepsze rozwiązania i sprawdzonych wzorców wielokrotnego użytku toodesign, tworzy i wykorzystuje Twojej mikrousług w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="bc324-103">Scenariusze i wzorce sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="bc324-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="bc324-104">Jeśli rozważasz usługę kompilowania dużych mikrousług przy użyciu usługi Azure Service Fabric, Dowiedz się od ekspertów hello, którzy zaprojektowany i zbudowany ta platforma jako usługa (PaaS).</span><span class="sxs-lookup"><span data-stu-id="bc324-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="bc324-105">Wprowadzenie do architektury właściwe, a następnie Dowiedz się, jak toooptimize zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc324-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="bc324-106">Witaj [usługi sieć szkieletowa Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) plan odpowiedzi na pytania hello najczęściej zadawane przez klientów rzeczywistych scenariuszy sieci szkieletowej usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc324-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="bc324-107">Dowiedz się, jak toodesign, tworzenie i działanie programu mikrousług w sieci szkieletowej usług za pomocą najlepszych rozwiązań i wzorców sprawdzona, wielokrotnego użytku.</span><span class="sxs-lookup"><span data-stu-id="bc324-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="bc324-108">Zapoznaj się z omówieniem usługi sieć szkieletowa usług, a następnie głębokość Poznaj tematów, które obejmują optymalizacji klastra i zabezpieczeń, migrowanie starszych aplikacji IoT na dużą skalę, hosting aparaty gier i inne.</span><span class="sxs-lookup"><span data-stu-id="bc324-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="bc324-109">Obejrzyj ciągłego dostarczania dla różnych obciążeń i nawet uzyskać hello szczegóły dotyczące obsługi systemu Linux i kontenerów.</span><span class="sxs-lookup"><span data-stu-id="bc324-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="bc324-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="bc324-110">Introduction</span></span>
<span data-ttu-id="bc324-111">Eksploruj najlepszych rozwiązań i Dowiedz się więcej o wybieraniu platforma jako usługa (PaaS) przez infrastrukturę jako usługę (IaaS).</span><span class="sxs-lookup"><span data-stu-id="bc324-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="bc324-112">Uzyskiwanie szczegółowych informacji hello na następujące zasady projektowania sprawdzonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc324-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="bc324-113">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-113">Video</span></span></th><th><span data-ttu-id="bc324-114">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Wprowadzenie tooService sieci szkieletowej</a></span><span class="sxs-lookup"><span data-stu-id="bc324-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="bc324-116">Planowanie klastra i zarządzania</span><span class="sxs-lookup"><span data-stu-id="bc324-116">Cluster planning and management</span></span>
<span data-ttu-id="bc324-117">Więcej informacji na temat planowania pojemności, optymalizacja klastra i zabezpieczenia klastra, w tym przyjrzeć sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="bc324-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="bc324-118">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-118">Video</span></span></th><th><span data-ttu-id="bc324-119">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="bc324-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planowanie klastra i zarządzania</a></span><span class="sxs-lookup"><span data-stu-id="bc324-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="bc324-121">Funkcji Hyper skali sieci web</span><span class="sxs-lookup"><span data-stu-id="bc324-121">Hyper-scale web</span></span>
<span data-ttu-id="bc324-122">Przegląd pojęć wokół hiperskali sieci web, w tym dostępności i niezawodności, hiperskali i zarządzanie stanem.</span><span class="sxs-lookup"><span data-stu-id="bc324-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="bc324-123">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-123">Video</span></span></th><th><span data-ttu-id="bc324-124">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Funkcji Hyper skali sieci web</a></span><span class="sxs-lookup"><span data-stu-id="bc324-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="bc324-126">IoT</span><span class="sxs-lookup"><span data-stu-id="bc324-126">IoT</span></span>
<span data-ttu-id="bc324-127">Poznaj hello Internetu rzeczy (IoT) w kontekście hello sieć szkieletowa usług Azure, w tym hello Azure IoT potoku, obsługi wielu dzierżawców i IoT na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="bc324-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="bc324-128">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-128">Video</span></span></th><th><span data-ttu-id="bc324-129">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="bc324-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="bc324-131">Gry</span><span class="sxs-lookup"><span data-stu-id="bc324-131">Gaming</span></span>
<span data-ttu-id="bc324-132">Spójrz na Włącz gier, interaktywne gry i hostingu istniejących aparaty gier.</span><span class="sxs-lookup"><span data-stu-id="bc324-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="bc324-133">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-133">Video</span></span></th><th><span data-ttu-id="bc324-134">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gry</a></span><span class="sxs-lookup"><span data-stu-id="bc324-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="bc324-136">Ciągłe dostarczanie</span><span class="sxs-lookup"><span data-stu-id="bc324-136">Continuous delivery</span></span>
<span data-ttu-id="bc324-137">Poznaj pojęcia, włącznie z ciągłej integracji/ciągłego dostarczania z Visual Studio Team Services, kompilacji/pakowania/publikowania przepływu pracy, środowisko instalacji i udziału pakietu usług.</span><span class="sxs-lookup"><span data-stu-id="bc324-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="bc324-138">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-138">Video</span></span></th><th><span data-ttu-id="bc324-139">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Ciągłego dostarczania</a></span><span class="sxs-lookup"><span data-stu-id="bc324-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="bc324-141">Migracja</span><span class="sxs-lookup"><span data-stu-id="bc324-141">Migration</span></span>
<span data-ttu-id="bc324-142">Więcej informacji na temat migracji z usługi w chmurze, oprócz toomigration starsze aplikacje.</span><span class="sxs-lookup"><span data-stu-id="bc324-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="bc324-143">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-143">Video</span></span></th><th><span data-ttu-id="bc324-144">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migracji</a></span><span class="sxs-lookup"><span data-stu-id="bc324-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="bc324-146">Kontenery i obsługi systemu Linux</span><span class="sxs-lookup"><span data-stu-id="bc324-146">Containers and Linux support</span></span>
<span data-ttu-id="bc324-147">Pobierz hello odpowiedzi na pytanie toohello, "Dlaczego kontenery?"</span><span class="sxs-lookup"><span data-stu-id="bc324-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="bc324-148">Więcej informacji na temat podglądu hello kontenery systemu Windows, Linux obsługuje i aranżacji kontenery systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="bc324-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="bc324-149">Ponadto dowiedzieć się, jak tooLinux aplikacji .NET Core toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bc324-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="bc324-150">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="bc324-150">Video</span></span></th><th><span data-ttu-id="bc324-151">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="bc324-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="bc324-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Kontenery i obsługi systemu Linux</a></span><span class="sxs-lookup"><span data-stu-id="bc324-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="bc324-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc324-153">Next steps</span></span>
<span data-ttu-id="bc324-154">Teraz, kiedy znasz scenariusze i platformy Service Fabric wzorce, przeczytaj więcej na temat sposobu zbyt[tworzenia i zarządzania klastrami](service-fabric-deploy-anywhere.md), [migracji usługi w chmurze tooService aplikacji sieci szkieletowej](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [— Konfiguracja ciągłego dostarczania](service-fabric-set-up-continuous-integration.md), i [wdrażanie kontenerów](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc324-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
