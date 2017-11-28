---
title: "aaaInstall programu RStudio z serwerem R w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Jak tooinstall programu RStudio z serwerem R w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="1db9d-103">Instalowanie programu RStudio z serwerem R w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1db9d-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="1db9d-104">W tym artykule opisano, jak tooinstall hello społecznościową wersję (bezpłatnie) [serwera programu RStudio](https://www.rstudio.com/products/rstudio-server/) hello krawędzi węzeł klastra przy użyciu niestandardowego skryptu.</span><span class="sxs-lookup"><span data-stu-id="1db9d-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="1db9d-105">Serwer programu RStudio udostępnia środowiska IDE bazujące na przeglądarce do użycia przez klientów zdalnych i jest powszechnie używany w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="1db9d-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="1db9d-106">Istnieje wiele zintegrowane środowisk deweloperskich (IDE) dostępnych dla R dzisiaj, w tym:</span><span class="sxs-lookup"><span data-stu-id="1db9d-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="1db9d-107">Firmy Microsoft [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="1db9d-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="1db9d-108">Serwer programu RStudio</span><span class="sxs-lookup"><span data-stu-id="1db9d-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="1db9d-109">Walware na podstawie Eclipse [StatET](http://www.walware.de/goto/statet).</span><span class="sxs-lookup"><span data-stu-id="1db9d-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="1db9d-110">Zaletą Hello instalacji programu RStudio serwera na powitania krawędzi węzła z klastra usługi HDInsight jest pełne środowisko IDE dla rozwoju hello i wykonywanie skryptów R z serwerem R w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="1db9d-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="1db9d-111">Ta konfiguracja może być znacznie większą wydajność niż domyślne hello konsoli R.</span><span class="sxs-lookup"><span data-stu-id="1db9d-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="1db9d-112">Hello procedury opisane w tym artykule jest stosowana tylko, jeśli nie wybrano tooinstall serwera programu RStudio community edition podczas inicjowania obsługi klastra.</span><span class="sxs-lookup"><span data-stu-id="1db9d-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="1db9d-113">Jeśli dodano podczas inicjowania obsługi, następnie tooaccess go kliknij na powitania **pulpity nawigacyjne serwera R** kafelka w hello Azure portalu wpis dla klastra, a następnie na powitania **R Studio Server** kafelka.</span><span class="sxs-lookup"><span data-stu-id="1db9d-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="1db9d-114">Wolisz toouse wersji Pro hello komercyjnie licencję programu RStudio serwera, należy postępować zgodnie z instrukcjami instalacji hello [serwera programu RStudio](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="1db9d-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="1db9d-115">Jeśli korzystasz z klastra usługi HDInsight, dla którego R został zainstalowany przy użyciu hello [zainstalować akcji skryptu języka R](hdinsight-hadoop-r-scripts-linux.md), hello kroków w tym dokumencie nie będą działać poprawnie, ponieważ wymagają one R Server w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1db9d-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="1db9d-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1db9d-116">Prerequisites</span></span>

* <span data-ttu-id="1db9d-117">Klaster Azure HDInsight z zainstalowanym serwerem R.</span><span class="sxs-lookup"><span data-stu-id="1db9d-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="1db9d-118">Aby uzyskać instrukcje, zobacz [wprowadzenie R Server w klastrach HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1db9d-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="1db9d-119">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="1db9d-119">An SSH client.</span></span> <span data-ttu-id="1db9d-120">Dystrybucje systemu Linux i Unix lub Macintosh OS X, hello `ssh` polecenie jest dostępne w systemie operacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="1db9d-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="1db9d-121">W systemie Windows, firma Microsoft zaleca [programów Cygwin](http://www.redhat.com/services/custom/cygwin/) z hello [opcji OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), lub [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="1db9d-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="1db9d-122">Instalowanie programu RStudio na powitania klastra przy użyciu niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="1db9d-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="1db9d-123">Poniżej przedstawiono kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1db9d-123">Here are hello steps:</span></span>

1. <span data-ttu-id="1db9d-124">Zidentyfikuj węzła krawędzi hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="1db9d-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="1db9d-125">Dla klastra usługi HDInsight, z serwerem R poniżej przedstawiono hello konwencję nazewnictwa dla węzła głównego i węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="1db9d-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="1db9d-126">Nagłówek węzła`CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="1db9d-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="1db9d-127">Węzeł krawędzi`CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="1db9d-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="1db9d-128">SSH do węzła krawędzi hello hello klastra przy użyciu wzorca nazewnictwa hello w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="1db9d-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="1db9d-129">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1db9d-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="1db9d-130">Po nawiązaniu połączenia stają się w klastrze hello użytkownika root.</span><span class="sxs-lookup"><span data-stu-id="1db9d-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="1db9d-131">W sesji SSH hello Użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1db9d-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="1db9d-132">Pobierz hello tooinstall skryptu niestandardowego programu RStudio.</span><span class="sxs-lookup"><span data-stu-id="1db9d-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="1db9d-133">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1db9d-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="1db9d-134">Zmień uprawnienia hello hello skryptu niestandardowego pliku, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="1db9d-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="1db9d-135">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1db9d-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="1db9d-136">Hasło SSH jest używany podczas tworzenia klastra usługi HDInsight z serwerem R, można pominąć ten krok i przejdź dalej toohello.</span><span class="sxs-lookup"><span data-stu-id="1db9d-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="1db9d-137">Jeśli używasz klucza SSH zamiast toocreate hello klastra, należy ustawić hasło dla użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="1db9d-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="1db9d-138">Należy to hasło, łącząc tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="1db9d-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="1db9d-139">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="1db9d-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="1db9d-140">Po wyświetleniu monitu o **Kerberos bieżącego hasła**, naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1db9d-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="1db9d-141">Należy pamiętać, że należy zastąpić `USERNAME` użytkownika SSH dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1db9d-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="1db9d-142">Jeśli pomyślnie ustawiono hasło, powinny być widoczne następujące wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="1db9d-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="1db9d-143">Zamknij hello sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="1db9d-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="1db9d-144">Tworzenie klastra toohello tunelu SSH przez mapowanie `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` na powitania HDInsight klastra toohello komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="1db9d-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="1db9d-145">Należy utworzyć tunel SSH przed otwarciem nowej sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1db9d-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="1db9d-146">Klient systemu Linux lub klienta systemu Windows z [programów Cygwin](http://www.redhat.com/services/custom/cygwin/), otwórz sesję terminala i użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1db9d-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="1db9d-147">Zastąp **USERNAME** użytkownika SSH dla klastra usługi HDInsight i Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1db9d-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="1db9d-148">Umożliwia także klucz SSH, zamiast hasła przez dodanie `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="1db9d-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="1db9d-149">Jeśli następnie używany klient systemu Windows z programu PuTTY</span><span class="sxs-lookup"><span data-stu-id="1db9d-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="1db9d-150">Otwórz program PuTTY i wprowadzić informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="1db9d-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="1db9d-151">W hello **kategorii** toohello sekcji lewej strony okna dialogowego hello, rozwiń **połączenia**, rozwiń węzeł **SSH**, a następnie wybierz **tuneli**.</span><span class="sxs-lookup"><span data-stu-id="1db9d-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="1db9d-152">Podaj następujące informacje na powitania hello **przekierowanie portów opcje kontrolujące SSH** formularza:</span><span class="sxs-lookup"><span data-stu-id="1db9d-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="1db9d-153">**Port źródłowy** — Witaj port na powitania klienta, że chcesz tooforward.</span><span class="sxs-lookup"><span data-stu-id="1db9d-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="1db9d-154">Na przykład **8787**.</span><span class="sxs-lookup"><span data-stu-id="1db9d-154">For example, **8787**.</span></span>
        * <span data-ttu-id="1db9d-155">**Docelowy** — Witaj lokalizacji docelowej, która musi być zamapowany toohello maszyny lokalnej klienta.</span><span class="sxs-lookup"><span data-stu-id="1db9d-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="1db9d-156">Na przykład **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="1db9d-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="1db9d-157">![Tworzenie tunelu SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Tworzenie tunelu SSH")</span><span class="sxs-lookup"><span data-stu-id="1db9d-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="1db9d-158">Kliknij przycisk **Dodaj** tooadd hello ustawienia, a następnie kliknij przycisk **Otwórz** tooopen połączenie SSH.</span><span class="sxs-lookup"><span data-stu-id="1db9d-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="1db9d-159">Po wyświetleniu monitu zaloguj się za tooestablish serwera toohello sesji i Włącz hello tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="1db9d-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="1db9d-160">Otwórz przeglądarkę sieci web i wprowadź hello następującego adresu URL na podstawie portu hello, wprowadzonych w tunelu hello:</span><span class="sxs-lookup"><span data-stu-id="1db9d-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="1db9d-161">Jesteś tooenter zostanie wyświetlony monit o hello SSH nazwy użytkownika i hasła tooconnect toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="1db9d-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="1db9d-162">Jeśli podczas tworzenia klastra hello jest używany klucz SSH, musi wprowadzić hasło hello, który został utworzony w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="1db9d-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="1db9d-163">![Połącz tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Tworzenie tunelu SSH")</span><span class="sxs-lookup"><span data-stu-id="1db9d-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="1db9d-164">tootest czy hello instalacji programu RStudio zakończyło się pomyślnie, można uruchomić skrypt testu, który wykonuje R zadań MapReduce i Spark na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="1db9d-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="1db9d-165">toodownload hello testu skryptu toorun w programu RStudio, przejdź wstecz toohello SSH konsoli i wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1db9d-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="1db9d-166">Jeśli utworzono klastra usługi Hadoop z R, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1db9d-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="1db9d-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="1db9d-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="1db9d-168">Jeśli utworzono klaster Spark z R, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1db9d-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="1db9d-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="1db9d-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="1db9d-170">W programu RStudio zobacz temat hello przetestować skrypt, który został pobrany.</span><span class="sxs-lookup"><span data-stu-id="1db9d-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="1db9d-171">Kliknij dwukrotnie hello pliku tooopen, wybierz zawartość hello hello pliku, a następnie kliknij **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="1db9d-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="1db9d-172">Powinny pojawić się dane wyjściowe hello w hello **konsoli** okienka:</span><span class="sxs-lookup"><span data-stu-id="1db9d-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="1db9d-173">![Testowanie instalacji hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "testowanie hello instalacji")</span><span class="sxs-lookup"><span data-stu-id="1db9d-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="1db9d-174">Innym rozwiązaniem byłoby tootype `source(testhdi.r)` lub `source(testhdi_spark.r)` tooexecute hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="1db9d-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="1db9d-175">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1db9d-175">See also</span></span>

* [<span data-ttu-id="1db9d-176">Opcje kontekstu platformy R Server w klastrach HDInsight obliczania</span><span class="sxs-lookup"><span data-stu-id="1db9d-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* <span data-ttu-id="1db9d-177">[Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="1db9d-177">[Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md)</span></span>

