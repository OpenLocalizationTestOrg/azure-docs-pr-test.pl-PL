---
title: "przy użyciu platformy .NET - Azure HDInsight klastrów Hadoop aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Hadoop, HBase, Storm i Spark klastry w systemie Linux usługi HDInsight przy użyciu hello zestawu .NET SDK usługi HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9c74e3dc-837f-4c90-bbb1-489bc7124a3d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 9460b0d27143c97860b3540fcec26851d755aa28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-net-sdk"></a><span data-ttu-id="8e511-103">Tworzenie klastrów z systemem Linux w usłudze HDInsight przy użyciu zestawu .NET SDK hello</span><span class="sxs-lookup"><span data-stu-id="8e511-103">Create Linux-based clusters in HDInsight using hello .NET SDK</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]


<span data-ttu-id="8e511-104">Dowiedz się, jak toocreate klastra usługi Hadoop w usłudze Azure HDInsight klastra przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8e511-104">Learn how toocreate a Hadoop cluster in Azure HDInsight cluster using hello .NET SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e511-105">Hello kroków w tym dokumencie Tworzenie klastra z węzła jednego procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="8e511-105">hello steps in this document create a cluster with one worker node.</span></span> <span data-ttu-id="8e511-106">Jeśli planowane jest więcej niż 32 węzłami procesów roboczych, podczas tworzenia klastra lub przez skalowanie klastra powitania po utworzeniu, należy tooselect rozmiarze węzła głównego z co najmniej 8 rdzeni i 14GB pamięci ram.</span><span class="sxs-lookup"><span data-stu-id="8e511-106">If you plan on more than 32 worker nodes, either at cluster creation or by scaling hello cluster after creation, you need tooselect a head node size with at least 8 cores and 14GB ram.</span></span>
>
> <span data-ttu-id="8e511-107">Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8e511-107">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e511-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8e511-108">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="8e511-109">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e511-109">**An Azure subscription**.</span></span> <span data-ttu-id="8e511-110">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8e511-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8e511-111">**Konto magazynu platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e511-111">**An Azure storage account**.</span></span> <span data-ttu-id="8e511-112">Zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8e511-112">See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="8e511-113">**Visual Studio 2013, Visual Studio 2015 lub Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="8e511-113">**Visual Studio 2013, Visual Studio 2015 or Visual Studio 2017**.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="8e511-114">Tworzenie klastrów</span><span class="sxs-lookup"><span data-stu-id="8e511-114">Create clusters</span></span>

1. <span data-ttu-id="8e511-115">Otwórz program Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8e511-115">Open Visual Studio 2017.</span></span>
2. <span data-ttu-id="8e511-116">Utwórz nową aplikację konsoli języka Visual C#.</span><span class="sxs-lookup"><span data-stu-id="8e511-116">Create a new Visual C# console application.</span></span>
3. <span data-ttu-id="8e511-117">Z hello **narzędzia** menu, kliknij przycisk **Menedżera pakietów NuGet**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="8e511-117">From hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="8e511-118">Uruchom następujące polecenie w hello konsoli tooinstall hello pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="8e511-118">Run hello following command in hello console tooinstall hello packages:</span></span>

    ```powershell
    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight
    ```

    <span data-ttu-id="8e511-119">Te polecenia Dodaj .NET bibliotek i odwołań toothem toohello bieżący projekt programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e511-119">These commands add .NET libraries and references toothem toohello current Visual Studio project.</span></span>
