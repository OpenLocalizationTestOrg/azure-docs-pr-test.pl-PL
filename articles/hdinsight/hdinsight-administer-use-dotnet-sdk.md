---
title: "klastry aaaManage Hadoop w usłudze HDInsight przy użyciu zestawu .NET SDK - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform administracyjne zadań hello klastrów platformy Hadoop w usłudze HDInsight przy użyciu zestawu SDK .NET usługi HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu zestawu .NET SDK
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Dowiedz się, jak toomanage HDInsight clusters przy użyciu [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Wymagania wstępne**

Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Połącz tooAzure HDInsight

Potrzebne są następujące pakiety Nuget hello:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Witaj poniższy przykład kodu pokazuje sposób tooAzure tooconnect przed przystąpieniem do administrowania HDInsight clusters w ramach Twojej subskrypcji platformy Azure.

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
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
        }
    }

Zobaczysz monit po uruchomieniu tego programu.  Jeśli nie chcesz, aby wiersz hello toosee, zobacz [tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinteraktywne](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Tworzenie klastrów
Zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu hello zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Lista klastrów
Witaj poniższy fragment kodu zawiera listę klastrów i niektóre właściwości:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Usuwanie klastrów
Użyj następującego toodelete fragment kodu klastra synchronicznie lub asynchronicznie hello: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Skalowanie klastrów
Skalowanie funkcji klastra Hello umożliwia toochange hello liczba węzłów procesu roboczego, używane przez klaster działa w usłudze Azure HDInsight bez konieczności toore — Tworzenie klastra hello.

> [!NOTE]
> Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane. Jeśli masz pewności, jaka wersja hello klastra, można sprawdzić hello stronę właściwości.  Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

wpływ Hello Zmienianie hello liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:

* Usługa Hadoop
  
    Można zwiększyć bezproblemowo hello liczba węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania. W trakcie operacji hello również można przesłać nowe zadania. Błędy w operacji skalowania bezpiecznie obsługi tak, aby hello klastra zawsze pozostanie w stanie funkcjonalności.
  
    Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby hello węzły danych są ponownie uruchamiane niektórych usług hello hello klastra. Powoduje to wszystkich uruchomionych i oczekujących zadań toofail na zakończenie hello hello operacji skalowania. Można jednak Prześlij ponownie hello zadania po zakończeniu operacji hello.
* HBase
  
    Można bezproblemowo dodać lub usunąć klaster HBase tooyour węzłów, jest uruchomiona. Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia hello operacji skalowania. Można jednak również ręcznie saldo serwerów regionalnych hello logując się do headnode hello klastra i uruchomione hello poniższych poleceń z poziomu okna wiersza polecenia:
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    Można bezproblemowo dodać lub usunąć klaster Storm tooyour węzłów danych jest uruchomiona. Jednak po pomyślnym zakończeniu hello operacji skalowania, konieczne będzie toorebalance hello topologii.
  
    Ponowne równoważenie można zrobić na dwa sposoby:
  
  * STORM interfejsu użytkownika sieci web
  * Narzędzia interfejsu wiersza polecenia (CLI)
    
    Zobacz toohello [dokumentację Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) więcej szczegółów.
    
    Witaj interfejsu użytkownika sieci web platformy Storm w klastrze jest dostępny hello HDInsight:
    
    ![HDInsight Storm Zrównoważ skali](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Poniżej przedstawiono przykładowy sposób hello toouse interfejsu wiersza polecenia polecenie topologii Storm hello toorebalance:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Witaj następującego kodu fragment kodu przedstawia sposób tooresize klastra synchronicznie lub asynchronicznie:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Dostęp do przydzielenia/odwołania
Klastry HDInsight są powitania po HTTP usługi sieci web (wszystkie te usługi mają RESTful punkty końcowe):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Domyślnie te usługi są przyznawane dostępu. Możesz można odwołać/Udziel dostępu hello. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Przez przyznawanie/odwoływanie dostępu hello, spowoduje zresetowanie hello klastra nazwę i hasło użytkownika.
> 
> 

Ponadto można to zrobić za pomocą hello portalu. Zobacz [administrowania HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Zaktualizuj poświadczenia użytkownika HTTP
To samo hello procedury jako [dostępu Grant/revoke HTTP](#grant/revoke-access). Jeśli klaster hello przyznano hello dostęp HTTP, należy je najpierw odwołać.  A następnie przyznać dostęp hello z nowymi poświadczeniami użytkownika HTTP.

## <a name="find-hello-default-storage-account"></a>Znajdź hello domyślne konto magazynu
Witaj następującego fragmentu kodu pokazano, jak tooget hello domyślna nazwa konta magazynu i hello domyślny klucz konta magazynu dla klastra.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Przesyłanie zadań
**zadania MapReduce toosubmit**

Zobacz [przykłady Uruchom MapReduce z Hadoop w usłudze HDInsight](hdinsight-hadoop-run-samples-linux.md).

**toosubmit zadań Hive** 

Zobacz [uruchamianie zapytań Hive przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**toosubmit zadań Pig**

Zobacz [Pig uruchomienie zadania przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**toosubmit Sqoop zadania**

Zobacz [Sqoop za pomocą usługi HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**toosubmit Oozie zadania**

Zobacz [Oozie Użyj Hadoop toodefine i Uruchom przepływ pracy w usłudze HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Przekazywanie danych tooAzure obiektu Blob magazynu
Zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Zobacz też
* [Dokumentacji zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Administrowanie HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]
* [Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]
* [Tworzenie klastrów usługi HDInsight][hdinsight-provision]
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


