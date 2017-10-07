---
title: "aaaTroubleshoot Brama sieci wirtualnej i połączenia za pomocą Monitora sieci Azure - REST | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak tootroubleshoot bramy sieci wirtualnej i połączenia obserwator sieci Azure przy użyciu REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="18335-103">Rozwiązywanie problemów z bramy sieci wirtualnej i połączeń za pomocą Monitora sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="18335-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="18335-104">Portal</span><span class="sxs-lookup"><span data-stu-id="18335-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="18335-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18335-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="18335-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="18335-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="18335-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="18335-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="18335-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="18335-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="18335-109">Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="18335-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="18335-110">Jeden z tych funkcji jest zasobem rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="18335-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="18335-111">Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="18335-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="18335-112">Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.</span><span class="sxs-lookup"><span data-stu-id="18335-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="18335-113">Ten artykuł przedstawia za pomocą zadań zarządzania różnych hello, które są obecnie dostępne dla zasobu Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="18335-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="18335-114">**Rozwiązywanie problemów z bramy sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="18335-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="18335-115">**Rozwiązywanie problemów z połączeniem**</span><span class="sxs-lookup"><span data-stu-id="18335-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="18335-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="18335-116">Before you begin</span></span>

<span data-ttu-id="18335-117">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18335-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="18335-118">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="18335-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="18335-119">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="18335-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="18335-120">Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="18335-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="18335-121">Omówienie</span><span class="sxs-lookup"><span data-stu-id="18335-121">Overview</span></span>

<span data-ttu-id="18335-122">Rozwiązywanie problemów z siecią obserwatora umożliwia określenie hello rozwiązywania problemów, które wynikają z połączeniami i bram sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="18335-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="18335-123">Po wysłaniu żądania zasobów toohello rozwiązywania problemów, dzienniki wykonywania zapytania dotyczącego i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="18335-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="18335-124">Po zakończeniu kontroli hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="18335-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="18335-125">Witaj Rozwiązywanie problemów z interfejsu API żądania są długie uruchomionych żądań, które może potrwać kilka minut tooreturn wynik.</span><span class="sxs-lookup"><span data-stu-id="18335-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="18335-126">Dzienniki są przechowywane w kontenerze na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="18335-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="18335-127">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="18335-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="18335-128">Rozwiązywanie problemów z bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="18335-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="18335-129">Witaj POST Rozwiązywanie problemów z żądania</span><span class="sxs-lookup"><span data-stu-id="18335-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="18335-130">Witaj następujące przykładowe zapytania hello stan bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="18335-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="18335-131">Ponieważ ta operacja jest długa uruchomiona, hello identyfikatora URI dla zapytań hello operacji i hello identyfikatora URI dla wyniku hello jest zwracany w hello nagłówka odpowiedzi, pokazane na powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="18335-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="18335-132">**Ważne wartości**</span><span class="sxs-lookup"><span data-stu-id="18335-132">**Important Values**</span></span>

* <span data-ttu-id="18335-133">**Azure AsyncOperation** — ta właściwość zawiera hello URI tooquery hello Async Rozwiązywanie problemów z operacji</span><span class="sxs-lookup"><span data-stu-id="18335-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="18335-134">**Lokalizacja** — ta właściwość zawiera hello identyfikatora URI, których hello wyniki są, gdy hello operacja została zakończona</span><span class="sxs-lookup"><span data-stu-id="18335-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="18335-135">Operacja asynchroniczna hello ukończenia zapytania</span><span class="sxs-lookup"><span data-stu-id="18335-135">Query hello async operation for completion</span></span>

<span data-ttu-id="18335-136">Na użytek hello operacji URI tooquery hello postęp operacji hello w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="18335-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="18335-137">Gdy trwa operacja hello, hello pokazuje odpowiedzi **w toku** w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="18335-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="18335-138">Podczas operacji hello jest zmiany stanu ukończenia hello za**zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="18335-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="18335-139">Pobierz wyniki hello</span><span class="sxs-lookup"><span data-stu-id="18335-139">Retrieve hello results</span></span>

