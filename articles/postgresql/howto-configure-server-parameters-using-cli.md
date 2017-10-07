---
title: "Parametry usługi hello aaaConfigure w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure hello usługi parametrów w bazie danych Azure przy użyciu PostgreSQL hello wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Dostosuj parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure
Można wyświetlić listę, wyświetlić i zaktualizować parametry konfiguracji serwera Azure PostgreSQL przy użyciu hello interfejsu wiersza polecenia (Azure CLI). Jednak tylko podzbiór aparatu konfiguracji są narażone na poziomie serwera i może być modyfikowany. 

## <a name="prerequisites"></a>Wymagania wstępne
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- Serwer i bazę danych [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) wiersza polecenia narzędzia lub użyj hello powłoki chmury Azure w przeglądarce hello.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Lista parametrów konfiguracji serwera dla bazy danych Azure PostgreSQL serwera
Uruchom wszystkie parametry można modyfikować w serwerze i ich wartości toolist hello [az postgres serwera konfiguracji na liście](/cli/azure/postgres/server/configuration#list) polecenia.

Możesz wyświetlić listę hello parametry konfiguracji serwera dla serwera hello **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Pokaż szczegóły parametru konfiguracji serwera
Szczegóły tooshow parametr określoną konfigurację serwera, uruchom hello [az postgres serwera konfiguracji Pokaż](/cli/azure/postgres/server/configuration#show) polecenia.

W tym przykładzie przedstawiono szczegóły hello **dziennika\_min\_wiadomości** parametru konfiguracji serwera dla serwera **mypgserver 20170401.postgres.database.azure.com** w obszarze Grupa zasobów **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Zmodyfikuj wartość parametru konfiguracji serwera
Można również zmodyfikować wartość hello niektórych parametru konfiguracji serwera i spowoduje to zaktualizowanie hello podstawowej konfiguracji wartość hello PostgreSQL serwera aparatu. tooupdate hello konfiguracji Użyj hello [zestawu konfiguracji serwera postgres az](/cli/azure/postgres/server/configuration#set) polecenia. 

tooupdate hello **dziennika\_min\_wiadomości** parametru konfiguracji serwera serwera **mypgserver 20170401.postgres.database.azure.com** wgrupiezasobów**myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Jeśli tooreset hello wartość parametru konfiguracji, po prostu wybierz tooleave limit hello opcjonalne `--value` parametr, a usługa hello zastosuje hello wartości domyślnej. W powyżej przykład jego wygląd:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Spowoduje to zresetowanie hello **dziennika\_min\_wiadomości** wartości domyślnej konfiguracji toohello **ostrzeżenie**. Aby uzyskać szczegółowe informacje o konfiguracji serwera i dopuszczalne wartości, zobacz dokumentację PostgreSQL [konfiguracji serwera](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Następne kroki
- Zobacz dzienniki serwera tooconfigure i dostępu, [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)
