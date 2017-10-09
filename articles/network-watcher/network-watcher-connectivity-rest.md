---
title: "aaaCheck łączność z obserwatora sieciowego Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toocheck łączność z obserwatora sieciowego w hello portalu Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="1d43e-103">Sprawdź łączność z obserwatora sieciowego Azure przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1d43e-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1d43e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1d43e-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="1d43e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d43e-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="1d43e-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="1d43e-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="1d43e-107">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="1d43e-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="1d43e-108">Dowiedz się, jak można ustalić toouse łączności tooverify Jeśli bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="1d43e-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1d43e-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1d43e-109">Before you begin</span></span>

<span data-ttu-id="1d43e-110">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="1d43e-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="1d43e-111">Wystąpienia obserwatora sieciowego w regionie hello ma toocheck łączności.</span><span class="sxs-lookup"><span data-stu-id="1d43e-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="1d43e-112">Maszyny wirtualne toocheck łączność z.</span><span class="sxs-lookup"><span data-stu-id="1d43e-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="1d43e-113">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d43e-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="1d43e-114">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="1d43e-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="1d43e-115">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1d43e-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="1d43e-116">Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="1d43e-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="1d43e-117">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="1d43e-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="1d43e-118">Zarejestruj hello możliwości wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="1d43e-118">Register hello preview capability</span></span>

<span data-ttu-id="1d43e-119">Sprawdź łączność jest obecnie w wersji zapoznawczej toouse ta funkcja wymaga toobe zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="1d43e-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="1d43e-120">toodo tego, hello uruchomienia następującego programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1d43e-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="1d43e-121">Rejestracja hello tooverify zakończyło się powodzeniem, uruchom następujące przykładowe Powershell hello:</span><span class="sxs-lookup"><span data-stu-id="1d43e-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="1d43e-122">Jeśli funkcja hello zostało prawidłowo zarejestrowane hello dane wyjściowe powinny odpowiadać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1d43e-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="1d43e-123">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="1d43e-123">Log in with ARMClient</span></span>

<span data-ttu-id="1d43e-124">Zaloguj się za tooarmclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d43e-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="1d43e-125">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1d43e-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="1d43e-126">Uruchom maszynę wirtualną powitania po tooreturn skryptu.</span><span class="sxs-lookup"><span data-stu-id="1d43e-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="1d43e-127">Te informacje są potrzebne do uruchomienia połączenia.</span><span class="sxs-lookup"><span data-stu-id="1d43e-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="1d43e-128">Hello następującego kodu wymaga wartości dla hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="1d43e-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="1d43e-129">**Identyfikator subskrypcji** — Witaj toouse identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1d43e-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="1d43e-130">**resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="1d43e-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="1d43e-131">Z danych wyjściowych poniżej hello, identyfikator hello maszyny wirtualnej hello jest używany w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="1d43e-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="1d43e-132">Sprawdź maszyny wirtualnej tooa łączności</span><span class="sxs-lookup"><span data-stu-id="1d43e-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="1d43e-133">W tym przykładzie sprawdza łączność tooa docelowej maszyny wirtualnej za pośrednictwem portu 80.</span><span class="sxs-lookup"><span data-stu-id="1d43e-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="1d43e-134">Przykład</span><span class="sxs-lookup"><span data-stu-id="1d43e-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1d43e-135">Ponieważ ta operacja jest długa systemem hello identyfikatora URI dla wyniku hello jest zwracany w nagłówek odpowiedzi hello pokazane na powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="1d43e-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1d43e-136">**Ważne wartości**</span><span class="sxs-lookup"><span data-stu-id="1d43e-136">**Important Values**</span></span>

* <span data-ttu-id="1d43e-137">**Lokalizacja** — ta właściwość zawiera hello identyfikatora URI, których hello wyniki są, gdy hello operacja została zakończona</span><span class="sxs-lookup"><span data-stu-id="1d43e-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="1d43e-138">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="1d43e-138">Response</span></span>

<span data-ttu-id="1d43e-139">powitania po odpowiedzi pochodzi z poprzedniego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="1d43e-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="1d43e-140">W tej odpowiedzi hello `ConnectionStatus` jest **informujący**.</span><span class="sxs-lookup"><span data-stu-id="1d43e-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="1d43e-141">Widać, że wszystkie hello sond wysyłane nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="1d43e-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="1d43e-142">łączność Hello na urządzenie wirtualne hello nie powiodła się z powodu tooa konfigurowane przez użytkownika `NetworkSecurityRule` o nazwie **UserRule_Port80**, skonfigurowany tooblock ruch przychodzący na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="1d43e-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="1d43e-143">Te informacje mogą być używane tooresearch problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="1d43e-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="1d43e-144">Sprawdź poprawność routingu problemów</span><span class="sxs-lookup"><span data-stu-id="1d43e-144">Validate routing issues</span></span>

