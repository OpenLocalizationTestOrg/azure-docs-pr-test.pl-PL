---
title: "AAA \"Azure CLI skryptu — tworzenie bazy danych platformy Azure dla programu MySQL | Dokumentacja firmy Microsoft\""
description: "Ten przykładowy skrypt interfejsu wiersza polecenia Azure bazy danych serwera MySQL tworzy i konfiguruje regułę zapory poziomu serwera."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Utwórz serwer MySQL i skonfigurować regułę zapory przy użyciu hello wiersza polecenia platformy Azure
Ten przykładowy skrypt interfejsu wiersza polecenia Azure bazy danych serwera MySQL tworzy i konfiguruje regułę zapory poziomu serwera. Po pomyślnym uruchomieniu skryptu hello hello MySQL serwer jest dostępny dla wszystkich usług platformy Azure i hello skonfigurowany adres IP.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt
W ten przykładowy skrypt edytować hello wyróżnione wiersze toocustomize hello admin użytkownika i hasło.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia
Po uruchomieniu przykładowym skrypcie hello hello następujące polecenie może być grupa zasobów hello tooremove używane i wszystkie zasoby skojarzone z nim.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu
Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| **Polecenie** | **Uwagi** |
|---|---|
| [Tworzenie grupy az](/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [utworzenie przez serwer mysql az](/cli/azure/mysql/server#create) | Tworzy serwer MySQL obsługującego hello baz danych. |
| [Utwórz az mysql Serwer zapory](/cli/azure/mysql/server/firewall-rule#create) | Tworzy serwer toohello dostępu tooallow reguły zapory i baz danych z zakresu adresów IP hello wprowadzona. |
| [Usuwanie grupy az](/cli/azure/group#delete) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki
- Przeczytaj więcej informacji na temat hello Azure CLI: [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).
- Spróbuj dodatkowych skryptów: [przykłady wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](../sample-scripts-azure-cli.md)
