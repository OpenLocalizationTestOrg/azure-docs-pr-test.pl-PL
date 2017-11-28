---
title: "Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci z obserwatora sieciowego Azure - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania przepływem grupy zabezpieczeń sieci dzienniki w obserwatora sieciowego Azure z wiersza polecenia platformy Azure"
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
ms.openlocfilehash: d5a8aa0cd274132798a0d8484a950926761dae7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="a2dcd-103">Konfigurowanie dzienników przepływu grupy zabezpieczeń sieci przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a2dcd-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a2dcd-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2dcd-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="a2dcd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2dcd-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="a2dcd-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="a2dcd-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="a2dcd-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="a2dcd-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="a2dcd-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="a2dcd-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="a2dcd-109">Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który służy do wyświetlania informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="a2dcd-110">Te dzienniki przepływu są zapisywane w formacie json i Pokaż przepływów wychodzącego i przychodzącego na podstawie reguły w poszczególnych kart przepływ dotyczy 5-elementowej informacji o przepływie (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), i jeśli ruch został dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="a2dcd-111">W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania zarządzania zasobów, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="a2dcd-112">Aby wykonać kroki opisane w tym artykule, należy [instalowanie interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a2dcd-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="a2dcd-113">Zarejestruj dostawcę usługi Insights</span><span class="sxs-lookup"><span data-stu-id="a2dcd-113">Register Insights provider</span></span>

<span data-ttu-id="a2dcd-114">Aby rejestrowanie działało poprawnie, przepływ **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="a2dcd-115">Jeśli nie masz pewności Jeśli **elemencie Microsoft.Insights** dostawca został zarejestrowany, uruchom następujący skrypt.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="a2dcd-116">Dzienniki przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="a2dcd-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="a2dcd-117">Polecenie, aby umożliwić przepływ dzienników przedstawiono w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a2dcd-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="a2dcd-118">Dzienniki przepływu wyłączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="a2dcd-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="a2dcd-119">Skorzystaj z następującego przykładu, aby wyłączyć przepływ dzienników:</span><span class="sxs-lookup"><span data-stu-id="a2dcd-119">Use the following example to disable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="a2dcd-120">Pobierz dziennik przepływu</span><span class="sxs-lookup"><span data-stu-id="a2dcd-120">Download a Flow log</span></span>

<span data-ttu-id="a2dcd-121">Lokalizacja magazynu dziennika przepływu jest definiowany podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="a2dcd-122">Wygodne narzędzie dostępu do tych dzienników przepływu na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="a2dcd-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="a2dcd-123">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="a2dcd-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="a2dcd-124">Informacje o strukturze dziennika można znaleźć [dziennika przepływu grupy zabezpieczeń sieci — omówienie](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a2dcd-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2dcd-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2dcd-125">Next Steps</span></span>

<span data-ttu-id="a2dcd-126">Dowiedz się, jak [wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="a2dcd-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="a2dcd-127">Dowiedz się, jak [wizualizacji NSG przepływu dzienników przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="a2dcd-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
