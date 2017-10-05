---
title: "Tworzenie klastra usługi Hadoop z kontami magazynu z bezpiecznym transferem w usłudze Azure HDInsight | Microsoft Docs"
description: "Dowiedz się, jak tworzyć klastry usługi HDInsight z kontami magazynu platformy Azure z bezpiecznym transferem."
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
ms.openlocfilehash: 370b2f081930fe88527436a1a127309aed6681f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="cb46f-104">Tworzenie klastra usługi Hadoop z kontami magazynu z bezpiecznym transferem w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb46f-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="cb46f-105">Funkcja [Wymagany bezpieczny transfer](../storage/common/storage-require-secure-transfer.md) poprawia bezpieczeństwo konta usługi Azure Storage poprzez wymuszanie kierowania wszystkich zapytań do konta przez zabezpieczone połączenie.</span><span class="sxs-lookup"><span data-stu-id="cb46f-105">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span></span> <span data-ttu-id="cb46f-106">Funkcja ta oraz schemat wasbs są obsługiwane tylko w klastrze usługi HDInsight w wersji 3.6 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="cb46f-106">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cb46f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb46f-107">Prerequisites</span></span>
<span data-ttu-id="cb46f-108">Przed rozpoczęciem tego samouczka potrzebna będzie:</span><span class="sxs-lookup"><span data-stu-id="cb46f-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="cb46f-109">**Subskrypcja platformy Azure**: aby utworzyć bezpłatne konto próbne na jeden miesiąc, przejdź do [azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="cb46f-109">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="cb46f-110">**Konto usługi Azure Storage z włączonym bezpiecznym transferem**.</span><span class="sxs-lookup"><span data-stu-id="cb46f-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="cb46f-111">Aby uzyskać instrukcje, zobacz [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) oraz [Wymaganie bezpiecznego transferu](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-111">For the instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="cb46f-112">**Kontener obiektów blob na koncie magazynu**.</span><span class="sxs-lookup"><span data-stu-id="cb46f-112">**A Blob container on the storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="cb46f-113">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="cb46f-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="cb46f-114">W tej sekcji tworzysz klaster Hadoop w usłudze HDInsight przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="cb46f-115">Szablon znajduje się w witrynie [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="cb46f-115">The template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="cb46f-116">Znajomość szablonów usługi Resource Manager nie jest wymagana do korzystania z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="cb46f-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="cb46f-117">Inne metody tworzenia klastrów i opis właściwości używanych w tym samouczku znajdziesz w artykule [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-117">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="cb46f-118">Kliknij poniższy obraz, aby zalogować się do platformy Azure i otworzyć szablon usługi Resource Manager w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cb46f-118">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="cb46f-119">Postępuj zgodnie z instrukcjami, aby utworzyć klaster o następujących specyfikacjach:</span><span class="sxs-lookup"><span data-stu-id="cb46f-119">Follow the instructions to create the cluster with the following specifications:</span></span> 

    - <span data-ttu-id="cb46f-120">Określ wersję usługi HDInsight na 3.6.</span><span class="sxs-lookup"><span data-stu-id="cb46f-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="cb46f-121">Domyślna wersja to 3.5.</span><span class="sxs-lookup"><span data-stu-id="cb46f-121">The default version is 3.5.</span></span> <span data-ttu-id="cb46f-122">Wymagana jest wersja 3.6 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="cb46f-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="cb46f-123">Określ konto magazynu z włączonym bezpiecznym transferem.</span><span class="sxs-lookup"><span data-stu-id="cb46f-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="cb46f-124">Użyj krótkiej nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="cb46f-124">Use short name for the storage account.</span></span>
    - <span data-ttu-id="cb46f-125">Konto magazynu i kontener obiektów blob należy utworzyć wcześniej.</span><span class="sxs-lookup"><span data-stu-id="cb46f-125">Both the storage account and the blob container must be created beforehand.</span></span> 

    <span data-ttu-id="cb46f-126">Aby uzyskać instrukcje, zobacz [Tworzenie klastra](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="cb46f-126">For the instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="cb46f-127">Jeśli użyjesz akcji skryptu do udostępnienia własnych plików konfiguracyjnych, musisz użyć rozwiązania wasbs w następujących ustawieniach:</span><span class="sxs-lookup"><span data-stu-id="cb46f-127">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span></span>

- <span data-ttu-id="cb46f-128">fs.defaultFS (lokacja podstawowa)</span><span class="sxs-lookup"><span data-stu-id="cb46f-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="cb46f-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="cb46f-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="cb46f-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="cb46f-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="cb46f-131">Dodawanie kolejnych kont magazynu</span><span class="sxs-lookup"><span data-stu-id="cb46f-131">Add additional storage accounts</span></span>

<span data-ttu-id="cb46f-132">Dostępnych jest kilka opcji dodawania kolejnych kont magazynu z bezpiecznym transferem:</span><span class="sxs-lookup"><span data-stu-id="cb46f-132">There are several options to add additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="cb46f-133">Zmodyfikuj szablon usługi Azure Resource Manager w ostatniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="cb46f-133">Modify the Azure Resource Manager template in the last section.</span></span>
- <span data-ttu-id="cb46f-134">Utwórz klaster przy użyciu witryny [Azure Portal](https://portal.azure.com) i określ połączone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="cb46f-134">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="cb46f-135">Użyj akcji skryptu, aby dodać kolejne konta magazynu z bezpiecznym transferem do istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb46f-135">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span></span>  <span data-ttu-id="cb46f-136">Aby uzyskać więcej informacji, zobacz [Dodawanie kolejnych kont magazynu do usługi HDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-136">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb46f-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb46f-137">Next steps</span></span>
<span data-ttu-id="cb46f-138">W tym samouczku zawarto informacje dotyczące tworzenia klastra usługi HDInsight oraz włączania bezpiecznego transferu na kontach magazynu.</span><span class="sxs-lookup"><span data-stu-id="cb46f-138">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span></span>

<span data-ttu-id="cb46f-139">Aby dowiedzieć się więcej na temat analizowania danych za pomocą usługi HDInsight, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cb46f-139">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="cb46f-140">Aby dowiedzieć się więcej o korzystaniu z programu Hive z usługą HDInsight, w tym poznać sposoby wykonywania zapytań Hive z programu Visual Studio, zobacz artykuł [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="cb46f-140">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="cb46f-141">Aby dowiedzieć się więcej na temat języka Pig, używanego do przekształcania danych, zobacz [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="cb46f-141">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="cb46f-142">Aby dowiedzieć się więcej o MapReduce, sposobie pisania programów przetwarzających dane w usłudze Hadoop, zobacz [Używanie MapReduce z usługą HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="cb46f-142">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="cb46f-143">Aby dowiedzieć się więcej o używaniu narzędzi HDInsight Tools for Visual Studio do analizowania danych w usłudze HDInsight, zobacz [Wprowadzenie do używania narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-143">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="cb46f-144">Aby dowiedzieć się więcej o sposobie przechowywania danych przez usługę HDInsight lub sposobie przesyłania danych do usługi HDInsight, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cb46f-144">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="cb46f-145">Aby uzyskać informacje o sposobie używania usługi Azure Storage przez usługę HDInsight, zobacz [Używanie usługi Azure Storage z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="cb46f-146">Aby uzyskać informacje na temat przekazywania danych do usługi HDInsight, zobacz [Przekazywanie danych do usługi HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="cb46f-146">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="cb46f-147">Aby dowiedzieć się więcej o tworzeniu klastra usługi HDInsight i zarządzaniu nim, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cb46f-147">To learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="cb46f-148">Aby uzyskać więcej informacji na temat zarządzania opartym na systemie Linux klastrem usługi HDInsight, zobacz [Zarządzanie klastrami usługi HDInsight za pomocą narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-148">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="cb46f-149">Aby dowiedzieć się więcej na temat opcji, które można wybrać podczas tworzenia klastra usługi HDInsight, zobacz [Tworzenie klastra usługi HDInsight w systemie Linux przy użyciu niestandardowych opcji](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-149">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="cb46f-150">Jeśli znasz system Linux i usługę Hadoop, ale chcesz poznać szczegóły dotyczące usługi Hadoop w usłudze HDInsight, zobacz [Praca z usługą HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="cb46f-150">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="cb46f-151">Artykuł zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="cb46f-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="cb46f-152">Adresy URL dla usług uruchamianych w klastrze, takich jak Ambari i WebHCat</span><span class="sxs-lookup"><span data-stu-id="cb46f-152">URLs for services hosted on the cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="cb46f-153">Lokalizacja plików usługi Hadoop oraz przykłady lokalnego systemu plików</span><span class="sxs-lookup"><span data-stu-id="cb46f-153">The location of Hadoop files and examples on the local file system</span></span>
  * <span data-ttu-id="cb46f-154">Korzystanie z usługi Azure Storage (WASB) zamiast systemu plików HDFS jako domyślnego magazynu danych</span><span class="sxs-lookup"><span data-stu-id="cb46f-154">The use of Azure Storage (WASB) instead of HDFS as the default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


