---
title: "puli elastycznej bazy danych SQL Azure SQL przenoszenia przykład aaaCLI | Dokumentacja firmy Microsoft"
description: "Przykład skryptu toomove bazy danych SQL w puli elastycznej SQL Azure CLI"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a>Użyj interfejsu wiersza polecenia toomove bazy danych Azure SQL w puli elastycznej SQL

Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy dwie pule elastyczne i przenosi bazy danych Azure SQL z jednej puli elastycznej SQL do innej puli elastycznej SQL i przenosi hello bazy danych poza poziom wydajności pojedynczej bazy danych Azure tooa puli elastycznej. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Utwórz az programu sql server](https://docs.microsoft.com/cli/azure/sql/server#create) | Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula. |
| [Utwórz sql az elastyczna pule](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Tworzy elastycznej puli w ramach powitania serwera logicznego. |
| [Tworzenie bazy danych sql az](https://docs.microsoft.com/cli/azure/sql/db#create) | Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych. |
| [Aktualizacja bazy danych sql az](https://docs.microsoft.com/cli/azure/sql/db#update) | Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).