5. <span data-ttu-id="8e511-120">W Eksploratorze rozwiązań kliknij dwukrotnie **Program.cs** tooopen, Wklej hello następującego kodu i podaj wartości zmiennych hello:</span><span class="sxs-lookup"><span data-stu-id="8e511-120">From Solution Explorer, double-click **Program.cs** tooopen it, paste hello following code, and provide values for hello variables:</span></span>

    ```csharp
    using System;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    namespace CreateHDInsightCluster
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;

            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            private const string ExistingResourceGroupName = "<Enter Resource Group Name>";
            private const string ExistingStorageName = "<Enter Default Storage Account Name>.blob.core.windows.net";
            private const string ExistingStorageKey = "<Enter Default Storage Account Key>";
            private const string ExistingBlobContainer = "<Enter Default Bob Container Name>";

            private const string NewClusterName = "<Enter HDInsight Cluster Name>";
            private const int NewClusterNumNodes = 2;
            private const string NewClusterLocation = "EAST US 2";     // Must be hello same as hello default Storage account
            private const OSType NewClusterOSType = OSType.Linux;
            private const string NewClusterType = "Hadoop";
            private const string NewClusterVersion = "3.5";
            private const string NewClusterUsername = "admin";
            private const string NewClusterPassword = "<Enter HTTP User Password>";
            private const string NewClusterSshUserName = "sshuser";

            // You can use eitehr password or public key. See https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix
            private const string NewClusterSshPassword = "<Enter SSH User Password>";
            private const string NewClusterSshPublicKey = @"---- BEGIN SSH2 PUBLIC KEY ----
                Comment: ""rsa-key-20150731""
                AAAAB3NzaC1yc2EAAAABJQAAAQEA4QiCRLqT7fnmUA5OhYWZNlZo6lLaY1c+IRsp
                gmPCsJVGQLu6O1wqcxRqiKk7keYq8bP5s30v6bIljsLZYTnyReNUa5LtFw7eauGr
                yVt3Pve6ejfWELhbVpi0iq8uJNFA9VvRkz8IP1JmjC5jsdnJhzQZtgkIrdn3w0e6
                WVfu15kKyY8YAiynVbdV51EB0SZaSLdMZkZQ81xi4DDtCZD7qvdtWEFwLa+EHdkd
                pzO36Mtev5XvseLQqzXzZ6aVBdlXoppGHXkoGHAMNOtEWRXpAUtEccjpATsaZhQR
                zZdZlzHduhM10ofS4YOYBADt9JohporbQVHM5w6qUhIgyiPo7w==
                ---- END SSH2 PUBLIC KEY ----"; //replace hello public key with your own

            static void Main(string[] args)
            {
                System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

                // Authenticate and get a token
                var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // Set parameters for hello new cluster
                var parameters = new ClusterCreateParameters
                {
                    ClusterSizeInNodes = NewClusterNumNodes,
                    UserName = NewClusterUsername,
                    ClusterType = NewClusterType,
                    OSType = NewClusterOSType,
                    Version = NewClusterVersion,

                    // Use an Azure storage account as hello default storage
                    DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

                    // Is hello cluster type RServer? If so, you can set hello EdgeNodeSize.
                    // Otherwise, hello default VM size is used.
                    //EdgeNodeSize = "Standard_D12_v2",

                    Password = NewClusterPassword,
                    Location = NewClusterLocation,

                    SshUserName = NewClusterSshUserName,
                    SshPassword = NewClusterSshPassword,
                    //SshPublicKey = NewClusterSshPublicKey
                };

                // Is hello cluster type RServer? If so, add hello RStudio configuration option.
                /*
                parameters.Configurations.Add(
                    "rserver",
                    new Dictionary<string, string>()
                    {
                        { "rstudio", "true" }
                    }
                );
                */

                // Create hello cluster
                _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

                System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials GetTokenCloudCredentials(string TenantId, string ClientId, string SubscriptionId)
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
    ```

6. <span data-ttu-id="8e511-121">Zastąp wartości elementu członkowskiego klasy hello.</span><span class="sxs-lookup"><span data-stu-id="8e511-121">Replace hello class member values.</span></span>
7. <span data-ttu-id="8e511-122">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8e511-122">Press **F5** toorun hello application.</span></span> <span data-ttu-id="8e511-123">Okno konsoli powinno powodować otwarcie i wyświetlić stan hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8e511-123">A console window should open and display hello status of hello application.</span></span> <span data-ttu-id="8e511-124">Możesz są tooenter zostanie wyświetlony monit o poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="8e511-124">You are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="8e511-125">Może upłynąć kilka minut toocreate klastra usługi HDInsight, zazwyczaj około 15.</span><span class="sxs-lookup"><span data-stu-id="8e511-125">It can take several minutes toocreate an HDInsight cluster, normally around 15.</span></span>

