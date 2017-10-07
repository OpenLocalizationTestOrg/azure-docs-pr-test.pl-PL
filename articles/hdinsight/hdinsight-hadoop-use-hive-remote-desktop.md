---
title: "aaaUse Hadoop Hive i pulpitu zdalnego w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooHadoop klastra w usłudze HDInsight przy użyciu pulpitu zdalnego, a następnie uruchom zapytań programu Hive za pomocą hello Hive interfejsu wiersza polecenia."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

W tym artykule dowiesz się, jak tooan tooconnect HDInsight klastra przy użyciu pulpitu zdalnego, a następnie uruchom Hive zapytania przy użyciu hello Hive interfejsu wiersza polecenia (CLI).

> [!IMPORTANT]
> Pulpit zdalny jest dostępna tylko w klastrach HDInsight, które używają systemu Windows jako system operacyjny hello. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [używanie Hive z HDInsight i Beeline](hdinsight-hadoop-use-hive-beeline.md) informacji na temat uruchamiania zapytań Hive bezpośrednio w klastrze hello z wiersza polecenia.

## <a id="prereq"></a>Wymagania wstępne
toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:

* Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)
* Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7

## <a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego
Włączenie pulpitu zdalnego dla klastra usługi HDInsight hello, a następnie połącz tooit, wykonując następujące instrukcje hello [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Polecenie gałęzi hello
Po podłączeniu pulpitu toohello dla klastra usługi HDInsight hello za pomocą hello następujące kroki toowork z gałęzi:

1. Na pulpicie HDInsight hello start hello **wiersza polecenia usługi Hadoop**.
2. Wprowadź hello następujące polecenia toostart hello Hive interfejsu wiersza polecenia:

        %hive_home%\bin\hive

    Rozpoczęto hello interfejsu wiersza polecenia, można zobaczyć w wierszu Hive CLI hello: `hive>`.
3. Używając hello interfejsu wiersza polecenia, wprowadź następujące instrukcje toocreate nowej tabeli o nazwie hello **log4jLogs** przy użyciu przykładowych danych:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Instrukcje te należy wykonać hello następujące akcje:

   * **DROP TABLE**: usuwa tabeli hello i hello pliku danych, jeśli hello tabela już istnieje.
   * **Tworzenie tabeli zewnętrznej**: tworzy nową tabelę "zewnętrzne" w gałęzi. Tabele zewnętrzne przechowywać tylko definicji tabeli hello w gałęzi (powitalne pozostanie danych w oryginalnej lokalizacji hello).

     > [!NOTE]
     > Tabele zewnętrzne należy używać oczekiwać hello podstawowych aktualizowane przez źródło zewnętrzne (na przykład procesu przekazywania danych) lub przez inną operację MapReduce toobe danych, ale zawsze mają toouse hello najnowsze dane zapytania Hive.
     >
     > Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.
     >
     >
   * **FORMAT wiersza**: informuje Hive sposób formatowania danych hello. W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.
   * **PRZECHOWYWANE jako lokalizacji TEXTFILE**: informuje gałąź rejestru, których hello dane są przechowywane (katalog hello przykład/danych) i są przechowywane jako tekst.
   * **Wybierz**: wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość hello **[Błąd]**. Powinny zostać zwrócone wartości **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.
   * **INPUT__FILE__NAME takich jak "%.log"** -informuje, który mamy powinno zwrócić tylko danych z plików w gałęzi. dziennika. To ogranicza hello wyszukiwania toohello sample.log pliku, który zawiera dane hello utrzymuje je z zwracać dane z innych przykładowe pliki danych, która nie pasuje do schematu hello zdefiniowanego.
4. Użyj hello następujące instrukcje toocreate nową tabelę "internal" o nazwie **errorLogs**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Instrukcje te należy wykonać hello następujące akcje:

   * **Utwórz Tabela Jeśli nie ISTNIEJE**: tworzy tabelę, jeśli jeszcze nie istnieje. Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używany, to wewnętrznej tabeli, który jest przechowywany w magazynie danych Hive hello i zarządza całkowicie Hive.

     > [!NOTE]
     > W odróżnieniu od **zewnętrznych** tabel, również porzucenie wewnętrznej tabeli usuwa hello podstawowych danych.
     >
     >
   * **ORC AS PRZECHOWYWANE**: hello ilość danych przechowywana w zoptymalizowaną wiersza tabelarycznego (ORC). Jest to wysoce zoptymalizowane i wydajne format do przechowywania danych Hive.
   * **ZASTĄP INSERT... Wybierz**: wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie wstawia hello danych do hello **errorLogs** tabeli.

     tooverify, który tylko wiersze, które zawierają **[Błąd]** w t4 kolumnie były przechowywane toohello **errorLogs** tabeli, należy użyć powitania po instrukcji tooreturn hello wszystkie wiersze z **errorLogs**:

       Wybierz * z errorLogs;

     Trzy wiersze danych ma zostać zwrócony, zawierający wszystkie **[Błąd]** w t4 kolumny.

## <a id="summary"></a>Podsumowanie
Jak widać, hello hello polecenie gałęzi zawiera toointeractively łatwe uruchamianie zapytań Hive w klastrze usługi HDInsight, monitor hello stan zadania i pobrać dane wyjściowe hello.

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów dla informacji debugowania:

* [Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows](hdinsight-debug-tez-ui.md)
* [Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
