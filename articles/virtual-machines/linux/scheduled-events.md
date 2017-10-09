---
title: aaaScheduled zdarzenia dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Zaplanowane zdarzenia przy użyciu usługi Azure metadanych hello pakietu na maszynach wirtualnych systemu Linux."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="534cc-103">Usługa Azure metadanych: Zaplanowanego zdarzenia (wersja zapoznawcza) dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="534cc-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="534cc-104">Podglądy odbywa się dostępne tooyou warunku hello zgadzają się toohello warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="534cc-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="534cc-105">Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="534cc-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="534cc-106">Zaplanowane zdarzenia jest jednym z subservices hello w obszarze hello Azure metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="534cc-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="534cc-107">Jest odpowiedzialny za udostępniając informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="534cc-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="534cc-108">Jest ona dostępna dla wszystkich typów maszyny wirtualnej platformy Azure, w tym PaaS i IaaS.</span><span class="sxs-lookup"><span data-stu-id="534cc-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="534cc-109">Zaplanowane zdarzenia daje zadań zapobiegawczych tooperform czasu maszyny wirtualnej efekt hello toominimize zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="534cc-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="534cc-110">Zaplanowane zdarzenia jest dostępna dla systemów Windows i maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="534cc-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="534cc-111">Informacji o zaplanowane zdarzeń w systemie Windows, temacie [zaplanowane zdarzenia dla maszyn wirtualnych systemu Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="534cc-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="534cc-112">Dlaczego zaplanowane zdarzenia?</span><span class="sxs-lookup"><span data-stu-id="534cc-112">Why Scheduled Events?</span></span>

<span data-ttu-id="534cc-113">Zaplanowane zdarzenia należy wykonać czynności wpływ hello toolimit intiated platformy konserwacji lub akcje inicjowane przez użytkownika w usłudze.</span><span class="sxs-lookup"><span data-stu-id="534cc-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="534cc-114">Mająca wiele wystąpień obciążeń wykorzystujących stan toomaintain techniki replikacji mogą być narażone toooutages wykonywane w wielu wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="534cc-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="534cc-115">Takie jak awarie może spowodować kosztowne zadania (na przykład odbudowywania indeksów) lub nawet utraty repliki.</span><span class="sxs-lookup"><span data-stu-id="534cc-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="534cc-116">W wielu innych przypadkach hello ogólnej dostępności usługi mogą być ulepszane, wykonując takie jak sekwencji łagodne zamykanie Kończenie (lub anulowanie) locie transakcji, ponowne przypisywanie zadań tooother maszyn wirtualnych w klastrze hello (ręcznego przełączania trybu failover) lub usunięcie hello Maszyna wirtualna z puli usługi równoważenia obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="534cc-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="534cc-117">Istnieją przypadki, w którym powiadamianie o tym administratora o nadchodzących zdarzenia lub rejestrowanie takie zdarzenia pomocy poprawy hello użytkowanie hostowanych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="534cc-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="534cc-118">Przypadki użycia Azure usługi metadanych powierzchni zaplanowane zdarzenia w następujących hello:</span><span class="sxs-lookup"><span data-stu-id="534cc-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="534cc-119">Platforma zainicjował konserwacji (na przykład wdrożenie systemu operacyjnego hosta)</span><span class="sxs-lookup"><span data-stu-id="534cc-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="534cc-120">Wywołania zainicjowane przez użytkownika (na przykład użytkownik zostanie ponownie uruchomiony lub wdraża ponownie maszyny Wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="534cc-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="534cc-121">podstawy Hello</span><span class="sxs-lookup"><span data-stu-id="534cc-121">hello basics</span></span>  

