---
title: "aaaCheck łączność z obserwatora sieciowego Azure - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak łączność toouse skontaktuj się z obserwatora sieciowego używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="86063-103">Sprawdź łączność z obserwatora sieciowego Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="86063-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="86063-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86063-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="86063-105">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="86063-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="86063-106">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="86063-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="86063-107">Dowiedz się, jak można ustalić toouse łączności tooverify Jeśli bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="86063-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="86063-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="86063-108">Before you begin</span></span>

<span data-ttu-id="86063-109">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="86063-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="86063-110">Wystąpienia obserwatora sieciowego w regionie hello ma toocheck łączności.</span><span class="sxs-lookup"><span data-stu-id="86063-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="86063-111">Maszyny wirtualne toocheck łączność z.</span><span class="sxs-lookup"><span data-stu-id="86063-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="86063-112">Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="86063-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="86063-113">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="86063-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="86063-114">Zarejestruj hello możliwości wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="86063-114">Register hello preview capability</span></span> 

<span data-ttu-id="86063-115">Sprawdź łączność jest obecnie w wersji zapoznawczej toouse ta funkcja wymaga toobe zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="86063-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="86063-116">toodo, uruchom hello następujące przykładowe interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="86063-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="86063-117">Rejestracja hello tooverify zakończyło się powodzeniem, uruchom następujące polecenia interfejsu wiersza polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="86063-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="86063-118">Jeśli funkcja hello zostało prawidłowo zarejestrowane hello dane wyjściowe powinny odpowiadać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="86063-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="86063-119">Sprawdź maszyny wirtualnej tooa łączności</span><span class="sxs-lookup"><span data-stu-id="86063-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="86063-120">W tym przykładzie sprawdza łączność tooa docelowej maszyny wirtualnej za pośrednictwem portu 80.</span><span class="sxs-lookup"><span data-stu-id="86063-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="86063-121">Przykład</span><span class="sxs-lookup"><span data-stu-id="86063-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="86063-122">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="86063-122">Response</span></span>

<span data-ttu-id="86063-123">powitania po odpowiedzi pochodzi z poprzedniego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="86063-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="86063-124">W tej odpowiedzi hello `ConnectionStatus` jest **informujący**.</span><span class="sxs-lookup"><span data-stu-id="86063-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="86063-125">Widać, że wszystkie hello sond wysyłane nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="86063-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="86063-126">łączność Hello na urządzenie wirtualne hello nie powiodła się z powodu tooa konfigurowane przez użytkownika `NetworkSecurityRule` o nazwie **UserRule_Port80**, skonfigurowany tooblock ruch przychodzący na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="86063-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="86063-127">Te informacje mogą być używane tooresearch problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="86063-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="86063-128">Sprawdź poprawność routingu problemów</span><span class="sxs-lookup"><span data-stu-id="86063-128">Validate routing issues</span></span>

<span data-ttu-id="86063-129">przykład Witaj służy do sprawdzania łączności między maszyną wirtualną i zdalny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="86063-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="86063-130">Przykład</span><span class="sxs-lookup"><span data-stu-id="86063-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="86063-131">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="86063-131">Response</span></span>

<span data-ttu-id="86063-132">W hello poniższy przykład, hello `connectionStatus` jest wyświetlany jako **informujący**.</span><span class="sxs-lookup"><span data-stu-id="86063-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="86063-133">W hello `hops` uzyskać szczegółowe informacje, widoczny w obszarze `issues` czy ruch hello zostało zablokowane z powodu tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="86063-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="86063-134">Sprawdź czas oczekiwania witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="86063-134">Check website latency</span></span>

<span data-ttu-id="86063-135">Witaj poniższy przykład sprawdza hello łączności tooa witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="86063-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="86063-136">Przykład</span><span class="sxs-lookup"><span data-stu-id="86063-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="86063-137">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="86063-137">Response</span></span>

<span data-ttu-id="86063-138">Hello po odpowiedzi, zawiera hello `connectionStatus` jest pokazywana jako **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="86063-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="86063-139">Gdy połączenie zostanie nawiązane, znajdują się wartości opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="86063-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="86063-140">Sprawdź łączność tooa pamięci masowej w punkcie końcowym</span><span class="sxs-lookup"><span data-stu-id="86063-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="86063-141">Witaj poniższy przykład służy do sprawdzania hello łączności z konta magazynu blogu tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86063-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="86063-142">Przykład</span><span class="sxs-lookup"><span data-stu-id="86063-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="86063-143">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="86063-143">Response</span></span>

<span data-ttu-id="86063-144">Witaj następujące json jest hello przykład odpowiedzi z polecenia cmdlet poprzedniej hello.</span><span class="sxs-lookup"><span data-stu-id="86063-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="86063-145">Jak wyboru hello zakończy się pomyślnie, hello `connectionStatus` właściwość pokazuje, jak **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="86063-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="86063-146">Podano hello szczegóły dotyczące hello liczba przeskoków wymagane tooreach hello — obiekt blob magazynu i opóźnień.</span><span class="sxs-lookup"><span data-stu-id="86063-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="86063-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86063-147">Next steps</span></span>

<span data-ttu-id="86063-148">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="86063-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="86063-149">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="86063-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
