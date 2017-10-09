---
title: "aaaTroubleshoot Brama sieci wirtualnej platformy Azure i połączeń - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toouse hello Azure obserwatora sieciowego Rozwiązywanie problemów z polecenia cmdlet programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="7488f-103">Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu programu PowerShell obserwatora sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7488f-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7488f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7488f-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="7488f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7488f-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="7488f-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="7488f-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="7488f-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="7488f-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="7488f-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7488f-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="7488f-109">Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7488f-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="7488f-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="7488f-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="7488f-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="7488f-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="7488f-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="7488f-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7488f-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="7488f-113">Before you begin</span></span>

<span data-ttu-id="7488f-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7488f-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="7488f-115">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="7488f-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="7488f-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7488f-116">Overview</span></span>

<span data-ttu-id="7488f-117">Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="7488f-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="7488f-118">Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="7488f-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="7488f-119">Po zakończeniu kontroli hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="7488f-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="7488f-120">Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik.</span><span class="sxs-lookup"><span data-stu-id="7488f-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="7488f-121">Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.</span><span class="sxs-lookup"><span data-stu-id="7488f-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="7488f-122">Rozwiązywanie problemów z bramy i połączenie</span><span class="sxs-lookup"><span data-stu-id="7488f-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="7488f-123">Przejdź toohello [portalu Azure](https://portal.azure.com) i kliknij przycisk **sieci** > **obserwatora sieciowego** > **diagnostyki sieci VPN**</span><span class="sxs-lookup"><span data-stu-id="7488f-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="7488f-124">Wybierz **subskrypcji**, **grupy zasobów**, i **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="7488f-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="7488f-125">Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="7488f-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="7488f-126">Zapisuje konta magazynu tooa odpowiednich dzienniki toobe sprawdzone.</span><span class="sxs-lookup"><span data-stu-id="7488f-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="7488f-127">Kliknij przycisk **konta magazynu** tooselect konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7488f-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="7488f-128">Na powitania **kont magazynu** bloku, wybrać istniejące konto magazynu, lub kliknij przycisk **+ konto magazynu** toocreate nowy.</span><span class="sxs-lookup"><span data-stu-id="7488f-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="7488f-129">Na powitania **kontenery** bloku, wybierz istniejącego kontenera, lub kliknij przycisk **+ kontener** toocreate nowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="7488f-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="7488f-130">Po zakończeniu kliknij przycisk **wybierz**</span><span class="sxs-lookup"><span data-stu-id="7488f-130">When complete click **Select**</span></span>
6. <span data-ttu-id="7488f-131">Wybierz hello bramy i połączenie tootroubleshoot zasobów, a następnie kliknij przycisk **Uruchom Rozwiązywanie problemów**</span><span class="sxs-lookup"><span data-stu-id="7488f-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="7488f-132">Jeśli wybrano wiele zasobów, rozwiązywania problemów jest uruchamiane jednocześnie zasobów bramy.</span><span class="sxs-lookup"><span data-stu-id="7488f-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="7488f-133">Nie można uruchomić na połączenie i związany z bramą w hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="7488f-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="7488f-134">Zalecane jest bram tootroubleshoot najpierw Rozwiązywanie problemów z połączenia jest procesem dłużej.</span><span class="sxs-lookup"><span data-stu-id="7488f-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="7488f-135">Podczas diagnostyki sieci VPN jest uruchomiona na powitania zasobów **rozwiązywania problemów stanu** będzie stan kolumny **uruchomiona**</span><span class="sxs-lookup"><span data-stu-id="7488f-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="7488f-136">Po zakończeniu hello zmiany stanu kolumny zbyt**dobra kondycja** lub **niezdrowego**.</span><span class="sxs-lookup"><span data-stu-id="7488f-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![Rozwiązywanie problemów ukończone][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="7488f-138">Opis wyników hello</span><span class="sxs-lookup"><span data-stu-id="7488f-138">Understanding hello results</span></span>

<span data-ttu-id="7488f-139">W hello **szczegóły** sekcji okna hello hello **stan** karcie są wyświetlane hello stan ostatniego rozwiązywania hello wykonywania hello wybrane zasobu.</span><span class="sxs-lookup"><span data-stu-id="7488f-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="7488f-140">Wyniki diagnostyki najnowsze hello są wyświetlane xx minut po hello ostatniego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="7488f-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="7488f-141">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7488f-141">Property</span></span>  |<span data-ttu-id="7488f-142">Opis</span><span class="sxs-lookup"><span data-stu-id="7488f-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7488f-143">Zasób</span><span class="sxs-lookup"><span data-stu-id="7488f-143">Resource</span></span>     | <span data-ttu-id="7488f-144">Zasób toohello łącza.</span><span class="sxs-lookup"><span data-stu-id="7488f-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="7488f-145">Ścieżki do magazynu</span><span class="sxs-lookup"><span data-stu-id="7488f-145">Storage path</span></span>     |  <span data-ttu-id="7488f-146">Konto magazynu toohello ścieżki i kontener zawierające dzienniki hello (Jeśli żadnego zostały utworzone podczas uruchamiania hello).</span><span class="sxs-lookup"><span data-stu-id="7488f-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="7488f-147">To ustawienie nie jest trwały, po zakończeniu działania hello portalu.</span><span class="sxs-lookup"><span data-stu-id="7488f-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="7488f-148">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="7488f-148">Summary</span></span>     | <span data-ttu-id="7488f-149">Podsumowanie kondycji zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="7488f-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="7488f-150">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="7488f-150">Detail</span></span>     | <span data-ttu-id="7488f-151">Szczegółowe informacje o kondycji zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="7488f-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="7488f-152">Ostatniego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="7488f-152">Last run</span></span>     | <span data-ttu-id="7488f-153">Witaj hello czas ostatniego czasu rozwiązywania problemów zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="7488f-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="7488f-154">Witaj **akcji** karta zawiera ogólne wskazówki dotyczące jak tooresolve hello problem.</span><span class="sxs-lookup"><span data-stu-id="7488f-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="7488f-155">Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="7488f-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="7488f-156">W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="7488f-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="7488f-157">Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7488f-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="7488f-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7488f-158">Next steps</span></span>

<span data-ttu-id="7488f-159">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="7488f-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
