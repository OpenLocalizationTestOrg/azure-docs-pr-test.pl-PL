---
title: "Instalacja oprogramowania Jupyter lokalnie i połączenia z klastrem usługi Azure HDInsight Spark | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować notesu Jupyter lokalnie na komputerze i podłącz go do klastra Apache Spark w usłudze Azure HDInsight."
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="f8dfc-103">Zainstaluj notesu Jupyter na komputerze i nawiązywanie Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="f8dfc-104">W tym artykule należy dowiedzieć się, jak zainstalować notesu Jupyter z niestandardowych PySpark (dla języka Python) i jądra Spark (na języku Scala) z Spark magic i notesu nawiązać połączenia z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="f8dfc-105">Może istnieć wiele przyczyn, aby instalacja oprogramowania Jupyter na komputerze lokalnym i mogą być również pewne wyzwania.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="f8dfc-106">Aby uzyskać więcej informacji, zobacz sekcję [Dlaczego należy zainstalować oprogramowania Jupyter na tym komputerze](#why-should-i-install-jupyter-on-my-computer) na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="f8dfc-107">Istnieją trzy kluczowe kroki związane z instalowanie Jupyter i Spark magic na komputerze.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="f8dfc-108">Zainstaluj notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="f8dfc-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="f8dfc-109">Instalowanie jądra PySpark i Spark przy użyciu Spark magic</span><span class="sxs-lookup"><span data-stu-id="f8dfc-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="f8dfc-110">Skonfiguruj magic Spark uzyskanie dostępu do klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="f8dfc-111">Aby uzyskać więcej informacji o niestandardowych jądra i magic Spark dostępne dla notesu Jupyter w klastrze z klastrem usługi HDInsight, zobacz [jądra dostępne dla notesu Jupyter klastrze Apache Spark w systemie Linux klastrów HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="f8dfc-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8dfc-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f8dfc-112">Prerequisites</span></span>
<span data-ttu-id="f8dfc-113">Wymagania wstępne wymienione w tym miejscu nie dotyczą instalowania Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="f8dfc-114">Są to podłączania notesu Jupyter w klastrze usługi HDInsight, po zainstalowaniu notesu.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="f8dfc-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-115">An Azure subscription.</span></span> <span data-ttu-id="f8dfc-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f8dfc-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f8dfc-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f8dfc-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f8dfc-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="f8dfc-119">Zainstaluj na tym komputerze notesu Jupyter</span><span class="sxs-lookup"><span data-stu-id="f8dfc-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="f8dfc-120">Python należy zainstalować przed zainstalowaniem notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="f8dfc-121">Zarówno Python i Jupyter są dostępne jako część [Anaconda dystrybucji](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="f8dfc-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="f8dfc-122">Po zainstalowaniu Anaconda, należy zainstalować dystrybucji języka Python.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="f8dfc-123">Po zainstalowaniu Anaconda, możesz dodać za pomocą odpowiednich poleceń instalacji Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="f8dfc-124">Pobierz [Instalator Anaconda](https://www.continuum.io/downloads) dla platformy i uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="f8dfc-125">Podczas uruchamiania Kreatora instalacji, upewnij się, że zostanie wybrana opcja, aby dodać Anaconda do zmiennej PATH.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="f8dfc-126">Uruchom następujące polecenie, aby instalacja oprogramowania Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="f8dfc-127">Aby uzyskać więcej informacji na temat instalowania Jupyter, zobacz [Jupyter instalowanie przy użyciu Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="f8dfc-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="f8dfc-128">Zainstaluj jądra i Spark magic</span><span class="sxs-lookup"><span data-stu-id="f8dfc-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="f8dfc-129">Aby uzyskać instrukcje dotyczące sposobu instalowania Spark magic, jądra PySpark i Spark, postępuj zgodnie z instrukcjami instalacji [dokumentacji sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="f8dfc-130">Pierwszym krokiem w dokumentacji magic Spark jest wyświetlany monit o zainstalowanie Spark magic.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="f8dfc-131">Zastąp ten pierwszy krok w łączu za pomocą następujących poleceń, w zależności od wersji z klastrem usługi HDInsight, z którą będzie łączyć się.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="f8dfc-132">Następnie wykonaj pozostałe kroki w dokumentacji magic Spark.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="f8dfc-133">Jeśli chcesz zainstalować różne jądra, należy wykonać krok 3 w sekcji instrukcje instalacji magic Spark.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="f8dfc-134">W przypadku klastrów v3.4 należy zainstalować sparkmagic 0.2.3, wykonując`pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="f8dfc-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="f8dfc-135">W przypadku klastrów w wersji 3.5 i v3.6 należy zainstalować sparkmagic 0.11.2, wykonując`pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="f8dfc-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="f8dfc-136">Skonfiguruj magic Spark do nawiązania połączenia klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="f8dfc-137">W tej sekcji skonfigurujesz magic Spark, która zainstalowane wcześniej do nawiązania połączenia klastra Apache Spark, który musi mieć już utworzone w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="f8dfc-138">Informacje o konfiguracji Jupyter zazwyczaj znajduje się w katalogu macierzystego użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="f8dfc-139">Aby zlokalizować katalog macierzysty na dowolnej platformie systemu operacyjnego, wpisz następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="f8dfc-140">Uruchom powłokę Python.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-140">Start the Python shell.</span></span> <span data-ttu-id="f8dfc-141">W oknie polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f8dfc-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="f8dfc-142">Na powłoki Python wprowadź następujące polecenie, aby dowiedzieć się, katalogu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="f8dfc-143">Przejdź do katalogu macierzystego i Utwórz folder o nazwie **.sparkmagic** Jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="f8dfc-144">W folderze, Utwórz plik o nazwie **config.json** i Dodaj następujący fragment kodu JSON wewnątrz niej.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="f8dfc-145">SUBSTITUTE **{USERNAME}**, **{CLUSTERDNSNAME}**, i **{BASE64ENCODEDPASSWORD}** z odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="f8dfc-146">Szereg narzędzi w ulubionych języka programowania lub w trybie online służy do generowania haseł kodowany w standardzie base64 rzeczywistego hasła.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="f8dfc-147">Konfigurowanie ustawień pulsu praw w `config.json`.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="f8dfc-148">Należy dodać te ustawienia na tym samym poziomie jako `kernel_python_credentials` i `kernel_scala_credentials` wstawki programu dodane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="f8dfc-149">Na przykład o tym, jak i kiedy należy dodać ustawienia pulsu, zobacz [config.json próbki](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="f8dfc-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="f8dfc-150">Aby uzyskać `sparkmagic 0.2.3` (klastrów v3.4), obejmują:</span><span class="sxs-lookup"><span data-stu-id="f8dfc-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="f8dfc-151">Aby uzyskać `sparkmagic 0.11.2` (klastrów w wersji 3.5 i v3.6), obejmują:</span><span class="sxs-lookup"><span data-stu-id="f8dfc-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="f8dfc-152">Aby upewnić się, że nie przedostają sesji są wysyłane impulsy.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="f8dfc-153">Gdy komputer przechodzi w stan uśpienia lub jest wyłączony, pulsu nie są wysyłane, co Trwa sesja wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="f8dfc-154">V3.4 klastrów, jeśli chcesz wyłączyć to zachowanie można ustawić konfiguracji Livy `livy.server.interactive.heartbeat.timeout` do `0` w interfejsie użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="f8dfc-155">Dla klastrów w wersji 3.5 Jeśli konfiguracja 3.5 powyżej, nie należy ustawiać sesji nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="f8dfc-156">Uruchom Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-156">Start Jupyter.</span></span> <span data-ttu-id="f8dfc-157">Użyj następującego polecenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="f8dfc-158">Sprawdź, czy możesz nawiązać klastra za pomocą notesu Jupyter i że za pomocą dostępnych magic Spark jądra.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="f8dfc-159">Wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-159">Perform the following steps.</span></span>

    <span data-ttu-id="f8dfc-160">a.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-160">a.</span></span> <span data-ttu-id="f8dfc-161">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-161">Create a new notebook.</span></span> <span data-ttu-id="f8dfc-162">W prawym górnym rogu, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="f8dfc-163">Powinna zostać wyświetlona domyślna jądra **Python2** i dwa nowe jądra, które można zainstalować **PySpark** i **Spark**.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="f8dfc-164">Kliknij przycisk **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-164">Click **PySpark**.</span></span>

    <span data-ttu-id="f8dfc-165">![Jądra w notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "jądra w notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="f8dfc-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="f8dfc-166">b.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-166">b.</span></span> <span data-ttu-id="f8dfc-167">Uruchom poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="f8dfc-168">Czy można pomyślnie pobrać dane wyjściowe, jest przetestować połączenie z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="f8dfc-169">Jeśli chcesz zaktualizować konfigurację notesu nawiązać do innego klastra, należy zaktualizować config.json o nowy zestaw wartości, jak pokazano w kroku 3 powyżej.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="f8dfc-170">Dlaczego Instalacja oprogramowania Jupyter na komputerze?</span><span class="sxs-lookup"><span data-stu-id="f8dfc-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="f8dfc-171">Może istnieć wiele przyczyn, dlaczego warto Instalacja oprogramowania Jupyter na komputerze, a następnie podłącz go do klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="f8dfc-172">Mimo że notesów Jupyter są już dostępne w klastrze Spark w usłudze Azure HDInsight, instalowanie oprogramowania Jupyter na komputerze zapewnia można równocześnie utworzyć notesy lokalnie, przetestować aplikację na klastrze uruchomione, a następnie przekaż notebooki do klastra.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="f8dfc-173">Aby przekazać notebooki do klastra, można przekazać je za pomocą notesu Jupyter, na którym jest uruchomiona lub klastra lub zapisać je w folderze /HdiNotebooks w ramach konta magazynu skojarzone z klastrem.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="f8dfc-174">Aby uzyskać więcej informacji dotyczących sposobu przechowywania notesów w klastrze, zobacz [notesów Jupyter przechowywania](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="f8dfc-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="f8dfc-175">Dzięki notesy dostępne lokalnie, możesz mogą łączyć się różne klastry Spark oparty na wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="f8dfc-176">GitHub można użyć do wdrożenia systemu kontroli źródła i kontroli wersji dla komputerów przenośnych.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="f8dfc-177">Można również mieć środowisku współpracy, gdy wielu użytkowników może korzystać z tego samego notesu.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="f8dfc-178">Możesz pracować z notesów lokalnie nawet bez klastra.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="f8dfc-179">Wystarczy tylko klastra do testowania notesy względem, aby nie ręcznie zarządzać notesy lub środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="f8dfc-180">Może być łatwiejsze do konfigurowania środowiska deweloperskiego lokalnego nie można skonfigurować instalację Jupyter w klastrze.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="f8dfc-181">Można korzystać z oprogramowania zainstalowane lokalnie bez konfigurowania co najmniej jeden klaster zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="f8dfc-182">Jupyter zainstalowany na komputerze lokalnym wielu użytkowników umożliwia uruchamianie tego samego notesu na tym samym klastrze Spark w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="f8dfc-183">W takiej sytuacji wiele sesji Livy są tworzone.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="f8dfc-184">Jeśli wystąpiły problemu i chcesz debugować, będzie się, że złożonym zadaniem w celu śledzenia sesji Livy, które należy do użytkownika, który.</span><span class="sxs-lookup"><span data-stu-id="f8dfc-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="f8dfc-185"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f8dfc-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f8dfc-186">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f8dfc-187">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="f8dfc-187">Scenarios</span></span>
* [<span data-ttu-id="f8dfc-188">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="f8dfc-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f8dfc-189">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="f8dfc-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f8dfc-190">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="f8dfc-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f8dfc-191">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f8dfc-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f8dfc-192">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f8dfc-193">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8dfc-193">Create and run applications</span></span>
* [<span data-ttu-id="f8dfc-194">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="f8dfc-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f8dfc-195">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="f8dfc-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f8dfc-196">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f8dfc-196">Tools and extensions</span></span>
* [<span data-ttu-id="f8dfc-197">Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="f8dfc-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f8dfc-198">Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="f8dfc-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f8dfc-199">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f8dfc-200">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f8dfc-201">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="f8dfc-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="f8dfc-202">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="f8dfc-202">Manage resources</span></span>
* [<span data-ttu-id="f8dfc-203">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f8dfc-204">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8dfc-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
