---
title: Tematy Apache Kafka aaaMirror - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Apache Kafka dublowania funkcji toomaintain repliki Kafka w klastrze usługi HDInsight przy dublowania tematy tooa dodatkowej klastra."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="bbe5a-103">Tematy Apache Kafka tooreplicate MirrorMaker za pomocą Kafka w usłudze HDInsight (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="bbe5a-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="bbe5a-104">Dowiedz się, jak toouse Apache Kafka przez dublowanie funkcji tooreplicate tematy tooa dodatkowej klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="bbe5a-105">Dublowanie mogą być uruchomione jako ciągły proces wykonywany lub sporadycznie używane jako metody migracji danych z jednego klastra tooanother.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="bbe5a-106">W tym przykładzie dublowanie jest używane tooreplicate tematy między dwoma klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="bbe5a-107">Obu klastrach znajdują się w sieci wirtualnej platformy Azure w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="bbe5a-108">Dublowanie nie należy traktować jako oznacza tooachieve odporności na uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="bbe5a-109">przesunięcia tooitems Hello w temacie różnią się między hello klastrów źródłowych i docelowych, więc klienci nie mogą używać hello dwa zamiennie.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="bbe5a-110">Jeśli masz obawy odporność na uszkodzenia, należy ustawić replikacji hello tematów w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="bbe5a-111">Aby uzyskać więcej informacji, zobacz [wprowadzenie Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bbe5a-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="bbe5a-112">Jak działa Kafka dublowania</span><span class="sxs-lookup"><span data-stu-id="bbe5a-112">How Kafka mirroring works</span></span>

<span data-ttu-id="bbe5a-113">Dublowania działa przy użyciu hello MirrorMaker narzędzia (część Apache Kafka) tooconsume rekordy z tematów w klastrze źródłowym hello, a następnie utwórz kopię lokalną w klastrze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="bbe5a-114">MirrorMaker używa jednej (lub więcej) *konsumentów* odczytanej z klastra źródłowego hello, a *producent* który zapisuje toohello klastra lokalnego (docelowy).</span><span class="sxs-lookup"><span data-stu-id="bbe5a-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="bbe5a-115">powitania po diagram przedstawia proces lustrzane hello:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Diagram hello dublowania procesu](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="bbe5a-117">Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka usługi za pośrednictwem hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="bbe5a-118">Kafka producentów i konsumentów, musi być w hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="bbe5a-119">W tym przykładzie zarówno hello źródła Kafka, jak i klastrów docelowych znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="bbe5a-120">Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram źródłowy i docelowy Kafka klastrów w sieci wirtualnej platformy Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="bbe5a-122">Witaj klastrów źródłowych i docelowych mogą być różne w hello liczby węzłów i partycji, różni się od przesunięcia w tematach hello również.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="bbe5a-123">Dublowania przechowuje hello wartości klucza, który jest używany do partycjonowania, więc na podstawie na klucz jest zachowana kolejność rekordów.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="bbe5a-124">Dublowanie bariery sieciowe</span><span class="sxs-lookup"><span data-stu-id="bbe5a-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="bbe5a-125">Jeśli potrzebujesz toomirror między klastrami Kafka w różnych sieciach, istnieją hello następujące dodatkowe zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="bbe5a-126">**Bram**: hello sieci muszą być stanie toocommunicate na powitania TCPIP poziom.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="bbe5a-127">**Rozpoznawanie nazw**: hello Kafka klastrów w każdej sieci musi być możliwe tooconnect tooeach innych przy użyciu nazwy hostów.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="bbe5a-128">Może to wymagać się, że serwer systemu nazw domen (DNS) w każdej sieci, który jest skonfigurowany toohello żądań tooforward innych sieci.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="bbe5a-129">Podczas tworzenia sieci wirtualnej platformy Azure, zamiast hello podane automatyczne DNS z sieci hello, należy określić niestandardowy DNS serwera i hello adres IP serwera hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="bbe5a-130">Po hello utworzenia sieci wirtualnej należy następnie utwórz maszynę wirtualną platformy Azure, który korzysta z tego adresu IP, a następnie zainstalować i skonfigurować oprogramowanie DNS na nim.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="bbe5a-131">Utworzyć i skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej hello hello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="bbe5a-132">Nie istnieje konfiguracja dodatkowe wymagane dla usługi HDInsight toouse powitania serwera DNS skonfigurowanego dla hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="bbe5a-133">Aby uzyskać więcej informacji na łącząca dwie sieci wirtualne platformy Azure, zobacz [skonfigurować połączenia do wirtualnymi](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bbe5a-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="bbe5a-134">Tworzenie Kafka klastrów</span><span class="sxs-lookup"><span data-stu-id="bbe5a-134">Create Kafka clusters</span></span>

<span data-ttu-id="bbe5a-135">Podczas tworzenia sieci wirtualnej platformy Azure i Kafka klastrów ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="bbe5a-136">Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure i dwa Kafka tooyour klastrów subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="bbe5a-137">Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="bbe5a-138">Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="bbe5a-139">dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="bbe5a-140">Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="bbe5a-141">Witaj Użyj następujących informacji toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="bbe5a-143">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="bbe5a-144">Ta grupa zawiera hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="bbe5a-145">**Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="bbe5a-146">**Podstawowa nazwa klastra**: Ta wartość jest używana jako podstawowej nazwy hello hello Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="bbe5a-147">Na przykład wprowadzenie **hdi** tworzy klastry o nazwie **hdi źródła** i **dest hdi**.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="bbe5a-148">**Nazwa użytkownika logowania klastra**: klastrów Kafka hello nazwa użytkownika administratora dla hello źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="bbe5a-149">**Hasło logowania klastra**: klastrów Kafka hello hasła użytkownika administratora dla hello źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="bbe5a-150">**Nazwa użytkownika SSH**: klastrów Kafka toocreate użytkownika SSH hello hello źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="bbe5a-151">**Hasło SSH**: klastrów Kafka hello hasła dla użytkownika SSH hello hello źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="bbe5a-152">Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="bbe5a-153">Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="bbe5a-154">Trwa około 20 minut toocreate hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="bbe5a-155">Po utworzeniu hello zasoby zostaną przekierowane tooa bloku hello grupę zasobów, która zawiera hello klastrów i pulpitu nawigacyjnego sieci web.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="bbe5a-157">Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ źródła** i **nazwę BAZOWĄ dest**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="bbe5a-158">Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="bbe5a-159">Tworzenie tematów</span><span class="sxs-lookup"><span data-stu-id="bbe5a-159">Create topics</span></span>

1. <span data-ttu-id="bbe5a-160">Połącz toohello **źródła** klastra przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="bbe5a-161">Zastąp **sshuser** z nazwą użytkownika SSH hello używany podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="bbe5a-162">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello używany podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="bbe5a-163">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bbe5a-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bbe5a-164">Użyj następujących hello polecenia toofind hello dozorcy hosty do klastra źródłowego hello:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="bbe5a-165">Utworzono hello Użyj następującego polecenia tooverify, który hello tematu:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="bbe5a-166">odpowiedź Hello zawiera `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="bbe5a-167">Witaj Użyj następujących informacji o hoście dozorcy hello tooview dla tego (hello **źródła**) klastra:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="bbe5a-168">To polecenie zwróci informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="bbe5a-169">Zapisz te informacje.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-169">Save this information.</span></span> <span data-ttu-id="bbe5a-170">W następnej sekcji hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="bbe5a-171">Konfigurowanie funkcji dublowania</span><span class="sxs-lookup"><span data-stu-id="bbe5a-171">Configure mirroring</span></span>

1. <span data-ttu-id="bbe5a-172">Połącz toohello **docelowego** klastra przy użyciu innej sesji SSH:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="bbe5a-173">Zastąp **sshuser** z nazwą użytkownika SSH hello używany podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="bbe5a-174">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello używany podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="bbe5a-175">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bbe5a-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bbe5a-176">Użyj hello następujące polecenie toocreate `consumer.properties` pliku, który opisuje sposób toocommunicate z hello **źródła** klastra:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="bbe5a-177">Witaj Użyj następującego tekstu jako zawartość hello hello `consumer.properties` pliku:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="bbe5a-178">Zastąp **SOURCE_ZKHOSTS** z hello dozorcy hostuje informacje z hello **źródła** klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="bbe5a-179">Ten plik zawiera opis powitania klienta informacji toouse podczas odczytywania ze źródła hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="bbe5a-180">Aby uzyskać więcej informacji o konfiguracji konsumenta, zobacz [Configs konsumenta](https://kafka.apache.org/documentation#consumerconfigs) na kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="bbe5a-181">toosave hello pliku, użyj **Ctrl + X**, **Y**, a następnie **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="bbe5a-182">Przed skonfigurowaniem producent hello, który komunikuje się z klastrem docelowego hello, należy znaleźć brokera hello hosty dla hello **docelowego** klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="bbe5a-183">Użyj następującego polecenia tooretrieve hello te informacje:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="bbe5a-184">Zastąp `$PASSWORD` z hasłem konta (Administrator) logowania hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="bbe5a-185">Zastąp `$CLUSTERNAME` o nazwie hello hello klastra docelowego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="bbe5a-186">Te polecenia zwracają informacje podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="bbe5a-187">Użyj powitania po toocreate `producer.properties` pliku, który opisuje sposób toocommunicate z hello **docelowego** klastra:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="bbe5a-188">Witaj Użyj następującego tekstu jako zawartość hello hello `producer.properties` pliku:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="bbe5a-189">Zastąp **DEST_BROKERS** hello brokera informacje z poprzedniego kroku hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="bbe5a-190">Aby uzyskać więcej informacji o konfiguracji producenta, zobacz [Configs producent](https://kafka.apache.org/documentation#producerconfigs) na kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="bbe5a-191">Uruchom MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="bbe5a-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="bbe5a-192">Z toohello połączenia SSH hello **docelowego** klastra, użyj powitania po procesie MirrorMaker hello toostart polecenia:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="bbe5a-193">Parametry Hello używana w tym przykładzie są:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="bbe5a-194">**--consumer.config**: Określa plik hello, który zawiera właściwości konsumenta.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="bbe5a-195">Te właściwości są używane toocreate konsumenta odczytująca hello *źródła* Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="bbe5a-196">**--producer.config**: Określa plik hello, który zawiera właściwości producenta.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="bbe5a-197">Te właściwości są używane toocreate producenta, która zapisuje toohello *docelowego* Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="bbe5a-198">**--dozwolonych**: listę tematów, które MirrorMaker replikuje z hello źródła klastra toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="bbe5a-199">**--num.streams**: hello liczba toocreate wątków konsumenta.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="bbe5a-200">Uruchamianie MirrorMaker zwraca informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="bbe5a-201">Z toohello połączenia SSH hello **źródła** klastra, użyj następującego polecenia toostart producent hello i wysyłanie komunikatów toohello tematu:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="bbe5a-202">Zastąp `$PASSWORD` hasłem logowania (Administrator) hello hello źródła klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="bbe5a-203">Zastąp `$CLUSTERNAME` o nazwie hello hello źródła klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="bbe5a-204">Po przyjeździe do pustego wiersza z kursorem, wpisz w kilku wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="bbe5a-205">Ustawienia te są wysyłane toohello tematu na powitania **źródła** klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="bbe5a-206">Na koniec użyj **klawisze Ctrl + C** tooend hello producent procesu.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="bbe5a-207">Z toohello połączenia SSH hello **docelowego** klastra, użyj **klawisze Ctrl + C** hello tooend MirrorMaker procesu.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="bbe5a-208">Następnie użyj hello następujące polecenia tooverify tego hello `testtopic` tematu został utworzony, a dane w temacie hello został toothis replikowanych dublowania:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="bbe5a-209">Zastąp `$PASSWORD` hasłem logowania (Administrator) hello hello klastra docelowego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="bbe5a-210">Zastąp `$CLUSTERNAME` o nazwie hello hello klastra docelowego.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="bbe5a-211">Witaj listę tematów zawiera teraz `testtopic`, który jest tworzony podczas MirrorMaster odzwierciedla hello tematu z docelowym toohello klastra źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="bbe5a-212">wiadomości powitania pobrane z tematu hello są takie same jak został wprowadzony w klastrze źródłowym hello hello.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="bbe5a-213">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="bbe5a-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="bbe5a-214">Ponieważ hello kroków w tym dokumencie Tworzenie zarówno klastrów w hello tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="bbe5a-215">Usunięcie grupy zasobów hello usuwa wszystkie zasoby utworzone, postępując w tym dokumencie, hello Azure Virtual Network i konto magazynu używane przez hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbe5a-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbe5a-216">Next Steps</span></span>

<span data-ttu-id="bbe5a-217">W tym dokumencie przedstawiono sposób toouse MirrorMaker toocreate repliki Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="bbe5a-218">Z Kafka, należy użyć następującego łącza toodiscover hello toowork inne sposoby:</span><span class="sxs-lookup"><span data-stu-id="bbe5a-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="bbe5a-219">[Dokumentację Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) na cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="bbe5a-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="bbe5a-220">Wprowadzenie do Apache Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbe5a-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="bbe5a-221">Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbe5a-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="bbe5a-222">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbe5a-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="bbe5a-223">Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bbe5a-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
