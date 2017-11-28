---
title: "aaaInstall Jupyter lokalnie & połączenia klastra Spark w usłudze HDInsight Azure tooan | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak notesu Jupyter tooinstall lokalnie na komputerze i podłącz go tooan klastra Apache Spark w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="12172-103">Zainstaluj notesu Jupyter na komputerze i połącz tooApache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="12172-104">W tym artykule dowiesz się, jak notesu Jupyter tooinstall, z hello PySpark niestandardowych (w przypadku języka Python) i jądra Spark (na języku Scala) z Spark magic i Połącz z klastrem usługi HDInsight tooan notesu hello.</span><span class="sxs-lookup"><span data-stu-id="12172-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="12172-105">Może istnieć wiele przyczyn tooinstall Jupyter na komputerze lokalnym i mogą być również pewne wyzwania.</span><span class="sxs-lookup"><span data-stu-id="12172-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="12172-106">Aby uzyskać więcej informacji, zobacz sekcję hello [Dlaczego należy zainstalować oprogramowania Jupyter na tym komputerze](#why-should-i-install-jupyter-on-my-computer) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="12172-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="12172-107">Istnieją trzy kroki klucza instalowania Jupyter i hello Spark magic na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="12172-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="12172-108">Zainstaluj notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="12172-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="12172-109">Instalowanie hello PySpark i jądra Spark przy użyciu hello Spark magic</span><span class="sxs-lookup"><span data-stu-id="12172-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="12172-110">Skonfiguruj tooaccess magic Spark klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="12172-111">Aby uzyskać więcej informacji o niestandardowych jądra hello i magic Spark hello dostępne dla notesu Jupyter w klastrze z klastrem usługi HDInsight, zobacz [jądra dostępne dla notesu Jupyter klastrze Apache Spark w systemie Linux klastrów HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="12172-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12172-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="12172-112">Prerequisites</span></span>
<span data-ttu-id="12172-113">Hello wymagania wstępne wymienione w tym miejscu nie dotyczą instalowania Jupyter.</span><span class="sxs-lookup"><span data-stu-id="12172-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="12172-114">Są to łączącego hello Jupyter notebook tooan HDInsight klastra po zainstalowaniu hello notesu.</span><span class="sxs-lookup"><span data-stu-id="12172-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="12172-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12172-115">An Azure subscription.</span></span> <span data-ttu-id="12172-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="12172-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="12172-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12172-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="12172-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="12172-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="12172-119">Zainstaluj na tym komputerze notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="12172-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="12172-120">Python należy zainstalować przed zainstalowaniem notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="12172-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="12172-121">Zarówno Python i Jupyter są dostępne jako część hello [Anaconda dystrybucji](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="12172-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="12172-122">Po zainstalowaniu Anaconda, należy zainstalować dystrybucji języka Python.</span><span class="sxs-lookup"><span data-stu-id="12172-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="12172-123">Po zainstalowaniu Anaconda, możesz dodać hello Jupyter instalacji za pomocą odpowiednich poleceń.</span><span class="sxs-lookup"><span data-stu-id="12172-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="12172-124">Pobierz hello [Instalator Anaconda](https://www.continuum.io/downloads) dla platformy i hello uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="12172-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="12172-125">Podczas uruchomiony Kreator instalacji hello upewnij się, że wybierz zmiennej PATH tooyour Anaconda tooadd hello opcji.</span><span class="sxs-lookup"><span data-stu-id="12172-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="12172-126">Uruchom następujące polecenie tooinstall Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="12172-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="12172-127">Aby uzyskać więcej informacji na temat instalowania Jupyter, zobacz [Jupyter instalowanie przy użyciu Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="12172-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="12172-128">Zainstaluj jądra hello i Spark magic</span><span class="sxs-lookup"><span data-stu-id="12172-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="12172-129">Aby uzyskać instrukcje dotyczące sposobu tooinstall hello Spark magic, hello PySpark i jądra Spark, wykonaj te instrukcje instalacji hello hello [dokumentacji sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="12172-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="12172-130">Hello pierwszy krok w dokumentacji magic Spark hello prośba tooinstall Spark magic.</span><span class="sxs-lookup"><span data-stu-id="12172-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="12172-131">Zastąp hello następujące polecenia, w zależności od wersji hello hello klastra usługi HDInsight, którą będzie łączyć się tym pierwszym etapem hello łącza.</span><span class="sxs-lookup"><span data-stu-id="12172-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="12172-132">Po wykonaniu tej wykonaj pozostałe kroki opisane w dokumentacji magic Spark hello hello.</span><span class="sxs-lookup"><span data-stu-id="12172-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="12172-133">Jeśli chcesz tooinstall hello różnych jądra, należy wykonać krok 3 w hello sekcji instrukcje instalacji magic Spark.</span><span class="sxs-lookup"><span data-stu-id="12172-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="12172-134">W przypadku klastrów v3.4 należy zainstalować sparkmagic 0.2.3, wykonując`pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="12172-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="12172-135">W przypadku klastrów w wersji 3.5 i v3.6 należy zainstalować sparkmagic 0.11.2, wykonując`pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="12172-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="12172-136">Konfigurowanie klastra Spark tooHDInsight magic tooconnect Spark</span><span class="sxs-lookup"><span data-stu-id="12172-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="12172-137">W tej sekcji skonfigurujesz hello magic Spark, zainstalowanej wcześniejszej tooconnect tooan klastra Apache Spark musi już utworzone w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12172-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="12172-138">Hello informacje o konfiguracji Jupyter zazwyczaj znajduje się w katalogu macierzystego hello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="12172-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="12172-139">toolocate katalogu macierzystego na dowolnej platformie systemu operacyjnego hello wpisz następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="12172-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="12172-140">Uruchom powłokę Python hello.</span><span class="sxs-lookup"><span data-stu-id="12172-140">Start hello Python shell.</span></span> <span data-ttu-id="12172-141">W oknie polecenia wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="12172-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="12172-142">Na hello powłoki Python wprowadź następujące polecenie toofind poza katalogiem macierzystym hello hello.</span><span class="sxs-lookup"><span data-stu-id="12172-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="12172-143">Przejdź do katalogu macierzystego toohello i Utwórz folder o nazwie **.sparkmagic** Jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="12172-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="12172-144">W folderze hello, Utwórz plik o nazwie **config.json** i Dodaj powitania po fragment kodu JSON wewnątrz niej.</span><span class="sxs-lookup"><span data-stu-id="12172-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="12172-145">SUBSTITUTE **{USERNAME}**, **{CLUSTERDNSNAME}**, i **{BASE64ENCODEDPASSWORD}** z odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="12172-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="12172-146">Liczba narzędzia w ulubionych języka programowania lub zaszyfrowanych haseł online toogenerate base64 służy do rzeczywistego hasła.</span><span class="sxs-lookup"><span data-stu-id="12172-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="12172-147">Konfigurowanie ustawień praw pulsu hello w `config.json`.</span><span class="sxs-lookup"><span data-stu-id="12172-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="12172-148">Należy dodać te ustawienia na powitania sam poziom jako hello `kernel_python_credentials` i `kernel_scala_credentials` wstawki programu dodane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="12172-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="12172-149">Na przykład, w jaki sposób i gdzie tooadd hello ustawienia pulsu, zobacz [config.json próbki](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="12172-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="12172-150">Aby uzyskać `sparkmagic 0.2.3` (klastrów v3.4), obejmują:</span><span class="sxs-lookup"><span data-stu-id="12172-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="12172-151">Aby uzyskać `sparkmagic 0.11.2` (klastrów w wersji 3.5 i v3.6), obejmują:</span><span class="sxs-lookup"><span data-stu-id="12172-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="12172-152">Tooensure nie przedostają sesji są wysyłane impulsy.</span><span class="sxs-lookup"><span data-stu-id="12172-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="12172-153">Gdy komputer przestanie toosleep lub jest wyłączony, pulsu hello nie są wysyłane, co w hello sesji jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="12172-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="12172-154">V3.4 klastrów, w razie potrzeby toodisable to zachowanie można ustawić hello Livy config `livy.server.interactive.heartbeat.timeout` zbyt`0` z hello interfejsu użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="12172-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="12172-155">Dla klastrów w wersji 3.5 Jeśli konfiguracja hello 3.5 powyżej, nie należy ustawiać hello sesji nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="12172-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="12172-156">Uruchom Jupyter.</span><span class="sxs-lookup"><span data-stu-id="12172-156">Start Jupyter.</span></span> <span data-ttu-id="12172-157">Następujące polecenie w wierszu polecenia hello hello użycia.</span><span class="sxs-lookup"><span data-stu-id="12172-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="12172-158">Sprawdź, czy możesz połączyć toohello klastra za pomocą notesu Jupyter hello i czy za pomocą magic Spark hello dostępne hello jądra.</span><span class="sxs-lookup"><span data-stu-id="12172-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="12172-159">Wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="12172-159">Perform hello following steps.</span></span>

    <span data-ttu-id="12172-160">a.</span><span class="sxs-lookup"><span data-stu-id="12172-160">a.</span></span> <span data-ttu-id="12172-161">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="12172-161">Create a new notebook.</span></span> <span data-ttu-id="12172-162">W prawym górnym rogu powitania kliknij **nowy**.</span><span class="sxs-lookup"><span data-stu-id="12172-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="12172-163">Powinny pojawić się hello domyślnego jądra **Python2** i Witaj dwie nowe jądra, których można zainstalować **PySpark** i **Spark**.</span><span class="sxs-lookup"><span data-stu-id="12172-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="12172-164">Kliknij przycisk **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="12172-164">Click **PySpark**.</span></span>

    <span data-ttu-id="12172-165">![Jądra w notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "jądra w notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="12172-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="12172-166">b.</span><span class="sxs-lookup"><span data-stu-id="12172-166">b.</span></span> <span data-ttu-id="12172-167">Uruchom hello następującego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="12172-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="12172-168">Czy można pomyślnie pobrać dane wyjściowe hello, jest testowany z klastrem usługi HDInsight toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="12172-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="12172-169">Jeśli chcesz tooupdate hello notesu konfiguracji tooconnect tooa innego klastra należy zaktualizować hello config.json hello nowy zestaw wartości, jak pokazano w kroku 3 powyżej.</span><span class="sxs-lookup"><span data-stu-id="12172-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="12172-170">Dlaczego Instalacja oprogramowania Jupyter na komputerze?</span><span class="sxs-lookup"><span data-stu-id="12172-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="12172-171">Może istnieć wiele przyczyn, dlaczego może być tooinstall Jupyter na komputerze, a następnie podłącz je tooa Spark klastra w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12172-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="12172-172">Mimo że notesów Jupyter są już dostępne na powitania klastra Spark w usłudze Azure HDInsight, zainstalowanie Jupyter na komputerze zapewnia hello toocreate opcji notesy lokalnie, przetestować aplikację na klastrze uruchomione, a następnie przekaż hello notesów toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="12172-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="12172-173">tooupload hello notesów toohello klastra możesz albo przekazać je za pomocą notesu Jupyter hello, w którym jest uruchomiona lub hello klastra lub zapisać je toohello /HdiNotebooks folderu hello konta magazynu skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="12172-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="12172-174">Aby uzyskać więcej informacji dotyczących sposobu przechowywania notesów w klastrze hello, zobacz [notesów Jupyter przechowywania](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="12172-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="12172-175">Z notesów hello dostępne lokalnie, możesz połączyć toodifferent klastry Spark oparty na wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="12172-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="12172-176">Można użyć tooimplement GitHub systemu kontroli źródła i kontroli wersji dla notebooków hello.</span><span class="sxs-lookup"><span data-stu-id="12172-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="12172-177">Może także zawierać środowisku współpracy, gdy wielu użytkowników może współpracować z hello sam notesu.</span><span class="sxs-lookup"><span data-stu-id="12172-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="12172-178">Możesz pracować z notesów lokalnie nawet bez klastra.</span><span class="sxs-lookup"><span data-stu-id="12172-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="12172-179">Wystarczy tootest klastra notesy względem, nie toomanually zarządzać notesy lub środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="12172-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="12172-180">Go może być łatwiejsze tooconfigure środowiska deweloperskiego lokalnego niż tooconfigure hello Jupyter instalacji na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="12172-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="12172-181">Można korzystać z całego oprogramowania hello zainstalowane lokalnie bez konfigurowania co najmniej jeden klaster zdalnego.</span><span class="sxs-lookup"><span data-stu-id="12172-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="12172-182">Za pomocą Jupyter zainstalowany na komputerze lokalnym, wielu użytkowników można uruchomić hello tego samego notesu na powitania Spark tego samego klastra na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="12172-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="12172-183">W takiej sytuacji wiele sesji Livy są tworzone.</span><span class="sxs-lookup"><span data-stu-id="12172-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="12172-184">Jeśli wystąpiły problemu i chcesz toodebug, że będzie on tootrack złożonych zadań, w którym sesja programu Livy należy toowhich użytkownika.</span><span class="sxs-lookup"><span data-stu-id="12172-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="12172-185"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="12172-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="12172-186">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="12172-187">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="12172-187">Scenarios</span></span>
* [<span data-ttu-id="12172-188">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="12172-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="12172-189">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="12172-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="12172-190">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="12172-191">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="12172-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="12172-192">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="12172-193">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="12172-193">Create and run applications</span></span>
* [<span data-ttu-id="12172-194">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="12172-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="12172-195">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="12172-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="12172-196">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="12172-196">Tools and extensions</span></span>
* [<span data-ttu-id="12172-197">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="12172-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="12172-198">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="12172-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="12172-199">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="12172-200">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="12172-201">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="12172-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="12172-202">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="12172-202">Manage resources</span></span>
* [<span data-ttu-id="12172-203">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="12172-204">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="12172-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
