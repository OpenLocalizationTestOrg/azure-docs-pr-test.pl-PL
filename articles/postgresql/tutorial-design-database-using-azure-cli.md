---
title: "Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak tooDesign Twojego pierwszego Azure bazy danych PostgreSQL przy użyciu wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Projektowanie pierwszą bazę danych Azure do PostgreSQL przy użyciu wiersza polecenia platformy Azure 
W tym samouczku używasz interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia toolearn jak do:
> [!div class="checklist"]
> * Tworzenie serwera usługi Azure Database for PostgreSQL
> * Konfigurowanie zapory serwera hello
> * Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate Narzędzia bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

Możesz użyć hello powłoki chmury Azure w przeglądarce hello lub [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli) na własne bloki kodu komputera toorun hello w tym samouczku.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Jeśli masz wiele subskrypcji, wybierz hello odpowiednie subskrypcji, w którym hello zasobów istnieje lub jest on rozliczany dla. Wybierz określony identyfikator subskrypcji na Twoim koncie za pomocą polecenia [az account set](/cli/azure/account#set).
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

Witaj poniższy przykład tworzy serwer o nazwie `mypgserver-20170401` w grupie zasobów `myresourcegroup` z identyfikator logowania administratora serwera `mylogin`. Nazwa serwera mapuje nazwę tooDNS i w związku z tym jest wymagana toobe globalnie unikatowa na platformie Azure. SUBSTITUTE hello `<server_admin_password>` o własne wartości.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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
>

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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Połącz tooAzure bazy danych dla bazy danych PostgreSQL przy użyciu psql
Jeśli komputer kliencki ma zainstalowany PostgreSQL, można użyć lokalnego wystąpienia programu [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), lub hello Azure Cloud Console tooconnect tooan Azure PostgreSQL serwera. Użyjmy teraz hello psql narzędzia wiersza polecenia tooconnect toohello bazy danych Azure, PostgreSQL serwera.

1. Uruchom następujące polecenie psql tooconnect tooan Azure bazy danych dla serwera PostgreSQL hello
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Na przykład następujące polecenie hello łączy toohello domyślna baza danych o nazwie **postgres** na serwerze PostgreSQL **mypgserver 20170401.postgres.database.azure.com** przy użyciu poświadczeń dostępu. Wprowadź hello `<server_admin_password>` wybrano po wyświetleniu monitu o hasło.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Po przejściu toohello podłączonego serwera, należy utworzyć pustą bazę danych, w wierszu hello.
```sql
CREATE DATABASE mypgsqldb;
```

3.  W wierszu polecenia hello wykonania hello następujące polecenia tooswitch połączenia toohello nowo utworzone w bazie danych **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Tworzenie tabel w bazie danych hello
Teraz, gdy wiesz, jak toohello tooconnect bazą danych Azure dla PostgreSQL, firma Microsoft może przejść w sposób toocomplete niektóre podstawowe zadania.

Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych. Ta funkcja pozwala utworzyć tabelę, która śledzi informacje o spisie.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Można wyświetlić hello nowo utworzony tabeli w hello listy tabel teraz, wpisując:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Ładowanie danych do tabel hello
Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego. W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Masz teraz dwa wiersze przykładowych danych do tabeli hello, utworzony wcześniej.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Zapytania i Aktualizuj hello dane w tabelach hello
Wykonanie poniższych informacji tooretrieve zapytania z tabeli bazy danych hello hello. 
```sql
SELECT * FROM inventory;
```

Można także zaktualizować hello dane w tabelach hello
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Przywracanie bazy danych tooa poprzedniego punktu w czasie
Załóżmy, że przypadkowo usunięto tabelę. Jest to coś, co nie można łatwo odzyskać z. Bazy danych platformy Azure dla PostgreSQL umożliwia toogo tooany Wstecz w momencie (w hello ostatnich dni too7 (Basic) i 35 dni (standardowe)) i przywracania w momencie tooa nowego serwera. Można użyć tego nowego serwera toorecover usunięte dane. Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Witaj `az postgres server restore` polecenie musi hello następujące parametry:
| Ustawienie | Sugerowana wartość | Opis  |
| --- | --- | --- |
| --grupy zasobów |  myResourceGroup |  Grupy zasobów, w których hello istnieje serwer źródłowy.  |
| — Nazwa | przywrócona mypgserver | Nazwa Hello hello nowy serwer, który jest tworzony przez polecenie restore hello. |
| Przywracanie punktu w czasie | 2017-04-13T13:59:00Z | Wybierz toorestore punktu w czasie, aby. Ta data i godzina musi być w okresie przechowywania kopii zapasowej serwera źródłowego hello. Użyj formatu ISO8601 daty i godziny. Na przykład możesz może używać własnych lokalnej strefie czasowej, takich jak `2017-04-13T05:59:00-08:00`, lub użyj formatu czasu UTC Zulu `2017-04-13T13:59:00Z`. |
| --serwera źródłowego | mypgserver 20170401 | Witaj, nazwa lub identyfikator toorestore serwera źródłowego hello z. |

Przywracanie serwera tooa w momencie tworzy nowy serwer, kopiowanie jako hello oryginalnego serwera na powitania punktu w czasie, które określisz. Hello lokalizacji i cenach wartości warstwy hello przywróceniu serwera są hello taki sam jak powitania serwera źródłowego.

polecenie Hello jest synchroniczne i zwróci po przywróceniu powitania serwera. Po zakończeniu przywracania hello zlokalizować hello nowy serwer, który został utworzony. Sprawdź hello danych zostało przywrócone, zgodnie z oczekiwaniami.


## <a name="next-steps"></a>Następne kroki
W tym samouczku można przedstawiono sposób toouse wiersza polecenia platformy Azure (interfejsu wiersza polecenia) i inne narzędzia do:
> [!div class="checklist"]
> * Tworzenie serwera usługi Azure Database for PostgreSQL
> * Konfigurowanie zapory serwera hello
> * Użyj [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate Narzędzia bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

Następnie Dowiedz się, jak toouse hello podobne zadania toodo portalu Azure, przejrzyj tego samouczka: [projektowania pierwszą bazę danych Azure za pomocą PostgreSQL hello portalu Azure](tutorial-design-database-using-azure-portal.md)
