---
title: "Azure CLI przykładowym skrypcie — pobranie szczegółów pamięci podręcznej Redis Azure | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie — pobranie szczegółów pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="7c559-103">Uzyskiwanie szczegółowych informacji o pamięci podręcznej Redis Azure</span><span class="sxs-lookup"><span data-stu-id="7c559-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="7c559-104">W tym scenariuszu należy dowiedzieć się, jak można pobrać szczegółów wystąpienia pamięci podręcznej Redis Azure, takich jak jej stan inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7c559-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="7c559-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7c559-105">Sample script</span></span>

<span data-ttu-id="7c559-106">[!code-azurecli[główne](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "pamięć podręczna Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="7c559-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="7c559-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7c559-107">Script explanation</span></span>

<span data-ttu-id="7c559-108">Ten skrypt można pobrać szczegółów wystąpienia pamięci podręcznej Redis Azure korzysta z następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="7c559-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="7c559-109">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7c559-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7c559-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7c559-110">Command</span></span> | <span data-ttu-id="7c559-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7c559-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c559-112">Pokaż redis az</span><span class="sxs-lookup"><span data-stu-id="7c559-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="7c559-113">Pobieranie szczegółów wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="7c559-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="7c559-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c559-114">Next steps</span></span>

<span data-ttu-id="7c559-115">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c559-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7c559-116">Dodatkowe przykłady skryptów w pamięci podręcznej Redis Azure CLI znajdują się w [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c559-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>