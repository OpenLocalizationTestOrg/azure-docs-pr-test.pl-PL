---
title: "aaaUse Hadoop Pig przy użyciu pulpitu zdalnego w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Pig toorun Pig Latin instrukcje z klastra platformy Hadoop działającej w systemie Windows tooa połączenia pulpitu zdalnego w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Uruchamianie zadań Pig połączenie pulpitu zdalnego
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Ten dokument zawiera wskazówki dotyczące korzystania z hello Pig polecenia toorun Pig Latin instrukcji z klastra usługi HDInsight opartej na systemie Windows tooa połączenia pulpitu zdalnego. Pig Latin umożliwia aplikacji MapReduce toocreate przez opisywania przekształceń danych, a nie mapy i zmniejszyć funkcji.

> [!IMPORTANT]
> Pulpit zdalny jest dostępna tylko w klastrach HDInsight, które używają systemu Windows jako system operacyjny hello. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [Use Pig HDInsight i SSH](hdinsight-hadoop-use-pig-ssh.md) informacji na temat interakcyjnego uruchamiania Pig zadania bezpośrednio na powitania klastra z wiersza polecenia.

## <a id="prereq"></a>Wymagania wstępne
toocomplete hello kroki opisane w tym artykule, należy hello poniżej.

* Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)
* Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7

## <a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego
Włączenie pulpitu zdalnego dla klastra usługi HDInsight hello, a następnie połącz tooit, wykonując następujące instrukcje hello [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Użyj polecenia Pig hello
1. Po utworzeniu połączenia pulpitu zdalnego, należy rozpocząć hello **wiersza polecenia platformy Hadoop** przy użyciu hello ikony na pulpicie hello.
2. Użyj następującego polecenia Pig hello toostart hello:

        %pig_home%\bin\pig

    Użytkownik zobaczy `grunt>` wiersza.
3. Wprowadź hello następującej instrukcji:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    To polecenie ładuje hello zawartość pliku sample.log hello do hello plików DZIENNIKÓW. Witaj zawartość pliku hello można wyświetlić przy użyciu hello następujące polecenie:

        DUMP LOGS;
4. Przekształć dane hello stosując poziom tooextract tylko hello rejestrowania wyrażenia regularnego z każdego rekordu:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Można użyć **zrzutu** tooview hello danych po przekształceniu hello. W takim przypadku `DUMP LEVELS;`.
5. Kontynuować stosowanie przekształceń przy użyciu hello następujące instrukcje. Użyj `DUMP` tooview hello wynik transformacji powitania po każdym kroku.

    <table>
    <tr>
    <th>— Instrukcja</th><th>Wyniki działania</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = poziomy filtru przez LOGLEVEL nie ma wartości null;</td><td>Usuwa wiersze, które zawierają wartość null dla poziomu dziennika hello i przechowuje wyniki hello do FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = FILTEREDLEVELS grupy przez LOGLEVEL;</td><td>Hello grup wierszy przez poziom dziennika i przechowuje wyniki hello do GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>CZĘSTOTLIWOŚCI = foreach GROUPEDLEVELS Generowanie grupy jako LOGLEVEL, COUNT (FILTEREDLEVELS. LOGLEVEL) jako liczba;</td><td>Tworzy nowy zestaw danych zawierający każdego dziennika unikatową wartość poziomu i ile razy występuje. To jest przechowywane w częstotliwości</td>
    </tr>
    <tr>
    <td>WYNIK = kolejności częstotliwości przez liczbę desc;</td><td>Porządkuje hello poziomy dziennika według liczby (malejąco) i magazyny do wyniku</td>
    </tr>
    </table>
6.Można także zapisać wyniki hello przekształcania za pomocą hello `STORE` instrukcji. Na przykład następujące polecenie hello zapisuje hello `RESULT` toohello **/example/data/pigout** katalogu w hello domyślnego kontenera magazynu dla klastra:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > Hello dane są przechowywane w katalogu określonym hello w plikach o nazwie **nnnnn części**. Jeśli istnieje już katalog hello, otrzymasz komunikat o błędzie.
   >
   >
7. Witaj tooexit o tej grunt monit, wprowadź powitania po instrukcji.

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin pliki wsadowe
Umożliwia także hello Pig polecenia toorun Pig Latin, który jest zawarty w pliku.

1. Po zakończeniu hello grunt wiersza, otwórz **Notatnik** i Utwórz nowy plik o nazwie **pigbatch.pig** w hello **PIG_HOME %** katalogu.
2. Wpisz lub Wklej hello następujące wiersze do hello **pigbatch.pig** pliku, a następnie zapisz go:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Użyj powitania po toorun hello **pigbatch.pig** pliku za pomocą polecenia pig hello.

        pig %PIG_HOME%\pigbatch.pig

    Po zakończeniu wykonywania zadania wsadowego hello powinna zostać wyświetlona hello następujące dane wyjściowe, które powinny być hello sam jako gdy używane `DUMP RESULT;` w poprzednich krokach hello:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Podsumowanie
Jak widać, hello polecenia Pig umożliwia toointeractively uruchamiania operacji MapReduce lub uruchamianie zadań Pig Latin, które są przechowywane w pliku wsadowym.

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)
