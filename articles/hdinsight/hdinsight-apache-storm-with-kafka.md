---
title: "aaaUse Kafka Apache z systemu Storm w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Apache Kafka jest instalowany z systemu Apache Storm w usłudze HDInsight. Dowiedz się, jak toowrite tooKafka, a następnie odczytu z niego, przy użyciu hello KafkaBolt i KafkaSpout składniki dostarczane z systemu Storm. Też dowiedzieć się, jak toouse hello toodefine framework strumienia i przesyłania topologii Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="b0a95-105">Apache Kafka (wersja zapoznawcza) za pomocą Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0a95-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="b0a95-106">Dowiedz się, jak toouse tooread Apache Storm z i tooApache Kafka zapisu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="b0a95-107">Również w przykładzie pokazano, jak dane toosave z toohello topologii Storm systemu plików HDFS zgodnego pliku system używany przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0a95-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a95-108">kroki Hello w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Storm w usłudze HDInsight i Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0a95-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="b0a95-109">Tych klastrów są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu hello toodirectly klastra Storm komunikować się z hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="b0a95-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="b0a95-110">Po zakończeniu kroków hello w tym dokumencie, pamiętaj toodelete hello klastrów tooavoid nadmiarowe opłat.</span><span class="sxs-lookup"><span data-stu-id="b0a95-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="b0a95-111">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="b0a95-111">Get hello code</span></span>

