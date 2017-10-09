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
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="a2646-104">Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello pojedynczej bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="a2646-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="a2646-105">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="a2646-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="a2646-106">Ten przewodnik szczegółów przy użyciu hello Azure CLI toodeploy bazy danych Azure SQL w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w [serwera logicznego bazy danych SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="a2646-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="a2646-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a2646-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a2646-108">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a2646-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a2646-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="a2646-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a2646-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a2646-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="a2646-111">Definiowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="a2646-111">Define variables</span></span>

<span data-ttu-id="a2646-112">Zdefiniuj zmienne do użytku w skryptach hello w tym szybki start.</span><span class="sxs-lookup"><span data-stu-id="a2646-112">Define variables for use in hello scripts in this quick start.</span></span>

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

## <a name="create-a-resource-group"></a><span data-ttu-id="a2646-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="a2646-113">Create a resource group</span></span>

<span data-ttu-id="a2646-114">Utwórz [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a2646-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a2646-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="a2646-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="a2646-116">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a2646-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="a2646-117">Tworzenie serwera logicznego</span><span class="sxs-lookup"><span data-stu-id="a2646-117">Create a logical server</span></span>

<span data-ttu-id="a2646-118">Utwórz [serwera logicznego bazy danych SQL Azure](sql-database-features.md) przy użyciu hello [az programu sql server Utwórz](/cli/azure/sql/server#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a2646-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="a2646-119">Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="a2646-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="a2646-120">Witaj poniższy przykład tworzy losowo nazwanym serwerze w grupie zasobów o nazwie identyfikator logowania administratora `ServerAdmin` oraz hasła `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="a2646-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="a2646-121">Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a2646-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="a2646-122">Konfigurowanie reguły zapory serwera</span><span class="sxs-lookup"><span data-stu-id="a2646-122">Configure a server firewall rule</span></span>

<span data-ttu-id="a2646-123">Utwórz [regułę zapory poziomu serwera bazy danych SQL Azure](sql-database-firewall-configure.md) przy użyciu hello [utworzyć zapory serwera sql az](/cli/azure/sql/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a2646-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="a2646-124">Reguły zapory poziomu serwera umożliwia aplikacji zewnętrznych, takich jak SQL Server Management Studio lub hello SQLCMD narzędzie tooconnect tooa bazy danych SQL za pośrednictwem zapory usługi SQL Database hello.</span><span class="sxs-lookup"><span data-stu-id="a2646-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="a2646-125">W hello poniższy przykład hello zapory jest otwarty tylko do innych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2646-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="a2646-126">tooenable łączność zewnętrzną, zmiana hello adres tooan odpowiedniego adresu IP dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="a2646-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="a2646-127">tooopen wszystkie adresy IP, użyj 0.0.0.0 jako hello początkowy adres IP i 255.255.255.255 jako hello adres końcowy.</span><span class="sxs-lookup"><span data-stu-id="a2646-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="a2646-128">Usługa SQL Database nawiązuje komunikację na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="a2646-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="a2646-129">Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci.</span><span class="sxs-lookup"><span data-stu-id="a2646-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="a2646-130">Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 1433.</span><span class="sxs-lookup"><span data-stu-id="a2646-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="a2646-131">Utwórz bazę danych na serwerze hello z przykładowymi danymi</span><span class="sxs-lookup"><span data-stu-id="a2646-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="a2646-132">Utwórz bazę danych z [poziom wydajności S0](sql-database-service-tiers.md) w powitania serwera przy użyciu hello [tworzenie bazy danych sql az](/cli/azure/sql/db#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a2646-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="a2646-133">Witaj poniższy przykład tworzy bazę danych o nazwie `mySampleDatabase` i obciążeń hello AdventureWorksLT przykładowe dane do tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a2646-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="a2646-134">Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami (inne Szybkie uruchamianie w tej kolekcji kompilacji na powitania wartości w tym szybki start).</span><span class="sxs-lookup"><span data-stu-id="a2646-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="a2646-135">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="a2646-135">Clean up resources</span></span>

<span data-ttu-id="a2646-136">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="a2646-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="a2646-137">Jeśli planujesz toocontinue toowork z kolejnych Szybki Start, nie czyszczenie zasobów hello utworzone w tym szybki start.</span><span class="sxs-lookup"><span data-stu-id="a2646-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="a2646-138">Jeśli nie planujesz toocontinue, użyj powitania po toodelete kroki wszystkie zasoby utworzone przez tego szybkiego startu w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a2646-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="a2646-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2646-139">Next steps</span></span>

<span data-ttu-id="a2646-140">Teraz, gdy już masz bazę danych, możesz nawiązać z nią połączenie i uruchamiać zapytania za pomocą ulubionych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a2646-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="a2646-141">Dowiedz się więcej, wybierając narzędzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="a2646-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="a2646-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="a2646-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="a2646-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a2646-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="a2646-144">.NET</span><span class="sxs-lookup"><span data-stu-id="a2646-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="a2646-145">PHP</span><span class="sxs-lookup"><span data-stu-id="a2646-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="a2646-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="a2646-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="a2646-147">Java</span><span class="sxs-lookup"><span data-stu-id="a2646-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="a2646-148">Python</span><span class="sxs-lookup"><span data-stu-id="a2646-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="a2646-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="a2646-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

