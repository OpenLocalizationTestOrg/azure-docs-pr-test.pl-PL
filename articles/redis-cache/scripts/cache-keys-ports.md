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
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Pobierz hello nazwy hosta, portów i klucze dla pamięci podręcznej Redis Azure

W tym scenariuszu dowiesz się używania wystąpienia pamięci podręcznej Redis Azure tooan tooconnect tooretrieve hello hostname, portów i kluczy.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia tooretrieve hello hostname, klucze i porty wystąpienia pamięci podręcznej Redis Azure. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Pokaż redis az](https://docs.microsoft.com/cli/azure/redis#show) | Pobieranie szczegółów wystąpienia pamięci podręcznej Redis Azure. |
| [klucze listy az redis](https://docs.microsoft.com/cli/azure/redis#list-keys) | Pobrać klucze dostępu dla wystąpienia pamięci podręcznej Redis Azure. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów interfejsu wiersza polecenia pamięci podręcznej Redis Azure można znaleźć w hello [dokumentacji pamięć podręczna Redis Azure](../cli-samples.md).
