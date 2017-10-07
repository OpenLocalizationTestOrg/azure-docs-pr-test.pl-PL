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
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Używanie Sqoop z platformą Hadoop w usłudze HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Dowiedz się, jak toouse Sqoop w HDInsight tooimport i eksportowanie między klastrem usługi HDInsight i bazy danych Azure SQL lub bazy danych SQL Server.

Mimo że Hadoop to fizyczne wybór przetwarzanie częściową strukturą i bez struktury danych, takie jak dzienniki i pliki, można również dane tooprocess strukturę potrzeby, które są przechowywane w relacyjnych baz danych.

[Sqoop] [ sqoop-user-guide-1.4.4] jest tootransfer narzędzie przeznaczone danych między klastrów platformy Hadoop a relacyjnymi bazami danych. Służy on tooimport danych z systemu zarządzania relacyjnymi bazami danych (RDBMS) takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed hello (HDFS), przekształcania danych hello w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować hello danych do RDBMS. W tym samouczku używasz bazy danych programu SQL Server relacyjnej bazy danych.

Dla wersji Sqoop, które są obsługiwane w klastrach HDInsight, zobacz [nowości w wersjach klastra hello dostarczanych z usługą HDInsight?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Zrozumienie hello scenariusza

Klaster usługi HDInsight jest dostarczany z przykładowymi danymi. Możesz użyć powitania po dwóch próbek:

* Plik dziennika log4j, który znajduje się pod adresem */example/data/sample.log*. powitania po dzienniki są wyodrębniane z pliku hello:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Tabeli programu Hive o nazwie *hivesampletable*, który odwołuje się do hello znajdujący się w pliku danych */hive/warehouse/hivesampletable*. Witaj tabela zawiera niektóre dane z urządzeń przenośnych. 
  
  | Pole | Typ danych |
  | --- | --- |
  | ClientID |Ciąg |
  | querytime |Ciąg |
  | rynku |Ciąg |
  | deviceplatform |Ciąg |
  | devicemake |Ciąg |
  | devicemodel |Ciąg |
  | state |Ciąg |
  | Kraju |Ciąg |
  | querydwelltime |O podwójnej precyzji |
  | Identyfikator sesji |bigint |
  | sessionpagevieworder |bigint |

Najpierw wyeksportować *sample.log* i *hivesampletable* toohello bazy danych Azure SQL lub tooSQL serwera, a następnie Importuj hello tabeli, która zawiera dane z urządzeń przenośnych hello kopii tooHDInsight za pomocą hello Następująca ścieżka:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Tworzenie klastra i bazy danych SQL
W tej sekcji przedstawiono, jak toocreate klastra, bazy danych SQL i hello schematów bazy danych SQL dla uruchomionego hello samouczka przy użyciu hello portalu Azure i szablonu usługi Azure Resource Manager. Szablon Hello znajdują się w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). Szablon usługi Resource Manager Hello wywołuje pliku bacpac pakietu toodeploy hello tabeli schematów tooSQL bazy danych.  Witaj pliku bacpac pakietu znajduje się w publicznym kontenerze obiektów blob, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Toouse Kontener prywatny hello pliku bacpac plików, należy użyć następującej wartości w szablonie hello hello:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Jeśli wolisz toouse programu Azure PowerShell toocreate hello klastra i hello bazy danych SQL, zobacz [dodatek a.](#appendix-a---a-powershell-sample).

1. Kliknij przycisk powitania po tooopen obrazu szablonu usługi Resource Manager w hello portalu Azure.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Wprowadź hello następujące właściwości:

    - **Subskrypcja**: Wprowadź subskrypcji platformy Azure.
    - **Grupa zasobów**: Utwórz nową grupę zasobów platformy Azure, lub wybierz istniejącą grupę zasobów.  Grupa zasobów to w celu zarządzania.  Jest to kontener dla obiektów.
    - **Lokalizacja**: Wybierz region.
    - **ClusterName**: Wprowadź nazwę klastra usługi Hadoop hello.
    - **Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania to admin.
    - **Nazwa użytkownika i hasło SSH**.
    - **Nazwa logowania serwera i hasło bazy danych SQL**.
    - **_artifacts lokalizacji**: Użyj wartości domyślnej hello, chyba że chcesz toouse własny plik backpac w innej lokalizacji.
    - **Token sygnatury dostępu współdzielonego lokalizacji _artifacts**: pozostaw to pole puste.
    - **Nazwa pliku pliku Bacpac**: Użyj wartości domyślnej hello, chyba że chcesz toouse pliku backpac.
     
     następujące wartości Hello są zapisane na stałe w sekcji zmiennych hello:
     
     | Domyślna nazwa konta magazynu | <CluterName>Magazyn |
     | --- | --- |
     | Nazwa serwera bazy danych SQL Azure |<ClusterName>dbserver |
     | Nazwa bazy danych SQL Azure |<ClusterName>bazy danych |
     
     Zapisz te wartości.  Należy je później w samouczku hello.

3. Kliknij przycisk **OK** toosave hello parametrów.

4 z hello **wdrożenie niestandardowe** bloku, kliknij przycisk **grupy zasobów** listy rozwijanej, a następnie kliknij przycisk **nowy** toocreate nową grupę zasobów. Witaj, grupy zasobów jest kontenerem, który grupuje klaster hello, hello zależne konto magazynu oraz inne powiązane zasoby.

5. Kliknij opcję **Postanowienia prawne**, a następnie kliknij przycisk **Utwórz**.

6. Kliknij przycisk **Utwórz**. Zostanie wyświetlony nowy Kafelek zatytułowany Submitting deployment dla wdrożenia szablonu. Trwa około 20 minut toocreate hello klastra i bazy danych SQL.

Jeśli wybierzesz toouse istniejącej bazy danych Azure SQL lub programu Microsoft SQL Server

* **Baza danych SQL Azure**: należy skonfigurować reguły zapory dla hello dostępu tooallow serwera bazy danych Azure SQL ze stacji roboczej. Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania zapory hello, zobacz [rozpocząć korzystanie z bazy danych Azure SQL][sqldatabase-get-started]. 
  
  > [!NOTE]
  > Domyślnie bazy danych Azure SQL umożliwia połączenia z usługami Azure, takich jak Azure HDInsight. Wyłączenie tego ustawienia zapory należy tooenable z hello portalu Azure. Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania reguł zapory, zobacz [tworzenie i Konfigurowanie bazy danych SQL][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: w przypadku klastra usługi HDInsight na powitania tej samej sieci wirtualnej na platformie Azure jako serwera SQL, można użyć hello kroków w tym artykule tooimport i eksportowanie danych tooa bazy danych SQL Server.
  
  > [!NOTE]
  > HDInsight obsługuje tylko na podstawie lokalizacji sieci wirtualnych, a jego obecnie nie współpracujesz z sieci wirtualne oparte na grupach koligacji.
  > 
  > 
  
  * toocreate i konfigurowanie sieci wirtualnej, zobacz [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * Jeśli używasz programu SQL Server w centrum danych, należy skonfigurować hello sieci wirtualnej co *lokacja lokacja* lub *punkt lokacja*.
      
      > [!NOTE]
      > Dla **punkt lokacja** sieci wirtualnych, programu SQL Server musi być uruchomiona powitania klienta VPN konfiguracji aplikacji, które są dostępne z hello **pulpitu nawigacyjnego** konfiguracji sieci wirtualnej platformy Azure.
      > 
      > 
    * Używając programu SQL Server na maszynie wirtualnej platformy Azure, żadnej konfiguracji sieci wirtualnej mogą być używane, gdy maszyna wirtualna hello hostowany program SQL Server jest członkiem hello tej samej sieci wirtualnej jako HDInsight.
  * toocreate klastra usługi HDInsight w sieci wirtualnej, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server należy także zezwolić uwierzytelniania. Należy użyć programu SQL Server hello toocomplete logowania kroków w tym artykule.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Uruchamianie zadań Sqoop
HDInsight można uruchamiać zadania Sqoop przy użyciu różnych metod. Użyj powitania po toodecide tabeli, która metoda jest odpowiednie dla Ciebie, a następnie wykonaj hello łącze, aby uzyskać wskazówki.

| **Użyj tej** Jeśli chcesz... | .. .an **interakcyjne** powłoki | ... **partii** przetwarzania | .. zwykle to **systemu operacyjnego klastra** | .. .from to **system operacyjny klienta** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X lub systemu Windows |
| [Zestaw SDK dla platformy .NET usługi Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux lub Windows |Systemu Windows (na razie) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux lub Windows |Windows |

## <a name="limitations"></a>Ograniczenia
* Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.
* Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop wykonuje wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.

## <a name="next-steps"></a>Następne kroki
Teraz wiesz już, jak toouse Sqoop. toolearn więcej, zobacz:

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystanie z usługą HDInsight Oozie][hdinsight-use-oozie]: Użyj Sqoop działań w przepływie pracy Oozie.
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]: Użyj Hive transmitowane tooanalyze opóźnienie danych, a następnie użyj bazy danych Azure SQL tooan Sqoop tooexport danych.
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]: znajdowanie innych metod do przekazywania danych tooHDInsight/usługi Azure Blob storage.

## <a name="appendix-a---a-powershell-sample"></a>Dodatek a. — przykład środowiska PowerShell
Przykładowe PowerShell Hello wykonuje hello następujące kroki:

1. Połącz tooAzure.
2. Utwórz grupę zasobów platformy Azure. Aby uzyskać więcej informacji, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)
3. Utwórz serwer bazy danych SQL Azure, bazy danych Azure SQL i dwie tabele. 
   
    Zamiast tego użyj programu SQL Server, należy użyć hello następujące instrukcje toocreate hello tabel:
   
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
   
    Witaj Najprostszym sposobem tooexamine hello bazy danych i tabele jest toouse programu Visual Studio. Witaj bazy danych serwera i bazy danych hello może sprawdzić za pomocą hello portalu Azure.
