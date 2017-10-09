---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie pamięci podręcznej Redis Azure | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie pamięci podręcznej Azure Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="262d5-103">Tworzenie usługi Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="262d5-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="262d5-104">W tym scenariuszu możesz dowiedzieć się, jak toocreate Azure pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="262d5-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="262d5-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="262d5-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="262d5-106">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="262d5-106">Script explanation</span></span>

<span data-ttu-id="262d5-107">Ten skrypt używa hello następujące polecenia toocreate grupy zasobów i pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="262d5-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="262d5-108">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="262d5-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="262d5-109">Polecenie</span><span class="sxs-lookup"><span data-stu-id="262d5-109">Command</span></span> | <span data-ttu-id="262d5-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="262d5-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="262d5-111">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="262d5-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="262d5-112">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="262d5-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="262d5-113">Tworzenie pamięci podręcznej redis az</span><span class="sxs-lookup"><span data-stu-id="262d5-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="262d5-114">Tworzenie wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="262d5-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="262d5-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="262d5-115">Next steps</span></span>

<span data-ttu-id="262d5-116">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="262d5-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="262d5-117">Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="262d5-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
