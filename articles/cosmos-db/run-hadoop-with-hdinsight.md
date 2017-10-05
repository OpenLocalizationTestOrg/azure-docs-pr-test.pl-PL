---
title: "Uruchomienie zadania usługi Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uruchomić proste zadanie Hive, Pig i MapReduce z bazy danych rozwiązania Cosmos Azure i usłudze Azure HDInsight."
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
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="54f32-103"><a name="Azure Cosmos DB-HDInsight"></a>Uruchom zadanie Apache Hive, Pig lub Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="54f32-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="54f32-104">W tym samouczku przedstawiono sposób uruchamiania [Apache Hive][apache-hive], [Apache Pig][apache-pig], i [Apache Hadoop] [ apache-hadoop] zadań MapReduce w usłudze Azure HDInsight z łącznikiem usługi Hadoop DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="54f32-105">Łącznik usługi Hadoop DB rozwiązania cosmos umożliwia rozwiązania Cosmos bazy danych, które będą działać jako źródło i ujście zadań Hive, Pig i MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54f32-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="54f32-106">W tym samouczku będzie używać rozwiązania Cosmos bazy danych jako źródła danych i docelowy zadania usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="54f32-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="54f32-107">Po ukończeniu tego samouczka, będziesz mieć możliwość odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="54f32-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="54f32-108">Jak załadować dane z rozwiązania Cosmos bazy danych przy użyciu zadania Hive, Pig lub MapReduce?</span><span class="sxs-lookup"><span data-stu-id="54f32-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="54f32-109">Sposób przechowywania danych w bazie danych rozwiązania Cosmos przy użyciu zadania Hive, Pig lub MapReduce?</span><span class="sxs-lookup"><span data-stu-id="54f32-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="54f32-110">Zalecamy rozpoczęcie pracy od obejrzenia poniższego klipu wideo, w którym przeprowadzana za pomocą zadania Hive za pomocą rozwiązania Cosmos bazę danych i usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="54f32-111">Następnie wróć do tego artykułu, gdy otrzymasz pełne szczegóły na uruchamianie zadania usługi analiza danych DB rozwiązania Cosmos w.</span><span class="sxs-lookup"><span data-stu-id="54f32-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="54f32-112">Ten samouczek zakłada, że masz wcześniejszego doświadczenia w używaniu platformy Apache Hadoop, Hive i Pig.</span><span class="sxs-lookup"><span data-stu-id="54f32-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="54f32-113">Jeśli jesteś nowym użytkownikiem usługi Apache Hadoop, Hive i Pig, zaleca się znaleźć [dokumentację Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="54f32-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="54f32-114">W tym samouczku przyjęto założenie, czy masz doświadczenie z rozwiązania Cosmos bazy danych, a konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="54f32-115">Jeśli jesteś nowym użytkownikiem rozwiązania Cosmos bazy danych lub nie masz konta rozwiązania Cosmos bazy danych, można znaleźć na naszych [wprowadzenie] [ getting-started] strony.</span><span class="sxs-lookup"><span data-stu-id="54f32-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="54f32-116">Nie masz czasu na ukończenie tego samouczka i po prostu chcesz uzyskać skrypty programu PowerShell pełny przykład Hive, Pig i MapReduce?</span><span class="sxs-lookup"><span data-stu-id="54f32-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="54f32-117">Nie ma problemu, pobierz je [tutaj][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="54f32-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="54f32-118">Pobieranie zawiera również pliki hql, pig i java dla tych przykładów.</span><span class="sxs-lookup"><span data-stu-id="54f32-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="54f32-119"><a name="NewestVersion"></a>Najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="54f32-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="54f32-120">Wersja łącznika usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="54f32-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="54f32-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="54f32-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="54f32-122">Identyfikator Uri skryptu</span><span class="sxs-lookup"><span data-stu-id="54f32-122">Script Uri</span></span></th>
        <td><span data-ttu-id="54f32-123">https://portalcontent.blob.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="54f32-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="54f32-124">Data modyfikacji</span><span class="sxs-lookup"><span data-stu-id="54f32-124">Date Modified</span></span></th>
        <td><span data-ttu-id="54f32-125">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="54f32-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="54f32-126">HDInsight obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="54f32-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="54f32-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="54f32-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="54f32-128">Dziennik zmian</span><span class="sxs-lookup"><span data-stu-id="54f32-128">Change Log</span></span></th>
        <td><span data-ttu-id="54f32-129">Zaktualizowano rozwiązania Cosmos Azure DB Java SDK 1.6.0</span><span class="sxs-lookup"><span data-stu-id="54f32-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="54f32-130">Dodano obsługę dla kolekcji partycjonowanych jako źródło i ujście</span><span class="sxs-lookup"><span data-stu-id="54f32-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="54f32-131"><a name="Prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="54f32-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="54f32-132">Przed wykonaniem instrukcji zawartych w tym samouczku, upewnij się, że masz następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54f32-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="54f32-133">Konto rozwiązania Cosmos bazy danych, bazy danych i kolekcji dokumentów wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="54f32-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="54f32-134">Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych rozwiązania Cosmos][getting-started].</span><span class="sxs-lookup"><span data-stu-id="54f32-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="54f32-135">Importować przykładowe dane do Twojego konta DB rozwiązania Cosmos z [narzędzia importu DB rozwiązania Cosmos][import-data].</span><span class="sxs-lookup"><span data-stu-id="54f32-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="54f32-136">Przepustowość.</span><span class="sxs-lookup"><span data-stu-id="54f32-136">Throughput.</span></span> <span data-ttu-id="54f32-137">Odczyty i zapisy z HDInsight będą liczone kierunku jednostek żądania przeznaczonym dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="54f32-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="54f32-138">Pojemność dodatkowe procedurę składowaną w ramach każdej wyjściowego kolekcji.</span><span class="sxs-lookup"><span data-stu-id="54f32-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="54f32-139">Procedury składowane są używane do przesyłania wynikowy dokumentów.</span><span class="sxs-lookup"><span data-stu-id="54f32-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="54f32-140">Wydajność wynikowy dokumentów z zadań Hive, Pig i MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54f32-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="54f32-141">[*Opcjonalnie*] pojemności dla dodatkowych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="54f32-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="54f32-142">Aby uniknąć tworzenia nowej kolekcji podczas wszystkich zadań, możesz drukowanie wyników do stdout, Zapisz dane wyjściowe z kontenerem WASB lub określ już istniejącą kolekcję.</span><span class="sxs-lookup"><span data-stu-id="54f32-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="54f32-143">W przypadku określania istniejącą kolekcję, zostanie utworzona nowych dokumentów w kolekcji i już istniejących dokumentów będzie dotyczył tylko, jeśli istnieje konflikt w *identyfikatorów*.</span><span class="sxs-lookup"><span data-stu-id="54f32-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="54f32-144">**Łącznik automatycznie spowoduje zastąpienie istniejących dokumentów konflikt identyfikatorów**.</span><span class="sxs-lookup"><span data-stu-id="54f32-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="54f32-145">Tę funkcję można wyłączyć przez ustawienie opcji upsert na wartość false.</span><span class="sxs-lookup"><span data-stu-id="54f32-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="54f32-146">Jeśli występuje konflikt upsert ma wartość false, zakończy się niepowodzeniem zadania usługi Hadoop; raportowania błędów konflikt identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="54f32-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="54f32-147"><a name="ProvisionHDInsight"></a>Krok 1: Tworzenie nowego klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="54f32-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="54f32-148">W tym samouczku używana akcji skryptu z portalu Azure do dostosowania z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="54f32-149">W tym samouczku używamy portalu Azure do tworzenia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="54f32-150">Aby uzyskać instrukcje dotyczące sposobu używania poleceń cmdlet programu PowerShell lub zestawu .NET SDK usługi HDInsight, zapoznaj się z [HDInsight dostosować klastry za pomocą akcji skryptu] [ hdinsight-custom-provision] artykułu.</span><span class="sxs-lookup"><span data-stu-id="54f32-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="54f32-151">Zaloguj się do [portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="54f32-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="54f32-152">Kliknij przycisk **+ nowy** górnej części nawigacji po lewej stronie, wyszukaj **HDInsight** w górnym pasku wyszukiwania w nowym bloku.</span><span class="sxs-lookup"><span data-stu-id="54f32-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="54f32-153">**HDInsight** opublikowanych przez **Microsoft** pojawi się w górnej części wyników.</span><span class="sxs-lookup"><span data-stu-id="54f32-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="54f32-154">Kliknij go, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="54f32-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="54f32-155">W nowym klastrze HDInsight utworzyć bloku, wprowadź użytkownika **nazwy klastra** i wybierz **subskrypcji** chcesz udostępnić ten zasób w obszarze.</span><span class="sxs-lookup"><span data-stu-id="54f32-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="54f32-156">Nazwa klastra</span><span class="sxs-lookup"><span data-stu-id="54f32-156">Cluster name</span></span></td><td><span data-ttu-id="54f32-157">Nazwa klastra.</span><span class="sxs-lookup"><span data-stu-id="54f32-157">Name the cluster.</span></span><br/>
<span data-ttu-id="54f32-158">Nazwa DNS musi uruchomić i kończyć się znakiem alfanumeryczne i może zawierać kresek.</span><span class="sxs-lookup"><span data-stu-id="54f32-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="54f32-159">Pole musi być ciągiem od 3 do 63 znaków.</span><span class="sxs-lookup"><span data-stu-id="54f32-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="54f32-160">Nazwa subskrypcji</span><span class="sxs-lookup"><span data-stu-id="54f32-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="54f32-161">Jeśli masz więcej niż jedną subskrypcję platformy Azure, wybierz subskrypcję, która będzie obsługiwać z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="54f32-162">
5.Kliknij przycisk **wybierz typ klastra** i ustaw następujące właściwości do określonych wartości.</span><span class="sxs-lookup"><span data-stu-id="54f32-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="54f32-163">Typ klastra</span><span class="sxs-lookup"><span data-stu-id="54f32-163">Cluster type</span></span></td><td><span data-ttu-id="54f32-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="54f32-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="54f32-165">Warstwy klastrów</span><span class="sxs-lookup"><span data-stu-id="54f32-165">Cluster tier</span></span></td><td><span data-ttu-id="54f32-166"><strong>Standardowa</strong></span><span class="sxs-lookup"><span data-stu-id="54f32-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="54f32-167">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="54f32-167">Operating System</span></span></td><td><span data-ttu-id="54f32-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="54f32-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="54f32-169">Wersja</span><span class="sxs-lookup"><span data-stu-id="54f32-169">Version</span></span></td><td><span data-ttu-id="54f32-170">Najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="54f32-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="54f32-171">Teraz, kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="54f32-171">Now, click **SELECT**.</span></span>

    ![Podaj szczegóły klastra Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="54f32-173">Polecenie **poświadczenia** można ustawić Twoje poświadczenia logowania i zdalnego dostępu.</span><span class="sxs-lookup"><span data-stu-id="54f32-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="54f32-174">Wybierz użytkownika **nazwa użytkownika logowania klastra** i **hasło logowania klastra**.</span><span class="sxs-lookup"><span data-stu-id="54f32-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="54f32-175">Zdalne w klastrze, wybierz opcję *tak* w dolnej części bloku i podaj nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="54f32-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="54f32-176">Polecenie **źródła danych** można ustawić lokalizacji głównej dla dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="54f32-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="54f32-177">Wybierz **metodę wyboru** i określenia już istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="54f32-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="54f32-178">W tym samym bloku określić **domyślny kontener** i **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="54f32-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="54f32-179">I kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="54f32-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54f32-180">Wybierz lokalizację bliski DB rozwiązania Cosmos regionu konta w celu poprawy wydajności</span><span class="sxs-lookup"><span data-stu-id="54f32-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="54f32-181">Polecenie **cennik** wybierz liczbę i rodzaj węzłach.</span><span class="sxs-lookup"><span data-stu-id="54f32-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="54f32-182">Możesz zachować konfigurację domyślną i skalować liczbę węzłów procesu roboczego na dalszym etapie.</span><span class="sxs-lookup"><span data-stu-id="54f32-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="54f32-183">Kliknij przycisk **konfiguracji opcjonalnej**, następnie **skryptu akcje** w bloku konfiguracji opcjonalnej.</span><span class="sxs-lookup"><span data-stu-id="54f32-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="54f32-184">W akcji skryptu wprowadź następujące informacje, aby dostosować z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="54f32-185">Właściwość</span><span class="sxs-lookup"><span data-stu-id="54f32-185">Property</span></span></th><th><span data-ttu-id="54f32-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="54f32-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="54f32-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54f32-187">Name</span></span></td>
             <td><span data-ttu-id="54f32-188">Określ nazwę akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="54f32-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="54f32-189">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="54f32-189">Script URI</span></span></td>
             <td><span data-ttu-id="54f32-190">Określ identyfikator URI do skryptu, które jest wywoływane, aby dostosować klastra.</span><span class="sxs-lookup"><span data-stu-id="54f32-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="54f32-191">Wprowadź:</span><span class="sxs-lookup"><span data-stu-id="54f32-191">Please enter:</span></span> </br> <span data-ttu-id="54f32-192"><strong>https://portalcontent.blob.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="54f32-193">Główny</span><span class="sxs-lookup"><span data-stu-id="54f32-193">Head</span></span></td>
             <td><span data-ttu-id="54f32-194">Kliknij pole wyboru, aby uruchomić skrypt programu PowerShell na węźle Head.</span><span class="sxs-lookup"><span data-stu-id="54f32-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="54f32-195">
             <strong>Zaznacz to pole wyboru</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="54f32-196">Węzeł roboczy</span><span class="sxs-lookup"><span data-stu-id="54f32-196">Worker</span></span></td>
             <td><span data-ttu-id="54f32-197">Kliknij pole wyboru, aby uruchomić skrypt programu PowerShell na węźle procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="54f32-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="54f32-198">
             <strong>Zaznacz to pole wyboru</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="54f32-199">Dozorca</span><span class="sxs-lookup"><span data-stu-id="54f32-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="54f32-200">Kliknij pole wyboru, aby uruchomić skrypt programu PowerShell na dozorcy.</span><span class="sxs-lookup"><span data-stu-id="54f32-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="54f32-201">
             <strong>Zbędny</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="54f32-202">Parametry</span><span class="sxs-lookup"><span data-stu-id="54f32-202">Parameters</span></span></td>
             <td><span data-ttu-id="54f32-203">Określ parametry, jeśli jest to wymagane przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="54f32-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="54f32-204">
             <strong>Brak parametrów potrzebne</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="54f32-205">
11.Tworzyć nowe **grupy zasobów** lub użyj istniejącej grupy zasobów w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54f32-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="54f32-206">12.</span><span class="sxs-lookup"><span data-stu-id="54f32-206">12.</span></span> <span data-ttu-id="54f32-207">Teraz, sprawdź **Przypnij do pulpitu nawigacyjnego** śledzenia jej wdrożenia, a następnie kliknij przycisk **Utwórz**!</span><span class="sxs-lookup"><span data-stu-id="54f32-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="54f32-208"><a name="InstallCmdlets"></a>Krok 2: Instalowanie i konfigurowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="54f32-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="54f32-209">Zainstaluj program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f32-209">Install Azure PowerShell.</span></span> <span data-ttu-id="54f32-210">Instrukcje można znaleźć [tutaj][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="54f32-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="54f32-211">Można również tylko dla zapytań programu Hive, można użyć edytora online Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="54f32-212">Aby to zrobić, zaloguj się do [Azure Portal][azure-portal], kliknij przycisk **HDInsight** w okienku po lewej stronie, aby wyświetlić listę z klastrami HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="54f32-213">Kliknij klaster ma być uruchamianie zapytań Hive, a następnie kliknij przycisk **konsoli zapytania**.</span><span class="sxs-lookup"><span data-stu-id="54f32-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="54f32-214">Otwórz zintegrowane środowisko obsługi skryptów programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="54f32-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="54f32-215">Na komputerze z systemem Windows 8 lub Windows Server 2012 lub nowszym można użyć wbudowanych wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="54f32-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="54f32-216">Na ekranie startowym wpisz **programu powershell ise** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="54f32-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="54f32-217">Na komputerze z systemem w wersji starszej niż Windows 8 lub Windows Server 2012 Użyj Start menu.</span><span class="sxs-lookup"><span data-stu-id="54f32-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="54f32-218">W Start menu wpisz **wiersza polecenia** w polu wyszukiwania, a następnie na liście wyników, kliknij przycisk **wiersza polecenia**.</span><span class="sxs-lookup"><span data-stu-id="54f32-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="54f32-219">W wierszu polecenia wpisz **powershell_ise** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="54f32-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="54f32-220">Dodaj konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54f32-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="54f32-221">W okienku konsoli wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="54f32-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="54f32-222">Wpisz adres e-mail skojarzony z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="54f32-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="54f32-223">Wpisz hasło dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54f32-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="54f32-224">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="54f32-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="54f32-225">Poniższy diagram identyfikuje ważne części środowiska skryptów programu PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="54f32-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagram do programu Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="54f32-227"><a name="RunHive"></a>Krok 3: Uruchomienie zadania Hive za pomocą rozwiązania Cosmos bazę danych i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="54f32-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="54f32-228">Wszystkie zmienne określają < > musi być wypełnione przy użyciu ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="54f32-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="54f32-229">Ustaw następujące zmienne w okienku skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f32-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="54f32-230">Zacznijmy konstruowanie ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="54f32-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="54f32-231">Firma Microsoft będzie Napisz zapytanie Hive, które przyjmuje sygnatury czasowe wygenerowany przez system (_ts) i unikatowe identyfikatory (_rid) z kolekcji bazy danych Azure rozwiązania Cosmos wszystkie dokumenty, zlicza wszystkie dokumenty za minutę, a następnie zapisuje wyniki do nowej kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="54f32-232">Najpierw utwórz tabeli programu Hive z naszych kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="54f32-233">W okienku skrypt programu PowerShell Dodaj poniższy fragment kodu <strong>po</strong> fragment kodu z #1.</span><span class="sxs-lookup"><span data-stu-id="54f32-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="54f32-234">Upewnij się, że obejmują przycinania t parametr opcjonalny DocumentDB.query naszych dokumentów, aby tylko _ts i _rid.</span><span class="sxs-lookup"><span data-stu-id="54f32-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="54f32-235">**Nazewnictwo DocumentDB.inputCollections nie błędu.**</span><span class="sxs-lookup"><span data-stu-id="54f32-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="54f32-236">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="54f32-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="54f32-237">Następnie utwórz tabeli programu Hive dla kolekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="54f32-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="54f32-238">Właściwości dokumentu danych wyjściowych będzie miesiąc, dzień, godzinę, minutę i łączna liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="54f32-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54f32-239">**Jeszcze ponownie nazewnictwa DocumentDB.outputCollections nie błędu.**</span><span class="sxs-lookup"><span data-stu-id="54f32-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="54f32-240">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="54f32-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="54f32-241">"*DocumentDB.outputCollections*"="*\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 1\>*,*\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 2\>*"</span><span class="sxs-lookup"><span data-stu-id="54f32-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="54f32-242">Nazwy kolekcji są oddzielone bez spacji, za pomocą tylko jednego przecinka.</span><span class="sxs-lookup"><span data-stu-id="54f32-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="54f32-243">Dokumenty będą okrężnego rozproszonych w wielu kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="54f32-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="54f32-244">Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w następnej kolekcji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="54f32-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="54f32-245">Na koniec załóżmy zgodności dokumentów przez miesiąc, dzień, godzinę i minutę i Wstaw wyniki do danych wyjściowych tabelę programu Hive.</span><span class="sxs-lookup"><span data-stu-id="54f32-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="54f32-246">Dodaj poniższy fragment kodu skryptu do tworzenia definicji zadania Hive z poprzedniego zapytania.</span><span class="sxs-lookup"><span data-stu-id="54f32-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="54f32-247">Można również użyć przełącznika - plik, aby określić plik skryptu HiveQL w systemie plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="54f32-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="54f32-248">Dodaj poniższy fragment kodu, aby oszczędzić czas rozpoczęcia i przesłać zadania technologii Hive.</span><span class="sxs-lookup"><span data-stu-id="54f32-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="54f32-249">Dodaj następujące polecenie, aby czekać na ukończenie zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="54f32-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="54f32-250">Dodaj następujący kod do wyjścia standardowego i godziny rozpoczęcia i zakończenia wydruku.</span><span class="sxs-lookup"><span data-stu-id="54f32-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="54f32-251">**Uruchom** nowy skrypt!</span><span class="sxs-lookup"><span data-stu-id="54f32-251">**Run** your new script!</span></span> <span data-ttu-id="54f32-252">**Kliknij przycisk** przycisk zielony execute.</span><span class="sxs-lookup"><span data-stu-id="54f32-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="54f32-253">Sprawdzenie wyników.</span><span class="sxs-lookup"><span data-stu-id="54f32-253">Check the results.</span></span> <span data-ttu-id="54f32-254">Zaloguj się do [portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="54f32-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="54f32-255">Kliknij przycisk <strong>Przeglądaj</strong> w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="54f32-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="54f32-256">Kliknij przycisk <strong>wszystko</strong> w prawym górnym rogu panelu przeglądania.</span><span class="sxs-lookup"><span data-stu-id="54f32-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="54f32-257">Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="54f32-258">Następnie znaleźć użytkownika <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z tą kolekcją dane wyjściowe określone zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="54f32-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="54f32-259">Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="54f32-260">Zobaczysz wyniki zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="54f32-260">You will see the results of your Hive query.</span></span>

   ![Wyniki zapytania hive][image-hive-query-results]

## <span data-ttu-id="54f32-262"><a name="RunPig"></a>Krok 4: Uruchom zadanie Pig przy użyciu rozwiązania Cosmos bazę danych i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="54f32-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="54f32-263">Wszystkie zmienne określają < > musi być wypełnione przy użyciu ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="54f32-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="54f32-264">Ustaw następujące zmienne w okienku skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f32-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="54f32-265">Zacznijmy konstruowanie ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="54f32-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="54f32-266">Firma Microsoft będzie Napisz zapytanie Pig, które przyjmuje sygnatury czasowe wygenerowany przez system (_ts) i unikatowe identyfikatory (_rid) z kolekcji bazy danych Azure rozwiązania Cosmos wszystkie dokumenty, zlicza wszystkie dokumenty za minutę, a następnie zapisuje wyniki do nowej kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="54f32-267">Po pierwsze ładowanie dokumentów z rozwiązania Cosmos bazy danych do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="54f32-268">W okienku skrypt programu PowerShell Dodaj poniższy fragment kodu <strong>po</strong> fragment kodu z #1.</span><span class="sxs-lookup"><span data-stu-id="54f32-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="54f32-269">Upewnij się dodać zapytanie bazy danych DocumentDB do opcjonalny parametr zapytania usługi DocumentDB przyciąć naszych dokumentów, aby tylko _ts i _rid.</span><span class="sxs-lookup"><span data-stu-id="54f32-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="54f32-270">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="54f32-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="54f32-271">"*\<Nazwa kolekcji usługi DocumentDB w danych wejściowych 1\>*,*\<Nazwa kolekcji usługi DocumentDB w danych wejściowych 2\>*"</span><span class="sxs-lookup"><span data-stu-id="54f32-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="54f32-272">Nazwy kolekcji są oddzielone bez spacji, za pomocą tylko jednego przecinka.</span><span class="sxs-lookup"><span data-stu-id="54f32-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="54f32-273">Dokumenty będą okrężnego rozproszonych w wielu kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="54f32-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="54f32-274">Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w następnej kolekcji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="54f32-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="54f32-275">Następnie umożliwia zgodności dokumentów przez miesiąc, dzień, godzinę, minutę i łączna liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="54f32-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="54f32-276">Ponadto umożliwia przechowywanie wyników w naszej nowej kolekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="54f32-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54f32-277">Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="54f32-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="54f32-278">"\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 1\>,\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 2\>"</span><span class="sxs-lookup"><span data-stu-id="54f32-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="54f32-279">Nazwy kolekcji są oddzielone bez spacji, za pomocą tylko jednego przecinka.</span><span class="sxs-lookup"><span data-stu-id="54f32-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="54f32-280">Dokumenty będą okrężnego rozproszonych w wielu kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="54f32-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="54f32-281">Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w następnej kolekcji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="54f32-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="54f32-282">Dodaj poniższy fragment kodu skryptu do tworzenia definicji zadania Pig z poprzedniego zapytania.</span><span class="sxs-lookup"><span data-stu-id="54f32-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="54f32-283">Można również użyć przełącznika - plik, aby określić plik skryptu Pig na system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="54f32-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="54f32-284">Dodaj poniższy fragment kodu, aby zaoszczędzić czas rozpoczęcia i przesłać zadania programu Pig.</span><span class="sxs-lookup"><span data-stu-id="54f32-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="54f32-285">Dodaj następujące polecenie, aby czekać na ukończenie zadania Pig.</span><span class="sxs-lookup"><span data-stu-id="54f32-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="54f32-286">Dodaj następujący kod do wyjścia standardowego i godziny rozpoczęcia i zakończenia wydruku.</span><span class="sxs-lookup"><span data-stu-id="54f32-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="54f32-287">**Uruchom** nowy skrypt!</span><span class="sxs-lookup"><span data-stu-id="54f32-287">**Run** your new script!</span></span> <span data-ttu-id="54f32-288">**Kliknij przycisk** przycisk zielony execute.</span><span class="sxs-lookup"><span data-stu-id="54f32-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="54f32-289">Sprawdzenie wyników.</span><span class="sxs-lookup"><span data-stu-id="54f32-289">Check the results.</span></span> <span data-ttu-id="54f32-290">Zaloguj się do [portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="54f32-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="54f32-291">Kliknij przycisk <strong>Przeglądaj</strong> w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="54f32-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="54f32-292">Kliknij przycisk <strong>wszystko</strong> w prawym górnym rogu panelu przeglądania.</span><span class="sxs-lookup"><span data-stu-id="54f32-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="54f32-293">Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="54f32-294">Następnie znaleźć użytkownika <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z tą kolekcją dane wyjściowe określone w zapytaniu Pig.</span><span class="sxs-lookup"><span data-stu-id="54f32-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="54f32-295">Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="54f32-296">Wyniki zapytania Pig będą widoczne.</span><span class="sxs-lookup"><span data-stu-id="54f32-296">You will see the results of your Pig query.</span></span>

    ![Wyniki zapytania pig][image-pig-query-results]

## <span data-ttu-id="54f32-298"><a name="RunMapReduce"></a>Krok 5: Uruchomienie zadania MapReduce przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="54f32-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="54f32-299">Ustaw następujące zmienne w okienku skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f32-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="54f32-300">Firma Microsoft będzie wykonywać zadania MapReduce, które zlicza liczbę wystąpień dla każdej właściwości dokumentu z kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="54f32-301">Dodaj następujący fragment kodu skryptu **po** fragment powyżej.</span><span class="sxs-lookup"><span data-stu-id="54f32-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="54f32-302">TallyProperties v01.jar jest dostarczany z niestandardowej instalacji łącznika usługi Hadoop DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54f32-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="54f32-303">Dodaj następujące polecenie, aby przesłać zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54f32-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="54f32-304">Oprócz definicji zadania MapReduce musisz także podać nazwę klastra usługi HDInsight, której chcesz uruchomić zadanie MapReduce, a poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="54f32-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="54f32-305">AzureHDInsightJob rozpoczęcia jest wywołania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="54f32-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="54f32-306">Aby sprawdzić ukończenia zadania, użyj *AzureHDInsightJob oczekiwania* polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="54f32-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="54f32-307">Dodaj następujące polecenie, aby sprawdzić błędy dotyczące uruchomienie zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54f32-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="54f32-308">**Uruchom** nowy skrypt!</span><span class="sxs-lookup"><span data-stu-id="54f32-308">**Run** your new script!</span></span> <span data-ttu-id="54f32-309">**Kliknij przycisk** przycisk zielony execute.</span><span class="sxs-lookup"><span data-stu-id="54f32-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="54f32-310">Sprawdzenie wyników.</span><span class="sxs-lookup"><span data-stu-id="54f32-310">Check the results.</span></span> <span data-ttu-id="54f32-311">Zaloguj się do [portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="54f32-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="54f32-312">Kliknij przycisk <strong>Przeglądaj</strong> w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="54f32-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="54f32-313">Kliknij przycisk <strong>wszystko</strong> w prawym górnym rogu panelu przeglądania.</span><span class="sxs-lookup"><span data-stu-id="54f32-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="54f32-314">Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="54f32-315">Następnie znaleźć użytkownika <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z tą kolekcją dane wyjściowe określone w zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54f32-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="54f32-316">Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</span><span class="sxs-lookup"><span data-stu-id="54f32-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="54f32-317">Zobaczysz wyników zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54f32-317">You will see the results of your MapReduce job.</span></span>

      ![MapReduce wyników zapytania][image-mapreduce-query-results]

## <span data-ttu-id="54f32-319"><a name="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54f32-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="54f32-320">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="54f32-320">Congratulations!</span></span> <span data-ttu-id="54f32-321">Właśnie uruchomiono pierwszy zadań Hive, Pig i MapReduce przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54f32-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="54f32-322">Mamy Otwórz powierzając jej ich konserwację naszych łącznika usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="54f32-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="54f32-323">Jeśli chcesz, można współtworzyć na [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="54f32-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="54f32-324">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="54f32-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="54f32-325">[Tworzenie aplikacji Java z usługi Documentdb][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="54f32-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="54f32-326">[Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="54f32-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="54f32-327">[Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight do analizy użycia przenośnych słuchawki][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="54f32-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="54f32-328">[Korzystać z usługi MapReduce z usługą HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="54f32-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="54f32-329">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="54f32-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="54f32-330">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="54f32-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="54f32-331">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="54f32-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
