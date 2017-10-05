---
title: Duplikuj tematy Apache Kafka - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak za pomocą funkcji dublowania Apache Kafka Obsługa repliki Kafka w klastrze usługi HDInsight Dublując tematów do dodatkowej klastra."
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
ms.openlocfilehash: e418cb01e1a9168e3662e8d6242903e052b6047b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="e508d-103">Użyj MirrorMaker w celu zreplikowania Apache Kafka tematy z Kafka w usłudze HDInsight (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="e508d-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="e508d-104">Dowiedz się, jak za pomocą funkcji dublowania Apache Kafka replikować tematów do dodatkowej klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="e508d-105">Dublowanie mogą być uruchomione jako ciągły proces wykonywany lub sporadycznie używane jako metody migracji danych z jednego klastra do innego.</span><span class="sxs-lookup"><span data-stu-id="e508d-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="e508d-106">W tym przykładzie dublowania służy do replikowania tematy między dwoma klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e508d-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="e508d-107">Obu klastrach znajdują się w sieci wirtualnej platformy Azure, w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="e508d-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="e508d-108">Dublowanie nie należy traktować jako środek do osiągnięcia odporności na uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="e508d-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="e508d-109">Przesunięcie do elementów w temacie różnią się między klastrami źródłowym i docelowym, więc klienci nie mogą używać dwa zamiennie.</span><span class="sxs-lookup"><span data-stu-id="e508d-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="e508d-110">Jeśli masz obawy odporność na uszkodzenia, należy ustawić replikacji tematami w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="e508d-111">Aby uzyskać więcej informacji, zobacz [wprowadzenie Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e508d-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="e508d-112">Jak działa Kafka dublowania</span><span class="sxs-lookup"><span data-stu-id="e508d-112">How Kafka mirroring works</span></span>

<span data-ttu-id="e508d-113">Dublowania działa przy użyciu narzędzia MirrorMaker (część Apache Kafka) do używać rekordów z tematów w klastrze źródłowym, a następnie utwórz kopię lokalną w klastrze docelowym.</span><span class="sxs-lookup"><span data-stu-id="e508d-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="e508d-114">MirrorMaker używa jednej (lub więcej) *konsumentów* odczytanej z klastra źródłowego i *producent* zapisuje klastra lokalnego (docelowy).</span><span class="sxs-lookup"><span data-stu-id="e508d-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="e508d-115">Na poniższym diagramie przedstawiono proces lustrzane:</span><span class="sxs-lookup"><span data-stu-id="e508d-115">The following diagram illustrates the Mirroring process:</span></span>

![Diagram procesu dublowania](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="e508d-117">Kafka Apache na HDInsight nie zapewniają dostęp do usługi Kafka za pośrednictwem publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="e508d-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="e508d-118">Producenci Kafka lub klienci, którzy muszą być w tej samej sieci wirtualnej platformy Azure jako węzły w klastrze Kafka.</span><span class="sxs-lookup"><span data-stu-id="e508d-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="e508d-119">W tym przykładzie zarówno Kafka źródłowego i docelowego klastrów znajdują się w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e508d-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="e508d-120">Na poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami:</span><span class="sxs-lookup"><span data-stu-id="e508d-120">The following diagram shows how communication flows between the clusters:</span></span>

![Diagram źródłowy i docelowy Kafka klastrów w sieci wirtualnej platformy Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="e508d-122">Klastry źródłowy i docelowy mogą być różne liczby węzłów i partycji, różni się od przesunięcia w tematach również.</span><span class="sxs-lookup"><span data-stu-id="e508d-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="e508d-123">Dublowania przechowuje wartości klucza, który jest używany do partycjonowania, więc na podstawie na klucz jest zachowana kolejność rekordów.</span><span class="sxs-lookup"><span data-stu-id="e508d-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="e508d-124">Dublowanie bariery sieciowe</span><span class="sxs-lookup"><span data-stu-id="e508d-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="e508d-125">Jeśli potrzebujesz duplikatów między klastrami Kafka w różnych sieciach, istnieją następujące dodatkowe zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="e508d-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="e508d-126">**Bram**: sieci musi mieć możliwość komunikacji na poziomie protokołu TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e508d-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="e508d-127">**Rozpoznawanie nazw**: Kafka klastrów w każdej sieci musi być w stanie nawiązać połączenia ze sobą przy użyciu nazwy hostów.</span><span class="sxs-lookup"><span data-stu-id="e508d-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="e508d-128">Może to wymagać serwer systemu nazw domen (DNS) w każdej sieci, która jest skonfigurowana do przesyłania żądań do innej sieci.</span><span class="sxs-lookup"><span data-stu-id="e508d-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="e508d-129">Podczas tworzenia sieci wirtualnej platformy Azure, zamiast używać automatycznego DNS podany w sieci, należy określić niestandardowy serwer DNS i adres IP serwera.</span><span class="sxs-lookup"><span data-stu-id="e508d-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="e508d-130">Po utworzeniu sieci wirtualnej można następnie utwórz maszynę wirtualną platformy Azure, który korzysta z tego adresu IP, a następnie zainstalować i skonfigurować oprogramowanie DNS na nim.</span><span class="sxs-lookup"><span data-stu-id="e508d-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="e508d-131">Tworzenie i konfigurowanie niestandardowych serwera DNS przed zainstalowaniem usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e508d-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="e508d-132">Brak konieczności dodatkowej konfiguracji dla usługi HDInsight użyć serwera DNS skonfigurowanego dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e508d-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="e508d-133">Aby uzyskać więcej informacji na łącząca dwie sieci wirtualne platformy Azure, zobacz [skonfigurować połączenia do wirtualnymi](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e508d-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="e508d-134">Tworzenie Kafka klastrów</span><span class="sxs-lookup"><span data-stu-id="e508d-134">Create Kafka clusters</span></span>

<span data-ttu-id="e508d-135">Podczas tworzenia sieci wirtualnej platformy Azure i Kafka klastrów ręcznie, łatwiej jest użyć szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e508d-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="e508d-136">Wykonaj następujące kroki, aby wdrożyć sieci wirtualnej platformy Azure i dwa klastry Kafka do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e508d-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="e508d-137">Poniższy przycisk umożliwia logowanie do platformy Azure i otwórz szablon w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e508d-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="e508d-138">Szablon usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="e508d-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="e508d-139">Aby zapewnić dostępność platformy Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzy węzły procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e508d-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="e508d-140">Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e508d-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="e508d-141">Użyj poniższych informacji, aby wypełnić wpisy na **wdrożenie niestandardowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="e508d-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="e508d-143">**Grupa zasobów**: Utwórz grupę lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="e508d-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="e508d-144">Ta grupa zawiera klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e508d-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="e508d-145">**Lokalizacja**: Wybierz lokalizację lokalizacji geograficznej blisko.</span><span class="sxs-lookup"><span data-stu-id="e508d-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="e508d-146">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="e508d-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="e508d-147">Na przykład wprowadzenie **hdi** tworzy klastry o nazwie **hdi źródła** i **dest hdi**.</span><span class="sxs-lookup"><span data-stu-id="e508d-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="e508d-148">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora na serwerze źródłowym i docelowym Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="e508d-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="e508d-149">**Hasło logowania klastra**: klastrów Kafka hasła użytkownika administratora na serwerze źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="e508d-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="e508d-150">**Nazwa użytkownika SSH**: użytkownika SSH do utworzenia na serwerze źródłowym i docelowym Kafka klastrów.</span><span class="sxs-lookup"><span data-stu-id="e508d-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="e508d-151">**Hasło SSH**: klastrów Kafka hasło użytkownika SSH na serwerze źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="e508d-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="e508d-152">Odczyt **warunków i postanowień**, a następnie wybierz **akceptuję warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="e508d-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="e508d-153">Ponadto sprawdź **Przypnij do pulpitu nawigacyjnego** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="e508d-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e508d-154">Tworzenie klastrów trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="e508d-154">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="e508d-155">Po utworzeniu zasoby są przekierowywane do bloku grupy zasobów, zawierającą klastrów i pulpitu nawigacyjnego sieci web.</span><span class="sxs-lookup"><span data-stu-id="e508d-155">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Bloku grupy zasobów dla sieci wirtualnej i klastrów](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e508d-157">Należy zauważyć, że nazwy klastrów usługi HDInsight są **nazwę BAZOWĄ źródła** i **nazwę BAZOWĄ dest**, gdzie nazwę BAZOWĄ jest podana nazwa do szablonu.</span><span class="sxs-lookup"><span data-stu-id="e508d-157">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="e508d-158">Te nazwy można użyć w kolejnych krokach, podczas nawiązywania połączenia z klastrów.</span><span class="sxs-lookup"><span data-stu-id="e508d-158">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="e508d-159">Tworzenie tematów</span><span class="sxs-lookup"><span data-stu-id="e508d-159">Create topics</span></span>

1. <span data-ttu-id="e508d-160">Połączyć się z **źródła** klastra przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="e508d-160">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="e508d-161">Zastąp **sshuser** z nazwą użytkownika SSH używany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-161">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="e508d-162">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej używany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-162">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="e508d-163">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e508d-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e508d-164">Aby znaleźć hosty dozorcy dla źródłowego klastra, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="e508d-164">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with the password for the cluster.

    Replace `$CLUSTERNAME` with the name of the source cluster.

3. To create a topic named `testtopic`, use the following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="e508d-165">Aby sprawdzić, czy temat został utworzony, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e508d-165">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="e508d-166">Odpowiedź zawiera `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="e508d-166">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="e508d-167">Umożliwia wyświetlanie informacji o hoście dozorcy tego następujące ( **źródła**) klastra:</span><span class="sxs-lookup"><span data-stu-id="e508d-167">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="e508d-168">Zwróci ono informacje podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e508d-168">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="e508d-169">Zapisz te informacje.</span><span class="sxs-lookup"><span data-stu-id="e508d-169">Save this information.</span></span> <span data-ttu-id="e508d-170">Jest on używany w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e508d-170">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="e508d-171">Konfigurowanie funkcji dublowania</span><span class="sxs-lookup"><span data-stu-id="e508d-171">Configure mirroring</span></span>

1. <span data-ttu-id="e508d-172">Połączyć się z **docelowego** klastra przy użyciu innej sesji SSH:</span><span class="sxs-lookup"><span data-stu-id="e508d-172">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="e508d-173">Zastąp **sshuser** z nazwą użytkownika SSH używany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-173">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="e508d-174">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej używany podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-174">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="e508d-175">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e508d-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e508d-176">Użyj następującego polecenia, aby utworzyć `consumer.properties` pliku, który opisuje sposób komunikowania się z **źródła** klastra:</span><span class="sxs-lookup"><span data-stu-id="e508d-176">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="e508d-177">Skorzystaj z poniższego tekstu jako zawartość `consumer.properties` pliku:</span><span class="sxs-lookup"><span data-stu-id="e508d-177">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="e508d-178">Zastąp **SOURCE_ZKHOSTS** dozorcy informacjami hostów z **źródła** klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-178">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="e508d-179">Ten plik zawiera opis informacji konsumentów do użycia podczas odczytu ze źródłowej Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-179">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="e508d-180">Aby uzyskać więcej informacji o konfiguracji konsumenta, zobacz [Configs konsumenta](https://kafka.apache.org/documentation#consumerconfigs) na kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="e508d-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="e508d-181">Aby zapisać plik, użyj **Ctrl + X**, **Y**, a następnie **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e508d-181">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="e508d-182">Przed skonfigurowaniem producenta, która komunikuje się z klastrem docelowym, należy znaleźć brokera hosty dla **docelowego** klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-182">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="e508d-183">Aby pobrać te informacje, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="e508d-183">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="e508d-184">Zastąp `$PASSWORD` z hasłem konta (Administrator) logowania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-184">Replace `$PASSWORD` with the login account (admin) password for the cluster.</span></span>

    <span data-ttu-id="e508d-185">Zastąp `$CLUSTERNAME` o nazwie klastra docelowego.</span><span class="sxs-lookup"><span data-stu-id="e508d-185">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="e508d-186">Te polecenia zwrócone informacje podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="e508d-186">These commands return information similar to the following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="e508d-187">Umożliwia tworzenie następujących `producer.properties` pliku, który opisuje sposób komunikowania się z **docelowego** klastra:</span><span class="sxs-lookup"><span data-stu-id="e508d-187">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="e508d-188">Skorzystaj z poniższego tekstu jako zawartość `producer.properties` pliku:</span><span class="sxs-lookup"><span data-stu-id="e508d-188">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="e508d-189">Zastąp **DEST_BROKERS** brokera informacje z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="e508d-189">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="e508d-190">Aby uzyskać więcej informacji o konfiguracji producenta, zobacz [Configs producent](https://kafka.apache.org/documentation#producerconfigs) na kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="e508d-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="e508d-191">Uruchom MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="e508d-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="e508d-192">Połączenie SSH **docelowego** klastra, użyj następującego polecenia, aby rozpocząć proces MirrorMaker:</span><span class="sxs-lookup"><span data-stu-id="e508d-192">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="e508d-193">Parametry używane w tym przykładzie są:</span><span class="sxs-lookup"><span data-stu-id="e508d-193">The parameters used in this example are:</span></span>

    * <span data-ttu-id="e508d-194">**--consumer.config**: Określa plik, który zawiera właściwości konsumenta.</span><span class="sxs-lookup"><span data-stu-id="e508d-194">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="e508d-195">Te właściwości są używane do tworzenia konsumenta, która odczytuje z *źródła* Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-195">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="e508d-196">**--producer.config**: Określa plik, który zawiera właściwości producenta.</span><span class="sxs-lookup"><span data-stu-id="e508d-196">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="e508d-197">Te właściwości są używane do tworzenia producenta, która zapisuje *docelowego* Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-197">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="e508d-198">**--dozwolonych**: listę tematów, które MirrorMaker replikuje dane z klastra źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="e508d-198">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="e508d-199">**--num.streams**: liczba wątków odbiorców do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="e508d-199">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="e508d-200">Uruchamianie MirrorMaker zwraca informacje podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e508d-200">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="e508d-201">Połączenie SSH **źródła** klastra, użyj następującego polecenia, aby uruchomić producenta i wysyłanie komunikatów do tematu:</span><span class="sxs-lookup"><span data-stu-id="e508d-201">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="e508d-202">Zastąp `$PASSWORD` przy użyciu hasła logowania (Administrator) dla źródłowego klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-202">Replace `$PASSWORD` with the login (admin) password for the source cluster.</span></span>

    <span data-ttu-id="e508d-203">Zastąp `$CLUSTERNAME` o nazwie klastra źródłowego.</span><span class="sxs-lookup"><span data-stu-id="e508d-203">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span>

     <span data-ttu-id="e508d-204">Po przyjeździe do pustego wiersza z kursorem, wpisz w kilku wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="e508d-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="e508d-205">Ustawienia te są wysyłane do tematu **źródła** klastra.</span><span class="sxs-lookup"><span data-stu-id="e508d-205">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="e508d-206">Na koniec użyj **klawisze Ctrl + C** można zakończyć procesu producenta.</span><span class="sxs-lookup"><span data-stu-id="e508d-206">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="e508d-207">Połączenie SSH **docelowego** klastra, użyj **klawisze Ctrl + C** można zakończyć procesu MirrorMaker.</span><span class="sxs-lookup"><span data-stu-id="e508d-207">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="e508d-208">Następnie użyj następujących poleceń, aby sprawdzić, czy `testtopic` tematu został utworzony i danych w temacie zostało zreplikowane do dublowania:</span><span class="sxs-lookup"><span data-stu-id="e508d-208">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="e508d-209">Zastąp `$PASSWORD` hasłem logowania (Administrator) do klastra docelowego.</span><span class="sxs-lookup"><span data-stu-id="e508d-209">Replace `$PASSWORD` with the login (admin) password for the destination cluster.</span></span>

    <span data-ttu-id="e508d-210">Zastąp `$CLUSTERNAME` o nazwie klastra docelowego.</span><span class="sxs-lookup"><span data-stu-id="e508d-210">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="e508d-211">Lista tematów zawiera teraz `testtopic`, który jest tworzony podczas MirrorMaster odzwierciedla tematu z klastra źródłowego do docelowego.</span><span class="sxs-lookup"><span data-stu-id="e508d-211">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="e508d-212">Wiadomości pobierane z tematu są takie same, jak został wprowadzony w klastrze źródłowym.</span><span class="sxs-lookup"><span data-stu-id="e508d-212">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="e508d-213">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="e508d-213">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e508d-214">Ponieważ kroki opisane w tym dokumencie utworzyć obu klastrów w tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e508d-214">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="e508d-215">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów utworzone przez tego dokumentu, Azure Virtual Network i konto magazynu używane przez klaster.</span><span class="sxs-lookup"><span data-stu-id="e508d-215">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e508d-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e508d-216">Next Steps</span></span>

<span data-ttu-id="e508d-217">W tym dokumencie przedstawiono sposób umożliwiają utworzenie repliki klastra Kafka MirrorMaker.</span><span class="sxs-lookup"><span data-stu-id="e508d-217">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="e508d-218">Aby dowiedzieć się, inne metody pracy z Kafka, użyj następujących łączy:</span><span class="sxs-lookup"><span data-stu-id="e508d-218">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="e508d-219">[Dokumentację Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) na cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="e508d-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="e508d-220">Wprowadzenie do Apache Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e508d-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="e508d-221">Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e508d-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="e508d-222">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e508d-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="e508d-223">Nawiązywanie połączenia z platformą Kafka za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e508d-223">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
