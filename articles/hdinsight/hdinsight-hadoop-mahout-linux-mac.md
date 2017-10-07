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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Generowanie zaleceń filmu przy użyciu Apache Mahout z opartą na systemie Linux platformą Hadoop w HDInsight (SSH)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Dowiedz się, jak toouse hello [Apache Mahout](http://mahout.apache.org) maszyny biblioteki uczenie na podstawie zaleceń filmu toogenerate Azure HDInsight.

Mahout jest [uczenia maszynowego] [ ml] biblioteki dla platformy Apache Hadoop. Mahout zawiera algorytmy przetwarzania danych, takich jak filtrowanie, klasyfikacji i klastrowania. W tym artykule używamy zaleceń filmu toogenerate aparat zalecenie, oparte na filmów, które miały Twoich znajomych.

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster usługi HDInsight opartej na systemie Linux. Informacje o tworzeniu jedną, zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight][getstarted].

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Klient SSH. Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

## <a name="mahout-versioning"></a>Przechowywanie wersji mahout

Aby uzyskać więcej informacji o wersji hello Mahout w usłudze HDInsight, zobacz [HDInsight wersje i składniki platformy Hadoop](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Opis zalecenia

Jedną z hello funkcje, które są udostępniane przez Mahout jest aparatem zalecenie. Ten aparat akceptuje dane w formacie hello `userID`, `itemId`, i `prefValue` (hello preferencji hello elementu). Mahout można wykonywać wystąpienia wspólnej analizy toodetermine: *użytkowników, którzy mają preferencji elementu również mieć preferencji tych innych elementów*. Mahout określa użytkownikom preferencje podobnych elementów, które mogą być używane toomake zalecenia.

Witaj poniższy przepływ pracy jest uproszczony przykład korzystający z danych film:

* **Wystąpienia wspólnej**: Jan, Alicja i Robert wszystkie zbędne *słów*, *Witaj ponownie ataki Empire*, i *powrotu hello Jedi*. Mahout Określa, że użytkownicy, którzy jak jeden z tych filmy również, takich jak hello pozostałe dwa.

* **Wystąpienia wspólnej**: Robert i Alicja również zbędne *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*. Mahout Określa, że użytkownicy, którzy także zbędne hello poprzednie trzy filmów, takich jak te trzy filmów.

* **Zalecenie podobieństwa**: ponieważ Jan zbędne hello pierwsze trzy filmów, Mahout analizuje filmy tej osoby z podobne preferencje zbędne, ale Jan nie ma obserwowane (zbędne/klasyfikowane). W takim przypadku zaleca Mahout *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*.

### <a name="understanding-hello-data"></a>Opis hello danych

Wygodnie [GroupLens Research] [ movielens] zapewnia filmów w formacie, który jest zgodny z Mahout klasyfikacji danych. Te dane są dostępne w magazynie domyślne klastra na `/HdiSamples/HdiSamples/MahoutMovieData`.

Istnieją dwa pliki `moviedb.txt` i `user-ratings.txt`. Plik ratings.txt użytkownika Hello jest używany podczas analizy, podczas moviedb.txt informacje tekstowe przyjazną dla użytkownika tooprovide używane przy wyświetlaniu wyników hello hello analizy.

Witaj dane zawarte w ratings.txt użytkownika ma struktury `userID`, `movieID`, `userRating`, i `timestamp`, który informuje NAS jak bardzo każdego użytkownika oceną filmu. Oto przykład hello danych:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Uruchom analizę hello

Z klastra toohello połączenia SSH należy użyć hello następujące polecenia toorun hello zalecenie zadania:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> zadanie Hello może potrwać kilka minut toocomplete i może działać wiele zadań MapReduce.

## <a name="view-hello-output"></a>Dane wyjściowe hello widoku

1. Po zakończeniu zadania hello hello Użyj następującego polecenia tooview hello wygenerowanych danych wyjściowych:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    dane wyjściowe Hello wygląda następująco:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    Pierwsza kolumna Hello jest hello `userID`. Witaj wartości zawartych w "[" i "]" są `movieId`:`recommendationScore`.

2. Więcej informacji można użyć hello dane wyjściowe, wraz z hello moviedb.txt, tooprovide na powitania zalecenia. Najpierw należy toocopy hello plików lokalnie za pomocą następującego polecenia hello:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    To polecenie kopie hello o nazwie pliku tooa danych wyjściowych **recommendations.txt** w bieżącym katalogu hello wraz z hello filmu danych plików.

3. Użyj następującego polecenia toocreate skrypt w języku Python, które wyszukuje nazwy filmu danych hello w danych wyjściowych zalecenia hello hello:

    ```bash
    nano show_recommendations.py
    ```

    Po otwarciu edytora hello, użyj następującego tekstu jako hello zawartość pliku hello hello:

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

    Naciśnij klawisz **Ctrl-X**, **Y**, a na końcu **Enter** toosave hello danych.

4. Uruchom skrypt w języku Python hello. Witaj następującego polecenia przyjęto założenie, że znajdują się w katalogu hello, gdzie zostały pobrane wszystkie pliki hello:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    To polecenie analizuje zalecenia hello wygenerowany dla użytkownika 4 identyfikator.

    * Witaj **ratings.txt użytkownika** plik jest używane tooretrieve filmów, które zostały sklasyfikowane.

    * Witaj **moviedb.txt** tooretrieve używane hello nazw filmów hello jest plik.

    * Witaj **recommendations.txt** jest używane tooretrieve hello zaleceń filmu dla tego użytkownika.

     Witaj danych wyjściowych tego polecenia jest podobne toohello następującego tekstu:

        7 lat w Tibet (1997), wynik = 5.0 Kowalski Indiana i hello ostatniego Crusade (1989), wynik = 5.0 Jaws (1975), wynik = 5.0 znaczeniu i świadomości (1995), wynik = 5.0 niezależność dzień (ID4) (1996), wynik = 5.0 Moje najlepszy przyjaciel ślubu (1997), wynik = 5.0 Jerry Maguire (1996 ), wynik = 5.0 Scream 2 (1997), wynik = 5.0 tooKill czasu, (1996), wynik = 5.0

## <a name="delete-temporary-data"></a>Usuń dane tymczasowe

Mahout zadania nie należy usuwać dane tymczasowe, który jest tworzony podczas przetwarzania zadania hello. Witaj `--tempDir` określony parametr w hello przykładowe zadania tooisolate hello tymczasowych plików do określonej ścieżki do łatwego usunięcia. pliki tymczasowe hello tooremove, użyj hello następujące polecenie:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Jeśli chcesz ponownie polecenie hello toorun, zostaną również usunięte hello katalogu wyjściowego. Użyj następującego toodelete hello tego katalogu:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już jak toouse Mahout, odnajdywanie inne sposoby pracy z danymi w usłudze HDInsight:

* [Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Pig z usługą HDInsight](hdinsight-use-pig.md)
* [MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

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
