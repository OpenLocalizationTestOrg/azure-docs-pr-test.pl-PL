---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - Get hello nazwy hosta, portów i klucze dla pamięci podręcznej Redis Azure | Dokumentacja firmy Microsoft"
description: "Azure przykładowym skrypcie interfejsu wiersza polecenia - Get hello hostname, porty i klucze dla wystąpienia pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="b7aba-103">Pobierz hello nazwy hosta, portów i klucze dla pamięci podręcznej Redis Azure</span><span class="sxs-lookup"><span data-stu-id="b7aba-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="b7aba-104">W tym scenariuszu dowiesz się używania wystąpienia pamięci podręcznej Redis Azure tooan tooconnect tooretrieve hello hostname, portów i kluczy.</span><span class="sxs-lookup"><span data-stu-id="b7aba-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b7aba-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b7aba-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="b7aba-106">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b7aba-106">Script explanation</span></span>

<span data-ttu-id="b7aba-107">Ten skrypt używa hello następujące polecenia tooretrieve hello hostname, klucze i porty wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="b7aba-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="b7aba-108">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b7aba-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b7aba-109">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b7aba-109">Command</span></span> | <span data-ttu-id="b7aba-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b7aba-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b7aba-111">Pokaż redis az</span><span class="sxs-lookup"><span data-stu-id="b7aba-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="b7aba-112">Pobieranie szczegółów wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="b7aba-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="b7aba-113">klucze listy az redis</span><span class="sxs-lookup"><span data-stu-id="b7aba-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="b7aba-114">Pobrać klucze dostępu dla wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="b7aba-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b7aba-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7aba-115">Next steps</span></span>

<span data-ttu-id="b7aba-116">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7aba-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b7aba-117">Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b7aba-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
