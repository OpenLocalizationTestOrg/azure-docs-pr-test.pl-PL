---
title: "Scenariusze i wzorców usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, najlepsze rozwiązania i sprawdzonych wzorców wielokrotnego użytku, projektowanie, tworzenie i obsługi Twojej mikrousług w sieci szkieletowej usług."
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
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="447f0-103">Scenariusze i wzorce sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="447f0-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="447f0-104">Jeśli rozważasz usługę kompilowania dużych mikrousług przy użyciu usługi Azure Service Fabric, Dowiedz się od ekspertów, którzy zaprojektowany i zbudowany ta platforma jako usługa (PaaS).</span><span class="sxs-lookup"><span data-stu-id="447f0-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="447f0-105">Wprowadzenie do architektury właściwe, a następnie Dowiedz się, jak zoptymalizować zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="447f0-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="447f0-106">[Usługi sieć szkieletowa Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) plan odpowiedzi na pytania najczęściej zadawane przez klientów rzeczywistych scenariuszy sieci szkieletowej usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="447f0-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="447f0-107">Dowiedz się, jak projektować i opracowywać mikrousługi oraz korzystać z nich w usłudze Service Fabric, korzystając z najlepszych rozwiązań i sprawdzonych wzorców z możliwością ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="447f0-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="447f0-108">Zapoznaj się z omówieniem usługi sieć szkieletowa usług, a następnie głębokość Poznaj tematów, które obejmują optymalizacji klastra i zabezpieczeń, migrowanie starszych aplikacji IoT na dużą skalę, hosting aparaty gier i inne.</span><span class="sxs-lookup"><span data-stu-id="447f0-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="447f0-109">Obejrzyj ciągłego dostarczania dla różnych obciążeń i nawet uzyskać szczegółowe informacje o pomocy technicznej systemu Linux i kontenerów.</span><span class="sxs-lookup"><span data-stu-id="447f0-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="447f0-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="447f0-110">Introduction</span></span>
<span data-ttu-id="447f0-111">Eksploruj najlepszych rozwiązań i Dowiedz się więcej o wybieraniu platforma jako usługa (PaaS) przez infrastrukturę jako usługę (IaaS).</span><span class="sxs-lookup"><span data-stu-id="447f0-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="447f0-112">Szczegółowe informacje o następujących zasadach projektowania sprawdzonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="447f0-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="447f0-113">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-113">Video</span></span></th><th><span data-ttu-id="447f0-114">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Wprowadzenie do sieci szkieletowej usług</a></span><span class="sxs-lookup"><span data-stu-id="447f0-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="447f0-116">Planowanie klastra i zarządzania</span><span class="sxs-lookup"><span data-stu-id="447f0-116">Cluster planning and management</span></span>
<span data-ttu-id="447f0-117">Więcej informacji na temat planowania pojemności, optymalizacja klastra i zabezpieczenia klastra, w tym przyjrzeć sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="447f0-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="447f0-118">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-118">Video</span></span></th><th><span data-ttu-id="447f0-119">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="447f0-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planowanie klastra i zarządzania</a></span><span class="sxs-lookup"><span data-stu-id="447f0-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="447f0-121">Funkcji Hyper skali sieci web</span><span class="sxs-lookup"><span data-stu-id="447f0-121">Hyper-scale web</span></span>
<span data-ttu-id="447f0-122">Przegląd pojęć wokół hiperskali sieci web, w tym dostępności i niezawodności, hiperskali i zarządzanie stanem.</span><span class="sxs-lookup"><span data-stu-id="447f0-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="447f0-123">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-123">Video</span></span></th><th><span data-ttu-id="447f0-124">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Funkcji Hyper skali sieci web</a></span><span class="sxs-lookup"><span data-stu-id="447f0-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="447f0-126">IoT</span><span class="sxs-lookup"><span data-stu-id="447f0-126">IoT</span></span>
<span data-ttu-id="447f0-127">Poznaj Internetu rzeczy (IoT) w kontekście sieci szkieletowej usług Azure, w tym potoku, obsługi wielu dzierżawców i IoT Azure IoT na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="447f0-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="447f0-128">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-128">Video</span></span></th><th><span data-ttu-id="447f0-129">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="447f0-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="447f0-131">Gry</span><span class="sxs-lookup"><span data-stu-id="447f0-131">Gaming</span></span>
<span data-ttu-id="447f0-132">Spójrz na Włącz gier, interaktywne gry i hostingu istniejących aparaty gier.</span><span class="sxs-lookup"><span data-stu-id="447f0-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="447f0-133">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-133">Video</span></span></th><th><span data-ttu-id="447f0-134">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gry</a></span><span class="sxs-lookup"><span data-stu-id="447f0-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="447f0-136">Ciągłe dostarczanie</span><span class="sxs-lookup"><span data-stu-id="447f0-136">Continuous delivery</span></span>
<span data-ttu-id="447f0-137">Poznaj pojęcia, włącznie z ciągłej integracji/ciągłego dostarczania z Visual Studio Team Services, kompilacji/pakowania/publikowania przepływu pracy, środowisko instalacji i udziału pakietu usług.</span><span class="sxs-lookup"><span data-stu-id="447f0-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="447f0-138">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-138">Video</span></span></th><th><span data-ttu-id="447f0-139">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Ciągłego dostarczania</a></span><span class="sxs-lookup"><span data-stu-id="447f0-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="447f0-141">Migracja</span><span class="sxs-lookup"><span data-stu-id="447f0-141">Migration</span></span>
<span data-ttu-id="447f0-142">Więcej informacji na temat migracji z usługi w chmurze, oprócz migracji starsze aplikacje.</span><span class="sxs-lookup"><span data-stu-id="447f0-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="447f0-143">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-143">Video</span></span></th><th><span data-ttu-id="447f0-144">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migracji</a></span><span class="sxs-lookup"><span data-stu-id="447f0-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="447f0-146">Kontenery i obsługi systemu Linux</span><span class="sxs-lookup"><span data-stu-id="447f0-146">Containers and Linux support</span></span>
<span data-ttu-id="447f0-147">Uzyskaj odpowiedzi na pytanie "Dlaczego kontenery?"</span><span class="sxs-lookup"><span data-stu-id="447f0-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="447f0-148">Więcej informacji na temat podglądu kontenery systemu Windows, Linux obsługuje i aranżacji kontenery systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="447f0-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="447f0-149">Ponadto dowiedzieć się, jak przeprowadzić migrację aplikacji .NET Core do systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="447f0-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="447f0-150">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="447f0-150">Video</span></span></th><th><span data-ttu-id="447f0-151">PowerPoint talii</span><span class="sxs-lookup"><span data-stu-id="447f0-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="447f0-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Kontenery i obsługi systemu Linux</a></span><span class="sxs-lookup"><span data-stu-id="447f0-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="447f0-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="447f0-153">Next steps</span></span>
<span data-ttu-id="447f0-154">Teraz, kiedy znasz już o wzorce sieci szkieletowej usług i scenariusze, Dowiedz się więcej o sposobie [tworzenia i zarządzania klastrami](service-fabric-deploy-anywhere.md), [migracji aplikacji usługi w chmurze do sieci szkieletowej usług](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [— Konfiguracja ciągłego dostarczania](service-fabric-set-up-continuous-integration.md), i [wdrażanie kontenerów](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="447f0-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
