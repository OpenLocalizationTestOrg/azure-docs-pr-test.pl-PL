---
title: "aaaScheduled zdarzeń za pomocą usługi Azure metadanych | Dokumentacja firmy Microsoft"
description: "Reagują tooImpactful zdarzenia na maszynie wirtualnej, zanim wystąpią."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="05f8c-103">Usługa Azure metadanych - zaplanowanego zdarzenia (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="05f8c-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="05f8c-104">Podglądy odbywa się dostępne tooyou warunku hello zgadzają się toohello warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="05f8c-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="05f8c-105">Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="05f8c-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="05f8c-106">Zaplanowane zdarzenia jest jednym z subservices hello w obszarze hello Azure metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="05f8c-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="05f8c-107">Jest odpowiedzialny za udostępniając informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="05f8c-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="05f8c-108">Jest ona dostępna dla wszystkich typów maszyny wirtualnej platformy Azure, w tym PaaS i IaaS.</span><span class="sxs-lookup"><span data-stu-id="05f8c-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="05f8c-109">Zaplanowane zdarzenia daje zadań zapobiegawczych tooperform czasu maszyny wirtualnej efekt hello toominimize zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="05f8c-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="05f8c-110">Wprowadzenie — dlaczego zaplanowane zdarzenia?</span><span class="sxs-lookup"><span data-stu-id="05f8c-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="05f8c-111">Zaplanowane zdarzenia należy wykonać czynności wpływ hello toolimit intiated platformy konserwacji lub akcje inicjowane przez użytkownika w usłudze.</span><span class="sxs-lookup"><span data-stu-id="05f8c-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="05f8c-112">Mająca wiele wystąpień obciążeń wykorzystujących stan toomaintain techniki replikacji mogą być narażone toooutages wykonywane w wielu wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="05f8c-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="05f8c-113">Takie jak awarie może spowodować kosztowne zadania (na przykład odbudowywania indeksów) lub nawet utraty repliki.</span><span class="sxs-lookup"><span data-stu-id="05f8c-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="05f8c-114">W wielu innych przypadkach hello ogólnej dostępności usługi mogą być ulepszane, wykonując takie jak sekwencji łagodne zamykanie Kończenie (lub anulowanie) locie transakcji, ponowne przypisywanie zadań tooother maszyn wirtualnych w klastrze hello (ręcznego przełączania trybu failover) lub usunięcie hello Maszyna wirtualna z puli usługi równoważenia obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="05f8c-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="05f8c-115">Istnieją przypadki, w którym powiadamianie o tym administratora o nadchodzących zdarzenia lub rejestrowanie takie zdarzenia pomocy poprawy hello użytkowanie hostowanych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="05f8c-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="05f8c-116">Przypadki użycia Azure usługi metadanych powierzchni zaplanowane zdarzenia w następujących hello:</span><span class="sxs-lookup"><span data-stu-id="05f8c-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="05f8c-117">Platforma zainicjował konserwacji (na przykład wdrożenie systemu operacyjnego hosta)</span><span class="sxs-lookup"><span data-stu-id="05f8c-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="05f8c-118">Wywołania zainicjowane przez użytkownika (na przykład użytkownik zostanie ponownie uruchomiony lub wdraża ponownie maszyny Wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="05f8c-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="05f8c-119">Zaplanowane zdarzenia - hello podstawy</span><span class="sxs-lookup"><span data-stu-id="05f8c-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="05f8c-120">Usługa Azure metadanych przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST jest dostępny w obrębie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05f8c-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="05f8c-121">informacje Hello są dostępne za pośrednictwem bez obsługi routingu IP, dzięki czemu nie jest uwidaczniana poza hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05f8c-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="05f8c-122">Zakres</span><span class="sxs-lookup"><span data-stu-id="05f8c-122">Scope</span></span>
<span data-ttu-id="05f8c-123">Zaplanowane zdarzenia są udostępniane tooall maszyn wirtualnych w usłudze w chmurze lub tooall maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="05f8c-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="05f8c-124">W związku z tym należy sprawdzić hello `Resources` w hello tooidentify zdarzenia, które maszyny wirtualne mają wpływ na toobe.</span><span class="sxs-lookup"><span data-stu-id="05f8c-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="05f8c-125">Odnajdywanie hello punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="05f8c-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="05f8c-126">W przypadku hello, w którym utworzono maszynę wirtualną w sieć wirtualną (VNet), usługa metadanych hello jest dostępna z statycznego adresu IP bez obsługi routingu, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="05f8c-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="05f8c-127">Jeśli nie utworzono hello maszyny wirtualnej w ramach sieci wirtualnej, hello domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest wymagane toodiscover hello punktu końcowego toouse.</span><span class="sxs-lookup"><span data-stu-id="05f8c-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="05f8c-128">Można znaleźć toolearn próbki toothis jak zbyt[odnajdywanie punktu końcowego hosta hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="05f8c-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="05f8c-129">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="05f8c-129">Versioning</span></span> 
<span data-ttu-id="05f8c-130">Witaj wystąpienia usługi metadanych jest kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="05f8c-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="05f8c-131">Wersje są obowiązkowe i hello bieżąca wersja to `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="05f8c-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="05f8c-132">Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api hello.</span><span class="sxs-lookup"><span data-stu-id="05f8c-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="05f8c-133">Ten format jest już obsługiwane i zostaną wycofane w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="05f8c-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="05f8c-134">Korzystanie z nagłówków</span><span class="sxs-lookup"><span data-stu-id="05f8c-134">Using Headers</span></span>
<span data-ttu-id="05f8c-135">Kwerenda hello metadanych usługi, należy określić nagłówek hello `Metadata: true` tooensure hello żądania nie został przypadkowo przekierowany.</span><span class="sxs-lookup"><span data-stu-id="05f8c-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="05f8c-136">Włączanie zaplanowanego zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="05f8c-137">Witaj po raz pierwszy wprowadzone żądania zaplanowanego zdarzenia Azure niejawnie włącza hello funkcji na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05f8c-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="05f8c-138">W związku z tym spodziewać opóźnione odpowiedzi w pierwszym wywołaniu się tootwo minut.</span><span class="sxs-lookup"><span data-stu-id="05f8c-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="05f8c-139">Użytkownik zainicjował konserwacji</span><span class="sxs-lookup"><span data-stu-id="05f8c-139">User Initiated Maintenance</span></span>
<span data-ttu-id="05f8c-140">Użytkownik zainicjował konserwacji maszyny wirtualnej za pomocą hello portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell spowoduje zaplanowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="05f8c-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="05f8c-141">Umożliwia tootest hello konserwacji przygotowania logikę w aplikacji i pozwala tooprepare Twojej aplikacji do obsługi inicjowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="05f8c-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="05f8c-142">Ponowne uruchomienie maszyny wirtualnej zostanie zaplanowane zdarzenie z typem `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="05f8c-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="05f8c-143">Ponownego wdrażania maszyny wirtualnej zostanie zaplanowane zdarzenie z typem `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="05f8c-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="05f8c-144">Obecnie maksymalnie 10 operacji konserwacji zainicjowanej przez użytkownika można jednocześnie zaplanować.</span><span class="sxs-lookup"><span data-stu-id="05f8c-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="05f8c-145">Ten limit zostanie złagodzony przed zaplanowane zdarzenia ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="05f8c-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="05f8c-146">Wynikiem zaplanowane zdarzenia konserwacji zainicjowanej przez użytkownika nie jest obecnie można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="05f8c-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="05f8c-147">Konfigurowalne jest planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="05f8c-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="05f8c-148">Przy użyciu interfejsu API hello</span><span class="sxs-lookup"><span data-stu-id="05f8c-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="05f8c-149">Zapytania do zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-149">Query for events</span></span>
<span data-ttu-id="05f8c-150">Po prostu, wprowadzając następujące hello wywołania mogą wykonywać kwerendę o zaplanowane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="05f8c-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="05f8c-151">Odpowiedź zawiera tablicę zaplanowanego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="05f8c-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="05f8c-152">Pusta tablica oznacza, że obecnie nie istnieją żadne zdarzenia według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="05f8c-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="05f8c-153">W przypadku hello w przypadku zaplanowanego zdarzenia odpowiedź hello zawiera tablicę zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="05f8c-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="05f8c-154">Właściwości zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-154">Event Properties</span></span>
|<span data-ttu-id="05f8c-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="05f8c-155">Property</span></span>  |  <span data-ttu-id="05f8c-156">Opis</span><span class="sxs-lookup"><span data-stu-id="05f8c-156">Description</span></span> |
| - | - |
| <span data-ttu-id="05f8c-157">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-157">EventId</span></span> | <span data-ttu-id="05f8c-158">Globalnie unikatowy identyfikator dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="05f8c-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="05f8c-159">Przykład:</span><span class="sxs-lookup"><span data-stu-id="05f8c-159">Example:</span></span> <br><ul><li><span data-ttu-id="05f8c-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="05f8c-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="05f8c-161">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-161">EventType</span></span> | <span data-ttu-id="05f8c-162">Wpływ powoduje, że to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="05f8c-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="05f8c-163">Wartości:</span><span class="sxs-lookup"><span data-stu-id="05f8c-163">Values:</span></span> <br><ul><li> <span data-ttu-id="05f8c-164">`Freeze`: hello maszyny wirtualnej jest zaplanowane toopause kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="05f8c-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="05f8c-165">Hello Procesora zostanie wstrzymana, ale nie ma żadnego wpływu na pamięć, otwartych plików lub połączeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="05f8c-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="05f8c-166">`Reboot`: hello zaplanowano ponownego uruchomienia maszyny wirtualnej (z systemem innym niż trwałej pamięci jest utracone).</span><span class="sxs-lookup"><span data-stu-id="05f8c-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="05f8c-167">`Redeploy`: hello maszyny wirtualnej jest zaplanowane toomove tooanother węzła (tymczasowych dyski zostaną utracone).</span><span class="sxs-lookup"><span data-stu-id="05f8c-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="05f8c-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="05f8c-168">ResourceType</span></span> | <span data-ttu-id="05f8c-169">Typ zasobu, który ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="05f8c-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="05f8c-170">Wartości:</span><span class="sxs-lookup"><span data-stu-id="05f8c-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="05f8c-171">Zasoby</span><span class="sxs-lookup"><span data-stu-id="05f8c-171">Resources</span></span>| <span data-ttu-id="05f8c-172">Lista zasobów, które ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="05f8c-172">List of resources this event impacts.</span></span> <span data-ttu-id="05f8c-173">Gwarantuje toocontain maszyny z co najwyżej jeden [domeny aktualizacji](windows/manage-availability.md), ale nie może zawierać wszystkie maszyny w hello UD.</span><span class="sxs-lookup"><span data-stu-id="05f8c-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="05f8c-174">Przykład:</span><span class="sxs-lookup"><span data-stu-id="05f8c-174">Example:</span></span> <br><ul><li> <span data-ttu-id="05f8c-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="05f8c-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="05f8c-176">Stan zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-176">Event Status</span></span> | <span data-ttu-id="05f8c-177">Stan tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="05f8c-177">Status of this event.</span></span> <br><br> <span data-ttu-id="05f8c-178">Wartości:</span><span class="sxs-lookup"><span data-stu-id="05f8c-178">Values:</span></span> <ul><li><span data-ttu-id="05f8c-179">`Scheduled`: To zdarzenie jest zaplanowane toostart po hello czas określony w hello `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="05f8c-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="05f8c-180">`Started`: To zdarzenie zostało rozpoczęte.</span><span class="sxs-lookup"><span data-stu-id="05f8c-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="05f8c-181">Nie `Completed` lub podobne stan kiedykolwiek jest dostarczana, zdarzenia hello już zostaną zwrócone, po zakończeniu hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="05f8c-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="05f8c-182">Nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="05f8c-182">NotBefore</span></span>| <span data-ttu-id="05f8c-183">Czas, po którym to zdarzenie może zostać uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="05f8c-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="05f8c-184">Przykład:</span><span class="sxs-lookup"><span data-stu-id="05f8c-184">Example:</span></span> <br><ul><li> <span data-ttu-id="05f8c-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="05f8c-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="05f8c-186">Planowanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="05f8c-186">Event Scheduling</span></span>
<span data-ttu-id="05f8c-187">Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości hello na podstawie zdarzeń typu.</span><span class="sxs-lookup"><span data-stu-id="05f8c-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="05f8c-188">Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="05f8c-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="05f8c-189">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="05f8c-189">EventType</span></span>  | <span data-ttu-id="05f8c-190">Minimalna powiadomień</span><span class="sxs-lookup"><span data-stu-id="05f8c-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="05f8c-191">Blokowanie</span><span class="sxs-lookup"><span data-stu-id="05f8c-191">Freeze</span></span>| <span data-ttu-id="05f8c-192">15 minut</span><span class="sxs-lookup"><span data-stu-id="05f8c-192">15 minutes</span></span> |
| <span data-ttu-id="05f8c-193">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="05f8c-193">Reboot</span></span> | <span data-ttu-id="05f8c-194">15 minut</span><span class="sxs-lookup"><span data-stu-id="05f8c-194">15 minutes</span></span> |
| <span data-ttu-id="05f8c-195">Ponowne wdrożenie</span><span class="sxs-lookup"><span data-stu-id="05f8c-195">Redeploy</span></span> | <span data-ttu-id="05f8c-196">10 minut</span><span class="sxs-lookup"><span data-stu-id="05f8c-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="05f8c-197">Uruchamianie zdarzenia (przyspieszenia)</span><span class="sxs-lookup"><span data-stu-id="05f8c-197">Starting an event (expedite)</span></span>

<span data-ttu-id="05f8c-198">Po rozpoznane nadchodzących zdarzenia i ukończyć logiki dla łagodne zamykanie należy zatwierdzić hello zaległych zdarzeń dokonując `POST` wywołania toohello metadanych usługi z hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="05f8c-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="05f8c-199">Wskazuje tooAzure skrócić powiadomień minimalna hello czasu (jeśli jest to możliwe).</span><span class="sxs-lookup"><span data-stu-id="05f8c-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="05f8c-200">Potwierdzeniem zdarzeniem umożliwi hello tooproceed zdarzeń dla wszystkich `Resources` w zdarzeniu hello hello nie tylko maszynę wirtualną, która potwierdza hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="05f8c-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="05f8c-201">W związku z tym można tooelect wiodące toocoordinate hello potwierdzenia, które mogą być prosta jako maszynę pierwszej hello na powitania `Resources` pola.</span><span class="sxs-lookup"><span data-stu-id="05f8c-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="05f8c-202">Przykłady</span><span class="sxs-lookup"><span data-stu-id="05f8c-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="05f8c-203">Przykładowe programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="05f8c-203">PowerShell Sample</span></span> 

<span data-ttu-id="05f8c-204">Witaj następujące przykładowe zapytania hello metadane usługi dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="05f8c-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


### <a name="c-sample"></a><span data-ttu-id="05f8c-205">C\# próbki</span><span class="sxs-lookup"><span data-stu-id="05f8c-205">C\# Sample</span></span> 

<span data-ttu-id="05f8c-206">Witaj poniższego przykładu jest proste klienta, który komunikuje się z usługą metadanych hello.</span><span class="sxs-lookup"><span data-stu-id="05f8c-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="05f8c-207">Zaplanowane zdarzenia mogą być przedstawiane za pomocą hello następujące struktury danych:</span><span class="sxs-lookup"><span data-stu-id="05f8c-207">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="05f8c-208">Witaj następujące przykładowe zapytania hello metadane usługi dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="05f8c-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

### <a name="python-sample"></a><span data-ttu-id="05f8c-209">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="05f8c-209">Python Sample</span></span> 

<span data-ttu-id="05f8c-210">Witaj następujące przykładowe zapytania hello metadane usługi dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="05f8c-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="05f8c-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05f8c-211">Next Steps</span></span> 

- <span data-ttu-id="05f8c-212">Dowiedz się więcej o hello interfejsami API dostępnymi w hello [wystąpienia usługi metadanych](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05f8c-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="05f8c-213">Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Windows Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="05f8c-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="05f8c-214">Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="05f8c-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
