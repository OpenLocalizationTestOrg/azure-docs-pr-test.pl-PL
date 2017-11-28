---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie podręczna Redis Azure Premium z usługą klastrowania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="7d621-103">Utwórz podręczna Redis Azure Premium z klastra</span><span class="sxs-lookup"><span data-stu-id="7d621-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="7d621-104">W tym scenariuszu możesz dowiedzieć się, jak toocreate warstwy Premium 6 GB pamięci podręcznej Redis Azure z usługą klastrowania włączona i dwa niezależne.</span><span class="sxs-lookup"><span data-stu-id="7d621-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="7d621-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7d621-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7d621-106">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7d621-106">Script explanation</span></span>

<span data-ttu-id="7d621-107">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów i pamięć podręczna redis warstwy Premium z usługą klastrowania Włącz.</span><span class="sxs-lookup"><span data-stu-id="7d621-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="7d621-108">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="7d621-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7d621-109">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7d621-109">Command</span></span> | <span data-ttu-id="7d621-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7d621-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7d621-111">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="7d621-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7d621-112">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="7d621-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7d621-113">Tworzenie pamięci podręcznej redis az</span><span class="sxs-lookup"><span data-stu-id="7d621-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="7d621-114">Tworzenie wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="7d621-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="7d621-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d621-115">Next steps</span></span>

<span data-ttu-id="7d621-116">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d621-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7d621-117">Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7d621-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
