---
title: "Rejestrowanie tooflow aaaIntroduction dla grup zabezpieczeń sieci z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono sposób przepływu NSG toouse rejestrowania funkcji Azure obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="231c9-103">Rejestrowanie tooflow wprowadzenie dla grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="231c9-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="231c9-104">Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który pozwala tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="231c9-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="231c9-105">Te dzienniki przepływu są zapisywane w formacie json i Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart stosuje, 5-elementowej informacji o przepływie hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), a jeśli hello ruchu jest dozwolone, lub Odmowa dostępu.</span><span class="sxs-lookup"><span data-stu-id="231c9-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![Przegląd dzienników przepływu][1]

<span data-ttu-id="231c9-107">Podczas przepływu rejestruje grup zabezpieczeń sieci docelowej, nie są wyświetlane hello takie same jak hello inne dzienniki.</span><span class="sxs-lookup"><span data-stu-id="231c9-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="231c9-108">Przepływ dzienniki są przechowywane tylko w ramach konta magazynu i następująca ścieżka rejestrowania hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="231c9-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="231c9-109">Witaj takie same zasady przechowywania, jak pokazano na inne dzienniki zastosować tooflow dzienników.</span><span class="sxs-lookup"><span data-stu-id="231c9-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="231c9-110">Dzienniki ma zasady przechowywania, które można ustawić dni too365 1 dzień.</span><span class="sxs-lookup"><span data-stu-id="231c9-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="231c9-111">Jeśli zasady przechowywania nie jest ustawiona, dzienniki hello są obsługiwane w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="231c9-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="231c9-112">Plik dziennika</span><span class="sxs-lookup"><span data-stu-id="231c9-112">Log file</span></span>

<span data-ttu-id="231c9-113">Dzienniki przepływu ma wiele właściwości.</span><span class="sxs-lookup"><span data-stu-id="231c9-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="231c9-114">Witaj poniżej znajduje się lista właściwości hello, które są zwracane w dzienniku przepływu NSG hello:</span><span class="sxs-lookup"><span data-stu-id="231c9-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="231c9-115">**czas** — jest to czas, gdy hello zdarzenia</span><span class="sxs-lookup"><span data-stu-id="231c9-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="231c9-116">**systemId** — identyfikator zasobu grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="231c9-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="231c9-117">**Kategoria** -hello kategorii zdarzenia hello to jest zawsze być NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="231c9-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="231c9-118">**RESOURCEID** — Witaj identyfikator hello NSG zasobu</span><span class="sxs-lookup"><span data-stu-id="231c9-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="231c9-119">**operationName** -zawsze NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="231c9-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="231c9-120">**właściwości** -zbiór właściwości hello przepływu</span><span class="sxs-lookup"><span data-stu-id="231c9-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="231c9-121">**Wersja** — numer wersji schematu programu hello przepływu dziennika zdarzeń</span><span class="sxs-lookup"><span data-stu-id="231c9-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="231c9-122">**przepływy** -kolekcji przepływów.</span><span class="sxs-lookup"><span data-stu-id="231c9-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="231c9-123">Ta właściwość ma wiele pozycji dla różnych zasad</span><span class="sxs-lookup"><span data-stu-id="231c9-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="231c9-124">**Reguła** -reguły, które hello są wyświetlane przepływów</span><span class="sxs-lookup"><span data-stu-id="231c9-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="231c9-125">**przepływy** -kolekcji przepływów</span><span class="sxs-lookup"><span data-stu-id="231c9-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="231c9-126">**Mac** — Witaj hello karty Sieciowej dla maszyny Wirtualnej, w których zebrano przepływu hello hello adres MAC</span><span class="sxs-lookup"><span data-stu-id="231c9-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="231c9-127">**flowTuples** — ciąg, który zawiera wiele właściwości krotki przepływu hello w formacie rozdzielone przecinkami</span><span class="sxs-lookup"><span data-stu-id="231c9-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="231c9-128">**Sygnatury czasu** — ta wartość jest sygnaturę czasową hello hello przepływu problemu w formacie epoka systemu UNIX.</span><span class="sxs-lookup"><span data-stu-id="231c9-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="231c9-129">**Źródłowy adres IP** — Witaj źródłowy adres IP</span><span class="sxs-lookup"><span data-stu-id="231c9-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="231c9-130">**Docelowy IP** — Witaj docelowy adres IP</span><span class="sxs-lookup"><span data-stu-id="231c9-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="231c9-131">**Port źródłowy** — Witaj port źródłowy</span><span class="sxs-lookup"><span data-stu-id="231c9-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="231c9-132">**Port docelowy** — Witaj Port docelowy</span><span class="sxs-lookup"><span data-stu-id="231c9-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="231c9-133">**Protokół** — Witaj protokołu hello przepływu.</span><span class="sxs-lookup"><span data-stu-id="231c9-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="231c9-134">Prawidłowe wartości to **T** dla protokołu TCP i **U** UDP</span><span class="sxs-lookup"><span data-stu-id="231c9-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="231c9-135">**Przepływu ruchu** — Witaj kierunek przepływu ruchu hello.</span><span class="sxs-lookup"><span data-stu-id="231c9-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="231c9-136">Prawidłowe wartości to **I** dla ruchu przychodzącego i **O** dla ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="231c9-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="231c9-137">**Ruch** — czy też odmówiono ruchu.</span><span class="sxs-lookup"><span data-stu-id="231c9-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="231c9-138">Prawidłowe wartości to **A** dla dozwolone i **D** dla odmowa.</span><span class="sxs-lookup"><span data-stu-id="231c9-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="231c9-139">następujące Hello jest przykładem dziennika przepływu.</span><span class="sxs-lookup"><span data-stu-id="231c9-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="231c9-140">Jak widać, że nie ma wiele rekordów, które należy wykonać opisane w powyższej sekcji hello listę właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="231c9-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="231c9-141">Wartości właściwości flowTuples hello są listę rozdzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="231c9-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="231c9-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="231c9-142">Next steps</span></span>

<span data-ttu-id="231c9-143">Dowiedz się, jak tooenable przepływu logowania po przejściu na stronę [przepływ włączenie rejestrowania](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="231c9-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="231c9-144">Więcej informacji na temat rejestrowania NSG, odwiedzając [dziennika analizy grup zabezpieczeń sieci (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="231c9-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="231c9-145">Dowiedzieć się, jeśli ruch jest dozwolony lub zabroniony na maszynie Wirtualnej, odwiedzając [Sprawdź, sprawdź, czy ruch z przepływem IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="231c9-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

