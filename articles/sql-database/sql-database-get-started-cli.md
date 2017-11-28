---
title: 'Interfejs wiersza polecenia platformy Azure: tworzenie bazy danych SQL | Microsoft Docs'
description: "Dowiedz się, jak utworzyć serwer logiczny, regułę zapory na poziomie serwera i bazy danych usługi SQL Database przy użyciu interfejsu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="fd17a-104">Tworzenie pojedynczej bazy danych Azure SQL Database za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fd17a-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="fd17a-105">Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="fd17a-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="fd17a-106">W tym przewodniku znajdują się szczegółowe informacje dotyczące użycia interfejsu wiersza polecenia platformy Azure na potrzeby wdrażania bazy danych Azure SQL Database w [grupie zasobów Azure](../azure-resource-manager/resource-group-overview.md) na [serwerze logicznym Azure SQL Database](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="fd17a-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="fd17a-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fd17a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fd17a-108">Jeśli chcesz zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="fd17a-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fd17a-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="fd17a-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="fd17a-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fd17a-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="fd17a-111">Definiowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="fd17a-111">Define variables</span></span>

<span data-ttu-id="fd17a-112">Zdefiniuj zmienne do wykorzystania w skryptach w tym przewodniku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="fd17a-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fd17a-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="fd17a-113">Create a resource group</span></span>

<span data-ttu-id="fd17a-114">Utwórz [grupę zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fd17a-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="fd17a-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="fd17a-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="fd17a-116">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myResourceGroup` w lokalizacji `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="fd17a-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="fd17a-117">Tworzenie serwera logicznego</span><span class="sxs-lookup"><span data-stu-id="fd17a-117">Create a logical server</span></span>

<span data-ttu-id="fd17a-118">Utwórz [serwer logiczny Azure SQL Database](sql-database-features.md) za pomocą polecenia [az sql server create](/cli/azure/sql/server#create).</span><span class="sxs-lookup"><span data-stu-id="fd17a-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="fd17a-119">Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="fd17a-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="fd17a-120">Poniższy przykład obejmuje tworzenie serwera o losowo wybranej nazwie w grupie zasobów za pomocą identyfikatora logowania administratora o nazwie `ServerAdmin` i z hasłem `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="fd17a-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="fd17a-121">Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="fd17a-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="fd17a-122">Konfigurowanie reguły zapory serwera</span><span class="sxs-lookup"><span data-stu-id="fd17a-122">Configure a server firewall rule</span></span>

<span data-ttu-id="fd17a-123">Utwórz [regułę zapory na poziomie serwera Azure SQL Database](sql-database-firewall-configure.md) za pomocą polecenia [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="fd17a-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="fd17a-124">Reguła zapory na poziomie serwera umożliwia zewnętrznej aplikacji, takiej jak SQL Server Management Studio lub narzędzie SQLCMD, nawiązanie połączenia z bazą danych SQL za pośrednictwem zapory usługi SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fd17a-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="fd17a-125">W poniższym przykładzie zapora jest otwarta tylko dla innych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd17a-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="fd17a-126">Aby włączyć łączność zewnętrzną, zmień adres IP na adres odpowiedni dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="fd17a-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="fd17a-127">Aby otworzyć wszystkie adresy IP, użyj wartości 0.0.0.0 jako początkowego adresu IP i wartości 255.255.255.255 jako adresu końcowego.</span><span class="sxs-lookup"><span data-stu-id="fd17a-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="fd17a-128">Usługa SQL Database nawiązuje komunikację na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="fd17a-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="fd17a-129">Jeśli próbujesz nawiązać połączenie z sieci firmowej, ruch wychodzący na porcie 1433 może być zablokowany przez firmową zaporę.</span><span class="sxs-lookup"><span data-stu-id="fd17a-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="fd17a-130">Jeśli zachodzi taka sytuacja, nie będzie można nawiązać połączenia z serwerem Azure SQL Database, chyba że dział IT otworzy port 1433.</span><span class="sxs-lookup"><span data-stu-id="fd17a-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="fd17a-131">Tworzenie na serwerze bazy danych z przykładowymi danymi</span><span class="sxs-lookup"><span data-stu-id="fd17a-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="fd17a-132">Utwórz bazę danych [o poziomie wydajności S0](sql-database-service-tiers.md) na serwerze za pomocą polecenia [az sql db create](/cli/azure/sql/db#create).</span><span class="sxs-lookup"><span data-stu-id="fd17a-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="fd17a-133">Poniższy przykład tworzy bazę danych o nazwie `mySampleDatabase` i ładuje do niej przykładowe dane AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="fd17a-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="fd17a-134">Zastąp te wstępnie zdefiniowane wartości zgodnie z potrzebami (inne przewodniki Szybki start w tej kolekcji bazują na wartościach z tego przewodnika).</span><span class="sxs-lookup"><span data-stu-id="fd17a-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="fd17a-135">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="fd17a-135">Clean up resources</span></span>

<span data-ttu-id="fd17a-136">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="fd17a-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="fd17a-137">Jeśli planujesz kontynuować pracę z kolejnymi przewodnikami Szybki start, nie usuwaj zasobów utworzonych w tym przewodniku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="fd17a-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="fd17a-138">Jeśli nie planujesz kontynuować pracy, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego szybkiego startu.</span><span class="sxs-lookup"><span data-stu-id="fd17a-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="fd17a-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd17a-139">Next steps</span></span>

<span data-ttu-id="fd17a-140">Teraz, gdy już masz bazę danych, możesz nawiązać z nią połączenie i uruchamiać zapytania za pomocą ulubionych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="fd17a-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="fd17a-141">Dowiedz się więcej, wybierając narzędzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="fd17a-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="fd17a-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="fd17a-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="fd17a-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fd17a-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="fd17a-144">.NET</span><span class="sxs-lookup"><span data-stu-id="fd17a-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="fd17a-145">PHP</span><span class="sxs-lookup"><span data-stu-id="fd17a-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="fd17a-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="fd17a-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="fd17a-147">Java</span><span class="sxs-lookup"><span data-stu-id="fd17a-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="fd17a-148">Python</span><span class="sxs-lookup"><span data-stu-id="fd17a-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="fd17a-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="fd17a-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

