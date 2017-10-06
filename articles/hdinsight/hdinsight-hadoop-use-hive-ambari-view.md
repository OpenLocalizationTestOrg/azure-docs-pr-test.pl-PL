---
title: "toowork widoków Ambari aaaUse z Hive w usłudze Azure HDInsight (Hadoop) - | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Hive View zapytań Hive toosubmit przeglądarki sieci web. Witaj Hive View jest częścią hello podane w interfejsie użytkownika sieci Web Ambari z klastrem usługi HDInsight opartej na systemie Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Użyj hello widoku Hive z usługą Hadoop w usłudze HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Dowiedz się, jak toorun Hive zapytania przy użyciu widoku Hive narzędzia Ambari. Ambari to zarządzania i monitorowania narzędzia dostarczanego z klastrami HDInsight opartych na systemie Linux. Jedną z funkcji hello zapewniana za pomocą narzędzia Ambari jest interfejsem użytkownika sieci Web, które mogą być używane toorun zapytań programu Hive.

> [!NOTE]
> Ambari ma wiele funkcji, które nie zostały omówione w tym dokumencie. Aby uzyskać więcej informacji, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari hello](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster usługi HDInsight opartej na systemie Linux. Aby uzyskać informacje dotyczące tworzenia klastra, zobacz [Rozpoczynanie pracy z opartą na systemie Linux usługą HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="open-hello-hive-view"></a>Otwórz widok Hive hello

Można widoków Ambari z hello portal Azure. Wybierz z klastrem usługi HDInsight, a następnie wybierz **widoków Ambari** z hello **szybkie linki** sekcji.

![Sekcja Szybkie linki hello portalu](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Z listy hello widoków, wybierz hello __Hive View__.

![Witaj wybrany widok gałęzi](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Podczas uzyskiwania dostępu do Ambari, to zostanie wyświetlony monit o tooauthenticate toohello lokacji. Wprowadź Witaj, Administratorze (domyślna `admin`) konta, nazwę i hasło używane podczas tworzenia hello klastra.

Powinny pojawić się Strona toohello podobne, po obrazu:

![Obraz powitania zapytania arkusza hello Hive widoku](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Uruchamianie zapytania

toorun zapytań programu hive za pomocą poniższych kroków z widoku Hive hello hello.

1. Z hello __zapytania__ karcie, Wklej hello następujące instrukcje HiveQL do arkusza hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Instrukcje te należy wykonać hello następujące akcje:

   * `DROP TABLE`— Usuwa tabeli hello i hello pliku danych, w przypadku, gdy tabela hello już istnieje.

   * `CREATE EXTERNAL TABLE`-Tworzy nową tabelę "external" w gałęzi.
   Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi. Hello danych pozostaje w hello oryginalnej lokalizacji.

   * `ROW FORMAT`— Sposób formatowania danych hello. W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.

   * `STORED AS TEXTFILE LOCATION`-Miejsce przechowywania danych hello i że jest przechowywane jako tekst.

   * `SELECT`-Wybiera liczbę wszystkich wierszy, gdzie t4 kolumna zawiera wartość hello [Błąd].

     > [!NOTE]
     > Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych. Na przykład automatyczne przekazywanie danych proces, lub przez inną operację MapReduce. Usunięcie tabeli zewnętrznej jest *nie* usunąć dane hello, tylko hello definicji tabeli.

    > [!IMPORTANT]
    > Pozostaw hello __bazy danych__ zaznaczenie na __domyślne__. Przykłady Hello w tym dokumencie Użyj hello domyślna baza danych uwzględnionych w usłudze HDInsight.

2. toostart hello zapytania, użyj hello **Execute** znajdujący się poniżej hello arkusza. Monitor przechodzi w stan pomarańczowy i hello tekst zostanie zmieniony zbyt**zatrzymać**.

3. Po zakończeniu hello zapytania, hello **wyniki** karcie są wyświetlane wyniki hello hello operacji. powitania po tekst jest wynikiem hello hello zapytania:

        sev       cnt
        [ERROR]   3

    Witaj **dzienniki** karty mogą być używane tooview hello rejestrowanie informacji o utworzonych przez zadanie hello.

   > [!TIP]
   > Witaj **Zapisz wyniki** okno dialogowe listy rozwijanej w hello górnym lewym rogu hello **wyniki przetwarzania zapytania** sekcji pozwala toodownload lub zapisać wyniki.

4. Wybierz hello pierwsze cztery wiersze tego zapytania, następnie wybierz **Execute**. Zwróć uwagę, że nie ma żadnych wyników po zakończeniu zadania hello. Przy użyciu hello **Execute** gdy część zapytania hello zaznaczona jest tylko uruchamia hello wybranego instrukcje. W takim przypadku hello zaznaczenia nie włączono hello końcowej instrukcji, która pobiera wiersze z tabeli hello. Po wybraniu tylko ten wiersz i użyj **Execute**, powinny pojawić się hello oczekiwano wyników.

5. tooadd arkusza, użyj hello **nowy arkusz** u dołu hello hello **edytora zapytań**. W nowym arkuszu hello wprowadź następujące instrukcje HiveQL hello:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Instrukcje te należy wykonać hello następujące akcje:

   * **Utwórz Tabela Jeśli nie ISTNIEJE** — tworzy tabelę, jeśli jeszcze nie istnieje. Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używana, jest tworzony wewnętrznej tabeli. Wewnętrznej tabeli są przechowywane w magazynie danych Hive hello i zarządza całkowicie Hive. W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli usuwa hello również danych źródłowych.

   * **ORC AS PRZECHOWYWANE** -przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC). ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.

   * **ZASTĄP INSERT... Wybierz** -wybiera wiersze z hello **log4jLogs** tabeli, która zawiera `[ERROR]`, a następnie hello wstawia dane do hello **errorLogs** tabeli.

     Użyj hello **Execute** przycisk toorun tego zapytania. Witaj **wyniki** karta nie zawiera żadnych informacji po hello zapytanie zwraca zero wierszy. Stan Hello powinny być widoczne jako **zakończyło się pomyślnie** po zakończeniu hello zapytania.

### <a name="visual-explain"></a>Wyjaśnić Visual

toodisplay wizualizacji hello planu zapytania, wybierz hello **wyjaśnić Visual** kartę poniżej hello arkusza.

Witaj **wyjaśnić Visual** widoku hello zapytania mogą być pomocne w opis przepływu hello złożonych zapytań. Odpowiednika tekstową tego widoku można wyświetlić przy użyciu hello **Wyjaśnij** przycisku na powitania edytora zapytań.

### <a name="tez-ui"></a>Interfejs użytkownika aplikacji tez

toodisplay hello Tez interfejsu użytkownika dla zapytania hello, wybierz hello **Tez** kartę poniżej hello arkusza.

> [!IMPORTANT]
> Tez jest nieużywane tooresolve wszystkie zapytania. Wiele zapytań można rozpoznawać bez korzystania z aplikacji Tez. 

Jeśli Tez była używana tooresolve hello zapytania, zostanie wyświetlony hello wykresu acyklicznego wskazówkami (DAG). Witaj tooview DAG dla zapytania, które zostały uruchomione w ostatnich hello, lub debugowania hello Tez proces, należy użyć hello [widoku Tez](hdinsight-debug-ambari-tez-view.md) zamiast tego.

## <a name="view-job-history"></a>Wyświetlanie historii zadań

Witaj __zadania__ kartę Wyświetla historię zapytań programu Hive.

![Obraz powitania historii zadań](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Tabele bazy danych

Można użyć hello __tabel__ karcie toowork z tabelami w bazie danych Hive.

![Obraz powitania karty tabele](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Zapisane kwerendy

Na karcie zapytania hello Opcjonalnie można zapisać zapytania. Po zapisaniu, można ponownie użyć kwerendy hello z hello __zapisane kwerendy__ kartę.

![Obraz karty zapisane kwerendy](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Funkcje zdefiniowane przez użytkownika

Można również rozszerzać hive za pomocą funkcji zdefiniowanej przez użytkownika (UDF). UDF umożliwia funkcjonalności tooimplement lub logikę, która nie jest łatwo uformowana w HiveQL.

Hello kartę UDF u góry hello hello Hive View pozwala toodeclare i Zapisywanie zestawu funkcji UDF. Te funkcje UDF mogą być używane z hello **edytora zapytań**.

![Obraz karty funkcji zdefiniowanej przez użytkownika](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Po dodaniu toohello UDF Hive View **Wstaw funkcje UDF** u dołu hello hello pojawi się przycisk **edytora zapytań**. Wybranie tego wpisu powoduje wyświetlenie listy rozwijanej hello funkcji UDF zdefiniowane w hello Hive widoku. Wybieranie funkcji zdefiniowanej przez użytkownika dodaje HiveQL instrukcje tooyour zapytania tooenable hello funkcji zdefiniowanej przez użytkownika.

Na przykład, jeśli zdefiniowano UDF z hello następujące właściwości:

* Nazwa zasobu: myudfs

* Ścieżka zasobu: /myudfs.jar

* Nazwa funkcji zdefiniowanej przez użytkownika: myawesomeudf

* Nazwa klasy funkcji zdefiniowanej przez użytkownika: com.myudfs.Awesome

Przy użyciu hello **Wstaw funkcje UDF** przycisk zawiera wpis o nazwie **myudfs**, z innej listy rozwijanej dla każdej funkcji zdefiniowanej przez użytkownika zdefiniowany dla tego zasobu. W takim przypadku **myawesomeudf**. Wybranie tego wpisu dodaje powitania od początku toohello hello zapytania:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

Następnie można hello UDF w zapytaniu. Na przykład `SELECT myawesomeudf(name) FROM people;`.

Aby uzyskać więcej informacji o korzystaniu z funkcji UDF z Hive w usłudze HDInsight Zobacz hello w następujących dokumentach:

* [Przy użyciu języka Python z Hive i Pig w usłudze HDInsight](hdinsight-python.md)
* [Jak tooadd niestandardowych tooHDInsight Hive funkcji zdefiniowanej przez użytkownika](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Gałąź, ustawienia

Ustawienia mogą być używane toochange różne ustawienia Hive. Na przykład zmiana aparat wykonywania hello gałęzi z tooMapReduce Tez (domyślnie: hello).

## <a id="nextsteps"></a>Następne kroki

Ogólne informacje na temat Hive w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)
