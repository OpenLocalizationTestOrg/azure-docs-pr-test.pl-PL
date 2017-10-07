---
title: "aaaUse Hadoop Hive na powitania konsoli zapytania w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello opartych na sieci web konsoli zapytania toorun zapytań programu Hive w usłudze HDInsight Hadoop klastra z przeglądarki."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Uruchamianie zapytań Hive przy użyciu hello konsoli zapytania
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

W tym artykule dowiesz się, jak toouse hello konsoli zapytania HDInsight toorun zapytań programu Hive w usłudze HDInsight Hadoop klastra z przeglądarki.

> [!IMPORTANT]
> Witaj HDInsight zapytania konsoli jest dostępna tylko w klastrach HDInsight opartych na systemie Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [uruchamianie zapytań Hive w widoku Hive narzędzia Ambari](hdinsight-hadoop-use-hive-ambari-view.md) informacji na temat uruchamiania zapytań Hive z przeglądarki sieci web.

## <a id="prereq"></a>Wymagania wstępne
toocomplete hello kroki opisane w tym artykule, należy hello poniżej.

* Klastra z systemem Windows usługi HDInsight Hadoop
* Nowoczesna przeglądarka sieci web

## <a id="run"></a>Uruchamianie zapytań Hive przy użyciu hello konsoli zapytania
1. Otwórz przeglądarkę sieci web i przejdź zbyt**https://CLUSTERNAME.azurehdinsight.net**, gdzie **CLUSTERNAME** jest nazwą hello klastra usługi HDInsight. Jeśli zostanie wyświetlony monit, wprowadź hello nazwę użytkownika i hasło użyte podczas tworzenia klastra hello.
2. Łącza hello u góry strony hello hello, zaznacz **Edytor Hive**. Spowoduje to wyświetlenie formularza, który może być instrukcje HiveQL hello używane tooenter, które mają toorun hello klastra usługi HDInsight.

    ![Edytor hive Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Zastąp tekst hello `Select * from hivesampletable` z hello następujące instrukcje HiveQL:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Instrukcje te należy wykonać hello następujące akcje:

   * **DROP TABLE**: usuwa tabeli hello i hello pliku danych, jeśli hello tabela już istnieje.
   * **Tworzenie tabeli zewnętrznej**: tworzy nową tabelę "zewnętrzne" w gałęzi. Tylko definicji tabeli hello są przechowywane w tabelach zewnętrznych w gałęzi; Hello danych pozostaje w hello oryginalnej lokalizacji.

     > [!NOTE]
     > Tabele zewnętrzne należy używać oczekiwać hello podstawowych aktualizowane przez źródło zewnętrzne (na przykład procesu przekazywania danych) lub przez inną operację MapReduce toobe danych, ale zawsze mają toouse hello najnowsze dane zapytania Hive.
     >
     > Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.
     >
     >
   * **FORMAT wiersza**: informuje Hive sposób formatowania danych hello. W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.
   * **PRZECHOWYWANE jako lokalizacji TEXTFILE**: informuje gałąź rejestru, których hello dane są przechowywane (katalog hello przykład/danych) i są przechowywane jako tekst
   * **Wybierz**: Wybierz liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartości hello **[Błąd]**. Powinny zostać zwrócone wartości **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.
   * **INPUT__FILE__NAME takich jak "%.log"** -informuje, który mamy powinno zwrócić tylko danych z plików w gałęzi. dziennika. To ogranicza hello wyszukiwania toohello sample.log pliku, który zawiera dane hello utrzymuje je z zwracać dane z innych przykładowe pliki danych, która nie pasuje do schematu hello zdefiniowanego.
3. Kliknij przycisk **przesłać**. Witaj **sesji zadania** na powitania u dołu strony hello powinien być wyświetlany szczegóły dotyczące hello zadania.
4. Gdy hello **stan** pola zmiany zbyt**Ukończono**, wybierz pozycję **Wyświetl szczegóły** hello zadania. Na stronie szczegółów hello hello **dane wyjściowe zadania** zawiera `[ERROR]    3`. Można użyć hello **Pobierz** przycisk pod tym toodownload pole plik zawierający dane wyjściowe hello hello zadania.

## <a id="summary"></a>Podsumowanie
Jak widać, powitalne Konsola zapytania zapewnia prosty sposób toorun zapytania Hive w programie klastra usługi HDInsight, monitorować stan zadania hello i pobrać dane wyjściowe hello.

Wybierz toolearn więcej informacji na temat przy użyciu konsoli zapytania Hive toorun zadań Hive, **wprowadzenie** u góry hello hello konsoli zapytania, a następnie użyć hello przykłady, które są udostępniane. Każda próbka przeprowadzi Cię przez proces hello przy użyciu danych tooanalyze gałęzi, w tym objaśnienia dotyczące instrukcje HiveQL hello używane w przykładowym hello.

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
