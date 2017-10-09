---
title: "Szybki start: tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecania platformy Azure | Microsoft Docs"
description: "Ta opcja szybkiego startu w tym artykule opisano sposób toouse hello Azure CLI toocreate bazy danych Azure MySQL serwera w ramach grupy zasobów platformy Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure
Ta opcja szybkiego startu w tym artykule opisano sposób toouse hello Azure CLI toocreate bazy danych Azure MySQL serwera w ramach grupy zasobów platformy Azure w ciągu około pięciu minut. Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Jeśli masz wiele subskrypcji, wybierz hello odpowiednie subskrypcji, w którym hello zasobów istnieje lub jest on rozliczany dla. Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Utwórz [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) przy użyciu hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia. Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.

Witaj poniższy przykład tworzy grupę zasobów o nazwie `myresourcegroup` w hello `westus` lokalizacji.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Tworzenie bazy danych Azure MySQL serwera z hello **utworzenie przez serwer mysql az** polecenia. Serwer umożliwia zarządzanie wieloma bazami danych. Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.

Witaj poniższy przykład tworzy Azure bazę danych MySQL serwera znajduje się w `westus` w grupie zasobów hello `myresourcegroup` o nazwie `myserver4demo`. powitania serwera zawiera dziennik administratora w nazwie `myadmin` i hasło `Password01!`. Serwer Hello jest tworzony z **podstawowe** warstwę wydajności i **50** obliczeniowe jednostki wspólne dla wszystkich baz danych hello powitania serwera. Możesz skalować możliwości obliczeniowe i Magazyn w górę lub w dół w zależności od potrzeb aplikacji hello.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Konfigurowanie reguły zapory
Utwórz bazę danych MySQL reguły zapory poziomu serwera przy użyciu hello Azure **az mysql reguły zapory serwera — Utwórz** polecenia. Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak hello **mysql.exe** narzędzia wiersza polecenia lub MySQL Workbench tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure MySQL hello. 

Witaj poniższy przykład powoduje utworzenie reguły zapory dla zakresu adresów wstępnie zdefiniowanych, czyli w tym przykładzie hello całego możliwe zakres adresów IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Konfigurowanie ustawień SSL
Domyślnie połączenia SSL między Twoim serwerem i aplikacjami klienckimi są wymuszane.  Dzięki temu zabezpieczeń "w ruchu" danych przez szyfrowanie hello strumienia danych za pośrednictwem hello internet.  toomake to szybki start łatwiej, możemy wyłączyć połączeń SSL serwera.  Nie jest to zalecane w przypadku serwerów produkcyjnych.  Aby uzyskać więcej informacji, zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](./howto-configure-ssl.md).

Witaj poniższy przykład powoduje wyłączenie wymuszenie SSL na serwerze programu MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Pobierz informacje o połączeniu hello

tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

wynik Hello jest w formacie JSON. Zanotuj hello **fullyQualifiedDomainName** i **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Połącz serwer toohello za pomocą narzędzia wiersza polecenia mysql.exe hello
Połącz przy użyciu powitania serwera tooyour **mysql.exe** narzędzia wiersza polecenia. Program MySQL możesz pobrać [stąd](https://dev.mysql.com/downloads/) i zainstalować go na swoim komputerze. Zamiast tego możesz również kliknąć pozycję hello **spróbuj on** znajdującego się na przykłady kodu lub hello `>_` przycisk hello górnym prawym pasku narzędzi w hello portalu Azure i uruchamiania hello **powłoki chmury Azure**.

Wpisz hello następnego polecenia: 

1. Połącz, używając serwera toohello **mysql** narzędzia wiersza polecenia:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Wyświetl stan serwera:
```sql
 mysql> status
```
Jeśli wszystko odbędzie się poprawnie, narzędzia wiersza polecenia hello powinien output hello następującego tekstu:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Aby zapoznać się z dodatkowymi poleceniami, zobacz [MySQL 5.7 Reference Manual - Chapter 4.5.1 (Podręcznik programu MySQL 5.7 — Rozdział 4.5.1)](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Połącz przy użyciu narzędzia Workbench MySQL graficznego interfejsu użytkownika hello serwer toohello
1.  Uruchom program hello MySQL Workbench aplikacji na komputerze klienckim. Aplikację MySQL Workbench możesz pobrać i zainstalować [stąd](https://dev.mysql.com/downloads/workbench/).

2.  W hello **instalacji nowego połączenia** okna dialogowego wprowadź hello następujących informacji **parametry** karty:

   ![konfigurowanie nowego połączenia](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Ustawienie** | **Sugerowana wartość** | **Opis** |
|---|---|---|
|   Nazwa połączenia | Moje połączenie | Podaj etykietę dla tego połączenia (może to być dowolny tekst) |
| Metoda połączenia | wybierz opcję Standardowa (TCP/IP) | Użyj protokołu TCP/IP w tooconnect tooAzure bazy danych dla programu MySQL > |
| Nazwa hosta | myserver4demo.mysql.database.azure.com | Wcześniej zanotowana nazwa serwera. |
| Port | 3306 | domyślny port MySQL Hello jest używany. |
| Nazwa użytkownika | myadmin@myserver4demo | Witaj identyfikator logowania administratora serwera zanotowaną wcześniej. |
| Hasło | **** | Użyj hello hasło konta administratora, przez skonfigurowane wcześniej. |

Kliknij przycisk **Testuj połączenie** tootest, jeśli wszystkie parametry są poprawnie skonfigurowane.
Teraz, możesz kliknąć połączenia hello toosuccessfully połączenia toohello serwera.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Jeśli nie potrzebujesz tych zasobów innym Szybki Start/samouczek, usunąć je, wykonując następujące polecenia hello: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Projektowanie bazy danych MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./tutorial-design-database-using-cli.md)
