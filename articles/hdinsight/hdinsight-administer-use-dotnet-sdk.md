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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="7da06-103">Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7da06-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="7da06-104">Dowiedz się, jak toomanage HDInsight clusters przy użyciu [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da06-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="7da06-105">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="7da06-105">**Prerequisites**</span></span>

<span data-ttu-id="7da06-106">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7da06-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="7da06-107">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="7da06-107">**An Azure subscription**.</span></span> <span data-ttu-id="7da06-108">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7da06-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="7da06-109">Połącz tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7da06-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="7da06-110">Potrzebne są następujące pakiety Nuget hello:</span><span class="sxs-lookup"><span data-stu-id="7da06-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="7da06-111">Witaj poniższy przykład kodu pokazuje sposób tooAzure tooconnect przed przystąpieniem do administrowania HDInsight clusters w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7da06-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="7da06-112">Zobaczysz monit po uruchomieniu tego programu.</span><span class="sxs-lookup"><span data-stu-id="7da06-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="7da06-113">Jeśli nie chcesz, aby wiersz hello toosee, zobacz [tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinteraktywne](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7da06-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="7da06-114">Tworzenie klastrów</span><span class="sxs-lookup"><span data-stu-id="7da06-114">Create clusters</span></span>
<span data-ttu-id="7da06-115">Zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu hello zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7da06-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="7da06-116">Lista klastrów</span><span class="sxs-lookup"><span data-stu-id="7da06-116">List clusters</span></span>
<span data-ttu-id="7da06-117">Witaj poniższy fragment kodu zawiera listę klastrów i niektóre właściwości:</span><span class="sxs-lookup"><span data-stu-id="7da06-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="7da06-118">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="7da06-118">Delete clusters</span></span>
<span data-ttu-id="7da06-119">Użyj następującego toodelete fragment kodu klastra synchronicznie lub asynchronicznie hello:</span><span class="sxs-lookup"><span data-stu-id="7da06-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="7da06-120">Skalowanie klastrów</span><span class="sxs-lookup"><span data-stu-id="7da06-120">Scale clusters</span></span>
<span data-ttu-id="7da06-121">Skalowanie funkcji klastra Hello umożliwia toochange hello liczba węzłów procesu roboczego, używane przez klaster działa w usłudze Azure HDInsight bez konieczności toore — Tworzenie klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7da06-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7da06-122">Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="7da06-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="7da06-123">Jeśli masz pewności, jaka wersja hello klastra, można sprawdzić hello stronę właściwości.</span><span class="sxs-lookup"><span data-stu-id="7da06-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="7da06-124">Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="7da06-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="7da06-125">wpływ Hello Zmienianie hello liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:</span><span class="sxs-lookup"><span data-stu-id="7da06-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="7da06-126">Usługa Hadoop</span><span class="sxs-lookup"><span data-stu-id="7da06-126">Hadoop</span></span>
  
    <span data-ttu-id="7da06-127">Można zwiększyć bezproblemowo hello liczba węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania.</span><span class="sxs-lookup"><span data-stu-id="7da06-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="7da06-128">W trakcie operacji hello również można przesłać nowe zadania.</span><span class="sxs-lookup"><span data-stu-id="7da06-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="7da06-129">Błędy w operacji skalowania bezpiecznie obsługi tak, aby hello klastra zawsze pozostanie w stanie funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="7da06-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="7da06-130">Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby hello węzły danych są ponownie uruchamiane niektórych usług hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="7da06-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="7da06-131">Powoduje to wszystkich uruchomionych i oczekujących zadań toofail na zakończenie hello hello operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="7da06-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="7da06-132">Można jednak Prześlij ponownie hello zadania po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7da06-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="7da06-133">HBase</span><span class="sxs-lookup"><span data-stu-id="7da06-133">HBase</span></span>
  
    <span data-ttu-id="7da06-134">Można bezproblemowo dodać lub usunąć klaster HBase tooyour węzłów, jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7da06-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="7da06-135">Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia hello operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="7da06-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="7da06-136">Można jednak również ręcznie saldo serwerów regionalnych hello logując się do headnode hello klastra i uruchomione hello poniższych poleceń z poziomu okna wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7da06-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="7da06-137">Storm</span><span class="sxs-lookup"><span data-stu-id="7da06-137">Storm</span></span>
  
    <span data-ttu-id="7da06-138">Można bezproblemowo dodać lub usunąć klaster Storm tooyour węzłów danych jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7da06-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="7da06-139">Jednak po pomyślnym zakończeniu hello operacji skalowania, konieczne będzie toorebalance hello topologii.</span><span class="sxs-lookup"><span data-stu-id="7da06-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="7da06-140">Ponowne równoważenie można zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="7da06-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="7da06-141">STORM interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="7da06-141">Storm web UI</span></span>
  * <span data-ttu-id="7da06-142">Narzędzia interfejsu wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="7da06-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="7da06-143">Zobacz toohello [dokumentację Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="7da06-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="7da06-144">Witaj interfejsu użytkownika sieci web platformy Storm w klastrze jest dostępny hello HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7da06-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![HDInsight Storm Zrównoważ skali](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="7da06-146">Poniżej przedstawiono przykładowy sposób hello toouse interfejsu wiersza polecenia polecenie topologii Storm hello toorebalance:</span><span class="sxs-lookup"><span data-stu-id="7da06-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="7da06-147">Witaj następującego kodu fragment kodu przedstawia sposób tooresize klastra synchronicznie lub asynchronicznie:</span><span class="sxs-lookup"><span data-stu-id="7da06-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="7da06-148">Dostęp do przydzielenia/odwołania</span><span class="sxs-lookup"><span data-stu-id="7da06-148">Grant/revoke access</span></span>
<span data-ttu-id="7da06-149">Klastry HDInsight są powitania po HTTP usługi sieci web (wszystkie te usługi mają RESTful punkty końcowe):</span><span class="sxs-lookup"><span data-stu-id="7da06-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="7da06-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="7da06-150">ODBC</span></span>
* <span data-ttu-id="7da06-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="7da06-151">JDBC</span></span>
* <span data-ttu-id="7da06-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="7da06-152">Ambari</span></span>
* <span data-ttu-id="7da06-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="7da06-153">Oozie</span></span>
* <span data-ttu-id="7da06-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="7da06-154">Templeton</span></span>

<span data-ttu-id="7da06-155">Domyślnie te usługi są przyznawane dostępu.</span><span class="sxs-lookup"><span data-stu-id="7da06-155">By default, these services are granted for access.</span></span> <span data-ttu-id="7da06-156">Możesz można odwołać/Udziel dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="7da06-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="7da06-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="7da06-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="7da06-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="7da06-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="7da06-159">Przez przyznawanie/odwoływanie dostępu hello, spowoduje zresetowanie hello klastra nazwę i hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7da06-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="7da06-160">Ponadto można to zrobić za pomocą hello portalu.</span><span class="sxs-lookup"><span data-stu-id="7da06-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="7da06-161">Zobacz [administrowania HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="7da06-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="7da06-162">Zaktualizuj poświadczenia użytkownika HTTP</span><span class="sxs-lookup"><span data-stu-id="7da06-162">Update HTTP user credentials</span></span>
<span data-ttu-id="7da06-163">To samo hello procedury jako [dostępu Grant/revoke HTTP](#grant/revoke-access). Jeśli klaster hello przyznano hello dostęp HTTP, należy je najpierw odwołać.</span><span class="sxs-lookup"><span data-stu-id="7da06-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="7da06-164">A następnie przyznać dostęp hello z nowymi poświadczeniami użytkownika HTTP.</span><span class="sxs-lookup"><span data-stu-id="7da06-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="7da06-165">Znajdź hello domyślne konto magazynu</span><span class="sxs-lookup"><span data-stu-id="7da06-165">Find hello default storage account</span></span>
<span data-ttu-id="7da06-166">Witaj następującego fragmentu kodu pokazano, jak tooget hello domyślna nazwa konta magazynu i hello domyślny klucz konta magazynu dla klastra.</span><span class="sxs-lookup"><span data-stu-id="7da06-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="7da06-167">Przesyłanie zadań</span><span class="sxs-lookup"><span data-stu-id="7da06-167">Submit jobs</span></span>
<span data-ttu-id="7da06-168">**zadania MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="7da06-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="7da06-169">Zobacz [przykłady Uruchom MapReduce z Hadoop w usłudze HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7da06-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="7da06-170">**toosubmit zadań Hive**</span><span class="sxs-lookup"><span data-stu-id="7da06-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="7da06-171">Zobacz [uruchamianie zapytań Hive przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7da06-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="7da06-172">**toosubmit zadań Pig**</span><span class="sxs-lookup"><span data-stu-id="7da06-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="7da06-173">Zobacz [Pig uruchomienie zadania przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7da06-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="7da06-174">**toosubmit Sqoop zadania**</span><span class="sxs-lookup"><span data-stu-id="7da06-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="7da06-175">Zobacz [Sqoop za pomocą usługi HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7da06-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="7da06-176">**toosubmit Oozie zadania**</span><span class="sxs-lookup"><span data-stu-id="7da06-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="7da06-177">Zobacz [Oozie Użyj Hadoop toodefine i Uruchom przepływ pracy w usłudze HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="7da06-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="7da06-178">Przekazywanie danych tooAzure obiektu Blob magazynu</span><span class="sxs-lookup"><span data-stu-id="7da06-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="7da06-179">Zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="7da06-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="7da06-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7da06-180">See Also</span></span>
* [<span data-ttu-id="7da06-181">Dokumentacji zestawu SDK .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="7da06-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="7da06-182">[Administrowanie HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="7da06-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="7da06-183">[Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="7da06-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="7da06-184">[Tworzenie klastrów usługi HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="7da06-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="7da06-185">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="7da06-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="7da06-186">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7da06-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