<span data-ttu-id="1d43e-145">przykład Witaj służy do sprawdzania łączności między maszyną wirtualną i zdalny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="1d43e-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="1d43e-146">Przykład</span><span class="sxs-lookup"><span data-stu-id="1d43e-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1d43e-147">Ponieważ ta operacja jest długa systemem hello identyfikatora URI dla wyniku hello jest zwracany w nagłówek odpowiedzi hello pokazane na powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="1d43e-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1d43e-148">**Ważne wartości**</span><span class="sxs-lookup"><span data-stu-id="1d43e-148">**Important Values**</span></span>

* <span data-ttu-id="1d43e-149">**Lokalizacja** — ta właściwość zawiera hello identyfikatora URI, których hello wyniki są, gdy hello operacja została zakończona</span><span class="sxs-lookup"><span data-stu-id="1d43e-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="1d43e-150">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="1d43e-150">Response</span></span>

<span data-ttu-id="1d43e-151">W hello poniższy przykład, hello `connectionStatus` jest wyświetlany jako **informujący**.</span><span class="sxs-lookup"><span data-stu-id="1d43e-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="1d43e-152">W hello `hops` uzyskać szczegółowe informacje, widoczny w obszarze `issues` czy ruch hello zostało zablokowane z powodu tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="1d43e-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="1d43e-153">Sprawdź czas oczekiwania witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="1d43e-153">Check website latency</span></span>

<span data-ttu-id="1d43e-154">Witaj poniższy przykład sprawdza hello łączności tooa witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1d43e-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="1d43e-155">Przykład</span><span class="sxs-lookup"><span data-stu-id="1d43e-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1d43e-156">Ponieważ ta operacja jest długa systemem hello identyfikatora URI dla wyniku hello jest zwracany w nagłówek odpowiedzi hello pokazane na powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="1d43e-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1d43e-157">**Ważne wartości**</span><span class="sxs-lookup"><span data-stu-id="1d43e-157">**Important Values**</span></span>

* <span data-ttu-id="1d43e-158">**Lokalizacja** — ta właściwość zawiera hello identyfikatora URI, których hello wyniki są, gdy hello operacja została zakończona</span><span class="sxs-lookup"><span data-stu-id="1d43e-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="1d43e-159">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="1d43e-159">Response</span></span>

<span data-ttu-id="1d43e-160">Hello po odpowiedzi, zawiera hello `connectionStatus` jest pokazywana jako **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="1d43e-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="1d43e-161">Gdy połączenie zostanie nawiązane, znajdują się wartości opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="1d43e-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="1d43e-162">Sprawdź łączność tooa pamięci masowej w punkcie końcowym</span><span class="sxs-lookup"><span data-stu-id="1d43e-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="1d43e-163">Witaj poniższy przykład służy do sprawdzania hello łączności z konta magazynu blogu tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d43e-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="1d43e-164">Przykład</span><span class="sxs-lookup"><span data-stu-id="1d43e-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1d43e-165">Ponieważ ta operacja jest długa systemem hello identyfikatora URI dla wyniku hello jest zwracany w nagłówek odpowiedzi hello pokazane na powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="1d43e-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1d43e-166">**Ważne wartości**</span><span class="sxs-lookup"><span data-stu-id="1d43e-166">**Important Values**</span></span>

* <span data-ttu-id="1d43e-167">**Lokalizacja** — ta właściwość zawiera hello identyfikatora URI, których hello wyniki są, gdy hello operacja została zakończona</span><span class="sxs-lookup"><span data-stu-id="1d43e-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="1d43e-168">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="1d43e-168">Response</span></span>

<span data-ttu-id="1d43e-169">Witaj poniższy przykład hello odpowiedź jest uruchomienie hello poprzedniego wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1d43e-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="1d43e-170">Jak wyboru hello zakończy się pomyślnie, hello `connectionStatus` właściwość pokazuje, jak **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="1d43e-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="1d43e-171">Podano hello szczegóły dotyczące hello liczba przeskoków wymagane tooreach hello — obiekt blob magazynu i opóźnień.</span><span class="sxs-lookup"><span data-stu-id="1d43e-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="1d43e-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d43e-172">Next steps</span></span>

<span data-ttu-id="1d43e-173">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="1d43e-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="1d43e-174">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1d43e-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














