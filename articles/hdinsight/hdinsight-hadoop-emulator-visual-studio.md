---
title: Data Lake tools dla programu Visual Studio z Hortonworks piaskownicy - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak za pomocą usługi Azure Data Lake tools dla programu Visual Studio piaskownicy Hortonworks uruchomiony na lokalnej maszynie wirtualnej. Z tych narzędzi można tworzyć i uruchamiania zadań Hive i Pig na piaskownicy, a dane wyjściowe zadania w widoku i historii."
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
ms.openlocfilehash: 574ccaa8b2d9448a60ddf8adc7f92fa3683b1d61
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="2afd1-104">Użyj usługi Azure Data Lake tools dla programu Visual Studio z piaskownicy Hortonworks</span><span class="sxs-lookup"><span data-stu-id="2afd1-104">Use the Azure Data Lake tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="2afd1-105">Usługa Azure Data Lake zawiera narzędzia do pracy z ogólnym klastrów platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2afd1-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="2afd1-106">Ten dokument zawiera kroki niezbędne do korzystania z narzędzi Data Lake z piaskownicy Hortonworks uruchomiony na lokalnej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2afd1-106">This document provides the steps needed to use the Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="2afd1-107">Przy użyciu izolowanego Hortonworks umożliwia pracę z platformą Hadoop lokalnie na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="2afd1-107">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="2afd1-108">Po opracowaniu rozwiązania, można wdrożyć ją na dużą skalę, następnie można przenieść do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2afd1-108">After you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2afd1-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2afd1-109">Prerequisites</span></span>

