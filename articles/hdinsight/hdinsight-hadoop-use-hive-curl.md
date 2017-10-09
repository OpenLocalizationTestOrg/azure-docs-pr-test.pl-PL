---
title: "aaaUse Hadoop Hive z Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przesyłania tooremotely Pig zadania tooHDInsight przy użyciu programu Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Uruchamianie zapytań Hive z usługą Hadoop w usłudze HDInsight za pomocą usługi REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Dowiedz się, jak toouse hello interfejsu API REST usługi WebHCat toorun Hive zapytania Hadoop w usłudze Azure HDInsight klastrze.

[Curl](http://curl.haxx.se/) jest używane toodemonstrate, jak można interakcję z usługą HDInsight przy użyciu pierwotne żądania HTTP. Witaj [jq](http://stedolan.github.io/jq/) narzędzie jest używane tooprocess hello JSON zwrócono dane z żądania REST.

> [!NOTE]
> Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz hello [potrzebnych tooknow dotyczące usługi Hadoop w HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md) dokumentu.

## <a id="curl"></a>Uruchamianie zapytań Hive

> [!NOTE]
> Po za pomocą cURL lub innego połączenia REST z usługą WebHCat, zapewniając hello nazwę użytkownika i hasło administratora klastra usługi HDInsight hello musi uwierzytelnić się hello żądania.
>
> Hello poleceń w tej sekcji, Zastąp **USERNAME** hello użytkownika tooauthenticate toohello klastra i Zastąp **hasło** hello hasła dla konta użytkownika hello. Zastąp **CLUSTERNAME** o nazwie hello klastra.
>
> Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelnianie podstawowe](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp upewnij się, że poświadczenia są bezpiecznie wysyłane toohello server, zawsze tworzyć żądania przy użyciu protokołu HTTP Secure (HTTPS).

1. Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Pojawi się odpowiedź toohello podobne, następującego tekstu:

        {"status":"ok","version":"v1"}

    Parametry Hello używane w tym poleceniu są następujące:

   * **-u** -hello nazwę użytkownika i hasło używane tooauthenticate hello żądania.
   * **-G** — wskazuje, że to żądanie jest operacji GET.

     Witaj rozpoczęciem powitalne adresu URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest hello takie same dla wszystkich żądań. Ścieżka Hello **/status**, wskazuje, że Żądanie hello jest tooreturn stan usługi WebHCat (znanej także jako Templeton) powitania serwera. Możesz również zażądać hello wersję gałęzi przy użyciu hello następujące polecenie:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     To żądanie zwraca odpowiedź toohello podobne, następującego tekstu:

       {"module": "hive", "version": "0.13.0.2.1.6.0-2103"}

2. Użyj powitania po toocreate tabela o nazwie **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    następujące parametry używane z tym żądaniem Hello:

   * **-d** — od `-G` nie jest używany, domyślnie przyjmowana jest hello żądania metody POST toohello. `-d`Określa hello wartości danych, które są wysyłane z żądania hello.

     * **User.name** -hello użytkownik, który uruchamia polecenie hello.
     * **wykonanie** — Witaj tooexecute instrukcje HiveQL.
     * **statusdir** -hello katalogu, w którym hello stanu dla tego zadania jest zapisywany.

     Instrukcje te należy wykonać hello następujące akcje:
   * **DROP TABLE** — Jeśli hello tabela już istnieje, jest usuwany.
   * **Tworzenie tabeli zewnętrznej** — tworzy nową tabelę "zewnętrzne" w gałęzi. Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi. Hello danych pozostaje w hello oryginalnej lokalizacji.

     > [!NOTE]
     > Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych. Na przykład procesu przekazywania danych lub inna operacja MapReduce.
     >
     > Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.

   * **FORMAT wiersza** — sposób formatowania danych hello. Witaj pól w każdym dzienniku są oddzielone spacją.
   * **PRZECHOWYWANE jako lokalizacji TEXTFILE** — w przypadku, gdy są przechowywane dane hello (katalog hello przykład/danych) i które są przechowywane jako tekst.
   * **Wybierz** -wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość hello **[Błąd]**. Ta instrukcja zwraca wartość **3** są trzy wiersze, które zawierają tę wartość.

     > [!NOTE]
     > Zwróć uwagę, hello spacji między instrukcje HiveQL zastępuje hello `+` znak, gdy jest używany z Curl. Wartości w cudzysłowie, zawierające spację, takich jak ogranicznik hello nie powinna zostać zastąpiona przez `+`.

   * **INPUT__FILE__NAME takich jak '% 25.log'** — ta instrukcja limity hello wyszukiwania tooonly używanych plików kończy się rozszerzeniem. dziennika.

     > [!NOTE]
     > Witaj `%25` jest hello zakodowane w adresie URL formularza %, więc warunek rzeczywiste hello jest `like '%.log'`. Hello % ma URL toobe zakodowane, ponieważ jest ona traktowana jako znak specjalny w adresach URL.

     To polecenie powinien zwrócić Identyfikatora zadania, które mogą być używane toocheck stan hello hello zadania.

       {"id": "job_1415651640909_0026"}

3. Stan hello toocheck hello zadania, hello Użyj następującego polecenia:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Zastąp **JOBID** z wartością hello zwracane w poprzednim kroku hello. Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.

    Jeśli hello zadanie zostało zakończone, stan hello jest **zakończyło się pomyślnie**.

   > [!NOTE]
   > To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu hello. Służy Jq tooretrieve hello tylko wartość stanu.

4. Gdy stan hello hello zadania został zmieniony zbyt**zakończyło się pomyślnie**, hello wyników zadania hello można pobrać z magazynu obiektów Blob platformy Azure. Witaj `statusdir` przekazany parametr zapytania o hello zawiera lokalizację hello hello pliku wyjściowego; w takim przypadku **/przykład/zwinięcie**. Ten adres są przechowywane dane wyjściowe hello w hello **przykład/zwinięcie** katalogu w hello klastrów domyślnego magazynu.

    Można wyświetlić listę i takie pliki należy pobierać za pomocą hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Aby uzyskać więcej informacji na temat używania hello wiersza polecenia platformy Azure z usługą Azure Storage, zobacz hello [Użyj Azure CLI 2.0 z usługą Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) dokumentu.

5. Użyj hello następujące instrukcje toocreate nową tabelę "internal" o nazwie **errorLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Instrukcje te należy wykonać hello następujące akcje:

   * **Utwórz Tabela Jeśli nie ISTNIEJE** — tworzy tabelę, jeśli jeszcze nie istnieje. Ta instrukcja tworzy wewnętrznej tabeli, który jest przechowywany w magazynie danych Hive hello i zarządza całkowicie Hive.

     > [!NOTE]
     > W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli usuwa hello również danych źródłowych.

   * **ORC AS PRZECHOWYWANE** -przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC). ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.
   * **ZASTĄP INSERT... Wybierz** -wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie wstawia hello danych do hello **errorLogs** tabeli.
   * **Wybierz** -wybiera wszystkie wiersze z nowego hello **errorLogs** tabeli.

6. Za pomocą Identyfikatora zadania hello zwrócił stan hello toocheck hello zadania. Po zakończyła się pomyślnie, należy użyć wiersza polecenia platformy Azure, jak opisano wcześniej toodownload i wyświetlania wyników hello hello. dane wyjściowe Hello powinien zawierać trzy wiersze, które zawierają **[Błąd]**.

## <a id="nextsteps"></a>Następne kroki

Ogólne informacje na temat programu Hive z HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów dla informacji debugowania:

* [Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux](hdinsight-debug-ambari-tez-view.md)

Aby uzyskać więcej informacji na powitania interfejsu API REST używany w tym dokumencie, zobacz hello [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) dokumentu.

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


