---
title: "aaaUse toocreate szablony usługi Azure HDInsight i usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj toocreate szablonów usługi Azure Resource Manager i klastry usługi HDInsight za pomocą usługi Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="ac498-103">Tworzenie klastra usługi HDInsight z Data Lake Store za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ac498-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac498-104">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="ac498-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ac498-105">Przy użyciu programu PowerShell (do magazynu domyślnego)</span><span class="sxs-lookup"><span data-stu-id="ac498-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ac498-106">Przy użyciu programu PowerShell (dla dodatkowego magazynu)</span><span class="sxs-lookup"><span data-stu-id="ac498-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ac498-107">Za pomocą Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="ac498-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ac498-108">Dowiedz się, jak klaster toouse tooconfigure programu PowerShell usługi Azure HDInsight z usługi Azure Data Lake Store, **jako dodatkowego magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ac498-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="ac498-109">Dla typów obsługiwanych klastra usługi Data Lake Store można użyć jako domyślnego magazynu lub konto dodatkowego miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="ac498-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="ac498-110">W przypadku usługi Data Lake Store jako dodatkowego magazynu hello domyślne konto magazynu dla klastrów hello będzie nadal Azure blob Storage (WASB) i hello plików związanych z klastrem (takich jak dzienniki, itp.) są zapisywane nadal toohello domyślny magazyn, podczas danych hello które Chcę tooprocess mogą być przechowywane w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ac498-111">Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpływa na wydajność lub pamięć masową toohello tooread/zapisu możliwości hello z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ac498-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ac498-112">W magazynie klastra usługi HDInsight przy użyciu usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac498-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ac498-113">Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ac498-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ac498-114">Klastry HDInsight toocreate opcji z dostępem do tooData Lake Store jako domyślny magazyn jest dostępny dla usługi HDInsight w wersji 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="ac498-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="ac498-115">Klastry HDInsight toocreate opcji z dostępem do tooData Lake Store jako dodatkowego magazynu jest dostępna dla usługi HDInsight w wersji 3.2, 3.4, 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="ac498-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ac498-116">W tym artykule możemy zainicjować klastra usługi Hadoop z usługą Data Lake Store jako dodatkowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="ac498-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ac498-117">Aby uzyskać instrukcje dotyczące sposobu toocreate usługi Hadoop klaster z usługi Data Lake Store jako domyślnego magazynu, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac498-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac498-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac498-118">Prerequisites</span></span>
<span data-ttu-id="ac498-119">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ac498-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="ac498-120">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="ac498-120">**An Azure subscription**.</span></span> <span data-ttu-id="ac498-121">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac498-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ac498-122">**Program Azure PowerShell 1.0 lub nowszy**.</span><span class="sxs-lookup"><span data-stu-id="ac498-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ac498-123">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac498-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ac498-124">**Nazwy głównej usługi Azure Active Directory usługi**.</span><span class="sxs-lookup"><span data-stu-id="ac498-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ac498-125">Kroki opisane w tym samouczku zawierają instrukcje na temat toocreate nazwy głównej usługi w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac498-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="ac498-126">Jednak należy usługi Azure AD administratora toobe stanie toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac498-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="ac498-127">Jeśli jesteś administratorem usługi Azure AD, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="ac498-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="ac498-128">**Jeśli nie jesteś administratorem usługi Azure AD**, nie będą mogli tooperform hello kroki wymagane toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ac498-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="ac498-129">W takim przypadku administrator usługi Azure AD należy najpierw utworzyć nazwy głównej usługi przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ac498-130">Także hello nazwy głównej usługi muszą zostać utworzone za pomocą certyfikatu, zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="ac498-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="ac498-131">Tworzenie klastra usługi HDInsight z usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac498-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="ac498-132">Hello szablonu usługi Resource Manager i wymagania wstępne hello przy użyciu szablonu hello są dostępne w witrynie GitHub pod [wdrażanie klastra usługi HDInsight Linux z nowej usługi Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="ac498-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="ac498-133">Wykonaj instrukcje hello podanych w tym toocreate łącze klastra usługi HDInsight z usługi Azure Data Lake Store jako dodatkowego magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ac498-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="ac498-134">instrukcje Hello w wymienionych powyżej łącze hello wymagają programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac498-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="ac498-135">Przed rozpoczęciem pracy z tych instrukcji upewnij się, że możesz zalogować się w tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac498-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="ac498-136">Na pulpicie otwórz nowe okno programu Azure PowerShell, a następnie wprowadź powitania po fragmentów.</span><span class="sxs-lookup"><span data-stu-id="ac498-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="ac498-137">Gdy zostanie wyświetlony monit o toolog, upewnij się, że logujesz się jako jeden hello/właścicieli subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="ac498-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="ac498-138">Przekaż przykładowe dane toohello Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac498-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="ac498-139">Szablon usługi Resource Manager Hello tworzy nowe konto usługi Data Lake Store i kojarzy ją z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ac498-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="ac498-140">Teraz musi przekazać niektóre przykładowe dane toohello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="ac498-141">Będziesz potrzebować te dane później w zadaniach samouczek toorun hello z klastra usługi HDInsight, które uzyskują dostęp do danych w hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="ac498-142">Aby uzyskać instrukcje dotyczące tooupload danych, zobacz [przekazać plik tooyour usługi Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="ac498-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="ac498-143">Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="ac498-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="ac498-144">Ustawić odpowiednich list ACL na powitania przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="ac498-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="ac498-145">toomake się, że jest dostępny z klastra usługi HDInsight hello hello przykładowe dane, które zostaną przesłane, należy się upewnić, że aplikacji hello Azure AD, która jest używana tooestablish tożsamości między klastrem usługi HDInsight hello i usługi Data Lake Store ma dostęp toohello plik lub folder, który ma w trakcie tooaccess.</span><span class="sxs-lookup"><span data-stu-id="ac498-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="ac498-146">toodo, wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="ac498-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="ac498-147">Znajdź nazwę hello hello aplikacji usługi Azure AD, który jest skojarzony z klastrem usługi HDInsight i hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="ac498-148">Tooopen hello HDInsight bloku klastra utworzonej przy użyciu szablonu usługi Resource Manager hello jest jednym ze sposobów toolook hello nazwy, kliknij przycisk hello **tożsamość usługi AAD klastra** , a następnie wyszukaj wartość hello **nazwy głównej usługi Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="ac498-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="ac498-149">Teraz podaj toothis dostępu do aplikacji usługi Azure AD na powitania plik lub folder, które mają tooaccess z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ac498-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="ac498-150">list ACL praw hello tooset na powitania plik lub folder, w usłudze Data Lake Store, zobacz [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="ac498-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="ac498-151">Uruchom zadania testowe na powitania HDInsight klastra toouse hello usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac498-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="ac498-152">Po skonfigurowaniu klastra usługi HDInsight można uruchamiać zadania testowego na powitania klastra tootest tego hello HDInsight klastra mogą uzyskiwać dostęp do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ac498-153">toodo tak, zostanie uruchomiony przykładowe zadania Hive, która tworzy tabelę przy użyciu hello przykładowych danych, aby przekazać wcześniejszych tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="ac498-154">W tej sekcji będzie SSH do klastra usługi HDInsight w systemie Linux i uruchamiania hello przykładowe zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="ac498-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="ac498-155">Jeśli używasz klienta z systemem Windows, firma Microsoft zaleca używanie **PuTTY**, który można pobrać z [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="ac498-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="ac498-156">Aby uzyskać więcej informacji na temat używania programu PuTTY, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ac498-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="ac498-157">Po nawiązaniu połączenia, należy uruchomić hello Hive interfejsu wiersza polecenia przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ac498-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="ac498-158">Używając hello interfejsu wiersza polecenia, wprowadź następujące instrukcje toocreate nowej tabeli o nazwie hello **pojazdów** przy użyciu hello przykładowe dane w hello usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="ac498-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="ac498-159">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="ac498-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ac498-160">Dostęp Data Lake Store za pomocą poleceń systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="ac498-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ac498-161">Po skonfigurowaniu hello HDInsight klastra toouse Data Lake Store można użyć hello systemu plików HDFS powłoki poleceń tooaccess hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="ac498-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="ac498-162">W tej sekcji będzie SSH do klastra usługi HDInsight w systemie Linux i hello wykonywania poleceń systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="ac498-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="ac498-163">Jeśli używasz klienta z systemem Windows, firma Microsoft zaleca używanie **PuTTY**, który można pobrać z [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="ac498-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="ac498-164">Aby uzyskać więcej informacji na temat używania programu PuTTY, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ac498-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="ac498-165">Po nawiązaniu połączenia użyj hello następujące pliki poleceń systemu plików HDFS hello toolist w hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="ac498-166">Powinny pojawić się plik hello czy przesłany wcześniejszych toohello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac498-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="ac498-167">Można również użyć hello `hdfs dfs -put` polecenia tooupload toohello niektórych plików usługi Data Lake Store, a następnie użyj `hdfs dfs -ls` tooverify czy hello pliki zostały pomyślnie przekazane.</span><span class="sxs-lookup"><span data-stu-id="ac498-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac498-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac498-168">Next steps</span></span>
* [<span data-ttu-id="ac498-169">Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac498-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