## <a name="use-bootstrap"></a><span data-ttu-id="8e511-126">Użyj ładowania początkowego</span><span class="sxs-lookup"><span data-stu-id="8e511-126">Use bootstrap</span></span>

<span data-ttu-id="8e511-127">Przy użyciu ładowania początkowego, można skonfigurować ustawienia dodanie podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="8e511-127">Using bootstrap, you can configure addition settings during hello cluster creations.</span></span>  <span data-ttu-id="8e511-128">Aby uzyskać więcej informacji, zobacz [HDInsight dostosować klastry za pomocą początkowego](hdinsight-hadoop-customize-cluster-bootstrap.md).</span><span class="sxs-lookup"><span data-stu-id="8e511-128">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

<span data-ttu-id="8e511-129">Zmodyfikuj przykładowy hello w [Tworzenie klastrów](#create-clusters) tooconfigure ustawienie gałęzi:</span><span class="sxs-lookup"><span data-stu-id="8e511-129">Modify hello sample in [Create clusters](#create-clusters) tooconfigure a Hive setting:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for hello new cluster
    var extendedParameters = new ClusterCreateParametersExtended
    {
        Location = NewClusterLocation,
        Properties = new ClusterCreateProperties
        {
            ClusterDefinition = new ClusterDefinition
            {
                ClusterType = NewClusterType.ToString()
            },
            ClusterVersion = NewClusterVersion,
            OperatingSystemType = NewClusterOSType
        }
    };

    var coreConfigs = new Dictionary<string, string>
    {
        {"fs.defaultFS", string.Format("wasb://{0}@{1}", ExistingBlobContainer, ExistingStorageName)},
        {
            string.Format("fs.azure.account.key.{0}", ExistingStorageName),
            ExistingStorageKey
        }
    };

    // bootstrap
    var hiveConfigs = new Dictionary<string, string>
    {
        { "hive.metastore.client.socket.timeout", "90"}
    };

    var gatewayConfigs = new Dictionary<string, string>
    {
        {"restAuthCredential.isEnabled", "true"},
        {"restAuthCredential.username", NewClusterUsername},
        {"restAuthCredential.password", NewClusterPassword}
    };

    var configurations = new Dictionary<string, Dictionary<string, string>>
    {
        {"core-site", coreConfigs},
        {"gateway", gatewayConfigs},
        {"hive-site", hiveConfigs}
    };

    var serializedConfig = JsonConvert.SerializeObject(configurations);
    extendedParameters.Properties.ClusterDefinition.Configurations = serializedConfig;

    var sshPublicKeys = new List<SshPublicKey>();
    var sshPublicKey = new SshPublicKey
    {
        CertificateData =
            string.Format("ssh-rsa {0}", NewClusterSshPublicKey)
    };
    sshPublicKeys.Add(sshPublicKey);

    var headNode = new Role
    {
        Name = "headnode",
        TargetInstanceCount = 2,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                // When use a SSH pulbic key, make sure tooremove comments, headers and trailers, and concatenate hello key into one line 
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    var workerNode = new Role
    {
        Name = "workernode",
        TargetInstanceCount = NewClusterNumNodes,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    extendedParameters.Properties.ComputeProfile = new ComputeProfile();
    extendedParameters.Properties.ComputeProfile.Roles.Add(headNode);
    extendedParameters.Properties.ComputeProfile.Roles.Add(workerNode);

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, extendedParameters);

    System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
    System.Console.ReadLine();
}
```

## <a name="use-script-action"></a><span data-ttu-id="8e511-130">Za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="8e511-130">Use Script Action</span></span>

<span data-ttu-id="8e511-131">Za pomocą akcji skryptu, można skonfigurować dodatkowe ustawienia podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="8e511-131">Using Script Action, you can configure additional settings during cluster creations.</span></span>  <span data-ttu-id="8e511-132">Aby uzyskać więcej informacji, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8e511-132">For more information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="8e511-133">Zmodyfikuj przykładowy hello w [Tworzenie klastrów](#create-clusters) toocall tooinstall akcji skryptu R:</span><span class="sxs-lookup"><span data-stu-id="8e511-133">Modify hello sample in [Create clusters](#create-clusters) toocall a Script Action tooinstall R:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for hello new cluster
    var parameters = new ClusterCreateParameters
    {
        ClusterSizeInNodes = NewClusterNumNodes,
        Location = NewClusterLocation,
        ClusterType = NewClusterType,
        OSType = NewClusterOSType,
        Version = NewClusterVersion,

        DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

        UserName = NewClusterUsername,
        Password = NewClusterPassword,
        SshUserName = NewClusterSshUserName,
        SshPublicKey = NewClusterSshPublicKey
    };

    ScriptAction rScriptAction = new ScriptAction("Install R",
        new Uri("https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh"), "");

    parameters.ScriptActions.Add(ClusterNodeType.HeadNode,new System.Collections.Generic.List<ScriptAction> { rScriptAction});
    parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { rScriptAction });

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

    System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
    System.Console.ReadLine();
}
```

## <a name="troubleshoot"></a><span data-ttu-id="8e511-134">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="8e511-134">Troubleshoot</span></span>

<span data-ttu-id="8e511-135">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="8e511-135">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e511-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e511-136">Next steps</span></span>
<span data-ttu-id="8e511-137">Po pomyślnym utworzeniu klastra usługi HDInsight, za pomocą powitania po toolearn jak toowork z klastrem.</span><span class="sxs-lookup"><span data-stu-id="8e511-137">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span> 

### <a name="hadoop-clusters"></a><span data-ttu-id="8e511-138">Klastry Hadoop</span><span class="sxs-lookup"><span data-stu-id="8e511-138">Hadoop clusters</span></span>
* [<span data-ttu-id="8e511-139">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-139">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8e511-140">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-140">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8e511-141">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-141">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="8e511-142">Klastrów HBase</span><span class="sxs-lookup"><span data-stu-id="8e511-142">HBase clusters</span></span>
* [<span data-ttu-id="8e511-143">Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-143">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="8e511-144">Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-144">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="8e511-145">Klastry STORM</span><span class="sxs-lookup"><span data-stu-id="8e511-145">Storm clusters</span></span>
* [<span data-ttu-id="8e511-146">Tworzenie topologii Java dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-146">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="8e511-147">Użyj składników języka Python w Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-147">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="8e511-148">Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-148">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="8e511-149">Klastry Spark</span><span class="sxs-lookup"><span data-stu-id="8e511-149">Spark clusters</span></span>
* [<span data-ttu-id="8e511-150">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="8e511-150">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8e511-151">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="8e511-151">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="8e511-152">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="8e511-152">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8e511-153">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-153">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8e511-154">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="8e511-154">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="run-jobs"></a><span data-ttu-id="8e511-155">Uruchamianie zadań</span><span class="sxs-lookup"><span data-stu-id="8e511-155">Run jobs</span></span>
* [<span data-ttu-id="8e511-156">Uruchamiania zadań Hive w usłudze HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e511-156">Run Hive jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="8e511-157">Uruchamianie zadań Pig w usłudze HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e511-157">Run Pig jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
* [<span data-ttu-id="8e511-158">Uruchamianie zadań Sqoop w usłudze HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8e511-158">Run Sqoop jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
* [<span data-ttu-id="8e511-159">Uruchamianie zadań Oozie w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8e511-159">Run Oozie jobs in HDInsight</span></span>](hdinsight-use-oozie.md)

