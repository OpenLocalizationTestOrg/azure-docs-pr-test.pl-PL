---
title: "Tworzenie bazy danych Azure dla PostgreSQL przy użyciu interfejsu wiersza polecenia Azure hello | Dokumentacja firmy Microsoft"
description: "Szybki start toocreate przewodnik i zarządzania nimi bazy danych Azure PostgreSQL serwera przy użyciu wiersza polecenia platformy Azure (interfejsu wiersza polecenia)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Tworzenie bazy danych Azure dla PostgreSQL przy użyciu hello wiersza polecenia platformy Azure
Bazy danych platformy Azure dla PostgreSQL jest zarządzana usługa, która pozwala toorun, zarządzanie i skalowania wysokiej dostępności PostgreSQL baz danych w chmurze hello. Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Ta opcja szybkiego startu przedstawia sposób toocreate Azure bazy danych dla serwera PostgreSQL w [grupy zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) przy użyciu hello wiersza polecenia platformy Azure.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Jeśli masz wiele subskrypcji, wybierz subskrypcję odpowiednie hello, naliczane hello zasobów. Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myresourcegroup` w hello `westus` lokalizacji.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Tworzenie serwera usługi Azure Database for PostgreSQL

Utwórz [Azure bazy danych serwera PostgreSQL](overview.md) przy użyciu hello [utworzenie przez serwer postgres az](/cli/azure/postgres/server#create) polecenia. Serwer zawiera grupę baz danych zarządzanych jako grupa. 

Witaj poniższy przykład tworzy serwer o nazwie `mypgserver-20170401` w grupie zasobów `myresourcegroup` z identyfikator logowania administratora serwera `mylogin`. Nazwa Hello serwera mapuje nazwę tooDNS i w związku z tym jest wymagana toobe globalnie unikatowa na platformie Azure. SUBSTITUTE hello `<server_admin_password>` o własne wartości.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> Hello identyfikator logowania administratora serwera i hasło, które są określone w tym miejscu są wymagane toolog Server toohello i jej baz danych w dalszej części tego szybki start. Zapamiętaj lub zapisz te informacje do wykorzystania w przyszłości.

Domyślnie baza danych **postgres** zostanie utworzona na Twoim serwerze. Witaj [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) baza danych jest domyślna baza danych przeznaczone do użytku przez użytkowników, narzędzia i aplikacje innych producentów. 


## <a name="configure-a-server-level-firewall-rule"></a>Konfigurowanie reguły zapory na poziomie serwera

Utwórz regułę zapory poziomu serwera Azure PostgreSQL z hello [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia. Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) lub [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure PostgreSQL hello. 

Można ustawić reguły zapory, która obejmuje IP zakresu toobe stanie tooconnect z sieci. Witaj poniższym przykładzie użyto [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) toocreate regułę zapory `AllowAllIps` zakres adresów IP. tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Serwer Azure PostgreSQL komunikuje się przez port 5432. Podczas nawiązywania połączenia z sieci firmowej ruch wychodzący przez port 5432 może być blokowany przez zaporę sieciową. Ma dział IT, otwórz port 5432 tooconnect tooyour bazy danych SQL Azure serwera.

## <a name="get-hello-connection-information"></a>Pobierz informacje o połączeniu hello

tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

wynik Hello jest w formacie JSON. Zanotuj hello **administratorLogin** i **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-toopostgresql-database-using-psql"></a>Połącz tooPostgreSQL bazy danych przy użyciu psql

Jeśli komputer kliencki ma zainstalowany PostgreSQL, można użyć lokalnego wystąpienia programu [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL serwera. Użyjmy teraz hello psql narzędzia wiersza polecenia tooconnect toohello Azure PostgreSQL serwera.

1. Uruchom następujące polecenie psql tooconnect tooan Azure bazy danych dla serwera PostgreSQL hello
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Na przykład następujące polecenie hello łączy toohello domyślna baza danych o nazwie **postgres** na serwerze PostgreSQL **mypgserver 20170401.postgres.database.azure.com** przy użyciu poświadczeń dostępu. Wprowadź hello `<server_admin_password>` wybrano po wyświetleniu monitu o hasło.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Po przejściu toohello podłączonego serwera, należy utworzyć pustą bazę danych, w wierszu hello.
```sql
CREATE DATABASE mypgsqldb;
```

3.  W wierszu polecenia hello wykonania hello następujące polecenia tooswitch połączenia toohello nowo utworzone w bazie danych **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Połącz tooPostgreSQL bazy danych przy użyciu pgAdmin

Serwer PostgreSQL tooAzure tooconnect przy użyciu hello graficznego interfejsu użytkownika narzędzia _pgAdmin_
1.  Uruchamianie hello _pgAdmin_ aplikacji na komputerze klienckim. Aplikację _pgAdmin_ można zainstalować ze strony http://www.pgadmin.org/.
2.  Wybierz **dodać nowy serwer** z hello **szybkie linki** menu.
3.  W hello **Utwórz — serwer** okno dialogowe **ogólne** wprowadź unikatową przyjazną nazwę dla serwera hello. Na przykład **Serwer Azure PostgreSQL**.
 ![Narzędzie pgAdmin — Tworzenie — Serwer](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  W hello **Utwórz — serwer** okno dialogowe **połączenia** karty:
    - Wprowadź nazwę FQDN serwera hello (na przykład **mypgserver 20170401.postgres.database.azure.com**) w hello **nazwę hosta / adres** pole. 
    - Wprowadź port 5432 do hello **portu** pole. 
    - Wprowadź hello **identyfikator logowania administratora serwera (user@mypgserver)** uzyskany wcześniej w tym Szybki Start i hasła podczas tworzenia powitania serwera na powitania **Username** i **hasło** pola odpowiednio.
    - W polu **Tryb SSL** wybierz wartość **Wymagany**. Domyślnie wszystkie serwery Azure PostgreSQL są tworzone z włączonym wymuszaniem protokołu SSL. tooturn Wyłącz wymuszanie protokołu SSL, zobacz szczegóły w [wymuszania SSL](./concepts-ssl-connection-security.md).

    ![Narzędzie pgAdmin — Tworzenie — Serwer](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Kliknij pozycję **Zapisz**.
6.  W okienku po lewej stronie przeglądarki hello, rozwiń węzeł hello **grup serwerów**. Wybierz swój serwer **Serwer Azure PostgreSQL**.
7.  Wybierz hello **serwera** połączona, a następnie wybierz **baz danych** na jego podstawie. 
8.  Kliknij prawym przyciskiem myszy **baz danych** tooCreate bazy danych.
9.  Wybierz nazwę bazy danych **mypgsqldb** i hello właściciela go jako identyfikator logowania administratora serwera **mylogin**.
10. Kliknij przycisk **zapisać** toocreate pustą bazę danych.
11. W hello **przeglądarki**, rozwiń węzeł hello **serwerów** grupy. Rozwiń węzeł serwera hello utworzony i zobacz hello bazy danych **mypgsqldb** na jego podstawie.
 ![Narzędzie pgAdmin — Tworzenie — Baza danych](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Czyszczenie wszystkich zasobów utworzonego w szybkiego startu hello przez usunięcie hello [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. Jeśli planujesz toocontinue toowork kolejne Przewodniki Szybki Start, czy nie Oczyszczanie hello zasoby utworzone w tym Szybki Start. Jeśli nie planujesz toocontinue, użyj hello następujące kroki toodelete wszystkie zasoby utworzone przez tego szybkiego startu w hello wiersza polecenia platformy Azure.

```azurecli-interactive
az group delete --name myresourcegroup
```

Jeśli chcesz tylko jeden serwer nowo utworzony hello toodelete, możesz uruchomić [usuwania serwera postgres az](/cli/azure/postgres/server#delete) polecenia.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Następne kroki
> [!div class="nextstepaction"]
> [Migrowanie bazy danych przy użyciu funkcji eksportowania i importowania](./howto-migrate-using-export-and-import.md)
