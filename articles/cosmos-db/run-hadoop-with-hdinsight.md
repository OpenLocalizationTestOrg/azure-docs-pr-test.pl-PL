---
title: "zadania aaaRun usługi Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania toorun proste Hive, Pig i MapReduce z bazy danych rozwiązania Cosmos Azure i usłudze Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="cbc19-103"><a name="Azure Cosmos DB-HDInsight"></a>Uruchom zadanie Apache Hive, Pig lub Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbc19-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="cbc19-104">W tym samouczku przedstawiono sposób toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], i [Apache Hadoop] [ apache-hadoop] Zadań MapReduce w usłudze Azure HDInsight z łącznikiem usługi Hadoop DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="cbc19-105">Łącznik usługi Hadoop rozwiązania cosmos w DB umożliwia tooact rozwiązania Cosmos bazy danych jako źródło i ujście zadań Hive, Pig i MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cbc19-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="cbc19-106">W tym samouczku będą używać rozwiązania Cosmos bazy danych jako hello danych źródłowym i docelowym zadania usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cbc19-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="cbc19-107">Po ukończeniu tego samouczka, będziesz w stanie tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="cbc19-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="cbc19-108">Jak załadować dane z rozwiązania Cosmos bazy danych przy użyciu zadania Hive, Pig lub MapReduce?</span><span class="sxs-lookup"><span data-stu-id="cbc19-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="cbc19-109">Sposób przechowywania danych w bazie danych rozwiązania Cosmos przy użyciu zadania Hive, Pig lub MapReduce?</span><span class="sxs-lookup"><span data-stu-id="cbc19-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="cbc19-110">Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym przeprowadzana za pomocą zadania Hive za pomocą rozwiązania Cosmos bazę danych i usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="cbc19-111">Następnie zwróć toothis artykułu, gdy otrzymasz hello pełne szczegóły na uruchamianie zadania usługi analiza danych DB rozwiązania Cosmos w.</span><span class="sxs-lookup"><span data-stu-id="cbc19-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="cbc19-112">Ten samouczek zakłada, że masz wcześniejszego doświadczenia w używaniu platformy Apache Hadoop, Hive i Pig.</span><span class="sxs-lookup"><span data-stu-id="cbc19-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="cbc19-113">Jeśli nowy tooApache Hadoop, Hive i Pig, zaleca się odwiedzenie hello [dokumentację Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="cbc19-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="cbc19-114">W tym samouczku przyjęto założenie, czy masz doświadczenie z rozwiązania Cosmos bazy danych, a konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="cbc19-115">Jeśli jesteś tooCosmos nowej bazy danych lub nie masz konta rozwiązania Cosmos bazy danych, można znaleźć na naszych [wprowadzenie] [ getting-started] strony.</span><span class="sxs-lookup"><span data-stu-id="cbc19-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="cbc19-116">Nie masz czasu toocomplete hello samouczka i po prostu chcesz skryptów programu PowerShell pełny przykład hello tooget Hive, Pig i MapReduce?</span><span class="sxs-lookup"><span data-stu-id="cbc19-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="cbc19-117">Nie ma problemu, pobierz je [tutaj][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="cbc19-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="cbc19-118">Pobieranie Hello zawiera również hello hql, pig i java pliki dla tych przykładów.</span><span class="sxs-lookup"><span data-stu-id="cbc19-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="cbc19-119"><a name="NewestVersion"></a>Najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="cbc19-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="cbc19-120">Wersja łącznika usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="cbc19-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="cbc19-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="cbc19-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="cbc19-122">Identyfikator Uri skryptu</span><span class="sxs-lookup"><span data-stu-id="cbc19-122">Script Uri</span></span></th>
        <td><span data-ttu-id="cbc19-123">https://portalcontent.blob.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="cbc19-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="cbc19-124">Data modyfikacji</span><span class="sxs-lookup"><span data-stu-id="cbc19-124">Date Modified</span></span></th>
        <td><span data-ttu-id="cbc19-125">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="cbc19-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="cbc19-126">HDInsight obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="cbc19-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="cbc19-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="cbc19-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="cbc19-128">Dziennik zmian</span><span class="sxs-lookup"><span data-stu-id="cbc19-128">Change Log</span></span></th>
        <td><span data-ttu-id="cbc19-129">Zaktualizowano rozwiązania Cosmos Azure DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="cbc19-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="cbc19-130">Dodano obsługę dla kolekcji partycjonowanych jako źródło i ujście</span><span class="sxs-lookup"><span data-stu-id="cbc19-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="cbc19-131"><a name="Prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cbc19-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="cbc19-132">Przed rozpoczęciem powitalne instrukcje w tym samouczku, upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="cbc19-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="cbc19-133">Konto rozwiązania Cosmos bazy danych, bazy danych i kolekcji dokumentów wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="cbc19-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="cbc19-134">Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych rozwiązania Cosmos][getting-started].</span><span class="sxs-lookup"><span data-stu-id="cbc19-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="cbc19-135">Importuj przykładowe dane na koncie DB rozwiązania Cosmos z hello [narzędzia importu DB rozwiązania Cosmos][import-data].</span><span class="sxs-lookup"><span data-stu-id="cbc19-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="cbc19-136">Przepustowość.</span><span class="sxs-lookup"><span data-stu-id="cbc19-136">Throughput.</span></span> <span data-ttu-id="cbc19-137">Odczyty i zapisy z HDInsight będą liczone kierunku jednostek żądania przeznaczonym dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="cbc19-138">Pojemność dodatkowe procedurę składowaną w ramach każdej wyjściowego kolekcji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="cbc19-139">procedury przechowywane Hello są używane do przesyłania wynikowy dokumentów.</span><span class="sxs-lookup"><span data-stu-id="cbc19-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="cbc19-140">Wydajność hello wynikowy dokumentów z hello zadań Hive, Pig i MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cbc19-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="cbc19-141">[*Opcjonalnie*] pojemności dla dodatkowych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="cbc19-142">Kolejność tworzenia hello tooavoid nową kolekcję podczas każdego zadania hello możesz wydrukować toostdout wyniki hello, Zapisz hello dane wyjściowe tooyour WASB kontenera lub określić już istniejącą kolekcję.</span><span class="sxs-lookup"><span data-stu-id="cbc19-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="cbc19-143">W przypadku hello określając istniejącą kolekcję, zostanie utworzona nowych dokumentów w kolekcji hello i już istniejących dokumentów będzie dotyczył tylko, jeśli istnieje konflikt w *identyfikatorów*.</span><span class="sxs-lookup"><span data-stu-id="cbc19-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="cbc19-144">**Łącznik Hello automatycznie spowoduje zastąpienie istniejących dokumentów konflikt identyfikatorów**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="cbc19-145">Można wyłączyć tę funkcję, ustawiając hello upsert opcji toofalse.</span><span class="sxs-lookup"><span data-stu-id="cbc19-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="cbc19-146">Jeśli występuje konflikt upsert ma wartość false, zakończy się niepowodzeniem zadania usługi Hadoop hello; raportowania błędów konflikt identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cbc19-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="cbc19-147"><a name="ProvisionHDInsight"></a>Krok 1: Tworzenie nowego klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbc19-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="cbc19-148">Ten samouczek używa akcji skryptu z toocustomize Azure Portal hello z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="cbc19-149">W tym samouczku używamy toocreate Azure Portal hello z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="cbc19-150">Aby uzyskać instrukcje dotyczące sposobu toouse poleceń cmdlet programu PowerShell lub hello zestawu .NET SDK usługi HDInsight, zapoznaj się [HDInsight dostosować klastry za pomocą akcji skryptu] [ hdinsight-custom-provision] artykułu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="cbc19-151">Zaloguj się toohello [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="cbc19-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="cbc19-152">Kliknij przycisk **+ nowy** u góry hello hello lewy pasek nawigacyjny, wyszukaj **HDInsight** w hello górnym pasku wyszukiwania na powitania nowy blok.</span><span class="sxs-lookup"><span data-stu-id="cbc19-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="cbc19-153">**HDInsight** opublikowanych przez **Microsoft** pojawi się u góry hello hello wyników.</span><span class="sxs-lookup"><span data-stu-id="cbc19-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="cbc19-154">Kliknij go, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="cbc19-155">Utwórz bloku na powitania nowego klastra usługi HDInsight, wprowadź użytkownika **nazwy klastra** i wybierz hello **subskrypcji** ma tooprovision tego zasobu w obszarze.</span><span class="sxs-lookup"><span data-stu-id="cbc19-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="cbc19-156">Nazwa klastra</span><span class="sxs-lookup"><span data-stu-id="cbc19-156">Cluster name</span></span></td><td><span data-ttu-id="cbc19-157">Nazwa klastra hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="cbc19-158">Nazwa DNS musi uruchomić i kończyć się znakiem alfanumeryczne i może zawierać kresek.</span><span class="sxs-lookup"><span data-stu-id="cbc19-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="cbc19-159">pole Hello musi być ciągiem od 3 do 63 znaków.</span><span class="sxs-lookup"><span data-stu-id="cbc19-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="cbc19-160">Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cbc19-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="cbc19-161">Jeśli masz więcej niż jedną subskrypcję platformy Azure, wybierz subskrypcję hello, który będzie hostem z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="cbc19-162">
5.Kliknij przycisk **wybierz typ klastra** i hello ustaw następujące właściwości toohello określone wartości.</span><span class="sxs-lookup"><span data-stu-id="cbc19-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="cbc19-163">Typ klastra</span><span class="sxs-lookup"><span data-stu-id="cbc19-163">Cluster type</span></span></td><td><span data-ttu-id="cbc19-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="cbc19-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="cbc19-165">Warstwy klastrów</span><span class="sxs-lookup"><span data-stu-id="cbc19-165">Cluster tier</span></span></td><td><span data-ttu-id="cbc19-166"><strong>Standardowa</strong></span><span class="sxs-lookup"><span data-stu-id="cbc19-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="cbc19-167">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="cbc19-167">Operating System</span></span></td><td><span data-ttu-id="cbc19-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="cbc19-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="cbc19-169">Wersja</span><span class="sxs-lookup"><span data-stu-id="cbc19-169">Version</span></span></td><td><span data-ttu-id="cbc19-170">Najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="cbc19-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="cbc19-171">Teraz, kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-171">Now, click **SELECT**.</span></span>

    ![Podaj szczegóły klastra Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="cbc19-173">Polecenie **poświadczenia** tooset Twoje poświadczenia logowania i zdalnego dostępu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="cbc19-174">Wybierz użytkownika **nazwa użytkownika logowania klastra** i **hasło logowania klastra**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="cbc19-175">Tooremote w klastrze, wybierz opcję *tak* u dołu bloku hello hello i podaj nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="cbc19-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="cbc19-176">Polecenie **źródła danych** dostęp do lokalizacji głównej dla danych tooset.</span><span class="sxs-lookup"><span data-stu-id="cbc19-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="cbc19-177">Wybierz hello **metodę wyboru** i określenia już istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="cbc19-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="cbc19-178">Na hello na tym samym bloku, określ **domyślny kontener** i **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="cbc19-179">I kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cbc19-180">Wybierz lokalizację tooyour Zamknij region konta DB rozwiązania Cosmos w celu poprawy wydajności</span><span class="sxs-lookup"><span data-stu-id="cbc19-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="cbc19-181">Polecenie **cennik** tooselect hello liczbę i rodzaj węzłach.</span><span class="sxs-lookup"><span data-stu-id="cbc19-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="cbc19-182">Później można zachować hello domyślnej konfiguracji i skali hello liczba węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="cbc19-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="cbc19-183">Kliknij przycisk **konfiguracji opcjonalnej**, następnie **akcji skryptu** w hello opcjonalne blok konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="cbc19-184">W akcji skryptu wprowadź następujące informacje toocustomize hello z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="cbc19-185">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cbc19-185">Property</span></span></th><th><span data-ttu-id="cbc19-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="cbc19-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="cbc19-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cbc19-187">Name</span></span></td>
             <td><span data-ttu-id="cbc19-188">Określ nazwę hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="cbc19-189">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="cbc19-189">Script URI</span></span></td>
             <td><span data-ttu-id="cbc19-190">Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra.</span><span class="sxs-lookup"><span data-stu-id="cbc19-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="cbc19-191">Wprowadź:</span><span class="sxs-lookup"><span data-stu-id="cbc19-191">Please enter:</span></span> </br> <span data-ttu-id="cbc19-192"><strong>https://portalcontent.blob.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="cbc19-193">Główny</span><span class="sxs-lookup"><span data-stu-id="cbc19-193">Head</span></span></td>
             <td><span data-ttu-id="cbc19-194">Kliknij przycisk hello wyboru toorun hello skrypt programu PowerShell na powitania Head węzła.</span><span class="sxs-lookup"><span data-stu-id="cbc19-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="cbc19-195">
             <strong>Zaznacz to pole wyboru</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="cbc19-196">Węzeł roboczy</span><span class="sxs-lookup"><span data-stu-id="cbc19-196">Worker</span></span></td>
             <td><span data-ttu-id="cbc19-197">Kliknij przycisk hello wyboru toorun hello skrypt programu PowerShell na powitania węzła procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="cbc19-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="cbc19-198">
             <strong>Zaznacz to pole wyboru</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="cbc19-199">Dozorca</span><span class="sxs-lookup"><span data-stu-id="cbc19-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="cbc19-200">Kliknij przycisk hello wyboru toorun hello skrypt programu PowerShell na powitania dozorcy.</span><span class="sxs-lookup"><span data-stu-id="cbc19-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="cbc19-201">
             <strong>Zbędny</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="cbc19-202">Parametry</span><span class="sxs-lookup"><span data-stu-id="cbc19-202">Parameters</span></span></td>
             <td><span data-ttu-id="cbc19-203">Określ parametry hello, jeśli są wymagane przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="cbc19-204">
             <strong>Brak parametrów potrzebne</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="cbc19-205">
11.Tworzyć nowe **grupy zasobów** lub użyj istniejącej grupy zasobów w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc19-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="cbc19-206">12.</span><span class="sxs-lookup"><span data-stu-id="cbc19-206">12.</span></span> <span data-ttu-id="cbc19-207">Teraz, sprawdź **toodashboard numeru Pin** tootrack jego wdrożenia i kliknij przycisk **Utwórz**!</span><span class="sxs-lookup"><span data-stu-id="cbc19-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="cbc19-208"><a name="InstallCmdlets"></a>Krok 2: Instalowanie i konfigurowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbc19-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="cbc19-209">Zainstaluj program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbc19-209">Install Azure PowerShell.</span></span> <span data-ttu-id="cbc19-210">Instrukcje można znaleźć [tutaj][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="cbc19-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="cbc19-211">Można również tylko dla zapytań programu Hive, można użyć edytora online Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="cbc19-212">toodo tak, zaloguj się w toohello [Azure Portal][azure-portal], kliknij przycisk **HDInsight** na powitania w okienku po lewej stronie tooview lista klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="cbc19-213">Kliknij klaster hello mają zapytań programu Hive toorun na, a następnie kliknij przycisk **konsoli zapytania**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="cbc19-214">Otwórz hello Azure PowerShell zintegrowane skryptów środowiska:</span><span class="sxs-lookup"><span data-stu-id="cbc19-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="cbc19-215">Na komputerze z systemem Windows 8 lub Windows Server 2012 lub nowszym, można użyć wbudowanych hello wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="cbc19-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="cbc19-216">Na ekranie startowym hello wpisz **programu powershell ise** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="cbc19-217">Na komputerze z systemem w wersji starszej niż Windows 8 lub Windows Server 2012 Użyj hello Start menu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="cbc19-218">W hello Start menu, wpisz **wiersza polecenia** w polu wyszukiwania hello, a następnie na liście hello wyników, kliknij przycisk **wiersza polecenia**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="cbc19-219">W hello wiersza polecenia, wpisz **powershell_ise** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="cbc19-220">Dodaj konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc19-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="cbc19-221">W okienku konsoli hello, wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="cbc19-222">Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="cbc19-223">Wpisz hasło powitania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc19-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="cbc19-224">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="cbc19-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="cbc19-225">powitania po diagram identyfikuje hello ważne części środowiska skryptów programu PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc19-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagram do programu Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="cbc19-227"><a name="RunHive"></a>Krok 3: Uruchomienie zadania Hive za pomocą rozwiązania Cosmos bazę danych i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbc19-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cbc19-228">Wszystkie zmienne określają < > musi być wypełnione przy użyciu ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="cbc19-229">Ustaw hello następujące zmienne w okienku skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbc19-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="cbc19-230">Zacznijmy konstruowanie ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="cbc19-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="cbc19-231">Firma Microsoft będzie Napisz zapytanie Hive, które przyjmuje sygnatury czasowe wygenerowany przez system (_ts) i unikatowe identyfikatory (_rid) z kolekcji bazy danych Azure rozwiązania Cosmos wszystkie dokumenty, zlicza wszystkie dokumenty za minutę hello, a następnie zapisuje wyniki hello do nowej kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="cbc19-232">Najpierw utwórz tabeli programu Hive z naszych kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="cbc19-233">Dodaj powitania po toohello fragment kodu skryptu PowerShell okienko <strong>po</strong> hello fragment kodu z #1.</span><span class="sxs-lookup"><span data-stu-id="cbc19-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="cbc19-234">Upewnij się, że zawierają hello opcjonalne DocumentDB.query parametru t przycinania _ts toojust dokumentów i _rid firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cbc19-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="cbc19-235">**Nazewnictwo DocumentDB.inputCollections nie błędu.**</span><span class="sxs-lookup"><span data-stu-id="cbc19-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="cbc19-236">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="cbc19-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="cbc19-237">Następnie utwórz tabeli programu Hive dla kolekcji danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="cbc19-238">właściwości dokumentu Hello danych wyjściowych będzie hello miesiąc, dzień, godzinę, minutę i hello całkowita liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="cbc19-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cbc19-239">**Jeszcze ponownie nazewnictwa DocumentDB.outputCollections nie błędu.**</span><span class="sxs-lookup"><span data-stu-id="cbc19-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="cbc19-240">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="cbc19-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="cbc19-241">"*DocumentDB.outputCollections*"="*\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 1\>*,*\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 2\>*"</span><span class="sxs-lookup"><span data-stu-id="cbc19-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="cbc19-242">nazwy kolekcji Hello są oddzielone bez spacji, za pomocą tylko jednego przecinka.</span><span class="sxs-lookup"><span data-stu-id="cbc19-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="cbc19-243">Dokumenty będą okrężnego rozproszonych w wielu kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="cbc19-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="cbc19-244">Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w kolekcji dalej hello i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="cbc19-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="cbc19-245">Na koniec załóżmy zgadzają hello dokumentów przez miesiąc, dzień, godzinę i wyniki hello minutę i Wstaw do hello output tabelę programu Hive.</span><span class="sxs-lookup"><span data-stu-id="cbc19-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="cbc19-246">Dodaj powitania po toocreate fragment kodu skryptu definicji zadania Hive z hello poprzednie zapytanie.</span><span class="sxs-lookup"><span data-stu-id="cbc19-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="cbc19-247">Można również użyć hello — plik przełącznika toospecify HiveQL pliku skryptu w systemie plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="cbc19-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="cbc19-248">Dodaj powitania po czas rozpoczęcia hello toosave fragment i przesłać zadania technologii Hive hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="cbc19-249">Dodaj następujące toowait dla toocomplete zadania Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="cbc19-250">Dodaj powitania po tooprint hello standardowe Wyjście i hello rozpoczęcia i zakończenia godzin.</span><span class="sxs-lookup"><span data-stu-id="cbc19-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="cbc19-251">**Uruchom** nowy skrypt!</span><span class="sxs-lookup"><span data-stu-id="cbc19-251">**Run** your new script!</span></span> <span data-ttu-id="cbc19-252">**Kliknij przycisk** zielony hello wykonania przycisku.</span><span class="sxs-lookup"><span data-stu-id="cbc19-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="cbc19-253">Sprawdzanie wyników hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-253">Check hello results.</span></span> <span data-ttu-id="cbc19-254">Zaloguj się na powitania [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="cbc19-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="cbc19-255">Kliknij przycisk <strong>Przeglądaj</strong> na powitania po lewej stronie panelu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="cbc19-256">Kliknij przycisk <strong>wszystko</strong> na powitania prawym górnym rogu hello przeglądania panelu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="cbc19-257">Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="cbc19-258">Następnie znaleźć Twoje <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z określonej w kolekcji danych wyjściowych hello Zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="cbc19-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="cbc19-259">Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="cbc19-260">Zostanie wyświetlone powitalne wyniki zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="cbc19-260">You will see hello results of your Hive query.</span></span>

   ![Wyniki zapytania hive][image-hive-query-results]

## <span data-ttu-id="cbc19-262"><a name="RunPig"></a>Krok 4: Uruchom zadanie Pig przy użyciu rozwiązania Cosmos bazę danych i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbc19-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cbc19-263">Wszystkie zmienne określają < > musi być wypełnione przy użyciu ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="cbc19-264">Ustaw hello następujące zmienne w okienku skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbc19-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="cbc19-265">Zacznijmy konstruowanie ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="cbc19-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="cbc19-266">Firma Microsoft będzie Napisz zapytanie Pig, które przyjmuje sygnatury czasowe wygenerowany przez system (_ts) i unikatowe identyfikatory (_rid) z kolekcji bazy danych Azure rozwiązania Cosmos wszystkie dokumenty, zlicza wszystkie dokumenty za minutę hello, a następnie zapisuje wyniki hello do nowej kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="cbc19-267">Po pierwsze ładowanie dokumentów z rozwiązania Cosmos bazy danych do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="cbc19-268">Dodaj powitania po toohello fragment kodu skryptu PowerShell okienko <strong>po</strong> hello fragment kodu z #1.</span><span class="sxs-lookup"><span data-stu-id="cbc19-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="cbc19-269">Upewnij się, tooadd DocumentDB naszych _ts toojust dokumentów oraz _rid tootrim parametru zapytania usługi DocumentDB toohello opcjonalne zapytania.</span><span class="sxs-lookup"><span data-stu-id="cbc19-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="cbc19-270">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="cbc19-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="cbc19-271">"*\<Nazwa kolekcji usługi DocumentDB w danych wejściowych 1\>*,*\<Nazwa kolekcji usługi DocumentDB w danych wejściowych 2\>*"</span><span class="sxs-lookup"><span data-stu-id="cbc19-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="cbc19-272">nazwy kolekcji Hello są oddzielone bez spacji, za pomocą tylko jednego przecinka.</span><span class="sxs-lookup"><span data-stu-id="cbc19-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="cbc19-273">Dokumenty będą okrężnego rozproszonych w wielu kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="cbc19-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="cbc19-274">Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w kolekcji dalej hello i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="cbc19-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="cbc19-275">Następnie Załóżmy zgadzają hello dokumentów przez hello miesiąc, dzień, godzinę, minutę i hello całkowita liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="cbc19-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="cbc19-276">Na koniec załóżmy przechowywać wyniki hello w naszej nowej kolekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="cbc19-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cbc19-277">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="cbc19-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="cbc19-278">"\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 1\>,\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 2\>"</span><span class="sxs-lookup"><span data-stu-id="cbc19-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="cbc19-279">nazwy kolekcji Hello są oddzielone bez spacji, za pomocą tylko jednego przecinka.</span><span class="sxs-lookup"><span data-stu-id="cbc19-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="cbc19-280">Dokumenty będą być rozproszone okrężnego w obrębie hello wielu kolekcji.</span><span class="sxs-lookup"><span data-stu-id="cbc19-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="cbc19-281">Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w kolekcji dalej hello i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="cbc19-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="cbc19-282">Dodaj powitania po toocreate fragment kodu skryptu definicji zadania Pig z hello poprzednie zapytanie.</span><span class="sxs-lookup"><span data-stu-id="cbc19-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="cbc19-283">Można również użyć hello — plik przełącznika toospecify pliku skryptu Pig na system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="cbc19-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="cbc19-284">Dodaj powitania po czas rozpoczęcia hello toosave fragment i przesłać zadania programu Pig hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="cbc19-285">Dodaj powitania po toowait dla hello Pig zadania toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cbc19-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="cbc19-286">Dodaj powitania po tooprint hello standardowe Wyjście i hello rozpoczęcia i zakończenia godzin.</span><span class="sxs-lookup"><span data-stu-id="cbc19-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="cbc19-287">**Uruchom** nowy skrypt!</span><span class="sxs-lookup"><span data-stu-id="cbc19-287">**Run** your new script!</span></span> <span data-ttu-id="cbc19-288">**Kliknij przycisk** zielony hello wykonania przycisku.</span><span class="sxs-lookup"><span data-stu-id="cbc19-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="cbc19-289">Sprawdzanie wyników hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-289">Check hello results.</span></span> <span data-ttu-id="cbc19-290">Zaloguj się na powitania [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="cbc19-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="cbc19-291">Kliknij przycisk <strong>Przeglądaj</strong> na powitania po lewej stronie panelu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="cbc19-292">Kliknij przycisk <strong>wszystko</strong> na powitania prawym górnym rogu hello przeglądania panelu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="cbc19-293">Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="cbc19-294">Następnie znaleźć Twoje <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z określonej w kolekcji danych wyjściowych hello Kwerenda Pig.</span><span class="sxs-lookup"><span data-stu-id="cbc19-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="cbc19-295">Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="cbc19-296">Zostanie wyświetlone hello wyników kwerendy Pig.</span><span class="sxs-lookup"><span data-stu-id="cbc19-296">You will see hello results of your Pig query.</span></span>

    ![Wyniki zapytania pig][image-pig-query-results]

## <span data-ttu-id="cbc19-298"><a name="RunMapReduce"></a>Krok 5: Uruchomienie zadania MapReduce przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbc19-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="cbc19-299">Ustaw hello następujące zmienne w okienku skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbc19-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="cbc19-300">Firma Microsoft będzie wykonywać zadania MapReduce, które zlicza hello liczba wystąpień dla każdej właściwości dokumentu z kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="cbc19-301">Dodaj następujący fragment kodu skryptu **po** fragment hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="cbc19-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="cbc19-302">TallyProperties v01.jar zawiera hello Instalacja niestandardowa programu hello łącznika usługi Hadoop DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cbc19-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="cbc19-303">Dodaj następujące zadania MapReduce hello toosubmit polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="cbc19-304">Dodatkowo toohello definicji zadania MapReduce, można też podać nazwy klastra usługi HDInsight hello miejscu zadania MapReduce hello toorun i poświadczenia hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="cbc19-305">Witaj AzureHDInsightJob rozpoczęcia jest wywołania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="cbc19-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="cbc19-306">toocheck hello ukończenia zadania hello, użyj hello *AzureHDInsightJob oczekiwania* polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cbc19-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="cbc19-307">Dodaj następujące polecenie toocheck hello błędy uruchomione zadania MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="cbc19-308">**Uruchom** nowy skrypt!</span><span class="sxs-lookup"><span data-stu-id="cbc19-308">**Run** your new script!</span></span> <span data-ttu-id="cbc19-309">**Kliknij przycisk** zielony hello wykonania przycisku.</span><span class="sxs-lookup"><span data-stu-id="cbc19-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="cbc19-310">Sprawdzanie wyników hello.</span><span class="sxs-lookup"><span data-stu-id="cbc19-310">Check hello results.</span></span> <span data-ttu-id="cbc19-311">Zaloguj się na powitania [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="cbc19-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="cbc19-312">Kliknij przycisk <strong>Przeglądaj</strong> na powitania po lewej stronie panelu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="cbc19-313">Kliknij przycisk <strong>wszystko</strong> na powitania prawym górnym rogu hello przeglądania panelu.</span><span class="sxs-lookup"><span data-stu-id="cbc19-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="cbc19-314">Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="cbc19-315">Następnie znaleźć Twoje <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z określonej w kolekcji danych wyjściowych hello zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cbc19-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="cbc19-316">Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="cbc19-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="cbc19-317">Zostanie wyświetlone powitalne wyników zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cbc19-317">You will see hello results of your MapReduce job.</span></span>

      ![MapReduce wyników zapytania][image-mapreduce-query-results]

## <span data-ttu-id="cbc19-319"><a name="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cbc19-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="cbc19-320">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="cbc19-320">Congratulations!</span></span> <span data-ttu-id="cbc19-321">Właśnie uruchomiono pierwszy zadań Hive, Pig i MapReduce przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbc19-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="cbc19-322">Mamy Otwórz powierzając jej ich konserwację naszych łącznika usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cbc19-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="cbc19-323">Jeśli chcesz, można współtworzyć na [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="cbc19-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="cbc19-324">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="cbc19-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="cbc19-325">[Tworzenie aplikacji Java z usługi Documentdb][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="cbc19-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="cbc19-326">[Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="cbc19-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="cbc19-327">[Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive HDInsight tooanalyze przenośnych słuchawki używana][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="cbc19-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="cbc19-328">[Korzystać z usługi MapReduce z usługą HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="cbc19-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="cbc19-329">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="cbc19-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="cbc19-330">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="cbc19-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="cbc19-331">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="cbc19-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