4. Tworzenie klastra usługi HDInsight.
   
    tooexamine hello klastra, można użyć hello portalu Azure lub programu Azure PowerShell.
5. Wstępnie przetworzyć hello źródłowego pliku danych.
   
    W tym samouczku możesz wyeksportować plik dziennika narzędzia log4j (rozdzielany plik) i bazy danych Azure SQL tooan tabeli Hive. Witaj rozdzielany plik jest nazywany */example/data/sample.log*. Wcześniej w samouczku hello widać kilka przykładów log4j dzienników. W pliku dziennika hello istnieją pewne puste wiersze i toothese podobne niektórych wierszy:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    To działa poprawnie na inne przykłady korzystających z tych danych, ale możemy było, należy usunąć te wyjątki możemy zaimportować hello Azure SQL database lub SQL Server. Eksport Sqoop zakończy się niepowodzeniem, jeśli jest ciągiem pustym ani wiersza z mniejszą elementów niż liczba hello pola zdefiniowane w tabeli bazy danych Azure SQL hello. Tabela log4jlogs Hello ma 7 pól typu ciąg.
   
    Ta procedura tworzy nowy plik w klastrze hello: tutorials/usesqoop/data/sample.log. tooexamine hello zmodyfikowane dane plików, można użyć hello portalu Azure, narzędzia Eksplorator magazynu Azure lub programu Azure PowerShell. [Rozpoczynanie pracy z usługą HDInsight] [ hdinsight-get-started] ma kod przykładowy dotyczące korzystania z programu Azure PowerShell toodownload pliku i wyświetlić zawartość pliku hello.
