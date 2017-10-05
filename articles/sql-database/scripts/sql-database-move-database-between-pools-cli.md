---
title: "Puli elastycznej bazy danych SQL Azure SQL przykład przenoszenia interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowy skrypt przenieść bazę danych SQL w puli elastycznej SQL"
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
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a>Użyj interfejsu wiersza polecenia, aby przenieść bazę danych Azure SQL w puli elastycznej SQL

Ten przykładowy skrypt wiersza polecenia platformy Azure tworzy dwie pule elastyczne i przenosi bazy danych Azure SQL z jednej puli elastycznej SQL do innej puli elastycznej SQL i przenosi bazy danych z puli elastycznej do poziomu wydajności pojedynczej bazy danych Azure. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "przeniesienie bazy danych między zestawami")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Utwórz az programu sql server](https://docs.microsoft.com/cli/azure/sql/server#create) | Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula. |
| [Utwórz sql az elastyczna pule](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Tworzy elastycznej puli w ramach serwera logicznego. |
| [Tworzenie bazy danych sql az](https://docs.microsoft.com/cli/azure/sql/db#create) | Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych. |
| [Aktualizacja bazy danych sql az](https://docs.microsoft.com/cli/azure/sql/db#update) | Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów bazy danych SQL interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure SQL Database](../sql-database-cli-samples.md).


