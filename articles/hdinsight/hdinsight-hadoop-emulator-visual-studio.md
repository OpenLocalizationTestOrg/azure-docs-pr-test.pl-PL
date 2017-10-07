---
title: aaaData Lake tools dla programu Visual Studio z Hortonworks piaskownicy - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure Data Lake tools dla programu Visual Studio z piaskownicy Hortonworks hello uruchomionych w lokalnej maszyny Wirtualnej. Z tych narzędzi można tworzyć i uruchamiania zadań Hive i Pig na piaskownicy hello i dane wyjściowe zadania w widoku i historii."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="19751-104">Za pomocą hello Azure Data Lake tools dla programu Visual Studio hello Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="19751-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="19751-105">Usługa Azure Data Lake zawiera narzędzia do pracy z ogólnym klastrów platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="19751-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="19751-106">Ten dokument zawiera kroki hello potrzebnych narzędzi Data Lake hello toouse z hello piaskownicy Hortonworks uruchomiony na lokalnej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="19751-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="19751-107">Użycie hello piaskownicy Hortonworks umożliwia toowork z platformą Hadoop lokalnie na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="19751-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="19751-108">Po opracowaniu rozwiązania, a toodeploy go na dużą skalę, można przenieść klastra usługi HDInsight tooan.</span><span class="sxs-lookup"><span data-stu-id="19751-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19751-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19751-109">Prerequisites</span></span>

