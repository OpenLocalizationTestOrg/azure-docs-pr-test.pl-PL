---
title: "aaaCustomize klastrów usługi HDInsight przy użyciu skryptu akcje - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize HDInsight clusters za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Dostosowywanie klastrów usługi HDInsight opartej na systemie Windows za pomocą akcji skryptu
**Akcja skryptu** mogą być używane tooinvoke [niestandardowych skryptów](hdinsight-hadoop-script-actions.md) podczas procesu tworzenia klastra hello instalowania dodatkowego oprogramowania na klastrze.

Hello informacje w tym artykule jest określonym na podstawie tooWindows klastrów usługi HDInsight. W klastrach opartych na systemie Linux, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

Klastry usługi HDInsight można dostosować w różnych innych metod, a także takie jak tym dodatkowych kont usługi Azure Storage, zmiana hello Hadoop plików konfiguracji (core-site.xml, hive-site.xml, itp.) lub dodawanie współdzielone biblioteki (np. Hive, Oozie) w typowe lokalizacje hello klastra. Te modyfikacje może odbywać się za pomocą programu Azure PowerShell, hello Azure HDInsight .NET SDK, lub hello portalu Azure. Aby uzyskać więcej informacji, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Akcja skryptu w procesie tworzenia klastra hello
Akcja skryptu jest używana tylko podczas hello procesu tworzenia klastra. Witaj poniższym diagramie przedstawiono podczas wykonywania akcji skryptu podczas procesu tworzenia hello:

![Dostosowywanie klastrów usługi HDInsight i etapy podczas tworzenia klastra][img-hdi-cluster-states]

Podczas wykonywania skryptu hello hello klastra wprowadza hello **ClusterCustomization** etapu. Na tym etapie hello skrypt jest uruchamiany w ramach konta administratora systemu hello, równolegle na powitania wszystkie określone węzłów w klastrze hello i zapewnia uprawnienia administrator o pełnych uprawnieniach w węzłach hello.

> [!NOTE]
> Ponieważ użytkownik ma uprawnienia administratora w węzłach klastra hello podczas **ClusterCustomization** etapie, można użyć hello skryptu tooperform operacje takie jak zatrzymanie i uruchomienie usług, w tym usług związanych z usługi Hadoop. Jako część skryptu hello, należy się upewnić, tym hello Ambari usług i innych usług związanych z Hadoop są gotowe do działania przed zakończeniu hello skryptu. Te usługi są wymagane toosuccessfully ustalić hello kondycję i stan hello klastra podczas jego tworzenia. Jeśli zmienisz żadnej konfiguracji w klastrze, który ma wpływ na tych usług, należy użyć funkcji pomocnika hello, które znajdują się. Aby uzyskać więcej informacji o funkcji pomocnika, zobacz [skryptów tworzenie akcji skryptu dla usługi HDInsight][hdinsight-write-script].
>
>

dane wyjściowe Hello i dzienników błędów hello skryptu hello są przechowywane w hello domyślne konto magazynu określone dla klastra hello. Witaj dzienniki są przechowywane w tabeli o nazwie hello **u < \cluster-name-fragment >< \time-stamp > setuplog**. Są to dzienniki agregacji ze skryptu hello uruchamiania we wszystkich węzłach hello (węzła głównego i węzły procesów roboczych) w klastrze hello.

Każdy klaster może akceptować wiele akcji skryptu, które jest wywoływane w kolejności hello, w którym są określone. Skrypt może uruchomionego na powitania węzła głównego i hello węzłów procesu roboczego.

Usługa HDInsight zapewnia kilka hello tooinstall skrypty następujące składniki w klastrach HDInsight:

| Nazwa | Skrypt |
| --- | --- |
| **Zainstaluj Spark** |https://hdiconfigactions.blob.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1. Zobacz [instalacji i używania platformy Spark w usłudze HDInsight clusters][hdinsight-install-spark]. |
| **Zainstalować język R** |https://hdiconfigactions.blob.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1. Zobacz [instalacji i używania R w klastrach HDInsight][hdinsight-install-r]. |
| **Zainstaluj Solr** |https://hdiconfigactions.blob.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1. Zobacz [instalacji i używania Solr w usłudze HDInsight clusters](hdinsight-hadoop-solr-install.md). |
| - **Zainstaluj Giraph** |https://hdiconfigactions.blob.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1. Zobacz [instalacji i używania Giraph w usłudze HDInsight clusters](hdinsight-hadoop-giraph-install.md). |
| **Wstępne ładowanie bibliotek technologii Hive** |https://hdiconfigactions.blob.Core.Windows.NET/setupcustomhivelibsv01/Setup-customhivelibs-v01.ps1. Zobacz [dodać Hive bibliotek w klastrach HDInsight](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Skrypty wywołania przy użyciu hello portalu Azure
**Z hello portalu Azure**

1. Rozpocznij tworzenie klastra, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. W obszarze Konfiguracja opcjonalna dla hello **akcji skryptu** bloku, kliknij przycisk **dodać akcję skryptu** tooprovide szczegółowych informacji o hello akcji skryptu, jak pokazano poniżej:

    ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize akcji skryptu Użyj klastra")

    <table border='1'>
        <tr><th>Właściwość</th><th>Wartość</th></tr>
        <tr><td>Nazwa</td>
            <td>Określ nazwę hello akcji skryptu.</td></tr>
        <tr><td>Identyfikator URI skryptu</td>
            <td>Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra. s</td></tr>
        <tr><td>HEAD/proces roboczy.</td>
            <td>Określ węzły hello (**Head** lub **procesu roboczego**) na których dostosowanie hello skrypt jest uruchamiany.</b>.
        <tr><td>Parametry</td>
            <td>Określ parametry hello, jeśli są wymagane przez skrypt hello.</td></tr>
    </table>

    Naciśnij klawisz ENTER tooadd więcej niż jednego skryptu akcji tooinstall wiele składników w klastrze hello.