<span data-ttu-id="18335-140">Gdy zwrócony stan hello **zakończyło się pomyślnie**, wywołanie metody GET na powitania klasy operationResult URI tooretrieve hello wyników.</span><span class="sxs-lookup"><span data-stu-id="18335-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="18335-141">Hello są następujące odpowiedzi przykłady typowych odpowiedzi obniżeniem zwrócony podczas wykonywania zapytania wyniki hello Rozwiązywanie problemów z bramą.</span><span class="sxs-lookup"><span data-stu-id="18335-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="18335-142">Zobacz [opis wyników hello](#understanding-the-results) tooget wyjaśnienia dotyczące właściwości, które hello w hello oznaczają odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="18335-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="18335-143">Rozwiązywanie problemów z połączeniami</span><span class="sxs-lookup"><span data-stu-id="18335-143">Troubleshoot Connections</span></span>

<span data-ttu-id="18335-144">Witaj następujące przykładowe zapytania hello stanu połączenia.</span><span class="sxs-lookup"><span data-stu-id="18335-144">hello following example queries hello status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> <span data-ttu-id="18335-145">Witaj Rozwiązywanie problemów z operacji nie można uruchomić równolegle na połączenie i jego odpowiednich bram.</span><span class="sxs-lookup"><span data-stu-id="18335-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="18335-146">Operacja Hello należy wykonać przed toorunning go na powitania poprzedni zasób.</span><span class="sxs-lookup"><span data-stu-id="18335-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="18335-147">Ponieważ jest to długo działające transakcji, nagłówek odpowiedzi hello, hello identyfikator URI do wykonywania zapytań w operacji hello i hello identyfikatora URI dla wyniku hello jest zwracane, jak pokazano w powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="18335-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="18335-148">**Ważne wartości**</span><span class="sxs-lookup"><span data-stu-id="18335-148">**Important Values**</span></span>

* <span data-ttu-id="18335-149">**Azure AsyncOperation** — ta właściwość zawiera hello URI tooquery hello Async Rozwiązywanie problemów z operacji</span><span class="sxs-lookup"><span data-stu-id="18335-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="18335-150">**Lokalizacja** — ta właściwość zawiera hello identyfikatora URI, których hello wyniki są, gdy hello operacja została zakończona</span><span class="sxs-lookup"><span data-stu-id="18335-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="18335-151">Operacja asynchroniczna hello ukończenia zapytania</span><span class="sxs-lookup"><span data-stu-id="18335-151">Query hello async operation for completion</span></span>

<span data-ttu-id="18335-152">Na użytek hello operacji URI tooquery hello postęp operacji hello w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="18335-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="18335-153">Gdy trwa operacja hello, hello pokazuje odpowiedzi **w toku** w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="18335-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="18335-154">Po zakończeniu operacji hello hello stan zmienia się zbyt**zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="18335-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="18335-155">Hello są następujące odpowiedzi przykłady typowych odpowiedzi zwracany podczas wykonywania zapytania wyniki hello Rozwiązywanie problemów z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="18335-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="18335-156">Pobierz wyniki hello</span><span class="sxs-lookup"><span data-stu-id="18335-156">Retrieve hello results</span></span>

<span data-ttu-id="18335-157">Gdy zwrócony stan hello **zakończyło się pomyślnie**, wywołanie metody GET na powitania klasy operationResult URI tooretrieve hello wyników.</span><span class="sxs-lookup"><span data-stu-id="18335-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="18335-158">Hello są następujące odpowiedzi przykłady typowych odpowiedzi zwracany podczas wykonywania zapytania wyniki hello Rozwiązywanie problemów z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="18335-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a><span data-ttu-id="18335-159">Opis wyników hello</span><span class="sxs-lookup"><span data-stu-id="18335-159">Understanding hello results</span></span>

<span data-ttu-id="18335-160">tekst akcji Hello zawiera ogólne wskazówki dotyczące sposobu tooresolve hello problem.</span><span class="sxs-lookup"><span data-stu-id="18335-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="18335-161">Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="18335-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="18335-162">W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="18335-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="18335-163">Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="18335-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="18335-164">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="18335-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="18335-165">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="18335-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="18335-166">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="18335-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="18335-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18335-167">Next steps</span></span>

<span data-ttu-id="18335-168">Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.</span><span class="sxs-lookup"><span data-stu-id="18335-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
