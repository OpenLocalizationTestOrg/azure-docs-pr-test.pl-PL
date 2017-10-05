---
title: "Hadoop Sqoop za pomocą Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zdalnie przesyłania zadań Sqoop do usługi HDInsight przy użyciu programu Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Uruchamianie zadań Sqoop z platformą Hadoop w usłudze HDInsight z Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Dowiedz się, jak używać Curl do uruchomienia zadań Sqoop na klastra usługi Hadoop w usłudze HDInsight.

Zwinięcie służy do pokazują, jak można interakcję z usługą HDInsight przy użyciu pierwotne żądania HTTP można uruchamiać, monitorować i pobrać wyniki zadań Sqoop. To działanie przy użyciu usługi WebHCat interfejsu API REST (wcześniej znane jako Templeton) pochodzącymi z klastrem usługi HDInsight.

> [!NOTE]
> Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale dopiero zaczynasz korzystać z usługi HDInsight, zobacz [informacji na temat korzystania z usługi HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Aby wykonać kroki opisane w tym artykule, będą potrzebne następujące czynności:

* Hadoop w klastrze usługi HDInsight (Linux lub z systemem Windows)
* [Narzędzie curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Przesyłanie zadań Sqoop przy użyciu Curl
> [!NOTE]
> Używając programu Curl lub innego połączenia REST z usługą WebHCat, należy uwierzytelnić żądania, podając nazwę użytkownika i hasło administratora klastra usługi HDInsight. Należy również użyć nazwy klastra jako części identyfikatora URI stosowanego przy wysyłaniu żądań do serwera.
> 
> W przypadku poleceń w tej sekcji należy zastąpić ciąg **USERNAME** nazwą użytkownika w celu dokonania uwierzytelnienia w klastrze oraz zastąpić ciąg **PASSWORD** hasłem do konta użytkownika. Zastąp ciąg **CLUSTERNAME** nazwą klastra.
> 
> Interfejs API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego](http://en.wikipedia.org/wiki/Basic_access_authentication). Należy zawsze tworzyć żądania przy użyciu protokołu HTTPS (HTTP Secure), aby mieć pewność, że poświadczenia są bezpiecznie wysyłane do serwera.
> 
> 

1. W wierszu polecenia wpisz następujące polecenie, aby sprawdzić możliwość nawiązania połączenia z klastrem usługi HDInsight:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Użytkownik powinien otrzymywać odpowiedź podobną do następującej:
   
        {"status":"ok","version":"v1"}
   
    W tym poleceniu są używane następujące parametry:
   
   * **-u** — nazwa użytkownika i hasło używane do uwierzytelnienia żądania.
   * **-G** — parametr wskazujący, że jest to żądanie GET.
     
     Adres URL, na początek **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, będą takie same dla wszystkich żądań. Ścieżka, **/status**, wskazuje, czy żądanie jest próbę zwrócenia stanu usługi WebHCat (znanej także jako Templeton) dla serwera. 
2. Poniższa tabela przedstawia zadania sqoop:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    W tym poleceniu są używane następujące parametry:

    * **-d** — od `-G` nie jest używany domyślnie żądania metody POST. `-d`Określa dane, które są wysyłane z żądania.

        * **User.name** — użytkownik, który uruchamia polecenie.

        * **polecenie** -Sqoop polecenie do wykonania.

        * **statusdir** -katalog, w którym zostanie zapisany stan dla tego zadania.

    To polecenie powinien zwrócić identyfikator zadania, który może służyć do sprawdzania stanu zadania.

        {"id":"job_1415651640909_0026"}

1. Aby sprawdzić stan zadania, użyj następującego polecenia. Zastąp **JOBID** o wartości zwracanej w poprzednim kroku. Na przykład, jeśli była zwracana wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Jeśli zadanie zostało zakończone, stan będzie **zakończyło się pomyślnie**.
   
   > [!NOTE]
   > To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu; jq służy do pobierania wartości stan.
   > 
   > 
2. Gdy stan zadania został zmieniony na **zakończyło się pomyślnie**, wyniki zadania można pobrać z magazynu obiektów Blob platformy Azure. `statusdir` Parametr przekazany z zapytaniem zawiera lokalizację pliku wyjściowego; w takim przypadku **wasb: / / / przykład/zwinięcie**. Ten adres są przechowywane dane wyjściowe zadania w **przykład/zwinięcie** katalogu na domyślnego kontenera magazynu używane przez klaster usługi HDInsight.
   
    Można wyświetlić listę i takie pliki należy pobierać za pomocą [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md). Na przykład, aby wyświetlić listę plików w **przykład/zwinięcie**, użyj następującego polecenia:
   
        azure storage blob list <container-name> example/curl
   
    Aby pobrać plik, użyj następującego polecenia:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Podaj nazwę konta magazynu zawierające obiektu blob przy użyciu `-a` i `-k` parametrów lub zestawu **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_dostępu\_klucza** zmiennych środowiskowych. Zobacz < href = "hdinsight przekazywania data.md" target = "_blank", aby uzyskać więcej informacji.
   > 
   > 

## <a name="limitations"></a>Ograniczenia
* Zbiorcze export - opartych na systemie Linux z usługi HDInsight, łącznik Sqoop, używany do eksportowania danych do programu Microsoft SQL Server lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.
* Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop będzie wykonywać wiele operacji wstawienia zamiast przetwarzanie wsadowe operacji insert.

## <a name="summary"></a>Podsumowanie
Jak pokazano w tym dokumencie, można użyć raw żądania HTTP można uruchamiać, monitorować i wyświetlić wyniki zadania Sqoop w klastrze usługi HDInsight.

Aby uzyskać więcej informacji dotyczących interfejsu REST używane w tym artykule, zobacz <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Podręcznik interfejsu API REST Sqoop</a>.

## <a name="next-steps"></a>Następne kroki
Ogólne informacje na temat programu Hive z HDInsight:

* [Używanie Sqoop z platformą Hadoop w usłudze HDInsight](hdinsight-use-sqoop.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

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


