---
title: aaaStart z Kafka Apache - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak Kafka Apache toocreate klastra w usłudze Azure HDInsight. Dowiedz się, jak toocreate tematów, subskrybentów i konsumentów."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="338ba-104">Wprowadzenie do platformy Apache Kafka (wersja zapoznawcza) w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="338ba-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="338ba-105">Dowiedz się, jak toocreate i użyj [Apache Kafka](https://kafka.apache.org) klastra w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="338ba-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="338ba-106">Kafka to rozproszona platforma przesyłania strumieniowego typu „open source”, dostępna z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="338ba-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="338ba-107">Jest często używana jako broker komunikatu, ponieważ zapewnia funkcje podobne tooa publikacji / subskrypcji kolejki komunikatów.</span><span class="sxs-lookup"><span data-stu-id="338ba-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="338ba-108">Obecnie są dostępne dwie wersje platformy Kafka w usłudze HDInsight: 0.9.0 (HDInsight 3.4) i 0.10.0 (HDInsight 3.5 i 3.6).</span><span class="sxs-lookup"><span data-stu-id="338ba-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="338ba-109">Hello kroków w tym dokumencie założono, że używasz Kafka na 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="338ba-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="338ba-110">Tworzenie klastra platformy Kafka</span><span class="sxs-lookup"><span data-stu-id="338ba-110">Create a Kafka cluster</span></span>

<span data-ttu-id="338ba-111">Użyj hello następujące kroki toocreate Kafka w klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="338ba-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="338ba-112">Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy**, **analizy i analiza**, a następnie wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="338ba-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Tworzenie klastra usługi HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="338ba-114">Z **podstawy**, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="338ba-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="338ba-115">**Nazwa klastra**: Nazwa hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="338ba-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="338ba-116">**Subskrypcja**: Wybierz hello toouse subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="338ba-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="338ba-117">**Nazwa użytkownika logowania klastra** i **hasło logowania klastra**: hello logowania podczas uzyskiwania dostępu do klastra hello za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="338ba-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="338ba-118">Korzystania z tych usług tooaccess poświadczeń, takich jak hello Interfejsu sieci Web Ambari lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="338ba-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="338ba-119">**Secure Shell (SSH) username**: hello logowania używany podczas uzyskiwania dostępu do klastra hello za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="338ba-120">Domyślnie jest hello takie samo jak hasło logowania klastra hello hello hasła.</span><span class="sxs-lookup"><span data-stu-id="338ba-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="338ba-121">**Grupa zasobów**: hello klastra hello toocreate grupy zasobów w.</span><span class="sxs-lookup"><span data-stu-id="338ba-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="338ba-122">**Lokalizacja**: hello regionu Azure toocreate hello klastra w.</span><span class="sxs-lookup"><span data-stu-id="338ba-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Wybieranie subskrypcji](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="338ba-124">Wybierz **typ klastra**, a następnie hello ustaw następujące wartości z **konfiguracji klastra**:</span><span class="sxs-lookup"><span data-stu-id="338ba-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="338ba-125">**Typ klastra**: Kafka</span><span class="sxs-lookup"><span data-stu-id="338ba-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="338ba-126">**Wersja**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="338ba-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="338ba-127">**Warstwa klastra**: Standardowa</span><span class="sxs-lookup"><span data-stu-id="338ba-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="338ba-128">Na koniec użyj hello **wybierz** przycisk toosave ustawienia.</span><span class="sxs-lookup"><span data-stu-id="338ba-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Wybieranie typu klastra](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="338ba-130">Po wybraniu typu klastra hello, użyj hello __wybierz__ tooset hello klastra typ przycisku.</span><span class="sxs-lookup"><span data-stu-id="338ba-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="338ba-131">Następnie użyj hello __dalej__ przycisk toofinish podstawową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="338ba-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="338ba-132">W bloku **Magazyn** wybierz lub utwórz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="338ba-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="338ba-133">Witaj czynności w tym dokumencie pozostaw hello innych pól na wartości domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="338ba-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="338ba-134">Użyj hello __dalej__ przycisk toosave magazynu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="338ba-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Ustaw hello ustawienia konta magazynu dla usługi HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="338ba-136">Z __aplikacji (opcjonalnie)__, wybierz pozycję __dalej__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="338ba-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="338ba-137">W tym przykładzie nie są wymagane żadne aplikacje.</span><span class="sxs-lookup"><span data-stu-id="338ba-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="338ba-138">Z __rozmiar klastra__, wybierz pozycję __dalej__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="338ba-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="338ba-139">dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="338ba-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Zestaw hello Kafka rozmiar klastra](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="338ba-141">Witaj **dyski dla każdego węzła procesu roboczego** kontroli hello skalowalność Kafka w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="338ba-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="338ba-142">Aby uzyskać więcej informacji, zobacz [Configure storage and scalability of Kafka on HDInsight (Konfigurowanie magazynu i skalowalności platformy Kafka w usłudze HDInsight)](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="338ba-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="338ba-143">Z __Zaawansowane ustawienia__, wybierz pozycję __dalej__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="338ba-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="338ba-144">Z hello **Podsumowanie**, należy przejrzeć konfigurację hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="338ba-145">Użyj hello __Edytuj__ łączy toochange wszystkie ustawienia, które są nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="338ba-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="338ba-146">Na koniec użyj the__Create__ przycisk toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Podsumowanie konfiguracji klastra](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="338ba-148">Może potrwać too20 minut toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="338ba-149">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="338ba-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="338ba-150">Podczas wykonywania hello następujące kroki, musisz użyć klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="338ba-151">Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="338ba-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="338ba-152">Z tego klienta użyj klastra toohello tooconnect SSH:</span><span class="sxs-lookup"><span data-stu-id="338ba-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="338ba-153">Zastąp **SSHUSER** z nazwą użytkownika SSH hello podany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="338ba-154">Zastąp **CLUSTERNAME** o nazwie hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="338ba-155">Po wyświetleniu monitu wprowadź hasło hello, używanego hello konta SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="338ba-156">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="338ba-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="338ba-157"><a id="getkafkainfo"></a>Pobierz hello dozorcy i brokera informacji o hoście</span><span class="sxs-lookup"><span data-stu-id="338ba-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="338ba-158">Podczas pracy z Kafka, musisz znać dwóch wartości host; Witaj *dozorcy* hostów i hello *brokera* hostów.</span><span class="sxs-lookup"><span data-stu-id="338ba-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="338ba-159">Te hosty są używane przez hello Kafka interfejsu API i wiele narzędzi hello, które są dostarczane z Kafka.</span><span class="sxs-lookup"><span data-stu-id="338ba-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="338ba-160">Użyj następujących zmiennych środowiskowych toocreate kroki, które zawierają informacje dotyczące hosta hello hello.</span><span class="sxs-lookup"><span data-stu-id="338ba-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="338ba-161">Te zmienne środowiskowe są używane w krokach hello w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="338ba-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="338ba-162">Z klastra toohello połączenia SSH, użyj hello następujące polecenie tooinstall hello `jq` narzędzia.</span><span class="sxs-lookup"><span data-stu-id="338ba-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="338ba-163">To narzędzie jest używane tooparse dokumentów JSON i jest przydatne podczas pobierania informacji o hoście brokera hello:</span><span class="sxs-lookup"><span data-stu-id="338ba-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="338ba-164">zmienne środowiskowe hello tooset informacje są pobierane z Ambari, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="338ba-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="338ba-165">Ustaw `CLUSTERNAME=` toohello nazwę hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="338ba-166">Ustaw `PASSWORD=` toohello hasło logowania (Administrator) używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="338ba-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="338ba-167">Witaj następujący tekst jest przykładem zawartość hello `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="338ba-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="338ba-168">Witaj następujący tekst jest przykładem zawartość hello `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="338ba-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="338ba-169">Witaj `cut` polecenia jest używane tootrim hello listę hostów tootwo hosta.</span><span class="sxs-lookup"><span data-stu-id="338ba-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="338ba-170">Nie trzeba tooprovide hello pełną listę hostów podczas tworzenia Kafka konsumenta lub producenta.</span><span class="sxs-lookup"><span data-stu-id="338ba-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="338ba-171">Nie należy polegać na powitania informacje zwrócone z tej sesji tooalways być dokładne.</span><span class="sxs-lookup"><span data-stu-id="338ba-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="338ba-172">Skala klastra hello nowe brokerzy zostały dodane lub usunięte.</span><span class="sxs-lookup"><span data-stu-id="338ba-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="338ba-173">Jeśli wystąpi błąd, a węzeł zostanie zastąpiony, mogą ulec zmianie nazwy hosta hello hello węzła.</span><span class="sxs-lookup"><span data-stu-id="338ba-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="338ba-174">Należy pobrać informacji hostów dozorcy i brokera hello, tuż przed jego użyciem tooensure ma nieprawidłowe informacje.</span><span class="sxs-lookup"><span data-stu-id="338ba-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="338ba-175">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="338ba-175">Create a topic</span></span>

<span data-ttu-id="338ba-176">Platforma Kafka przechowuje strumienie danych w kategoriach nazywanych *tematami*.</span><span class="sxs-lookup"><span data-stu-id="338ba-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="338ba-177">Programu SSH połączenia tooa klastra headnode można użyć skryptu dostarczonego z Kafka toocreate tematu:</span><span class="sxs-lookup"><span data-stu-id="338ba-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="338ba-178">To polecenie łączy tooZookeeper przy użyciu informacji o hoście hello przechowywane w `$KAFKAZKHOSTS`, a następnie utworzyć temat Kafka o nazwie **testu**.</span><span class="sxs-lookup"><span data-stu-id="338ba-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="338ba-179">Możesz sprawdzić, czy ten temat hello został utworzony przy użyciu hello następujące tematy toolist skryptu:</span><span class="sxs-lookup"><span data-stu-id="338ba-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="338ba-180">Hello dane wyjściowe tego polecenia Lista Kafka tematów, który zawiera hello **test** tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="338ba-181">Tworzenie i używanie rekordów</span><span class="sxs-lookup"><span data-stu-id="338ba-181">Produce and consume records</span></span>

<span data-ttu-id="338ba-182">Platforma Kafka przechowuje *rekordy* w tematach.</span><span class="sxs-lookup"><span data-stu-id="338ba-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="338ba-183">Rekordy są tworzone przez *producentów* i używane przez *odbiorców*.</span><span class="sxs-lookup"><span data-stu-id="338ba-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="338ba-184">Producenci pobierają rekordy z *brokerów* platformy Kafka.</span><span class="sxs-lookup"><span data-stu-id="338ba-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="338ba-185">Każdy węzeł procesu roboczego w klastrze usługi HDInsight jest brokerem platformy Kafka.</span><span class="sxs-lookup"><span data-stu-id="338ba-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="338ba-186">Użyj hello następujące kroki toostore rekordy na temat do testowania hello utworzony wcześniej, a następnie przeczytaj je za pomocą z klientem:</span><span class="sxs-lookup"><span data-stu-id="338ba-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="338ba-187">W sesji SSH hello Użyj skryptu dostarczonego z Kafka toowrite rekordów toohello tematu:</span><span class="sxs-lookup"><span data-stu-id="338ba-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="338ba-188">Użytkownik nie są zwracane toohello monitu po wykonaniu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="338ba-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="338ba-189">Zamiast tego wpisz kilka wiadomości SMS, a następnie użyć **klawisze Ctrl + C** toostop wysyłania toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="338ba-190">Każdy wiersz jest wysyłany jako oddzielny rekord.</span><span class="sxs-lookup"><span data-stu-id="338ba-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="338ba-191">Użyj skryptu dostarczonego z Kafka tooread rekordy z tematu hello:</span><span class="sxs-lookup"><span data-stu-id="338ba-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="338ba-192">To polecenie pobiera hello rekordy z tematu hello i wyświetla je.</span><span class="sxs-lookup"><span data-stu-id="338ba-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="338ba-193">Przy użyciu `--from-beginning` informuje toostart konsumenta powitania od początku hello strumienia hello, pobierane są wszystkie rekordy.</span><span class="sxs-lookup"><span data-stu-id="338ba-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="338ba-194">Użyj __klawisze Ctrl + C__ toostop powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="338ba-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="338ba-195">Interfejs API producenta i odbiorcy</span><span class="sxs-lookup"><span data-stu-id="338ba-195">Producer and consumer API</span></span>

<span data-ttu-id="338ba-196">Można również programowego tworzenia i wykorzystywania rekordów przy użyciu hello [API Kafka](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="338ba-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="338ba-197">toobuild producent Java i konsumentów, użyj hello następujące kroki od środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="338ba-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="338ba-198">Musi mieć hello następujące składniki zainstalowane w środowisku projektowania:</span><span class="sxs-lookup"><span data-stu-id="338ba-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="338ba-199">[Zestaw Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) lub równoważny, taki jak OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="338ba-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="338ba-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="338ba-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="338ba-201">Klient SSH i hello `scp` polecenia.</span><span class="sxs-lookup"><span data-stu-id="338ba-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="338ba-202">Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="338ba-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="338ba-203">Pobierz przykłady hello z [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="338ba-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="338ba-204">Na przykład producent i konsument hello, użyj hello projektu w hello `Producer-Consumer` katalogu.</span><span class="sxs-lookup"><span data-stu-id="338ba-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="338ba-205">Ten przykład zawiera następujące klasy hello:</span><span class="sxs-lookup"><span data-stu-id="338ba-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="338ba-206">**Uruchom** — uruchamia powitania klienta lub producenta.</span><span class="sxs-lookup"><span data-stu-id="338ba-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="338ba-207">**Producent** -magazynów 1 000 000 rekordów toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="338ba-208">**Konsument** -odczytuje rekordy z hello tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="338ba-209">toocreate pakiet jar zmiany lokalizacji toohello katalogów hello `Producer-Consumer` hello katalogu i użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="338ba-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="338ba-210">To polecenie tworzy katalog o nazwie `target`, który zawiera plik o nazwie `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="338ba-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="338ba-211">Użyj następujących hello polecenia toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` klastra usługi HDInsight tooyour pliku:</span><span class="sxs-lookup"><span data-stu-id="338ba-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="338ba-212">Zastąp **SSHUSER** hello użytkownika SSH dla klastra i Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="338ba-213">Po wyświetleniu monitu wprowadź hasło hello hello użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="338ba-214">Raz hello `scp` polecenia zakończenie kopiowania pliku hello, Połącz toohello klastra przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="338ba-215">Witaj Użyj następującego polecenia toowrite rejestruje toohello temat do testowania:</span><span class="sxs-lookup"><span data-stu-id="338ba-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="338ba-216">Po zakończeniu procesu hello, użyj poniższych tooread polecenie z tematu hello hello:</span><span class="sxs-lookup"><span data-stu-id="338ba-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="338ba-217">rejestruje Hello Odczyt, wraz z liczbą rekordów, zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="338ba-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="338ba-218">Może pojawić się kilka więcej niż 1 000 000 rejestrowane jako wysłanej kilka tematu toohello rekordów za pomocą skryptu w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="338ba-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="338ba-219">Użyj __klawisze Ctrl + C__ tooexit powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="338ba-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="338ba-220">Wielu odbiorców</span><span class="sxs-lookup"><span data-stu-id="338ba-220">Multiple consumers</span></span>

<span data-ttu-id="338ba-221">Odbiorcy platformy Kafka używają grupy odbiorców podczas odczytywania rekordów.</span><span class="sxs-lookup"><span data-stu-id="338ba-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="338ba-222">Przy użyciu hello same grupy z wielu klientów powoduje obciążenia zrównoważonym odczyty z tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="338ba-223">Każdy odbiorca w grupie hello odbiera część hello rekordów.</span><span class="sxs-lookup"><span data-stu-id="338ba-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="338ba-224">toosee przez ten proces w akcji, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="338ba-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="338ba-225">Otwórz nowy klaster toohello sesji SSH, dzięki czemu masz dwa z nich.</span><span class="sxs-lookup"><span data-stu-id="338ba-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="338ba-226">W każdej sesji, należy użyć hello następujących toostart konsumenta z hello tego samego Identyfikatora grupy odbiorców:</span><span class="sxs-lookup"><span data-stu-id="338ba-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="338ba-227">To polecenie uruchamia konsumenta za pomocą Identyfikatora grupy hello `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="338ba-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="338ba-228">Używanie poleceń hello w hello [uzyskać hello dozorcy i brokera informacji o hoście](#getkafkainfo) tooset sekcji `$KAFKABROKERS` dla tej sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="338ba-229">Obejrzyj jako każdej sesji rekordy hello liczby otrzymywanych z hello tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="338ba-230">Suma Hello zarówno sesji powinien hello tego samego zgodnie z wcześniej otrzymanej od jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="338ba-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="338ba-231">Użycie przez klientów w ramach hello tej samej grupy jest obsługiwany za pomocą partycji hello hello tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="338ba-232">Dla hello `test` tematu utworzonego wcześniej, ma osiem partycji.</span><span class="sxs-lookup"><span data-stu-id="338ba-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="338ba-233">Otwórz osiem sesji SSH, uruchom klienta we wszystkich sesjach każdy odbiorca odczytuje rekordy z jednej partycji dla tematu hello.</span><span class="sxs-lookup"><span data-stu-id="338ba-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="338ba-234">Grupa odbiorców nie może zawierać więcej wystąpień odbiorców niż partycji.</span><span class="sxs-lookup"><span data-stu-id="338ba-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="338ba-235">W tym przykładzie jednej grupy konsumentów może zawierać zapasowej tooeight konsumentów, ponieważ jest hello liczby partycji w temacie hello.</span><span class="sxs-lookup"><span data-stu-id="338ba-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="338ba-236">Może też istnieć wiele grup odbiorców — każda z nich może zawierać maksymalnie ośmiu odbiorców.</span><span class="sxs-lookup"><span data-stu-id="338ba-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="338ba-237">Rekordy przechowywane w Kafka są przechowywane w kolejności hello odbieranych w partycji.</span><span class="sxs-lookup"><span data-stu-id="338ba-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="338ba-238">dostarczania uporządkowanego tooachieve rekordów *w partycji*, Utwórz grupę konsumenta, jeśli hello liczbą wystąpień klienta odpowiada hello liczby partycji.</span><span class="sxs-lookup"><span data-stu-id="338ba-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="338ba-239">dostarczania uporządkowanego tooachieve rekordów *w temacie hello*, Utwórz grupę odbiorców z wystąpieniem tylko jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="338ba-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="338ba-240">Interfejs API przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="338ba-240">Streaming API</span></span>

<span data-ttu-id="338ba-241">Witaj przesyłania strumieniowego interfejsu API dodano tooKafka w wersji 0.10.0; wcześniejszych wersji polegają na Apache Spark lub Storm do przetwarzania strumienia.</span><span class="sxs-lookup"><span data-stu-id="338ba-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="338ba-242">Jeśli nie zostało to jeszcze zrobione, Pobierz przykłady hello z [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour Środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="338ba-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="338ba-243">W przypadku przesyłania strumieniowego przykład hello, należy użyć hello projektu w hello `streaming` katalogu.</span><span class="sxs-lookup"><span data-stu-id="338ba-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="338ba-244">Ten projekt zawiera tylko jedną klasę `Stream`, która odczytuje rekordy z hello `test` wcześniej utworzony temat.</span><span class="sxs-lookup"><span data-stu-id="338ba-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="338ba-245">Zlicza wyrazy hello odczytu i emituje każdego tematu tooa word i licznik o nazwie `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="338ba-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="338ba-246">Witaj `wordcounts` tematu jest tworzony w kolejnym kroku w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="338ba-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="338ba-247">Z wiersza polecenia hello w środowisku projektowania, zmień lokalizację toohello katalogów hello `Streaming` katalogu, a następnie hello Użyj następującego polecenia toocreate pakietu jar:</span><span class="sxs-lookup"><span data-stu-id="338ba-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="338ba-248">To polecenie tworzy katalog o nazwie `target`, który zawiera plik o nazwie `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="338ba-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="338ba-249">Użyj następujących hello polecenia toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` klastra usługi HDInsight tooyour pliku:</span><span class="sxs-lookup"><span data-stu-id="338ba-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="338ba-250">Zastąp **SSHUSER** hello użytkownika SSH dla klastra i Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="338ba-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="338ba-251">Po wyświetleniu monitu wprowadź hasło hello hello użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="338ba-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="338ba-252">Raz hello `scp` polecenia zakończenie kopiowania pliku hello, Połącz toohello klastra przy użyciu protokołu SSH, a następnie użyj hello następujące polecenia toocreate hello `wordcounts` tematu:</span><span class="sxs-lookup"><span data-stu-id="338ba-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="338ba-253">Następnie uruchom hello przesyłania strumieniowego procesu za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="338ba-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="338ba-254">To polecenie uruchamia hello przesyłania strumieniowego proces w tle hello.</span><span class="sxs-lookup"><span data-stu-id="338ba-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="338ba-255">Użyj hello następujące polecenie toohello wiadomości toosend `test` tematu.</span><span class="sxs-lookup"><span data-stu-id="338ba-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="338ba-256">Komunikaty te są przetwarzane przez hello przesyłania strumieniowego przykładzie:</span><span class="sxs-lookup"><span data-stu-id="338ba-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="338ba-257">Witaj Użyj następującego polecenia tooview hello dane wyjściowe są zapisywane toohello `wordcounts` tematu przez hello przesyłania strumieniowego proces:</span><span class="sxs-lookup"><span data-stu-id="338ba-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="338ba-258">tooview hello danych, musi podać hello tooprint konsumenta hello i toouse Deserializator hello hello klucza i wartości.</span><span class="sxs-lookup"><span data-stu-id="338ba-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="338ba-259">Nazwa klucza Hello jest słowem hello i hello wartość klucza zawiera hello liczby.</span><span class="sxs-lookup"><span data-stu-id="338ba-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="338ba-260">Witaj danych wyjściowych jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="338ba-260">hello output is similar toohello following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="338ba-261">Liczba Hello zwiększa zawsze, gdy napotkano wyrazu.</span><span class="sxs-lookup"><span data-stu-id="338ba-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="338ba-262">Użyj hello __klawisze Ctrl + C__ tooexit hello konsumenta, a następnie użyj hello `fg` polecenia toobring hello wstecz toohello zadania przesyłania strumieniowego tła pierwszego planu.</span><span class="sxs-lookup"><span data-stu-id="338ba-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="338ba-263">Użyj __klawisze Ctrl + C__ tooexit on również.</span><span class="sxs-lookup"><span data-stu-id="338ba-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="338ba-264">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="338ba-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="338ba-265">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="338ba-265">Troubleshoot</span></span>

<span data-ttu-id="338ba-266">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="338ba-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="338ba-267">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="338ba-267">Next steps</span></span>

<span data-ttu-id="338ba-268">W tym dokumencie uzyskanych hello podstawowe informacje dotyczące pracy z Kafka Apache na HDInsight.</span><span class="sxs-lookup"><span data-stu-id="338ba-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="338ba-269">Użyj następującego toolearn więcej informacji na temat pracy z Kafka hello:</span><span class="sxs-lookup"><span data-stu-id="338ba-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="338ba-270">Ensure high availability of your data with Kafka on HDInsight (Zapewnianie wysokiej dostępności danych dzięki platformie Kafka w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="338ba-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="338ba-271">Increase scalability by configuring managed disks with Kafka on HDInsight (Zwiększanie skalowalności przez konfigurowanie dysków zarządzanych przy użyciu platformy Kafka w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="338ba-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="338ba-272">[Dokumentacja platformy Apache Kafka](http://kafka.apache.org/documentation.html) na stronie kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="338ba-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="338ba-273">Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="338ba-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="338ba-274">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="338ba-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="338ba-275">Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="338ba-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="338ba-276">Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="338ba-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
