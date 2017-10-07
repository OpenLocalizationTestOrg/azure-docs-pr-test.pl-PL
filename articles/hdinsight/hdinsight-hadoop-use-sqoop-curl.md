---
title: "aaaUse Hadoop Sqoop z Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooremotely przesłać tooHDInsight zadania Sqoop przy użyciu programu Curl."
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Uruchamianie zadań Sqoop z platformą Hadoop w usłudze HDInsight z Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Dowiedz się, jak klastra toouse Curl toorun Sqoop zadania na platformie Hadoop w usłudze HDInsight.

Zwinięcie jest używane toodemonstrate sposób można interakcji z usługą HDInsight przy użyciu raw toorun żądania HTTP, monitor i pobrać hello wyniki zadań Sqoop. To działanie za pomocą hello WebHCat interfejsu API REST (wcześniej znane jako Templeton) pochodzącymi z klastrem usługi HDInsight.

> [!NOTE]
> Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz [informacji na temat korzystania z usługi HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:

* Hadoop w klastrze usługi HDInsight (Linux lub z systemem Windows)
* [Narzędzie curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Przesyłanie zadań Sqoop przy użyciu Curl
> [!NOTE]
> Po za pomocą Curl lub innego połączenia REST z usługą WebHCat, zapewniając hello nazwę użytkownika i hasło administratora klastra usługi HDInsight hello musi uwierzytelnić się hello żądania. Należy również użyć nazwy klastra hello jako część hello identyfikator URI (Uniform Resource) używane toosend hello żądań toohello serwera.
> 
> Hello poleceń w tej sekcji, Zastąp **USERNAME** hello użytkownika tooauthenticate toohello klastra i Zastąp **hasło** hello hasła dla konta użytkownika hello. Zastąp **CLUSTERNAME** o nazwie hello klastra.
> 
> Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelnianie podstawowe](http://en.wikipedia.org/wiki/Basic_access_authentication). Należy zawsze tworzyć żądania przy użyciu HTTPS (HTTP Secure) toohelp upewnij się, że poświadczenia są bezpiecznie wysyłane toohello serwera.
> 
> 

1. Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Powinien zostać wyświetlony poniżej toohello podobne odpowiedzi:
   
        {"status":"ok","version":"v1"}
   
    Parametry Hello używane w tym poleceniu są następujące:
   
   * **-u** -hello nazwę użytkownika i hasło używane tooauthenticate hello żądania.
   * **-G** — parametr wskazujący, że jest to żądanie GET.
     
     Witaj rozpoczęciem powitalne adresu URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, będzie hello takie same dla wszystkich żądań. Ścieżka Hello **/status**, wskazuje, że Żądanie hello jest tooreturn stan usługi WebHCat (znanej także jako Templeton) powitania serwera. 
2. Użyj powitania po toosubmit zadania sqoop:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    Parametry Hello używane w tym poleceniu są następujące:

    * **-d** — od `-G` nie jest używany, domyślnie przyjmowana jest hello żądania metody POST toohello. `-d`Określa hello wartości danych, które są wysyłane z żądania hello.

        * **User.name** -hello użytkownik, który uruchamia polecenie hello.

        * **polecenie** — Witaj tooexecute polecenia Sqoop.

        * **statusdir** -hello katalogu, w którym hello stanu dla tego zadania zostanie zapisany.

    To polecenie powinien zwrócić Identyfikatora zadania, które mogą być używane toocheck stan hello hello zadania.

        {"id":"job_1415651640909_0026"}

1. Stan hello toocheck hello zadania, hello Użyj następującego polecenia. Zastąp **JOBID** z wartością hello zwracane w poprzednim kroku hello. Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Jeśli hello zadanie zostało zakończone, stan hello zostanie **zakończyło się pomyślnie**.
   
   > [!NOTE]
   > To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu hello; Służy jq tooretrieve hello tylko wartość stanu.
   > 
   > 
2. Gdy stan hello hello zadania został zmieniony zbyt**zakończyło się pomyślnie**, hello wyników zadania hello można pobrać z magazynu obiektów Blob platformy Azure. Witaj `statusdir` przekazany parametr zapytania o hello zawiera lokalizację hello hello pliku wyjściowego; w takim przypadku **wasb: / / / przykład/zwinięcie**. Ten adres są przechowywane dane wyjściowe hello hello zadania w hello **przykład/zwinięcie** katalogu na powitania domyślnego kontenera magazynu używane przez klaster usługi HDInsight.
   
    Można wyświetlić listę i takie pliki należy pobierać za pomocą hello [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md). Na przykład pliki toolist w **przykład/zwinięcie**, użyj następującego polecenia hello:
   
        azure storage blob list <container-name> example/curl
   
    toodownload plik, użyj następujących hello:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Należy określić nazwy konta magazynu hello zawierającej hello obiektów blob przy użyciu hello `-a` i `-k` parametrów lub zestaw hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_dostępu\_klucza** zmiennych środowiskowych. Zobacz < href = "hdinsight przekazywania data.md" target = "_blank", aby uzyskać więcej informacji.
   > 
   > 

## <a name="limitations"></a>Ograniczenia
* Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.
* Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop będzie wykonywać wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.

## <a name="summary"></a>Podsumowanie
Jak pokazano w tym dokumencie, można użyć raw toorun żądania HTTP, monitor i wyświetlić wyniki hello Sqoop zadań w klastrze usługi HDInsight.

Aby uzyskać więcej informacji na interfejsie REST hello używane w tym artykule, zobacz hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Podręcznik interfejsu API REST Sqoop</a>.

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


