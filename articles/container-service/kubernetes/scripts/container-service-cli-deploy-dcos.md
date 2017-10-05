---
title: "Azure CLI skrypt przykładowy — Tworzenie klastra usługi ACS DC/OS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ff90aee308a993ae0d36288191d1496affacce2a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="2db36-104">Tworzenie klastra DC/OS usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2db36-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="2db36-105">W tym przykładzie powoduje utworzenie klastra usługi kontenera platformy Azure z systemem DCOS.</span><span class="sxs-lookup"><span data-stu-id="2db36-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2db36-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="2db36-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="2db36-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="2db36-107">Clean up deployment</span></span> 

<span data-ttu-id="2db36-108">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="2db36-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2db36-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="2db36-109">Script explanation</span></span>

<span data-ttu-id="2db36-110">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2db36-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="2db36-111">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="2db36-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2db36-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="2db36-112">Command</span></span> | <span data-ttu-id="2db36-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2db36-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2db36-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="2db36-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2db36-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="2db36-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2db36-116">Utwórz acs az</span><span class="sxs-lookup"><span data-stu-id="2db36-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="2db36-117">Tworzy i klastrem usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="2db36-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2db36-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2db36-118">Next steps</span></span>

<span data-ttu-id="2db36-119">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2db36-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2db36-120">Dodatkowe przykłady skryptów wiersza polecenia usługi kontenera platformy Azure można znaleźć w [dokumentacji usługi kontenera platformy Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2db36-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>