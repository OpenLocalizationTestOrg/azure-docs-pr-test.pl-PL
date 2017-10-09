---
title: AAA "Azure CLI Azure skali skryptu bazy danych PostgreSQL | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie usługi Azure CLI - bazą danych Azure skalowania dla poziom wydajności różnych tooa PostgreSQL serwera po zapytań hello metryki."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Monitorowanie i skalować pojedynczy serwer PostgreSQL przy użyciu wiersza polecenia platformy Azure
Ten przykładowy skrypt CLI skaluje pojedynczej bazy danych Azure na poziomie wydajności różnych tooa serwera PostgreSQL po zapytań hello metryki. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt
W ten przykładowy skrypt zmienić hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło. Zastąp identyfikator subskrypcji hello używane w poleceniach monitor az hello z identyfikatorem subskrypcji.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia
Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu
Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| **Polecenie** | **Uwagi** |
|---|---|
| [Tworzenie grupy az](/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [utworzenie przez serwer postgres az](/cli/azure/postgres/server#create) | Tworzy serwer PostgreSQL obsługującego hello baz danych. |
| [Lista metryki monitor az](/cli/azure/monitor/metrics#list) | Wyświetl listę hello wartość metryki hello zasobów. |
| [Usuwanie grupy az](/cli/azure/group#delete) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki
- Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview)
- Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla PostgreSQL](../sample-scripts-azure-cli.md)
- Przeczytaj więcej na temat skalowania: [warstwy usług](../concepts-service-tiers.md) i [obliczeniowe i jednostek magazynu](../concepts-compute-unit-and-storage.md)
