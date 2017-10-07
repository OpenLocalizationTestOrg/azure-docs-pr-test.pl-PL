---
title: "dzienniki serwera dostępu i aaaConfigure PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak dostępu i tooconfigure hello do dzienników serwera w bazie danych Azure dla PostgreSQL przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Konfigurowanie i uzyskać dostępu do dzienników serwera przy użyciu wiersza polecenia platformy Azure
Możesz pobrać hello PostgreSQL dzienników błędów serwera przy użyciu hello interfejsu wiersza polecenia (Azure CLI). Dzienniki tootransaction dostępu nie jest obsługiwane. 

## <a name="prerequisites"></a>Wymagania wstępne
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- [PostgreSQL serwera bazy danych Azure](quickstart-create-server-database-azure-cli.md)
- Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) wiersza polecenia narzędzia lub użyj hello powłoki chmury Azure w przeglądarce hello.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Konfigurowanie rejestrowania w bazie danych Azure dla PostgreSQL
Można skonfigurować powitania serwera tooaccess zapytania dzienników i dzienników błędów. Dzienniki błędów mogą zawierać informacje automatycznego próżni, połączenia i punkty kontrolne.
1. Włączanie rejestrowania
2. Dziennik aktualizacji\_instrukcji i dziennika\_min\_czas trwania\_rejestrowanie zapytań tooenable — instrukcja
3. Okres przechowywania aktualizacji

Aby uzyskać więcej informacji, zobacz [Dostosowywanie parametry konfiguracji serwera](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Lista dzienników bazy danych Azure PostgreSQL serwera
pliki dziennika dostępne hello toolist dla serwera, uruchom hello [az postgres dzienniki serwera listy](/cli/azure/postgres/server-logs#list) polecenia.

Możesz wyświetlić listę plików dziennika powitania serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**i bezpośrednie jego tekstu tooa plik o nazwie **dziennika\_pliki\_lista.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Pobierz dzienniki lokalnie z serwera hello
Witaj [Pobierz dzienniki serwera az postgres](/cli/azure/postgres/server-logs#download) polecenie umożliwia toodownload osobnych plikach dziennika dla serwera. 

W tym przykładzie pliki do pobrania hello pliku dziennika określonego serwera hello **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup** tooyour lokalnego środowiska.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Następne kroki
- toolearn więcej informacji na temat dzienniki serwera, zobacz [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)
- Aby uzyskać więcej informacji na parametry serwera, zobacz [dostosować parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure](howto-configure-server-parameters-using-cli.md)
