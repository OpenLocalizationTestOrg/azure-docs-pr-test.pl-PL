---
title: "zalecenia aaaGenerate przy użyciu Mahout HDInsight z programu PowerShell - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Apache Mahout machine learning zaleceń filmu toogenerate biblioteki z usługą HDInsight (Hadoop) z skryptu programu PowerShell uruchomionego na komputerze klienckim."
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
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="118fe-103">Generowanie zaleceń filmu przy użyciu Apache Mahout Hadoop w usłudze HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="118fe-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="118fe-104">Dowiedz się, jak toouse hello [Apache Mahout](http://mahout.apache.org) maszyny biblioteki uczenie na podstawie zaleceń filmu toogenerate Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="118fe-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="118fe-105">przykład Witaj w tym dokumencie korzysta z programu Azure PowerShell toorun Mahout zadania.</span><span class="sxs-lookup"><span data-stu-id="118fe-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="118fe-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="118fe-106">Prerequisites</span></span>

* <span data-ttu-id="118fe-107">Klaster usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="118fe-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="118fe-108">Informacje o tworzeniu jedną, zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="118fe-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="118fe-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="118fe-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="118fe-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="118fe-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="118fe-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="118fe-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="118fe-112"><a name="recommendations"></a>Generowanie zaleceń przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="118fe-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="118fe-113">zadanie Hello w tej sekcji działa przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="118fe-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="118fe-114">Wiele klas hello wyposażone Mahout obecnie nie współpracujesz z programem Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="118fe-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="118fe-115">Lista klas, które nie są obsługiwane przy użyciu programu Azure PowerShell, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji.</span><span class="sxs-lookup"><span data-stu-id="118fe-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="118fe-116">Na przykład za pomocą SSH tooconnect tooHDInsight i uruchamiania przykładów Mahout bezpośrednio w klastrze hello, zobacz [Generowanie zaleceń filmu przy użyciu Mahout i HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="118fe-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="118fe-117">Jedną z hello funkcje, które są udostępniane przez Mahout jest aparatem zalecenie.</span><span class="sxs-lookup"><span data-stu-id="118fe-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="118fe-118">Ten aparat akceptuje dane w formacie hello `userID`, `itemId`, i `prefValue` (hello preferencji Użytkownicy hello elementu).</span><span class="sxs-lookup"><span data-stu-id="118fe-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="118fe-119">Mahout używa hello danych toodetermine użytkowników o podobnych elementów preferencji, które mogą być używane toomake zalecenia.</span><span class="sxs-lookup"><span data-stu-id="118fe-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="118fe-120">Witaj poniższy przykład jest uproszczone przewodnika działania procesu zalecenie hello:</span><span class="sxs-lookup"><span data-stu-id="118fe-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="118fe-121">**wystąpienie wspólnej**: Jan, Alicja i Robert wszystkie zbędne *słów*, *Witaj ponownie ataki Empire*, i *powrotu hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="118fe-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="118fe-122">Mahout Określa, że użytkownicy, którzy jak jeden z tych filmy również, takich jak hello pozostałe dwa.</span><span class="sxs-lookup"><span data-stu-id="118fe-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="118fe-123">**wystąpienie wspólnej**: Robert i Alicja również zbędne *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="118fe-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="118fe-124">Mahout Określa, że użytkownicy, którzy także zbędne hello poprzednie trzy filmów, takich jak te filmów.</span><span class="sxs-lookup"><span data-stu-id="118fe-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="118fe-125">**Zalecenie podobieństwa**: ponieważ Jan zbędne hello pierwsze trzy filmów, Mahout analizuje filmy tej osoby z podobne preferencje zbędne, ale Jan nie ma obserwowane (zbędne/klasyfikowane).</span><span class="sxs-lookup"><span data-stu-id="118fe-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="118fe-126">W takim przypadku zaleca Mahout *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="118fe-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="118fe-127">Opis hello danych</span><span class="sxs-lookup"><span data-stu-id="118fe-127">Understanding hello data</span></span>

<span data-ttu-id="118fe-128">[Badania GroupLens] [ movielens] zapewnia filmów w formacie, który jest zgodny z Mahout klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="118fe-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="118fe-129">Dane te są dostępne na powitania domyślny magazyn dla klastra w `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="118fe-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="118fe-130">Istnieją dwa pliki `moviedb.txt` (informacje na temat filmów hello) i `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="118fe-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="118fe-131">Witaj `user-ratings.txt` plik jest używany podczas analizy.</span><span class="sxs-lookup"><span data-stu-id="118fe-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="118fe-132">Witaj `moviedb.txt` pliku jest wartością tekstową przyjazną dla użytkownika tooprovide używane przy wyświetlaniu wyników hello hello analizy.</span><span class="sxs-lookup"><span data-stu-id="118fe-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="118fe-133">Witaj dane zawarte w ratings.txt użytkownika ma struktury `userID`, `movieID`, `userRating`, i `timestamp`, który informuje NAS jak bardzo każdego użytkownika oceną filmu.</span><span class="sxs-lookup"><span data-stu-id="118fe-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="118fe-134">Oto przykład hello danych:</span><span class="sxs-lookup"><span data-stu-id="118fe-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="118fe-135">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="118fe-135">Run hello job</span></span>

<span data-ttu-id="118fe-136">Użyj powitania po toorun skrypt programu Windows PowerShell zadanie, które używa aparatu zalecenie Mahout hello z danymi filmu hello:</span><span class="sxs-lookup"><span data-stu-id="118fe-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="118fe-137">Ten plik wyświetla monit o podanie informacji o klastra usługi HDInsight używane tooconnect tooyour i wykonywania zadań.</span><span class="sxs-lookup"><span data-stu-id="118fe-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="118fe-138">Może potrwać kilka minut hello toocomplete zadania i Pobierz plik output.txt hello.</span><span class="sxs-lookup"><span data-stu-id="118fe-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="118fe-139">Mahout zadania nie należy usuwać dane tymczasowe, który jest tworzony podczas przetwarzania zadania hello.</span><span class="sxs-lookup"><span data-stu-id="118fe-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="118fe-140">Witaj `--tempDir` określony parametr w hello przykładowe zadania tooisolate hello tymczasowe pliki w określonym katalogu.</span><span class="sxs-lookup"><span data-stu-id="118fe-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="118fe-141">zadanie Mahout Hello nie zwraca hello tooSTDOUT danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="118fe-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="118fe-142">Zamiast tego, przechowuje go w katalogu określonym produktem wyjściowym hello co **części r-00000**.</span><span class="sxs-lookup"><span data-stu-id="118fe-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="118fe-143">skrypt Hello pliki do pobrania tego pliku zbyt**output.txt** w bieżącym katalogu hello na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="118fe-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="118fe-144">Witaj następujący tekst jest przykładem hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="118fe-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="118fe-145">Pierwsza kolumna Hello jest hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="118fe-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="118fe-146">Witaj wartości zawartych w "[" i "]" są `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="118fe-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="118fe-147">skrypt Hello spowoduje pobranie hello `moviedb.txt` i `user-ratings.txt` pliki, które są potrzebne tooformat hello dane wyjściowe toobe bardziej czytelne.</span><span class="sxs-lookup"><span data-stu-id="118fe-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="118fe-148">Dane wyjściowe hello widoku</span><span class="sxs-lookup"><span data-stu-id="118fe-148">View hello output</span></span>

<span data-ttu-id="118fe-149">Chociaż hello wygenerowanych danych wyjściowych może być OK do użycia w aplikacji, nie jest przyjazną dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="118fe-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="118fe-150">Witaj `moviedb.txt` z hello serwer może być używane tooresolve hello `movieId` tooa filmu nazwy.</span><span class="sxs-lookup"><span data-stu-id="118fe-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="118fe-151">Użyj hello następujące zalecenia toodisplay skrypt programu PowerShell z nazwami film:</span><span class="sxs-lookup"><span data-stu-id="118fe-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="118fe-152">Witaj Użyj następującego polecenia toodisplay hello zalecenia w formacie przyjazną dla użytkownika:</span><span class="sxs-lookup"><span data-stu-id="118fe-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="118fe-153">Witaj danych wyjściowych jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="118fe-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
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
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="118fe-154"><a name="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="118fe-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="118fe-155">Nie można zastąpić pliki</span><span class="sxs-lookup"><span data-stu-id="118fe-155">Cannot overwrite files</span></span>

<span data-ttu-id="118fe-156">Wykonaj zadania mahout nie oczyszczania plików tymczasowych, które zostały utworzone podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="118fe-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="118fe-157">Ponadto zadania hello nie zastępuj istniejącego pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="118fe-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="118fe-158">tooavoid błędy po uruchomieniu zadania Mahout, Usuń pliki tymczasowe i dane wyjściowe między działa.</span><span class="sxs-lookup"><span data-stu-id="118fe-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="118fe-159">tooremove hello plików utworzonych przez hello skrypty wcześniej w tym dokumencie za pomocą hello następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="118fe-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="118fe-160"><a name="nopowershell"></a>Klasy, które nie są obsługiwane przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="118fe-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="118fe-161">Zadania mahout, używane przez następujące klasy hello zwracać różne komunikaty o błędach w przypadku używania z programu Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="118fe-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="118fe-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="118fe-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="118fe-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="118fe-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="118fe-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="118fe-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="118fe-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="118fe-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="118fe-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="118fe-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="118fe-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="118fe-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="118fe-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="118fe-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="118fe-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="118fe-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="118fe-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="118fe-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="118fe-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="118fe-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="118fe-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="118fe-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="118fe-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="118fe-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="118fe-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="118fe-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="118fe-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="118fe-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="118fe-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="118fe-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="118fe-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="118fe-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="118fe-178">zadania toorun, korzystających z tych klas, Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH i uruchamianie zadań hello z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="118fe-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="118fe-179">Na przykład przy użyciu protokołu SSH toorun Mahout zadań, zobacz [Generowanie zaleceń filmu przy użyciu Mahout i HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="118fe-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="118fe-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="118fe-180">Next steps</span></span>

<span data-ttu-id="118fe-181">Teraz, kiedy znasz już jak toouse Mahout, odnajdywanie inne sposoby pracy z danymi w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="118fe-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="118fe-182">Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="118fe-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="118fe-183">Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="118fe-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="118fe-184">MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="118fe-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
