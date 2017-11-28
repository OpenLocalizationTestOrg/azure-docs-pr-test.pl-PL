---
title: "Przykłady aaaStorm starter Apache Storm w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak analizy danych big data toodo i przetwarzania danych w czasie rzeczywistym za pomocą platformy Apache Storm i hello przykłady z projektu storm starter w usłudze HDInsight."
keywords: "projekt Storm Starter, przykład z platformy Apache Storm"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="83b8e-104">Wprowadzenie do Apache Storm w usłudze HDInsight przy użyciu hello storm-starter przykłady</span><span class="sxs-lookup"><span data-stu-id="83b8e-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="83b8e-105">Dowiedz się, jak toouse Apache Storm w usłudze HDInsight przy użyciu hello przykłady z projektu storm starter.</span><span class="sxs-lookup"><span data-stu-id="83b8e-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="83b8e-106">Apache Storm to skalowalny, odporny na błędy, rozproszony system obliczeniowy działający w czasie rzeczywistym do przetwarzania strumieni danych.</span><span class="sxs-lookup"><span data-stu-id="83b8e-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="83b8e-107">Dzięki platformie Storm w usłudze Azure HDInsight można utworzyć oparty na chmurze klaster Storm do wykonywania analizy danych big data w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="83b8e-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83b8e-108">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="83b8e-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="83b8e-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="83b8e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83b8e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83b8e-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="83b8e-111">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="83b8e-111">**An Azure subscription**.</span></span> <span data-ttu-id="83b8e-112">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="83b8e-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="83b8e-113">**Znajomość protokołów SSH i SCP**.</span><span class="sxs-lookup"><span data-stu-id="83b8e-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="83b8e-114">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="83b8e-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="83b8e-115">Tworzenie klastra Storm</span><span class="sxs-lookup"><span data-stu-id="83b8e-115">Create a Storm cluster</span></span>

