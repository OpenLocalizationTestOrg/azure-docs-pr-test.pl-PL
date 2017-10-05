---
title: "Apache Storm za pomocą usługi Power BI — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Tworzenie raportu usługi Power BI przy użyciu danych z topologii C# uruchomiona w klastrze Apache Storm w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="a8383-103">Wizualizuj dane z topologii Apache Storm przy użyciu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="a8383-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="a8383-104">Usługa Power BI pozwala wizualnie wyświetlanie danych w postaci raportów.</span><span class="sxs-lookup"><span data-stu-id="a8383-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="a8383-105">Ten dokument zawiera przykładowy sposób użycia systemu Apache Storm w usłudze HDInsight można wygenerować danych do usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="a8383-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="a8383-106">Kroki opisane w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8383-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="a8383-107">Skompilowany projekt może zostać przesłane do klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a8383-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a8383-108">Tylko opartych na systemie Linux klastrów utworzone po 10/28/2016 Obsługa SCP.NET topologii.</span><span class="sxs-lookup"><span data-stu-id="a8383-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="a8383-109">Aby używać topologii C# z klastrem opartych na systemie Linux, należy zaktualizować pakiet Microsoft.SCP.Net.SDK NuGet używanych w projekcie do wersji 0.10.0.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a8383-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="a8383-110">Wersja pakietu musi być również zgodna z wersją główną systemu Storm zainstalowanego w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="a8383-111">Na przykład system Storm występujący w usłudze HDInsight w wersjach 3.3 i 3.4 jest w wersji 0.10.x, a usługa HDInsight 3.5 używa systemu Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="a8383-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="a8383-112">Topologie C# w klastrach opartych na systemie Linux muszą korzystać z platformy .NET 4.5 i używać platformy Mono, aby mogły działać w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="a8383-113">Większość elementów pracy.</span><span class="sxs-lookup"><span data-stu-id="a8383-113">Most things work.</span></span> <span data-ttu-id="a8383-114">Należy jednak sprawdzić [zgodności Mono](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.</span><span class="sxs-lookup"><span data-stu-id="a8383-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="a8383-115">Wersja języka Java tego projektu, który współpracuje z usługą HDInsight opartą na systemie Linux lub z systemem Windows, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8383-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a8383-116">Prerequisites</span></span>

