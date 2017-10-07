---
title: "zalecenia aaaGenerate przy użyciu Mahout i HDInsight (SSH) - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Apache Mahout machine learning zaleceń filmu toogenerate biblioteki z usługą HDInsight (Hadoop)."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="5eaaa-103">Generowanie zaleceń filmu przy użyciu Apache Mahout z opartą na systemie Linux platformą Hadoop w HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="5eaaa-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="5eaaa-104">Dowiedz się, jak toouse hello [Apache Mahout](http://mahout.apache.org) maszyny biblioteki uczenie na podstawie zaleceń filmu toogenerate Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="5eaaa-105">Mahout jest [uczenia maszynowego] [ ml] biblioteki dla platformy Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="5eaaa-106">Mahout zawiera algorytmy przetwarzania danych, takich jak filtrowanie, klasyfikacji i klastrowania.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="5eaaa-107">W tym artykule używamy zaleceń filmu toogenerate aparat zalecenie, oparte na filmów, które miały Twoich znajomych.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eaaa-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5eaaa-108">Prerequisites</span></span>

* <span data-ttu-id="5eaaa-109">Klaster usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5eaaa-110">Informacje o tworzeniu jedną, zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="5eaaa-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5eaaa-111">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5eaaa-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5eaaa-113">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-113">An SSH client.</span></span> <span data-ttu-id="5eaaa-114">Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="5eaaa-115">Przechowywanie wersji mahout</span><span class="sxs-lookup"><span data-stu-id="5eaaa-115">Mahout versioning</span></span>

