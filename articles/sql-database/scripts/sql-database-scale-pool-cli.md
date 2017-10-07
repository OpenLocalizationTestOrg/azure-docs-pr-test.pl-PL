---
title: "przykład aaaCLI skaluje elastycznej puli Azure SQL bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowy skrypt tooscale puli elastycznej SQL w bazie danych SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a>Użyj interfejsu wiersza polecenia tooscale puli elastycznej SQL w bazie danych SQL Azure

Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy pule elastyczne SQL, przenosi puli baz danych, a następnie zmienia poziomy wydajności puli elastycznej. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, serwera logicznego bazy danych SQL i reguły zapory. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Utwórz az programu sql server](https://docs.microsoft.com/cli/azure/sql/server#create) | Tworzy serwer logiczny, że hosty hello bazy danych SQL. |
| [Utwórz sql az elastyczna pule](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Tworzy elastycznej puli baz danych w ramach powitania serwera logicznego. |
| [Tworzenie bazy danych sql az](https://docs.microsoft.com/cli/azure/sql/db#create) | Tworzy hello bazy danych SQL w powitania serwera logicznego. |
| [Aktualizacja pule elastyczne sql az](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | Aktualizuje elastycznej puli baz danych, w tym hello zmiany przykład przypisane eDTU. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).
