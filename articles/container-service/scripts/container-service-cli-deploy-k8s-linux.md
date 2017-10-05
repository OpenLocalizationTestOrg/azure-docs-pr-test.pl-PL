---
title: "Azure CLI skrypt przykładowy — Tworzenie klastra Kubernetes Linux ACS | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie klastra Kubernetes Linux ACS"
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
ms.openlocfilehash: 46bc37ab9949d070d19a3d8946fd5b00acf7f5d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="dda7a-104">Utwórz Kubernetes Linux klastrem usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dda7a-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="dda7a-105">W tym przykładzie powoduje utworzenie klastra usługi kontenera platformy Azure z systemem Kubernetes kontenerów opartymi na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="dda7a-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dda7a-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="dda7a-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="dda7a-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="dda7a-107">Clean up deployment</span></span> 

<span data-ttu-id="dda7a-108">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="dda7a-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dda7a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="dda7a-109">Script explanation</span></span>

<span data-ttu-id="dda7a-110">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="dda7a-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="dda7a-111">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="dda7a-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dda7a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="dda7a-112">Command</span></span> | <span data-ttu-id="dda7a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dda7a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dda7a-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="dda7a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dda7a-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="dda7a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dda7a-116">Utwórz acs az</span><span class="sxs-lookup"><span data-stu-id="dda7a-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="dda7a-117">Tworzy i klastrem usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="dda7a-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dda7a-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dda7a-118">Next steps</span></span>

<span data-ttu-id="dda7a-119">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dda7a-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dda7a-120">Dodatkowe przykłady skryptów wiersza polecenia usługi kontenera platformy Azure można znaleźć w [dokumentacji usługi kontenera platformy Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dda7a-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

