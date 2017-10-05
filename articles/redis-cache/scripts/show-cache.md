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
# <a name="get-details-of-an-azure-redis-cache"></a>Uzyskiwanie szczegółowych informacji o pamięci podręcznej Redis Azure

W tym scenariuszu należy dowiedzieć się, jak można pobrać szczegółów wystąpienia pamięci podręcznej Redis Azure, takich jak jej stan inicjowania obsługi administracyjnej.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[główne](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "pamięć podręczna Redis Azure")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt można pobrać szczegółów wystąpienia pamięci podręcznej Redis Azure korzysta z następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Pokaż redis az](https://docs.microsoft.com/cli/azure/redis#show) | Pobieranie szczegółów wystąpienia pamięci podręcznej Redis Azure. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów w pamięci podręcznej Redis Azure CLI znajdują się w [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).