* <span data-ttu-id="a8383-117">Użytkownik usługi Azure Active Directory z [usługi Power BI](https://powerbi.com) dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8383-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="a8383-118">Klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-118">An HDInsight cluster.</span></span> <span data-ttu-id="a8383-119">Aby uzyskać więcej informacji, zobacz [wprowadzenie Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a8383-120">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="a8383-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a8383-121">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="a8383-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="a8383-122">Visual Studio (jedna z następujących wersji)</span><span class="sxs-lookup"><span data-stu-id="a8383-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="a8383-123">Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="a8383-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="a8383-124">Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="a8383-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="a8383-125">Program Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a8383-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="a8383-126">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="a8383-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="a8383-127">Narzędzia HDInsight Tools for Visual Studio: zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) uzyskać informacji o informacje dotyczące instalacji.</span><span class="sxs-lookup"><span data-stu-id="a8383-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a8383-128">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="a8383-128">How it works</span></span>

<span data-ttu-id="a8383-129">Ten przykład zawiera topologii Storm C# losowo generowany danych dziennika usług Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="a8383-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="a8383-130">Następnie napisano te dane do bazy danych SQL i tam jest używany do generowania raportów w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="a8383-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="a8383-131">Następujące pliki wdrożenia główne funkcje w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a8383-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="a8383-132">**SqlAzureBolt.cs**: zapisuje informacje wygenerowane w topologii Storm do bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a8383-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="a8383-133">**IISLogsTable.sql**: instrukcji języka Transact-SQL używanego do generowania danych przechowywanych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a8383-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="a8383-134">Tworzenie tabeli w bazie danych SQL, przed rozpoczęciem topologii w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="a8383-135">Pobierz przykład</span><span class="sxs-lookup"><span data-stu-id="a8383-135">Download the example</span></span>

<span data-ttu-id="a8383-136">Pobierz [przykład HDInsight C# Storm usługi Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="a8383-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="a8383-137">Aby go pobrać, albo rozwidlenia/klonowania za pomocą [git](http://git-scm.com/), lub użyj **Pobierz** łącze, aby pobrać .zip archiwum.</span><span class="sxs-lookup"><span data-stu-id="a8383-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="a8383-138">Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="a8383-138">Create a database</span></span>

1. <span data-ttu-id="a8383-139">Aby utworzyć bazę danych, wykonaj czynności w [samouczek usługi SQL Database](../sql-database/sql-database-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a8383-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="a8383-140">Połącz z bazą danych, wykonując kroki opisane w [nawiązywanie połączenia z bazą danych SQL z programem Visual Studio](../sql-database/sql-database-connect-query.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a8383-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="a8383-141">W Eksploratorze obiektów kliknij prawym przyciskiem myszy bazę danych, a następnie wybierz **nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="a8383-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="a8383-142">Wklej zawartość **IISLogsTable.sql** plik dołączony do projektu pobrany do okna zapytania, a następnie użyć Ctrl + Shift + E do wykonania zapytania.</span><span class="sxs-lookup"><span data-stu-id="a8383-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="a8383-143">Powinien zostać wyświetlony komunikat pomyślnie ukończyć polecenia.</span><span class="sxs-lookup"><span data-stu-id="a8383-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="a8383-144">Konfigurowanie przykładowej</span><span class="sxs-lookup"><span data-stu-id="a8383-144">Configure the sample</span></span>

1. <span data-ttu-id="a8383-145">Z [portalu Azure](https://portal.azure.com), wybierz bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a8383-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="a8383-146">Z **Essentials** części bloku bazy danych SQL, wybierz opcję **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="a8383-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="a8383-147">Na liście Skopiuj **ADO.NET (uwierzytelnianie SQL)** informacji.</span><span class="sxs-lookup"><span data-stu-id="a8383-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="a8383-148">Otwórz próbki w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8383-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="a8383-149">Z **Eksploratora rozwiązań**, otwórz **App.config** pliku, a następnie znajdź następujący wpis:</span><span class="sxs-lookup"><span data-stu-id="a8383-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="a8383-150">Zastąp **TOBEFILLED ##** wartości z ciągu połączenia bazy danych skopiowany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a8383-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="a8383-151">Zastąp **{Twojej\_username}** i **{Twojej\_hasło}** przy użyciu nazwy użytkownika i hasła dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8383-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="a8383-152">Zapisz i zamknij plik.</span><span class="sxs-lookup"><span data-stu-id="a8383-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="a8383-153">Wdrażanie przykładowej</span><span class="sxs-lookup"><span data-stu-id="a8383-153">Deploy the sample</span></span>

1. <span data-ttu-id="a8383-154">Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **StormToSQL** projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a8383-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="a8383-155">Wybierz klaster usługi HDInsight z **klaster Storm** okna dialogowego z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a8383-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a8383-156">Może potrwać kilka sekund **klaster Storm** listy rozwijanej, aby umieścić nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="a8383-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="a8383-157">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a8383-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="a8383-158">Jeśli masz więcej niż jedną subskrypcję, zaloguj się za jedną, która zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="a8383-159">Po przesłaniu topologii __podglądu topologii__ pojawi się.</span><span class="sxs-lookup"><span data-stu-id="a8383-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="a8383-160">Aby wyświetlić tej topologii, wybierz wpis SqlAzureWriterTopology z listy.</span><span class="sxs-lookup"><span data-stu-id="a8383-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![Topologie, w przypadku topologii wybrane](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="a8383-162">Użyj tego widoku, aby wyświetlić informacje o topologii lub kliknij dwukrotnie wpis (na przykład SqlAzureBolt), aby wyświetlić informacje dotyczące składnika w topologii.</span><span class="sxs-lookup"><span data-stu-id="a8383-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="a8383-163">Po topologii był uruchamiany przez kilka minut, wróć do okna zapytania SQL używanego do utworzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8383-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="a8383-164">Zastąp istniejące instrukcje następujące zapytanie:</span><span class="sxs-lookup"><span data-stu-id="a8383-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="a8383-165">Użyj klawiszy Ctrl + Shift + E można wykonać zapytania, a powinien zostać wyświetlony wyniki podobne do następujących danych:</span><span class="sxs-lookup"><span data-stu-id="a8383-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="a8383-166">Te dane został zapisany od topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="a8383-167">Tworzenie raportu</span><span class="sxs-lookup"><span data-stu-id="a8383-167">Create a report</span></span>

1. <span data-ttu-id="a8383-168">Połączyć się z [łącznika usługi Azure SQL Database](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) dla usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="a8383-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="a8383-169">W ramach **baz danych**, wybierz pozycję **uzyskać**.</span><span class="sxs-lookup"><span data-stu-id="a8383-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="a8383-170">Wybierz **bazy danych SQL Azure**, a następnie wybierz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a8383-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8383-171">Może wystąpić konieczność pobrania Power BI Desktop, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="a8383-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="a8383-172">Jeśli tak, wykonaj następujące kroki, aby połączyć:</span><span class="sxs-lookup"><span data-stu-id="a8383-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="a8383-173">Otwórz Power BI Desktop i wybierz __Pobierz dane__.</span><span class="sxs-lookup"><span data-stu-id="a8383-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="a8383-174">Wybierz 2 __Azure__, a następnie __bazy danych Azure SQL__.</span><span class="sxs-lookup"><span data-stu-id="a8383-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="a8383-175">Wprowadź informacje do połączenia z bazą danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a8383-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="a8383-176">Te informacje można znaleźć, odwiedzając [portalu Azure](https://portal.azure.com) i wybrać bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a8383-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a8383-177">Należy również określić interwał odświeżania i filtry niestandardowe przy użyciu **włączyć zaawansowane opcje** z okna dialogowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="a8383-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="a8383-178">Po nawiązaniu połączenia, pojawi się nowy zestaw danych o takiej samej nazwie jako bazy danych, z którym połączenie.</span><span class="sxs-lookup"><span data-stu-id="a8383-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="a8383-179">Wybierz zestaw danych, aby rozpocząć projektowanie raportu.</span><span class="sxs-lookup"><span data-stu-id="a8383-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="a8383-180">Z **pola**, rozwiń węzeł **IISLOGS** wpisu.</span><span class="sxs-lookup"><span data-stu-id="a8383-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="a8383-181">Aby utworzyć raport zawierający listę łodyg identyfikatora URI, zaznacz pole wyboru **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="a8383-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Tworzenie raportu](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="a8383-183">Następnie przeciągnij **metody** do raportu.</span><span class="sxs-lookup"><span data-stu-id="a8383-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="a8383-184">Aktualizacje raport listy łodyg i odpowiedniej metody HTTP użytej dla żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8383-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![Dodawanie danych — metoda](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="a8383-186">Z **wizualizacje** wybierz opcję **pola** ikony, a następnie wybierz strzałkę w dół obok pozycji **— metoda** w **wartości** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a8383-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="a8383-187">Aby wyświetlić liczbę razy ile dostęp do identyfikatora URI, zaznacz **liczba**.</span><span class="sxs-lookup"><span data-stu-id="a8383-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Zmiana liczby metod](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="a8383-189">Następnie wybierz pozycję **skumulowany wykres kolumnowy** Aby zmienić sposób wyświetlania informacji.</span><span class="sxs-lookup"><span data-stu-id="a8383-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Zmiana na wykresach skumulowanych](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="a8383-191">Aby zapisać raport, wybierz **zapisać** i wprowadź nazwę dla raportu.</span><span class="sxs-lookup"><span data-stu-id="a8383-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="a8383-192">Zatrzymywanie topologii</span><span class="sxs-lookup"><span data-stu-id="a8383-192">Stop the topology</span></span>

<span data-ttu-id="a8383-193">Topologia jest nadal uruchomiona do momentu Zatrzymaj ją lub usunąć Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="a8383-194">Aby zatrzymać topologii, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8383-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="a8383-195">W programie Visual Studio wróć do podglądu topologii i wybierz topologii.</span><span class="sxs-lookup"><span data-stu-id="a8383-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="a8383-196">Wybierz **Kill** przycisk, aby zatrzymać topologii.</span><span class="sxs-lookup"><span data-stu-id="a8383-196">Select the **Kill** button to stop the topology.</span></span>

    ![Kasowanie przycisk w topologii podsumowania](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="a8383-198">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="a8383-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="a8383-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8383-199">Next steps</span></span>

<span data-ttu-id="a8383-200">W tym dokumencie przedstawiono sposób wysyłania danych z topologii Storm do bazy danych SQL, a następnie wizualizacji danych przy użyciu usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="a8383-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="a8383-201">Aby uzyskać informacje na temat pracy z innymi technologiami Azure za pomocą Storm w usłudze HDInsight zobacz następujący dokument:</span><span class="sxs-lookup"><span data-stu-id="a8383-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="a8383-202">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8383-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
