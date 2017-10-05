---
title: "Azure CLI skrypt przykładowy — tworzenie podręczna Redis Azure Premium z usługą klastrowania | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie warstwy Premium usługi pamięć podręczna Redis Azure z usługą klastrowania"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="fbe1c-103">Utwórz podręczna Redis Azure Premium z klastra</span><span class="sxs-lookup"><span data-stu-id="fbe1c-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="fbe1c-104">W tym scenariuszu możesz dowiedzieć się, jak utworzyć warstwy Premium 6 GB pamięci podręcznej Redis Azure z włączoną funkcją klastrowania i dwa niezależne.</span><span class="sxs-lookup"><span data-stu-id="fbe1c-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="fbe1c-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="fbe1c-105">Sample script</span></span>

<span data-ttu-id="fbe1c-106">[!code-azurecli[główne](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "pamięć podręczna Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="fbe1c-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fbe1c-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="fbe1c-107">Script explanation</span></span>

<span data-ttu-id="fbe1c-108">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów i pamięć podręczna redis warstwy Premium z usługą klastrowania Włącz.</span><span class="sxs-lookup"><span data-stu-id="fbe1c-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="fbe1c-109">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fbe1c-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fbe1c-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="fbe1c-110">Command</span></span> | <span data-ttu-id="fbe1c-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fbe1c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fbe1c-112">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="fbe1c-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fbe1c-113">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="fbe1c-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fbe1c-114">Tworzenie pamięci podręcznej redis az</span><span class="sxs-lookup"><span data-stu-id="fbe1c-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="fbe1c-115">Tworzenie wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="fbe1c-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fbe1c-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbe1c-116">Next steps</span></span>

<span data-ttu-id="fbe1c-117">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbe1c-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fbe1c-118">Dodatkowe przykłady skryptów w pamięci podręcznej Redis Azure CLI znajdują się w [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fbe1c-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>