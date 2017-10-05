---
title: "Uruchamianie zadań Apache Sqoop w usłudze Azure HDInsight (Hadoop) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać programu Azure PowerShell na stacji roboczej uruchom Sqoop importowania i eksportowania między klastrem Hadoop i bazy danych Azure SQL."
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
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="9b7d3-103">Używanie Sqoop z platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b7d3-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="9b7d3-104">Dowiedz się, jak używać Sqoop w usłudze HDInsight umożliwia importowanie i eksportowanie między klastrem usługi HDInsight i bazy danych Azure SQL lub bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="9b7d3-105">Mimo że Hadoop to fizyczne wybór przetwarzanie częściową strukturą i bez struktury danych, takie jak dzienniki i pliki, może również być potrzebne do przetwarzania danych strukturalnych, który jest przechowywany w relacyjnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="9b7d3-106">[Sqoop] [ sqoop-user-guide-1.4.4] to narzędzie przeznaczone do transferu danych między klastrów platformy Hadoop a relacyjnymi bazami danych.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="9b7d3-107">Można go użyć do importowania danych z systemu zarządzania relacyjnymi bazami danych (RDBMS), takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed (HDFS), Przekształć dane w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować dane do RDBMS.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="9b7d3-108">W tym samouczku używasz bazy danych programu SQL Server relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="9b7d3-109">Dla wersji Sqoop, które są obsługiwane w klastrach HDInsight, zobacz [nowości w wersjach klastra dostarczanych z usługą HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="9b7d3-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="9b7d3-110">Zrozumienie tego scenariusza</span><span class="sxs-lookup"><span data-stu-id="9b7d3-110">Understand the scenario</span></span>

<span data-ttu-id="9b7d3-111">Klaster usługi HDInsight jest dostarczany z przykładowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="9b7d3-112">Można użyć następujących dwóch próbek:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-112">You use the following two samples:</span></span>

* <span data-ttu-id="9b7d3-113">Plik dziennika log4j, który znajduje się pod adresem */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="9b7d3-114">Następujące dzienniki są wyodrębniane z pliku:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="9b7d3-115">Tabeli programu Hive o nazwie *hivesampletable*, który znajduje się w pliku danych odwołuje się do */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="9b7d3-116">Tabela zawiera niektóre dane z urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="9b7d3-117">Pole</span><span class="sxs-lookup"><span data-stu-id="9b7d3-117">Field</span></span> | <span data-ttu-id="9b7d3-118">Typ danych</span><span class="sxs-lookup"><span data-stu-id="9b7d3-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="9b7d3-119">ClientID</span><span class="sxs-lookup"><span data-stu-id="9b7d3-119">clientid</span></span> |<span data-ttu-id="9b7d3-120">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-120">string</span></span> |
  | <span data-ttu-id="9b7d3-121">querytime</span><span class="sxs-lookup"><span data-stu-id="9b7d3-121">querytime</span></span> |<span data-ttu-id="9b7d3-122">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-122">string</span></span> |
  | <span data-ttu-id="9b7d3-123">rynku</span><span class="sxs-lookup"><span data-stu-id="9b7d3-123">market</span></span> |<span data-ttu-id="9b7d3-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-124">string</span></span> |
  | <span data-ttu-id="9b7d3-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="9b7d3-125">deviceplatform</span></span> |<span data-ttu-id="9b7d3-126">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-126">string</span></span> |
  | <span data-ttu-id="9b7d3-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="9b7d3-127">devicemake</span></span> |<span data-ttu-id="9b7d3-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-128">string</span></span> |
  | <span data-ttu-id="9b7d3-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="9b7d3-129">devicemodel</span></span> |<span data-ttu-id="9b7d3-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-130">string</span></span> |
  | <span data-ttu-id="9b7d3-131">state</span><span class="sxs-lookup"><span data-stu-id="9b7d3-131">state</span></span> |<span data-ttu-id="9b7d3-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-132">string</span></span> |
  | <span data-ttu-id="9b7d3-133">Kraju</span><span class="sxs-lookup"><span data-stu-id="9b7d3-133">country</span></span> |<span data-ttu-id="9b7d3-134">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b7d3-134">string</span></span> |
  | <span data-ttu-id="9b7d3-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="9b7d3-135">querydwelltime</span></span> |<span data-ttu-id="9b7d3-136">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="9b7d3-136">double</span></span> |
  | <span data-ttu-id="9b7d3-137">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="9b7d3-137">sessionid</span></span> |<span data-ttu-id="9b7d3-138">bigint</span><span class="sxs-lookup"><span data-stu-id="9b7d3-138">bigint</span></span> |
  | <span data-ttu-id="9b7d3-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="9b7d3-139">sessionpagevieworder</span></span> |<span data-ttu-id="9b7d3-140">bigint</span><span class="sxs-lookup"><span data-stu-id="9b7d3-140">bigint</span></span> |

<span data-ttu-id="9b7d3-141">Najpierw wyeksportować *sample.log* i *hivesampletable* do bazy danych Azure SQL lub programu SQL Server, a następnie zaimportuj tabelę, która zawiera dane z urządzeń przenośnych z powrotem do usługi HDInsight przy użyciu następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="9b7d3-142">Tworzenie klastra i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="9b7d3-142">Create cluster and SQL database</span></span>
<span data-ttu-id="9b7d3-143">W tej sekcji przedstawiono sposób tworzenia klastra, bazy danych SQL i schematów bazy danych SQL do uruchamiania tego samouczka przy użyciu portalu Azure i szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="9b7d3-144">Szablon można znaleźć w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="9b7d3-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="9b7d3-145">Szablon usługi Resource Manager wymaga pliku bacpac pakiet do wdrożenia schematy tabeli z bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="9b7d3-146">Pakiet pliku bacpac znajduje się w publicznym kontenerze obiektów blob, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="9b7d3-147">Jeśli chcesz użyć kontenera prywatne dla pliku bacpac plików, użyj następujących wartości w szablonie:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="9b7d3-148">Jeśli wolisz korzystać z programu Azure PowerShell do tworzenia klastra i bazy danych SQL, zobacz [dodatek a.](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="9b7d3-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="9b7d3-149">Kliknij poniższy obraz, aby otworzyć szablon Menedżera zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="9b7d3-150">Wprowadź następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-150">Enter the following properties:</span></span>

    - <span data-ttu-id="9b7d3-151">**Subskrypcja**: Wprowadź subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="9b7d3-152">**Grupa zasobów**: Utwórz nową grupę zasobów platformy Azure, lub wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="9b7d3-153">Grupa zasobów to w celu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="9b7d3-154">Jest to kontener dla obiektów.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-154">It is a container for objects.</span></span>
    - <span data-ttu-id="9b7d3-155">**Lokalizacja**: Wybierz region.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="9b7d3-156">**ClusterName**: Wprowadź nazwę klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="9b7d3-157">**Nazwa logowania i hasło klastra**: domyślna nazwa logowania to admin.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="9b7d3-158">**Nazwa użytkownika i hasło SSH**.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="9b7d3-159">**Nazwa logowania serwera i hasło bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="9b7d3-160">**_artifacts lokalizacji**: Użyj wartości domyślnej, chyba że chcesz użyć pliku backpac w innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="9b7d3-161">**Token sygnatury dostępu współdzielonego lokalizacji _artifacts**: pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="9b7d3-162">**Nazwa pliku pliku Bacpac**: Użyj wartości domyślnej, chyba że chcesz użyć pliku backpac.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="9b7d3-163">Zapisane na stałe w sekcji zmiennych są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="9b7d3-164">Domyślna nazwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="9b7d3-164">Default storage account name</span></span> | <span data-ttu-id="9b7d3-165"><CluterName>Magazyn</span><span class="sxs-lookup"><span data-stu-id="9b7d3-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="9b7d3-166">Nazwa serwera bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9b7d3-166">Azure SQL database server name</span></span> |<span data-ttu-id="9b7d3-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="9b7d3-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="9b7d3-168">Nazwa bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9b7d3-168">Azure SQL database name</span></span> |<span data-ttu-id="9b7d3-169"><ClusterName>bazy danych</span><span class="sxs-lookup"><span data-stu-id="9b7d3-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="9b7d3-170">Zapisz te wartości.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-170">Please write down these values.</span></span>  <span data-ttu-id="9b7d3-171">Będą potrzebne później podczas korzystania z samouczka.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="9b7d3-172">3. Kliknij przycisk **OK**, aby zapisać parametry.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="9b7d3-173">4. W bloku **Wdrożenie niestandardowe** kliknij pole listy rozwijanej **Grupa zasobów**, a następnie kliknij przycisk **Nowa**, aby utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="9b7d3-174">Grupa zasobów jest kontenerem, który grupuje klaster, zależne konto magazynu oraz inne powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="9b7d3-175">5. Kliknij opcję **Postanowienia prawne**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="9b7d3-176">6. Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-176">6.Click **Create**.</span></span> <span data-ttu-id="9b7d3-177">Zostanie wyświetlony nowy Kafelek zatytułowany Submitting deployment dla wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="9b7d3-178">Utworzenie klastra i bazy danych SQL trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="9b7d3-179">Jeśli chcesz użyć istniejącej bazy danych Azure SQL lub programu Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="9b7d3-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="9b7d3-180">**Baza danych SQL Azure**: należy skonfigurować reguły zapory dla serwera bazy danych Azure SQL, aby umożliwić dostęp ze stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="9b7d3-181">Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania zapory, zobacz [rozpocząć korzystanie z bazy danych Azure SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="9b7d3-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="9b7d3-182">Domyślnie bazy danych Azure SQL umożliwia połączenia z usługami Azure, takich jak Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="9b7d3-183">Wyłączenie tego ustawienia zapory, należy ją włączyć w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="9b7d3-184">Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania reguł zapory, zobacz [tworzenie i Konfigurowanie bazy danych SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="9b7d3-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="9b7d3-185">**SQL Server**: z klastrem usługi HDInsight znajduje się w tej samej sieci wirtualnej na platformie Azure jako serwera SQL, można użyć kroki opisane w tym artykule, umożliwia importowanie i eksportowanie danych do bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9b7d3-186">HDInsight obsługuje tylko na podstawie lokalizacji sieci wirtualnych, a jego obecnie nie współpracujesz z sieci wirtualne oparte na grupach koligacji.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="9b7d3-187">Aby utworzyć i skonfigurować sieć wirtualną, zobacz [utworzyć sieć wirtualną przy użyciu portalu Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="9b7d3-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="9b7d3-188">Jeśli używasz programu SQL Server w centrum danych, należy skonfigurować sieci wirtualnej co *lokacja lokacja* lub *punkt lokacja*.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="9b7d3-189">Dla **punkt lokacja** sieci wirtualnych, programu SQL Server musi być uruchomiona klienta sieci VPN konfiguracji aplikacji, które są dostępne z **pulpitu nawigacyjnego** konfiguracji sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="9b7d3-190">Używając programu SQL Server na maszynie wirtualnej platformy Azure, żadnej konfiguracji sieci wirtualnej umożliwia maszynie wirtualnej hostowany program SQL Server jest członkiem tej samej sieci wirtualnej jako HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="9b7d3-191">Aby utworzyć klaster usługi HDInsight w sieci wirtualnej, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="9b7d3-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9b7d3-192">SQL Server należy także zezwolić uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="9b7d3-193">Aby wykonać kroki opisane w tym artykule, należy użyć identyfikatora logowania programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="9b7d3-194">Uruchamianie zadań Sqoop</span><span class="sxs-lookup"><span data-stu-id="9b7d3-194">Run Sqoop jobs</span></span>
<span data-ttu-id="9b7d3-195">HDInsight można uruchamiać zadania Sqoop przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="9b7d3-196">Skorzystaj z poniższej tabeli do określania, która metoda jest odpowiednie dla Ciebie, a następnie kliknij link, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="9b7d3-197">**Użyj tej** Jeśli chcesz...</span><span class="sxs-lookup"><span data-stu-id="9b7d3-197">**Use this** if you want...</span></span> | <span data-ttu-id="9b7d3-198">.. .an **interakcyjne** powłoki</span><span class="sxs-lookup"><span data-stu-id="9b7d3-198">...an **interactive** shell</span></span> | <span data-ttu-id="9b7d3-199">... **partii** przetwarzania</span><span class="sxs-lookup"><span data-stu-id="9b7d3-199">...**batch** processing</span></span> | <span data-ttu-id="9b7d3-200">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="9b7d3-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="9b7d3-201">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="9b7d3-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="9b7d3-202">SSH</span><span class="sxs-lookup"><span data-stu-id="9b7d3-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="9b7d3-203">✔</span><span class="sxs-lookup"><span data-stu-id="9b7d3-203">✔</span></span> |<span data-ttu-id="9b7d3-204">✔</span><span class="sxs-lookup"><span data-stu-id="9b7d3-204">✔</span></span> |<span data-ttu-id="9b7d3-205">Linux</span><span class="sxs-lookup"><span data-stu-id="9b7d3-205">Linux</span></span> |<span data-ttu-id="9b7d3-206">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="9b7d3-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9b7d3-207">Zestaw SDK dla platformy .NET usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="9b7d3-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="9b7d3-208">✔</span><span class="sxs-lookup"><span data-stu-id="9b7d3-208">✔</span></span> |<span data-ttu-id="9b7d3-209">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="9b7d3-209">Linux or Windows</span></span> |<span data-ttu-id="9b7d3-210">Systemu Windows (na razie)</span><span class="sxs-lookup"><span data-stu-id="9b7d3-210">Windows (for now)</span></span> |
| [<span data-ttu-id="9b7d3-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7d3-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="9b7d3-212">✔</span><span class="sxs-lookup"><span data-stu-id="9b7d3-212">✔</span></span> |<span data-ttu-id="9b7d3-213">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="9b7d3-213">Linux or Windows</span></span> |<span data-ttu-id="9b7d3-214">Windows</span><span class="sxs-lookup"><span data-stu-id="9b7d3-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="9b7d3-215">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="9b7d3-215">Limitations</span></span>
* <span data-ttu-id="9b7d3-216">Zbiorcze export - opartych na systemie Linux z usługi HDInsight, łącznik Sqoop, używany do eksportowania danych do programu Microsoft SQL Server lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="9b7d3-217">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop wykonuje wiele operacji wstawienia zamiast przetwarzanie wsadowe operacji insert.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b7d3-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b7d3-218">Next steps</span></span>
<span data-ttu-id="9b7d3-219">Teraz ma przedstawiono sposób używania Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="9b7d3-220">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-220">To learn more, see:</span></span>

* [<span data-ttu-id="9b7d3-221">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b7d3-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9b7d3-222">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b7d3-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="9b7d3-223">[Korzystanie z usługą HDInsight Oozie][hdinsight-use-oozie]: Użyj Sqoop działań w przepływie pracy Oozie.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="9b7d3-224">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]: Użyj gałąź rejestru, aby transmitowane analizować opóźnienie danych, a następnie użyj Sqoop eksportować dane do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="9b7d3-225">[Przekazywanie danych do usługi HDInsight][hdinsight-upload-data]: znajdowanie innych metod do przekazywania danych do magazynu obiektów Blob HDInsight/Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="9b7d3-226">Dodatek a. — przykład środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7d3-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="9b7d3-227">Przykładowe PowerShell wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="9b7d3-228">Połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-228">Connect to Azure.</span></span>
2. <span data-ttu-id="9b7d3-229">Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-229">Create an Azure resource group.</span></span> <span data-ttu-id="9b7d3-230">Aby uzyskać więcej informacji, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9b7d3-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="9b7d3-231">Utwórz serwer bazy danych SQL Azure, bazy danych Azure SQL i dwie tabele.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="9b7d3-232">Jeśli zamiast tego użyj programu SQL Server umożliwia tworzenie tabel następujące instrukcje:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
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
   
    <span data-ttu-id="9b7d3-233">Najprostszym sposobem Sprawdź, czy baza danych i tabele jest używać programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="9b7d3-234">Serwer bazy danych i bazy danych można zbadać za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="9b7d3-235">Tworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="9b7d3-236">Aby zbadać klastra, można użyć portalu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="9b7d3-237">Wstępnie przetworzyć plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="9b7d3-238">W tym samouczku możesz wyeksportować plik dziennika narzędzia log4j (rozdzielany plik) i tabeli programu Hive z bazą danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="9b7d3-239">Rozdzielany plik jest nazywany */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="9b7d3-240">Kilka przykładów log4j dzienników widać wcześniej w samouczku.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="9b7d3-241">W pliku dziennika istnieją pewne puste wiersze i wiersze podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="9b7d3-242">Jest to poprawnie inne przykłady korzystających z tych danych, ale możemy było, należy usunąć te wyjątki można zaimportować do bazy danych Azure SQL lub programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="9b7d3-243">Eksport Sqoop zakończy się niepowodzeniem, jeśli jest ciągiem pustym ani wiersza z mniejszą elementów niż liczba pól zdefiniowanych w tabeli bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="9b7d3-244">Tabela log4jlogs zawiera 7 pola typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="9b7d3-245">Ta procedura tworzy nowy plik w klastrze: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="9b7d3-246">Do modyfikacji danych w pliku można użyć portalu Azure, narzędzia do Eksploratora magazynu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="9b7d3-247">[Rozpoczynanie pracy z usługą HDInsight] [ hdinsight-get-started] zawiera przykładowy kod do pobierania pliku i wyświetlić zawartość pliku przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="9b7d3-248">Eksportuj plik danych do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="9b7d3-249">Plik źródłowy jest tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="9b7d3-250">Tabela, w którym dane są eksportowane do nosi nazwę log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9b7d3-251">Inne niż informacje o parametrach połączenia kroki opisane w tej sekcji powinny działać dla bazy danych Azure SQL lub programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="9b7d3-252">Kroki te zostały przetestowane przy użyciu następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="9b7d3-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="9b7d3-253">**Konfiguracja punktu do lokacji sieci wirtualnej platformy Azure**: sieci wirtualnej połączenia klastra usługi HDInsight do programu SQL Server w prywatnym centrum danych.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="9b7d3-254">Zobacz [skonfigurowania sieci VPN punkt-lokacja w portalu zarządzania](../vpn-gateway/vpn-gateway-point-to-site-create.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="9b7d3-255">**Azure HDInsight 3.1**: zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md) informacji o tworzeniu klastra w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="9b7d3-256">**SQL Server 2014**: skonfigurowanych umożliwia uwierzytelnianie i uruchamianie klienta VPN pakiet konfiguracji do nawiązania bezpiecznego sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="9b7d3-257">Eksportowanie tabeli programu Hive z bazą danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="9b7d3-258">Importowanie tabeli mobiledata w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="9b7d3-259">Do modyfikacji danych w pliku można użyć portalu Azure, narzędzia do Eksploratora magazynu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="9b7d3-260">[Rozpoczynanie pracy z usługą HDInsight] [ hdinsight-get-started] ma próbki kodu o pobranie pliku i wyświetlić zawartość pliku za pomocą programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b7d3-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="9b7d3-261">Przykładowe programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7d3-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
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
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
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

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

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