3. Kliknij przycisk **wybierz** toosave hello konfigurację akcji skryptu i kontynuować tworzenia klastra.

## <a name="call-scripts-using-azure-powershell"></a>Skrypty wywołania przy użyciu programu Azure PowerShell
Tego poniższy skrypt programu PowerShell pokazano, jak tooinstall Spark w systemie Windows na podstawie klastra usługi HDInsight.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall innego oprogramowania, konieczne będzie pliku skryptu hello tooreplace w skrypcie hello:

Po wyświetleniu monitu wprowadź poświadczenia hello hello klastra. Może upłynąć kilka minut przed utworzeniem klastra hello.

## <a name="call-scripts-using-net-sdk"></a>Skrypty wywołania przy użyciu zestawu .NET SDK
Witaj poniższym przykładzie pokazano sposób tooinstall Spark w systemie Windows na podstawie klastra usługi HDInsight. tooinstall innego oprogramowania, konieczne będzie pliku skryptu hello tooreplace w kodzie hello.

**toocreate klastra usługi HDInsight Spark**

1. Tworzenie aplikacji konsolowej C# w programie Visual Studio.
2. Z hello Konsola Menedżera pakietów Nuget uruchom następujące polecenie hello.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Użyj hello następujące instrukcje using w pliku Program.cs hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Umieść kod hello w klasie hello hello następujący:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. Naciśnij klawisz **F5** toorun hello aplikacji.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Obsługa oprogramowania typu open source używane w klastrach HDInsight
Hello usługi HDInsight systemu Microsoft Azure to elastyczna platforma, która umożliwia toobuild aplikacje danych big data w chmurze hello przy użyciu ekosystem technologii open source utworzona wokół Hadoop. Microsoft Azure udostępnia ogólnego poziomu wsparcia dla technologii open source, zgodnie z opisem w hello **obsługuje zakresu** sekcji hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">witryny sieci Web często zadawane pytania dotyczące obsługi Azure</a>. Hello usługa HDInsight zapewnia dodatkowy poziom obsługi dla niektórych składników hello zgodnie z poniższym opisem.

Istnieją dwa typy składników open source, które są dostępne w hello usługi HDInsight:

* **Wbudowanych składników** — te składniki są wstępnie zainstalowane w klastrach HDInsight i podaj podstawowych funkcji programu hello klastra. Na przykład YARN ResourceManager, język zapytań Hive hello (HiveQL) i biblioteki Mahout hello należy toothis kategorii. Pełna lista składniki klastra jest dostępna w [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md) </a>.
* **Niestandardowe składniki** -, jako użytkownik hello klastra, można zainstalować lub użyć w obciążenie jakiegokolwiek składnika dostępne w społeczności hello lub utworzone przez użytkownika.

Wbudowane składniki są w pełni obsługiwane, a Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane i Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.
>
> Niestandardowe składniki odbierania toohelp Obsługa uzasadnione ekonomicznie toofurther należy rozwiązać problem hello. Może to spowodować nad rozwiązaniem problemu hello lub proszenia tooengage dostępnych kanałów dla hello otwarty technologii źródła wykryto głębokie doświadczenia z tej technologii. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).
>
>

Witaj usługi HDInsight udostępnia kilka metod toouse niestandardowych składników. Niezależnie od tego, jak składnik jest używany lub zainstalowany w klastrze hello hello sam poziom obsługi ma zastosowanie. Poniżej znajduje się lista hello Najczęstszym że składnikach niestandardowych mogą być używane w klastrach HDInsight:

1. Przesyłanie zadań — usługi Hadoop i innych typów zadań, które wykonać albo użyć niestandardowych składników mogą być przesłane toohello klastra.
2. Dostosowywanie klastra — podczas tworzenia klastra, można określić dodatkowe ustawienia i niestandardowych składników, które zostaną zainstalowane w węzłach klastra hello.
3. Próbek - dla popularnych niestandardowych składników, firma Microsoft i inne osoby mogą powodować przykłady sposobu użycia tych składników na powitania klastrów usługi HDInsight. Te przykłady są udostępniane bez obsługi.

## <a name="develop-script-action-scripts"></a>Tworzenie skryptów akcji skryptu
Zobacz [skryptów tworzenie akcji skryptu dla usługi HDInsight][hdinsight-write-script].

## <a name="see-also"></a>Zobacz też
* [Tworzenie klastrów Hadoop w usłudze HDInsight] [ hdinsight-provision-cluster] zawiera instrukcje dotyczące sposobu toocreate HDInsight klastra przy użyciu niestandardowych opcji.
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight][hdinsight-write-script]
* [Zainstalować i używać platformy Spark w usłudze hdinsight][hdinsight-install-spark]
* [Zainstaluj i użyj języka R w klastrach HDInsight][hdinsight-install-r]
* [Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install.md).
* [Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Etapy podczas tworzenia klastra"
