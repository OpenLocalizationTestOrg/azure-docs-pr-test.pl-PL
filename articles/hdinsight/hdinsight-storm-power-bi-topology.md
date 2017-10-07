---
title: "aaaUse Apache Storm w usłudze Power BI - Azure HDInsight | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="81aa8-103">Użyj usługi Power BI toovisualize danych od topologii Apache Storm</span><span class="sxs-lookup"><span data-stu-id="81aa8-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="81aa8-104">Usługa Power BI umożliwia toovisually Wyświetl dane jako raporty.</span><span class="sxs-lookup"><span data-stu-id="81aa8-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="81aa8-105">Ten dokument zawiera przykładowy sposób toouse Apache Storm na HDInsight toogenerate danych dla usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="81aa8-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="81aa8-106">Witaj kroki opisane w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81aa8-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="81aa8-107">Hello skompilowany projekt może być przesłane tooa opartych na systemie Linux klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="81aa8-108">Tylko opartych na systemie Linux klastrów utworzone po 10/28/2016 Obsługa SCP.NET topologii.</span><span class="sxs-lookup"><span data-stu-id="81aa8-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="81aa8-109">toouse topologii C# z opartą na systemie Linux klastrem, hello aktualizacji pakietu Microsoft.SCP.Net.SDK NuGet używana przez tooversion Twojego projektu 0.10.0.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="81aa8-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="81aa8-110">Hello wersję pakietu hello musi być również zgodna wersja główna hello Storm zainstalowany w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="81aa8-111">Na przykład system Storm występujący w usłudze HDInsight w wersjach 3.3 i 3.4 jest w wersji 0.10.x, a usługa HDInsight 3.5 używa systemu Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="81aa8-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="81aa8-112">Topologie języka C# w klastrach opartych na systemie Linux należy użyć .NET 4.5 i użyj Mono toorun na powitania klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="81aa8-113">Większość elementów pracy.</span><span class="sxs-lookup"><span data-stu-id="81aa8-113">Most things work.</span></span> <span data-ttu-id="81aa8-114">Należy jednak sprawdzić hello [zgodności Mono](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.</span><span class="sxs-lookup"><span data-stu-id="81aa8-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="81aa8-115">Wersja języka Java tego projektu, który współpracuje z usługą HDInsight opartą na systemie Linux lub z systemem Windows, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="81aa8-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81aa8-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="81aa8-116">Prerequisites</span></span>

