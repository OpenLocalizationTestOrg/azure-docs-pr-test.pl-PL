---
title: "Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci z obserwatora sieciowego Azure - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania przepływem grupy zabezpieczeń sieci dzienniki w obserwatora sieciowego Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0"
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
ms.openlocfilehash: 2ea8543857c062e76f96da99fb295ce831c3c5f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="b1df1-103">Konfigurowanie dzienniki przepływu grupy zabezpieczeń sieci przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="b1df1-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b1df1-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b1df1-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="b1df1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1df1-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="b1df1-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="b1df1-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="b1df1-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="b1df1-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="b1df1-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="b1df1-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="b1df1-109">Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który służy do wyświetlania informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="b1df1-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="b1df1-110">Te dzienniki przepływu są zapisywane w formacie json i Pokaż przepływów wychodzącego i przychodzącego na podstawie reguły w poszczególnych kart przepływ dotyczy 5-elementowej informacji o przepływie (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), i jeśli ruch został dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="b1df1-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="b1df1-111">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="b1df1-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="b1df1-112">Obserwatora sieciowego aktualnie używa interfejsu wiersza polecenia platformy Azure w wersji 1.0 do obsługi interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b1df1-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="b1df1-113">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="b1df1-113">Register Insights provider</span></span>

<span data-ttu-id="b1df1-114">Aby rejestrowanie działało poprawnie, przepływ **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="b1df1-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="b1df1-115">Jeśli nie masz pewności Jeśli **elemencie Microsoft.Insights** dostawca został zarejestrowany, uruchom następujący skrypt.</span><span class="sxs-lookup"><span data-stu-id="b1df1-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="b1df1-116">Dzienniki przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="b1df1-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="b1df1-117">Polecenie, aby umożliwić przepływ dzienników przedstawiono w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b1df1-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="b1df1-118">Dzienniki przepływu wyłączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="b1df1-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="b1df1-119">Skorzystaj z następującego przykładu, aby wyłączyć przepływ dzienników:</span><span class="sxs-lookup"><span data-stu-id="b1df1-119">Use the following example to disable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="b1df1-120">Pobierz dziennik przepływu</span><span class="sxs-lookup"><span data-stu-id="b1df1-120">Download a Flow log</span></span>

<span data-ttu-id="b1df1-121">Lokalizacja magazynu dziennika przepływu jest definiowany podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="b1df1-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="b1df1-122">Wygodne narzędzie dostępu do tych dzienników przepływu na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="b1df1-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="b1df1-123">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="b1df1-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="b1df1-124">Informacje o strukturze dziennika można znaleźć [dziennika przepływu grupy zabezpieczeń sieci — omówienie](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b1df1-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1df1-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1df1-125">Next Steps</span></span>

<span data-ttu-id="b1df1-126">Dowiedz się, jak [wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="b1df1-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="b1df1-127">Dowiedz się, jak [wizualizacji NSG przepływu dzienników przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="b1df1-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
