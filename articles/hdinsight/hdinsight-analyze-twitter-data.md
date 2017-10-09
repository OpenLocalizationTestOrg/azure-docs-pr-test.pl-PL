---
title: "aaaAnalyze danych Twitter z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Hive tooanalyze Twitter danych na platformie Hadoop w HDInsight toofind hello częstotliwości użycia określonego wyrazu."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="5fca9-103">Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="5fca9-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="5fca9-104">Społecznościowych witryn sieci Web są jednym z głównych wymusza pobudzenie hello przyjmowania danych big data.</span><span class="sxs-lookup"><span data-stu-id="5fca9-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="5fca9-105">Publiczny interfejsów API dostarczonych przez witryn, takie jak Twitter są użyteczne źródło danych do analizowania i zrozumienie trendów popularnych.</span><span class="sxs-lookup"><span data-stu-id="5fca9-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="5fca9-106">W tym samouczku zostanie uzyskać tweetów za pomocą usługi Twitter, przesyłanie strumieniowe interfejsu API, a następnie użyj Apache Hive w usłudze Azure HDInsight tooget listę użytkowników usługi Twitter, których wysłane hello większość tweetów, zawierających określony wyraz.</span><span class="sxs-lookup"><span data-stu-id="5fca9-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fca9-107">Witaj czynności w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="5fca9-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="5fca9-108">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5fca9-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="5fca9-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="5fca9-110">Dla klastra opartych na systemie Linux tooa określonych czynności [Twitter analizowanie danych przy użyciu Hive w usłudze HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5fca9-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fca9-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5fca9-111">Prerequisites</span></span>
<span data-ttu-id="5fca9-112">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="5fca9-113">**Stacja robocza** przy użyciu programu Azure PowerShell zainstalowana i skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="5fca9-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="5fca9-114">tooexecute skryptów programu Windows PowerShell, należy uruchomić program Azure PowerShell jako administrator i ustawić zasady wykonywania hello także*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="5fca9-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="5fca9-115">Zobacz [skryptów programu Windows PowerShell Uruchom][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="5fca9-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="5fca9-116">Przed uruchomieniem skryptów programu Windows PowerShell, upewnij się, że są połączone tooyour subskrypcji platformy Azure przy użyciu następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="5fca9-117">Jeśli masz wiele subskrypcji Azure, użyj następującego polecenia cmdlet tooset hello bieżącej subskrypcji hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="5fca9-118">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5fca9-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="5fca9-119">Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5fca9-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="5fca9-120">Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fca9-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="5fca9-121">Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5fca9-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="5fca9-122">**Klaster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="5fca9-123">Aby uzyskać instrukcje dotyczące inicjowania obsługi klastra, zobacz [rozpocząć korzystanie z usługi HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="5fca9-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="5fca9-124">Nazwa klastra hello trzeba będzie później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="5fca9-125">Witaj poniższej tabeli wymieniono pliki hello używane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="5fca9-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="5fca9-126">Pliki</span><span class="sxs-lookup"><span data-stu-id="5fca9-126">Files</span></span> | <span data-ttu-id="5fca9-127">Opis</span><span class="sxs-lookup"><span data-stu-id="5fca9-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5fca9-128">/Tutorials/Twitter/Data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="5fca9-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="5fca9-129">Witaj źródło danych pod kątem hello zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="5fca9-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="5fca9-130">/Tutorials/Twitter/Output</span><span class="sxs-lookup"><span data-stu-id="5fca9-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="5fca9-131">folder wyjściowy Hello hello zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="5fca9-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="5fca9-132">Witaj domyślną nazwę pliku wyjściowego zadania Hive jest **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="5fca9-133">Tutorials/Twitter/Twitter.hql</span><span class="sxs-lookup"><span data-stu-id="5fca9-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="5fca9-134">plik skryptu HiveQL Hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="5fca9-135">/Tutorials/Twitter/JobStatus</span><span class="sxs-lookup"><span data-stu-id="5fca9-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="5fca9-136">Witaj stan zadania usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5fca9-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="5fca9-137">Twitter Get źródła danych</span><span class="sxs-lookup"><span data-stu-id="5fca9-137">Get Twitter feed</span></span>
<span data-ttu-id="5fca9-138">W tym samouczku użyjesz hello [przesyłania strumieniowego interfejsów API w usłudze Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="5fca9-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="5fca9-139">Witaj określonych Twitter przesyłania strumieniowego korzystasz z interfejsu API jest [stanów/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="5fca9-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="5fca9-140">Plik zawierający 10 000 tweetów i plik skryptu Hive hello (opisane w następnej sekcji hello) zostały przekazane w publicznego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="5fca9-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="5fca9-141">W tej sekcji można pominąć, jeśli chcesz toouse hello przekazać pliki.</span><span class="sxs-lookup"><span data-stu-id="5fca9-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="5fca9-142">[Tweetów danych](https://dev.twitter.com/docs/platform-objects/tweets) są przechowywane w formacie JavaScript Object Notation (JSON) hello, który zawiera złożone, zagnieżdżone struktury.</span><span class="sxs-lookup"><span data-stu-id="5fca9-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="5fca9-143">Zamiast zapisywania wielu wierszy kodu, korzystając z konwencjonalnej język programowania, można przekształcić tej struktury zagnieżdżone do tabeli programu Hive, dzięki czemu mogą być przeszukiwane przez język SQL (Structured Query) — takie jak języka o nazwie HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5fca9-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="5fca9-144">Twitter używa API tooits dostępu tooprovide autoryzacji OAuth.</span><span class="sxs-lookup"><span data-stu-id="5fca9-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="5fca9-145">OAuth to protokół uwierzytelniania, umożliwiający użytkownikom tooapprove aplikacji tooact w ich imieniu bez udostępniania swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="5fca9-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="5fca9-146">Więcej informacji można znaleźć w folderze [oauth.net](http://oauth.net/) lub hello znakomity [tooOAuth przewodnik dla początkujących](http://hueniverse.com/oauth/) z Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="5fca9-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="5fca9-147">Witaj pierwszy krok toouse OAuth jest toocreate nową aplikację w witrynie Twitter Developer hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="5fca9-148">**toocreate aplikacji Twitter**</span><span class="sxs-lookup"><span data-stu-id="5fca9-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="5fca9-149">Zaloguj się za[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="5fca9-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="5fca9-150">Kliknij przycisk hello **Zamów teraz** łącza, jeśli nie masz konta w usłudze Twitter.</span><span class="sxs-lookup"><span data-stu-id="5fca9-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="5fca9-151">Kliknij przycisk **Utwórz nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="5fca9-152">Wprowadź **nazwa**, **opis**, **witryny sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="5fca9-153">Można uzupełnić adres URL hello **witryny sieci Web** pola.</span><span class="sxs-lookup"><span data-stu-id="5fca9-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="5fca9-154">Witaj w poniższej tabeli przedstawiono niektóre przykładowe wartości toouse:</span><span class="sxs-lookup"><span data-stu-id="5fca9-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="5fca9-155">Pole</span><span class="sxs-lookup"><span data-stu-id="5fca9-155">Field</span></span> | <span data-ttu-id="5fca9-156">Wartość</span><span class="sxs-lookup"><span data-stu-id="5fca9-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="5fca9-157">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5fca9-157">Name</span></span> |<span data-ttu-id="5fca9-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="5fca9-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="5fca9-159">Opis</span><span class="sxs-lookup"><span data-stu-id="5fca9-159">Description</span></span> |<span data-ttu-id="5fca9-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="5fca9-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="5fca9-161">Witryna sieci Web</span><span class="sxs-lookup"><span data-stu-id="5fca9-161">Website</span></span> |<span data-ttu-id="5fca9-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="5fca9-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="5fca9-163">Sprawdź **tak, zgadzam się**, a następnie kliknij przycisk **tworzenie aplikacji Twitter**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="5fca9-164">Kliknij przycisk hello **uprawnienia** kartę hello domyślne uprawnienia **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="5fca9-165">To jest wystarczająca dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="5fca9-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="5fca9-166">Kliknij przycisk hello **kluczy i tokenów dostępu** kartę.</span><span class="sxs-lookup"><span data-stu-id="5fca9-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="5fca9-167">Kliknij przycisk **Utwórz moje tokenu dostępu**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="5fca9-168">Kliknij przycisk **OAuth testu** w hello prawym górnym rogu strony hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="5fca9-169">Zapisz **konsumenta**, **klucz tajny klienta**, **token dostępu**, i **klucz tajny tokenu dostępu**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="5fca9-170">Potrzebujesz wartości hello później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="5fca9-171">W tym samouczku użyjesz wywołania usługi sieci web hello toomake środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fca9-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="5fca9-172">C# .NET przykładowy, [analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="5fca9-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="5fca9-173">Witaj wywołania usługi sieci web innych popularnych narzędzie toomake jest [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="5fca9-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="5fca9-174">Zwinięcie można pobrać z [tutaj][curl-download].</span><span class="sxs-lookup"><span data-stu-id="5fca9-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="5fca9-175">Korzystając z polecenia curl hello w systemie Windows, użyj podwójnych cudzysłowów zamiast apostrofy dla wartości opcji hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="5fca9-176">**tweetów tooget**</span><span class="sxs-lookup"><span data-stu-id="5fca9-176">**tooget tweets**</span></span>

1. <span data-ttu-id="5fca9-177">Otwórz hello Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="5fca9-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="5fca9-178">(Na ekranie powitania Start systemu Windows 8, wpisz **PowerShell_ISE** , a następnie kliknij przycisk **programu Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="5fca9-179">Zobacz [uruchomić środowisko Windows PowerShell w systemie Windows 8 i Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="5fca9-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="5fca9-180">Skopiuj hello następującego skryptu w okienku skryptów hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="5fca9-181">Ustaw hello pierwsze pięć tooeight zmienne w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="5fca9-182">Zmienna</span><span class="sxs-lookup"><span data-stu-id="5fca9-182">Variable</span></span>|<span data-ttu-id="5fca9-183">Opis</span><span class="sxs-lookup"><span data-stu-id="5fca9-183">Description</span></span>
    ---|---
    <span data-ttu-id="5fca9-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="5fca9-184">$clusterName</span></span>|<span data-ttu-id="5fca9-185">Jest to nazwa hello klastra usługi HDInsight hello miejscu aplikacji hello toorun.</span><span class="sxs-lookup"><span data-stu-id="5fca9-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="5fca9-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="5fca9-186">$oauth_consumer_key</span></span>|<span data-ttu-id="5fca9-187">To jest aplikacja usługi Twitter hello **konsumenta** zapisanej wcześniej podczas tworzenia aplikacji Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="5fca9-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="5fca9-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="5fca9-189">To jest aplikacja usługi Twitter hello **klucz tajny klienta** zapisanej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="5fca9-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="5fca9-190">$oauth_token</span></span>|<span data-ttu-id="5fca9-191">To jest aplikacja usługi Twitter hello **token dostępu** zapisanej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="5fca9-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="5fca9-192">$oauth_token_secret</span></span>|<span data-ttu-id="5fca9-193">To jest aplikacja usługi Twitter hello **klucz tajny tokenu dostępu** zapisanej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="5fca9-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="5fca9-194">$destBlobName</span></span>|<span data-ttu-id="5fca9-195">Jest to nazwa obiektu blob danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-195">This is hello output blob name.</span></span> <span data-ttu-id="5fca9-196">Witaj, wartość domyślna to **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="5fca9-197">Jeśli zmienisz hello wartość domyślną, konieczne będzie skryptów programu Windows PowerShell hello tooupdate odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="5fca9-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="5fca9-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="5fca9-198">$trackString</span></span>|<span data-ttu-id="5fca9-199">Usługa sieci web Hello zwróci słowa kluczowe powiązane toothese tweetów.</span><span class="sxs-lookup"><span data-stu-id="5fca9-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="5fca9-200">Witaj, wartość domyślna to **HDInsight Azure, chmury,**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="5fca9-201">Zmiana wartości domyślnej hello odpowiednio spowoduje zaktualizowanie hello skryptów programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fca9-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="5fca9-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="5fca9-202">$lineMax</span></span>|<span data-ttu-id="5fca9-203">wartość Hello Określa, ile skryptu hello tweetów będzie odczytywać.</span><span class="sxs-lookup"><span data-stu-id="5fca9-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="5fca9-204">Trwa około 3 minuty tooread tweetów 100.</span><span class="sxs-lookup"><span data-stu-id="5fca9-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="5fca9-205">Można ustawić większą liczbę, ale ich może zająć więcej czasu toodownload.</span><span class="sxs-lookup"><span data-stu-id="5fca9-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="5fca9-206">Naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="5fca9-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="5fca9-207">Jeśli wystąpiły problemy, jako obejście, wybierz wszystkie wiersze hello, a następnie naciśnij klawisz **F8**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="5fca9-208">Zostanie wyświetlona "Zakończ"!</span><span class="sxs-lookup"><span data-stu-id="5fca9-208">You shall see "Complete!"</span></span> <span data-ttu-id="5fca9-209">na końcu hello hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5fca9-209">at hello end of hello output.</span></span> <span data-ttu-id="5fca9-210">Komunikaty o błędach pojawi się czerwone.</span><span class="sxs-lookup"><span data-stu-id="5fca9-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="5fca9-211">Jako procedury weryfikacji można sprawdzić pliku wyjściowego hello **/tutorials/twitter/data/tweets.txt**, w magazynie obiektów Blob platformy Azure za pomocą Eksploratora usługi storage platformy Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fca9-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="5fca9-212">Aby uzyskać przykładowy skrypt programu Windows PowerShell do wyświetlania listy plików, zobacz [magazynu obiektów Blob użycia z usługą HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="5fca9-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="5fca9-213">Utwórz skrypt HiveQL</span><span class="sxs-lookup"><span data-stu-id="5fca9-213">Create HiveQL script</span></span>
<span data-ttu-id="5fca9-214">Przy użyciu programu Azure PowerShell, można uruchomić wiele instrukcje HiveQL co w czasie, lub pakietu hello instrukcji HiveQL do pliku skryptu.</span><span class="sxs-lookup"><span data-stu-id="5fca9-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="5fca9-215">W tym samouczku utworzysz skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5fca9-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="5fca9-216">plik skryptu Hello musi być przekazana tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="5fca9-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="5fca9-217">W następnej sekcji hello należy uruchomić plik skryptu hello przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fca9-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="5fca9-218">plik skryptu Hive Hello i plik zawierający 10 000 tweetów zostały przekazane w publicznego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="5fca9-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="5fca9-219">W tej sekcji można pominąć, jeśli chcesz toouse hello przekazać pliki.</span><span class="sxs-lookup"><span data-stu-id="5fca9-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="5fca9-220">Witaj skrypt HiveQL zostaną wykonane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="5fca9-221">**Witaj tweets_raw tabelę** w przypadku, gdy tabela hello już istnieje.</span><span class="sxs-lookup"><span data-stu-id="5fca9-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="5fca9-222">**Tworzenie tabeli Hive tweets_raw hello**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="5fca9-223">Ta gałąź strukturalnych Tabela tymczasowa przechowuje dane powitania dla dalszego wyodrębniania, transformacji i ładowania (ETL) przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="5fca9-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="5fca9-224">Aby uzyskać informacje na partycje, zobacz [samouczek Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="5fca9-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="5fca9-225">**Ładowanie danych** z folderu źródłowego hello, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="5fca9-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="5fca9-226">teraz została przekształcona Hello dużych tweetów dataset w formacie JSON zagnieżdżonych w strukturze tabeli tymczasowej gałęzi.</span><span class="sxs-lookup"><span data-stu-id="5fca9-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="5fca9-227">**Upuść hello tweetów tabeli** w przypadku, gdy tabela hello już istnieje.</span><span class="sxs-lookup"><span data-stu-id="5fca9-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="5fca9-228">**Utwórz tabelę tweetów hello**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-228">**Create hello tweets table**.</span></span> <span data-ttu-id="5fca9-229">Aby przed dataset tweetów hello można badać przy korzystaniu z programu Hive, musisz toorun inny proces ETL.</span><span class="sxs-lookup"><span data-stu-id="5fca9-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="5fca9-230">Ten proces ETL definiuje bardziej szczegółowe schemat tabeli hello danych, które są przechowywane w tabeli "twitter_raw" hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="5fca9-231">**Wstaw tabelę Zastąp**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-231">**Insert overwrite table**.</span></span> <span data-ttu-id="5fca9-232">To złożony skryptu Hive zostanie zaczną działać poza zestaw długich zadań MapReduce przez hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5fca9-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="5fca9-233">W zależności od rozmiar zestawu danych i hello klastra może to potrwać około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="5fca9-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="5fca9-234">**Wstaw zastąpić katalogu**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="5fca9-235">Uruchom zapytanie i dane wyjściowe plik tooa dataset hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="5fca9-236">To zapytanie spowoduje zwrócenie listy użytkowników usługi Twitter wysyłane większość tweetów, znajdujące się na powitania word "Azure".</span><span class="sxs-lookup"><span data-stu-id="5fca9-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="5fca9-237">**toocreate gałąź skryptów i przekaż go tooAzure**</span><span class="sxs-lookup"><span data-stu-id="5fca9-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="5fca9-238">Otwórz program Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="5fca9-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="5fca9-239">Skopiuj hello następującego skryptu w okienku skryptów hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-239">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="5fca9-240">Ustaw hello najpierw dwie zmienne w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="5fca9-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="5fca9-241">Zmienna</span><span class="sxs-lookup"><span data-stu-id="5fca9-241">Variable</span></span> | <span data-ttu-id="5fca9-242">Opis</span><span class="sxs-lookup"><span data-stu-id="5fca9-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="5fca9-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="5fca9-243">$clusterName</span></span> |<span data-ttu-id="5fca9-244">Wprowadź nazwę klastra usługi HDInsight hello, w której mają toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5fca9-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="5fca9-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="5fca9-245">$subscriptionID</span></span> |<span data-ttu-id="5fca9-246">Wprowadź swój identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5fca9-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="5fca9-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="5fca9-247">$sourceDataPath</span></span> |<span data-ttu-id="5fca9-248">Witaj gdzie zapytań programu Hive hello będzie odczytywać dane hello lokalizacji magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5fca9-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="5fca9-249">Nie trzeba toochange tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="5fca9-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="5fca9-250">$outputPath</span></span> |<span data-ttu-id="5fca9-251">Witaj lokalizacji magazynu obiektów Blob platformy Azure, gdzie zapytań programu Hive hello dane wyjściowe obejmują hello wyników.</span><span class="sxs-lookup"><span data-stu-id="5fca9-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="5fca9-252">Nie trzeba toochange tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="5fca9-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="5fca9-253">$hqlScriptFile</span></span> |<span data-ttu-id="5fca9-254">Witaj lokalizację i nazwę pliku hello pliku skryptu hello HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5fca9-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="5fca9-255">Nie trzeba toochange tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="5fca9-256">Naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="5fca9-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="5fca9-257">Jeśli wystąpiły problemy, jako obejście, wybierz wszystkie wiersze hello, a następnie naciśnij klawisz **F8**.</span><span class="sxs-lookup"><span data-stu-id="5fca9-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="5fca9-258">Zostanie wyświetlona "Zakończ"!</span><span class="sxs-lookup"><span data-stu-id="5fca9-258">You shall see "Complete!"</span></span> <span data-ttu-id="5fca9-259">na końcu hello hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5fca9-259">at hello end of hello output.</span></span> <span data-ttu-id="5fca9-260">Komunikaty o błędach pojawi się czerwone.</span><span class="sxs-lookup"><span data-stu-id="5fca9-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="5fca9-261">Jako procedury weryfikacji można sprawdzić pliku wyjściowego hello **/tutorials/twitter/twitter.hql**, w magazynie obiektów Blob platformy Azure za pomocą Eksploratora usługi storage platformy Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fca9-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="5fca9-262">Aby uzyskać przykładowy skrypt programu Windows PowerShell do wyświetlania listy plików, zobacz [magazynu obiektów Blob użycia z usługą HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="5fca9-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="5fca9-263">Przetwarzaj dane Twitter przy użyciu usługi Hive</span><span class="sxs-lookup"><span data-stu-id="5fca9-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="5fca9-264">Zakończono wszystkie hello prac.</span><span class="sxs-lookup"><span data-stu-id="5fca9-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="5fca9-265">Można teraz wywołać skryptu Hive hello i hello wyniki sprawdzenia.</span><span class="sxs-lookup"><span data-stu-id="5fca9-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="5fca9-266">Przesłać zadania technologii Hive</span><span class="sxs-lookup"><span data-stu-id="5fca9-266">Submit a Hive job</span></span>
<span data-ttu-id="5fca9-267">Użyj następującego skryptu Hive hello toorun skrypt programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="5fca9-268">Konieczne będzie tooset hello pierwszej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5fca9-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="5fca9-269">Witaj toouse tweetów i skrypt HiveQL, który został przekazany w hello ostatnich dwóch sekcjach too"/tutorials/twitter/twitter.hql $hqlScriptFile zestaw hello".</span><span class="sxs-lookup"><span data-stu-id="5fca9-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="5fca9-270">toouse hello te, które zostały przekazane tooa publicznego obiektu blob dla Ciebie, ustawić $hqlScriptFile także"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="5fca9-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="5fca9-271">Sprawdzanie wyników hello</span><span class="sxs-lookup"><span data-stu-id="5fca9-271">Check hello results</span></span>
<span data-ttu-id="5fca9-272">Użyj następującego skryptu programu Windows PowerShell, toocheck hello dane wyjściowe zadania Hive hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="5fca9-273">Należy najpierw dwie zmienne hello tooset.</span><span class="sxs-lookup"><span data-stu-id="5fca9-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabelę programu Hive Hello używa \001 hello ogranicznik pola. <span data-ttu-id="5fca9-275">Ogranicznik Hello nie jest widoczny w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="5fca9-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="5fca9-276">Po wyniki analizy hello zostały umieszczone w magazynie obiektów Blob platformy Azure, można wyeksportować hello danych tooan Azure SQL bazy danych/programu SQL server, wyeksportować hello tooExcel danych za pomocą dodatku Power Query lub połączyć dane toohello aplikacji przy użyciu hello Hive sterownik ODBC.</span><span class="sxs-lookup"><span data-stu-id="5fca9-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="5fca9-277">Aby uzyskać więcej informacji, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop], [analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-delay-data], [ Łączenie programu Excel tooHDInsight z dodatku Power Query][hdinsight-power-query], i [tooHDInsight łączenie programu Excel z hello sterownik Microsoft Hive ODBC][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="5fca9-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fca9-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fca9-278">Next steps</span></span>
<span data-ttu-id="5fca9-279">W tym samouczku zaobserwowano, jak tootransform bez struktury zestawu danych JSON w strukturze tooquery tabeli Hive Eksplorowanie i analizowanie danych z serwisem Twitter przy użyciu usługi HDInsight w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="5fca9-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="5fca9-280">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="5fca9-280">toolearn more, see:</span></span>

* <span data-ttu-id="5fca9-281">[Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="5fca9-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="5fca9-282">[Analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="5fca9-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="5fca9-283">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="5fca9-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="5fca9-284">[Łączenie programu Excel tooHDInsight z dodatku Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="5fca9-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="5fca9-285">[Łączenie programu Excel tooHDInsight z hello sterownik Microsoft Hive ODBC][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="5fca9-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="5fca9-286">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5fca9-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
