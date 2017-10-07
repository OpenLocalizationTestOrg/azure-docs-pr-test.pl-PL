---
title: "aaaTroubleshoot połączenia - Azure CLI 1.0 i Brama sieci wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toouse hello Azure obserwatora sieciowego Rozwiązywanie problemów z interfejsu wiersza polecenia platformy Azure w wersji 1.0"
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
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="c51e7-103">Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu usługi Azure sieci obserwatora Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c51e7-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c51e7-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c51e7-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="c51e7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c51e7-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="c51e7-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c51e7-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="c51e7-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c51e7-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="c51e7-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="c51e7-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="c51e7-109">Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c51e7-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="c51e7-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="c51e7-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="c51e7-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="c51e7-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="c51e7-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="c51e7-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="c51e7-113">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="c51e7-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c51e7-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c51e7-114">Before you begin</span></span>

<span data-ttu-id="c51e7-115">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c51e7-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="c51e7-116">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="c51e7-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="c51e7-117">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c51e7-117">Overview</span></span>

<span data-ttu-id="c51e7-118">Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="c51e7-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="c51e7-119">Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="c51e7-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="c51e7-120">Po zakończeniu kontroli hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="c51e7-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="c51e7-121">Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik.</span><span class="sxs-lookup"><span data-stu-id="c51e7-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="c51e7-122">Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.</span><span class="sxs-lookup"><span data-stu-id="c51e7-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="c51e7-123">Pobieranie połączenia bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c51e7-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="c51e7-124">W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie.</span><span class="sxs-lookup"><span data-stu-id="c51e7-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="c51e7-125">Można również przekazać go Brama sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c51e7-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="c51e7-126">Witaj następujące polecenie cmdlet wyświetla listę hello połączeń sieci vpn w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="c51e7-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="c51e7-127">Można również uruchomić toosee polecenia hello hello połączeń w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c51e7-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="c51e7-128">Po utworzeniu hello nazwę połączenia hello, można uruchomić tego polecenia tooget jego identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="c51e7-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="c51e7-129">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="c51e7-129">Create a storage account</span></span>

<span data-ttu-id="c51e7-130">Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu, zapisuje dzienniki tooa magazynu konta toobe sprawdzone.</span><span class="sxs-lookup"><span data-stu-id="c51e7-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="c51e7-131">W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.</span><span class="sxs-lookup"><span data-stu-id="c51e7-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="c51e7-132">Tworzenie konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="c51e7-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="c51e7-133">Uzyskaj klucze konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="c51e7-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="c51e7-134">Tworzenie kontenera hello</span><span class="sxs-lookup"><span data-stu-id="c51e7-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="c51e7-135">Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="c51e7-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="c51e7-136">Rozwiązywanie problemów z zasobami za pomocą hello `network watcher troubleshoot` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c51e7-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="c51e7-137">Grupy zasobów hello polecenia cmdlet hello jest przekazywana, hello nazwa hello obserwatora sieciowego, hello identyfikator połączenia hello hello identyfikator hello konta magazynu i hello ścieżki toohello obiektu blob toostore hello Rozwiązywanie problemów z wynikiem.</span><span class="sxs-lookup"><span data-stu-id="c51e7-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="c51e7-138">Po uruchomieniu polecenia cmdlet hello obserwatora sieciowego przegląda hello zasobów tooverify hello kondycji.</span><span class="sxs-lookup"><span data-stu-id="c51e7-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="c51e7-139">Zwraca wyniki hello toohello powłoki, a są przechowywane dzienniki hello wyników na koncie magazynu hello określony.</span><span class="sxs-lookup"><span data-stu-id="c51e7-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="c51e7-140">Opis wyników hello</span><span class="sxs-lookup"><span data-stu-id="c51e7-140">Understanding hello results</span></span>

<span data-ttu-id="c51e7-141">tekst akcji Hello zawiera ogólne wskazówki dotyczące sposobu tooresolve hello problem.</span><span class="sxs-lookup"><span data-stu-id="c51e7-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="c51e7-142">Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="c51e7-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="c51e7-143">W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c51e7-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="c51e7-144">Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c51e7-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="c51e7-145">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c51e7-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c51e7-146">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="c51e7-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="c51e7-147">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="c51e7-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c51e7-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c51e7-148">Next steps</span></span>

<span data-ttu-id="c51e7-149">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="c51e7-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
