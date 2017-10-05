---
title: "Przykładowy skrypt Azure CLI — Usuń pamięć podręczna Azure Redis | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt Azure CLI — Usuń pamięć podręczna Azure Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="c67b5-103">Usuń pamięć podręczna Azure Redis</span><span class="sxs-lookup"><span data-stu-id="c67b5-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="c67b5-104">W tym scenariuszu Dowiedz się jak usunąć pamięć podręczna Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="c67b5-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="c67b5-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c67b5-105">Sample script</span></span>

<span data-ttu-id="c67b5-106">[!code-azurecli[główne](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "pamięć podręczna Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="c67b5-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c67b5-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c67b5-107">Script explanation</span></span>

<span data-ttu-id="c67b5-108">Ten skrypt używa następujących poleceń, można usunąć wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="c67b5-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="c67b5-109">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c67b5-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c67b5-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c67b5-110">Command</span></span> | <span data-ttu-id="c67b5-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c67b5-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c67b5-112">Usuń redis az</span><span class="sxs-lookup"><span data-stu-id="c67b5-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="c67b5-113">Usuń wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="c67b5-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c67b5-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c67b5-114">Next steps</span></span>

<span data-ttu-id="c67b5-115">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c67b5-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c67b5-116">Dodatkowe przykłady skryptów w pamięci podręcznej Redis Azure CLI znajdują się w [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c67b5-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>