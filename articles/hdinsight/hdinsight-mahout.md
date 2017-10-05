---
title: "Generowanie zaleceń przy użyciu Mahout HDInsight z programu PowerShell - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać biblioteki uczenia maszynowego Apache Mahout celu generowania zaleceń filmu z usługą HDInsight (Hadoop) ze skryptu środowiska PowerShell uruchomionego na komputerze klienckim."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 934de9ca2df48b29ef7a56d5729d59d77875ea7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="89c2c-103">Generowanie zaleceń filmu przy użyciu Apache Mahout Hadoop w usłudze HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="89c2c-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="89c2c-104">Dowiedz się, jak używać [Apache Mahout](http://mahout.apache.org) maszyny biblioteki learning z usługą Azure HDInsight w celu generowania zaleceń filmu.</span><span class="sxs-lookup"><span data-stu-id="89c2c-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span> <span data-ttu-id="89c2c-105">W przykładzie w niniejszym dokumencie użyto programu Azure PowerShell do uruchamiania zadań Mahout.</span><span class="sxs-lookup"><span data-stu-id="89c2c-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89c2c-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89c2c-106">Prerequisites</span></span>

* <span data-ttu-id="89c2c-107">Klaster usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="89c2c-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="89c2c-108">Informacje o tworzeniu jedną, zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="89c2c-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c2c-109">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="89c2c-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="89c2c-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="89c2c-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="89c2c-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89c2c-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="89c2c-112"><a name="recommendations"></a>Generowanie zaleceń przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89c2c-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="89c2c-113">Zadania w tej sekcji działa przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89c2c-113">The job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="89c2c-114">Wiele klas wyposażone Mahout obecnie nie współpracujesz z programem Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89c2c-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="89c2c-115">Lista klas, które nie są obsługiwane przy użyciu programu Azure PowerShell, zobacz [Rozwiązywanie problemów](#troubleshooting) sekcji.</span><span class="sxs-lookup"><span data-stu-id="89c2c-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="89c2c-116">Na przykład przy użyciu protokołu SSH do nawiązania połączenia usługi HDInsight i uruchamiania przykładów Mahout bezpośrednio w klastrze, zobacz [Generowanie zaleceń filmu przy użyciu Mahout i HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="89c2c-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="89c2c-117">Jedną z funkcji, które są udostępniane przez Mahout jest aparatem zalecenia.</span><span class="sxs-lookup"><span data-stu-id="89c2c-117">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="89c2c-118">Ten aparat akceptuje dane w formacie `userID`, `itemId`, i `prefValue` (preferencji Użytkownicy elementu).</span><span class="sxs-lookup"><span data-stu-id="89c2c-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span></span> <span data-ttu-id="89c2c-119">Mahout używa danych w celu określenia użytkowników z preferencje podobnych elementów, które mogą być używane zaleceń.</span><span class="sxs-lookup"><span data-stu-id="89c2c-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="89c2c-120">Poniższy przykład jest uproszczone przewodnika działania procesu zalecenia:</span><span class="sxs-lookup"><span data-stu-id="89c2c-120">The following example is a simplified walk-through of how the recommendation process works:</span></span>

* <span data-ttu-id="89c2c-121">**wystąpienie wspólnej**: Jan, Alicja i Robert wszystkie zbędne *słów*, *ponownie ataki Empire*, i *powrotu Jedi*.</span><span class="sxs-lookup"><span data-stu-id="89c2c-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="89c2c-122">Mahout Określa, że użytkownicy, którzy także, takich jak jeden z tych filmów, takich jak pozostałe dwa.</span><span class="sxs-lookup"><span data-stu-id="89c2c-122">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="89c2c-123">**wystąpienie wspólnej**: Robert i Alicja również zbędne *zagrożenie fantom*, *ataku klonów*, i *zemsty Sith*.</span><span class="sxs-lookup"><span data-stu-id="89c2c-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="89c2c-124">Mahout Określa, że użytkownicy, którzy także zbędne poprzednie trzy filmów, takich jak te filmów.</span><span class="sxs-lookup"><span data-stu-id="89c2c-124">Mahout determines that users who liked the previous three movies also like these movies.</span></span>

* <span data-ttu-id="89c2c-125">**Zalecenie podobieństwa**: ponieważ Jan zbędne pierwsze trzy filmów, Mahout analizuje filmy tej osoby z podobne preferencje zbędne, ale Jan nie ma obserwowane (zbędne/klasyfikowane).</span><span class="sxs-lookup"><span data-stu-id="89c2c-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="89c2c-126">W takim przypadku zaleca Mahout *zagrożenie fantom*, *ataku klonów*, i *zemsty Sith*.</span><span class="sxs-lookup"><span data-stu-id="89c2c-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="89c2c-127">Opis danych</span><span class="sxs-lookup"><span data-stu-id="89c2c-127">Understanding the data</span></span>

<span data-ttu-id="89c2c-128">[Badania GroupLens] [ movielens] zapewnia filmów w formacie, który jest zgodny z Mahout klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="89c2c-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="89c2c-129">Dane te są dostępne na domyślny magazyn dla klastra w `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="89c2c-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="89c2c-130">Istnieją dwa pliki `moviedb.txt` (informacje na temat filmów) i `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="89c2c-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="89c2c-131">`user-ratings.txt` Plik jest używany podczas analizy.</span><span class="sxs-lookup"><span data-stu-id="89c2c-131">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="89c2c-132">`moviedb.txt` Pliku służy do zapewnienia tekst przyjazną dla użytkownika, wyświetlając wyniki analizy.</span><span class="sxs-lookup"><span data-stu-id="89c2c-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span></span>

<span data-ttu-id="89c2c-133">Dane zawarte w ratings.txt użytkownika ma struktury `userID`, `movieID`, `userRating`, i `timestamp`, który informuje NAS jak bardzo każdego użytkownika oceną filmu.</span><span class="sxs-lookup"><span data-stu-id="89c2c-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="89c2c-134">Oto przykładowe dane:</span><span class="sxs-lookup"><span data-stu-id="89c2c-134">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-the-job"></a><span data-ttu-id="89c2c-135">Uruchamianie zadania</span><span class="sxs-lookup"><span data-stu-id="89c2c-135">Run the job</span></span>

<span data-ttu-id="89c2c-136">Użyj następującego skryptu programu Windows PowerShell do uruchomienia zadania, które używa aparatu zalecenie Mahout z danymi film:</span><span class="sxs-lookup"><span data-stu-id="89c2c-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="89c2c-137">Ten plik monituje o informacje, które służą do łączenia się z klastrem usługi HDInsight i uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="89c2c-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span></span> <span data-ttu-id="89c2c-138">Może upłynąć kilka minut na zakończenie i Pobierz plik output.txt zadań.</span><span class="sxs-lookup"><span data-stu-id="89c2c-138">It may take several minutes for the jobs to complete and download the output.txt file.</span></span>

<span data-ttu-id="89c2c-139">[!code-powershell[główne](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span><span class="sxs-lookup"><span data-stu-id="89c2c-139">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span></span>

> [!NOTE]
> <span data-ttu-id="89c2c-140">Mahout zadania nie należy usuwać dane tymczasowe, który jest tworzony podczas przetwarzania zadania.</span><span class="sxs-lookup"><span data-stu-id="89c2c-140">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="89c2c-141">`--tempDir` Parametr jest określony w zadaniu przykład aby wyodrębnić pliki tymczasowe w określonym katalogu.</span><span class="sxs-lookup"><span data-stu-id="89c2c-141">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span></span>

<span data-ttu-id="89c2c-142">Zadanie Mahout nie zwraca dane wyjściowe stdout.</span><span class="sxs-lookup"><span data-stu-id="89c2c-142">The Mahout job does not return the output to STDOUT.</span></span> <span data-ttu-id="89c2c-143">Zamiast tego, przechowuje go w katalogu określonym produktem wyjściowym jako **części r-00000**.</span><span class="sxs-lookup"><span data-stu-id="89c2c-143">Instead, it stores it in the specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="89c2c-144">Ten plik, aby pliki do pobrania skryptu **output.txt** w bieżącym katalogu na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="89c2c-144">The script downloads this file to **output.txt** in the current directory on your workstation.</span></span>

<span data-ttu-id="89c2c-145">Przykładem zawartości tego pliku jest następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="89c2c-145">The following text is an example of the content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="89c2c-146">Pierwsza kolumna `userID`.</span><span class="sxs-lookup"><span data-stu-id="89c2c-146">The first column is the `userID`.</span></span> <span data-ttu-id="89c2c-147">Wartości zawartych w "[" i "]" są `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="89c2c-147">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="89c2c-148">Skrypt również pobiera `moviedb.txt` i `user-ratings.txt` pliki, które są potrzebne do formatowania danych wyjściowych, aby było bardziej czytelne.</span><span class="sxs-lookup"><span data-stu-id="89c2c-148">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span></span>

### <a name="view-the-output"></a><span data-ttu-id="89c2c-149">Wyświetl dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="89c2c-149">View the output</span></span>

<span data-ttu-id="89c2c-150">Chociaż wygenerowanych danych wyjściowych może być OK do użycia w aplikacji, nie jest przyjazną dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89c2c-150">Although the generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="89c2c-151">`moviedb.txt` z serwera może być używany do rozpoznania `movieId` na nazwę filmu.</span><span class="sxs-lookup"><span data-stu-id="89c2c-151">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span></span> <span data-ttu-id="89c2c-152">Umożliwia wyświetlanie zaleceń o nazwach filmu następujący skrypt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="89c2c-152">Use the following PowerShell script to display recommendations with movie names:</span></span>

<span data-ttu-id="89c2c-153">[!code-powershell[główne](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span><span class="sxs-lookup"><span data-stu-id="89c2c-153">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span></span>

<span data-ttu-id="89c2c-154">Aby wyświetlić zalecenia w formacie przyjazną dla użytkownika, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="89c2c-154">Use the following command to display the recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="89c2c-155">Dane wyjściowe będą podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="89c2c-155">The output is similar to the following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, The (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of the Dove, The (1997)            4.6666665
    People vs. Larry Flynt, The (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="89c2c-156"><a name="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="89c2c-156"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="89c2c-157">Nie można zastąpić pliki</span><span class="sxs-lookup"><span data-stu-id="89c2c-157">Cannot overwrite files</span></span>

<span data-ttu-id="89c2c-158">Wykonaj zadania mahout nie oczyszczania plików tymczasowych, które zostały utworzone podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="89c2c-158">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="89c2c-159">Ponadto zadania nie zastępuj istniejącego pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="89c2c-159">In addition, the jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="89c2c-160">Aby uniknąć błędów podczas uruchamiania zadania Mahout, Usuń pliki tymczasowe i dane wyjściowe między działa.</span><span class="sxs-lookup"><span data-stu-id="89c2c-160">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="89c2c-161">Aby usunąć pliki tworzone przez skrypty wcześniej w tym dokumencie, użyj następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="89c2c-161">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have to get a list and delete one at a time
# Start with the output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next the temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="89c2c-162"><a name="nopowershell"></a>Klasy, które nie są obsługiwane przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89c2c-162"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="89c2c-163">Zadania mahout, używane przez następujące klasy zwracać różne komunikaty o błędach w przypadku używania z programu Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="89c2c-163">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="89c2c-164">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="89c2c-164">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="89c2c-165">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="89c2c-165">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="89c2c-166">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="89c2c-166">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="89c2c-167">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="89c2c-167">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="89c2c-168">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="89c2c-168">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="89c2c-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="89c2c-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="89c2c-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="89c2c-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="89c2c-171">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="89c2c-171">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="89c2c-172">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="89c2c-172">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="89c2c-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="89c2c-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="89c2c-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="89c2c-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="89c2c-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="89c2c-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="89c2c-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="89c2c-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="89c2c-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="89c2c-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="89c2c-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="89c2c-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="89c2c-179">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="89c2c-179">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="89c2c-180">Aby uruchomić zadania korzystające z tych klas, połącz się z klastrem usługi HDInsight przy użyciu protokołu SSH, a następnie uruchom zadania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="89c2c-180">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span></span> <span data-ttu-id="89c2c-181">Na przykład do uruchomienia zadań Mahout przy użyciu protokołu SSH, zobacz [Generowanie zaleceń filmu przy użyciu Mahout i HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="89c2c-181">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89c2c-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89c2c-182">Next steps</span></span>

<span data-ttu-id="89c2c-183">Teraz, kiedy znasz sposobu używania Mahout, odnajdywanie inne sposoby pracy z danymi w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="89c2c-183">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="89c2c-184">Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="89c2c-184">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="89c2c-185">Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="89c2c-185">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="89c2c-186">MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="89c2c-186">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
