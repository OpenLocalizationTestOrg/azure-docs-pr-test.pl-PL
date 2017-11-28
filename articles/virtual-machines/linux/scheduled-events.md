---
title: Zaplanowane zdarzenia dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Zaplanowane zdarzenia przy użyciu usługi Azure metadanych dla na maszynach wirtualnych systemu Linux."
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
ms.openlocfilehash: 75e509a7e39f5b268ce550d0c4dea2261d4fe56f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="fbf3a-103">Usługa Azure metadanych: Zaplanowanego zdarzenia (wersja zapoznawcza) dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fbf3a-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="fbf3a-104">Podglądy są udostępniane użytkownikowi, pod warunkiem że wyrażasz zgodę na warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="fbf3a-105">Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="fbf3a-106">Zaplanowane zdarzenia jest jednym z subservices w usłudze Azure metadanych.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="fbf3a-107">Jest odpowiedzialny za udostępniając informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="fbf3a-108">Jest ona dostępna dla wszystkich typów maszyny wirtualnej platformy Azure, w tym PaaS i IaaS.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="fbf3a-109">Zaplanowane zdarzenia daje czasu maszyny wirtualnej do wykonywania zadań zapobiegawcze, aby zminimalizować wpływ zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="fbf3a-110">Zaplanowane zdarzenia jest dostępna dla systemów Windows i maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="fbf3a-111">Informacji o zaplanowane zdarzeń w systemie Windows, temacie [zaplanowane zdarzenia dla maszyn wirtualnych systemu Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="fbf3a-112">Dlaczego zaplanowane zdarzenia?</span><span class="sxs-lookup"><span data-stu-id="fbf3a-112">Why Scheduled Events?</span></span>

<span data-ttu-id="fbf3a-113">Bez zaplanowane zdarzenia należy wykonać kroki, aby ograniczyć wpływ intiated platformy konserwacji lub akcje inicjowane przez użytkownika w usłudze.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="fbf3a-114">Mająca wiele wystąpień obciążeń, które są używane do zarządzania stanem technik replikacji, mogą być narażone na awarie wykonywane w wielu wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="fbf3a-115">Takie jak awarie może spowodować kosztowne zadania (na przykład odbudowywania indeksów) lub nawet utraty repliki.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="fbf3a-116">W wielu innych przypadkach ogólnych dostępności usługi mogą być ulepszane wykonując sekwencji łagodne zamykanie, takie jak pula modułu równoważenia obciążenia Kończenie (lub anulowanie) locie transakcji, ponowne przypisywanie zadań do innych maszyn wirtualnych w klastrze (ręcznego przełączania trybu failover) lub usuwanie maszyny wirtualnej z sieci.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="fbf3a-117">Istnieją przypadki, w którym powiadamianie o tym administratora o nadchodzących zdarzenia lub rejestrowanie takie zdarzenia pomocy poprawy użytkowanie aplikacji hostowanych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="fbf3a-118">Usługa Azure metadanych udostępnia zaplanowane zdarzenia w następujących przypadkach użycia:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="fbf3a-119">Platforma zainicjował konserwacji (na przykład wdrożenie systemu operacyjnego hosta)</span><span class="sxs-lookup"><span data-stu-id="fbf3a-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="fbf3a-120">Wywołania zainicjowane przez użytkownika (na przykład użytkownik zostanie ponownie uruchomiony lub wdraża ponownie maszyny Wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="fbf3a-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="fbf3a-121">Podstawy</span><span class="sxs-lookup"><span data-stu-id="fbf3a-121">The basics</span></span>  

<span data-ttu-id="fbf3a-122">Usługa Azure metadanych przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST jest dostępny z poziomu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="fbf3a-123">Informacje są dostępne za pośrednictwem IP bez obsługi routingu, dzięki czemu nie jest uwidaczniana poza maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="fbf3a-124">Zakres</span><span class="sxs-lookup"><span data-stu-id="fbf3a-124">Scope</span></span>
<span data-ttu-id="fbf3a-125">Zaplanowane zdarzenia są udostępniane dla wszystkich maszyn wirtualnych w usłudze w chmurze lub dla wszystkich maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="fbf3a-126">W związku z tym należy sprawdzić `Resources` w zdarzenia w celu określenia, na które będzie to mieć wpływ na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="fbf3a-127">Odnajdywanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="fbf3a-127">Discovering the endpoint</span></span>
<span data-ttu-id="fbf3a-128">W przypadku, gdy utworzono maszynę wirtualną w sieć wirtualną (VNet), usługa metadanych jest dostępne ze statycznego adresu IP bez obsługi routingu, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="fbf3a-129">Jeśli maszyna wirtualna nie została utworzona w ramach sieci wirtualnej, a domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest potrzebny do odnajdywania punktu końcowego do użycia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="fbf3a-130">Odwołuje się do poniższego przykładu, aby dowiedzieć się, jak [odnajdywanie punktu końcowego hosta](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="fbf3a-131">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="fbf3a-131">Versioning</span></span> 
<span data-ttu-id="fbf3a-132">Wystąpienie usługi metadanych jest kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="fbf3a-133">Wersje są obowiązkowe i bieżąca wersja to `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="fbf3a-134">Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="fbf3a-135">Ten format jest już obsługiwane i zostaną wycofane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="fbf3a-136">Korzystanie z nagłówków</span><span class="sxs-lookup"><span data-stu-id="fbf3a-136">Using headers</span></span>
<span data-ttu-id="fbf3a-137">Kwerenda usługi metadanych, należy określić nagłówek `Metadata: true` aby upewnić się, żądanie nie zostało przekierowane przypadkowo.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="fbf3a-138">Włączanie zaplanowanego zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="fbf3a-139">Utwórz żądanie zaplanowanego zdarzenia po raz pierwszy Azure niejawnie włączy tę funkcję na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="fbf3a-140">W związku z tym spodziewać opóźnione odpowiedzi w Twoje pierwsze wywołanie do dwóch minut.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="fbf3a-141">Konserwacja zainicjowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="fbf3a-141">User initiated maintenance</span></span>
<span data-ttu-id="fbf3a-142">Użytkownik zainicjował konserwacji maszyny wirtualnej za pośrednictwem portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell powoduje zaplanowane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="fbf3a-143">To umożliwia przetestowanie logiki przygotowania konserwacji w aplikacji oraz umożliwia aplikacji w taki sposób przygotować się do obsługi inicjowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="fbf3a-144">Ponowne uruchomienie maszyny wirtualnej planuje zdarzenia z typem `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="fbf3a-145">Ponownego wdrażania maszyny wirtualnej planuje zdarzenia z typem `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="fbf3a-146">Obecnie maksymalnie 10 operacji konserwacji zainicjowanej przez użytkownika można jednocześnie zaplanować.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="fbf3a-147">Ten limit zostanie złagodzony przed zaplanowane zdarzenia ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="fbf3a-148">Wynikiem zaplanowane zdarzenia konserwacji zainicjowanej przez użytkownika nie jest obecnie można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="fbf3a-149">Konfigurowalne jest planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="fbf3a-150">Korzystanie z interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fbf3a-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="fbf3a-151">Zapytania do zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-151">Query for events</span></span>
<span data-ttu-id="fbf3a-152">Mogą wykonywać kwerendę o zaplanowane zdarzenia po prostu, wprowadzając następujące wywołanie:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="fbf3a-153">Odpowiedź zawiera tablicę zaplanowanego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="fbf3a-154">Pusta tablica oznacza, że obecnie nie istnieją żadne zdarzenia według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="fbf3a-155">W przypadku w przypadku zaplanowanego zdarzenia odpowiedzi zawiera tablicę zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="fbf3a-156">Właściwości zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-156">Event properties</span></span>
|<span data-ttu-id="fbf3a-157">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fbf3a-157">Property</span></span>  |  <span data-ttu-id="fbf3a-158">Opis</span><span class="sxs-lookup"><span data-stu-id="fbf3a-158">Description</span></span> |
| - | - |
| <span data-ttu-id="fbf3a-159">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-159">EventId</span></span> | <span data-ttu-id="fbf3a-160">Globalnie unikatowy identyfikator dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="fbf3a-161">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-161">Example:</span></span> <br><ul><li><span data-ttu-id="fbf3a-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="fbf3a-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="fbf3a-163">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-163">EventType</span></span> | <span data-ttu-id="fbf3a-164">Wpływ powoduje, że to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="fbf3a-165">Wartości:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-165">Values:</span></span> <br><ul><li> <span data-ttu-id="fbf3a-166">`Freeze`: Planowane maszyny wirtualnej jest wstrzymywać w kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="fbf3a-167">Procesor jest wstrzymana, ale nie ma żadnego wpływu na pamięć, otwartych plików lub połączeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="fbf3a-168">`Reboot`: Ponowne uruchomienie zaplanowano maszyny wirtualnej (z systemem innym niż trwałej pamięci jest utracone).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="fbf3a-169">`Redeploy`: Zaplanowano maszynę wirtualną można przenieść do innego węzła (tymczasowych dyski zostaną utracone).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="fbf3a-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="fbf3a-170">ResourceType</span></span> | <span data-ttu-id="fbf3a-171">Typ zasobu, który ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="fbf3a-172">Wartości:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="fbf3a-173">Zasoby</span><span class="sxs-lookup"><span data-stu-id="fbf3a-173">Resources</span></span>| <span data-ttu-id="fbf3a-174">Lista zasobów, które ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-174">List of resources this event impacts.</span></span> <span data-ttu-id="fbf3a-175">Gwarantuje zawiera maszyny z co najwyżej jeden [domeny aktualizacji](manage-availability.md), ale nie może zawierać wszystkie maszyny w UD.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="fbf3a-176">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-176">Example:</span></span> <br><ul><li> <span data-ttu-id="fbf3a-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="fbf3a-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="fbf3a-178">Stan zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-178">Event Status</span></span> | <span data-ttu-id="fbf3a-179">Stan tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-179">Status of this event.</span></span> <br><br> <span data-ttu-id="fbf3a-180">Wartości:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-180">Values:</span></span> <ul><li><span data-ttu-id="fbf3a-181">`Scheduled`: To zdarzenie jest zaplanowane do uruchomienia po upływie czasu określonego w `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="fbf3a-182">`Started`: To zdarzenie zostało rozpoczęte.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="fbf3a-183">Nie `Completed` lub podobne stan kiedykolwiek jest dostarczana, zdarzenie nie zostanie zwrócony po zakończeniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="fbf3a-184">Nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="fbf3a-184">NotBefore</span></span>| <span data-ttu-id="fbf3a-185">Czas, po którym to zdarzenie może zostać uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="fbf3a-186">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fbf3a-186">Example:</span></span> <br><ul><li> <span data-ttu-id="fbf3a-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="fbf3a-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="fbf3a-188">Planowanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fbf3a-188">Event scheduling</span></span>
<span data-ttu-id="fbf3a-189">Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości oparty na typie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="fbf3a-190">Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="fbf3a-191">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-191">EventType</span></span>  | <span data-ttu-id="fbf3a-192">Minimalna powiadomień</span><span class="sxs-lookup"><span data-stu-id="fbf3a-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="fbf3a-193">Blokowanie</span><span class="sxs-lookup"><span data-stu-id="fbf3a-193">Freeze</span></span>| <span data-ttu-id="fbf3a-194">15 minut</span><span class="sxs-lookup"><span data-stu-id="fbf3a-194">15 minutes</span></span> |
| <span data-ttu-id="fbf3a-195">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="fbf3a-195">Reboot</span></span> | <span data-ttu-id="fbf3a-196">15 minut</span><span class="sxs-lookup"><span data-stu-id="fbf3a-196">15 minutes</span></span> |
| <span data-ttu-id="fbf3a-197">Ponowne wdrożenie</span><span class="sxs-lookup"><span data-stu-id="fbf3a-197">Redeploy</span></span> | <span data-ttu-id="fbf3a-198">10 minut</span><span class="sxs-lookup"><span data-stu-id="fbf3a-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="fbf3a-199">Uruchamianie zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fbf3a-199">Starting an event</span></span> 

<span data-ttu-id="fbf3a-200">Po rozpoznane nadchodzących zdarzenia i ukończyć logiki dla łagodne zamykanie należy zatwierdzić zaległych zdarzeń dokonując `POST` wywołanie usługi metadanych z `EventId`.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="fbf3a-201">To wskazuje na platformie Azure skrócić minimalna powiadomień czasu (jeśli jest to możliwe).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="fbf3a-202">Potwierdzeniem zdarzenia umożliwia zdarzeń w przypadku wszystkich `Resources` w przypadku, nie tylko w maszynie wirtualnej, który potwierdza zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="fbf3a-203">W związku z tym można wybrać opcję wybiera wiodące do koordynowania potwierdzenia, które mogą być prosta jako maszynę pierwszej w `Resources` pola.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="fbf3a-204">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="fbf3a-204">Python sample</span></span> 

<span data-ttu-id="fbf3a-205">Poniższy przykład korzysta z usługi metadanych dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="fbf3a-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fbf3a-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbf3a-206">Next steps</span></span> 

- <span data-ttu-id="fbf3a-207">Dowiedz się więcej o interfejsami API dostępnymi w [metadanych wystąpienia usługi](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-207">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="fbf3a-208">Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="fbf3a-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
