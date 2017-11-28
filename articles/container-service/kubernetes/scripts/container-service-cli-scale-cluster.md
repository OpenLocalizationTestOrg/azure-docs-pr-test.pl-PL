---
title: "Azure CLI przykładowym skrypcie - skalowanie klastra usługi ACS | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - skalowanie klastra usługi ACS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 14e9f9d85bc0c1428240f15831632eafe2a0f80e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="d4ed0-104">Skalowanie klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ed0-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="d4ed0-105">Ten przykładowy skali i usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ed0-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d4ed0-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d4ed0-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="d4ed0-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d4ed0-107">Clean up deployment</span></span> 

<span data-ttu-id="d4ed0-108">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d4ed0-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d4ed0-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d4ed0-109">Script explanation</span></span>

<span data-ttu-id="d4ed0-110">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d4ed0-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="d4ed0-111">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d4ed0-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d4ed0-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d4ed0-112">Command</span></span> | <span data-ttu-id="d4ed0-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d4ed0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4ed0-114">AZ acs skali</span><span class="sxs-lookup"><span data-stu-id="d4ed0-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="d4ed0-115">Skalowanie klastra usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="d4ed0-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4ed0-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4ed0-116">Next steps</span></span>

<span data-ttu-id="d4ed0-117">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4ed0-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d4ed0-118">Dodatkowe przykłady skryptów wiersza polecenia usługi kontenera platformy Azure można znaleźć w [dokumentacji usługi kontenera platformy Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d4ed0-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

