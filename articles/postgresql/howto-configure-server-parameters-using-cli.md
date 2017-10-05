---
title: "Skonfiguruj parametry usługi w bazie danych Azure dla PostgreSQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak skonfigurować parametry usługi w bazie danych Azure dla PostgreSQL przy użyciu wiersza polecenia wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Dostosuj parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure
Można wyświetlić listę, wyświetlić i zaktualizować parametry konfiguracji serwera Azure PostgreSQL przy użyciu interfejsu wiersza polecenia (Azure CLI). Jednak tylko podzbiór aparatu konfiguracji są narażone na poziomie serwera i może być modyfikowany. 

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków opisanych ten przewodnik, potrzebne są:
- Serwer i bazę danych [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) narzędzia wiersza polecenia lub użyć powłoki chmury Azure w przeglądarce.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Lista parametrów konfiguracji serwera dla bazy danych Azure PostgreSQL serwera
Aby wyświetlić listę wszystkich parametrów można modyfikować w serwerze i ich wartości, należy uruchomić [az postgres serwera konfiguracji na liście](/cli/azure/postgres/server/configuration#list) polecenia.

Można wyświetlić parametry konfiguracji serwera dla serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Pokaż szczegóły parametru konfiguracji serwera
Aby wyświetlić szczegółowe informacje dotyczące parametru określoną konfigurację serwera, uruchom [az postgres serwera konfiguracji Pokaż](/cli/azure/postgres/server/configuration#show) polecenia.

W tym przykładzie przedstawiono szczegóły **dziennika\_min\_wiadomości** parametru konfiguracji serwera dla serwera **mypgserver 20170401.postgres.database.azure.com** w obszarze Grupa zasobów **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Zmodyfikuj wartość parametru konfiguracji serwera
Można również zmodyfikować wartość niektórych parametru konfiguracji serwera i spowoduje to zaktualizowanie odpowiednia wartość konfiguracji dla aparatu serwera PostgreSQL. Aby zaktualizować Użyj konfiguracji [zestawu konfiguracji serwera postgres az](/cli/azure/postgres/server/configuration#set) polecenia. 

Aby zaktualizować **dziennika\_min\_wiadomości** parametru konfiguracji serwera serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Jeśli chcesz zresetować wartość parametru konfiguracji, po prostu chcesz Opuść opcjonalny `--value` parametr i usługi będą stosowane wartości domyślnej. W powyżej przykład jego wygląd:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Spowoduje to zresetowanie **dziennika\_min\_wiadomości** konfiguracji przy użyciu wartości domyślnej **ostrzeżenie**. Aby uzyskać szczegółowe informacje o konfiguracji serwera i dopuszczalne wartości, zobacz dokumentację PostgreSQL [konfiguracji serwera](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Następne kroki
- Aby skonfigurować i uzyskać dostępu do dzienników serwera, zobacz [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)