* <span data-ttu-id="19751-110">Witaj Hortonworks piaskownicy, działających w maszynie wirtualnej na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="19751-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="19751-111">Ten dokument został zapisany i przetestowana piaskownicy hello uruchomionych w Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="19751-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="19751-112">Aby uzyskać informacje na temat konfigurowania hello piaskownicy, zobacz hello [wprowadzenie hello Hortonworks piaskownicy.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="19751-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="19751-113">dokument.</span><span class="sxs-lookup"><span data-stu-id="19751-113">document.</span></span>

* <span data-ttu-id="19751-114">Visual Studio 2013, Visual Studio 2015 lub Visual Studio 2017 (dowolna wersja).</span><span class="sxs-lookup"><span data-stu-id="19751-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="19751-115">Witaj [zestawu Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/) 2.7.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="19751-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="19751-116">Witaj [Azure Data Lake tools dla Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="19751-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="19751-117">Konfigurowanie haseł dla hello piaskownicy</span><span class="sxs-lookup"><span data-stu-id="19751-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="19751-118">Upewnij się, tym powitalne Hortonworks piaskownicy jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="19751-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="19751-119">Następnie wykonaj kroki hello hello [wprowadzenie w hello piaskownicy Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="19751-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="19751-120">Te kroki konfigurowania hello hasło hello SSH `root` konta i hello Ambari `admin` konta.</span><span class="sxs-lookup"><span data-stu-id="19751-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="19751-121">Te hasła są używane podczas łączenia toohello piaskownicy w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19751-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="19751-122">Połącz hello narzędzia toohello piaskownicy</span><span class="sxs-lookup"><span data-stu-id="19751-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="19751-123">Otwórz program Visual Studio, wybierz **widoku**, a następnie wybierz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="19751-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="19751-124">Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello **HDInsight** wpis, a następnie wybierz **połączyć tooHDInsight emulatora**.</span><span class="sxs-lookup"><span data-stu-id="19751-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Zrzut ekranu z Eksploratora serwera, z tooHDInsight Connect emulatora wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="19751-126">Z hello **połączyć tooHDInsight emulatora** okna dialogowego wprowadź hasło hello skonfigurowane dla narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="19751-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją pole tekstowe hasła](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="19751-128">Wybierz **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="19751-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="19751-129">Użyj hello **hasło** hasło hello tooenter pola skonfigurowanych hello `root` konta.</span><span class="sxs-lookup"><span data-stu-id="19751-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="19751-130">Pozostaw hello innych pól na powitania wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="19751-130">Leave hello other fields at hello default value.</span></span>

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją pole tekstowe hasła](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="19751-132">Wybierz **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="19751-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="19751-133">Poczekaj, aż weryfikacji hello toofinish usług.</span><span class="sxs-lookup"><span data-stu-id="19751-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="19751-134">W niektórych przypadkach sprawdzanie poprawności może zakończyć się niepowodzeniem i monit tooupdate hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="19751-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="19751-135">Jeśli weryfikacja zakończy się niepowodzeniem, wybierz **aktualizacji**i zaczekaj, aż hello konfiguracji i weryfikacji dla hello toofinish usługi.</span><span class="sxs-lookup"><span data-stu-id="19751-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnionym przycisku Aktualizuj](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="19751-137">proces aktualizacji Hello używa powitalne toomodify Ambari toowhat konfiguracji Hortonworks piaskownicy jest oczekiwane przez hello usługi Data Lake tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19751-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="19751-138">Po zakończeniu sprawdzania poprawności, wybierz **Zakończ** toocomplete konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="19751-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="19751-139">![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją przycisk Zakończ](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="19751-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="19751-140">W zależności od szybkości hello Środowisko deweloperskie i hello ilość pamięci przydzielonej maszynie wirtualnej toohello ona potrwać kilka minut tooconfigure i zweryfikować hello usług.</span><span class="sxs-lookup"><span data-stu-id="19751-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="19751-141">Po wykonaniu tych kroków, masz teraz **lokalnego klastra usługi HDInsight** wpis w Eksploratorze serwera w obszarze hello **HDInsight** sekcji.</span><span class="sxs-lookup"><span data-stu-id="19751-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="19751-142">Napisz zapytanie Hive</span><span class="sxs-lookup"><span data-stu-id="19751-142">Write a Hive query</span></span>

<span data-ttu-id="19751-143">Gałąź zapewnia języka przypominającego SQL kwerendy (HiveQL) do pracy z danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="19751-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="19751-144">Użyj hello następujące czynności toolearn jak toorun na żądanie zapytania względem hello lokalnym klastrem.</span><span class="sxs-lookup"><span data-stu-id="19751-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="19751-145">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy wpis hello hello klastra lokalnego dodanego wcześniej, a następnie wybierz **Napisz zapytanie Hive**.</span><span class="sxs-lookup"><span data-stu-id="19751-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Zrzut ekranu z Eksploratora serwera zapisu wyróżnione zapytanie Hive](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="19751-147">Pojawi się okno nowego zapytania.</span><span class="sxs-lookup"><span data-stu-id="19751-147">A new query window appears.</span></span> <span data-ttu-id="19751-148">W tym miejscu można szybko zapisu i przesyłanie klastra lokalnego toohello zapytania.</span><span class="sxs-lookup"><span data-stu-id="19751-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="19751-149">W nowym oknie zapytania hello wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="19751-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="19751-150">Kwerenda hello toorun, wybierz opcję **przesyłania** u góry hello hello okna.</span><span class="sxs-lookup"><span data-stu-id="19751-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="19751-151">Pozostaw hello inne wartości (**partii** i nazwa serwera) na powitania wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="19751-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Zrzut ekranu okna zapytań, przycisk Prześlij hello wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="19751-153">Można również użyć hello menu rozwijanym obok zbyt**przesyłania** tooselect **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="19751-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="19751-154">Zaawansowane opcje pozwalają tooprovide dodatkowe opcje podczas przesyłania zadania hello.</span><span class="sxs-lookup"><span data-stu-id="19751-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Zrzut ekranu przedstawia skryptu, okno dialogowe](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="19751-156">Po przesłaniu zapytania hello jest wyświetlany stan zadania hello.</span><span class="sxs-lookup"><span data-stu-id="19751-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="19751-157">Stan zadania Hello Wyświetla informacje o zadaniu hello jest przetwarzany przez Hadoop.</span><span class="sxs-lookup"><span data-stu-id="19751-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="19751-158">**Stan zadania** zawiera stan hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="19751-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="19751-159">Stan Hello jest okresowo aktualizowana lub skorzystać z hello Odśwież ikona toorefresh hello stan ręcznie.</span><span class="sxs-lookup"><span data-stu-id="19751-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Okno dialogowe zrzut ekranu widoku zadania, z wyróżnioną pozycją stan zadania](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="19751-161">Po hello **stan zadania** zmiany zbyt**zakończone**, zostanie wyświetlony skierowany acykliczne Graph (DAG).</span><span class="sxs-lookup"><span data-stu-id="19751-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="19751-162">Ten schemat przedstawia ścieżka wykonywania hello, określony przez Tez podczas przetwarzania zapytania Hive hello.</span><span class="sxs-lookup"><span data-stu-id="19751-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="19751-163">Tez jest hello domyślnego wykonywania aparatu gałęzi w klastrze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="19751-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19751-164">Tez jest to domyślna hello, korzystając z klastrów usługi HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="19751-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="19751-165">Nie jest domyślnym hello w usłudze HDInsight z systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="19751-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="19751-166">toouse go, należy dodać wiersz hello `set hive.execution.engine = tez;` toohello początku zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="19751-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="19751-167">Użyj hello **dane wyjściowe zadania** link tooview hello w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19751-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="19751-168">W takim przypadku jest 823, hello liczbę wierszy w tabeli sample_08 hello.</span><span class="sxs-lookup"><span data-stu-id="19751-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="19751-169">Można wyświetlić informacje diagnostyczne o zadaniu hello przy użyciu hello **dziennik zadań** i **Pobierz dziennik YARN** łącza.</span><span class="sxs-lookup"><span data-stu-id="19751-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="19751-170">Można również uruchamiać zadania Hive interaktywnego, zmieniając hello **partii** pola zbyt**Interactive**.</span><span class="sxs-lookup"><span data-stu-id="19751-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="19751-171">Następnie wybierz **Execute**.</span><span class="sxs-lookup"><span data-stu-id="19751-171">Then select **Execute**.</span></span>

    ![Zrzut ekranu interakcyjne i wykonywanie przycisków wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="19751-173">Interakcyjne zapytania strumieni hello dziennika danych wyjściowych wygenerowanych podczas przetwarzania toohello **danych wyjściowych serwera HiveServer2** okna.</span><span class="sxs-lookup"><span data-stu-id="19751-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19751-174">Witaj informacji jest hello takie same, który jest dostępny z hello **dziennik zadań** link po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="19751-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Zrzut ekranu przedstawiający pliku dziennika](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="19751-176">Utwórz projekt Hive</span><span class="sxs-lookup"><span data-stu-id="19751-176">Create a Hive project</span></span>

<span data-ttu-id="19751-177">Można również utworzyć projekt, który zawiera wiele skryptów Hive.</span><span class="sxs-lookup"><span data-stu-id="19751-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="19751-178">Użyj projektu, gdy pokrewne skrypty lub mają toostore skryptów w systemie kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="19751-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="19751-179">W programie Visual Studio, wybierz **pliku**, **nowy**, a następnie **projektu**.</span><span class="sxs-lookup"><span data-stu-id="19751-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="19751-180">Z listy hello projektów, rozwiń węzeł **szablony**, rozwiń węzeł **usługi Azure Data Lake**, a następnie wybierz **gałąź (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="19751-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="19751-181">Wybierz z listy hello szablonów **Hive próbki**.</span><span class="sxs-lookup"><span data-stu-id="19751-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="19751-182">Wprowadź nazwę i lokalizację, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="19751-182">Enter a name and location, and then select **OK**.</span></span>

    ![Wyróżnione okno zrzut ekranu nowego projektu, przy użyciu usługi Azure Data Lake, HIVE, przykładowe Hive i OK](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="19751-184">Witaj **Hive próbki** projekt zawiera dwa skrypty **WebLogAnalysis.hql** i **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="19751-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="19751-185">Można kierować te skrypty, używając hello sam **przesyłania** u góry hello hello okna.</span><span class="sxs-lookup"><span data-stu-id="19751-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="19751-186">Utwórz projekt usługi Pig</span><span class="sxs-lookup"><span data-stu-id="19751-186">Create a Pig project</span></span>

<span data-ttu-id="19751-187">Gałąź zawiera języka przypominającego SQL do pracy z danych strukturalnych, natomiast Pig działanie polega na przekształcenia danych.</span><span class="sxs-lookup"><span data-stu-id="19751-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="19751-188">Pig zapewnia języka (Pig Latin), która pozwala toodevelop potoku transformacji.</span><span class="sxs-lookup"><span data-stu-id="19751-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="19751-189">toouse Pig z lokalnym klastrem hello, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="19751-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="19751-190">Otwórz program Visual Studio i wybierz **pliku**, **nowy**, a następnie **projektu**.</span><span class="sxs-lookup"><span data-stu-id="19751-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="19751-191">Z listy hello projektów, rozwiń węzeł **szablony**, rozwiń węzeł **usługi Azure Data Lake**, a następnie wybierz **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="19751-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="19751-192">Wybierz z listy hello szablonów **aplikacji Pig**.</span><span class="sxs-lookup"><span data-stu-id="19751-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="19751-193">Wprowadź nazwę lokalizacji, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="19751-193">Enter a name, location, and then select **OK**.</span></span>

    ![Okno zrzut ekranu nowego projektu, przy użyciu usługi Azure Data Lake, Pig, Pig, aplikacji i OK, wyróżniony](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="19751-195">Wprowadź hello następującego tekstu jako zawartość hello hello **script.pig** pliku, który został utworzony z tego projektu.</span><span class="sxs-lookup"><span data-stu-id="19751-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="19751-196">Pig używa innego języka niż Hive, sposób uruchamiania zadań hello jest jednolita obu językach za pośrednictwem hello **przesyłania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="19751-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="19751-197">Wybór hello listy rozwijanej obok **przesyłania** Wyświetla okno dialogowe Zaawansowane przesyłania programu Pig.</span><span class="sxs-lookup"><span data-stu-id="19751-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Zrzut ekranu przedstawia skryptu, okno dialogowe](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="19751-199">Stan zadania Hello i danych wyjściowych będzie również wyświetlana, hello takie same jak zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="19751-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Zrzut ekranu przedstawiający zakończonych zadań Pig](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="19751-201">Wyświetl zadania</span><span class="sxs-lookup"><span data-stu-id="19751-201">View jobs</span></span>

<span data-ttu-id="19751-202">Narzędzia Data Lake pozwalają również tooeasily Wyświetl informacje o zadaniach, które zostały uruchomione na platformie Hadoop.</span><span class="sxs-lookup"><span data-stu-id="19751-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="19751-203">Użyj następujących hello kroki toosee hello zadania, które zostały uruchomione w klastrze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="19751-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="19751-204">Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy klaster lokalny hello, a następnie wybierz **Wyświetl zadania**.</span><span class="sxs-lookup"><span data-stu-id="19751-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="19751-205">Zostanie wyświetlona lista zadań, które zostały przesłane toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="19751-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Zrzut ekranu z Eksploratora serwera, z wyróżnioną pozycją zadaniami widoku](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="19751-207">Z listy hello zadań wybierz jedną szczegóły zadania hello tooview.</span><span class="sxs-lookup"><span data-stu-id="19751-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Zrzut ekranu z zadania przeglądarki, z jednym z wyróżnionym zadania hello](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="19751-209">wyświetlane informacje Hello jest podobne toowhat, który zostanie wyświetlony po uruchomieniu zapytania Hive i Pig, w tym linki tooview hello danych wyjściowych dziennika informacje i.</span><span class="sxs-lookup"><span data-stu-id="19751-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="19751-210">Można również zmodyfikować i ponownie prześlij zadanie hello w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="19751-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="19751-211">Wyświetl Hive baz danych</span><span class="sxs-lookup"><span data-stu-id="19751-211">View Hive databases</span></span>

1. <span data-ttu-id="19751-212">W **Eksploratora serwera**, rozwiń węzeł hello **lokalnego klastra usługi HDInsight** wpis, a następnie rozwiń węzeł **bazy danych programu Hive**.</span><span class="sxs-lookup"><span data-stu-id="19751-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="19751-213">Witaj **domyślne** i **xademo** baz danych w klastrze lokalnym hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="19751-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="19751-214">Rozszerzanie bazy danych zawiera tabele hello w hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="19751-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Zrzut ekranu Eksploratora serwera z bazami danych rozwinięty](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="19751-216">Rozszerzanie tabeli Wyświetla hello kolumn dla tabeli.</span><span class="sxs-lookup"><span data-stu-id="19751-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="19751-217">dane hello widoku tooquickly, kliknij prawym przyciskiem myszy tabelę, a następnie wybierz **Wyświetl pierwszych 100 wierszy**.</span><span class="sxs-lookup"><span data-stu-id="19751-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Zrzut ekranu z Eksploratora serwera, z tabeli rozwinięty i Wyświetl pierwszych 100 wierszy wybrane](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="19751-219">Właściwości bazy danych i tabeli</span><span class="sxs-lookup"><span data-stu-id="19751-219">Database and table properties</span></span>

<span data-ttu-id="19751-220">Można wyświetlić właściwości hello bazy danych lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="19751-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="19751-221">Wybieranie **właściwości** Wyświetla szczegóły elementu hello wybrany w oknie właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="19751-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="19751-222">Na przykład zobacz hello informacje wyświetlane na powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="19751-222">For example, see hello information shown in hello following screenshot:</span></span>

![Zrzut ekranu właściwości okna](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="19751-224">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="19751-224">Create a table</span></span>

<span data-ttu-id="19751-225">toocreate tabelę, kliknij prawym przyciskiem myszy bazę danych, a następnie wybierz **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="19751-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Zrzut ekranu z Eksploratora serwera, z Create Table wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="19751-227">Następnie można utworzyć tabeli hello za pomocą formularza.</span><span class="sxs-lookup"><span data-stu-id="19751-227">You can then create hello table using a form.</span></span> <span data-ttu-id="19751-228">U dołu hello hello następującego zrzutu ekranu, zobacz hello HiveQL raw, używany toocreate hello tabela.</span><span class="sxs-lookup"><span data-stu-id="19751-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Zrzut ekranu przedstawiający hello formularz używany toocreate tabeli](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="19751-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19751-230">Next steps</span></span>

* [<span data-ttu-id="19751-231">Learning liny hello hello Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="19751-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="19751-232">Samouczek Hadoop — wprowadzenie HDP</span><span class="sxs-lookup"><span data-stu-id="19751-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
