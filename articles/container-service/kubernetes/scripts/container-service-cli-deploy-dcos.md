---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie klastra DC/OS ACS | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie klastra ACS DC/OS"
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
ms.openlocfilehash: cbc990e5e650487d6aa4572c7ff5e1c3fa150906
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="6e684-104">Tworzenie klastra DC/OS usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6e684-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="6e684-105">W tym przykładzie powoduje utworzenie klastra usługi kontenera platformy Azure z systemem DCOS.</span><span class="sxs-lookup"><span data-stu-id="6e684-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6e684-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6e684-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="6e684-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6e684-107">Clean up deployment</span></span> 

<span data-ttu-id="6e684-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6e684-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6e684-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6e684-109">Script explanation</span></span>

<span data-ttu-id="6e684-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6e684-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="6e684-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="6e684-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6e684-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6e684-112">Command</span></span> | <span data-ttu-id="6e684-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6e684-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6e684-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6e684-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6e684-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6e684-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6e684-116">Utwórz acs az</span><span class="sxs-lookup"><span data-stu-id="6e684-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="6e684-117">Tworzy i klastrem usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="6e684-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e684-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e684-118">Next steps</span></span>

<span data-ttu-id="6e684-119">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e684-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6e684-120">Dodatkowe przykłady skryptów wiersza polecenia usługi kontenera platformy Azure można znaleźć w hello [dokumentacji usługi kontenera platformy Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6e684-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
