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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Generowanie zaleceń filmu przy użyciu Apache Mahout Hadoop w usłudze HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Dowiedz się, jak toouse hello [Apache Mahout](http://mahout.apache.org) maszyny biblioteki uczenie na podstawie zaleceń filmu toogenerate Azure HDInsight. przykład Witaj w tym dokumencie korzysta z programu Azure PowerShell toorun Mahout zadania.

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster usługi HDInsight opartej na systemie Linux. Informacje o tworzeniu jedną, zobacz [Rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight][getstarted].

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Generowanie zaleceń przy użyciu programu Azure PowerShell

> [!WARNING]
> zadanie Hello w tej sekcji działa przy użyciu programu Azure PowerShell. Wiele klas hello wyposażone Mahout obecnie nie współpracujesz z programem Azure PowerShell. Lista klas, które nie są obsługiwane przy użyciu programu Azure PowerShell, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji.
>
> Na przykład za pomocą SSH tooconnect tooHDInsight i uruchamiania przykładów Mahout bezpośrednio w klastrze hello, zobacz [Generowanie zaleceń filmu przy użyciu Mahout i HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Jedną z hello funkcje, które są udostępniane przez Mahout jest aparatem zalecenie. Ten aparat akceptuje dane w formacie hello `userID`, `itemId`, i `prefValue` (hello preferencji Użytkownicy hello elementu). Mahout używa hello danych toodetermine użytkowników o podobnych elementów preferencji, które mogą być używane toomake zalecenia.

Witaj poniższy przykład jest uproszczone przewodnika działania procesu zalecenie hello:

* **wystąpienie wspólnej**: Jan, Alicja i Robert wszystkie zbędne *słów*, *Witaj ponownie ataki Empire*, i *powrotu hello Jedi*. Mahout Określa, że użytkownicy, którzy jak jeden z tych filmy również, takich jak hello pozostałe dwa.

* **wystąpienie wspólnej**: Robert i Alicja również zbędne *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*. Mahout Określa, że użytkownicy, którzy także zbędne hello poprzednie trzy filmów, takich jak te filmów.

* **Zalecenie podobieństwa**: ponieważ Jan zbędne hello pierwsze trzy filmów, Mahout analizuje filmy tej osoby z podobne preferencje zbędne, ale Jan nie ma obserwowane (zbędne/klasyfikowane). W takim przypadku zaleca Mahout *hello zagrożenie fantom*, *atak powitania klony*, i *zemsty hello Sith*.

### <a name="understanding-hello-data"></a>Opis hello danych

[Badania GroupLens] [ movielens] zapewnia filmów w formacie, który jest zgodny z Mahout klasyfikacji danych. Dane te są dostępne na powitania domyślny magazyn dla klastra w `/HdiSamples//HdiSamples/MahoutMovieData`.

Istnieją dwa pliki `moviedb.txt` (informacje na temat filmów hello) i `user-ratings.txt`. Witaj `user-ratings.txt` plik jest używany podczas analizy. Witaj `moviedb.txt` pliku jest wartością tekstową przyjazną dla użytkownika tooprovide używane przy wyświetlaniu wyników hello hello analizy.

Witaj dane zawarte w ratings.txt użytkownika ma struktury `userID`, `movieID`, `userRating`, i `timestamp`, który informuje NAS jak bardzo każdego użytkownika oceną filmu. Oto przykład hello danych:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Uruchom zadanie hello

Użyj powitania po toorun skrypt programu Windows PowerShell zadanie, które używa aparatu zalecenie Mahout hello z danymi filmu hello:

> [!NOTE]
> Ten plik wyświetla monit o podanie informacji o klastra usługi HDInsight używane tooconnect tooyour i wykonywania zadań. Może potrwać kilka minut hello toocomplete zadania i Pobierz plik output.txt hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Mahout zadania nie należy usuwać dane tymczasowe, który jest tworzony podczas przetwarzania zadania hello. Witaj `--tempDir` określony parametr w hello przykładowe zadania tooisolate hello tymczasowe pliki w określonym katalogu.

zadanie Mahout Hello nie zwraca hello tooSTDOUT danych wyjściowych. Zamiast tego, przechowuje go w katalogu określonym produktem wyjściowym hello co **części r-00000**. skrypt Hello pliki do pobrania tego pliku zbyt**output.txt** w bieżącym katalogu hello na stacji roboczej.

Witaj następujący tekst jest przykładem hello zawartość tego pliku:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

Pierwsza kolumna Hello jest hello `userID`. Witaj wartości zawartych w "[" i "]" są `movieId`:`recommendationScore`.

skrypt Hello spowoduje pobranie hello `moviedb.txt` i `user-ratings.txt` pliki, które są potrzebne tooformat hello dane wyjściowe toobe bardziej czytelne.

### <a name="view-hello-output"></a>Dane wyjściowe hello widoku

Chociaż hello wygenerowanych danych wyjściowych może być OK do użycia w aplikacji, nie jest przyjazną dla użytkownika. Witaj `moviedb.txt` z hello serwer może być używane tooresolve hello `movieId` tooa filmu nazwy. Użyj hello następujące zalecenia toodisplay skrypt programu PowerShell z nazwami film:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Witaj Użyj następującego polecenia toodisplay hello zalecenia w formacie przyjazną dla użytkownika: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Witaj danych wyjściowych jest podobne toohello następującego tekstu:

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

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="cannot-overwrite-files"></a>Nie można zastąpić pliki

Wykonaj zadania mahout nie oczyszczania plików tymczasowych, które zostały utworzone podczas przetwarzania. Ponadto zadania hello nie zastępuj istniejącego pliku wyjściowego.

tooavoid błędy po uruchomieniu zadania Mahout, Usuń pliki tymczasowe i dane wyjściowe między działa. tooremove hello plików utworzonych przez hello skrypty wcześniej w tym dokumencie za pomocą hello następującego skryptu programu PowerShell:

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

### <a name="nopowershell"></a>Klasy, które nie są obsługiwane przy użyciu programu Azure PowerShell

Zadania mahout, używane przez następujące klasy hello zwracać różne komunikaty o błędach w przypadku używania z programu Windows PowerShell:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

zadania toorun, korzystających z tych klas, Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH i uruchamianie zadań hello z wiersza polecenia hello. Na przykład przy użyciu protokołu SSH toorun Mahout zadań, zobacz [Generowanie zaleceń filmu przy użyciu Mahout i HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już jak toouse Mahout, odnajdywanie inne sposoby pracy z danymi w usłudze HDInsight:

* [Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Pig z usługą HDInsight](hdinsight-use-pig.md)
* [MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

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
