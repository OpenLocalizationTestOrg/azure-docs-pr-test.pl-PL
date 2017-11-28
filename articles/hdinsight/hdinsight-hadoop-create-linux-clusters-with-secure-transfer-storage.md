---
title: "aaaCreate Hadoop klaster z zapewnienia bezpiecznego transferu kont magazynu w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate klastrów usługi HDInsight z zapewnienia bezpiecznego transferu włączone konta magazynu platformy Azure."
keywords: hadoop getting started,hadoop linux,hadoop quickstart,secure transfer,azure storage account
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="1b225-104">Tworzenie klastra usługi Hadoop z kontami magazynu z bezpiecznym transferem w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b225-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="1b225-105">Witaj [bezpieczny transfer wymagane](../storage/common/storage-require-secure-transfer.md) funkcji zwiększa bezpieczeństwo hello konta magazynu Azure, wymuszając wszystkich żądań tooyour konta za pośrednictwem bezpiecznego połączenia.</span><span class="sxs-lookup"><span data-stu-id="1b225-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="1b225-106">Ten schemat wasbs funkcji i hello są obsługiwane tylko przez wersja klastra usługi HDInsight 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1b225-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1b225-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1b225-107">Prerequisites</span></span>
<span data-ttu-id="1b225-108">Przed rozpoczęciem tego samouczka potrzebna będzie:</span><span class="sxs-lookup"><span data-stu-id="1b225-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="1b225-109">**Subskrypcja platformy Azure**: toocreate bezpłatne konto próbne jeden miesiąc, przejdź zbyt[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="1b225-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="1b225-110">**Konto usługi Azure Storage z włączonym bezpiecznym transferem**.</span><span class="sxs-lookup"><span data-stu-id="1b225-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="1b225-111">Witaj instrukcje, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) i [wymaga zapewnienia bezpiecznego transferu](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="1b225-112">**Kontener obiektów Blob na koncie magazynu hello**.</span><span class="sxs-lookup"><span data-stu-id="1b225-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="1b225-113">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="1b225-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="1b225-114">W tej sekcji tworzysz klaster Hadoop w usłudze HDInsight przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="1b225-115">Szablon Hello znajduje się w [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="1b225-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="1b225-116">Znajomość szablonów usługi Resource Manager nie jest wymagana do korzystania z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1b225-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="1b225-117">Inne metody tworzenia klastrów i opis właściwości hello używane w tym samouczku, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="1b225-118">Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b225-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="1b225-119">Wykonaj hello instrukcje toocreate hello klastra z hello następujące specyfikacje:</span><span class="sxs-lookup"><span data-stu-id="1b225-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="1b225-120">Określ wersję usługi HDInsight na 3.6.</span><span class="sxs-lookup"><span data-stu-id="1b225-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="1b225-121">Wersja domyślna Hello jest 3.5.</span><span class="sxs-lookup"><span data-stu-id="1b225-121">hello default version is 3.5.</span></span> <span data-ttu-id="1b225-122">Wymagana jest wersja 3.6 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="1b225-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="1b225-123">Określ konto magazynu z włączonym bezpiecznym transferem.</span><span class="sxs-lookup"><span data-stu-id="1b225-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="1b225-124">Krótka nazwa używana dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="1b225-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="1b225-125">Zarówno hello konta magazynu i kontener obiektów blob hello musi zostać utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1b225-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="1b225-126">Witaj instrukcje, zobacz [Utwórz klaster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="1b225-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="1b225-127">Jeśli używasz tooprovide akcji skryptu w plikach konfiguracji, należy użyć wasbs w hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="1b225-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="1b225-128">fs.defaultFS (lokacja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="1b225-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="1b225-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="1b225-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="1b225-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="1b225-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="1b225-131">Dodawanie kolejnych kont magazynu</span><span class="sxs-lookup"><span data-stu-id="1b225-131">Add additional storage accounts</span></span>

<span data-ttu-id="1b225-132">Istnieje kilka opcji tooadd dodatkowe zapewnienia bezpiecznego transferu włączone kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="1b225-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="1b225-133">Szablon usługi Azure Resource Manager hello w ostatniej sekcji hello zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="1b225-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="1b225-134">Tworzenie klastra przy użyciu hello [portalu Azure](https://portal.azure.com) i określ połączonym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b225-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="1b225-135">Użyj skryptu akcji tooadd dodatkowe zapewnienia bezpiecznego transferu włączyć magazyn kont tooan istniejącym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1b225-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="1b225-136">Aby uzyskać więcej informacji, zobacz [dodać dodatkowy magazyn kont tooHDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b225-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b225-137">Next steps</span></span>
<span data-ttu-id="1b225-138">W tym samouczku uzyskanych jak toocreate klastra usługi HDInsight, a następnie włączyć bezpieczny transfer toohello kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b225-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="1b225-139">toolearn więcej informacji na temat analizowania danych z usługą HDInsight, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="1b225-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="1b225-140">toolearn więcej informacji o korzystaniu z programu Hive z usługą HDInsight, w tym, jak tooperform Hive zapytań z programu Visual Studio, zobacz [używanie Hive z usługą HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="1b225-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="1b225-141">toolearn temat Pig, języka używany tootransform danych, zobacz [Use Pig z usługą HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="1b225-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="1b225-142">toolearn o MapReduce, sposób programy toowrite, które przetwarzają dane w usłudze Hadoop, zobacz [Użyj MapReduce z usługą HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="1b225-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="1b225-143">toolearn o za pomocą hello narzędzi HDInsight Visual Studio tooanalyze danych w usłudze HDInsight, zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="1b225-144">więcej informacji na temat sposobu HDInsight przechowuje dane toolearn lub tooget danych do usługi HDInsight, zobacz temat hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="1b225-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="1b225-145">Aby uzyskać informacje o sposobie używania usługi Azure Storage przez usługę HDInsight, zobacz [Używanie usługi Azure Storage z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="1b225-146">Aby uzyskać informacje na temat tooupload tooHDInsight danych, zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="1b225-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="1b225-147">toolearn więcej informacji na temat tworzenia i zarządzania nią klastra usługi HDInsight, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="1b225-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="1b225-148">toolearn o zarządzaniu klaster usługi HDInsight opartej na systemie Linux, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="1b225-149">toolearn więcej informacji na temat opcji hello można wybrać podczas tworzenia klastra usługi HDInsight, zobacz [tworzenia HDInsight w systemie Linux przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="1b225-150">Jeśli zapoznali się z systemem Linux i usługę Hadoop, ale mają tooknow szczegóły dotyczące usługi Hadoop na powitania HDInsight, zobacz [pracy z usługą HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="1b225-151">Artykuł zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1b225-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="1b225-152">Adresy URL dla usług uruchamianych w klastrze hello, takich jak Ambari i WebHCat</span><span class="sxs-lookup"><span data-stu-id="1b225-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="1b225-153">Witaj lokalizację plików usługi Hadoop oraz przykłady hello lokalnego systemu plików</span><span class="sxs-lookup"><span data-stu-id="1b225-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="1b225-154">Użyj Hello z usługi Azure Storage (WASB) zamiast systemu plików HDFS jako hello domyślnego magazynu danych</span><span class="sxs-lookup"><span data-stu-id="1b225-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


