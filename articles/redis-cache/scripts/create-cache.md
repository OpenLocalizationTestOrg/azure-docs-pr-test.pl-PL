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
# <a name="create-an-azure-redis-cache"></a>Tworzenie usługi Azure Redis Cache

W tym scenariuszu możesz dowiedzieć się, jak toocreate Azure pamięci podręcznej Redis.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupy zasobów i pamięci podręcznej redis. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/cli/azure/redis#create) | Tworzenie wystąpienia pamięci podręcznej Redis. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).
