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
# <a name="delete-an-azure-redis-cache"></a>Usuń pamięć podręczna Azure Redis

W tym scenariuszu Dowiedz się jak usunąć pamięć podręczna Redis Azure.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[główne](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "pamięć podręczna Redis Azure")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń, można usunąć wystąpienia pamięci podręcznej Redis Azure. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Usuń redis az](https://docs.microsoft.com/cli/azure/redis#delete) | Usuń wystąpienia pamięci podręcznej Redis. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów w pamięci podręcznej Redis Azure CLI znajdują się w [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).