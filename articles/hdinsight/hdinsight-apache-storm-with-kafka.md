---
title: "Używających Apache Kafka Storm w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Apache Kafka jest instalowany z systemu Apache Storm w usłudze HDInsight. Dowiedz się, jak zapisać Kafka, a następnie przeczytaj z niego, przy użyciu składników KafkaBolt i KafkaSpout, ile z systemu Storm. Również Dowiedz się, jak za pomocą architektury strumień do definiowania i przesyłania topologii Storm."
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
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="36a29-105">Apache Kafka (wersja zapoznawcza) za pomocą Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a29-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="36a29-106">Dowiedz się, jak używać systemu Apache Storm do odczytu i zapisu Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="36a29-107">Również w tym przykładzie pokazano, jak zapisać dane od topologii Storm do systemu plików HDFS zgodnego używane przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a29-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="36a29-108">Kroki opisane w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Storm w usłudze HDInsight i Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a29-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="36a29-109">Te klastry są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu klaster Storm do bezpośredniego komunikowania się z Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="36a29-110">Po zakończeniu kroków w tym dokumencie, pamiętaj, aby usuwać te klastry, aby zapobiec zmianom nadmiarowe.</span><span class="sxs-lookup"><span data-stu-id="36a29-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="36a29-111">Uzyskiwanie kodu</span><span class="sxs-lookup"><span data-stu-id="36a29-111">Get the code</span></span>

