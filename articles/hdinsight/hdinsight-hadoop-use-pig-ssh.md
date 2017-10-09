---
title: "aaaUse Hadoop Pig przy użyciu protokołu SSH w klastrze usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć tooa opartych na systemie Linux klastra usługi Hadoop przy użyciu protokołu SSH, a następnie hello Pig polecenia toorun Pig Latin instrukcji interakcyjnego lub jako partii zadań."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Uruchamianie zadań Pig na opartych na systemie Linux klaster o hello polecenia Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Dowiedz się, jak toointeractively uruchamiania zadań Pig z klastra usługi HDInsight tooyour połączenia SSH. Witaj język programowania Pig Latin umożliwia toodescribe transformacje, których są stosowane toohello wejściowych danych tooproduce hello potrzebne w danych wyjściowych.

> [!IMPORTANT]
> Witaj czynności w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a id="ssh"></a>Połącz przy użyciu protokołu SSH

Użyj klastra usługi HDInsight tooyour tooconnect SSH. Witaj poniższy przykład łączy tooa klastra o nazwie **myhdinsight** jako hello konta o nazwie **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Jeśli podano klucz certyfikatu dla uwierzytelniania SSH** podczas tworzenia klastra usługi HDInsight hello może być konieczne lokalizacji hello toospecify hello klucza prywatnego na komputerze klienckim.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Jeśli podano hasło dla uwierzytelniania SSH** podczas tworzenia klastra usługi HDInsight hello hello hasło po wyświetleniu monitu podaj.

Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Użyj polecenia Pig hello

1. Po nawiązaniu połączenia, należy uruchomić hello Pig wiersza polecenia (CLI) przy użyciu hello następujące polecenie:

        pig

    Po chwili powinna zostać wyświetlona `grunt>` wiersza.

2. Wprowadź hello następującej instrukcji:

        LOGS = LOAD '/example/data/sample.log';

    To polecenie ładuje hello zawartość pliku sample.log hello w dzienniku. Witaj zawartość pliku hello można wyświetlić przy użyciu hello następującej instrukcji:

        DUMP LOGS;

3. Następnie przekształcania danych hello stosując poziom tooextract tylko hello rejestrowania wyrażenia regularnego z każdego rekordu przy użyciu hello następującej instrukcji:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Można użyć **zrzutu** tooview hello danych po przekształceniu hello. W takim przypadku należy użyć `DUMP LEVELS;`.

4. Kontynuować stosowanie przekształceń za pomocą instrukcji hello w hello w poniższej tabeli:

    | Pig Latin — instrukcja | Jakie instrukcji hello jest |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Usuwa wiersze, które zawierają wartość null dla poziomu dziennika hello i przechowuje wyniki hello do `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Hello grup wierszy przez poziom dziennika i przechowuje wyniki hello do `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Tworzy zestaw danych zawierający każdego dziennika unikatową wartość poziomu i ile razy występuje. zestaw danych Hello jest przechowywany w `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Porządkuje poziomy dziennika hello według liczby (malejąco) i są przechowywane w `RESULT`. |

    > [!TIP]
    > Użyj `DUMP` tooview hello wynik transformacji powitania po każdym kroku.

5. Można także zapisać wyniki hello przekształcania za pomocą hello `STORE` instrukcji. Na przykład po instrukcji hello zapisuje hello `RESULT` toohello `/example/data/pigout` katalogu na powitania domyślny magazyn dla klastra:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > Hello dane są przechowywane w katalogu określonym hello w plikach o nazwie `part-nnnnn`. Jeśli hello katalog już istnieje, zostanie wyświetlony błąd.

6. Witaj tooexit o tej grunt monit, wprowadź hello następującej instrukcji:

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin pliki wsadowe

Umożliwia także hello Pig polecenia toorun Pig Latin zawarte w pliku.

1. Po zakończeniu hello grunt wiersza, użyj hello następujące polecenie toopipe STDIN do pliku o nazwie `pigbatch.pig`. Ten plik jest tworzony w katalogu macierzystym hello hello konta użytkownika SSH.

        cat > ~/pigbatch.pig

2. Wpisz lub Wklej hello następujące wiersze, a następnie użyj klawiszy Ctrl + D po zakończeniu.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Użyj hello następujące polecenie toorun hello `pigbatch.pig` pliku za pomocą polecenia Pig hello.

        pig ~/pigbatch.pig

    Po zakończeniu zadania wsadowego hello, zapoznaj się hello następujące dane wyjściowe:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Następne kroki

Ogólne informacje na temat Pig w usłudze HDInsight zobacz następujące dokumentu hello:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)

Aby uzyskać więcej informacji na inne sposoby toowork z platformą Hadoop w usłudze HDInsight Zobacz hello w następujących dokumentach:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)
