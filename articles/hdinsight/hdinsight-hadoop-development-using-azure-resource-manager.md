---
title: "narzędzia tooAzure aaaMigrate Menedżera zasobów dla usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Jak narzędzia tooAzure toomigrate programowanie Menedżera zasobów dla klastrów usługi HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Migrowanie tooAzure narzędzi programistycznych opartych na Menedżera zasobów dla klastrów usługi HDInsight

HDInsight wycofano narzędzi Azure Service Manager ASM dla usługi HDInsight. Jeśli był używany programu Azure PowerShell, interfejsu wiersza polecenia Azure lub hello zestawu .NET SDK HDInsight toowork z klastrami usługi HDInsight, to toouse zachęca hello Azure Resource Manager ARM-bitowego programu PowerShell, interfejsu wiersza polecenia i zestawu .NET SDK w przyszłości. Ten artykuł zawiera wskaźniki dotyczące toomigrate toohello nowe opartego na architekturze ARM podejście. Wszędzie tam, gdzie ma to zastosowanie, w tym artykule jest także punktów hello różnic między hello ASM i ARM podejścia dla usługi HDInsight.

> [!IMPORTANT]
> Hello obsługę funkcji ASM programu PowerShell, interfejsu wiersza polecenia, jak i zestawu .NET SDK nie będzie kontynuowane na **1 stycznia 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Migrowanie tooAzure interfejsu wiersza polecenia Azure Resource Manager
Hello Azure CLI teraz domyślne tooAzure tryb Resource Manager (ARM), chyba że w przypadku uaktualniania z poprzedniej instalacji; w takim przypadku należy toouse hello `azure config mode arm` tryb tooARM tooswitch polecenia.

podstawowe polecenia Hello tego wiersza polecenia platformy Azure z usługą HDInsight przy użyciu usługi Azure Service Management (ASM) pod warunkiem toowork hello są takie same hello podczas przy użyciu programu ARM; Jednak niektóre parametry i przełączników mogą mieć nowych nazw, a dostępnych wiele nowych parametrów podczas przy użyciu programu ARM. Na przykład może teraz użyć `azure hdinsight cluster create` toospecify hello Azure Virtual Network, powinny zostać utworzone w klastrze lub Hive i informacji na potrzeby magazynu metadanych Oozie.

Dostępne są następujące podstawowe polecenia do pracy z usługą HDInsight przy użyciu usługi Azure Resource Manager:

* `azure hdinsight cluster create`-Tworzy nowy klaster usługi HDInsight
* `azure hdinsight cluster delete`— Usuwa istniejącego klastra usługi HDInsight
* `azure hdinsight cluster show`-wyświetlać informacje na temat istniejącego klastra
* `azure hdinsight cluster list`— Wyświetla klastrów usługi HDInsight dla subskrypcji platformy Azure

Użyj hello `-h` przełącznika tooinspect hello parametry i opcje dostępne dla każdego polecenia.

### <a name="new-commands"></a>Nowe polecenia
Są dostępne z usługi Azure Resource Manager nowego polecenia:

* `azure hdinsight cluster resize`-dynamicznie zmiany hello liczba węzłów procesu roboczego w klastrze hello
* `azure hdinsight cluster enable-http-access`— Umożliwia klastra toohello dostępu protokołu HTTPs (na domyślne)
* `azure hdinsight cluster disable-http-access`— Wyłącza HTTPs dostęp toohello klastra
* `azure hdinsight script-action`-Zawiera polecenia służące do tworzenia/Zarządzanie akcji skryptu w klastrze
* `azure hdinsight config`-Zawiera polecenia służące do tworzenia pliku konfiguracji, który może być używany z hello `hdinsight cluster create` polecenia tooprovide informacje o konfiguracji.

### <a name="deprecated-commands"></a>Przestarzałe poleceń
Jeśli używasz hello `azure hdinsight job` tooyour klastra usługi HDInsight polecenia toosubmit zadań, nie są one dostępne za pośrednictwem hello poleceń ARM. Tooprogrammatically przesyłania zadań tooHDInsight ze skryptów, należy zamiast tego należy używać hello dostarczanych z usługą HDInsight interfejsów API REST. Aby uzyskać więcej informacji na przesyłanie zadań przy użyciu interfejsów API REST zobacz następujące dokumenty hello.

* [Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu cURL](hdinsight-hadoop-use-mapreduce-curl.md)
* [Uruchamianie zapytań Hive z usługą Hadoop w usłudze HDInsight przy użyciu programu cURL](hdinsight-hadoop-use-hive-curl.md)
* [Uruchamianie zadań Pig z usługą Hadoop w usłudze HDInsight przy użyciu programu cURL](hdinsight-hadoop-use-pig-curl.md)

