---
title: "aaaApache Spark przesyłania strumieniowego z Kafka - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Spark Apache Spark toostream danych do lub wychodzący Kafka Apache przy użyciu DStreams. W tym przykładzie można przesyłać strumieniowo dane za pomocą notesu Jupyter z platformy Spark w usłudze HDInsight."
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
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="9f414-105">Apache Spark przesyłania strumieniowego (DStream) przykład: Kafka (wersja zapoznawcza) w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f414-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="9f414-106">Dowiedz się, jak toouse Spark Apache Spark toostream danych do lub wychodzący Kafka Apache na HDInsight przy użyciu DStreams.</span><span class="sxs-lookup"><span data-stu-id="9f414-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="9f414-107">W tym przykładzie użyto notesu Jupyter w klastrze Spark hello.</span><span class="sxs-lookup"><span data-stu-id="9f414-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="9f414-108">kroki Hello w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Spark w usłudze HDInsight i Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f414-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="9f414-109">Tych klastrów są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu hello toodirectly klastra Spark komunikować się z hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="9f414-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="9f414-110">Po zakończeniu kroków hello w tym dokumencie, pamiętaj toodelete hello klastrów tooavoid nadmiarowe opłat.</span><span class="sxs-lookup"><span data-stu-id="9f414-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="9f414-111">Tworzenie klastrów hello</span><span class="sxs-lookup"><span data-stu-id="9f414-111">Create hello clusters</span></span>

<span data-ttu-id="9f414-112">Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka brokerzy za pośrednictwem hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="9f414-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="9f414-113">Wszystko, co rozmów, muszą mieć tooKafka hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="9f414-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="9f414-114">W tym przykładzie zarówno hello Kafka, jak i klastry Spark znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9f414-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="9f414-115">Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:</span><span class="sxs-lookup"><span data-stu-id="9f414-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram klastry Spark i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="9f414-117">Chociaż Kafka sam jest ograniczona toocommunication w ramach sieci wirtualnej hello, inne usługi w klastrze hello takich jak SSH i Ambari są dostępne za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="9f414-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="9f414-118">Aby uzyskać więcej informacji na powitania publicznego portów dostępnych z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="9f414-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="9f414-119">Chociaż można utworzyć sieci wirtualnej platformy Azure, Kafka i Spark klastry ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9f414-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="9f414-120">Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure, Kafka, i Spark klastrów tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9f414-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="9f414-121">Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9f414-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="9f414-122">Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="9f414-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9f414-123">dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="9f414-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="9f414-124">Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="9f414-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="9f414-125">Ten szablon umożliwia tworzenie klastra usługi HDInsight 3,6 Kafka i Spark.</span><span class="sxs-lookup"><span data-stu-id="9f414-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="9f414-126">Witaj Użyj następujących informacji toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="9f414-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="9f414-128">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="9f414-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="9f414-129">Ta grupa zawiera hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f414-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="9f414-130">**Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.</span><span class="sxs-lookup"><span data-stu-id="9f414-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="9f414-131">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="9f414-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="9f414-132">Na przykład wprowadzenie **hdi** tworzy Spark klastra o nazwie spark hdi__ i Kafka klastra o nazwie **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="9f414-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="9f414-133">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="9f414-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="9f414-134">**Hasło logowania klastra**: hello hasła użytkownika administratora klastrów platformy Spark i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="9f414-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="9f414-135">**Nazwa użytkownika SSH**: hello toocreate użytkownika SSH hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="9f414-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="9f414-136">**Hasło SSH**: hello hasło użytkownika SSH hello hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="9f414-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="9f414-137">Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="9f414-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="9f414-138">Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="9f414-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="9f414-139">Trwa około 20 minut toocreate hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="9f414-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="9f414-140">Po utworzeniu hello zasoby zostaną przekierowane tooa bloku hello grupę zasobów, która zawiera hello klastrów i pulpitu nawigacyjnego sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f414-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="9f414-142">Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ spark** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="9f414-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="9f414-143">Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.</span><span class="sxs-lookup"><span data-stu-id="9f414-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="9f414-144">Użyj notesów hello</span><span class="sxs-lookup"><span data-stu-id="9f414-144">Use hello notebooks</span></span>

<span data-ttu-id="9f414-145">Kod Hello na przykład hello opisanych w niniejszym dokumencie jest dostępny w [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="9f414-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="9f414-146">Wykonaj kroki hello hello `README.md` pliku toocomplete w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9f414-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="9f414-147">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="9f414-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="9f414-148">Ponieważ hello kroków w tym dokumencie Tworzenie zarówno klastrów w hello tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9f414-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="9f414-149">Usuwanie grupy hello usuwa wszystkie zasoby utworzone, postępując w tym dokumencie, hello Azure Virtual Network i konto magazynu używane przez hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="9f414-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f414-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9f414-150">Next steps</span></span>

<span data-ttu-id="9f414-151">W tym przykładzie przedstawiono sposób toouse Spark tooread i zapisać tooKafka.</span><span class="sxs-lookup"><span data-stu-id="9f414-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="9f414-152">Z Kafka, należy użyć następującego łącza toodiscover hello toowork inne sposoby:</span><span class="sxs-lookup"><span data-stu-id="9f414-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="9f414-153">Wprowadzenie do Apache Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f414-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="9f414-154">Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f414-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="9f414-155">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f414-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