<span data-ttu-id="534cc-122">Usługa Azure metadanych przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST jest dostępny w obrębie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="534cc-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="534cc-123">informacje Hello są dostępne za pośrednictwem bez obsługi routingu IP, dzięki czemu nie jest uwidaczniana poza hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="534cc-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="534cc-124">Zakres</span><span class="sxs-lookup"><span data-stu-id="534cc-124">Scope</span></span>
<span data-ttu-id="534cc-125">Zaplanowane zdarzenia są udostępniane tooall maszyn wirtualnych w usłudze w chmurze lub tooall maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="534cc-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="534cc-126">W związku z tym należy sprawdzić hello `Resources` w hello tooidentify zdarzenia, które maszyny wirtualne mają wpływ na toobe.</span><span class="sxs-lookup"><span data-stu-id="534cc-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="534cc-127">Odnajdywanie punktu końcowego hello</span><span class="sxs-lookup"><span data-stu-id="534cc-127">Discovering hello endpoint</span></span>
<span data-ttu-id="534cc-128">W przypadku hello, w którym utworzono maszynę wirtualną w sieć wirtualną (VNet), usługa metadanych hello jest dostępna z statycznego adresu IP bez obsługi routingu, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="534cc-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="534cc-129">Jeśli nie utworzono hello maszyny wirtualnej w ramach sieci wirtualnej, hello domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest wymagane toodiscover hello punktu końcowego toouse.</span><span class="sxs-lookup"><span data-stu-id="534cc-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="534cc-130">Można znaleźć toolearn próbki toothis jak zbyt[odnajdywanie punktu końcowego hosta hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="534cc-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="534cc-131">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="534cc-131">Versioning</span></span> 
<span data-ttu-id="534cc-132">Witaj wystąpienia usługi metadanych jest kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="534cc-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="534cc-133">Wersje są obowiązkowe i hello bieżąca wersja to `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="534cc-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="534cc-134">Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api hello.</span><span class="sxs-lookup"><span data-stu-id="534cc-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="534cc-135">Ten format jest już obsługiwane i zostaną wycofane w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="534cc-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="534cc-136">Korzystanie z nagłówków</span><span class="sxs-lookup"><span data-stu-id="534cc-136">Using headers</span></span>
<span data-ttu-id="534cc-137">Kwerenda hello metadanych usługi, należy określić nagłówek hello `Metadata: true` tooensure hello żądania nie został przypadkowo przekierowany.</span><span class="sxs-lookup"><span data-stu-id="534cc-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="534cc-138">Włączanie zaplanowanego zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="534cc-139">Witaj po raz pierwszy wprowadzone żądania zaplanowanego zdarzenia Azure niejawnie włącza hello funkcji na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="534cc-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="534cc-140">W związku z tym spodziewać opóźnione odpowiedzi w pierwszym wywołaniu się tootwo minut.</span><span class="sxs-lookup"><span data-stu-id="534cc-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="534cc-141">Konserwacja zainicjowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="534cc-141">User initiated maintenance</span></span>
<span data-ttu-id="534cc-142">Użytkownik zainicjował konserwacji maszyny wirtualnej za pomocą hello portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell powoduje zaplanowane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="534cc-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="534cc-143">Umożliwia tootest hello konserwacji przygotowania logikę w aplikacji i pozwala tooprepare Twojej aplikacji do obsługi inicjowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="534cc-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="534cc-144">Ponowne uruchomienie maszyny wirtualnej planuje zdarzenia z typem `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="534cc-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="534cc-145">Ponownego wdrażania maszyny wirtualnej planuje zdarzenia z typem `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="534cc-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="534cc-146">Obecnie maksymalnie 10 operacji konserwacji zainicjowanej przez użytkownika można jednocześnie zaplanować.</span><span class="sxs-lookup"><span data-stu-id="534cc-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="534cc-147">Ten limit zostanie złagodzony przed zaplanowane zdarzenia ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="534cc-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="534cc-148">Wynikiem zaplanowane zdarzenia konserwacji zainicjowanej przez użytkownika nie jest obecnie można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="534cc-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="534cc-149">Konfigurowalne jest planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="534cc-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="534cc-150">Przy użyciu interfejsu API hello</span><span class="sxs-lookup"><span data-stu-id="534cc-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="534cc-151">Zapytania do zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-151">Query for events</span></span>
<span data-ttu-id="534cc-152">Po prostu, wprowadzając następujące hello wywołania mogą wykonywać kwerendę o zaplanowane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="534cc-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="534cc-153">Odpowiedź zawiera tablicę zaplanowanego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="534cc-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="534cc-154">Pusta tablica oznacza, że obecnie nie istnieją żadne zdarzenia według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="534cc-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="534cc-155">W przypadku hello w przypadku zaplanowanego zdarzenia odpowiedź hello zawiera tablicę zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="534cc-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="534cc-156">Właściwości zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-156">Event properties</span></span>
|<span data-ttu-id="534cc-157">Właściwość</span><span class="sxs-lookup"><span data-stu-id="534cc-157">Property</span></span>  |  <span data-ttu-id="534cc-158">Opis</span><span class="sxs-lookup"><span data-stu-id="534cc-158">Description</span></span> |
| - | - |
| <span data-ttu-id="534cc-159">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-159">EventId</span></span> | <span data-ttu-id="534cc-160">Globalnie unikatowy identyfikator dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="534cc-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="534cc-161">Przykład:</span><span class="sxs-lookup"><span data-stu-id="534cc-161">Example:</span></span> <br><ul><li><span data-ttu-id="534cc-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="534cc-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="534cc-163">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-163">EventType</span></span> | <span data-ttu-id="534cc-164">Wpływ powoduje, że to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="534cc-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="534cc-165">Wartości:</span><span class="sxs-lookup"><span data-stu-id="534cc-165">Values:</span></span> <br><ul><li> <span data-ttu-id="534cc-166">`Freeze`: hello maszyny wirtualnej jest zaplanowane toopause kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="534cc-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="534cc-167">Witaj procesora CPU jest wstrzymana, ale nie ma żadnego wpływu na pamięć, otwartych plików lub połączeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="534cc-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="534cc-168">`Reboot`: hello zaplanowano ponownego uruchomienia maszyny wirtualnej (z systemem innym niż trwałej pamięci jest utracone).</span><span class="sxs-lookup"><span data-stu-id="534cc-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="534cc-169">`Redeploy`: hello maszyny wirtualnej jest zaplanowane toomove tooanother węzła (tymczasowych dyski zostaną utracone).</span><span class="sxs-lookup"><span data-stu-id="534cc-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="534cc-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="534cc-170">ResourceType</span></span> | <span data-ttu-id="534cc-171">Typ zasobu, który ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="534cc-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="534cc-172">Wartości:</span><span class="sxs-lookup"><span data-stu-id="534cc-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="534cc-173">Zasoby</span><span class="sxs-lookup"><span data-stu-id="534cc-173">Resources</span></span>| <span data-ttu-id="534cc-174">Lista zasobów, które ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="534cc-174">List of resources this event impacts.</span></span> <span data-ttu-id="534cc-175">Gwarantuje toocontain maszyny z co najwyżej jeden [domeny aktualizacji](manage-availability.md), ale nie może zawierać wszystkie maszyny w hello UD.</span><span class="sxs-lookup"><span data-stu-id="534cc-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="534cc-176">Przykład:</span><span class="sxs-lookup"><span data-stu-id="534cc-176">Example:</span></span> <br><ul><li> <span data-ttu-id="534cc-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="534cc-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="534cc-178">Stan zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-178">Event Status</span></span> | <span data-ttu-id="534cc-179">Stan tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="534cc-179">Status of this event.</span></span> <br><br> <span data-ttu-id="534cc-180">Wartości:</span><span class="sxs-lookup"><span data-stu-id="534cc-180">Values:</span></span> <ul><li><span data-ttu-id="534cc-181">`Scheduled`: To zdarzenie jest zaplanowane toostart po hello czas określony w hello `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="534cc-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="534cc-182">`Started`: To zdarzenie zostało rozpoczęte.</span><span class="sxs-lookup"><span data-stu-id="534cc-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="534cc-183">Nie `Completed` lub podobne stan kiedykolwiek jest dostarczana, zdarzenia hello już zostaną zwrócone, po zakończeniu hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="534cc-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="534cc-184">Nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="534cc-184">NotBefore</span></span>| <span data-ttu-id="534cc-185">Czas, po którym to zdarzenie może zostać uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="534cc-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="534cc-186">Przykład:</span><span class="sxs-lookup"><span data-stu-id="534cc-186">Example:</span></span> <br><ul><li> <span data-ttu-id="534cc-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="534cc-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="534cc-188">Planowanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="534cc-188">Event scheduling</span></span>
<span data-ttu-id="534cc-189">Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości hello na podstawie zdarzeń typu.</span><span class="sxs-lookup"><span data-stu-id="534cc-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="534cc-190">Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="534cc-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="534cc-191">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-191">EventType</span></span>  | <span data-ttu-id="534cc-192">Minimalna powiadomień</span><span class="sxs-lookup"><span data-stu-id="534cc-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="534cc-193">Blokowanie</span><span class="sxs-lookup"><span data-stu-id="534cc-193">Freeze</span></span>| <span data-ttu-id="534cc-194">15 minut</span><span class="sxs-lookup"><span data-stu-id="534cc-194">15 minutes</span></span> |
| <span data-ttu-id="534cc-195">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="534cc-195">Reboot</span></span> | <span data-ttu-id="534cc-196">15 minut</span><span class="sxs-lookup"><span data-stu-id="534cc-196">15 minutes</span></span> |
| <span data-ttu-id="534cc-197">Ponowne wdrożenie</span><span class="sxs-lookup"><span data-stu-id="534cc-197">Redeploy</span></span> | <span data-ttu-id="534cc-198">10 minut</span><span class="sxs-lookup"><span data-stu-id="534cc-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="534cc-199">Uruchamianie zdarzenia</span><span class="sxs-lookup"><span data-stu-id="534cc-199">Starting an event</span></span> 

<span data-ttu-id="534cc-200">Po rozpoznane nadchodzących zdarzenia i ukończyć logiki dla łagodne zamykanie należy zatwierdzić hello zaległych zdarzeń dokonując `POST` wywołania toohello metadanych usługi z hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="534cc-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="534cc-201">Wskazuje tooAzure skrócić powiadomień minimalna hello czasu (jeśli jest to możliwe).</span><span class="sxs-lookup"><span data-stu-id="534cc-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="534cc-202">Potwierdzeniem zdarzenia umożliwia hello tooproceed zdarzeń dla wszystkich `Resources` w zdarzeniu hello hello nie tylko maszynę wirtualną, która potwierdza hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="534cc-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="534cc-203">W związku z tym można tooelect wiodące toocoordinate hello potwierdzenia, które mogą być prosta jako maszynę pierwszej hello na powitania `Resources` pola.</span><span class="sxs-lookup"><span data-stu-id="534cc-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="534cc-204">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="534cc-204">Python sample</span></span> 

<span data-ttu-id="534cc-205">Witaj następujące przykładowe zapytania hello metadane usługi dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="534cc-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="534cc-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="534cc-206">Next steps</span></span> 

- <span data-ttu-id="534cc-207">Dowiedz się więcej o hello interfejsami API dostępnymi w hello [metadanych wystąpienia usługi](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="534cc-207">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="534cc-208">Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="534cc-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