<span data-ttu-id="36a29-112">Kod używany w przykładzie podanym w tym dokumencie jest dostępny na [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="36a29-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="36a29-113">Aby skompilować ten projekt, należy następującej konfiguracji dla swojego środowiska programowania:</span><span class="sxs-lookup"><span data-stu-id="36a29-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="36a29-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="36a29-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="36a29-115">HDInsight w wersji 3.5 lub nowszej wymagają Java 8.</span><span class="sxs-lookup"><span data-stu-id="36a29-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="36a29-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="36a29-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="36a29-117">Klient SSH (należy `ssh` i `scp` poleceń) — Aby uzyskać informacje, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="36a29-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="36a29-118">Edytor tekstu lub IDE.</span><span class="sxs-lookup"><span data-stu-id="36a29-118">A text editor or IDE.</span></span>

<span data-ttu-id="36a29-119">Po zainstalowaniu na deweloperskiej stacji roboczej Java i zestaw JDK, który można konfigurować następujące zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="36a29-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="36a29-120">Jednak należy sprawdzić, czy istnieją i że zawierają one poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="36a29-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="36a29-121">`JAVA_HOME`-powinny wskazywać na katalog, w którym jest zainstalowany zestaw JDK.</span><span class="sxs-lookup"><span data-stu-id="36a29-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="36a29-122">`PATH`— powinna zawierać następujących ścieżkach:</span><span class="sxs-lookup"><span data-stu-id="36a29-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="36a29-123">`JAVA_HOME`(lub równoważne ścieżki).</span><span class="sxs-lookup"><span data-stu-id="36a29-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="36a29-124">`JAVA_HOME\bin`(lub równoważne ścieżki).</span><span class="sxs-lookup"><span data-stu-id="36a29-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="36a29-125">Katalog, w którym zainstalowano Maven.</span><span class="sxs-lookup"><span data-stu-id="36a29-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="36a29-126">Tworzenie klastrów</span><span class="sxs-lookup"><span data-stu-id="36a29-126">Create the clusters</span></span>

<span data-ttu-id="36a29-127">Kafka Apache na HDInsight nie zapewnia dostępu do brokerzy Kafka za pośrednictwem publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="36a29-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="36a29-128">Wszystkie elementy, które komunikuje się Kafka musi być w tej samej sieci wirtualnej platformy Azure jako węzły w klastrze Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="36a29-129">W tym przykładzie zarówno Kafka, jak i Storm klastrach znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36a29-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="36a29-130">Na poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami:</span><span class="sxs-lookup"><span data-stu-id="36a29-130">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram klastrów Storm i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="36a29-132">Inne usługi w klastrze, takich jak SSH i Ambari są dostępne za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="36a29-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="36a29-133">Aby uzyskać więcej informacji na portach publicznego dostępne z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="36a29-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="36a29-134">Podczas tworzenia sieci wirtualnej platformy Azure, Kafka, i ręcznie klastrów Storm, łatwiej jest użyć szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36a29-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="36a29-135">Wykonaj następujące kroki, aby wdrożyć sieci wirtualnej platformy Azure, Kafka, a Storm klastrów do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36a29-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="36a29-136">Poniższy przycisk umożliwia logowanie do platformy Azure i otwórz szablon w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36a29-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="36a29-137">Szablon usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="36a29-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="36a29-138">Tworzy następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="36a29-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="36a29-139">Grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36a29-139">Azure resource group</span></span>
    * <span data-ttu-id="36a29-140">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="36a29-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="36a29-141">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="36a29-141">Azure Storage account</span></span>
    * <span data-ttu-id="36a29-142">Kafka w usłudze HDInsight w wersji 3,6 (trzech węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="36a29-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="36a29-143">STORM w usłudze HDInsight w wersji 3,6 (trzech węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="36a29-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="36a29-144">Aby zapewnić dostępność platformy Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzy węzły procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="36a29-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="36a29-145">Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="36a29-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="36a29-146">Użyj poniższych wskazówek, aby wypełnić wpisy na **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="36a29-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="36a29-148">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="36a29-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="36a29-149">Ta grupa zawiera klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a29-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="36a29-150">**Lokalizacja**: Wybierz lokalizację lokalizacji geograficznej blisko.</span><span class="sxs-lookup"><span data-stu-id="36a29-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="36a29-151">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa dla Storm i klastry Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="36a29-152">Na przykład wprowadzenie **hdi** jest tworzony klaster Storm o nazwie **storm hdi** i Kafka klastra o nazwie **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="36a29-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="36a29-153">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora w przypadku klastrów Storm i Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="36a29-154">**Hasło logowania klastra**: hasła użytkownika administratora w przypadku klastrów Storm i Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="36a29-155">**Nazwa użytkownika SSH**: użytkownika SSH do tworzenia klastrów Storm i Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="36a29-156">**Hasło SSH**: hasło dla użytkownika SSH w przypadku klastrów Storm i Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="36a29-157">Odczyt **warunków i postanowień**, a następnie wybierz **akceptuję warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="36a29-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="36a29-158">Ponadto sprawdź **Przypnij do pulpitu nawigacyjnego** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="36a29-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="36a29-159">Tworzenie klastrów trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="36a29-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="36a29-160">Po utworzeniu zasobów bloku grupy zasobów jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="36a29-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej i klastrów](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="36a29-162">Należy zauważyć, że nazwy klastrów usługi HDInsight są **nazwę BAZOWĄ storm** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest podana nazwa do szablonu.</span><span class="sxs-lookup"><span data-stu-id="36a29-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="36a29-163">Te nazwy można użyć w kolejnych krokach, podczas nawiązywania połączenia z klastrów.</span><span class="sxs-lookup"><span data-stu-id="36a29-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="36a29-164">Opis kodu</span><span class="sxs-lookup"><span data-stu-id="36a29-164">Understanding the code</span></span>

<span data-ttu-id="36a29-165">Ten projekt zawiera dwie topologie:</span><span class="sxs-lookup"><span data-stu-id="36a29-165">This project contains two topologies:</span></span>

* <span data-ttu-id="36a29-166">**KafkaWriter**: zdefiniowane przez **writer.yaml** pliku, ta topologia zapisuje losowe zdań Kafka przy użyciu KafkaBolt dostarczane z systemu Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="36a29-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="36a29-167">Ta topologia używa niestandardowego **SentenceSpout** składnik do generowania losowego zdań.</span><span class="sxs-lookup"><span data-stu-id="36a29-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="36a29-168">**KafkaReader**: zdefiniowane przez **reader.yaml** plik, ta topologia odczytuje dane z Kafka przy użyciu KafkaSpout dostarczane z systemu Apache Storm, a następnie rejestruje dane do stdout.</span><span class="sxs-lookup"><span data-stu-id="36a29-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="36a29-169">Ta topologia używa Storm HdfsBolt do zapisu danych do magazynu domyślnego dla klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="36a29-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="36a29-170">Strumień</span><span class="sxs-lookup"><span data-stu-id="36a29-170">Flux</span></span>

<span data-ttu-id="36a29-171">Topologie są definiowane przy użyciu [strumień](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="36a29-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="36a29-172">Strumień została wprowadzona w systemie Storm 0.10.x i umożliwia rozdzielenie konfiguracji topologii z kodu.</span><span class="sxs-lookup"><span data-stu-id="36a29-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="36a29-173">Dla topologie, wykorzystujące framework strumienia topologia jest zdefiniowany w pliku yaml programu.</span><span class="sxs-lookup"><span data-stu-id="36a29-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="36a29-174">Może to być plik yaml programu zawarte w ramach topologii.</span><span class="sxs-lookup"><span data-stu-id="36a29-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="36a29-175">Można także użyć podczas przesyłania topologii autonomiczny plik.</span><span class="sxs-lookup"><span data-stu-id="36a29-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="36a29-176">Strumień obsługuje również podstawienie zmiennej w czasie wykonywania, który jest używany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="36a29-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="36a29-177">Następujące parametry są ustawione w czasie wykonywania dla tych topologii:</span><span class="sxs-lookup"><span data-stu-id="36a29-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="36a29-178">`${kafka.topic}`: Nazwa Kafka temat topologii odczytu/zapisu do.</span><span class="sxs-lookup"><span data-stu-id="36a29-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="36a29-179">`${kafka.broker.hosts}`: Uruchom hostów, które przekazuje informacje dotyczące Kafka na.</span><span class="sxs-lookup"><span data-stu-id="36a29-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="36a29-180">Informacje o brokera jest używany przez KafkaBolt podczas zapisywania Kafka.</span><span class="sxs-lookup"><span data-stu-id="36a29-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="36a29-181">`${kafka.zookeeper.hosts}`: Hostów, które dozorcy działa na Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="36a29-182">Aby uzyskać więcej informacji dotyczących topologii strumienia, zobacz [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="36a29-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="36a29-183">Pobierz i kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="36a29-183">Download and compile the project</span></span>

1. <span data-ttu-id="36a29-184">Na środowiska deweloperskiego pobrać projekt z [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), Otwórz wiersza polecenia i przejdź do lokalizacji został pobrany projekt.</span><span class="sxs-lookup"><span data-stu-id="36a29-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="36a29-185">Z **hdinsight-storm-java-kafka** katalogu, użyj następującego polecenia, aby skompilować projekt i utworzenie pakietu wdrażania:</span><span class="sxs-lookup"><span data-stu-id="36a29-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="36a29-186">Proces pakietu tworzy plik o nazwie `KafkaTopology-1.0-SNAPSHOT.jar` w `target` katalogu.</span><span class="sxs-lookup"><span data-stu-id="36a29-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="36a29-187">Użyj następujących poleceń, aby skopiować pakiet do Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a29-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="36a29-188">Zastąp **USERNAME** z nazwą użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="36a29-189">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej używane podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="36a29-190">Po wyświetleniu monitu wprowadź hasło, które zostały użyte podczas tworzenia klastrów.</span><span class="sxs-lookup"><span data-stu-id="36a29-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="36a29-191">Konfigurowanie topologii</span><span class="sxs-lookup"><span data-stu-id="36a29-191">Configure the topology</span></span>

1. <span data-ttu-id="36a29-192">Użyj jednej z następujących metod odnajdywania hostów brokera Kafka:</span><span class="sxs-lookup"><span data-stu-id="36a29-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
    > <span data-ttu-id="36a29-193">W przykładzie Bash, przy założeniu, że `$CLUSTERNAME` zawiera nazwę klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a29-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="36a29-194">Założono również, że [jq](https://stedolan.github.io/jq/) jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="36a29-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="36a29-195">Po wyświetleniu monitu wprowadź hasło dla konta logowania klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="36a29-196">Wartość zwracana jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="36a29-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="36a29-197">Może być więcej niż dwa hosty broker dla klastra, nie trzeba zapewniają pełną listę wszystkich hostów do klientów.</span><span class="sxs-lookup"><span data-stu-id="36a29-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="36a29-198">Jedno lub dwa jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="36a29-198">One or two is enough.</span></span>

2. <span data-ttu-id="36a29-199">Użyj jednej z następujących metod odnajdywania hostów dozorcy Kafka:</span><span class="sxs-lookup"><span data-stu-id="36a29-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
    > <span data-ttu-id="36a29-200">W przykładzie Bash, przy założeniu, że `$CLUSTERNAME` zawiera nazwę klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a29-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="36a29-201">Założono również, że [jq](https://stedolan.github.io/jq/) jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="36a29-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="36a29-202">Po wyświetleniu monitu wprowadź hasło dla konta logowania klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="36a29-203">Wartość zwracana jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="36a29-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="36a29-204">W czasie więcej niż dwa węzły dozorcy zapewniają pełną listę wszystkich hostów do klientów nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="36a29-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="36a29-205">Jedno lub dwa jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="36a29-205">One or two is enough.</span></span>

    <span data-ttu-id="36a29-206">Zapisz tę wartość, ponieważ jest używana później.</span><span class="sxs-lookup"><span data-stu-id="36a29-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="36a29-207">Edytuj `dev.properties` w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="36a29-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="36a29-208">Dodaj informacje hostów brokera i dozorcy do zgodnych wierszy w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="36a29-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="36a29-209">Poniższy przykład jest konfigurowana przy użyciu przykładowe wartości z poprzednich kroków:</span><span class="sxs-lookup"><span data-stu-id="36a29-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="36a29-210">Zapisz `dev.properties` pliku, a następnie przekaż go do klastra Storm za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="36a29-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="36a29-211">Zastąp **USERNAME** z nazwą użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="36a29-212">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej używane podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="36a29-213">Uruchom moduł zapisujący</span><span class="sxs-lookup"><span data-stu-id="36a29-213">Start the writer</span></span>

1. <span data-ttu-id="36a29-214">Użyj następującego polecenia do nawiązania połączenia z klastrem Storm przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="36a29-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="36a29-215">Zastąp **USERNAME** przy użyciu nazwy użytkownika SSH używany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="36a29-216">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej używany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="36a29-217">Po wyświetleniu monitu wprowadź hasło, które zostały użyte podczas tworzenia klastrów.</span><span class="sxs-lookup"><span data-stu-id="36a29-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="36a29-218">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="36a29-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="36a29-219">Z połączenia SSH wpisz następujące polecenie do utworzenia tematu Kafka używane przez topologii:</span><span class="sxs-lookup"><span data-stu-id="36a29-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="36a29-220">Zastąp `$KAFKAZKHOSTS` z dozorcy hosta informacji pobrany w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="36a29-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="36a29-221">Połączenie SSH z klastrem Storm Użyj następującego polecenia można uruchomić modułu zapisującego topologii:</span><span class="sxs-lookup"><span data-stu-id="36a29-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="36a29-222">Parametry używane w tym poleceniu są:</span><span class="sxs-lookup"><span data-stu-id="36a29-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="36a29-223">`org.apache.storm.flux.Flux`: Użyj strumienia do skonfigurowania i uruchomienia tej topologii.</span><span class="sxs-lookup"><span data-stu-id="36a29-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="36a29-224">`--remote`: Przesyłania topologii do Nimbus.</span><span class="sxs-lookup"><span data-stu-id="36a29-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="36a29-225">Topologia jest dystrybuowana do węzłów procesu roboczego w klastrze.</span><span class="sxs-lookup"><span data-stu-id="36a29-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="36a29-226">`-R /writer.yaml`: Użyj `writer.yaml` pliku, aby skonfigurować topologię.</span><span class="sxs-lookup"><span data-stu-id="36a29-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="36a29-227">`-R`Wskazuje, że ten zasób jest uwzględniona w pliku jar.</span><span class="sxs-lookup"><span data-stu-id="36a29-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="36a29-228">Znajduje się w folderze głównym jar, więc `/writer.yaml` jest ścieżką do niego.</span><span class="sxs-lookup"><span data-stu-id="36a29-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="36a29-229">`--filter`: Wypełnić wpisów w `writer.yaml` topologię za pomocą wartości w `dev.properties` pliku.</span><span class="sxs-lookup"><span data-stu-id="36a29-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="36a29-230">Na przykład wartość `kafka.topic` wpis w pliku jest używany do zastępowania `${kafka.topic}` wejścia w definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="36a29-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="36a29-231">Po rozpoczęciu topologii, użyj następującego polecenia, aby sprawdzić, czy jest zapisywania danych do tematu Kafka:</span><span class="sxs-lookup"><span data-stu-id="36a29-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="36a29-232">Zastąp `$KAFKAZKHOSTS` z dozorcy hosta informacji pobrany w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="36a29-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="36a29-233">To polecenie używa skryptu dostarczone z Kafka do monitorowania tematu.</span><span class="sxs-lookup"><span data-stu-id="36a29-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="36a29-234">Po chwili należy uruchomić, zwracanie losowe zdania, które zostały zapisane w temacie.</span><span class="sxs-lookup"><span data-stu-id="36a29-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="36a29-235">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="36a29-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="36a29-236">Użyj klawiszy Ctrl + c, aby zatrzymać skrypt.</span><span class="sxs-lookup"><span data-stu-id="36a29-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="36a29-237">Uruchom czytnik</span><span class="sxs-lookup"><span data-stu-id="36a29-237">Start the reader</span></span>

1. <span data-ttu-id="36a29-238">W sesji SSH z klastrem Storm Użyj następującego polecenia można uruchomić topologii czytnika:</span><span class="sxs-lookup"><span data-stu-id="36a29-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="36a29-239">Po uruchomieniu topologii Otwórz interfejsu użytkownika platformy Storm.</span><span class="sxs-lookup"><span data-stu-id="36a29-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="36a29-240">Interfejs użytkownika sieci web znajduje się pod adresem https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="36a29-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="36a29-241">Zastąp __nazwę BAZOWĄ__ o nazwie podstawowej używane podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="36a29-242">Po wyświetleniu monitu użyj nazwy logowania administratora (domyślnie `admin`) i hasło używane podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="36a29-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="36a29-243">Widzisz stronę sieci web podobną do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="36a29-243">You see a web page similar to the following image:</span></span>

    ![STORM interfejsu użytkownika](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="36a29-245">Z poziomu interfejsu użytkownika Storm, wybierz __czytnika kafka__ łącze w __podsumowanie topologii__ sekcji, aby wyświetlić informacje o __kafka czytnika__ topologii.</span><span class="sxs-lookup"><span data-stu-id="36a29-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Sekcji podsumowania topologii Storm interfejsu użytkownika sieci web](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="36a29-247">Aby wyświetlić informacje na temat wystąpień elementu bolt rejestratora, zaznacz __bolt rejestratora__ łącze w __elementów Bolt (czas wszystkich)__ sekcji.</span><span class="sxs-lookup"><span data-stu-id="36a29-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Łącze bolt rejestratora w sekcji elementów bolt](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="36a29-249">W __modułów__ wybierz łącze w __portu__ kolumny do wyświetlania rejestrowania informacji dotyczących tego wystąpienia składnika.</span><span class="sxs-lookup"><span data-stu-id="36a29-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![Łącze modułów](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="36a29-251">Dziennik zawiera dziennik odczytanych z tematu Kafka danych.</span><span class="sxs-lookup"><span data-stu-id="36a29-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="36a29-252">Informacje w dzienniku jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="36a29-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="36a29-253">Zatrzymywanie topologii</span><span class="sxs-lookup"><span data-stu-id="36a29-253">Stop the topologies</span></span>

<span data-ttu-id="36a29-254">W sesji SSH z klastrem Storm Użyj następujących poleceń, aby zatrzymać topologii Storm:</span><span class="sxs-lookup"><span data-stu-id="36a29-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="36a29-255">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="36a29-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="36a29-256">Ponieważ kroki opisane w tym dokumencie utworzyć obu klastrów w tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36a29-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="36a29-257">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów tworzone przez wykonanie tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="36a29-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36a29-258">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36a29-258">Next steps</span></span>

<span data-ttu-id="36a29-259">Aby uzyskać więcej przykładowe topologie, które mogą być używane z systemu Storm w usłudze HDInsight, zobacz [topologii Storm przykład i składniki](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="36a29-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="36a29-260">Aby uzyskać informacje dotyczące wdrażania i monitorowania topologii na HDInsight opartych na systemie Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="36a29-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>