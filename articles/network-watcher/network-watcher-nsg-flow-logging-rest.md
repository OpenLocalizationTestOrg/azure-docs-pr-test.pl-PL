---
title: "rejestruje aaaManage przepływu sieciową grupę zabezpieczeń z obserwatora sieciowego Azure - interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono sposób rejestrowania toomanage przepływu sieciowej grupy zabezpieczeń w obserwatora sieciowego Azure z interfejsu API REST"
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
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="99e42-103">Konfigurowanie grup zabezpieczeń sieci przepływu dzienników przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="99e42-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="99e42-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="99e42-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="99e42-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99e42-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="99e42-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="99e42-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="99e42-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="99e42-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="99e42-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="99e42-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="99e42-109">Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który pozwala tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="99e42-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="99e42-110">Te dzienniki przepływu są zapisywane w formacie json i Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart stosuje, 5-elementowej informacji o przepływie hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), a jeśli hello ruchu jest dozwolone, lub Odmowa dostępu.</span><span class="sxs-lookup"><span data-stu-id="99e42-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="99e42-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="99e42-111">Before you begin</span></span>

<span data-ttu-id="99e42-112">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99e42-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="99e42-113">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="99e42-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="99e42-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="99e42-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="99e42-115">Dla interfejsu API REST obserwatora sieciowego wywołania hello Nazwa grupy zasobów w żądaniu hello się, że identyfikator URI jest hello grupę zasobów, która zawiera hello obserwatora sieciowego nie zasoby hello czynności diagnostyczne hello są wykonywane na.</span><span class="sxs-lookup"><span data-stu-id="99e42-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="99e42-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="99e42-116">Scenario</span></span>

<span data-ttu-id="99e42-117">Scenariusz Hello omówione w tym artykule przedstawiono sposób tooenable, wyłącz i zapytania przepływu dzienników przy użyciu interfejsu API REST hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="99e42-118">toolearn więcej informacji na temat loggings przepływu sieciowej grupy zabezpieczeń, odwiedź stronę [rejestrowania przepływu grupy zabezpieczeń sieci — omówienie](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99e42-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="99e42-119">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="99e42-119">In this scenario, you will:</span></span>

* <span data-ttu-id="99e42-120">Włączanie dzienników przepływu</span><span class="sxs-lookup"><span data-stu-id="99e42-120">Enable flow logs</span></span>
* <span data-ttu-id="99e42-121">Wyłącz dzienniki przepływu</span><span class="sxs-lookup"><span data-stu-id="99e42-121">Disable flow logs</span></span>
* <span data-ttu-id="99e42-122">Kwerenda o stan dzienniki przepływu</span><span class="sxs-lookup"><span data-stu-id="99e42-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="99e42-123">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="99e42-123">Log in with ARMClient</span></span>

<span data-ttu-id="99e42-124">Zaloguj się za tooarmclient przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="99e42-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="99e42-125">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="99e42-125">Register Insights provider</span></span>

<span data-ttu-id="99e42-126">Aby przepływ hello pomyślnie, rejestrowanie toowork **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="99e42-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="99e42-127">Jeśli nie masz pewności, czy hello **elemencie Microsoft.Insights** dostawca jest zarejestrowany, uruchom hello poniższy skrypt.</span><span class="sxs-lookup"><span data-stu-id="99e42-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="99e42-128">Dzienniki przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="99e42-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="99e42-129">Dzienniki przepływu tooenable polecenia Hello jest pokazywana w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="99e42-129">hello command tooenable flow logs is shown in hello following example:</span></span>

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

<span data-ttu-id="99e42-130">zwrócił odpowiedź Hello hello w poprzednim przykładzie jest następujący:</span><span class="sxs-lookup"><span data-stu-id="99e42-130">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="99e42-131">Dzienniki przepływu wyłączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="99e42-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="99e42-132">Rejestruje hello Użyj następującego przepływu toodisable przykład.</span><span class="sxs-lookup"><span data-stu-id="99e42-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="99e42-133">Witaj wywołanie jest hello samo co włączenie dzienników przepływu, z wyjątkiem **false** ustawiono dla właściwości hello włączone.</span><span class="sxs-lookup"><span data-stu-id="99e42-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

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

<span data-ttu-id="99e42-134">zwrócił odpowiedź Hello hello w poprzednim przykładzie jest następujący:</span><span class="sxs-lookup"><span data-stu-id="99e42-134">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="99e42-135">Dzienniki przepływu zapytań</span><span class="sxs-lookup"><span data-stu-id="99e42-135">Query flow logs</span></span>

<span data-ttu-id="99e42-136">powitania po wywołania REST zapytania hello stan przepływu dzienniki na grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="99e42-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="99e42-137">Hello poniżej przedstawiono przykład zwrócił odpowiedź hello:</span><span class="sxs-lookup"><span data-stu-id="99e42-137">hello following is an example of hello response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="99e42-138">Pobierz dziennik przepływu</span><span class="sxs-lookup"><span data-stu-id="99e42-138">Download a flow log</span></span>

<span data-ttu-id="99e42-139">Witaj lokalizacji magazynu dziennika przepływu jest definiowany podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="99e42-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="99e42-140">Tooaccess wygodne narzędzie, te konta magazynu tooa Dzienniki zapisane przepływu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="99e42-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="99e42-141">Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="99e42-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="99e42-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99e42-142">Next steps</span></span>

<span data-ttu-id="99e42-143">Dowiedz się, jak za[wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="99e42-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="99e42-144">Dowiedz się, jak za[wizualizacji NSG przepływu dzienników przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="99e42-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