<span data-ttu-id="83b8e-116">Użyj hello następujące kroki toocreate platformy Storm w klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="83b8e-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="83b8e-117">Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy**, **analizy i analiza**, a następnie wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="83b8e-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Tworzenie klastra usługi HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="83b8e-119">Z hello **podstawy** bloku, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="83b8e-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="83b8e-120">**Nazwa klastra**: Nazwa hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83b8e-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="83b8e-121">**Subskrypcja**: Wybierz hello toouse subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="83b8e-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="83b8e-122">**Nazwa użytkownika logowania klastra** i **hasło logowania klastra**: hello logowania podczas uzyskiwania dostępu do klastra hello za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83b8e-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="83b8e-123">Korzystania z tych usług tooaccess poświadczeń, takich jak hello Interfejsu sieci Web Ambari lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="83b8e-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="83b8e-124">**Secure Shell (SSH) username**: hello logowania używany podczas uzyskiwania dostępu do klastra hello za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="83b8e-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="83b8e-125">Domyślnie jest hello takie samo jak hasło logowania klastra hello hello hasła.</span><span class="sxs-lookup"><span data-stu-id="83b8e-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="83b8e-126">**Grupa zasobów**: hello klastra hello toocreate grupy zasobów w.</span><span class="sxs-lookup"><span data-stu-id="83b8e-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="83b8e-127">**Lokalizacja**: hello regionu Azure toocreate hello klastra w.</span><span class="sxs-lookup"><span data-stu-id="83b8e-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Wybieranie subskrypcji](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="83b8e-129">Wybierz **typ klastra**, a następnie hello ustaw następujące wartości na powitania **konfiguracji klastra** bloku:</span><span class="sxs-lookup"><span data-stu-id="83b8e-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="83b8e-130">**Typ klastra**: Storm</span><span class="sxs-lookup"><span data-stu-id="83b8e-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="83b8e-131">**System operacyjny**: Linux</span><span class="sxs-lookup"><span data-stu-id="83b8e-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="83b8e-132">**Wersja**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="83b8e-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="83b8e-133">**Warstwa klastra**: Standardowa</span><span class="sxs-lookup"><span data-stu-id="83b8e-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="83b8e-134">Na koniec użyj hello **wybierz** przycisk toosave ustawienia.</span><span class="sxs-lookup"><span data-stu-id="83b8e-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Wybieranie typu klastra](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="83b8e-136">Po wybraniu typu klastra hello, użyj hello __wybierz__ tooset hello klastra typ przycisku.</span><span class="sxs-lookup"><span data-stu-id="83b8e-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="83b8e-137">Następnie użyj hello __dalej__ przycisk toofinish podstawową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="83b8e-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="83b8e-138">Z hello **magazynu** bloku, wybierz lub Utwórz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="83b8e-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="83b8e-139">Hello czynności w tym dokumencie pozostaw hello innych pól w tym bloku na powitania wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="83b8e-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="83b8e-140">Użyj hello __dalej__ przycisk toosave magazynu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="83b8e-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Ustaw hello ustawienia konta magazynu dla usługi HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="83b8e-142">Z hello **Podsumowanie** bloku, Przejrzyj konfigurację hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="83b8e-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="83b8e-143">Użyj hello __Edytuj__ łączy toochange wszystkie ustawienia, które są nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="83b8e-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="83b8e-144">Na koniec użyj the__Create__ przycisk toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="83b8e-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Podsumowanie konfiguracji klastra](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="83b8e-146">Może potrwać too20 minut toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="83b8e-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="83b8e-147">Uruchamianie przykładu z projektu Storm Starter w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="83b8e-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="83b8e-148">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="83b8e-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="83b8e-149">Jeśli użyto toosecure hasło konta użytkownika SSH, to zostanie wyświetlony monit o tooenter go.</span><span class="sxs-lookup"><span data-stu-id="83b8e-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="83b8e-150">Jeśli używasz klucza publicznego, należy posłużyć hello `-i` toospecify parametru hello odpowiedniego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="83b8e-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="83b8e-151">Na przykład `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="83b8e-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="83b8e-152">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="83b8e-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="83b8e-153">Użyj następującego polecenia toostart przykładową topologię hello:</span><span class="sxs-lookup"><span data-stu-id="83b8e-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="83b8e-154">W poprzednich wersjach usługi HDInsight, nazwa klasy hello topologii hello jest `storm.starter.WordCountTopology` zamiast `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="83b8e-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="83b8e-155">To polecenie uruchamia hello przykładową topologię WordCount w klastrze hello o przyjaznej nazwie "wordcount".</span><span class="sxs-lookup"><span data-stu-id="83b8e-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="83b8e-156">Losowo generuje on zdań i hello liczby wystąpień poszczególnych wyrazów w zdaniach hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="83b8e-157">Podczas przesyłania własnego klastra toohello topologie, należy najpierw skopiować plik jar hello zawierający hello klastra przed użyciem hello `storm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="83b8e-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="83b8e-158">Użyj hello `scp` pliku hello toocopy polecenia.</span><span class="sxs-lookup"><span data-stu-id="83b8e-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="83b8e-159">Na przykład: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="83b8e-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="83b8e-160">przykład Witaj WordCount i inne przykłady storm-starter znajdują się już w klastrze na `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="83b8e-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="83b8e-161">Jeśli interesuje Cię wyświetlanie źródła hello hello storm-starter przykłady, można znaleźć kod hello na [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="83b8e-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="83b8e-162">Ten link dotyczy platformy Storm 1.1.x, która jest dostarczana z usługą HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="83b8e-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="83b8e-163">W przypadku innych wersji systemu Storm, użyj hello __gałęzi__ przycisk u góry hello tooselect strony hello z innej wersji systemu Storm.</span><span class="sxs-lookup"><span data-stu-id="83b8e-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="83b8e-164">Monitor hello topologii</span><span class="sxs-lookup"><span data-stu-id="83b8e-164">Monitor hello topology</span></span>

