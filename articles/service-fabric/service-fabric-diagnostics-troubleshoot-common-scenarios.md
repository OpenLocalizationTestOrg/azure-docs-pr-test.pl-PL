---
title: "aaaTroubleshooting z śledzenie zdarzeń | Dokumentacja firmy Microsoft"
description: "Witaj najczęściej występujących problemów podczas wdrażania usługi na usługi sieć szkieletowa usług Microsoft Azure."
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
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="218de-103">Rozwiązywanie typowych problemów podczas wdrażania usługi w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="218de-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="218de-104">Jeśli korzystasz z usług na komputerze dewelopera, jest łatwe toouse [narzędzia do debugowania programu Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="218de-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="218de-105">W przypadku klastrów zdalnego [raportów o kondycji](service-fabric-view-entities-aggregated-health.md) są zawsze toostart dobrym miejscem.</span><span class="sxs-lookup"><span data-stu-id="218de-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="218de-106">Witaj najprostszym tooaccess sposoby te raporty są za pomocą programu PowerShell lub [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="218de-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="218de-107">W tym artykule założono, że debugowania zdalnego klastra i mieć podstawową wiedzę na temat tego, jak toouse jednego z tych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="218de-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="218de-108">Awarii aplikacji</span><span class="sxs-lookup"><span data-stu-id="218de-108">Application crash</span></span>
<span data-ttu-id="218de-109">Witaj "partycji jest poniżej docelowa liczba repliki lub wystąpienie" raport jest wskazuje, że usługa uległa awarii.</span><span class="sxs-lookup"><span data-stu-id="218de-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="218de-110">toofind się, gdy awarii usługi ma nieco więcej dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="218de-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="218de-111">Kiedy usługa jest uruchomiona na dużą skalę, Twój najlepszy przyjaciel zostanie zestaw dobrze przemyślany śladów.</span><span class="sxs-lookup"><span data-stu-id="218de-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="218de-112">Zalecamy wypróbowanie [diagnostyki Azure](service-fabric-diagnostics-how-to-setup-wad.md) zbierania tych danych śledzenia i przy użyciu rozwiązania, takie jak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) do przeglądania i wyszukiwanie hello śladów.</span><span class="sxs-lookup"><span data-stu-id="218de-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![SFX partycji kondycji](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="218de-114">Podczas inicjowania usługi lub aktora</span><span class="sxs-lookup"><span data-stu-id="218de-114">During service or actor initialization</span></span>
<span data-ttu-id="218de-115">Wszelkie wyjątki przed zainicjowaniem hello typ usługi spowoduje, że hello toocrash procesu.</span><span class="sxs-lookup"><span data-stu-id="218de-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="218de-116">Dla tego typu awarii (Crash) w dzienniku zdarzeń aplikacji hello wyświetli błąd hello z usługi.</span><span class="sxs-lookup"><span data-stu-id="218de-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="218de-117">Są to najczęściej toosee wyjątki hello przed zainicjowaniem hello usługi.</span><span class="sxs-lookup"><span data-stu-id="218de-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="218de-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="218de-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="218de-119">Ten błąd jest często powodu toomissing zależności zestawu.</span><span class="sxs-lookup"><span data-stu-id="218de-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="218de-120">Sprawdź właściwość CopyLocal hello w Visual Studio lub hello Globalna pamięć podręczna zestawów hello węzła.</span><span class="sxs-lookup"><span data-stu-id="218de-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="218de-121">***System.Runtime.InteropServices.COMException*** *w System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="218de-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="218de-122">Oznacza to, że nazwa typu usługi zarejestrowanych hello jest niezgodna z hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="218de-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="218de-123">[Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md) mogą być automatycznie dziennik zdarzeń aplikacji hello tooupload skonfigurowanych dla wszystkich węzłów.</span><span class="sxs-lookup"><span data-stu-id="218de-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="218de-124">RunAsync() lub OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="218de-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="218de-125">W przypadku awarii hello odbywa się podczas inicjowania hello lub systemem typu zarejestrowanej usługi lub aktora, hello wyjątek zostanie przechwycony przez sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="218de-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="218de-126">Możesz wyświetlić te od dostawców EventSource hello szczegółowo opisane w sekcji "Następne kroki" hello.</span><span class="sxs-lookup"><span data-stu-id="218de-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="218de-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="218de-127">Next steps</span></span>
<span data-ttu-id="218de-128">Dowiedz się więcej o istniejące dane diagnostyczne udostępniane przez usługi sieć szkieletowa usług:</span><span class="sxs-lookup"><span data-stu-id="218de-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="218de-129">Niezawodne diagnostyki złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="218de-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="218de-130">Niezawodne usługi diagnostyki</span><span class="sxs-lookup"><span data-stu-id="218de-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

