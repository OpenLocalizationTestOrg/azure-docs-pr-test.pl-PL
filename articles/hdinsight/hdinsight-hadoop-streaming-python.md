---
title: "aaaDevelop Python przesyłania strumieniowego MapReduce zadania z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Python w strumieniowym zadań MapReduce. Hadoop udostępnia interfejs API przesyłania strumieniowego dla MapReduce do pisania w językach innych niż Java."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Opracowywanie Python przesyłania strumieniowego programy MapReduce dla usługi HDInsight

Dowiedz się, jak toouse Python w strumieniowym działania MapReduce. Hadoop udostępnia interfejs API przesyłania strumieniowego dla MapReduce, Zmniejsz funkcje w językach innych niż Java i możliwość toowrite mapy. Witaj kroki opisane w tym dokumencie hello mapy implementacji i zmniejszyć składników w języku Python.

## <a name="prerequisites"></a>Wymagania wstępne

* Opartych na systemie Linux platformą Hadoop w klastrze usługi HDInsight

  > [!IMPORTANT]
  > kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Edytor tekstu

  > [!IMPORTANT]
  > Edytor tekstu Hello musi używać LF co hello zakończenia linii. Przy użyciu wiersza koniec CRLF powoduje, że błędy podczas uruchamiania zadania MapReduce hello w klastrach HDInsight opartych na systemie Linux.

* Witaj `ssh` i `scp` polecenia, lub [programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Liczba programu Word

W tym przykładzie jest podstawowe wyrazów zaimplementowana w języku python mapowania i reduktor. mapowania Hello dzieli zdania na poszczególnych wyrazów, a reduktor hello agreguje hello słów i liczby tooproduce hello w danych wyjściowych.

powitania po schemat blokowy przedstawia co się działo podczas mapy hello i ograniczyć faz.

![Ilustracja hello mapreduce procesu](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>MapReduce przesyłania strumieniowego

Hadoop umożliwia toospecify pliku, który zawiera mapy hello i zmniejszyć logikę, która jest używana przez zadanie. Hello określonych wymagań dotyczących hello mapowania i zmniejszyć logiki są:

* **Wejściowy**: hello mapy co pozwala zmniejszyć liczbę składników należy odczytać dane wejściowe z STDIN.
* **Dane wyjściowe**: hello mapy co pozwala zmniejszyć liczbę składników musi być zapisana tooSTDOUT danych wyjściowych.
* **Format danych**: hello danych używane i wyprodukowanych musi być parę klucza i wartości, rozdzielając znak tabulacji.

Python może z łatwością obsłużyć te wymagania przy użyciu hello `sys` tooread modułu z STDIN z zastosowaniem `print` tooprint tooSTDOUT. Witaj pozostałych zadań jest po prostu formatowania danych hello za pomocą karty (`\t`) znak między hello klucz i wartość.

## <a name="create-hello-mapper-and-reducer"></a>Utwórz mapowania hello i reduktor

1. Utwórz plik o nazwie `mapper.py` i hello Użyj następującego kodu jako zawartość hello:

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. Utwórz plik o nazwie **reducer.py** i hello Użyj następującego kodu jako zawartość hello:

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a>Uruchamianie przy użyciu programu PowerShell

tooensure że pliki mają zakończenia wierszy prawo hello, hello Użyj następującego skryptu programu PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Użyj hello następujące pliki hello tooupload skrypt programu PowerShell, uruchom zadanie hello i wyświetlić dane wyjściowe hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Uruchom w sesji SSH

1. Ze środowiska deweloperskiego w hello sam katalogu jako `mapper.py` i `reducer.py` plików, użyj następującego polecenia hello:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Zastąp `username` z nazwą użytkownika SSH powitania dla klastra, i `clustername` o nazwie hello klastra.

    To polecenie kopiuje pliki hello z węzłem głównym toohello hello systemu lokalnego.

    > [!NOTE]
    > Jeśli używasz toosecure hasło konta SSH, zostanie wyświetlony monit o hasło hello. Jeśli używasz klucza SSH, może być toouse hello `-i` parametr i hello ścieżki toohello klucza prywatnego. Na przykład `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Połącz toohello klastra przy użyciu protokołu SSH:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Aby uzyskać więcej informacji o zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. tooensure hello mapper.py i reducer.py mają hello Popraw zakończenia wierszy, użyj następującego polecenia hello:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Użyj hello następujące zadania MapReduce hello toostart polecenia.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    To polecenie ma hello następujące elementy:

   * **hadoop streaming.jar**: używane podczas wykonywania operacji MapReduce przesyłania strumieniowego. Hadoop go interfejsów z hello MapReduce kod zewnętrzny podane przez użytkownika.

   * **— pliki**: dodaje określony hello zadania MapReduce toohello plików.

   * **-mapowania**: Określa, że Hadoop, która plików toouse hello mapowania.

   * **-Reduktor**: Określa, że Hadoop, która plików toouse hello reduktor.

   * **-wejściowych**: hello pliku wejściowego możemy należy policzyć wyrazów z.

   * **-dane wyjściowe**: hello katalogu, w którym hello dane wyjściowe są zapisywane.

    Jak działa hello zadania MapReduce, proces hello jest wyświetlana jako wartości procentowe.

        05-15-02 19:01:04 informacji o mapreduce. Zadanie: 0% zmniejszyć mapy 0% 05-15-02 19:01:16 informacji o mapreduce. Zadanie: 0% zmniejszyć mapy 100% 05-15-02 19:01:27 informacji o mapreduce. Zadania: 100% zmniejszyć mapy 100%


5. dane wyjściowe hello tooview, hello Użyj następującego polecenia:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    To polecenie wyświetla listę słów i ile razy program word hello wystąpił.

## <a name="next-steps"></a>Następne kroki

Teraz wiesz już, jak zadania przesyłania strumieniowego MapRedcue toouse z usługą HDInsight, za pomocą następującego łącza tooexplore hello toowork inne sposoby z usługą Azure HDInsight.

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystanie z zadań MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)
