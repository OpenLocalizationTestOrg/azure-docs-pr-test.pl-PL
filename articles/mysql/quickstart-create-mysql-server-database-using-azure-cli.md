---
title: "Szybki start: tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecania platformy Azure | Microsoft Docs"
description: "W tym przewodniku Szybki start opisano, jak utworzyć serwer usługi Azure Database for MySQL w grupie zasobów platformy Azure za pomocą interfejsu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: 3d66efa6935150c665a3f568e60c35ddbd70e8be
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure
W tym przewodniku Szybki start opisano, jak utworzyć serwer usługi Azure Database for MySQL w grupie zasobów platformy Azure za pomocą interfejsu wiersza polecenia platformy Azure w czasie około pięciu minut. Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję, w której zasób istnieje lub dla której są za niego naliczane opłaty. Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Utwórz [grupę zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) za pomocą polecenia [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create). Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.

Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myresourcegroup` w lokalizacji `westus`.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Utwórz serwer usługi Azure Database for MySQL za pomocą polecenia **az mysql server create**. Serwer umożliwia zarządzanie wieloma bazami danych. Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.

W poniższym przykładzie w regionie `westus` w grupie zasobów `myresourcegroup` jest tworzony serwer usługi Azure Database for MySQL o nazwie `myserver4demo`. Serwer ma identyfikator logowania administratora o nazwie `myadmin` i hasło `Password01!`. Serwer jest tworzony w ramach warstwy wydajności **Podstawowa** i z użyciem **50** jednostek obliczeniowych współdzielonych między wszystkimi bazami danych na tym serwerze. Możesz skalować zasoby obliczeniowe i magazyn w górę lub w dół w zależności od potrzeb aplikacji.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Konfigurowanie reguły zapory
Utwórz regułę zapory na poziomie serwera usługi Azure Database for MySQL za pomocą polecenia **az mysql server firewall-rule create**. Reguła zapory na poziomie serwera pozwala aplikacji zewnętrznej, takiej jak narzędzie wiersza polecenia **mysql.exe** lub program MySQL Workbench, na nawiązywanie połączeń z Twoim serwerem przez zaporę usługi Azure MySQL. 

W poniższym przykładzie jest tworzona reguła zapory dla wstępnie zdefiniowanego zakresu adresów, który w tym przypadku jest całym możliwym zakresem adresów IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Konfigurowanie ustawień SSL
Domyślnie połączenia SSL między Twoim serwerem i aplikacjami klienckimi są wymuszane.  Zapewnia to bezpieczeństwo danych „w ruchu” przez szyfrowanie strumienia danych przesyłanych przez Internet.  Aby uprościć ten przewodnik Szybki start, wyłączamy połączenia SSL dla Twojego serwera.  Nie jest to zalecane w przypadku serwerów produkcyjnych.  Aby uzyskać więcej informacji, zobacz [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL (Konfigurowanie łączności SSL w aplikacji w celu bezpiecznego nawiązywania połączeń z usługą Azure Database for MySQL)](./howto-configure-ssl.md).

W poniższym przykładzie jest wyłączane wymuszanie protokołu SSL na Twoim serwerze MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a>Uzyskiwanie informacji o połączeniu

Aby nawiązać połączenie z serwerem, musisz podać informacje o hoście i poświadczenia dostępu.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

Wynik jest w formacie JSON. Zanotuj wartości **fullyQualifiedDomainName** i **administratorLogin**.
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a>Nawiązywanie połączenia z serwerem za pomocą narzędzia wiersza polecenia mysql.exe
Nawiąż połączenia z serwerem za pomocą narzędzia wiersza polecenia **mysql.exe**. Program MySQL możesz pobrać [stąd](https://dev.mysql.com/downloads/) i zainstalować go na swoim komputerze. Zamiast tego możesz też kliknąć przycisk **Wypróbuj** przy przykładach kodu lub przycisk `>_` na pasku narzędzi po prawej stronie u góry w witrynie Azure Portal i uruchomić usługę **Azure Cloud Shell**.

Wpisz kolejne polecenia: 

1. Nawiąż połączenie z serwerem za pomocą narzędzia wiersza polecenia **mysql**:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Wyświetl stan serwera:
```sql
 mysql> status
```
Jeśli wszystko pójdzie dobrze, narzędzie wiersza polecenia powinno zwrócić następujący tekst:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

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

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a>Nawiązywanie połączenia z serwerem za pomocą narzędzia z graficznym interfejsem użytkownika MySQL Workbench
1.  Uruchom aplikację MySQL Workbench na swoim komputerze klienckim. Aplikację MySQL Workbench możesz pobrać i zainstalować [stąd](https://dev.mysql.com/downloads/workbench/).

2.  W oknie dialogowym **Konfigurowanie nowego połączenia** wprowadź poniższe informacje na karcie **Parametry**:

   ![konfigurowanie nowego połączenia](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Ustawienie** | **Sugerowana wartość** | **Opis** |
|---|---|---|
|   Nazwa połączenia | Moje połączenie | Podaj etykietę dla tego połączenia (może to być dowolny tekst) |
| Metoda połączenia | wybierz opcję Standardowa (TCP/IP) | Użyj protokołu TCP/IP do nawiązania połączenia z bazą danych platformy Azure Database dla programu MySQL |
| Nazwa hosta | myserver4demo.mysql.database.azure.com | Wcześniej zanotowana nazwa serwera. |
| Port | 3306 | Używany jest domyślny port dla programu MySQL. |
| Nazwa użytkownika | myadmin@myserver4demo | Identyfikator logowania administratora serwera zanotowany przez Ciebie wcześniej. |
| Hasło | **** | Użyj hasła do konta administratora, które zostało ustawione wcześniej. |

Kliknij przycisk **Testuj połączenie**, aby sprawdzić, czy wszystkie parametry zostały prawidłowo skonfigurowane.
Teraz możesz kliknąć połączenie, aby pomyślnie nawiązać połączenie z serwerem.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Jeśli te zasoby nie są Ci potrzebne do pracy z innym przewodnikiem Szybki start lub samouczkiem, możesz je usunąć, uruchamiając następujące polecenie: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Projektowanie bazy danych MySQL za pomocą interfejsu wiersza polecenia platformy Azure](./tutorial-design-database-using-cli.md)
