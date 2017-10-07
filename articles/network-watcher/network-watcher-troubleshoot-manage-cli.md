---
title: "aaaTroubleshoot połączenia - Azure CLI 2.0 i Brama sieci wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toouse hello Azure obserwatora sieciowego Rozwiązywanie problemów z 2.0 interfejsu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="8febc-103">Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu usługi Azure sieci obserwatora Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8febc-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8febc-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8febc-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="8febc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8febc-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="8febc-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="8febc-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="8febc-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="8febc-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="8febc-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="8febc-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="8febc-109">Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8febc-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="8febc-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="8febc-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="8febc-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="8febc-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="8febc-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="8febc-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="8febc-113">W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="8febc-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8febc-114">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8febc-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8febc-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8febc-115">Before you begin</span></span>

<span data-ttu-id="8febc-116">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="8febc-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="8febc-117">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="8febc-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="8febc-118">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8febc-118">Overview</span></span>

<span data-ttu-id="8febc-119">Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="8febc-119">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="8febc-120">Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="8febc-120">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="8febc-121">Po zakończeniu kontroli hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="8febc-121">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="8febc-122">Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik.</span><span class="sxs-lookup"><span data-stu-id="8febc-122">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="8febc-123">Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.</span><span class="sxs-lookup"><span data-stu-id="8febc-123">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="8febc-124">Pobieranie połączenia bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8febc-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="8febc-125">W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie.</span><span class="sxs-lookup"><span data-stu-id="8febc-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="8febc-126">Można również przekazać go Brama sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8febc-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="8febc-127">Witaj następujące polecenie cmdlet wyświetla listę hello połączeń sieci vpn w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8febc-127">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="8febc-128">Po utworzeniu hello nazwę połączenia hello, można uruchomić tego polecenia tooget jego identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="8febc-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="8febc-129">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="8febc-129">Create a storage account</span></span>

<span data-ttu-id="8febc-130">Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu, zapisuje dzienniki tooa magazynu konta toobe sprawdzone.</span><span class="sxs-lookup"><span data-stu-id="8febc-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="8febc-131">W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.</span><span class="sxs-lookup"><span data-stu-id="8febc-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="8febc-132">Tworzenie konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="8febc-132">Create hello storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="8febc-133">Uzyskaj klucze konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="8febc-133">Get hello storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="8febc-134">Tworzenie kontenera hello</span><span class="sxs-lookup"><span data-stu-id="8febc-134">Create hello container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="8febc-135">Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="8febc-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="8febc-136">Rozwiązywanie problemów z zasobami za pomocą hello `az network watcher troubleshooting` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8febc-136">You troubleshoot resources with hello `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="8febc-137">Grupy zasobów hello polecenia cmdlet hello jest przekazywana, hello nazwa hello obserwatora sieciowego, hello identyfikator połączenia hello hello identyfikator hello konta magazynu i hello ścieżki toohello obiektu blob toostore hello Rozwiązywanie problemów z wynikiem.</span><span class="sxs-lookup"><span data-stu-id="8febc-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="8febc-138">Po uruchomieniu polecenia cmdlet hello obserwatora sieciowego przegląda hello zasobów tooverify hello kondycji.</span><span class="sxs-lookup"><span data-stu-id="8febc-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="8febc-139">Zwraca wyniki hello toohello powłoki, a są przechowywane dzienniki hello wyników na koncie magazynu hello określony.</span><span class="sxs-lookup"><span data-stu-id="8febc-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="8febc-140">Opis wyników hello</span><span class="sxs-lookup"><span data-stu-id="8febc-140">Understanding hello results</span></span>

<span data-ttu-id="8febc-141">tekst akcji Hello zawiera ogólne wskazówki dotyczące sposobu tooresolve hello problem.</span><span class="sxs-lookup"><span data-stu-id="8febc-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="8febc-142">Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="8febc-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="8febc-143">W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="8febc-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="8febc-144">Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8febc-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="8febc-145">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8febc-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8febc-146">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="8febc-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="8febc-147">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="8febc-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8febc-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8febc-148">Next steps</span></span>

<span data-ttu-id="8febc-149">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="8febc-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
