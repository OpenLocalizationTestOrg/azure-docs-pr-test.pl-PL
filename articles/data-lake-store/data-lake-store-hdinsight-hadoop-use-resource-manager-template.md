---
title: "Użyj szablonów platformy Azure, aby utworzyć HDInsight i usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Korzystanie z szablonów usługi Azure Resource Manager do tworzenia i klastry usługi HDInsight za pomocą usługi Azure Data Lake Store"
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="5370c-103">Tworzenie klastra usługi HDInsight z Data Lake Store za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5370c-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5370c-104">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="5370c-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="5370c-105">Przy użyciu programu PowerShell (do magazynu domyślnego)</span><span class="sxs-lookup"><span data-stu-id="5370c-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="5370c-106">Przy użyciu programu PowerShell (dla dodatkowego magazynu)</span><span class="sxs-lookup"><span data-stu-id="5370c-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="5370c-107">Za pomocą Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="5370c-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="5370c-108">Dowiedz się, jak skonfigurować klaster usługi HDInsight z usługi Azure Data Lake Store, przy użyciu programu Azure PowerShell **jako dodatkowego magazynu**.</span><span class="sxs-lookup"><span data-stu-id="5370c-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="5370c-109">Dla typów obsługiwanych klastra usługi Data Lake Store można użyć jako domyślnego magazynu lub konto dodatkowego miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="5370c-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="5370c-110">W przypadku usługi Data Lake Store jako dodatkowego magazynu domyślne konto magazynu dla klastrów nadal będzie Azure blob Storage (WASB) i plików związanych z klastrem (na przykład dzienników itp.) nadal są zapisywane do magazynu domyślnego, gdy mogą być przechowywane dane, które ma być przetwarzane w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="5370c-111">Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpływa na wydajność lub możliwości odczytu i zapisu do magazynu z klastra.</span><span class="sxs-lookup"><span data-stu-id="5370c-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="5370c-112">W magazynie klastra usługi HDInsight przy użyciu usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5370c-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="5370c-113">Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5370c-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="5370c-114">Możliwość tworzenia klastrów usługi HDInsight z dostępem do usługi Data Lake Store jako domyślny magazyn jest dostępny dla usługi HDInsight w wersji 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="5370c-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="5370c-115">Możliwość tworzenia klastrów usługi HDInsight z dostępem do usługi Data Lake Store jako dodatkowego magazynu jest dostępna dla usługi HDInsight w wersji 3.2, 3.4, 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="5370c-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="5370c-116">W tym artykule możemy zainicjować klastra usługi Hadoop z usługą Data Lake Store jako dodatkowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="5370c-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="5370c-117">Aby uzyskać instrukcje dotyczące sposobu tworzenia klastra usługi Hadoop z usługi Data Lake Store jako domyślnego magazynu, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5370c-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5370c-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5370c-118">Prerequisites</span></span>
<span data-ttu-id="5370c-119">Przed przystąpieniem do wykonania kroków opisanych w tym samouczku należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="5370c-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5370c-120">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="5370c-120">**An Azure subscription**.</span></span> <span data-ttu-id="5370c-121">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5370c-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5370c-122">**Program Azure PowerShell 1.0 lub nowszy**.</span><span class="sxs-lookup"><span data-stu-id="5370c-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="5370c-123">Zobacz artykuł [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5370c-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5370c-124">**Nazwy głównej usługi Azure Active Directory usługi**.</span><span class="sxs-lookup"><span data-stu-id="5370c-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="5370c-125">Kroki opisane w tym samouczku zawierają instrukcje dotyczące sposobu tworzenia nazwy głównej usługi w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5370c-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="5370c-126">Jednak musi być administrator usługi Azure AD, aby można było utworzyć nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="5370c-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="5370c-127">Jeśli jesteś administratorem usługi Azure AD, możesz pominąć te wymagania wstępne i kontynuować samouczka.</span><span class="sxs-lookup"><span data-stu-id="5370c-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="5370c-128">**Jeśli nie jesteś administratorem usługi Azure AD**, nie można wykonać kroki wymagane do utworzenia nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="5370c-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="5370c-129">W takim przypadku administrator usługi Azure AD należy najpierw utworzyć nazwy głównej usługi przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="5370c-130">Ponadto nazwy głównej usługi musi być utworzony przy użyciu certyfikatu, zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="5370c-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="5370c-131">Tworzenie klastra usługi HDInsight z usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5370c-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="5370c-132">Szablon usługi Resource Manager i wymagań wstępnych dotyczących używania szablonu, są dostępne w witrynie GitHub pod [wdrażanie klastra usługi HDInsight Linux z nowej usługi Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="5370c-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="5370c-133">Postępuj zgodnie z instrukcjami w to łącze, aby utworzyć klaster usługi HDInsight za pomocą usługi Azure Data Lake Store jako dodatkowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="5370c-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="5370c-134">Instrukcje w wymienionych powyżej łącze wymagają programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5370c-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="5370c-135">Przed rozpoczęciem pracy z tych instrukcji upewnij się, że logujesz się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5370c-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="5370c-136">Na pulpicie otwórz nowe okno programu Azure PowerShell, a następnie wprowadź poniższe fragmenty kodu.</span><span class="sxs-lookup"><span data-stu-id="5370c-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="5370c-137">Po wyświetleniu monitu zaloguj się jako jeden z administratorów/właścicieli subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="5370c-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="5370c-138">Przekaż przykładowe dane do usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5370c-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="5370c-139">Szablon usługi Resource Manager tworzy nowe konto usługi Data Lake Store i kojarzy ją z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5370c-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="5370c-140">Teraz należy przesłać przykładowych danych do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="5370c-141">Te dane potrzebne później w samouczku do uruchomienia zadań z klastra usługi HDInsight, że dostęp do danych w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="5370c-142">Aby uzyskać instrukcje na temat przekazywania danych, zobacz [przekazania pliku do usługi Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="5370c-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="5370c-143">Jeśli szukasz przykładowych danych do przekazania, możesz pobrać folder **Ambulance Data** z [repozytorium Git usługi Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="5370c-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="5370c-144">Ustawić odpowiednich list ACL na przykładowych danych</span><span class="sxs-lookup"><span data-stu-id="5370c-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="5370c-145">Aby upewnić się, że jest dostępny z klastra usługi HDInsight przykładowe dane, które zostaną przesłane, upewnij się, że jest używany do ustanawiania tożsamości między klastrem usługi HDInsight i usługi Data Lake Store miał dostęp do pliku/folderu, który próbujesz uzyskać dostęp do aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5370c-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="5370c-146">Aby to zrobić, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="5370c-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="5370c-147">Znajdź nazwę aplikacji usługi Azure AD, który jest skojarzony z klastrem usługi HDInsight i usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="5370c-148">Jednym ze sposobów Szukaj nazwy jest, aby otworzyć blok klastra usługi HDInsight utworzonego przy użyciu szablonu usługi Resource Manager, kliknij przycisk **tożsamość usługi AAD klastra** , a następnie wyszukaj wartość **nazwę wyświetlaną nazwę główną usługi**.</span><span class="sxs-lookup"><span data-stu-id="5370c-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="5370c-149">Teraz zapewniają dostęp do tej aplikacji usługi Azure AD na plik lub folder, który chcesz uzyskać dostęp z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5370c-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="5370c-150">Aby ustawić prawo listy ACL na plik lub folder, w usłudze Data Lake Store, zobacz [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="5370c-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="5370c-151">Uruchom zadania testowe w klastrze usługi HDInsight do użycia usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5370c-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="5370c-152">Po skonfigurowaniu klastra usługi HDInsight można uruchamiać zadania testowego w klastrze, aby sprawdzić, czy klastra usługi HDInsight można uzyskać dostępu do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="5370c-153">Aby to zrobić, zostanie uruchomiony przykładowe zadania Hive, która tworzy tabelę przy użyciu przykładowych danych, który został wcześniej przekazany do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="5370c-154">W tej sekcji zostanie SSH do klastra usługi HDInsight w systemie Linux i uruchomić przykładowe zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="5370c-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="5370c-155">Jeśli używasz klienta z systemem Windows, firma Microsoft zaleca używanie **PuTTY**, który można pobrać z [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="5370c-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="5370c-156">Aby uzyskać więcej informacji na temat używania programu PuTTY, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="5370c-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="5370c-157">Po nawiązaniu połączenia, należy uruchomić interfejsu wiersza polecenia Hive za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5370c-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="5370c-158">Przy użyciu interfejsu wiersza polecenia, wpisz poniższe instrukcje, aby utworzyć nową tabelę o nazwie **pojazdów** przy użyciu przykładowych danych w usłudze Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="5370c-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="5370c-159">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="5370c-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="5370c-160">Dostęp Data Lake Store za pomocą poleceń systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="5370c-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="5370c-161">Po skonfigurowaniu klastra usługi HDInsight do użycia usługi Data Lake Store służy poleceń powłoki systemu plików HDFS można uzyskać dostępu do magazynu.</span><span class="sxs-lookup"><span data-stu-id="5370c-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="5370c-162">W tej sekcji zostanie SSH w systemie Linux usługi HDInsight klastra, a następnie uruchom polecenia systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="5370c-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="5370c-163">Jeśli używasz klienta z systemem Windows, firma Microsoft zaleca używanie **PuTTY**, który można pobrać z [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="5370c-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="5370c-164">Aby uzyskać więcej informacji na temat używania programu PuTTY, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="5370c-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="5370c-165">Po nawiązaniu połączenia użyj następującego polecenia systemu plików HDFS, aby wyświetlić listę plików w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="5370c-166">Powinny pojawić się plik, który został wcześniej przekazany do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5370c-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="5370c-167">Można również użyć `hdfs dfs -put` polecenie, aby przekazać pliki do usługi Data Lake Store, a następnie użyj `hdfs dfs -ls` Aby sprawdzić, czy pliki zostały pomyślnie przekazane.</span><span class="sxs-lookup"><span data-stu-id="5370c-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5370c-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5370c-168">Next steps</span></span>
* [<span data-ttu-id="5370c-169">Kopiowanie danych z obiektów blob magazynu Azure do usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5370c-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