<span data-ttu-id="83b8e-165">Hello interfejsu użytkownika platformy Storm udostępnia interfejs sieci web do pracy z uruchomionymi topologiami i znajduje się w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83b8e-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="83b8e-166">Użyj następujących topologii hello toomonitor czynności przy użyciu interfejsu użytkownika platformy Storm hello hello:</span><span class="sxs-lookup"><span data-stu-id="83b8e-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="83b8e-167">Witaj toodisplay interfejsu użytkownika platformy Storm, otwórz toohttps://CLUSTERNAME.azurehdinsight.net/stormui przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="83b8e-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="83b8e-168">Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="83b8e-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="83b8e-169">Jeśli pojawi się monit tooprovide nazwy użytkownika i hasła, wprowadź hello administratora klastra (admin) i hasło użyte podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="83b8e-170">W obszarze **podsumowanie topologii**, wybierz pozycję hello **wordcount** wpisu w hello **nazwa** kolumny.</span><span class="sxs-lookup"><span data-stu-id="83b8e-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="83b8e-171">Informacje o topologii hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="83b8e-171">Information about hello topology is displayed.</span></span>

    ![Pulpit nawigacyjny platformy Storm z informacjami o topologii przykładu z projektu Storm Starter o nazwie WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="83b8e-173">Ta strona zawiera hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="83b8e-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="83b8e-174">**Statystyka topologii** — podstawowe informacje na temat wydajności topologii hello podzielone na okna czasowe.</span><span class="sxs-lookup"><span data-stu-id="83b8e-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="83b8e-175">Wybór określonego okna zmiany hello czas okna czasowego informacji wyświetlanych w innych sekcjach strony hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="83b8e-176">**Spouts** — podstawowe informacje o elementach spout, łącznie hello ostatnim błędem zwróconym przez poszczególne elementy spout.</span><span class="sxs-lookup"><span data-stu-id="83b8e-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="83b8e-177">**Bolts** (Elementy bolt) — podstawowe informacje o elementach bolt.</span><span class="sxs-lookup"><span data-stu-id="83b8e-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="83b8e-178">**Topologia konfiguracji** — szczegółowe informacje o konfiguracji topologii hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="83b8e-179">Ta strona zawiera również akcje, które można podjąć w topologii hello:</span><span class="sxs-lookup"><span data-stu-id="83b8e-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="83b8e-180">**Activate** (Aktywuj) — wznowienie przetwarzania dezaktywowanej topologii.</span><span class="sxs-lookup"><span data-stu-id="83b8e-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="83b8e-181">**Deactivate** (Dezaktywuj) — wstrzymanie uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="83b8e-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="83b8e-182">**Rebalance** — można dostosować równoległość hello hello topologii.</span><span class="sxs-lookup"><span data-stu-id="83b8e-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="83b8e-183">Po zmianie hello liczby węzłów w klastrze hello, należy przeprowadzić ponowne równoważenie uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="83b8e-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="83b8e-184">Ponowne równoważenie można dostosować równoległość toocompensate hello zwiększonej/zmniejszonej liczby węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="83b8e-185">Aby uzyskać więcej informacji, zobacz [opis hello równoległości topologii Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="83b8e-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="83b8e-186">**Kasowanie** -kończy topologii Storm po hello określony limit czasu.</span><span class="sxs-lookup"><span data-stu-id="83b8e-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="83b8e-187">Na tej stronie, wybierz pozycję z hello **Spouts** lub **Bolts** sekcji.</span><span class="sxs-lookup"><span data-stu-id="83b8e-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="83b8e-188">Zostaną wyświetlone informacje o hello wybranego składnika.</span><span class="sxs-lookup"><span data-stu-id="83b8e-188">Information about hello selected component is displayed.</span></span>

    ![Pulpit nawigacyjny Storm z informacjami o wybranych składnikach.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="83b8e-190">Ta strona wyświetla hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="83b8e-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="83b8e-191">**Spout/Bolt stats** — podstawowe informacje na temat wydajności składników hello podzielone na okna czasowe.</span><span class="sxs-lookup"><span data-stu-id="83b8e-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="83b8e-192">Wybór określonego okna zmiany hello czas okna czasowego informacji wyświetlanych w innych sekcjach strony hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="83b8e-193">**Wprowadź statystykę** (tylko dla elementów bolt) — informacje na temat składników, które tworzą dane używane przez hello bolt.</span><span class="sxs-lookup"><span data-stu-id="83b8e-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="83b8e-194">**Output stats** (Statystyki danych wyjściowych) — informacje na temat danych emitowanych przez dany element bolt.</span><span class="sxs-lookup"><span data-stu-id="83b8e-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="83b8e-195">**Executors** (Wykonawcy) — informacje dotyczące wystąpień danego składnika.</span><span class="sxs-lookup"><span data-stu-id="83b8e-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="83b8e-196">**Errors** (Błędy) — błędy generowane przez dany składnik.</span><span class="sxs-lookup"><span data-stu-id="83b8e-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="83b8e-197">Podczas wyświetlania szczegółowych informacji hello spout lub bolt, zaznacz wpis hello **portu** kolumny w hello **modułów** sekcji Szczegóły tooview dla określonego wystąpienia hello składnika.</span><span class="sxs-lookup"><span data-stu-id="83b8e-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="83b8e-198">W tym przykładzie hello word **siedmiu** wystąpił 1493957 razy.</span><span class="sxs-lookup"><span data-stu-id="83b8e-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="83b8e-199">Ta liczba jest ile razy napotkano word powitania od momentu uruchomienia tej topologii.</span><span class="sxs-lookup"><span data-stu-id="83b8e-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="83b8e-200">Zatrzymywanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="83b8e-200">Stop hello topology</span></span>

<span data-ttu-id="83b8e-201">Zwraca toohello **podsumowanie topologii** dla topologii WordCount hello, a następnie wybierz hello **Kill** przycisk od hello **akcje topologii** sekcji.</span><span class="sxs-lookup"><span data-stu-id="83b8e-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="83b8e-202">Po wyświetleniu monitu wprowadź 10 hello toowait sekund przed zatrzymaniem topologii hello.</span><span class="sxs-lookup"><span data-stu-id="83b8e-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="83b8e-203">Po upływie okresu czasu hello hello topologia nie będzie już wyświetlany podczas odwiedzania hello **interfejsu użytkownika platformy Storm** sekcji hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="83b8e-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="83b8e-204">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="83b8e-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="83b8e-205">W razie problemów podczas tworzenia klastra usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="83b8e-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="83b8e-206"><a id="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83b8e-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="83b8e-207">W tym samouczku platformy Apache Storm znasz już podstawy hello pracy z systemu Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83b8e-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="83b8e-208">Następnie Dowiedz się, jak za[topologie oparte na opracowanie Java za pomocą programu Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="83b8e-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="83b8e-209">Jeśli znasz już opracowywania topologii opartych na języku Java i chcesz toodeploy istniejących tooHDInsight topologii, zobacz [wdrażanie topologii Apache Storm w usłudze HDInsight oraz zarządzania nimi](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="83b8e-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="83b8e-210">Jeśli jesteś deweloperem platformy .NET, możesz tworzyć topologie C# lub hybrydowe topologie C#/Java za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83b8e-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="83b8e-211">Aby uzyskać więcej informacji na ten temat, zobacz [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu narzędzi Hadoop dla programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="83b8e-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="83b8e-212">Na przykład topologie, które mogą być używane z systemu Storm w usłudze HDInsight, zobacz temat hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="83b8e-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="83b8e-213">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="83b8e-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
