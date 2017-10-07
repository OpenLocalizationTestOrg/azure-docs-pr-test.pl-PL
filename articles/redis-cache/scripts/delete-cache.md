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
# <a name="delete-an-azure-redis-cache"></a>Usuń pamięć podręczna Azure Redis

W tym scenariuszu możesz dowiedzieć się, jak toodelete Azure pamięci podręcznej Redis.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toodelete wystąpienia pamięci podręcznej Redis Azure. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Usuń redis az](https://docs.microsoft.com/cli/azure/redis#delete) | Usuń wystąpienia pamięci podręcznej Redis. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).
