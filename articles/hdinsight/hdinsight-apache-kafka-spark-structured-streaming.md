---
title: "aaaApache Spark strukturalnych przesyłania strumieniowego z Kafka - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Apache Spark dane przesyłane strumieniowo (DStream) tooget do lub wychodzący Apache Kafka. W tym przykładzie można przesyłać strumieniowo dane za pomocą notesu Jupyter z platformy Spark w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="89cc2-104">Użyj Spark strukturalnych przesyłania strumieniowego z Kafka (wersja zapoznawcza) w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="89cc2-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="89cc2-105">Dowiedz się, jak toouse strukturalnych przesyłania strumieniowego Spark tooread danych z Kafka Apache na Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="89cc2-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="89cc2-106">Struktura przesyłania strumieniowego Spark jest aparatem przetwarzania strumienia oparty na Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="89cc2-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="89cc2-107">Umożliwia się, że możesz obliczenia przesyłania strumieniowego tooexpress hello taki sam jak partii obliczeń w danych statycznych.</span><span class="sxs-lookup"><span data-stu-id="89cc2-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="89cc2-108">Aby uzyskać więcej informacji o strukturze przesyłania strumieniowego, zobacz hello [strukturalnych przesyłania strumieniowego przewodnik programowania w języku [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) w serwisie Apache.org.</span><span class="sxs-lookup"><span data-stu-id="89cc2-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89cc2-109">W tym przykładzie użyto Spark 2.1 w usłudze HDInsight 3,6.</span><span class="sxs-lookup"><span data-stu-id="89cc2-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="89cc2-110">Strukturalne Streaming jest uznawany za __alfa__ 2.1 Spark.</span><span class="sxs-lookup"><span data-stu-id="89cc2-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="89cc2-111">kroki Hello w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Spark w usłudze HDInsight i Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="89cc2-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="89cc2-112">Tych klastrów są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu hello toodirectly klastra Spark komunikować się z hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="89cc2-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="89cc2-113">Po zakończeniu kroków hello w tym dokumencie, pamiętaj toodelete hello klastrów tooavoid nadmiarowe opłat.</span><span class="sxs-lookup"><span data-stu-id="89cc2-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="89cc2-114">Tworzenie klastrów hello</span><span class="sxs-lookup"><span data-stu-id="89cc2-114">Create hello clusters</span></span>

<span data-ttu-id="89cc2-115">Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka brokerzy za pośrednictwem hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="89cc2-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="89cc2-116">Wszystko, co rozmów, muszą mieć tooKafka hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="89cc2-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="89cc2-117">W tym przykładzie zarówno hello Kafka, jak i klastry Spark znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89cc2-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="89cc2-118">Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:</span><span class="sxs-lookup"><span data-stu-id="89cc2-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram klastry Spark i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="89cc2-120">Witaj Kafka usługi jest ograniczone toocommunication w ramach sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="89cc2-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="89cc2-121">Inne usługi w klastrze hello, takich jak SSH i Ambari, są dostępne za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="89cc2-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="89cc2-122">Aby uzyskać więcej informacji na powitania publicznego portów dostępnych z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="89cc2-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="89cc2-123">Chociaż można utworzyć sieci wirtualnej platformy Azure, Kafka i Spark klastry ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="89cc2-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="89cc2-124">Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure, Kafka, i Spark klastrów tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89cc2-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="89cc2-125">Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="89cc2-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="89cc2-126">Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="89cc2-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="89cc2-127">Ten szablon tworzy hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="89cc2-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="89cc2-128">Kafka w klastrze HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="89cc2-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="89cc2-129">Platforma Spark w klastrze HDInsight 3,6.</span><span class="sxs-lookup"><span data-stu-id="89cc2-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="89cc2-130">Sieci wirtualnej platformy Azure, zawierającą hello klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="89cc2-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="89cc2-131">Witaj strukturalnych notesu przesyłania strumieniowego w tym przykładzie wymaga platforma Spark w usłudze HDInsight 3,6.</span><span class="sxs-lookup"><span data-stu-id="89cc2-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="89cc2-132">Jeśli używasz starszej wersji platformy Spark w usłudze HDInsight, wystąpią błędy, korzystając z hello notesu.</span><span class="sxs-lookup"><span data-stu-id="89cc2-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="89cc2-133">Witaj Użyj następujących informacji toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="89cc2-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="89cc2-135">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="89cc2-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="89cc2-136">Ta grupa zawiera hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="89cc2-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="89cc2-137">**Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.</span><span class="sxs-lookup"><span data-stu-id="89cc2-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="89cc2-138">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="89cc2-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="89cc2-139">Na przykład wprowadzenie **hdi** tworzy Spark klastra o nazwie spark hdi__ i Kafka klastra o nazwie **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="89cc2-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="89cc2-140">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="89cc2-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="89cc2-141">**Hasło logowania klastra**: hello hasła użytkownika administratora klastrów platformy Spark i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="89cc2-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="89cc2-142">**Nazwa użytkownika SSH**: hello toocreate użytkownika SSH hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="89cc2-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="89cc2-143">**Hasło SSH**: hello hasło użytkownika SSH hello hello Spark i Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="89cc2-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="89cc2-144">Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="89cc2-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="89cc2-145">Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="89cc2-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="89cc2-146">Trwa około 20 minut toocreate hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="89cc2-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="89cc2-147">Po utworzeniu zasobów hello jesteś bloku grupy zasobów toohello przekierowane.</span><span class="sxs-lookup"><span data-stu-id="89cc2-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="89cc2-149">Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ spark** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="89cc2-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="89cc2-150">Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.</span><span class="sxs-lookup"><span data-stu-id="89cc2-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="89cc2-151">Pobierz hello Kafka brokerzy</span><span class="sxs-lookup"><span data-stu-id="89cc2-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="89cc2-152">Witaj kodu w tym przykładzie łączy toohello Kafka broker hosty w hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="89cc2-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="89cc2-153">toofind hello Kafka brokera hostów, użyj hello poniższy przykład programu PowerShell lub Bash:</span><span class="sxs-lookup"><span data-stu-id="89cc2-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="89cc2-154">W tym przykładzie oczekuje `$PASSWORD` toocontain hello hasło do logowania do klastra hello, i `$CLUSTERNAME` toocontain nazwę hello hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="89cc2-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="89cc2-155">W tym przykładzie użyto hello [jq](https://stedolan.github.io/jq/) narzędzie tooparse danych poza hello dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="89cc2-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="89cc2-156">Witaj danych wyjściowych jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="89cc2-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="89cc2-157">Zapisz te informacje, ponieważ jest używany w hello następujące części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="89cc2-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="89cc2-158">Pobierz notesów hello</span><span class="sxs-lookup"><span data-stu-id="89cc2-158">Get hello notebooks</span></span>

