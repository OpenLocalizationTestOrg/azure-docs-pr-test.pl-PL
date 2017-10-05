---
title: "Apache Spark przesyłania strumieniowego z Kafka - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak służące do lub wychodzący przy użyciu DStreams Kafka Apache Spark Apache Spark do transmisji danych. W tym przykładzie można przesyłać strumieniowo dane za pomocą notesu Jupyter z platformy Spark w usłudze HDInsight."
keywords: "przykład kafka, dozorcy kafka, spark, przesyłanie strumieniowe kafka, przesyłania strumieniowego przykład kafka spark"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="c4380-105">Apache Spark przesyłania strumieniowego (DStream) przykład: Kafka (wersja zapoznawcza) w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4380-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="c4380-106">Dowiedz się, jak używać Spark Apache Spark do transmisji danych do lub wychodzący Kafka Apache na HDInsight przy użyciu DStreams.</span><span class="sxs-lookup"><span data-stu-id="c4380-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="c4380-107">W tym przykładzie użyto notesu Jupyter w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="c4380-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="c4380-108">Kroki opisane w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Spark w usłudze HDInsight i Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4380-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="c4380-109">Te klastry są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu klastra Spark do bezpośredniego komunikowania się z Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="c4380-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="c4380-110">Po zakończeniu kroków w tym dokumencie, pamiętaj, aby usuwać te klastry, aby zapobiec zmianom nadmiarowe.</span><span class="sxs-lookup"><span data-stu-id="c4380-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="c4380-111">Tworzenie klastrów</span><span class="sxs-lookup"><span data-stu-id="c4380-111">Create the clusters</span></span>

<span data-ttu-id="c4380-112">Kafka Apache na HDInsight nie zapewnia dostępu do brokerzy Kafka za pośrednictwem publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="c4380-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="c4380-113">Wszystkie elementy, które komunikuje się Kafka musi być w tej samej sieci wirtualnej platformy Azure jako węzły w klastrze Kafka.</span><span class="sxs-lookup"><span data-stu-id="c4380-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="c4380-114">W tym przykładzie zarówno Kafka, jak i Spark klastrach znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4380-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="c4380-115">Na poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami:</span><span class="sxs-lookup"><span data-stu-id="c4380-115">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram klastry Spark i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="c4380-117">Chociaż Kafka sam jest ograniczone do komunikacji w sieci wirtualnej, są dostępne inne usługi w klastrze, takich jak SSH i Ambari w Internecie.</span><span class="sxs-lookup"><span data-stu-id="c4380-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="c4380-118">Aby uzyskać więcej informacji na portach publicznego dostępne z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="c4380-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="c4380-119">Podczas tworzenia sieci wirtualnej platformy Azure, Kafka, i Spark klastrów ręcznie, łatwiej jest użyć szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4380-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="c4380-120">Wykonaj następujące kroki, aby wdrożyć sieci wirtualnej platformy Azure, Kafka i Spark klastrów do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4380-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="c4380-121">Poniższy przycisk umożliwia logowanie do platformy Azure i otwórz szablon w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c4380-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="c4380-122">Szablon usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="c4380-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c4380-123">Aby zapewnić dostępność platformy Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzy węzły procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="c4380-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="c4380-124">Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="c4380-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="c4380-125">Ten szablon umożliwia tworzenie klastra usługi HDInsight 3,6 Kafka i Spark.</span><span class="sxs-lookup"><span data-stu-id="c4380-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="c4380-126">Użyj poniższych informacji, aby wypełnić wpisy na **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="c4380-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="c4380-128">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="c4380-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="c4380-129">Ta grupa zawiera klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4380-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="c4380-130">**Lokalizacja**: Wybierz lokalizację lokalizacji geograficznej blisko.</span><span class="sxs-lookup"><span data-stu-id="c4380-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="c4380-131">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa platformy Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="c4380-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="c4380-132">Na przykład wprowadzenie **hdi** tworzy Spark klastra o nazwie spark hdi__ i Kafka klastra o nazwie **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="c4380-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="c4380-133">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora klastrów platformy Spark i Kafka.</span><span class="sxs-lookup"><span data-stu-id="c4380-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c4380-134">**Hasło logowania klastra**: hasła użytkownika administratora klastrów platformy Spark i Kafka.</span><span class="sxs-lookup"><span data-stu-id="c4380-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c4380-135">**Nazwa użytkownika SSH**: użytkownika SSH do tworzenia klastrów platformy Spark i Kafka.</span><span class="sxs-lookup"><span data-stu-id="c4380-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c4380-136">**Hasło SSH**: hasło dla użytkownika SSH dla klastrów Spark i Kafka.</span><span class="sxs-lookup"><span data-stu-id="c4380-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="c4380-137">Odczyt **warunków i postanowień**, a następnie wybierz **akceptuję warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="c4380-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="c4380-138">Ponadto sprawdź **Przypnij do pulpitu nawigacyjnego** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="c4380-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="c4380-139">Tworzenie klastrów trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="c4380-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="c4380-140">Po utworzeniu zasoby są przekierowywane do bloku grupy zasobów, zawierającą klastrów i pulpitu nawigacyjnego sieci web.</span><span class="sxs-lookup"><span data-stu-id="c4380-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej i klastrów](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="c4380-142">Należy zauważyć, że nazwy klastrów usługi HDInsight są **nazwę BAZOWĄ spark** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest podana nazwa do szablonu.</span><span class="sxs-lookup"><span data-stu-id="c4380-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="c4380-143">Te nazwy można użyć w kolejnych krokach, podczas nawiązywania połączenia z klastrów.</span><span class="sxs-lookup"><span data-stu-id="c4380-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="c4380-144">Użyj notebooki</span><span class="sxs-lookup"><span data-stu-id="c4380-144">Use the notebooks</span></span>

<span data-ttu-id="c4380-145">Kod, na przykład opisanych w niniejszym dokumencie jest dostępny na [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="c4380-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="c4380-146">Postępuj zgodnie z instrukcjami `README.md` plik, aby ukończyć w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c4380-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="c4380-147">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="c4380-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c4380-148">Ponieważ kroki opisane w tym dokumencie utworzyć obu klastrów w tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c4380-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="c4380-149">Usuwanie grupy usuwa wszystkie zasoby utworzone przez tego dokumentu, Azure Virtual Network i konto magazynu używane przez klaster.</span><span class="sxs-lookup"><span data-stu-id="c4380-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4380-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4380-150">Next steps</span></span>

<span data-ttu-id="c4380-151">W tym przykładzie przedstawiono sposób użycia platformy Spark do odczytu i zapisu do Kafka.</span><span class="sxs-lookup"><span data-stu-id="c4380-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="c4380-152">Aby dowiedzieć się, inne metody pracy z Kafka, użyj następujących łączy:</span><span class="sxs-lookup"><span data-stu-id="c4380-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="c4380-153">Wprowadzenie do Apache Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4380-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="c4380-154">Tworzenie repliki platformy Kafka w usłudze HDInsight przy użyciu narzędzia MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="c4380-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="c4380-155">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4380-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

