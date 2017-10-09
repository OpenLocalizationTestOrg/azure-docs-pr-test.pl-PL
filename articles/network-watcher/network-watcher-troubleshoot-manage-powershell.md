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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="73587-103">Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu programu PowerShell obserwatora sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="73587-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="73587-104">Portal</span><span class="sxs-lookup"><span data-stu-id="73587-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="73587-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73587-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="73587-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="73587-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="73587-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="73587-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="73587-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="73587-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="73587-109">Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="73587-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="73587-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="73587-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="73587-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="73587-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="73587-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="73587-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="73587-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="73587-113">Before you begin</span></span>

<span data-ttu-id="73587-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="73587-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="73587-115">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="73587-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="73587-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="73587-116">Overview</span></span>

<span data-ttu-id="73587-117">Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="73587-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="73587-118">Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="73587-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="73587-119">Po zakończeniu kontroli hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="73587-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="73587-120">Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik.</span><span class="sxs-lookup"><span data-stu-id="73587-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="73587-121">Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.</span><span class="sxs-lookup"><span data-stu-id="73587-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="73587-122">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="73587-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="73587-123">pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="73587-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="73587-124">Witaj `$networkWatcher` zmienna jest przekazywana toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="73587-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="73587-125">Pobieranie połączenia bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="73587-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="73587-126">W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie.</span><span class="sxs-lookup"><span data-stu-id="73587-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="73587-127">Można również przekazać go Brama sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73587-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="73587-128">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="73587-128">Create a storage account</span></span>

<span data-ttu-id="73587-129">Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu, zapisuje dzienniki tooa magazynu konta toobe sprawdzone.</span><span class="sxs-lookup"><span data-stu-id="73587-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="73587-130">W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.</span><span class="sxs-lookup"><span data-stu-id="73587-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="73587-131">Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="73587-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="73587-132">Rozwiązywanie problemów z zasobami za pomocą hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73587-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="73587-133">Jest przekazywana hello polecenia cmdlet hello obserwatora sieciowego obiektu, hello identyfikator hello połączenia lub brama sieci wirtualnej, identyfikator konta magazynu hello i hello ścieżki toostore hello wyników.</span><span class="sxs-lookup"><span data-stu-id="73587-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="73587-134">Witaj `Start-AzureRmNetworkWatcherResourceTroubleshooting` jest długo działające i może potrwać kilka minut toocomplete polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73587-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="73587-135">Po uruchomieniu polecenia cmdlet hello obserwatora sieciowego przegląda hello zasobów tooverify hello kondycji.</span><span class="sxs-lookup"><span data-stu-id="73587-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="73587-136">Zwraca wyniki hello toohello powłoki, a są przechowywane dzienniki hello wyników na koncie magazynu hello określony.</span><span class="sxs-lookup"><span data-stu-id="73587-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="73587-137">Opis wyników hello</span><span class="sxs-lookup"><span data-stu-id="73587-137">Understanding hello results</span></span>

<span data-ttu-id="73587-138">tekst akcji Hello zawiera ogólne wskazówki dotyczące sposobu tooresolve hello problem.</span><span class="sxs-lookup"><span data-stu-id="73587-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="73587-139">Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="73587-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="73587-140">W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="73587-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="73587-141">Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="73587-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="73587-142">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="73587-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="73587-143">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="73587-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="73587-144">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="73587-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="73587-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73587-145">Next steps</span></span>

<span data-ttu-id="73587-146">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="73587-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
