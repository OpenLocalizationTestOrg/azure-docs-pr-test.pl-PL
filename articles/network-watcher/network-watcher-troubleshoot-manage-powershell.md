---
title: "Rozwiązywanie problemów z bramy sieci wirtualnej platformy Azure i połączenia - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak użyć obserwatora sieciowego Azure Rozwiązywanie problemów z polecenia cmdlet programu PowerShell"
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
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="b2097-103">Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu programu PowerShell obserwatora sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b2097-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b2097-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b2097-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="b2097-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2097-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="b2097-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="b2097-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="b2097-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="b2097-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="b2097-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="b2097-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="b2097-109">Obserwatora sieciowego zawiera wiele funkcji w odniesieniu do zrozumienia zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b2097-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="b2097-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="b2097-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="b2097-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b2097-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="b2097-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="b2097-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b2097-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b2097-113">Before you begin</span></span>

<span data-ttu-id="b2097-114">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b2097-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="b2097-115">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="b2097-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="b2097-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b2097-116">Overview</span></span>

<span data-ttu-id="b2097-117">Rozwiązywanie problemów z zasobów umożliwia rozwiązywanie problemów, które wynikają z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="b2097-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="b2097-118">Po wysłaniu żądania do zasobów dotyczących rozwiązywania problemów, dzienniki są proszeni i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="b2097-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="b2097-119">Po zakończeniu kontroli wyniki są zwracane.</span><span class="sxs-lookup"><span data-stu-id="b2097-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="b2097-120">Żądania dotyczące rozwiązywania problemów są długotrwałe żądania zasobów, może to potrwać kilka minut do zwrócenia wyniku.</span><span class="sxs-lookup"><span data-stu-id="b2097-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="b2097-121">Dzienniki na rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.</span><span class="sxs-lookup"><span data-stu-id="b2097-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="b2097-122">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="b2097-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="b2097-123">Pierwszym krokiem jest pobrać wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b2097-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="b2097-124">`$networkWatcher` Zmienna jest przekazywana do `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="b2097-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="b2097-125">Pobieranie połączenia bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b2097-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="b2097-126">W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie.</span><span class="sxs-lookup"><span data-stu-id="b2097-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="b2097-127">Można również przekazać go Brama sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2097-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="b2097-128">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="b2097-128">Create a storage account</span></span>

<span data-ttu-id="b2097-129">Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji zasobu, zapisuje dzienniki na konto magazynu, należy sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="b2097-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="b2097-130">W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.</span><span class="sxs-lookup"><span data-stu-id="b2097-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="b2097-131">Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="b2097-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="b2097-132">Rozwiązywanie problemów z zasobami za pomocą `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b2097-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="b2097-133">Polecenie cmdlet jest przekazywana obiektów obserwatora sieciowego, identyfikator połączenia lub brama sieci wirtualnej, identyfikator konta magazynu i ścieżki do przechowywania wyników.</span><span class="sxs-lookup"><span data-stu-id="b2097-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="b2097-134">`Start-AzureRmNetworkWatcherResourceTroubleshooting` Polecenia cmdlet jest długo działające i może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b2097-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="b2097-135">Po uruchomieniu polecenia cmdlet obserwatora sieciowego przegląda zasobów, aby sprawdzić kondycję.</span><span class="sxs-lookup"><span data-stu-id="b2097-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="b2097-136">Zwraca wyniki do powłoki, a zapisuje dzienniki wyników w określone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2097-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="b2097-137">Opis wyników</span><span class="sxs-lookup"><span data-stu-id="b2097-137">Understanding the results</span></span>

<span data-ttu-id="b2097-138">Tekst akcji zawiera ogólne wskazówki na temat sposobu rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="b2097-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="b2097-139">Jeśli dla problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="b2097-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="b2097-140">W przypadku których nie ma dodatkowych wskazówek, odpowiedź zawiera adres url, aby otworzyć sprawę pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b2097-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="b2097-141">Aby uzyskać więcej informacji na temat właściwości odpowiedzi i dostępnych odwiedź [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b2097-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="b2097-142">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zapoznaj się [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="b2097-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="b2097-143">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="b2097-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="b2097-144">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj przy użyciu następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="b2097-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2097-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2097-145">Next steps</span></span>

<span data-ttu-id="b2097-146">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="b2097-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
