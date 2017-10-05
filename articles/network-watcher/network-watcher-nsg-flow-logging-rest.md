---
title: "Dzienniki przepływ zarządzania sieciową grupę zabezpieczeń z obserwatora sieciowego Azure - interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Ta strona opisano sposób zarządzania dziennikami przepływu sieciowej grupy zabezpieczeń w obserwatora sieciowego Azure z interfejsu API REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c89a2ab4c39978771c940a819493b4e2283d5f9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="c5d8e-103">Konfigurowanie grup zabezpieczeń sieci przepływu dzienników przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="c5d8e-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c5d8e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c5d8e-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="c5d8e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5d8e-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="c5d8e-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c5d8e-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="c5d8e-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c5d8e-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="c5d8e-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="c5d8e-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="c5d8e-109">Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który służy do wyświetlania informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="c5d8e-110">Te dzienniki przepływu są zapisywane w formacie json i Pokaż przepływów wychodzącego i przychodzącego na podstawie reguły w poszczególnych kart przepływ dotyczy 5-elementowej informacji o przepływie (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), i jeśli ruch został dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c5d8e-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c5d8e-111">Before you begin</span></span>

<span data-ttu-id="c5d8e-112">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="c5d8e-113">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="c5d8e-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c5d8e-114">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="c5d8e-115">Dla wywołań interfejsu API REST obserwatora sieciowego się, że nazwa grupy zasobów w identyfikatorze URI żądania jest grupę zasobów, która zawiera obserwatora sieciowego nie zasoby są wykonywane czynności diagnostyczne na.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-115">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="c5d8e-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="c5d8e-116">Scenario</span></span>

<span data-ttu-id="c5d8e-117">Scenariusz omówione w tym artykule przedstawiono sposób włączenia i wyłączenia zapytania przepływu dzienników przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-117">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="c5d8e-118">Aby dowiedzieć się więcej o loggings przepływu sieciowej grupy zabezpieczeń, odwiedź stronę [rejestrowania przepływu grupy zabezpieczeń sieci — omówienie](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5d8e-118">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="c5d8e-119">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="c5d8e-119">In this scenario, you will:</span></span>

* <span data-ttu-id="c5d8e-120">Włączanie dzienników przepływu</span><span class="sxs-lookup"><span data-stu-id="c5d8e-120">Enable flow logs</span></span>
* <span data-ttu-id="c5d8e-121">Wyłącz dzienniki przepływu</span><span class="sxs-lookup"><span data-stu-id="c5d8e-121">Disable flow logs</span></span>
* <span data-ttu-id="c5d8e-122">Kwerenda o stan dzienniki przepływu</span><span class="sxs-lookup"><span data-stu-id="c5d8e-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c5d8e-123">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="c5d8e-123">Log in with ARMClient</span></span>

<span data-ttu-id="c5d8e-124">Zaloguj się do armclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="c5d8e-125">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="c5d8e-125">Register Insights provider</span></span>

<span data-ttu-id="c5d8e-126">Aby rejestrowanie działało poprawnie, przepływ **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-126">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="c5d8e-127">Jeśli nie masz pewności Jeśli **elemencie Microsoft.Insights** dostawca został zarejestrowany, uruchom następujący skrypt.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-127">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="c5d8e-128">Dzienniki przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="c5d8e-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="c5d8e-129">Polecenie, aby umożliwić przepływ dzienników przedstawiono w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c5d8e-129">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="c5d8e-130">Odpowiedź zwrócona z poprzedniego przykładu wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c5d8e-130">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="c5d8e-131">Dzienniki przepływu wyłączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="c5d8e-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="c5d8e-132">Skorzystaj z następującego przykładu, aby wyłączyć przepływ dzienników.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-132">Use the following example to disable flow logs.</span></span> <span data-ttu-id="c5d8e-133">Wywołanie jest taka sama jak Włączanie dzienników przepływu, z wyjątkiem **false** ustawiono dla właściwości włączone.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-133">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="c5d8e-134">Odpowiedź zwrócona z poprzedniego przykładu wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c5d8e-134">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="c5d8e-135">Dzienniki przepływu zapytań</span><span class="sxs-lookup"><span data-stu-id="c5d8e-135">Query flow logs</span></span>

<span data-ttu-id="c5d8e-136">Następujące kwerendy wywołania REST stan przepływu dzienniki na grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-136">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="c5d8e-137">Poniżej przedstawiono przykład odpowiedź zwrócona:</span><span class="sxs-lookup"><span data-stu-id="c5d8e-137">The following is an example of the response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="c5d8e-138">Pobierz dziennik przepływu</span><span class="sxs-lookup"><span data-stu-id="c5d8e-138">Download a flow log</span></span>

<span data-ttu-id="c5d8e-139">Lokalizacja magazynu dziennika przepływu jest definiowany podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c5d8e-139">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="c5d8e-140">Wygodne narzędzie dostępu do tych dzienników przepływu na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="c5d8e-140">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="c5d8e-141">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c5d8e-141">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="c5d8e-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5d8e-142">Next steps</span></span>

<span data-ttu-id="c5d8e-143">Dowiedz się, jak [wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="c5d8e-143">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="c5d8e-144">Dowiedz się, jak [wizualizacji NSG przepływu dzienników przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="c5d8e-144">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