* <span data-ttu-id="2afd1-110">Piaskownica Hortonworks działający na maszynie wirtualnej na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="2afd1-110">The Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="2afd1-111">Ten dokument został zapisany i przetestowana piaskownicy uruchomionych w Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="2afd1-111">This document was written and tested with the sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="2afd1-112">Aby uzyskać informacje na temat konfigurowania piaskownicy, zobacz [wprowadzenie Hortonworks piaskownicy.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2afd1-112">For information on setting up the sandbox, see the [Get started with the Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="2afd1-113">dokument.</span><span class="sxs-lookup"><span data-stu-id="2afd1-113">document.</span></span>

* <span data-ttu-id="2afd1-114">Visual Studio 2013, Visual Studio 2015 lub Visual Studio 2017 (dowolna wersja).</span><span class="sxs-lookup"><span data-stu-id="2afd1-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="2afd1-115">[Zestawu Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/) 2.7.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2afd1-115">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="2afd1-116">[Azure Data Lake tools dla Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="2afd1-116">The [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="2afd1-117">Konfigurowanie haseł piaskownicy</span><span class="sxs-lookup"><span data-stu-id="2afd1-117">Configure passwords for the sandbox</span></span>

<span data-ttu-id="2afd1-118">Upewnij się, że piaskownicy Hortonworks jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="2afd1-118">Make sure that the Hortonworks Sandbox is running.</span></span> <span data-ttu-id="2afd1-119">Następnie postępuj zgodnie z instrukcjami [wprowadzenie w piaskownicy Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2afd1-119">Then follow the steps in the [Get started in the Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="2afd1-120">Te kroki skonfigurować hasło SSH `root` konto i Ambari `admin` konta.</span><span class="sxs-lookup"><span data-stu-id="2afd1-120">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="2afd1-121">Te hasła są używane, gdy połączysz się piaskownicy w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2afd1-121">These passwords are used when you connect to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="2afd1-122">Połączenie narzędzi do piaskownicy</span><span class="sxs-lookup"><span data-stu-id="2afd1-122">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="2afd1-123">Otwórz program Visual Studio, wybierz **widoku**, a następnie wybierz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="2afd1-124">Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy **HDInsight** wpis, a następnie wybierz **Połącz z emulatora HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-124">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![Zrzut ekranu z Eksploratora serwera, z Połącz z emulatora HDInsight wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="2afd1-126">Z **Połącz z emulatora HDInsight** okna dialogowego wprowadź hasło, które są skonfigurowane dla narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="2afd1-126">From the **Connect to HDInsight Emulator** dialog box, enter the password that you configured for Ambari.</span></span>

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją pole tekstowe hasła](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="2afd1-128">Wybierz **dalej** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="2afd1-128">Select **Next** to continue.</span></span>

4. <span data-ttu-id="2afd1-129">Użyj **hasło** pole hasło skonfigurowane dla `root` konta.</span><span class="sxs-lookup"><span data-stu-id="2afd1-129">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="2afd1-130">Pozostaw pola wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="2afd1-130">Leave the other fields at the default value.</span></span>

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją pole tekstowe hasła](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="2afd1-132">Wybierz **dalej** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="2afd1-132">Select **Next** to continue.</span></span>

5. <span data-ttu-id="2afd1-133">Poczekaj, aż weryfikacji usług, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="2afd1-133">Wait for validation of the services to finish.</span></span> <span data-ttu-id="2afd1-134">W niektórych przypadkach sprawdzanie poprawności może zakończyć się niepowodzeniem i monit o zaktualizowanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2afd1-134">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="2afd1-135">Jeśli weryfikacja zakończy się niepowodzeniem, wybierz **aktualizacji**i zaczekaj, aż konfiguracji i weryfikacji dla usługi zakończyć.</span><span class="sxs-lookup"><span data-stu-id="2afd1-135">If validation fails, select **Update**, and wait for the configuration and verification for the service to finish.</span></span>

    ![Zrzut ekranu przedstawiający okno dialogowe z wyróżnionym przycisku Aktualizuj](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="2afd1-137">Proces aktualizacji używa narzędzia Ambari, aby zmodyfikować konfigurację piaskownicy Hortonworks do czego oczekuje się przy użyciu usługi Data Lake tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2afd1-137">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="2afd1-138">Po zakończeniu sprawdzania poprawności, wybierz **Zakończ** aby zakończyć konfigurację.</span><span class="sxs-lookup"><span data-stu-id="2afd1-138">After validation has finished, select **Finish** to complete configuration.</span></span>
    <span data-ttu-id="2afd1-139">![Zrzut ekranu przedstawiający okno dialogowe z wyróżnioną pozycją przycisk Zakończ](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="2afd1-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="2afd1-140">W zależności od szybkości środowiska projektowego i ilość pamięci przydzielonej do maszyny wirtualnej może upłynąć kilka minut, aby skonfigurować i zweryfikować usług.</span><span class="sxs-lookup"><span data-stu-id="2afd1-140">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="2afd1-141">Po wykonaniu tych kroków, masz teraz **lokalnego klastra usługi HDInsight** wpis w Eksploratorze serwera w obszarze **HDInsight** sekcji.</span><span class="sxs-lookup"><span data-stu-id="2afd1-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under the **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="2afd1-142">Napisz zapytanie Hive</span><span class="sxs-lookup"><span data-stu-id="2afd1-142">Write a Hive query</span></span>

<span data-ttu-id="2afd1-143">Gałąź zapewnia języka przypominającego SQL kwerendy (HiveQL) do pracy z danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="2afd1-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="2afd1-144">Wykonaj następujące kroki, aby dowiedzieć się, jak do wykonywania kwerend na żądanie do klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2afd1-144">Use the following steps to learn how to run on-demand queries against the local cluster.</span></span>

1. <span data-ttu-id="2afd1-145">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy wpis dla klastra lokalnego dodanego wcześniej, a następnie wybierz **Napisz zapytanie Hive**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-145">In **Server Explorer**, right-click the entry for the local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Zrzut ekranu z Eksploratora serwera zapisu wyróżnione zapytanie Hive](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="2afd1-147">Pojawi się okno nowego zapytania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-147">A new query window appears.</span></span> <span data-ttu-id="2afd1-148">W tym miejscu można szybko zapisu i przesłać zapytanie z lokalnym klastrem.</span><span class="sxs-lookup"><span data-stu-id="2afd1-148">Here you can quickly write and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="2afd1-149">W nowym oknie zapytania wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2afd1-149">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="2afd1-150">Aby uruchomić zapytanie, zaznacz **przesyłania** w górnej części okna.</span><span class="sxs-lookup"><span data-stu-id="2afd1-150">To run the query, select **Submit** at the top of the window.</span></span> <span data-ttu-id="2afd1-151">Pozostaw inne wartości (**partii** i nazwa serwera) na wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="2afd1-151">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![Zrzut ekranu okna zapytań, przycisk Prześlij wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="2afd1-153">Umożliwia także menu rozwijanym obok pozycji **przesyłania** wybierz **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-153">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="2afd1-154">Zaawansowane opcje umożliwiają udostępniają dodatkowe opcje podczas przesyłania zadania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-154">Advanced options allow you to provide additional options when you submit the job.</span></span>

    ![Zrzut ekranu przedstawia skryptu, okno dialogowe](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="2afd1-156">Po przesłaniu zapytania, zostanie wyświetlony stan zadania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-156">After you submit the query, the job status appears.</span></span> <span data-ttu-id="2afd1-157">Stan zadania Wyświetla informacje o zadaniu jest przetwarzany przez Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2afd1-157">The job status displays information about the job as it is processed by Hadoop.</span></span> <span data-ttu-id="2afd1-158">**Stan zadania** zawiera informacje o stanie zadania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-158">**Job State** provides the status of the job.</span></span> <span data-ttu-id="2afd1-159">Stan jest okresowo aktualizowana, lub można ręcznie odświeżyć stan ikony odświeżania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-159">The state is updated periodically, or you can use the refresh icon to refresh the state manually.</span></span>

    ![Okno dialogowe zrzut ekranu widoku zadania, z wyróżnioną pozycją stan zadania](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="2afd1-161">Po **stan zadania** zmienia się na **zakończone**, zostanie wyświetlony skierowany acykliczne Graph (DAG).</span><span class="sxs-lookup"><span data-stu-id="2afd1-161">After the **Job State** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="2afd1-162">Ten schemat przedstawia ścieżka wykonywania określonej przez Tez podczas przetwarzania zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="2afd1-162">This diagram describes the execution path that was determined by Tez when processing the Hive query.</span></span> <span data-ttu-id="2afd1-163">Tez jest domyślny aparat wykonywania gałęzi w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2afd1-163">Tez is the default execution engine for Hive on the local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2afd1-164">Tez jest to wartość domyślna, korzystając z klastrów usługi HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="2afd1-164">Tez is also the default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2afd1-165">Nie jest domyślnie w usłudze HDInsight z systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2afd1-165">It is not the default on Windows-based HDInsight.</span></span> <span data-ttu-id="2afd1-166">Aby go użyć, należy dodać wiersz `set hive.execution.engine = tez;` na początku zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="2afd1-166">To use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="2afd1-167">Użyj **dane wyjściowe zadania** łącze, aby wyświetlić dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2afd1-167">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="2afd1-168">W takim przypadku jest 823, liczbę wierszy w tabeli sample_08.</span><span class="sxs-lookup"><span data-stu-id="2afd1-168">In this case, it is 823, the number of rows in the sample_08 table.</span></span> <span data-ttu-id="2afd1-169">Można wyświetlić informacje diagnostyczne o zadaniu przy użyciu **dziennik zadań** i **Pobierz dziennik YARN** łącza.</span><span class="sxs-lookup"><span data-stu-id="2afd1-169">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="2afd1-170">Można również uruchamiać zadania Hive interaktywnego, zmieniając **partii** do **Interactive**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-170">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**.</span></span> <span data-ttu-id="2afd1-171">Następnie wybierz **Execute**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-171">Then select **Execute**.</span></span>

    ![Zrzut ekranu interakcyjne i wykonywanie przycisków wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="2afd1-173">Interakcyjne zapytania strumieni dziennika dane wyjściowe, generowane podczas przetwarzania na **danych wyjściowych serwera HiveServer2** okna.</span><span class="sxs-lookup"><span data-stu-id="2afd1-173">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2afd1-174">Informacje są takie same, który jest dostępny z **dziennik zadań** link po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-174">The information is the same that is available from the **Job Log** link after a job has finished.</span></span>

    ![Zrzut ekranu przedstawiający pliku dziennika](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="2afd1-176">Utwórz projekt Hive</span><span class="sxs-lookup"><span data-stu-id="2afd1-176">Create a Hive project</span></span>

<span data-ttu-id="2afd1-177">Można również utworzyć projekt, który zawiera wiele skryptów Hive.</span><span class="sxs-lookup"><span data-stu-id="2afd1-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="2afd1-178">Użyj projektu, jeśli pokrewne skrypty lub przechowywania skryptów w systemie kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="2afd1-178">Use a project when you have related scripts or want to store scripts in a version control system.</span></span>

1. <span data-ttu-id="2afd1-179">W programie Visual Studio, wybierz **pliku**, **nowy**, a następnie **projektu**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="2afd1-180">Z listy projektów, rozwiń węzeł **szablony**, rozwiń węzeł **usługi Azure Data Lake**, a następnie wybierz **gałąź (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-180">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="2afd1-181">Wybierz z listy szablonów **Hive próbki**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-181">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="2afd1-182">Wprowadź nazwę i lokalizację, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-182">Enter a name and location, and then select **OK**.</span></span>

    ![Wyróżnione okno zrzut ekranu nowego projektu, przy użyciu usługi Azure Data Lake, HIVE, przykładowe Hive i OK](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="2afd1-184">**Hive próbki** projekt zawiera dwa skrypty **WebLogAnalysis.hql** i **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-184">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="2afd1-185">Skrypty te można przesłać za pomocą takie same **przesyłania** u góry okna.</span><span class="sxs-lookup"><span data-stu-id="2afd1-185">You can submit these scripts by using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="2afd1-186">Utwórz projekt usługi Pig</span><span class="sxs-lookup"><span data-stu-id="2afd1-186">Create a Pig project</span></span>

<span data-ttu-id="2afd1-187">Gałąź zawiera języka przypominającego SQL do pracy z danych strukturalnych, natomiast Pig działanie polega na przekształcenia danych.</span><span class="sxs-lookup"><span data-stu-id="2afd1-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="2afd1-188">Pig zapewnia umożliwia tworzenie potoku transformacji języka (Pig Latin).</span><span class="sxs-lookup"><span data-stu-id="2afd1-188">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="2afd1-189">Aby korzystanie z języka Pig z lokalnym klastrem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2afd1-189">To use Pig with the local cluster, follow these steps:</span></span>

1. <span data-ttu-id="2afd1-190">Otwórz program Visual Studio i wybierz **pliku**, **nowy**, a następnie **projektu**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="2afd1-191">Z listy projektów, rozwiń węzeł **szablony**, rozwiń węzeł **usługi Azure Data Lake**, a następnie wybierz **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-191">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="2afd1-192">Wybierz z listy szablonów **aplikacji Pig**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-192">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="2afd1-193">Wprowadź nazwę lokalizacji, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-193">Enter a name, location, and then select **OK**.</span></span>

    ![Okno zrzut ekranu nowego projektu, przy użyciu usługi Azure Data Lake, Pig, Pig, aplikacji i OK, wyróżniony](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="2afd1-195">Wprowadź następujący tekst jako zawartość **script.pig** pliku, który został utworzony z tego projektu.</span><span class="sxs-lookup"><span data-stu-id="2afd1-195">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

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

    <span data-ttu-id="2afd1-196">Pig używa innego języka niż Hive, sposób uruchamiania zadania jest jednolita obu językach za pośrednictwem **przesyłania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2afd1-196">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages, through the **Submit** button.</span></span> <span data-ttu-id="2afd1-197">Wybieranie listy rozwijanej obok **przesyłania** Wyświetla okno dialogowe Zaawansowane przesyłania programu Pig.</span><span class="sxs-lookup"><span data-stu-id="2afd1-197">Selecting the drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Zrzut ekranu przedstawia skryptu, okno dialogowe](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="2afd1-199">Stan zadania i dane wyjściowe będzie również wyświetlana, taka sama jak zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="2afd1-199">The job status and output is also displayed, the same as a Hive query.</span></span>

    ![Zrzut ekranu przedstawiający zakończonych zadań Pig](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="2afd1-201">Wyświetl zadania</span><span class="sxs-lookup"><span data-stu-id="2afd1-201">View jobs</span></span>

<span data-ttu-id="2afd1-202">Narzędzia Data Lake umożliwiają również łatwe wyświetlanie informacji o zadaniach, które zostały uruchomione na platformie Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2afd1-202">Data Lake tools also allow you to easily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="2afd1-203">Wykonaj następujące kroki, aby wyświetlić zadania, które zostały uruchomione w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2afd1-203">Use the following steps to see the jobs that have been run on the local cluster.</span></span>

1. <span data-ttu-id="2afd1-204">Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy klaster lokalny, a następnie wybierz **Wyświetl zadania**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-204">From **Server Explorer**, right-click the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="2afd1-205">Zostanie wyświetlona lista zadań, które zostały przesłane do klastra.</span><span class="sxs-lookup"><span data-stu-id="2afd1-205">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![Zrzut ekranu z Eksploratora serwera, z wyróżnioną pozycją zadaniami widoku](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="2afd1-207">Z listy zadań wybierz jedną, aby wyświetlić szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="2afd1-207">From the list of jobs, select one to view the job details.</span></span>

    ![Zrzut ekranu z zadania przeglądarki, z jednym z wyróżnionym zadania](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="2afd1-209">Informacje wyświetlane jest podobne do zostanie wyświetlony po uruchomieniu zapytania Hive i Pig, oraz łącza do wyświetlania danych wyjściowych i rejestrowania informacji.</span><span class="sxs-lookup"><span data-stu-id="2afd1-209">The information displayed is similar to what you see after running a Hive or Pig query, including links to view the output and log information.</span></span>

3. <span data-ttu-id="2afd1-210">Można również zmodyfikować i ponownie prześlij zadanie w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2afd1-210">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="2afd1-211">Wyświetl Hive baz danych</span><span class="sxs-lookup"><span data-stu-id="2afd1-211">View Hive databases</span></span>

1. <span data-ttu-id="2afd1-212">W **Eksploratora serwera**, rozwiń węzeł **lokalnego klastra usługi HDInsight** wpis, a następnie rozwiń węzeł **bazy danych programu Hive**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-212">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="2afd1-213">**Domyślne** i **xademo** są wyświetlane bazy danych w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2afd1-213">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="2afd1-214">Rozszerzanie bazy danych zawiera tabele w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2afd1-214">Expanding a database shows the tables within the database.</span></span>

    ![Zrzut ekranu Eksploratora serwera z bazami danych rozwinięty](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="2afd1-216">Rozszerzanie tabeli są wyświetlane dla tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2afd1-216">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="2afd1-217">Aby szybko wyświetlić dane, kliknij prawym przyciskiem myszy tabelę, a następnie wybierz **Wyświetl pierwszych 100 wierszy**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-217">To quickly view the data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Zrzut ekranu z Eksploratora serwera, z tabeli rozwinięty i Wyświetl pierwszych 100 wierszy wybrane](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="2afd1-219">Właściwości bazy danych i tabeli</span><span class="sxs-lookup"><span data-stu-id="2afd1-219">Database and table properties</span></span>

<span data-ttu-id="2afd1-220">Można wyświetlić właściwości bazy danych lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="2afd1-220">You can view the properties of a database or table.</span></span> <span data-ttu-id="2afd1-221">Wybieranie **właściwości** Wyświetla szczegóły wybranego elementu w oknie właściwości.</span><span class="sxs-lookup"><span data-stu-id="2afd1-221">Selecting **Properties** displays details for the selected item in the properties window.</span></span> <span data-ttu-id="2afd1-222">Na przykład zapoznaj się z informacjami pokazano na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2afd1-222">For example, see the information shown in the following screenshot:</span></span>

![Zrzut ekranu właściwości okna](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="2afd1-224">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="2afd1-224">Create a table</span></span>

<span data-ttu-id="2afd1-225">Aby utworzyć tabelę, kliknij prawym przyciskiem myszy bazę danych, a następnie wybierz **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="2afd1-225">To create a table, right-click a database, and then select **Create Table**.</span></span>

![Zrzut ekranu z Eksploratora serwera, z Create Table wyróżnione](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="2afd1-227">Następnie można utworzyć tabeli za pomocą formularza.</span><span class="sxs-lookup"><span data-stu-id="2afd1-227">You can then create the table using a form.</span></span> <span data-ttu-id="2afd1-228">Na dole Poniższy zrzut ekranu widać HiveQL raw, który jest używany do tworzenia tabeli.</span><span class="sxs-lookup"><span data-stu-id="2afd1-228">At the bottom of the following screenshot, you can see the raw HiveQL that is used to create the table.</span></span>

![Zrzut ekranu przedstawiający formularz używany do tworzenia tabeli](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="2afd1-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2afd1-230">Next steps</span></span>

* [<span data-ttu-id="2afd1-231">Learning liny piaskownicy Hortonworks</span><span class="sxs-lookup"><span data-stu-id="2afd1-231">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="2afd1-232">Samouczek Hadoop — wprowadzenie HDP</span><span class="sxs-lookup"><span data-stu-id="2afd1-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
