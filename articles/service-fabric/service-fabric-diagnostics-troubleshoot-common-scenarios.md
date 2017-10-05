---
title: "Rozwiązywanie problemów z śledzenie zdarzeń | Dokumentacja firmy Microsoft"
description: "Najczęściej występujących problemów podczas wdrażania usługi na usługi sieć szkieletowa usług Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="fe02a-103">Rozwiązywanie typowych problemów podczas wdrażania usługi w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="fe02a-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="fe02a-104">Jeśli korzystasz z usług na komputerze dewelopera, jest łatwy w użyciu [narzędzia do debugowania programu Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="fe02a-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="fe02a-105">W przypadku klastrów zdalnego [raportów o kondycji](service-fabric-view-entities-aggregated-health.md) zawsze są dobrym miejscem do rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="fe02a-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="fe02a-106">Najprostszym sposobem dostęp do tych raportów jest za pomocą programu PowerShell lub [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="fe02a-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="fe02a-107">W tym artykule założono, że debugowania zdalnego klastra i mieć podstawową wiedzę na temat sposobów użycia jednej z tych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="fe02a-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="fe02a-108">Awarii aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe02a-108">Application crash</span></span>
<span data-ttu-id="fe02a-109">"Partycji jest poniżej docelowa liczba repliki lub wystąpienie" raport jest wskazuje, że usługa uległa awarii.</span><span class="sxs-lookup"><span data-stu-id="fe02a-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="fe02a-110">Aby dowiedzieć się, gdy awarii usługi ma nieco więcej dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="fe02a-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="fe02a-111">Kiedy usługa jest uruchomiona na dużą skalę, Twój najlepszy przyjaciel zostanie zestaw dobrze przemyślany śladów.</span><span class="sxs-lookup"><span data-stu-id="fe02a-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="fe02a-112">Zalecamy wypróbowanie [diagnostyki Azure](service-fabric-diagnostics-how-to-setup-wad.md) zbierania tych danych śledzenia i przy użyciu rozwiązania, takie jak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) do przeglądania i wyszukiwanie dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="fe02a-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![SFX partycji kondycji](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="fe02a-114">Podczas inicjowania usługi lub aktora</span><span class="sxs-lookup"><span data-stu-id="fe02a-114">During service or actor initialization</span></span>
<span data-ttu-id="fe02a-115">Wszelkie wyjątki przed zainicjowaniem typu usługi spowoduje, że proces awarii.</span><span class="sxs-lookup"><span data-stu-id="fe02a-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="fe02a-116">W przypadku tych typów awarii w dzienniku zdarzeń aplikacji zostaną wyświetlone błędu z usługi.</span><span class="sxs-lookup"><span data-stu-id="fe02a-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="fe02a-117">Są to najczęściej wyjątki, aby zobaczyć przed zainicjowaniem usługi.</span><span class="sxs-lookup"><span data-stu-id="fe02a-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="fe02a-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="fe02a-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="fe02a-119">Ten błąd jest często z powodu braku zależności zestawu.</span><span class="sxs-lookup"><span data-stu-id="fe02a-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="fe02a-120">Sprawdź właściwość CopyLocal w Visual Studio lub w globalnej pamięci podręcznej zestawów dla węzła.</span><span class="sxs-lookup"><span data-stu-id="fe02a-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="fe02a-121">***System.Runtime.InteropServices.COMException*** *w System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="fe02a-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="fe02a-122">Oznacza to, że nazwa typu zarejestrowanej usługi nie jest zgodna manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="fe02a-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="fe02a-123">[Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md) można skonfigurować, aby automatycznie przekazać wszystkie węzły w dzienniku zdarzeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe02a-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="fe02a-124">RunAsync() lub OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="fe02a-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="fe02a-125">W przypadku awarii podczas inicjowania lub systemem typu zarejestrowanej usługi lub aktora, wyjątek zostanie przechwycony przez sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="fe02a-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="fe02a-126">Możesz wyświetlić te od dostawców EventSource szczegółowo opisane w sekcji "Następne kroki".</span><span class="sxs-lookup"><span data-stu-id="fe02a-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe02a-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe02a-127">Next steps</span></span>
<span data-ttu-id="fe02a-128">Dowiedz się więcej o istniejące dane diagnostyczne udostępniane przez usługi sieć szkieletowa usług:</span><span class="sxs-lookup"><span data-stu-id="fe02a-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="fe02a-129">Niezawodne diagnostyki złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="fe02a-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="fe02a-130">Niezawodne usługi diagnostyki</span><span class="sxs-lookup"><span data-stu-id="fe02a-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