Aby informacji na temat innych sposobów toorun MapReduce, Hive i wieprzowa interaktywnego, zobacz [Użyj MapReduce z Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md), [używanie Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md), i [Use Pig z platformą Hadoop w HDInsight](hdinsight-use-pig.md).

### <a name="examples"></a>Przykłady
**Tworzenie klastra**

* Polecenie stary (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Nowe polecenie (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Usuwanie klastra**

* Polecenie stary (ASM)-`azure hdinsight cluster delete myhdicluster`
* Nowe polecenie (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`

**Lista klastrów**

* Polecenie stary (ASM)-`azure hdinsight cluster list`
* Nowe polecenie (ARM)-`azure hdinsight cluster list`

> [!NOTE]
> Dla polecenia listy hello, określając hello grupy zasobów przy użyciu `-g` zwróci tylko klastry hello w hello określonej grupy zasobów.
> 
> 

**Pokaż informacje o klastrze**

* Polecenie stary (ASM)-`azure hdinsight cluster show myhdicluster`
* Nowe polecenie (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Migrowanie tooAzure programu PowerShell usługi Azure Resource Manager
Witaj ogólne informacje dotyczące programu Azure PowerShell w trybie Azure Resource Manager (ARM) hello można znaleźć w folderze [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).

Witaj poleceń cmdlet programu Azure PowerShell ARM może być zainstalowane obok siebie z hello ASM poleceń cmdlet. polecenia cmdlet Hello z dwóch trybów hello można rozróżnić przy użyciu ich nazw.  Tryb ARM Hello ma *AzureRmHDInsight* w nazwach polecenia cmdlet hello porównanie zbyt*AzureHDInsight* w trybie ASM hello.  Na przykład *AzureRmHDInsightCluster nowy* vs. *Nowy AzureHDInsightCluster*. Parametry i opcje może mieć nazwy wiadomości i dostępnych wiele nowych parametrów podczas przy użyciu programu ARM.  Na przykład kilka poleceń cmdlet wymagają nowy przełącznik o nazwie *- ResourceGroupName*. 

Przed użyciem polecenia cmdlet usługi HDInsight hello, możesz połączyć tooyour konto platformy Azure i Utwórz nową grupę zasobów:

* Login-AzureRmAccount lub [AzureRmProfile wybierz](https://msdn.microsoft.com/library/mt619310.aspx). Zobacz [uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Nowe AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Zmieniono nazwę polecenia cmdlet
Witaj toolist polecenia cmdlet funkcji ASM usługi HDInsight w konsoli środowiska Windows PowerShell:

    help *azurermhdinsight*

Witaj Poniższa tabela zawiera listę poleceń cmdlet funkcji ASM hello i nazw w trybie ARM hello:

| Polecenia cmdlet funkcji ASM | Polecenia cmdlet ARM |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Dodaj AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Dodaj AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Dodaj AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Dodaj AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Udziel AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Udziel AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Wywołanie AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[Nowe AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[Nowe AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[Nowe AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[Nowe AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[Nowe AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[Nowe AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[Nowe AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Usuń AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Odwołaj AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Odwołaj AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Zestaw AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Zestaw AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Użyj AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[AzureRmHDInsightJob oczekiwania](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Nowe polecenia cmdlet
Oto Hello hello nowe polecenia cmdlet, które są dostępne tylko w trybie ARM hello. 

**Akcja skryptu pokrewnych poleceń cmdlet:**

* **Get-AzureRmHDInsightPersistedScriptAction**: hello pobiera utrwalone akcji skryptu dla klastra i wyświetla je w porządku chronologicznym lub pobiera szczegóły dla akcji utrwalonych skryptów określony. 
* **Get-AzureRmHDInsightScriptActionHistory**: pobiera historii akcji skryptu hello klastra i wyświetla go w odwrotnej kolejności chronologicznej lub pobiera szczegóły akcji wcześniej wykonanie skryptu. 
* **Usuń AzureRmHDInsightPersistedScriptAction**: usuwa akcji utrwalonego skryptu z klastra usługi HDInsight.
* **Zestaw AzureRmHDInsightPersistedScriptAction**: ustawia toobe akcji skryptu wcześniej wykonanych akcji utrwalonego skryptu.
* **Przedstawia AzureRmHDInsightScriptAction**: przesyła nowy klaster Azure HDInsight tooan akcji skryptu. 

Użycie dodatkowych informacji, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

**Tożsamość Clsuter pokrewnych poleceń cmdlet:**

* **Dodaj AzureRmHDInsightClusterIdentity**: dodaje obiekt konfiguracji klastra tożsamości tooa klastra, dzięki czemu hello klastra usługi HDInsight mogą uzyskiwać dostęp do usługi Azure Data Lake magazynów. Zobacz [tworzenia klastra usługi HDInsight z Data Lake Store za pomocą programu Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>Przykłady
**Tworzenie klastra**

Polecenie stary (ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Nowe polecenie (ARM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Usuwanie klastra**

Polecenie stary (ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

Nowe polecenie (ARM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Klaster listą**

Polecenie stary (ASM):

    Get-AzureHDInsightCluster

Nowe polecenie (ARM):

    Get-AzureRmHDInsightCluster 

**Pokaż klastra**

Polecenie stary (ASM):

    Get-AzureHDInsightCluster -Name $clusterName

Nowe polecenie (ARM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Inne przykłady
* [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Przesyłania zadań Hive](hdinsight-hadoop-use-hive-powershell.md)
* [Przesyłanie zadań Pig](hdinsight-hadoop-use-pig-powershell.md)
* [Przesyłanie zadań Sqoop](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Migrowanie toohello opartego na architekturze ARM HDInsight zestawu SDK .NET
Witaj, na podstawie zarządzania usługą Azure [zestawu .NET SDK usługi HDInsight (ASM)](https://msdn.microsoft.com/library/azure/mt416619.aspx) jest już przestarzały. Są zachęcani toouse hello na podstawie zarządzania zasobami Azure [zestawu .NET SDK usługi HDInsight (ARM)](https://msdn.microsoft.com/library/azure/mt271028.aspx). Witaj następujące pakiety usługi HDInsight opartych na funkcji ASM są przestarzałe.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

Ta sekcja zawiera wskaźniki toomore informacje na temat tooperform niektórych zadań z wykorzystaniem hello opartego na architekturze ARM zestawu SDK.

| Jak... przy użyciu hello SDK HDInsight oparte na usłudze ARM | Linki |
| --- | --- |
| Tworzenie klastrów usługi HDInsight przy użyciu zestawu .NET SDK |Zobacz [Tworzenie klastrów usługi HDInsight przy użyciu zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| Dostosowywanie klastra przy użyciu akcji skryptu przy użyciu zestawu .NET SDK |Zobacz [dostosować HDInsight Linux klastrów za pomocą akcji skryptu](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| Uwierzytelniania aplikacji interaktywnego przy użyciu usługi Azure Active Directory przy użyciu zestawu .NET SDK |Zobacz [uruchamianie zapytań Hive przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md). fragment kodu Hello w tym artykule używa hello podejście uwierzytelnianie interakcyjne. |
| Uwierzytelniania aplikacji nieinteraktywnie przy użyciu usługi Azure Active Directory przy użyciu zestawu .NET SDK |Zobacz [utworzyć nieinterakcyjnych aplikacji dla usługi HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| Przesłać zadania technologii Hive, przy użyciu zestawu .NET SDK |Zobacz [Hive przesyłania zadań](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| Przesłać zadania programu Pig przy użyciu zestawu .NET SDK |Zobacz [Pig przesyłania zadań](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| Prześlij zadanie Sqoop przy użyciu zestawu .NET SDK |Zobacz [Sqoop przesyłania zadań](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| Lista klastrów usługi HDInsight przy użyciu zestawu .NET SDK |Zobacz [klastrów usługi HDInsight listy](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| Skalowanie klastrów usługi HDInsight przy użyciu zestawu .NET SDK |Zobacz [klastrów usługi HDInsight skali](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| Klastry tooHDInsight dostępu do przydzielenia/odwołania przy użyciu zestawu .NET SDK |Zobacz [Grant/revoke dostępu tooHDInsight klastrów](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| Zaktualizuj poświadczenia użytkownika HTTP dla klastrów usługi HDInsight przy użyciu zestawu .NET SDK |Zobacz [HTTP aktualizacji poświadczeń użytkownika do klastrów usługi HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| Znajdź hello domyślne konto magazynu dla klastrów usługi HDInsight przy użyciu zestawu .NET SDK |Zobacz [znaleźć hello domyślne konto magazynu dla klastrów usługi HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| Usuwać klastry usługi HDInsight przy użyciu zestawu .NET SDK |Zobacz [klastrów HDInsight usunąć](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>Przykłady
Poniżej przedstawiono kilka przykładów w sposób operacja jest wykonywane przy użyciu hello ASM na podstawie zestawu SDK i fragment kodu równoważne hello na powitania opartego na architekturze ARM zestawu SDK.

**Tworzenie klienta CRUD klastra**

* Polecenie stary (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Nowe polecenie (ARM) (autoryzacji głównej usługi)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Nowe polecenie (ARM) (Autoryzacja użytkownika)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Tworzenie klastra**

* Polecenie stary (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Nowe polecenie (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**Włączanie dostępu HTTP**

* Polecenie stary (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Nowe polecenie (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Usuwanie klastra**

* Polecenie stary (ASM)
  
        client.DeleteCluster(dnsName);
* Nowe polecenie (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

