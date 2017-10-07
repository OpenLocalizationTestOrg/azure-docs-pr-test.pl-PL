---
title: "aaaAzure konta skryptu interfejsu wiersza polecenia Get kluczy dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - Get klucze konta dla bazy danych Azure rozwiązania Cosmos"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: d6462b3eebc8bc6935a6fa07dcae37a33e5f382e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-hello-azure-cli"></a>Uzyskaj klucze konta dla bazy danych rozwiązania Cosmos Azure przy użyciu hello Azure CLI

W tym przykładzie pobiera klucze konta dla każdego typu konta bazy danych Azure rozwiązania Cosmos.  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "Get Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [AZ cosmosdb aktualizacji](https://docs.microsoft.com/cli/azure/cosmosdb#update) | Aktualizuje konto bazy danych Azure rozwiązania Cosmos. |
| [AZ cosmosdb listy kluczy](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | Tworzy serwer logiczny, że hosty hello bazy danych SQL. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/group#delete) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów wiersza polecenia platformy Azure rozwiązania Cosmos bazy danych można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure rozwiązania Cosmos DB](../cli-samples.md).
