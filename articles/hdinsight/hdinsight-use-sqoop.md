---
title: "aaaRun Apache Sqoop zadania w usłudze Azure HDInsight (Hadoop) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse programu Azure PowerShell z toorun stacji roboczej Sqoop importowania i eksportowania między klastrem Hadoop i bazy danych Azure SQL."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="51543-103">Używanie Sqoop z platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="51543-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="51543-104">Dowiedz się, jak toouse Sqoop w HDInsight tooimport i eksportowanie między klastrem usługi HDInsight i bazy danych Azure SQL lub bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="51543-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="51543-105">Mimo że Hadoop to fizyczne wybór przetwarzanie częściową strukturą i bez struktury danych, takie jak dzienniki i pliki, można również dane tooprocess strukturę potrzeby, które są przechowywane w relacyjnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="51543-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="51543-106">[Sqoop] [ sqoop-user-guide-1.4.4] jest tootransfer narzędzie przeznaczone danych między klastrów platformy Hadoop a relacyjnymi bazami danych.</span><span class="sxs-lookup"><span data-stu-id="51543-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="51543-107">Służy on tooimport danych z systemu zarządzania relacyjnymi bazami danych (RDBMS) takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed hello (HDFS), przekształcania danych hello w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować hello danych do RDBMS.</span><span class="sxs-lookup"><span data-stu-id="51543-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="51543-108">W tym samouczku używasz bazy danych programu SQL Server relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="51543-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="51543-109">Dla wersji Sqoop, które są obsługiwane w klastrach HDInsight, zobacz [nowości w wersjach klastra hello dostarczanych z usługą HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="51543-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="51543-110">Zrozumienie hello scenariusza</span><span class="sxs-lookup"><span data-stu-id="51543-110">Understand hello scenario</span></span>

<span data-ttu-id="51543-111">Klaster usługi HDInsight jest dostarczany z przykładowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="51543-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="51543-112">Możesz użyć powitania po dwóch próbek:</span><span class="sxs-lookup"><span data-stu-id="51543-112">You use hello following two samples:</span></span>

* <span data-ttu-id="51543-113">Plik dziennika log4j, który znajduje się pod adresem */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="51543-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="51543-114">powitania po dzienniki są wyodrębniane z pliku hello:</span><span class="sxs-lookup"><span data-stu-id="51543-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="51543-115">Tabeli programu Hive o nazwie *hivesampletable*, który odwołuje się do hello znajdujący się w pliku danych */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="51543-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="51543-116">Witaj tabela zawiera niektóre dane z urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="51543-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="51543-117">Pole</span><span class="sxs-lookup"><span data-stu-id="51543-117">Field</span></span> | <span data-ttu-id="51543-118">Typ danych</span><span class="sxs-lookup"><span data-stu-id="51543-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="51543-119">ClientID</span><span class="sxs-lookup"><span data-stu-id="51543-119">clientid</span></span> |<span data-ttu-id="51543-120">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-120">string</span></span> |
  | <span data-ttu-id="51543-121">querytime</span><span class="sxs-lookup"><span data-stu-id="51543-121">querytime</span></span> |<span data-ttu-id="51543-122">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-122">string</span></span> |
  | <span data-ttu-id="51543-123">rynku</span><span class="sxs-lookup"><span data-stu-id="51543-123">market</span></span> |<span data-ttu-id="51543-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-124">string</span></span> |
  | <span data-ttu-id="51543-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="51543-125">deviceplatform</span></span> |<span data-ttu-id="51543-126">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-126">string</span></span> |
  | <span data-ttu-id="51543-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="51543-127">devicemake</span></span> |<span data-ttu-id="51543-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-128">string</span></span> |
  | <span data-ttu-id="51543-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="51543-129">devicemodel</span></span> |<span data-ttu-id="51543-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-130">string</span></span> |
  | <span data-ttu-id="51543-131">state</span><span class="sxs-lookup"><span data-stu-id="51543-131">state</span></span> |<span data-ttu-id="51543-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-132">string</span></span> |
  | <span data-ttu-id="51543-133">Kraju</span><span class="sxs-lookup"><span data-stu-id="51543-133">country</span></span> |<span data-ttu-id="51543-134">Ciąg</span><span class="sxs-lookup"><span data-stu-id="51543-134">string</span></span> |
  | <span data-ttu-id="51543-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="51543-135">querydwelltime</span></span> |<span data-ttu-id="51543-136">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="51543-136">double</span></span> |
  | <span data-ttu-id="51543-137">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="51543-137">sessionid</span></span> |<span data-ttu-id="51543-138">bigint</span><span class="sxs-lookup"><span data-stu-id="51543-138">bigint</span></span> |
  | <span data-ttu-id="51543-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="51543-139">sessionpagevieworder</span></span> |<span data-ttu-id="51543-140">bigint</span><span class="sxs-lookup"><span data-stu-id="51543-140">bigint</span></span> |

<span data-ttu-id="51543-141">Najpierw wyeksportować *sample.log* i *hivesampletable* toohello bazy danych Azure SQL lub tooSQL serwera, a następnie Importuj hello tabeli, która zawiera dane z urządzeń przenośnych hello kopii tooHDInsight za pomocą hello Następująca ścieżka:</span><span class="sxs-lookup"><span data-stu-id="51543-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="51543-142">Tworzenie klastra i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="51543-142">Create cluster and SQL database</span></span>
<span data-ttu-id="51543-143">W tej sekcji przedstawiono, jak toocreate klastra, bazy danych SQL i hello schematów bazy danych SQL dla uruchomionego hello samouczka przy użyciu hello portalu Azure i szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51543-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="51543-144">Szablon Hello znajdują się w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="51543-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="51543-145">Szablon usługi Resource Manager Hello wywołuje pliku bacpac pakietu toodeploy hello tabeli schematów tooSQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="51543-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="51543-146">Witaj pliku bacpac pakietu znajduje się w publicznym kontenerze obiektów blob, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="51543-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="51543-147">Toouse Kontener prywatny hello pliku bacpac plików, należy użyć następującej wartości w szablonie hello hello:</span><span class="sxs-lookup"><span data-stu-id="51543-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="51543-148">Jeśli wolisz toouse programu Azure PowerShell toocreate hello klastra i hello bazy danych SQL, zobacz [dodatek a.](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="51543-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="51543-149">Kliknij przycisk powitania po tooopen obrazu szablonu usługi Resource Manager w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="51543-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="51543-150">Wprowadź hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="51543-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="51543-151">**Subskrypcja**: Wprowadź subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51543-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="51543-152">**Grupa zasobów**: Utwórz nową grupę zasobów platformy Azure, lub wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="51543-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="51543-153">Grupa zasobów to w celu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="51543-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="51543-154">Jest to kontener dla obiektów.</span><span class="sxs-lookup"><span data-stu-id="51543-154">It is a container for objects.</span></span>
    - <span data-ttu-id="51543-155">**Lokalizacja**: Wybierz region.</span><span class="sxs-lookup"><span data-stu-id="51543-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="51543-156">**ClusterName**: Wprowadź nazwę klastra usługi Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="51543-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="51543-157">**Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania to admin.</span><span class="sxs-lookup"><span data-stu-id="51543-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="51543-158">**Nazwa użytkownika i hasło SSH**.</span><span class="sxs-lookup"><span data-stu-id="51543-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="51543-159">**Nazwa logowania serwera i hasło bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="51543-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="51543-160">**_artifacts lokalizacji**: Użyj wartości domyślnej hello, chyba że chcesz toouse własny plik backpac w innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="51543-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="51543-161">**Token sygnatury dostępu współdzielonego lokalizacji _artifacts**: pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="51543-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="51543-162">**Nazwa pliku pliku Bacpac**: Użyj wartości domyślnej hello, chyba że chcesz toouse pliku backpac.</span><span class="sxs-lookup"><span data-stu-id="51543-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="51543-163">następujące wartości Hello są zapisane na stałe w sekcji zmiennych hello:</span><span class="sxs-lookup"><span data-stu-id="51543-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="51543-164">Domyślna nazwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="51543-164">Default storage account name</span></span> | <span data-ttu-id="51543-165"><CluterName>Magazyn</span><span class="sxs-lookup"><span data-stu-id="51543-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="51543-166">Nazwa serwera bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="51543-166">Azure SQL database server name</span></span> |<span data-ttu-id="51543-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="51543-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="51543-168">Nazwa bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="51543-168">Azure SQL database name</span></span> |<span data-ttu-id="51543-169"><ClusterName>bazy danych</span><span class="sxs-lookup"><span data-stu-id="51543-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="51543-170">Zapisz te wartości.</span><span class="sxs-lookup"><span data-stu-id="51543-170">Please write down these values.</span></span>  <span data-ttu-id="51543-171">Należy je później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="51543-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="51543-172">3. Kliknij przycisk **OK** toosave hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="51543-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="51543-173">4 z hello **wdrożenie niestandardowe** bloku, kliknij przycisk **grupy zasobów** listy rozwijanej, a następnie kliknij przycisk **nowy** toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="51543-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="51543-174">Witaj, grupy zasobów jest kontenerem, który grupuje klaster hello, hello zależne konto magazynu oraz inne powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="51543-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="51543-175">5. Kliknij opcję **Postanowienia prawne**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="51543-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="51543-176">6. Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="51543-176">6.Click **Create**.</span></span> <span data-ttu-id="51543-177">Zostanie wyświetlony nowy Kafelek zatytułowany Submitting deployment dla wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="51543-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="51543-178">Trwa około 20 minut toocreate hello klastra i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="51543-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="51543-179">Jeśli wybierzesz toouse istniejącej bazy danych Azure SQL lub programu Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="51543-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="51543-180">**Baza danych SQL Azure**: należy skonfigurować reguły zapory dla hello dostępu tooallow serwera bazy danych Azure SQL ze stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="51543-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="51543-181">Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania zapory hello, zobacz [rozpocząć korzystanie z bazy danych Azure SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="51543-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="51543-182">Domyślnie bazy danych Azure SQL umożliwia połączenia z usługami Azure, takich jak Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51543-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="51543-183">Wyłączenie tego ustawienia zapory należy tooenable z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="51543-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="51543-184">Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania reguł zapory, zobacz [tworzenie i Konfigurowanie bazy danych SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="51543-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="51543-185">**SQL Server**: w przypadku klastra usługi HDInsight na powitania tej samej sieci wirtualnej na platformie Azure jako serwera SQL, można użyć hello kroków w tym artykule tooimport i eksportowanie danych tooa bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="51543-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="51543-186">HDInsight obsługuje tylko na podstawie lokalizacji sieci wirtualnych, a jego obecnie nie współpracujesz z sieci wirtualne oparte na grupach koligacji.</span><span class="sxs-lookup"><span data-stu-id="51543-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="51543-187">toocreate i konfigurowanie sieci wirtualnej, zobacz [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="51543-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="51543-188">Jeśli używasz programu SQL Server w centrum danych, należy skonfigurować hello sieci wirtualnej co *lokacja lokacja* lub *punkt lokacja*.</span><span class="sxs-lookup"><span data-stu-id="51543-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="51543-189">Dla **punkt lokacja** sieci wirtualnych, programu SQL Server musi być uruchomiona powitania klienta VPN konfiguracji aplikacji, które są dostępne z hello **pulpitu nawigacyjnego** konfiguracji sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51543-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="51543-190">Używając programu SQL Server na maszynie wirtualnej platformy Azure, żadnej konfiguracji sieci wirtualnej mogą być używane, gdy maszyna wirtualna hello hostowany program SQL Server jest członkiem hello tej samej sieci wirtualnej jako HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51543-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="51543-191">toocreate klastra usługi HDInsight w sieci wirtualnej, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="51543-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="51543-192">SQL Server należy także zezwolić uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="51543-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="51543-193">Należy użyć programu SQL Server hello toocomplete logowania kroków w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="51543-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="51543-194">Uruchamianie zadań Sqoop</span><span class="sxs-lookup"><span data-stu-id="51543-194">Run Sqoop jobs</span></span>
<span data-ttu-id="51543-195">HDInsight można uruchamiać zadania Sqoop przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="51543-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="51543-196">Użyj powitania po toodecide tabeli, która metoda jest odpowiednie dla Ciebie, a następnie wykonaj hello łącze, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="51543-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="51543-197">**Użyj tej** Jeśli chcesz...</span><span class="sxs-lookup"><span data-stu-id="51543-197">**Use this** if you want...</span></span> | <span data-ttu-id="51543-198">.. .an **interakcyjne** powłoki</span><span class="sxs-lookup"><span data-stu-id="51543-198">...an **interactive** shell</span></span> | <span data-ttu-id="51543-199">... **partii** przetwarzania</span><span class="sxs-lookup"><span data-stu-id="51543-199">...**batch** processing</span></span> | <span data-ttu-id="51543-200">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="51543-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="51543-201">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="51543-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="51543-202">SSH</span><span class="sxs-lookup"><span data-stu-id="51543-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="51543-203">✔</span><span class="sxs-lookup"><span data-stu-id="51543-203">✔</span></span> |<span data-ttu-id="51543-204">✔</span><span class="sxs-lookup"><span data-stu-id="51543-204">✔</span></span> |<span data-ttu-id="51543-205">Linux</span><span class="sxs-lookup"><span data-stu-id="51543-205">Linux</span></span> |<span data-ttu-id="51543-206">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="51543-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="51543-207">Zestaw SDK dla platformy .NET usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="51543-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="51543-208">✔</span><span class="sxs-lookup"><span data-stu-id="51543-208">✔</span></span> |<span data-ttu-id="51543-209">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="51543-209">Linux or Windows</span></span> |<span data-ttu-id="51543-210">Systemu Windows (na razie)</span><span class="sxs-lookup"><span data-stu-id="51543-210">Windows (for now)</span></span> |
| [<span data-ttu-id="51543-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="51543-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="51543-212">✔</span><span class="sxs-lookup"><span data-stu-id="51543-212">✔</span></span> |<span data-ttu-id="51543-213">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="51543-213">Linux or Windows</span></span> |<span data-ttu-id="51543-214">Windows</span><span class="sxs-lookup"><span data-stu-id="51543-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="51543-215">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="51543-215">Limitations</span></span>
* <span data-ttu-id="51543-216">Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="51543-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="51543-217">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop wykonuje wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="51543-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51543-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51543-218">Next steps</span></span>
<span data-ttu-id="51543-219">Teraz wiesz już, jak toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="51543-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="51543-220">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="51543-220">toolearn more, see:</span></span>

* [<span data-ttu-id="51543-221">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="51543-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="51543-222">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="51543-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="51543-223">[Korzystanie z usługą HDInsight Oozie][hdinsight-use-oozie]: Użyj Sqoop działań w przepływie pracy Oozie.</span><span class="sxs-lookup"><span data-stu-id="51543-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="51543-224">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]: Użyj Hive transmitowane tooanalyze opóźnienie danych, a następnie użyj bazy danych Azure SQL tooan Sqoop tooexport danych.</span><span class="sxs-lookup"><span data-stu-id="51543-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="51543-225">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]: znajdowanie innych metod do przekazywania danych tooHDInsight/usługi Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="51543-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="51543-226">Dodatek a. — przykład środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="51543-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="51543-227">Przykładowe PowerShell Hello wykonuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="51543-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="51543-228">Połącz tooAzure.</span><span class="sxs-lookup"><span data-stu-id="51543-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="51543-229">Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51543-229">Create an Azure resource group.</span></span> <span data-ttu-id="51543-230">Aby uzyskać więcej informacji, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="51543-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="51543-231">Utwórz serwer bazy danych SQL Azure, bazy danych Azure SQL i dwie tabele.</span><span class="sxs-lookup"><span data-stu-id="51543-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="51543-232">Zamiast tego użyj programu SQL Server, należy użyć hello następujące instrukcje toocreate hello tabel:</span><span class="sxs-lookup"><span data-stu-id="51543-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="51543-233">Witaj Najprostszym sposobem tooexamine hello bazy danych i tabele jest toouse programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51543-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="51543-234">Witaj bazy danych serwera i bazy danych hello może sprawdzić za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="51543-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="51543-235">Tworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51543-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="51543-236">tooexamine hello klastra, można użyć hello portalu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51543-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="51543-237">Wstępnie przetworzyć hello źródłowego pliku danych.</span><span class="sxs-lookup"><span data-stu-id="51543-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="51543-238">W tym samouczku możesz wyeksportować plik dziennika narzędzia log4j (rozdzielany plik) i bazy danych Azure SQL tooan tabeli Hive.</span><span class="sxs-lookup"><span data-stu-id="51543-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="51543-239">Witaj rozdzielany plik jest nazywany */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="51543-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="51543-240">Wcześniej w samouczku hello widać kilka przykładów log4j dzienników.</span><span class="sxs-lookup"><span data-stu-id="51543-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="51543-241">W pliku dziennika hello istnieją pewne puste wiersze i toothese podobne niektórych wierszy:</span><span class="sxs-lookup"><span data-stu-id="51543-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="51543-242">To działa poprawnie na inne przykłady korzystających z tych danych, ale możemy było, należy usunąć te wyjątki możemy zaimportować hello Azure SQL database lub SQL Server.</span><span class="sxs-lookup"><span data-stu-id="51543-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="51543-243">Eksport Sqoop zakończy się niepowodzeniem, jeśli jest ciągiem pustym ani wiersza z mniejszą elementów niż liczba hello pola zdefiniowane w tabeli bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="51543-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="51543-244">Tabela log4jlogs Hello ma 7 pól typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="51543-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="51543-245">Ta procedura tworzy nowy plik w klastrze hello: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="51543-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="51543-246">tooexamine hello zmodyfikowane dane plików, można użyć hello portalu Azure, narzędzia Eksplorator magazynu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51543-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="51543-247">[Rozpoczynanie pracy z usługą HDInsight] [ hdinsight-get-started] ma kod przykładowy dotyczące korzystania z programu Azure PowerShell toodownload pliku i wyświetlić zawartość pliku hello.</span><span class="sxs-lookup"><span data-stu-id="51543-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="51543-248">Eksportowanie bazy danych Azure SQL toohello pliku danych.</span><span class="sxs-lookup"><span data-stu-id="51543-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="51543-249">plik źródłowy Hello jest tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="51543-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="51543-250">gdzie danych hello jest wyeksportowany toois tabeli Hello o nazwie log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="51543-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="51543-251">Inne niż informacje o parametrach połączenia kroki hello w tej sekcji powinny działać dla bazy danych Azure SQL lub programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="51543-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="51543-252">Kroki te zostały przetestowane przy użyciu następującej konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="51543-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="51543-253">**Konfiguracja punktu do lokacji sieci wirtualnej platformy Azure**: hello HDInsight tooa klastra programu SQL Server w prywatnym centrum danych połączone sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51543-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="51543-254">Zobacz [skonfigurowania sieci VPN punkt-lokacja w portalu zarządzania hello](../vpn-gateway/vpn-gateway-point-to-site-create.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="51543-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="51543-255">**Azure HDInsight 3.1**: zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md) informacji o tworzeniu klastra w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51543-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="51543-256">**SQL Server 2014**: konfigurowane bezpiecznie tooallow uwierzytelniania i uruchomione hello VPN klienta konfiguracji pakietu tooconnect toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51543-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="51543-257">Eksportowanie bazy danych Azure SQL toohello tabeli Hive.</span><span class="sxs-lookup"><span data-stu-id="51543-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="51543-258">Importuj klastra usługi HDInsight toohello hello mobiledata tabeli.</span><span class="sxs-lookup"><span data-stu-id="51543-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="51543-259">tooexamine hello zmodyfikowane dane plików, można użyć hello portalu Azure, narzędzia Eksplorator magazynu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51543-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="51543-260">[Rozpoczynanie pracy z usługą HDInsight] [ hdinsight-get-started] ma kod przykładowy o korzystaniu z programu Azure PowerShell toodownload pliku i wyświetlić zawartość pliku hello.</span><span class="sxs-lookup"><span data-stu-id="51543-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="51543-261">Przykładowe PowerShell Hello</span><span class="sxs-lookup"><span data-stu-id="51543-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
