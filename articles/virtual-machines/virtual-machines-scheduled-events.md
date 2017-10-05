---
title: "Zaplanowane zdarzenia za pomocą usługi Azure metadanych | Dokumentacja firmy Microsoft"
description: "Reagowanie na zdarzenia Impactful na maszynie wirtualnej zanim wystąpią."
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
ms.openlocfilehash: 793803bfc12059a68ec881da9de37116f7a0eb8c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="e59db-103">Usługa Azure metadanych - zaplanowanego zdarzenia (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="e59db-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="e59db-104">Podglądy są udostępniane użytkownikowi, pod warunkiem że wyrażasz zgodę na warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="e59db-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="e59db-105">Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="e59db-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="e59db-106">Zaplanowane zdarzenia jest jednym z subservices w usłudze Azure metadanych.</span><span class="sxs-lookup"><span data-stu-id="e59db-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="e59db-107">Jest odpowiedzialny za udostępniając informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="e59db-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="e59db-108">Jest ona dostępna dla wszystkich typów maszyny wirtualnej platformy Azure, w tym PaaS i IaaS.</span><span class="sxs-lookup"><span data-stu-id="e59db-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="e59db-109">Zaplanowane zdarzenia daje czasu maszyny wirtualnej do wykonywania zadań zapobiegawcze, aby zminimalizować wpływ zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e59db-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="e59db-110">Wprowadzenie — dlaczego zaplanowane zdarzenia?</span><span class="sxs-lookup"><span data-stu-id="e59db-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="e59db-111">Bez zaplanowane zdarzenia należy wykonać kroki, aby ograniczyć wpływ intiated platformy konserwacji lub akcje inicjowane przez użytkownika w usłudze.</span><span class="sxs-lookup"><span data-stu-id="e59db-111">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="e59db-112">Mająca wiele wystąpień obciążeń, które są używane do zarządzania stanem technik replikacji, mogą być narażone na awarie wykonywane w wielu wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="e59db-112">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="e59db-113">Takie jak awarie może spowodować kosztowne zadania (na przykład odbudowywania indeksów) lub nawet utraty repliki.</span><span class="sxs-lookup"><span data-stu-id="e59db-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="e59db-114">W wielu innych przypadkach ogólnych dostępności usługi mogą być ulepszane wykonując sekwencji łagodne zamykanie, takie jak pula modułu równoważenia obciążenia Kończenie (lub anulowanie) locie transakcji, ponowne przypisywanie zadań do innych maszyn wirtualnych w klastrze (ręcznego przełączania trybu failover) lub usuwanie maszyny wirtualnej z sieci.</span><span class="sxs-lookup"><span data-stu-id="e59db-114">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="e59db-115">Istnieją przypadki, w którym powiadamianie o tym administratora o nadchodzących zdarzenia lub rejestrowanie takie zdarzenia pomocy poprawy użytkowanie aplikacji hostowanych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e59db-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="e59db-116">Usługa Azure metadanych udostępnia zaplanowane zdarzenia w następujących przypadkach użycia:</span><span class="sxs-lookup"><span data-stu-id="e59db-116">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="e59db-117">Platforma zainicjował konserwacji (na przykład wdrożenie systemu operacyjnego hosta)</span><span class="sxs-lookup"><span data-stu-id="e59db-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="e59db-118">Wywołania zainicjowane przez użytkownika (na przykład użytkownik zostanie ponownie uruchomiony lub wdraża ponownie maszyny Wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="e59db-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---the-basics"></a><span data-ttu-id="e59db-119">Zaplanowane zdarzenia — podstawy</span><span class="sxs-lookup"><span data-stu-id="e59db-119">Scheduled Events - The Basics</span></span>  

<span data-ttu-id="e59db-120">Usługa Azure metadanych przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST jest dostępny z poziomu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e59db-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="e59db-121">Informacje są dostępne za pośrednictwem IP bez obsługi routingu, dzięki czemu nie jest uwidaczniana poza maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e59db-121">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="e59db-122">Zakres</span><span class="sxs-lookup"><span data-stu-id="e59db-122">Scope</span></span>
<span data-ttu-id="e59db-123">Zaplanowane zdarzenia są udostępniane dla wszystkich maszyn wirtualnych w usłudze w chmurze lub dla wszystkich maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="e59db-123">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="e59db-124">W związku z tym należy sprawdzić `Resources` w zdarzenia w celu określenia, na które będzie to mieć wpływ na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e59db-124">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="e59db-125">Odnajdywanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e59db-125">Discovering the Endpoint</span></span>
<span data-ttu-id="e59db-126">W przypadku, gdy utworzono maszynę wirtualną w sieć wirtualną (VNet), usługa metadanych jest dostępne ze statycznego adresu IP bez obsługi routingu, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="e59db-126">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="e59db-127">Jeśli maszyna wirtualna nie została utworzona w ramach sieci wirtualnej, a domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest potrzebny do odnajdywania punktu końcowego do użycia.</span><span class="sxs-lookup"><span data-stu-id="e59db-127">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="e59db-128">Odwołuje się do poniższego przykładu, aby dowiedzieć się, jak [odnajdywanie punktu końcowego hosta](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="e59db-128">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="e59db-129">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="e59db-129">Versioning</span></span> 
<span data-ttu-id="e59db-130">Wystąpienie usługi metadanych jest kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="e59db-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="e59db-131">Wersje są obowiązkowe i bieżąca wersja to `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="e59db-131">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="e59db-132">Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="e59db-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="e59db-133">Ten format jest już obsługiwane i zostaną wycofane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="e59db-133">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="e59db-134">Korzystanie z nagłówków</span><span class="sxs-lookup"><span data-stu-id="e59db-134">Using Headers</span></span>
<span data-ttu-id="e59db-135">Kwerenda usługi metadanych, należy określić nagłówek `Metadata: true` aby upewnić się, żądanie nie zostało przekierowane przypadkowo.</span><span class="sxs-lookup"><span data-stu-id="e59db-135">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="e59db-136">Włączanie zaplanowanego zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="e59db-137">Utwórz żądanie zaplanowanego zdarzenia po raz pierwszy Azure niejawnie włączy tę funkcję na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e59db-137">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="e59db-138">W związku z tym spodziewać opóźnione odpowiedzi w Twoje pierwsze wywołanie do dwóch minut.</span><span class="sxs-lookup"><span data-stu-id="e59db-138">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="e59db-139">Użytkownik zainicjował konserwacji</span><span class="sxs-lookup"><span data-stu-id="e59db-139">User Initiated Maintenance</span></span>
<span data-ttu-id="e59db-140">Użytkownik zainicjował konserwacji maszyny wirtualnej za pośrednictwem portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell spowoduje zaplanowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-140">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="e59db-141">To umożliwia przetestowanie logiki przygotowania konserwacji w aplikacji oraz umożliwia aplikacji w taki sposób przygotować się do obsługi inicjowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e59db-141">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="e59db-142">Ponowne uruchomienie maszyny wirtualnej zostanie zaplanowane zdarzenie z typem `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="e59db-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="e59db-143">Ponownego wdrażania maszyny wirtualnej zostanie zaplanowane zdarzenie z typem `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="e59db-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="e59db-144">Obecnie maksymalnie 10 operacji konserwacji zainicjowanej przez użytkownika można jednocześnie zaplanować.</span><span class="sxs-lookup"><span data-stu-id="e59db-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="e59db-145">Ten limit zostanie złagodzony przed zaplanowane zdarzenia ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e59db-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="e59db-146">Wynikiem zaplanowane zdarzenia konserwacji zainicjowanej przez użytkownika nie jest obecnie można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="e59db-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="e59db-147">Konfigurowalne jest planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="e59db-147">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="e59db-148">Korzystanie z interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e59db-148">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="e59db-149">Zapytania do zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-149">Query for events</span></span>
<span data-ttu-id="e59db-150">Mogą wykonywać kwerendę o zaplanowane zdarzenia po prostu, wprowadzając następujące wywołanie:</span><span class="sxs-lookup"><span data-stu-id="e59db-150">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="e59db-151">Odpowiedź zawiera tablicę zaplanowanego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="e59db-152">Pusta tablica oznacza, że obecnie nie istnieją żadne zdarzenia według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="e59db-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="e59db-153">W przypadku w przypadku zaplanowanego zdarzenia odpowiedzi zawiera tablicę zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="e59db-153">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="e59db-154">Właściwości zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-154">Event Properties</span></span>
|<span data-ttu-id="e59db-155">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e59db-155">Property</span></span>  |  <span data-ttu-id="e59db-156">Opis</span><span class="sxs-lookup"><span data-stu-id="e59db-156">Description</span></span> |
| - | - |
| <span data-ttu-id="e59db-157">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-157">EventId</span></span> | <span data-ttu-id="e59db-158">Globalnie unikatowy identyfikator dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="e59db-159">Przykład:</span><span class="sxs-lookup"><span data-stu-id="e59db-159">Example:</span></span> <br><ul><li><span data-ttu-id="e59db-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="e59db-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="e59db-161">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-161">EventType</span></span> | <span data-ttu-id="e59db-162">Wpływ powoduje, że to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="e59db-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="e59db-163">Wartości:</span><span class="sxs-lookup"><span data-stu-id="e59db-163">Values:</span></span> <br><ul><li> <span data-ttu-id="e59db-164">`Freeze`: Planowane maszyny wirtualnej jest wstrzymywać w kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="e59db-164">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="e59db-165">Procesor CPU zostanie wstrzymana, ale nie ma żadnego wpływu na pamięć, otwartych plików lub połączeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="e59db-165">The CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="e59db-166">`Reboot`: Ponowne uruchomienie zaplanowano maszyny wirtualnej (z systemem innym niż trwałej pamięci jest utracone).</span><span class="sxs-lookup"><span data-stu-id="e59db-166">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="e59db-167">`Redeploy`: Zaplanowano maszynę wirtualną można przenieść do innego węzła (tymczasowych dyski zostaną utracone).</span><span class="sxs-lookup"><span data-stu-id="e59db-167">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="e59db-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="e59db-168">ResourceType</span></span> | <span data-ttu-id="e59db-169">Typ zasobu, który ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="e59db-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="e59db-170">Wartości:</span><span class="sxs-lookup"><span data-stu-id="e59db-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="e59db-171">Zasoby</span><span class="sxs-lookup"><span data-stu-id="e59db-171">Resources</span></span>| <span data-ttu-id="e59db-172">Lista zasobów, które ma wpływ na to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="e59db-172">List of resources this event impacts.</span></span> <span data-ttu-id="e59db-173">Gwarantuje zawiera maszyny z co najwyżej jeden [domeny aktualizacji](windows/manage-availability.md), ale nie może zawierać wszystkie maszyny w UD.</span><span class="sxs-lookup"><span data-stu-id="e59db-173">This is guaranteed to contain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="e59db-174">Przykład:</span><span class="sxs-lookup"><span data-stu-id="e59db-174">Example:</span></span> <br><ul><li> <span data-ttu-id="e59db-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="e59db-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="e59db-176">Stan zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-176">Event Status</span></span> | <span data-ttu-id="e59db-177">Stan tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-177">Status of this event.</span></span> <br><br> <span data-ttu-id="e59db-178">Wartości:</span><span class="sxs-lookup"><span data-stu-id="e59db-178">Values:</span></span> <ul><li><span data-ttu-id="e59db-179">`Scheduled`: To zdarzenie jest zaplanowane do uruchomienia po upływie czasu określonego w `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="e59db-179">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="e59db-180">`Started`: To zdarzenie zostało rozpoczęte.</span><span class="sxs-lookup"><span data-stu-id="e59db-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="e59db-181">Nie `Completed` lub podobne stan kiedykolwiek jest dostarczana, zdarzenie nie zostanie zwrócony po zakończeniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-181">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="e59db-182">Nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="e59db-182">NotBefore</span></span>| <span data-ttu-id="e59db-183">Czas, po którym to zdarzenie może zostać uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="e59db-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="e59db-184">Przykład:</span><span class="sxs-lookup"><span data-stu-id="e59db-184">Example:</span></span> <br><ul><li> <span data-ttu-id="e59db-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="e59db-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="e59db-186">Planowanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="e59db-186">Event Scheduling</span></span>
<span data-ttu-id="e59db-187">Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości oparty na typie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-187">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="e59db-188">Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości.</span><span class="sxs-lookup"><span data-stu-id="e59db-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="e59db-189">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e59db-189">EventType</span></span>  | <span data-ttu-id="e59db-190">Minimalna powiadomień</span><span class="sxs-lookup"><span data-stu-id="e59db-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="e59db-191">Blokowanie</span><span class="sxs-lookup"><span data-stu-id="e59db-191">Freeze</span></span>| <span data-ttu-id="e59db-192">15 minut</span><span class="sxs-lookup"><span data-stu-id="e59db-192">15 minutes</span></span> |
| <span data-ttu-id="e59db-193">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="e59db-193">Reboot</span></span> | <span data-ttu-id="e59db-194">15 minut</span><span class="sxs-lookup"><span data-stu-id="e59db-194">15 minutes</span></span> |
| <span data-ttu-id="e59db-195">Ponowne wdrożenie</span><span class="sxs-lookup"><span data-stu-id="e59db-195">Redeploy</span></span> | <span data-ttu-id="e59db-196">10 minut</span><span class="sxs-lookup"><span data-stu-id="e59db-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="e59db-197">Uruchamianie zdarzenia (przyspieszenia)</span><span class="sxs-lookup"><span data-stu-id="e59db-197">Starting an event (expedite)</span></span>

<span data-ttu-id="e59db-198">Po rozpoznane nadchodzących zdarzenia i ukończyć logiki dla łagodne zamykanie należy zatwierdzić zaległych zdarzeń dokonując `POST` wywołanie usługi metadanych z `EventId`.</span><span class="sxs-lookup"><span data-stu-id="e59db-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="e59db-199">To wskazuje na platformie Azure skrócić minimalna powiadomień czasu (jeśli jest to możliwe).</span><span class="sxs-lookup"><span data-stu-id="e59db-199">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="e59db-200">Potwierdzeniem zdarzeniem umożliwi zdarzeń w przypadku wszystkich `Resources` w przypadku, nie tylko w maszynie wirtualnej, który potwierdza zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e59db-200">Acknowledging a event will allow the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="e59db-201">W związku z tym można wybrać opcję wybiera wiodące do koordynowania potwierdzenia, które mogą być prosta jako maszynę pierwszej w `Resources` pola.</span><span class="sxs-lookup"><span data-stu-id="e59db-201">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="e59db-202">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e59db-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="e59db-203">Przykładowe programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e59db-203">PowerShell Sample</span></span> 

<span data-ttu-id="e59db-204">Poniższy przykład korzysta z usługi metadanych dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="e59db-204">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
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


### <a name="c-sample"></a><span data-ttu-id="e59db-205">C\# próbki</span><span class="sxs-lookup"><span data-stu-id="e59db-205">C\# Sample</span></span> 

<span data-ttu-id="e59db-206">Poniższy przykład jest proste klienta, który komunikuje się z usługą metadanych.</span><span class="sxs-lookup"><span data-stu-id="e59db-206">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="e59db-207">Zaplanowane zdarzenia mogą być przedstawiane za pomocą następujących struktur danych:</span><span class="sxs-lookup"><span data-stu-id="e59db-207">Scheduled Events can be represented using the following data structures:</span></span>

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

<span data-ttu-id="e59db-208">Poniższy przykład korzysta z usługi metadanych dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="e59db-208">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter to approve executing events\n");
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

            Console.WriteLine("Complete. Press enter to repeat\n\n");
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

### <a name="python-sample"></a><span data-ttu-id="e59db-209">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="e59db-209">Python Sample</span></span> 

<span data-ttu-id="e59db-210">Poniższy przykład korzysta z usługi metadanych dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.</span><span class="sxs-lookup"><span data-stu-id="e59db-210">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e59db-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e59db-211">Next Steps</span></span> 

- <span data-ttu-id="e59db-212">Dowiedz się więcej o interfejsami API dostępnymi w [wystąpienia usługi metadanych](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e59db-212">Read more about the APIs available in the [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="e59db-213">Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Windows Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="e59db-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="e59db-214">Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="e59db-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
