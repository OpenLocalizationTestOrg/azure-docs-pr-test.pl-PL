---
title: "Zarządzanie klastrami Hadoop w HDInsight przy użyciu zestawu .NET SDK - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonywać zadania administracyjne dla klastrów Hadoop w usłudze HDInsight przy użyciu zestawu SDK .NET usługi HDInsight."
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
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="c0908-103">Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c0908-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="c0908-104">Informacje o sposobie zarządzania klastrami HDInsight przy użyciu [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0908-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="c0908-105">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="c0908-105">**Prerequisites**</span></span>

<span data-ttu-id="c0908-106">Przed rozpoczęciem korzystania z informacji zawartych w tym artykule należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="c0908-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c0908-107">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="c0908-107">**An Azure subscription**.</span></span> <span data-ttu-id="c0908-108">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c0908-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="c0908-109">Połączenie do usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0908-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="c0908-110">Potrzebne są następujące pakiety Nuget:</span><span class="sxs-lookup"><span data-stu-id="c0908-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="c0908-111">Poniższy przykład kodu pokazuje sposób podłączania na platformie Azure, zanim będzie możliwe zarządzanie klastrami usługi HDInsight w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c0908-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="c0908-112">Zobaczysz monit po uruchomieniu tego programu.</span><span class="sxs-lookup"><span data-stu-id="c0908-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="c0908-113">Jeśli nie chcesz wyświetlić monit, zobacz [tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinteraktywne](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c0908-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="c0908-114">Tworzenie klastrów</span><span class="sxs-lookup"><span data-stu-id="c0908-114">Create clusters</span></span>
<span data-ttu-id="c0908-115">Zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="c0908-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="c0908-116">Lista klastrów</span><span class="sxs-lookup"><span data-stu-id="c0908-116">List clusters</span></span>
<span data-ttu-id="c0908-117">Poniższy fragment kodu zawiera klastrów i niektóre właściwości:</span><span class="sxs-lookup"><span data-stu-id="c0908-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="c0908-118">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="c0908-118">Delete clusters</span></span>
<span data-ttu-id="c0908-119">Aby usunąć klaster, synchronicznie lub asynchronicznie, użyj poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="c0908-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="c0908-120">Skalowanie klastrów</span><span class="sxs-lookup"><span data-stu-id="c0908-120">Scale clusters</span></span>
<span data-ttu-id="c0908-121">Skalowanie funkcji klastra umożliwia zmianę liczby węzłów procesu roboczego używane przez klaster, który jest uruchomiony w usłudze Azure HDInsight bez konieczności ponownego tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="c0908-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c0908-122">Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c0908-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="c0908-123">Jeśli masz pewności, jaka wersja klastra, można sprawdzić na stronie właściwości.</span><span class="sxs-lookup"><span data-stu-id="c0908-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="c0908-124">Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="c0908-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="c0908-125">Wpływ zmianę liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:</span><span class="sxs-lookup"><span data-stu-id="c0908-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="c0908-126">Usługa Hadoop</span><span class="sxs-lookup"><span data-stu-id="c0908-126">Hadoop</span></span>
  
    <span data-ttu-id="c0908-127">Można bezproblemowo zwiększyć liczbę węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania.</span><span class="sxs-lookup"><span data-stu-id="c0908-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="c0908-128">Również można przesłać nowe zadania, gdy operacja jest w toku.</span><span class="sxs-lookup"><span data-stu-id="c0908-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="c0908-129">Błędy w operacji skalowania bezpiecznie obsługi tak, aby zawsze pozostanie w stanie funkcjonalności klastra.</span><span class="sxs-lookup"><span data-stu-id="c0908-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="c0908-130">Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby węzłów danych są ponownie uruchamiane niektóre z tych usług w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c0908-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="c0908-131">Powoduje to wszystkich uruchomionych i oczekujące zadania się niepowodzeniem po zakończeniu operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="c0908-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="c0908-132">Można jednak Prześlij ponownie zadania po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="c0908-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="c0908-133">HBase</span><span class="sxs-lookup"><span data-stu-id="c0908-133">HBase</span></span>
  
    <span data-ttu-id="c0908-134">Można bezproblemowo dodać lub usunąć węzły do klastra HBase jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c0908-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="c0908-135">Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="c0908-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="c0908-136">Można jednak również ręcznie saldo serwery regionalne logowanie do headnode klastra i uruchamiając następujące polecenia z poziomu okna wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="c0908-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="c0908-137">Storm</span><span class="sxs-lookup"><span data-stu-id="c0908-137">Storm</span></span>
  
    <span data-ttu-id="c0908-138">Bezproblemowo można dodawać i usuwać dane węzły do klastra Storm, jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c0908-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="c0908-139">Jednak po pomyślnym zakończeniu operacji skalowania, konieczne będzie ponowne zrównoważenie topologii.</span><span class="sxs-lookup"><span data-stu-id="c0908-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="c0908-140">Ponowne równoważenie można zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="c0908-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="c0908-141">STORM interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="c0908-141">Storm web UI</span></span>
  * <span data-ttu-id="c0908-142">Narzędzia interfejsu wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="c0908-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="c0908-143">Zapoznaj się z [dokumentację Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="c0908-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="c0908-144">Interfejs użytkownika sieci web Storm jest dostępna w klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c0908-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![HDInsight Storm Zrównoważ skali](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="c0908-146">Oto przykład sposobu użycia polecenia interfejsu wiersza polecenia do ponowne zrównoważenie topologii Storm:</span><span class="sxs-lookup"><span data-stu-id="c0908-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="c0908-147">Poniższy fragment kodu przedstawia sposób zmiany rozmiaru klastra synchronicznie lub asynchronicznie:</span><span class="sxs-lookup"><span data-stu-id="c0908-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="c0908-148">Dostęp do przydzielenia/odwołania</span><span class="sxs-lookup"><span data-stu-id="c0908-148">Grant/revoke access</span></span>
<span data-ttu-id="c0908-149">Klastry HDInsight są następujące usługi sieci web HTTP (wszystkie te usługi mają RESTful punkty końcowe):</span><span class="sxs-lookup"><span data-stu-id="c0908-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="c0908-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="c0908-150">ODBC</span></span>
* <span data-ttu-id="c0908-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="c0908-151">JDBC</span></span>
* <span data-ttu-id="c0908-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="c0908-152">Ambari</span></span>
* <span data-ttu-id="c0908-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="c0908-153">Oozie</span></span>
* <span data-ttu-id="c0908-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="c0908-154">Templeton</span></span>

<span data-ttu-id="c0908-155">Domyślnie te usługi są przyznawane dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0908-155">By default, these services are granted for access.</span></span> <span data-ttu-id="c0908-156">Możesz można odwołać/udzielenie dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0908-156">You can revoke/grant the access.</span></span> <span data-ttu-id="c0908-157">Aby można było odwołać:</span><span class="sxs-lookup"><span data-stu-id="c0908-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="c0908-158">Aby udzielić:</span><span class="sxs-lookup"><span data-stu-id="c0908-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="c0908-159">Przez przyznawanie/odwoływanie dostępu, spowoduje zresetowanie klastra, nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="c0908-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="c0908-160">Można to również zrobić w portalu.</span><span class="sxs-lookup"><span data-stu-id="c0908-160">This can also be done via the Portal.</span></span> <span data-ttu-id="c0908-161">Zobacz [administrowania HDInsight przy użyciu portalu Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="c0908-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="c0908-162">Zaktualizuj poświadczenia użytkownika HTTP</span><span class="sxs-lookup"><span data-stu-id="c0908-162">Update HTTP user credentials</span></span>
<span data-ttu-id="c0908-163">Jest tej samej procedury co [dostępu Grant/revoke HTTP](#grant/revoke-access). Jeśli klaster przyznano dostęp HTTP, należy je najpierw odwołać.</span><span class="sxs-lookup"><span data-stu-id="c0908-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="c0908-164">A następnie przyznać dostęp z nowymi poświadczeniami użytkownika HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0908-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="c0908-165">Znajdź domyślne konto magazynu</span><span class="sxs-lookup"><span data-stu-id="c0908-165">Find the default storage account</span></span>
<span data-ttu-id="c0908-166">Poniższy fragment kodu przedstawia sposób uzyskać domyślna nazwa konta magazynu i domyślny klucz konta magazynu dla klastra.</span><span class="sxs-lookup"><span data-stu-id="c0908-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="c0908-167">Przesyłanie zadań</span><span class="sxs-lookup"><span data-stu-id="c0908-167">Submit jobs</span></span>
<span data-ttu-id="c0908-168">**Aby przesłać zadania MapReduce**</span><span class="sxs-lookup"><span data-stu-id="c0908-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="c0908-169">Zobacz [przykłady Uruchom MapReduce z Hadoop w usłudze HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c0908-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="c0908-170">**Do przesyłania zadań Hive**</span><span class="sxs-lookup"><span data-stu-id="c0908-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="c0908-171">Zobacz [uruchamianie zapytań Hive przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c0908-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="c0908-172">**Do przesyłania zadań Pig**</span><span class="sxs-lookup"><span data-stu-id="c0908-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="c0908-173">Zobacz [Pig uruchomienie zadania przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c0908-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="c0908-174">**Do przesyłania zadań Sqoop**</span><span class="sxs-lookup"><span data-stu-id="c0908-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="c0908-175">Zobacz [Sqoop za pomocą usługi HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c0908-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="c0908-176">**Do przesyłania zadań Oozie**</span><span class="sxs-lookup"><span data-stu-id="c0908-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="c0908-177">Zobacz [Oozie użycia z usługą Hadoop do definiowania i uruchomić przepływ pracy w usłudze HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="c0908-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="c0908-178">Przekazywanie danych do magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c0908-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="c0908-179">Zobacz [Przekazywanie danych do usługi HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="c0908-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="c0908-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c0908-180">See Also</span></span>
* [<span data-ttu-id="c0908-181">Dokumentacji zestawu SDK .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0908-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="c0908-182">[Administrowanie HDInsight przy użyciu portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="c0908-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="c0908-183">[Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="c0908-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="c0908-184">[Tworzenie klastrów usługi HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="c0908-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="c0908-185">[Przekazywanie danych do usługi HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c0908-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c0908-186">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c0908-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


