---
title: 'Interfejs wiersza polecenia platformy Azure: tworzenie bazy danych SQL | Microsoft Docs'
description: "Dowiedz się, jak toocreate serwera logicznego SQL Database, regułę zapory poziomu serwera i baz danych przy użyciu hello wiersza polecenia platformy Azure."
keywords: "samouczek usługi sql database, tworzenie bazy danych sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello pojedynczej bazy danych Azure SQL

Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Ten przewodnik szczegółów przy użyciu hello Azure CLI toodeploy bazy danych Azure SQL w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w [serwera logicznego bazy danych SQL Azure](sql-database-features.md).

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Definiowanie zmiennych

Zdefiniuj zmienne do użytku w skryptach hello w tym szybki start.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Tworzenie serwera logicznego

Utwórz [serwera logicznego bazy danych SQL Azure](sql-database-features.md) przy użyciu hello [az programu sql server Utwórz](/cli/azure/sql/server#create) polecenia. Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa. Witaj poniższy przykład tworzy losowo nazwanym serwerze w grupie zasobów o nazwie identyfikator logowania administratora `ServerAdmin` oraz hasła `ChangeYourAdminPassword1`. Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Konfigurowanie reguły zapory serwera

Utwórz [regułę zapory poziomu serwera bazy danych SQL Azure](sql-database-firewall-configure.md) przy użyciu hello [utworzyć zapory serwera sql az](/cli/azure/sql/server/firewall-rule#create) polecenia. Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak SQL Server Management Studio lub hello SQLCMD narzędzie tooconnect tooa bazy danych SQL za pośrednictwem zapory usługi SQL Database hello. W hello poniższy przykład hello zapory jest otwarty tylko do innych zasobów platformy Azure. tooenable łączność zewnętrzną, zmiana hello adres tooan odpowiedniego adresu IP dla danego środowiska. tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> Usługa SQL Database nawiązuje komunikację na porcie 1433. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Utwórz bazę danych na serwerze hello z przykładowymi danymi

Utwórz bazę danych z [poziom wydajności S0](sql-database-service-tiers.md) w powitania serwera przy użyciu hello [tworzenie bazy danych sql az](/cli/azure/sql/db#create) polecenia. Witaj poniższy przykład tworzy bazę danych o nazwie `mySampleDatabase` i obciążeń hello AdventureWorksLT przykładowe dane do tej bazy danych. Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami (inne Szybkie uruchamianie w tej kolekcji kompilacji na powitania wartości w tym szybki start).

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. 

> [!TIP]
> Jeśli planujesz toocontinue toowork z kolejnych Szybki Start, nie czyszczenie zasobów hello utworzone w tym szybki start. Jeśli nie planujesz toocontinue, użyj powitania po toodelete kroki wszystkie zasoby utworzone przez tego szybkiego startu w portalu Azure hello.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Następne kroki

Teraz, gdy już masz bazę danych, możesz nawiązać z nią połączenie i uruchamiać zapytania za pomocą ulubionych narzędzi. Dowiedz się więcej, wybierając narzędzie poniżej:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