<span data-ttu-id="b0a95-112">Kod Hello na przykład hello używane w tym dokumencie jest dostępny w [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="b0a95-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="b0a95-113">toocompile tego projektu należy hello następującej konfiguracji dla swojego środowiska programowania:</span><span class="sxs-lookup"><span data-stu-id="b0a95-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="b0a95-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b0a95-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="b0a95-115">HDInsight w wersji 3.5 lub nowszej wymagają Java 8.</span><span class="sxs-lookup"><span data-stu-id="b0a95-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="b0a95-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="b0a95-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="b0a95-117">Klient SSH (należy hello `ssh` i `scp` poleceń) — Aby uzyskać informacje, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b0a95-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="b0a95-118">Edytor tekstu lub IDE.</span><span class="sxs-lookup"><span data-stu-id="b0a95-118">A text editor or IDE.</span></span>

<span data-ttu-id="b0a95-119">Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalowania Java i hello JDK na deweloperskiej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="b0a95-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="b0a95-120">Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="b0a95-121">`JAVA_HOME`— powinna wskazywać katalog toohello hello JDK zainstalowanym.</span><span class="sxs-lookup"><span data-stu-id="b0a95-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="b0a95-122">`PATH`— powinna zawierać hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="b0a95-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="b0a95-123">`JAVA_HOME`(lub równoważne ścieżki hello).</span><span class="sxs-lookup"><span data-stu-id="b0a95-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b0a95-124">`JAVA_HOME\bin`(lub równoważne ścieżki hello).</span><span class="sxs-lookup"><span data-stu-id="b0a95-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b0a95-125">Hello katalog, w którym zainstalowano Maven.</span><span class="sxs-lookup"><span data-stu-id="b0a95-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="b0a95-126">Tworzenie klastrów hello</span><span class="sxs-lookup"><span data-stu-id="b0a95-126">Create hello clusters</span></span>

<span data-ttu-id="b0a95-127">Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka brokerzy za pośrednictwem hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="b0a95-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="b0a95-128">Wszystko, co rozmów, muszą mieć tooKafka hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="b0a95-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="b0a95-129">W tym przykładzie zarówno hello Kafka, jak i klastry Storm znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a95-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="b0a95-130">Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:</span><span class="sxs-lookup"><span data-stu-id="b0a95-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram klastrów Storm i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="b0a95-132">Inne usługi w klastrze hello, takich jak SSH i Ambari są dostępne za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="b0a95-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="b0a95-133">Aby uzyskać więcej informacji na powitania publicznego portów dostępnych z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="b0a95-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="b0a95-134">Podczas tworzenia sieci wirtualnej platformy Azure, Kafka, i klastrów Storm ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0a95-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="b0a95-135">Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure, Kafka, i klastrów Storm tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a95-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="b0a95-136">Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a95-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="b0a95-137">Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="b0a95-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="b0a95-138">Tworzy hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="b0a95-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="b0a95-139">Grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b0a95-139">Azure resource group</span></span>
    * <span data-ttu-id="b0a95-140">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="b0a95-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="b0a95-141">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b0a95-141">Azure Storage account</span></span>
    * <span data-ttu-id="b0a95-142">Kafka w usłudze HDInsight w wersji 3,6 (trzech węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="b0a95-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="b0a95-143">STORM w usłudze HDInsight w wersji 3,6 (trzech węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="b0a95-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="b0a95-144">dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="b0a95-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="b0a95-145">Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="b0a95-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="b0a95-146">Użyj hello następujące wskazówki toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="b0a95-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="b0a95-148">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="b0a95-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="b0a95-149">Ta grupa zawiera hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0a95-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="b0a95-150">**Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.</span><span class="sxs-lookup"><span data-stu-id="b0a95-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="b0a95-151">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello w przypadku klastrów Storm i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="b0a95-152">Na przykład wprowadzenie **hdi** jest tworzony klaster Storm o nazwie **storm hdi** i Kafka klastra o nazwie **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="b0a95-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="b0a95-153">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello w przypadku klastrów Storm i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="b0a95-154">**Hasło logowania klastra**: hello hasła użytkownika administratora w przypadku klastrów Storm i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="b0a95-155">**Nazwa użytkownika SSH**: hello toocreate użytkownika SSH w przypadku klastrów Storm i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="b0a95-156">**Hasło SSH**: hello hasło użytkownika SSH hello w przypadku klastrów Storm i Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="b0a95-157">Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="b0a95-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="b0a95-158">Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="b0a95-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="b0a95-159">Trwa około 20 minut toocreate hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="b0a95-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="b0a95-160">Po utworzeniu zasobów hello hello bloku grupy zasobów hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="b0a95-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="b0a95-162">Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ storm** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="b0a95-163">Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="b0a95-164">Znajomość hello kodu</span><span class="sxs-lookup"><span data-stu-id="b0a95-164">Understanding hello code</span></span>

<span data-ttu-id="b0a95-165">Ten projekt zawiera dwie topologie:</span><span class="sxs-lookup"><span data-stu-id="b0a95-165">This project contains two topologies:</span></span>

* <span data-ttu-id="b0a95-166">**KafkaWriter**: zdefiniowane przez hello **writer.yaml** pliku, ta topologia zapisuje tooKafka losowe zdań przy użyciu hello KafkaBolt dostarczane z systemu Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="b0a95-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="b0a95-167">Ta topologia używa niestandardowego **SentenceSpout** składnika toogenerate losowe zdań.</span><span class="sxs-lookup"><span data-stu-id="b0a95-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="b0a95-168">**KafkaReader**: zdefiniowane przez hello **reader.yaml** pliku, ta topologia odczytuje dane z Kafka przy użyciu hello KafkaSpout dostarczane z systemu Apache Storm, a następnie dzienniki hello toostdout danych.</span><span class="sxs-lookup"><span data-stu-id="b0a95-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="b0a95-169">Ta topologia używa hello Storm HdfsBolt toowrite danych toodefault magazynu dla klastra Storm hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="b0a95-170">Strumień</span><span class="sxs-lookup"><span data-stu-id="b0a95-170">Flux</span></span>

<span data-ttu-id="b0a95-171">topologie Hello są definiowane przy użyciu [strumień](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b0a95-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="b0a95-172">Strumień została wprowadzona w systemie Storm 0.10.x i pozwala konfiguracji topologii hello tooseparate z hello kodu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="b0a95-173">Dla topologie, wykorzystujące framework strumień hello topologii hello jest zdefiniowany w pliku yaml programu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="b0a95-174">może to być zawarte w ramach topologii hello Hello yaml programu plik.</span><span class="sxs-lookup"><span data-stu-id="b0a95-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="b0a95-175">Można także użyć podczas przesyłania topologii hello autonomiczny plik.</span><span class="sxs-lookup"><span data-stu-id="b0a95-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="b0a95-176">Strumień obsługuje również podstawienie zmiennej w czasie wykonywania, który jest używany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b0a95-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="b0a95-177">Witaj następujące parametry są ustawione w czasie wykonywania dla tych topologii:</span><span class="sxs-lookup"><span data-stu-id="b0a95-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="b0a95-178">`${kafka.topic}`: Nazwa hello hello temat Kafka, który topologie hello odczytu/zapisu do.</span><span class="sxs-lookup"><span data-stu-id="b0a95-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="b0a95-179">`${kafka.broker.hosts}`: hello hostem tego hello Kafka przekazuje informacje dotyczące uruchamiania na.</span><span class="sxs-lookup"><span data-stu-id="b0a95-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="b0a95-180">informacje brokera Hello jest używany przez hello KafkaBolt podczas zapisywania tooKafka.</span><span class="sxs-lookup"><span data-stu-id="b0a95-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="b0a95-181">`${kafka.zookeeper.hosts}`: hello hostów, które dozorcy działa na w hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="b0a95-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="b0a95-182">Aby uzyskać więcej informacji dotyczących topologii strumienia, zobacz [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b0a95-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="b0a95-183">Pobierz i skompiluj projekt hello</span><span class="sxs-lookup"><span data-stu-id="b0a95-183">Download and compile hello project</span></span>

1. <span data-ttu-id="b0a95-184">Na środowiska deweloperskiego pobrać projekt hello z [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), Otwórz wiersza polecenia i zmień lokalizację toohello katalogów został pobrany hello projektu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="b0a95-185">Z hello **hdinsight-storm-java-kafka** katalogu, użyj hello następujące polecenia toocompile hello projektu i utworzenie pakietu wdrażania:</span><span class="sxs-lookup"><span data-stu-id="b0a95-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="b0a95-186">proces pakietu Hello tworzy plik o nazwie `KafkaTopology-1.0-SNAPSHOT.jar` w hello `target` katalogu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="b0a95-187">Użyj następującego polecenia toocopy hello pakietu tooyour Storm w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="b0a95-188">Zastąp **USERNAME** z nazwą użytkownika SSH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="b0a95-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="b0a95-189">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello są używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="b0a95-190">Po wyświetleniu monitu wprowadź hasło hello, które zostały użyte podczas tworzenia klastrów hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="b0a95-191">Konfigurowanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="b0a95-191">Configure hello topology</span></span>

1. <span data-ttu-id="b0a95-192">Użyj jednej z hello następujące metody toodiscover hello Kafka brokera hostów:</span><span class="sxs-lookup"><span data-stu-id="b0a95-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b0a95-193">Witaj Bash przykładzie założono, że `$CLUSTERNAME` zawiera nazwę hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0a95-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="b0a95-194">Założono również, że [jq](https://stedolan.github.io/jq/) jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="b0a95-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="b0a95-195">Po wyświetleniu monitu wprowadź hasło hello hello klastra logowania konta.</span><span class="sxs-lookup"><span data-stu-id="b0a95-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="b0a95-196">zwrócona wartość Hello jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b0a95-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="b0a95-197">Może być więcej niż dwa hosty broker dla klastra, nie trzeba tooprovide pełną listę wszystkich tooclients hostów.</span><span class="sxs-lookup"><span data-stu-id="b0a95-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="b0a95-198">Jedno lub dwa jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="b0a95-198">One or two is enough.</span></span>

2. <span data-ttu-id="b0a95-199">Użyj jednej z hello następujące metody toodiscover hello dozorcy Kafka hostów:</span><span class="sxs-lookup"><span data-stu-id="b0a95-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b0a95-200">Witaj Bash przykładzie założono, że `$CLUSTERNAME` zawiera nazwę hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0a95-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="b0a95-201">Założono również, że [jq](https://stedolan.github.io/jq/) jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="b0a95-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="b0a95-202">Po wyświetleniu monitu wprowadź hasło hello hello klastra logowania konta.</span><span class="sxs-lookup"><span data-stu-id="b0a95-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="b0a95-203">zwrócona wartość Hello jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b0a95-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="b0a95-204">Gdy istnieje więcej niż dwa węzły dozorcy, nie trzeba tooprovide pełną listę wszystkich tooclients hostów.</span><span class="sxs-lookup"><span data-stu-id="b0a95-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="b0a95-205">Jedno lub dwa jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="b0a95-205">One or two is enough.</span></span>

    <span data-ttu-id="b0a95-206">Zapisz tę wartość, ponieważ jest używana później.</span><span class="sxs-lookup"><span data-stu-id="b0a95-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="b0a95-207">Edytuj hello `dev.properties` pliku w katalogu głównym hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="b0a95-208">Dodaj hello brokera i dozorcy hostów informacji toohello zgodnych wierszy w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="b0a95-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="b0a95-209">Witaj poniższy przykład jest konfigurowana przy użyciu hello przykładowe wartości z poprzednich kroków hello:</span><span class="sxs-lookup"><span data-stu-id="b0a95-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="b0a95-210">Zapisz hello `dev.properties` pliku, a następnie przy użyciu hello następujące polecenia tooupload go klaster Storm toohello:</span><span class="sxs-lookup"><span data-stu-id="b0a95-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="b0a95-211">Zastąp **USERNAME** z nazwą użytkownika SSH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="b0a95-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="b0a95-212">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello są używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="b0a95-213">Moduł zapisujący hello Start</span><span class="sxs-lookup"><span data-stu-id="b0a95-213">Start hello writer</span></span>

1. <span data-ttu-id="b0a95-214">Użyj powitania po klaster Storm toohello tooconnect przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="b0a95-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="b0a95-215">Zastąp **USERNAME** z nazwą użytkownika SSH hello używany podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="b0a95-216">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello używany podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="b0a95-217">Po wyświetleniu monitu wprowadź hasło hello, które zostały użyte podczas tworzenia klastrów hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="b0a95-218">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b0a95-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b0a95-219">Hello połączenia SSH używając hello następujące polecenia toocreate hello tematu Kafka używane przez hello topologii:</span><span class="sxs-lookup"><span data-stu-id="b0a95-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="b0a95-220">Zastąp `$KAFKAZKHOSTS` z hello dozorcy hosta pobrane w poprzedniej sekcji hello informacje.</span><span class="sxs-lookup"><span data-stu-id="b0a95-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="b0a95-221">Klaster Storm hello SSH połączenia toohello używając hello następujące polecenia toostart hello zapisywania topologii:</span><span class="sxs-lookup"><span data-stu-id="b0a95-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="b0a95-222">Parametry Hello używane w tym poleceniu są:</span><span class="sxs-lookup"><span data-stu-id="b0a95-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="b0a95-223">`org.apache.storm.flux.Flux`: Za pomocą strumienia tooconfigure, a następnie uruchom tej topologii.</span><span class="sxs-lookup"><span data-stu-id="b0a95-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="b0a95-224">`--remote`: Prześlij hello tooNimbus topologii.</span><span class="sxs-lookup"><span data-stu-id="b0a95-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="b0a95-225">Witaj topologia jest rozmieszczona na powitania węzłów procesu roboczego w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="b0a95-226">`-R /writer.yaml`: Użycie hello `writer.yaml` pliku tooconfigure hello topologii.</span><span class="sxs-lookup"><span data-stu-id="b0a95-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="b0a95-227">`-R`Wskazuje, że ten zasób jest uwzględniona w pliku jar hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="b0a95-228">Znajduje się w katalogu głównym hello hello jar, więc `/writer.yaml` jest hello tooit ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b0a95-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="b0a95-229">`--filter`: Wypełnić wpisów w hello `writer.yaml` topologii przy użyciu wartości w hello `dev.properties` pliku.</span><span class="sxs-lookup"><span data-stu-id="b0a95-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="b0a95-230">Na przykład Witaj wartość hello `kafka.topic` wpis w pliku hello jest używany tooreplace hello `${kafka.topic}` wejścia w definicji topologii hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="b0a95-231">Po rozpoczęciu topologii hello, użyj następującego polecenia tooverify, że jest zapisywania danych toohello Kafka tematu hello:</span><span class="sxs-lookup"><span data-stu-id="b0a95-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="b0a95-232">Zastąp `$KAFKAZKHOSTS` z hello dozorcy hosta pobrane w poprzedniej sekcji hello informacje.</span><span class="sxs-lookup"><span data-stu-id="b0a95-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="b0a95-233">To polecenie używa skryptu dostarczone z Kafka toomonitor hello tematu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="b0a95-234">Po chwili należy uruchomić, zwracanie losowe zdania, które zostały zapisane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="b0a95-235">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="b0a95-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="b0a95-236">Użyj klawiszy Ctrl + c toostop hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="b0a95-237">Czytnik hello Start</span><span class="sxs-lookup"><span data-stu-id="b0a95-237">Start hello reader</span></span>

1. <span data-ttu-id="b0a95-238">Klaster Storm hello SSH sesji toohello używając hello następujące polecenia toostart hello czytnika topologii:</span><span class="sxs-lookup"><span data-stu-id="b0a95-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="b0a95-239">Po uruchomieniu topologii hello Otwórz hello interfejsu użytkownika platformy Storm.</span><span class="sxs-lookup"><span data-stu-id="b0a95-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="b0a95-240">Interfejs użytkownika sieci web znajduje się pod adresem https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="b0a95-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="b0a95-241">Zastąp __nazwę BAZOWĄ__ o nazwie podstawowej hello używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="b0a95-242">Po wyświetleniu monitu użyj nazwy logowania administratora hello (domyślnie `admin`) i hasło używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b0a95-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="b0a95-243">Zostaną wyświetlone podobne toohello o następujące obraz strony sieci web:</span><span class="sxs-lookup"><span data-stu-id="b0a95-243">You see a web page similar toohello following image:</span></span>

    ![STORM interfejsu użytkownika](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="b0a95-245">Hello interfejsu użytkownika platformy Storm, zaznacz hello __czytnika kafka__ łącze w hello __podsumowanie topologii__ sekcji toodisplay informacji na temat hello __kafka czytnika__ topologii.</span><span class="sxs-lookup"><span data-stu-id="b0a95-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Topologia sekcji podsumowania hello interfejsu użytkownika sieci web Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="b0a95-247">toodisplay informacji na temat wystąpień hello hello bolt rejestratora składników, wybierz hello __bolt rejestratora__ łącze w hello __elementów Bolt (czas wszystkich)__ sekcji.</span><span class="sxs-lookup"><span data-stu-id="b0a95-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Rejestrator bolt link w sekcji elementów bolt hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="b0a95-249">W hello __modułów__ wybierz łącze w hello __portu__ kolumny toodisplay rejestrowanie informacji o wystąpieniu hello składnika.</span><span class="sxs-lookup"><span data-stu-id="b0a95-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Łącze modułów](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="b0a95-251">Dziennik Hello zawiera dziennik hello dane odczytane ze hello Kafka tematu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="b0a95-252">Witaj informacji w dzienniku hello jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b0a95-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="b0a95-253">Zatrzymywanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="b0a95-253">Stop hello topologies</span></span>

<span data-ttu-id="b0a95-254">Z klastra Storm toohello sesji SSH należy użyć powitania po topologii Storm hello toostop polecenia:</span><span class="sxs-lookup"><span data-stu-id="b0a95-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="b0a95-255">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="b0a95-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b0a95-256">Ponieważ hello kroków w tym dokumencie Tworzenie zarówno klastrów w hello tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a95-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="b0a95-257">Usunięcie grupy zasobów hello usuwa wszystkie zasoby utworzone przez wykonanie tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b0a95-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0a95-258">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0a95-258">Next steps</span></span>

<span data-ttu-id="b0a95-259">Aby uzyskać więcej przykładowe topologie, które mogą być używane z systemu Storm w usłudze HDInsight, zobacz [topologii Storm przykład i składniki](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b0a95-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="b0a95-260">Aby uzyskać informacje dotyczące wdrażania i monitorowania topologii na HDInsight opartych na systemie Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="b0a95-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>