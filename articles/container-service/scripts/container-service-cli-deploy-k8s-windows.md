---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie klastra Kubernetes ACS systemu Windows | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie klastra Kubernetes ACS w systemie Windows"
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
ms.openlocfilehash: ace2f7a6dcd3ab02b61217766f4774cddbe8828b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a><span data-ttu-id="1d01f-104">Tworzenie klastra Kubernetes Windows usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d01f-104">Create an Azure Container Service Kubernetes Windows Cluster</span></span>

<span data-ttu-id="1d01f-105">W tym przykładzie powoduje utworzenie klastra usługi kontenera platformy Azure z systemem Kubernetes dla systemu Windows na podstawie kontenerów.</span><span class="sxs-lookup"><span data-stu-id="1d01f-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1d01f-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="1d01f-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys \
  --admin-username azureuser \
  --admin-password Password12 \
  --windows
```

## <a name="clean-up-deployment"></a><span data-ttu-id="1d01f-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="1d01f-107">Clean up deployment</span></span> 

<span data-ttu-id="1d01f-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="1d01f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1d01f-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="1d01f-109">Script explanation</span></span>

<span data-ttu-id="1d01f-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1d01f-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="1d01f-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1d01f-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1d01f-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="1d01f-112">Command</span></span> | <span data-ttu-id="1d01f-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1d01f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1d01f-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="1d01f-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1d01f-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="1d01f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1d01f-116">Utwórz acs az</span><span class="sxs-lookup"><span data-stu-id="1d01f-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="1d01f-117">Tworzy i klastrem usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="1d01f-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1d01f-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d01f-118">Next steps</span></span>

<span data-ttu-id="1d01f-119">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d01f-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1d01f-120">Dodatkowe przykłady skryptów wiersza polecenia usługi kontenera platformy Azure można znaleźć w hello [dokumentacji usługi kontenera platformy Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1d01f-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
