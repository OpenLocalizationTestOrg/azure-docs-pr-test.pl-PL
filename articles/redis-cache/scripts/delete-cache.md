---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Usuń pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="f6515-103">Usuń pamięć podręczna Azure Redis</span><span class="sxs-lookup"><span data-stu-id="f6515-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="f6515-104">W tym scenariuszu możesz dowiedzieć się, jak toodelete Azure pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="f6515-104">In this scenario, you learn how toodelete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f6515-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f6515-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f6515-106">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f6515-106">Script explanation</span></span>

<span data-ttu-id="f6515-107">Ten skrypt używa hello następujące polecenia toodelete wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="f6515-107">This script uses hello following commands toodelete an Azure Redis Cache instance.</span></span> <span data-ttu-id="f6515-108">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f6515-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f6515-109">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f6515-109">Command</span></span> | <span data-ttu-id="f6515-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6515-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6515-111">Usuń redis az</span><span class="sxs-lookup"><span data-stu-id="f6515-111">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="f6515-112">Usuń wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="f6515-112">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f6515-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6515-113">Next steps</span></span>

<span data-ttu-id="f6515-114">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6515-114">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f6515-115">Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f6515-115">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