* <span data-ttu-id="81aa8-117">Użytkownik usługi Azure Active Directory z [usługi Power BI](https://powerbi.com) dostępu.</span><span class="sxs-lookup"><span data-stu-id="81aa8-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="81aa8-118">Klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-118">An HDInsight cluster.</span></span> <span data-ttu-id="81aa8-119">Aby uzyskać więcej informacji, zobacz [wprowadzenie Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="81aa8-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="81aa8-120">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="81aa8-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="81aa8-121">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="81aa8-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="81aa8-122">Visual Studio (jedna hello następujące wersje)</span><span class="sxs-lookup"><span data-stu-id="81aa8-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="81aa8-123">Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="81aa8-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="81aa8-124">Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="81aa8-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="81aa8-125">Program Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="81aa8-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="81aa8-126">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="81aa8-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="81aa8-127">Witaj narzędzia HDInsight Tools for Visual Studio: zobacz [rozpocząć korzystanie z hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) uzyskać informacji o informacje dotyczące instalacji.</span><span class="sxs-lookup"><span data-stu-id="81aa8-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="81aa8-128">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="81aa8-128">How it works</span></span>

<span data-ttu-id="81aa8-129">Ten przykład zawiera topologii Storm C# losowo generowany danych dziennika usług Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="81aa8-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="81aa8-130">Te dane są następnie zapisywane tooa bazy danych SQL i tam jest używane toogenerate raporty w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="81aa8-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="81aa8-131">Witaj następujące główne funkcje hello wdrożenie plików w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="81aa8-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="81aa8-132">**SqlAzureBolt.cs**: zapisuje informacje wygenerowane w tooSQL topologii Storm hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="81aa8-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="81aa8-133">**IISLogsTable.sql**: hello języka Transact-SQL instrukcje używane toogenerate hello bazy danych, która hello dane są przechowywane w.</span><span class="sxs-lookup"><span data-stu-id="81aa8-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="81aa8-134">Utwórz tabelę hello w bazie danych SQL, przed rozpoczęciem powitalne topologii w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="81aa8-135">Pobierz przykład Witaj</span><span class="sxs-lookup"><span data-stu-id="81aa8-135">Download hello example</span></span>

<span data-ttu-id="81aa8-136">Pobierz hello [przykład HDInsight C# Storm usługi Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="81aa8-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="81aa8-137">toodownload, albo rozwidlenia/klonowania za pomocą [git](http://git-scm.com/), lub użyj hello **Pobierz** toodownload łącze .zip hello archiwum.</span><span class="sxs-lookup"><span data-stu-id="81aa8-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="81aa8-138">Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="81aa8-138">Create a database</span></span>

1. <span data-ttu-id="81aa8-139">toocreate bazy danych, wykonaj kroki hello w hello [samouczek usługi SQL Database](../sql-database/sql-database-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="81aa8-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="81aa8-140">Bazy danych toohello Połącz przez hello następujące kroki w hello [połączyć tooa bazy danych SQL z programem Visual Studio](../sql-database/sql-database-connect-query.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="81aa8-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="81aa8-141">W Eksploratorze obiektów kliknij prawym przyciskiem myszy hello bazy danych, a następnie wybierz **nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="81aa8-142">Wklej zawartość hello hello **IISLogsTable.sql** dołączony hello pobrany projekt w oknie zapytania hello, a następnie użyj klawiszy Ctrl + Shift + E tooexecute hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="81aa8-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="81aa8-143">Wiadomość hello polecenia zakończyła się pomyślnie, powinien zostać wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="81aa8-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="81aa8-144">Konfigurowanie przykładowej hello</span><span class="sxs-lookup"><span data-stu-id="81aa8-144">Configure hello sample</span></span>

1. <span data-ttu-id="81aa8-145">Z hello [portalu Azure](https://portal.azure.com), wybierz bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="81aa8-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="81aa8-146">Z hello **Essentials** sekcji hello SQL bloku bazy danych, wybierz opcję **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="81aa8-147">Na wyświetlonej liście hello skopiuj hello **ADO.NET (uwierzytelnianie SQL)** informacji.</span><span class="sxs-lookup"><span data-stu-id="81aa8-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="81aa8-148">Przykład Witaj Otwórz w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81aa8-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="81aa8-149">Z **Eksploratora rozwiązań**, otwórz hello **App.config** pliku, a następnie znajdź hello wejścia:</span><span class="sxs-lookup"><span data-stu-id="81aa8-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="81aa8-150">Zastąp hello **TOBEFILLED ##** wartości z ciągu połączenia bazy danych hello skopiowany w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="81aa8-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="81aa8-151">Zastąp **{Twojej\_username}** i **{Twojej\_hasło}** hello nazwy użytkownika i hasło na powitania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="81aa8-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="81aa8-152">Zapisz i zamknij hello plików.</span><span class="sxs-lookup"><span data-stu-id="81aa8-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="81aa8-153">Wdrażanie przykładowej hello</span><span class="sxs-lookup"><span data-stu-id="81aa8-153">Deploy hello sample</span></span>

1. <span data-ttu-id="81aa8-154">Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **StormToSQL** projekt i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="81aa8-155">Wybierz hello klastra usługi HDInsight z hello **klaster Storm** okna dialogowego z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="81aa8-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="81aa8-156">Może to potrwać kilka sekund na powitania **klaster Storm** toopopulate listy rozwijanej o nazwy serwerów.</span><span class="sxs-lookup"><span data-stu-id="81aa8-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="81aa8-157">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="81aa8-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="81aa8-158">Jeśli masz więcej niż jedną subskrypcję, zaloguj się za toohello, który zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="81aa8-159">Po przesłaniu topologii hello hello __podglądu topologii__ pojawi się.</span><span class="sxs-lookup"><span data-stu-id="81aa8-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="81aa8-160">tooview tej topologii, wybierz hello SqlAzureWriterTopology wpisu z listy hello.</span><span class="sxs-lookup"><span data-stu-id="81aa8-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![topologie Hello, z topologią hello wybrane](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="81aa8-162">Można użyć tego widoku toosee informacji na temat topologii hello, lub kliknij dwukrotnie wpis (na przykład hello SqlAzureBolt) toosee informacji tooa określonego składnika w topologii hello.</span><span class="sxs-lookup"><span data-stu-id="81aa8-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="81aa8-163">Po hello topologii ma był uruchamiany przez kilka minut, oknie zapytania SQL zwracany toohello używane toocreate hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="81aa8-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="81aa8-164">Zastąp istniejące instrukcje hello hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="81aa8-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="81aa8-165">Użyj klawiszy Ctrl + Shift + E tooexecute hello zapytania, a powinien zostać wyświetlony wyniki toohello podobne następujące dane:</span><span class="sxs-lookup"><span data-stu-id="81aa8-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="81aa8-166">Te dane od topologii Storm hello została zapisana.</span><span class="sxs-lookup"><span data-stu-id="81aa8-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="81aa8-167">Tworzenie raportu</span><span class="sxs-lookup"><span data-stu-id="81aa8-167">Create a report</span></span>

1. <span data-ttu-id="81aa8-168">Połącz toohello [łącznika usługi Azure SQL Database](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) dla usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="81aa8-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="81aa8-169">W ramach **baz danych**, wybierz pozycję **uzyskać**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="81aa8-170">Wybierz **bazy danych SQL Azure**, a następnie wybierz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="81aa8-171">Konieczne podanie toodownload hello Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="81aa8-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="81aa8-172">Jeśli tak, użyj powitania po tooconnect kroki:</span><span class="sxs-lookup"><span data-stu-id="81aa8-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="81aa8-173">Otwórz Power BI Desktop i wybierz __Pobierz dane__.</span><span class="sxs-lookup"><span data-stu-id="81aa8-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="81aa8-174">Wybierz 2 __Azure__, a następnie __bazy danych Azure SQL__.</span><span class="sxs-lookup"><span data-stu-id="81aa8-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="81aa8-175">Wprowadź hello informacji tooconnect tooyour bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="81aa8-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="81aa8-176">Te informacje można znaleźć na stronie powitania [portalu Azure](https://portal.azure.com) i wybrać bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="81aa8-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="81aa8-177">Można również ustawić interwał odświeżania hello i filtry niestandardowe przy użyciu **włączyć zaawansowane opcje** hello Połącz okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81aa8-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="81aa8-178">Po nawiązaniu połączenia, pojawi się nowy zestaw danych z hello takie same nazwy jako hello bazy danych zostanie połączony.</span><span class="sxs-lookup"><span data-stu-id="81aa8-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="81aa8-179">Wybierz toobegin dataset hello projektowania raportu.</span><span class="sxs-lookup"><span data-stu-id="81aa8-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="81aa8-180">Z **pola**, rozwiń węzeł hello **IISLOGS** wpisu.</span><span class="sxs-lookup"><span data-stu-id="81aa8-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="81aa8-181">toocreate raport, że listy hello URI wynika, zaznacz pole wyboru powitania dla **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Tworzenie raportu](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="81aa8-183">Następnie przeciągnij **metody** toohello raportu.</span><span class="sxs-lookup"><span data-stu-id="81aa8-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="81aa8-184">Witaj raport aktualizacje toolist Witaj wynika i hello odpowiedniej metody HTTP używany do hello żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="81aa8-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![Dodawanie hello danych — metoda](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="81aa8-186">Z hello **wizualizacje** kolumnę, wybierz hello **pola** ikonę, a następnie wybierz hello Strzałka w dół obok zbyt**— metoda** w hello **wartości**sekcji.</span><span class="sxs-lookup"><span data-stu-id="81aa8-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="81aa8-187">Wybierz toodisplay uzyskaniu liczba ile razy identyfikatora URI **liczba**.</span><span class="sxs-lookup"><span data-stu-id="81aa8-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Zmiana liczby tooa metod](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="81aa8-189">Następnie wybierz pozycję hello **skumulowany wykres kolumnowy** toochange sposób wyświetlania informacji hello.</span><span class="sxs-lookup"><span data-stu-id="81aa8-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Zmiana tooa skumulowany wykres.](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="81aa8-191">toosave hello raportu, wybierz opcję **zapisać** , a następnie wprowadź nazwę raportu hello.</span><span class="sxs-lookup"><span data-stu-id="81aa8-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="81aa8-192">Zatrzymywanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="81aa8-192">Stop hello topology</span></span>

<span data-ttu-id="81aa8-193">toorun topologii Hello będzie nadal występował, zatrzymaj ją lub usunąć hello Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81aa8-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="81aa8-194">toostop hello topologii, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="81aa8-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="81aa8-195">W programie Visual Studio wróć toohello topologii Podgląd i wybierz hello topologii.</span><span class="sxs-lookup"><span data-stu-id="81aa8-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="81aa8-196">Wybierz hello **Kill** przycisk toostop hello topologii.</span><span class="sxs-lookup"><span data-stu-id="81aa8-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kasowanie przycisk w topologii hello podsumowania](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="81aa8-198">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="81aa8-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="81aa8-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="81aa8-199">Next steps</span></span>

<span data-ttu-id="81aa8-200">W tym dokumencie przedstawiono sposób toosend danych z tooSQL topologii Storm bazy danych, następnie wizualizacji danych hello przy użyciu usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="81aa8-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="81aa8-201">Aby uzyskać informacje na temat toowork z innymi technologiami Azure za pomocą Storm w usłudze HDInsight, zobacz następujące dokumentu hello:</span><span class="sxs-lookup"><span data-stu-id="81aa8-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="81aa8-202">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="81aa8-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
