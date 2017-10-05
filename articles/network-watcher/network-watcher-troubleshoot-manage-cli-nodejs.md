---
title: "Rozwiązywanie problemów z bramy sieci wirtualnej platformy Azure i połączenia - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak użyć obserwatora sieciowego Azure Rozwiązywanie problemów z interfejsu wiersza polecenia platformy Azure w wersji 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 9de4b2a0bdda7ffbd269883877a708d67312092f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="40215-103">Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu usługi Azure sieci obserwatora Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="40215-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="40215-104">Portal</span><span class="sxs-lookup"><span data-stu-id="40215-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="40215-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40215-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="40215-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="40215-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="40215-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="40215-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="40215-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="40215-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="40215-109">Obserwatora sieciowego zawiera wiele funkcji w odniesieniu do zrozumienia zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="40215-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="40215-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="40215-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="40215-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="40215-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="40215-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="40215-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="40215-113">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="40215-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="40215-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="40215-114">Before you begin</span></span>

<span data-ttu-id="40215-115">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="40215-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="40215-116">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="40215-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="40215-117">Omówienie</span><span class="sxs-lookup"><span data-stu-id="40215-117">Overview</span></span>

<span data-ttu-id="40215-118">Rozwiązywanie problemów z zasobów umożliwia rozwiązywanie problemów, które wynikają z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="40215-118">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="40215-119">Po wysłaniu żądania do zasobów dotyczących rozwiązywania problemów, dzienniki są proszeni i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="40215-119">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="40215-120">Po zakończeniu kontroli wyniki są zwracane.</span><span class="sxs-lookup"><span data-stu-id="40215-120">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="40215-121">Żądania dotyczące rozwiązywania problemów są długotrwałe żądania zasobów, może to potrwać kilka minut do zwrócenia wyniku.</span><span class="sxs-lookup"><span data-stu-id="40215-121">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="40215-122">Dzienniki na rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.</span><span class="sxs-lookup"><span data-stu-id="40215-122">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="40215-123">Pobieranie połączenia bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="40215-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="40215-124">W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie.</span><span class="sxs-lookup"><span data-stu-id="40215-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="40215-125">Można również przekazać go Brama sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="40215-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="40215-126">Następujące polecenie cmdlet wyświetla listę połączeń sieci vpn w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="40215-126">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="40215-127">Można również uruchomić polecenie, aby wyświetlić połączeń w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="40215-127">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="40215-128">Po utworzeniu nazwę połączenia, można uruchomić to polecenie, aby pobrać jego identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="40215-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="40215-129">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="40215-129">Create a storage account</span></span>

<span data-ttu-id="40215-130">Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji zasobu, zapisuje dzienniki na konto magazynu, należy sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="40215-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="40215-131">W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.</span><span class="sxs-lookup"><span data-stu-id="40215-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="40215-132">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="40215-132">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="40215-133">Uzyskaj klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="40215-133">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="40215-134">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="40215-134">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="40215-135">Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="40215-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="40215-136">Rozwiązywanie problemów z zasobami za pomocą `network watcher troubleshoot` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="40215-136">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="40215-137">Jest przekazywana polecenia cmdlet grupy zasobów, nazwę obserwatora sieciowego, identyfikator połączenia, identyfikator konta magazynu i ścieżki do obiektu blob do przechowywania Rozwiązywanie problemów z wynikiem.</span><span class="sxs-lookup"><span data-stu-id="40215-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="40215-138">Po uruchomieniu polecenia cmdlet obserwatora sieciowego przegląda zasobów, aby sprawdzić kondycję.</span><span class="sxs-lookup"><span data-stu-id="40215-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="40215-139">Zwraca wyniki do powłoki, a zapisuje dzienniki wyników w określone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="40215-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="40215-140">Opis wyników</span><span class="sxs-lookup"><span data-stu-id="40215-140">Understanding the results</span></span>

<span data-ttu-id="40215-141">Tekst akcji zawiera ogólne wskazówki na temat sposobu rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="40215-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="40215-142">Jeśli dla problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="40215-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="40215-143">W przypadku których nie ma dodatkowych wskazówek, odpowiedź zawiera adres url, aby otworzyć sprawę pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="40215-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="40215-144">Aby uzyskać więcej informacji na temat właściwości odpowiedzi i dostępnych odwiedź [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="40215-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="40215-145">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zapoznaj się [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="40215-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="40215-146">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="40215-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="40215-147">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj przy użyciu następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="40215-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="40215-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40215-148">Next steps</span></span>

<span data-ttu-id="40215-149">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="40215-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
