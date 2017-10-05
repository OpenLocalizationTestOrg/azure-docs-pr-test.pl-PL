---
title: "Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci z obserwatora sieciowego Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania przepływem grupy zabezpieczeń sieci dzienniki w Azure obserwatora sieciowego przy użyciu programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9fa2e2e1c09b119bd2a1e149fd2cc080957af296
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a><span data-ttu-id="f1f93-103">Konfigurowanie przepływu grupy zabezpieczeń sieci dzienników przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1f93-103">Configuring Network Security Group Flow logs with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f1f93-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f1f93-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="f1f93-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1f93-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="f1f93-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="f1f93-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="f1f93-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="f1f93-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="f1f93-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="f1f93-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="f1f93-109">Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który służy do wyświetlania informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="f1f93-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="f1f93-110">Te dzienniki przepływu są zapisywane w formacie json i Pokaż przepływów wychodzącego i przychodzącego na podstawie reguły w poszczególnych kart przepływ dotyczy 5-elementowej informacji o przepływie (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), i jeśli ruch został dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="f1f93-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="f1f93-111">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="f1f93-111">Register Insights provider</span></span>

<span data-ttu-id="f1f93-112">Aby rejestrowanie działało poprawnie, przepływ **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="f1f93-112">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="f1f93-113">Jeśli nie masz pewności Jeśli **elemencie Microsoft.Insights** dostawca został zarejestrowany, uruchom następujący skrypt.</span><span class="sxs-lookup"><span data-stu-id="f1f93-113">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="f1f93-114">Dzienniki przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="f1f93-114">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="f1f93-115">Polecenie, aby umożliwić przepływ dzienników przedstawiono w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="f1f93-115">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="f1f93-116">Dzienniki przepływu wyłączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="f1f93-116">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="f1f93-117">Skorzystaj z następującego przykładu, aby wyłączyć przepływ dzienników:</span><span class="sxs-lookup"><span data-stu-id="f1f93-117">Use the following example to disable flow logs:</span></span>

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="f1f93-118">Pobierz dziennik przepływu</span><span class="sxs-lookup"><span data-stu-id="f1f93-118">Download a Flow log</span></span>

<span data-ttu-id="f1f93-119">Lokalizacja magazynu dziennika przepływu jest definiowany podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="f1f93-119">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="f1f93-120">Wygodne narzędzie dostępu do tych dzienników przepływu na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="f1f93-120">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="f1f93-121">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="f1f93-121">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="f1f93-122">Informacje o strukturze dziennika można znaleźć [dziennika przepływu grupy zabezpieczeń sieci — omówienie](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f1f93-122">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1f93-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f1f93-123">Next Steps</span></span>

<span data-ttu-id="f1f93-124">Dowiedz się, jak [wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="f1f93-124">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="f1f93-125">Dowiedz się, jak [wizualizacji NSG przepływu dzienników przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="f1f93-125">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>