<span data-ttu-id="5eaaa-116">Aby uzyskać więcej informacji o wersji hello Mahout w usłudze HDInsight, zobacz [HDInsight wersje i składniki platformy Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="5eaaa-117"><a name="recommendations"></a>Opis zalecenia</span><span class="sxs-lookup"><span data-stu-id="5eaaa-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="5eaaa-118">Jedną z hello funkcje, które są udostępniane przez Mahout jest aparatem zalecenie.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="5eaaa-119">Ten aparat akceptuje dane w formacie hello `userID`, `itemId`, i `prefValue` (hello preferencji hello elementu).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="5eaaa-120">Mahout można wykonywać wystąpienia wspólnej analizy toodetermine: *użytkowników, którzy mają preferencji elementu również mieć preferencji tych innych elementów*.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="5eaaa-121">Mahout określa użytkownikom preferencje podobnych elementów, które mogą być używane toomake zalecenia.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="5eaaa-122">Witaj poniższy przepływ pracy jest uproszczony przykład korzystający z danych film:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="5eaaa-123">**Wystąpienia wspólnej**: Jan, Alicja i Robert wszystkie zbędne *słów*, *Witaj ponownie ataki Empire*, i *powrotu hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="5eaaa-124">Mahout Określa, że użytkownicy, którzy jak jeden z tych filmy również, takich jak hello pozostałe dwa.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="5eaaa-125">**Wystąpienia wspólnej**: Robert i Alicja również zbędne *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="5eaaa-126">Mahout Określa, że użytkownicy, którzy także zbędne hello poprzednie trzy filmów, takich jak te trzy filmów.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="5eaaa-127">**Zalecenie podobieństwa**: ponieważ Jan zbędne hello pierwsze trzy filmów, Mahout analizuje filmy tej osoby z podobne preferencje zbędne, ale Jan nie ma obserwowane (zbędne/klasyfikowane).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="5eaaa-128">W takim przypadku zaleca Mahout *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="5eaaa-129">Opis hello danych</span><span class="sxs-lookup"><span data-stu-id="5eaaa-129">Understanding hello data</span></span>

<span data-ttu-id="5eaaa-130">Wygodnie [GroupLens Research] [ movielens] zapewnia filmów w formacie, który jest zgodny z Mahout klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="5eaaa-131">Te dane są dostępne w magazynie domyślne klastra na `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="5eaaa-132">Istnieją dwa pliki `moviedb.txt` i `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="5eaaa-133">Plik ratings.txt użytkownika Hello jest używany podczas analizy, podczas moviedb.txt informacje tekstowe przyjazną dla użytkownika tooprovide używane przy wyświetlaniu wyników hello hello analizy.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="5eaaa-134">Witaj dane zawarte w ratings.txt użytkownika ma struktury `userID`, `movieID`, `userRating`, i `timestamp`, który informuje NAS jak bardzo każdego użytkownika oceną filmu.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="5eaaa-135">Oto przykład hello danych:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="5eaaa-136">Uruchom analizę hello</span><span class="sxs-lookup"><span data-stu-id="5eaaa-136">Run hello analysis</span></span>

<span data-ttu-id="5eaaa-137">Z klastra toohello połączenia SSH należy użyć hello następujące polecenia toorun hello zalecenie zadania:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="5eaaa-138">zadanie Hello może potrwać kilka minut toocomplete i może działać wiele zadań MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="5eaaa-139">Dane wyjściowe hello widoku</span><span class="sxs-lookup"><span data-stu-id="5eaaa-139">View hello output</span></span>

1. <span data-ttu-id="5eaaa-140">Po zakończeniu zadania hello hello Użyj następującego polecenia tooview hello wygenerowanych danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="5eaaa-141">dane wyjściowe Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="5eaaa-142">Pierwsza kolumna Hello jest hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="5eaaa-143">Witaj wartości zawartych w "[" i "]" są `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="5eaaa-144">Więcej informacji można użyć hello dane wyjściowe, wraz z hello moviedb.txt, tooprovide na powitania zalecenia.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="5eaaa-145">Najpierw należy toocopy hello plików lokalnie za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="5eaaa-146">To polecenie kopie hello o nazwie pliku tooa danych wyjściowych **recommendations.txt** w bieżącym katalogu hello wraz z hello filmu danych plików.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="5eaaa-147">Użyj następującego polecenia toocreate skrypt w języku Python, które wyszukuje nazwy filmu danych hello w danych wyjściowych zalecenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="5eaaa-148">Po otwarciu edytora hello, użyj następującego tekstu jako hello zawartość pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="5eaaa-149">Naciśnij klawisz **Ctrl-X**, **Y**, a na końcu **Enter** toosave hello danych.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="5eaaa-150">Uruchom skrypt w języku Python hello.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-150">Run hello Python script.</span></span> <span data-ttu-id="5eaaa-151">Witaj następującego polecenia przyjęto założenie, że znajdują się w katalogu hello, gdzie zostały pobrane wszystkie pliki hello:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="5eaaa-152">To polecenie analizuje zalecenia hello wygenerowany dla użytkownika 4 identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="5eaaa-153">Witaj **ratings.txt użytkownika** plik jest używane tooretrieve filmów, które zostały sklasyfikowane.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="5eaaa-154">Witaj **moviedb.txt** tooretrieve używane hello nazw filmów hello jest plik.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="5eaaa-155">Witaj **recommendations.txt** jest używane tooretrieve hello zaleceń filmu dla tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="5eaaa-156">Witaj danych wyjściowych tego polecenia jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="5eaaa-157">7 lat w Tibet (1997), wynik = 5.0 Kowalski Indiana i hello ostatniego Crusade (1989), wynik = 5.0 Jaws (1975), wynik = 5.0 znaczeniu i świadomości (1995), wynik = 5.0 niezależność dzień (ID4) (1996), wynik = 5.0 Moje najlepszy przyjaciel ślubu (1997), wynik = 5.0 Jerry Maguire (1996 ), wynik = 5.0 Scream 2 (1997), wynik = 5.0 tooKill czasu, (1996), wynik = 5.0</span><span class="sxs-lookup"><span data-stu-id="5eaaa-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="5eaaa-158">Usuń dane tymczasowe</span><span class="sxs-lookup"><span data-stu-id="5eaaa-158">Delete temporary data</span></span>

<span data-ttu-id="5eaaa-159">Mahout zadania nie należy usuwać dane tymczasowe, który jest tworzony podczas przetwarzania zadania hello.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="5eaaa-160">Witaj `--tempDir` określony parametr w hello przykładowe zadania tooisolate hello tymczasowych plików do określonej ścieżki do łatwego usunięcia.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="5eaaa-161">pliki tymczasowe hello tooremove, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="5eaaa-162">Jeśli chcesz ponownie polecenie hello toorun, zostaną również usunięte hello katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="5eaaa-163">Użyj następującego toodelete hello tego katalogu:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="5eaaa-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5eaaa-164">Next steps</span></span>

<span data-ttu-id="5eaaa-165">Teraz, kiedy znasz już jak toouse Mahout, odnajdywanie inne sposoby pracy z danymi w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5eaaa-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="5eaaa-166">Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="5eaaa-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5eaaa-167">Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="5eaaa-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5eaaa-168">MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="5eaaa-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
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