6. Eksportowanie bazy danych Azure SQL toohello pliku danych.
   
    plik źródłowy Hello jest tutorials/usesqoop/data/sample.log. gdzie danych hello jest wyeksportowany toois tabeli Hello o nazwie log4jlogs.
   
   > [!NOTE]
   > Inne niż informacje o parametrach połączenia kroki hello w tej sekcji powinny działać dla bazy danych Azure SQL lub programu SQL Server. Kroki te zostały przetestowane przy użyciu następującej konfiguracji hello:
   > 
   > * **Konfiguracja punktu do lokacji sieci wirtualnej platformy Azure**: hello HDInsight tooa klastra programu SQL Server w prywatnym centrum danych połączone sieci wirtualnej. Zobacz [skonfigurowania sieci VPN punkt-lokacja w portalu zarządzania hello](../vpn-gateway/vpn-gateway-point-to-site-create.md) Aby uzyskać więcej informacji.
   > * **Azure HDInsight 3.1**: zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md) informacji o tworzeniu klastra w sieci wirtualnej.
   > * **SQL Server 2014**: konfigurowane bezpiecznie tooallow uwierzytelniania i uruchomione hello VPN klienta konfiguracji pakietu tooconnect toohello sieci wirtualnej.
   > 
   > 
7. Eksportowanie bazy danych Azure SQL toohello tabeli Hive.
8. Importuj klastra usługi HDInsight toohello hello mobiledata tabeli.
   
    tooexamine hello zmodyfikowane dane plików, można użyć hello portalu Azure, narzędzia Eksplorator magazynu Azure lub programu Azure PowerShell.  [Rozpoczynanie pracy z usługą HDInsight] [ hdinsight-get-started] ma kod przykładowy o korzystaniu z programu Azure PowerShell toodownload pliku i wyświetlić zawartość pliku hello.

### <a name="hello-powershell-sample"></a>Przykładowe PowerShell Hello
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
