---
title: "aaaAzure CLI przykłady tooscale Azure bazy danych serwera MySQL | Dokumentacja firmy Microsoft"
description: "Ten przykładowy skrypt interfejsu wiersza polecenia skaluje bazy danych Azure na poziomie wydajności różnych tooa serwera MySQL po zapytań hello metryki."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a>Monitorowanie i skalowania bazy danych Azure programu MySQL serwera przy użyciu wiersza polecenia platformy Azure
Ten przykładowy skrypt interfejsu wiersza polecenia skaluje pojedynczej bazy danych Azure na poziomie wydajności różnych tooa serwera MySQL po zapytań hello metryki.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt
W ten przykładowy skrypt zmienić hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło. Zastąp identyfikator subskrypcji hello używane w poleceniach monitor az hello z identyfikatorem subskrypcji.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia
Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu
Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| **Polecenie** | **Uwagi** |
|---|---|
| [Tworzenie grupy az](/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [utworzenie przez serwer mysql az](/cli/azure/mysql/server#create) | Tworzy serwer MySQL obsługującego hello baz danych. |
| [Lista metryki monitor az](/cli/azure/monitor/metrics#list) | Wyświetl listę hello wartość metryki hello zasobów. |
| [Usuwanie grupy az](/cli/azure/group#delete) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki
- Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).
- Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](../sample-scripts-azure-cli.md)
- Aby uzyskać więcej informacji na temat skalowania, zobacz [warstwy usług](../concepts-service-tiers.md) i [obliczeniowe i Magazyn jednostek](../concepts-compute-unit-and-storage.md).
