---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - skalować klastra usługi ACS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="392b4-104">Skalowanie klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="392b4-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="392b4-105">Ten przykładowy skali i usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="392b4-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="392b4-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="392b4-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="392b4-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="392b4-107">Clean up deployment</span></span> 

<span data-ttu-id="392b4-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="392b4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="392b4-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="392b4-109">Script explanation</span></span>

<span data-ttu-id="392b4-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="392b4-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="392b4-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="392b4-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="392b4-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="392b4-112">Command</span></span> | <span data-ttu-id="392b4-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="392b4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="392b4-114">AZ acs skali</span><span class="sxs-lookup"><span data-stu-id="392b4-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="392b4-115">Skalowanie klastra usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="392b4-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="392b4-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="392b4-116">Next steps</span></span>

<span data-ttu-id="392b4-117">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="392b4-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="392b4-118">Dodatkowe przykłady skryptów wiersza polecenia usługi kontenera platformy Azure można znaleźć w hello [dokumentacji usługi kontenera platformy Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="392b4-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

