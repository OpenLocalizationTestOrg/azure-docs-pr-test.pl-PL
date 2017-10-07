---
title: "aaaDesign pierwszy Azure bazy danych dla bazy danych MySQL — wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek wyjaśnia sposób toocreate i zarządzanie bazą danych Azure MySQL serwera i bazy danych przy użyciu usługi Azure CLI 2.0 z wiersza polecenia hello."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Projektowanie pierwszej bazy danych Azure, aby baza danych MySQL

Bazy danych platformy Azure dla programu MySQL jest usługą relacyjnych baz danych w hello firmy Microsoft w chmurze oparte na aparacie bazy danych MySQL Community Edition. W tym samouczku używasz interfejsu wiersza polecenia Azure (interfejsu wiersza polecenia) i inne narzędzia toolearn jak do:

> [!div class="checklist"]
> * Utwórz bazę danych systemu Azure dla programu MySQL
> * Konfigurowanie zapory serwera hello
> * Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bazy danych
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
Utwórz [grupy zasobów platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) z [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia. Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.

Witaj poniższy przykład tworzy grupę zasobów o nazwie `mycliresource` w hello `westus` lokalizacji.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Utwórz bazę danych Azure, dla polecenia Utwórz MySQL co serwer hello az mysql. Serwer umożliwia zarządzanie wieloma bazami danych. Zwykle dla każdego projektu lub użytkownika używana jest oddzielna baza danych.

Witaj poniższy przykład tworzy Azure bazę danych MySQL serwera znajduje się w `westus` w grupie zasobów hello `mycliresource` o nazwie `mycliserver`. powitania serwera zawiera dziennik administratora w nazwie `myadmin` i hasło `Password01!`. Serwer Hello jest tworzony z **podstawowe** warstwę wydajności i **50** obliczeniowe jednostki wspólne dla wszystkich baz danych hello powitania serwera. Możesz skalować możliwości obliczeniowe i Magazyn w górę lub w dół w zależności od potrzeb aplikacji hello.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Konfigurowanie reguły zapory
Utwórz bazę danych Azure, aby utworzyć regułę zapory poziomu serwera MySQL z hello az mysql reguły zapory serwera — polecenie. Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak **mysql** narzędzia wiersza polecenia lub MySQL Workbench tooconnect tooyour serwerem za pośrednictwem zapory usługi Azure MySQL hello. 

Witaj poniższy przykład powoduje utworzenie reguły zapory dla zakresu adresów wstępnie zdefiniowane. Ten przykład przedstawia hello całego możliwe zakres adresów IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Pobierz informacje o połączeniu hello

tooconnect tooyour serwera, należy tooprovide hosta dostępu i informacji o poświadczenia.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

wynik Hello jest w formacie JSON. Zanotuj hello **fullyQualifiedDomainName** i **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
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

## <a name="connect-toohello-server-using-mysql"></a>Połącz serwer toohello przy użyciu mysql
Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour połączenia bazy danych platformy Azure dla serwera MySQL. W tym przykładzie polecenie hello jest:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Tworzenie pustej bazy danych
Po wyświetleniu toohello podłączonego serwera, należy utworzyć pustą bazę danych.
```sql
mysql> CREATE DATABASE mysampledb;
```

W wierszu hello Uruchom hello następujące bazy danych polecenie tooswitch hello połączenia toothis nowo utworzone:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Tworzenie tabel w bazie danych hello
Teraz, gdy wiesz, jak tooconnect toohello Azure bazy danych dla bazy danych MySQL, firma Microsoft może przejść przez jak toocomplete niektóre podstawowe zadania.

Firma Microsoft najpierw utwórz tabelę i załaduj go z niektórych danych. Teraz utworzyć tabelę, która przechowuje informacje dotyczące spisu.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Ładowanie danych do tabel hello
Teraz, gdy mamy tabeli możemy wstawić niektóre dane do niego. W oknie wiersza polecenia Otwórz hello uruchom następujące zapytanie tooinsert hello niektórych wierszy danych.
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

Należy również zaktualizować hello dane w tabelach hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

wiersz Hello pobiera odpowiednio aktualizowany podczas pobierania danych.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Przywracanie bazy danych tooa poprzedniego punktu w czasie
Załóżmy, że zostanie przypadkowo usunięte w tej tabeli. Jest to coś, co nie można łatwo odzyskać z. Bazy danych platformy Azure dla programu MySQL pozwala toogo tooany zapasowego punktu w czasie w hello ostatnio zapasowej too35 dni i przywrócić ten punkt w czasie tooa nowego serwera. Można użyć tego nowego serwera toorecover usunięte dane. Witaj następujące kroki przywracania hello przykładowy serwer tooa punkt przed dodano hello tabeli.

Witaj przywracania należy hello następujących informacji:

- Punkt przywracania: Wybierz w momencie po hello serwer został zmieniony. Musi być większa niż lub równa wartości kopii zapasowej najstarsze toohello źródłowej bazy danych.
- Serwer docelowy: Podaj nową nazwę serwera ma toorestore do
- Serwer źródłowy: Podaj nazwę hello powitania serwera ma toorestore z
- Lokalizacja: Nie można wybrać hello region, domyślnie jest taka sama jak powitania serwera źródłowego

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

toorestore powitania serwera i [tooa w momencie przywracania](./howto-restore-server-portal.md) przed hello tabeli został usunięty. Przywracanie serwera tooa innego punktu w czasie tworzy zduplikowane nowy serwer jako hello oryginalny serwer określoną hello punktu w czasie, pod warunkiem, że w okresie przechowywania hello dla Twojego [warstwy usług](./concepts-service-tiers.md).

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono do:
> [!div class="checklist"]
> * Utwórz bazę danych systemu Azure dla programu MySQL
> * Konfigurowanie zapory serwera hello
> * Użyj [narzędzia wiersza polecenia mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bazy danych
> * Ładuj dane przykładowe
> * Zapytania o dane
> * Aktualizowanie danych
> * Przywracanie danych

> [!div class="nextstepaction"]
> [Bazy danych platformy Azure dla programu MySQL — przykłady wiersza polecenia platformy Azure](./sample-scripts-azure-cli.md)