<span data-ttu-id="89cc2-159">Kod Hello na przykład hello opisanych w niniejszym dokumencie jest dostępny w [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="89cc2-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="89cc2-160">Przekaż notesów hello</span><span class="sxs-lookup"><span data-stu-id="89cc2-160">Upload hello notebooks</span></span>

<span data-ttu-id="89cc2-161">Użyj poniższych kroków tooupload hello notesów z tooyour projektu hello Spark w klastrze usługi HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="89cc2-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="89cc2-162">W przeglądarce sieci web Połącz toohello notesu Jupyter w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="89cc2-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="89cc2-163">W hello następującego adresu URL, Zastąp `CLUSTERNAME` o nazwie hello Kafka klastra:</span><span class="sxs-lookup"><span data-stu-id="89cc2-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="89cc2-164">Po wyświetleniu monitu wprowadź hello logowania do klastra (admin) i hasło użyte podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="89cc2-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="89cc2-165">Hello górny po prawej stronie powitania strony, użyj funkcji hello __przekazać__ hello tooupload przycisk __strumienia-Tweetów-To_Kafka.ipynb__ klastra toohello plików.</span><span class="sxs-lookup"><span data-stu-id="89cc2-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="89cc2-166">Wybierz __Otwórz__ toostart hello przekazywania.</span><span class="sxs-lookup"><span data-stu-id="89cc2-166">Select __Open__ toostart hello upload.</span></span>

    ![Użyj hello przekazywania przycisk tooselect i przekazać Notes](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Wybierz plik KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="89cc2-169">Znajdź hello __strumienia-Tweetów-To_Kafka.ipynb__ wpis na liście hello notesów i wybierz __przekazać__ przycisk obok siebie.</span><span class="sxs-lookup"><span data-stu-id="89cc2-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Przekazywanie hello użyj przycisku obok hello KafkaStreaming.ipynb wpis tooupload go toohello notesu serwera](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="89cc2-171">Powtórz kroki od 1 do 3 tooload hello __Spark-strukturę-przesyłania strumieniowego-od-Kafka.ipynb__ notesu.</span><span class="sxs-lookup"><span data-stu-id="89cc2-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="89cc2-172">Ładowanie tweetów do Kafka</span><span class="sxs-lookup"><span data-stu-id="89cc2-172">Load tweets into Kafka</span></span>

<span data-ttu-id="89cc2-173">Po hello pliki zostały przekazane, wybierz hello __strumienia-Tweetów-To_Kafka.ipynb__ wpis tooopen hello notesu.</span><span class="sxs-lookup"><span data-stu-id="89cc2-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="89cc2-174">Wykonaj kroki hello hello notesu tooload tweetów do Kafka.</span><span class="sxs-lookup"><span data-stu-id="89cc2-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="89cc2-175">Przy użyciu strukturalnych przesyłania strumieniowego Spark tweetów procesu</span><span class="sxs-lookup"><span data-stu-id="89cc2-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="89cc2-176">Wybierz hello z hello strony głównej notesu Jupyter __Spark-strukturę-przesyłania strumieniowego-od-Kafka.ipynb__ wpisu.</span><span class="sxs-lookup"><span data-stu-id="89cc2-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="89cc2-177">Wykonaj kroki hello hello notesu tooload tweetów z Kafka przy użyciu strukturalnych przesyłania strumieniowego Spark.</span><span class="sxs-lookup"><span data-stu-id="89cc2-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89cc2-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89cc2-178">Next steps</span></span>

<span data-ttu-id="89cc2-179">Teraz, kiedy znasz już toouse Spark strukturalnych przesyłania strumieniowego, zobacz temat powitania po więcej informacji na temat pracy z platformy Spark i Kafka toolearn dokumentów:</span><span class="sxs-lookup"><span data-stu-id="89cc2-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="89cc2-180">[Jak toouse Spark przesyłania strumieniowego (DStream) z Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="89cc2-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="89cc2-181">Rozpoczynać notesu Jupyter i Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="89cc2-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)