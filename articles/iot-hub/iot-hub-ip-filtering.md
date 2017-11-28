---
title: "filtry połączenia IP Centrum IoT aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak adresy IP toouse, które filtrowania tooblock połączenia z określonego adresu IP dla Centrum Azure IoT tooyour. Możesz zablokować połączenia z poszczególnych lub zakresów adresów IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="b3f0b-104">Używanie filtrów IP</span><span class="sxs-lookup"><span data-stu-id="b3f0b-104">Use IP filters</span></span>

<span data-ttu-id="b3f0b-105">Zabezpieczenia są istotnym elementem każde rozwiązanie IoT oparte na usłudze Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="b3f0b-106">Czasami potrzebny tooexplicitly określić hello adresów IP, z których urządzenia można podłączyć jako część konfiguracji zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="b3f0b-107">Witaj _filtrów IP_ pozwala tooconfigure reguł odrzucenia lub akceptować ruch z określonych adresów IPv4.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="b3f0b-108">Gdy toouse</span><span class="sxs-lookup"><span data-stu-id="b3f0b-108">When toouse</span></span>

<span data-ttu-id="b3f0b-109">Istnieją dwa określonych przypadków użycia, gdy punkty końcowe Centrum IoT hello tooblock przydatne dla określonych adresów IP nie jest:</span><span class="sxs-lookup"><span data-stu-id="b3f0b-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="b3f0b-110">Centrum IoT powinny odbierać dane tylko z określonego zakresu adresów IP i odrzucić wszystkie inne elementy.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="b3f0b-111">Na przykład w przypadku korzystania z Centrum IoT [Azure Express Route] toocreate prywatnych połączeń między centrum IoT i infrastruktury lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="b3f0b-112">Należy tooreject ruchu z adresów IP, które zostały zidentyfikowane jako podejrzane przez administratora Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="b3f0b-113">Sposób stosowania reguły filtrowania</span><span class="sxs-lookup"><span data-stu-id="b3f0b-113">How filter rules are applied</span></span>

<span data-ttu-id="b3f0b-114">reguły filtra IP Hello są stosowane w hello poziomu usług Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="b3f0b-115">W związku z tym reguł filtru IP hello zastosować tooall połączeń z urządzeniami i aplikacjami zaplecza za pomocą obsługiwanych protokołów.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="b3f0b-116">Każda próba połączenia z adresu IP odpowiadającego wydzielenia reguły IP w Centrum IoT odbiera kod stanu 401 nieautoryzowane i opis.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="b3f0b-117">komunikat odpowiedzi Hello nie mogą zawierać hello IP reguły.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="b3f0b-118">Ustawienie domyślne</span><span class="sxs-lookup"><span data-stu-id="b3f0b-118">Default setting</span></span>

<span data-ttu-id="b3f0b-119">Domyślnie program hello **filtrów IP** siatki w portalu hello Centrum IoT jest pusta.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="b3f0b-120">To ustawienie domyślne oznacza, że Centrum akceptuje połączenia dowolnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="b3f0b-121">To ustawienie domyślne to równoważne tooa regułę, która akceptuje zakres adresów IP 0.0.0.0/0 hello.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![Filtr IP domyślnych Centrum IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="b3f0b-123">Dodawanie lub edytowanie reguły filtru adresu IP</span><span class="sxs-lookup"><span data-stu-id="b3f0b-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="b3f0b-124">Po dodaniu reguły filtru adresu IP, zostanie wyświetlony monit o hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="b3f0b-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="b3f0b-125">**Nazwę reguły filtru IP** który musi być unikatowy, bez uwzględniania wielkości liter, alfanumeryczne ciąg się too128 znaków.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="b3f0b-126">Tylko plus znaki alfanumeryczne ASCII 7-bitowego hello `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="b3f0b-127">Wybierz **Odrzuć** lub **zaakceptować** jako hello **akcji** reguły filtru IP hello.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="b3f0b-128">Podaj pojedynczy adres IPv4 lub blok adresów IP w notacji CIDR.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="b3f0b-129">Na przykład w CIDR 192.168.100.0/22 notacji reprezentuje hello 1024 adresy IPv4 z 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Dodaj Centrum IoT tooan reguły filtru adresu IP][img-ip-filter-add-rule]

<span data-ttu-id="b3f0b-131">Po zapisaniu hello reguły, zostanie wyświetlony alert informujący, że aktualizacja hello jest w toku.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Powiadomienie o zapisywaniu regułę filtru IP][img-ip-filter-save-new-rule]

<span data-ttu-id="b3f0b-133">Witaj **Dodaj** opcja jest wyłączona po przejściu hello maksymalnie 10 reguł filtru IP.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="b3f0b-134">Dwukrotne kliknięcie hello wiersza, który zawiera reguły hello można edytować istniejącą regułę.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="b3f0b-135">Odrzucanie IP adresy można zapobiec innymi usługami Azure (np. Azure Stream Analytics, maszynach wirtualnych platformy Azure lub hello Explorer urządzenia w portalu hello) interakcję z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="b3f0b-136">Jeśli używasz usługi Azure Stream Analytics (ASA) tooread komunikaty z Centrum IoT z filtrowania IP włączone, użyj nazwy Centrum zdarzeń zgodnych hello i punktu końcowego Centrum IoT w hello ASA parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="b3f0b-137">Usuń regułę filtru IP</span><span class="sxs-lookup"><span data-stu-id="b3f0b-137">Delete an IP filter rule</span></span>

<span data-ttu-id="b3f0b-138">toodelete reguły filtru adresu IP, wybierz co najmniej jedną regułę hello siatki i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Usuń regułę filtru IP Centrum IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="b3f0b-140">Szacowanie reguły filtru adresu IP</span><span class="sxs-lookup"><span data-stu-id="b3f0b-140">IP filter rule evaluation</span></span>

<span data-ttu-id="b3f0b-141">Reguły filtru IP są stosowane w kolejności i hello Pierwsza reguła określa, czy adres IP hello dopasowań hello zaakceptować lub odrzucić akcji.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="b3f0b-142">Na przykład jeśli adresy tooaccept w 192.168.100.0/22 zakresu hello i odrzucić wszystkie inne hello pierwszą regułę w siatce hello powinna obsługiwać 192.168.100.0/22 zakres adresów hello.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="b3f0b-143">Reguła dalej Hello Odrzuć wszystkie adresy przy użyciu hello zakresu 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="b3f0b-144">Można zmienić kolejność hello reguł filtru IP w siatce hello klikając hello pionowy Wielokropek na powitania początku wiersza i przy użyciu przeciągania i upuść.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="b3f0b-145">filtru IP nowego toosave reguły kolejności, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="b3f0b-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Zmień kolejność hello reguł filtru IP Centrum IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="b3f0b-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3f0b-147">Next steps</span></span>

<span data-ttu-id="b3f0b-148">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b3f0b-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="b3f0b-149">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="b3f0b-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="b3f0b-150">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="b3f0b-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md