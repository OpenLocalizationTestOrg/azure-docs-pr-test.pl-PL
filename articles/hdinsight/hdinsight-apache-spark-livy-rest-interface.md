---
title: "aaaUse klastra tooSpark zadania toosubmit Livy Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toosubmit interfejsu API REST Spark Apache Spark zadania zdalnie tooan klaster Azure HDInsight."
keywords: Platforma Apache spark rest api, livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Użyj interfejsu API Apache Spark REST toosubmit zdalnego zadania tooan klastra Spark w usłudze HDInsight

Dowiedz się, jak toouse Livy, hello Apache interfejsu API REST Spark, która jest używana toosubmit zdalnego zadania tooan Azure HDInsight Spark klastra. Szczegółowa dokumentacja zobacz [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

Można użyć Livy toorun interakcyjne Spark powłok lub przesłać Uruchom na Spark toobe zadania wsadowego. Ten artykuł zawiera informacje o przy użyciu programu Livy toosubmit partii zadań. wstawki Hello w tym artykule Użyj toomake cURL końcowym Livy Spark toohello wywołania interfejsu API REST.

**Wymagania wstępne:**

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). W tym artykule wykorzystano toodemonstrate cURL jak wywołuje toomake interfejsu API REST względem klastra Spark w usłudze HDInsight.

## <a name="submit-a-livy-spark-batch-job"></a>Prześlij zadanie wsadowe Livy Spark
Przed wysłaniem wsadowym należy przekazać hello aplikacji jar w magazynie klastra hello skojarzony z klastrem hello. Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), narzędzie wiersza polecenia, toodo tak. Brak danych tooupload można użyć różnych innych klientów. Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Przykłady**:

* Jeśli plik jar hello znajduje się w magazynie klastra hello (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Jeśli chcesz toopass hello jar filename i hello classname jako część pliku wejściowego (w tym przykładzie dane_wejściowe.txt zgodnie)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Dowiedz się o uruchomiona w klastrze hello partie Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Przykłady**:

* Jeśli chcesz tooretrieve wszystkie instancje Livy Spark hello uruchomiona w klastrze hello:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Jeśli chcesz, aby tooretrieve określonej partii o dany identyfikator partii
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Usuwanie zadania wsadowego Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Przykład**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark i wysokiej dostępności
Livy przewiduje Spark zadania uruchomione w klastrze hello wysokiej dostępności. Oto kilka przykładów.

* Jeśli hello usługi Livy ulegnie awarii, gdy prześlesz zadania zdalnie tooa Spark klaster, hello zadanie nadal toorun w tle hello. Gdy Livy jest tworzenie kopii zapasowej, przywraca stan hello hello zadania i raporty go.
* Notesów Jupyter w usłudze HDInsight są obsługiwane przez Livy w hello wewnętrznej bazy danych. Jeśli notes działa zadanie Spark i ponownym pobiera hello usługi Livy notesu hello nadal toorun hello kodu komórek. 

## <a name="show-me-an-example"></a>Pokaż przykład
W tej sekcji możemy przyjrzeć się zadania wsadowego toosubmit przykłady toouse Livy Spark, monitorować postęp zadania hello hello, a następnie usuń go. Witaj używamy w tym przykładzie jest aplikacja hello jedną opracowane w artykule hello [Utwórz autonomiczny Scala aplikacji i toorun w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-create-standalone-application.md). w tym miejscu kroki Hello założono, że:

* Ma już kopiowane hello aplikacji jar toohello magazynu konta skojarzonego z klastrem hello.
* Masz CuRL zainstalowany na komputerze hello, gdzie chcesz następujące kroki.

Wykonaj następujące kroki hello:

1. Daj nam najpierw sprawdź, czy Livy Spark jest uruchomiona w klastrze hello. Firma Microsoft może zrobić, pobieranie listy uruchomionych partie. Jeśli są uruchomione zadanie, używając programu Livy dla powitania po raz pierwszy, dane wyjściowe hello powinien zwrócić zero.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Należy pobrać dane wyjściowe podobne toohello po fragment kodu:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Zwróć uwagę, jak ostatni wiersz hello w danych wyjściowych hello mówi **łącznie: 0**, które sugeruje nie uruchomionego partie.

2. Daj nam przesłać zadanie wsadowe. powitania po fragment używa pliku wejściowego (dane_wejściowe.txt zgodnie) toopass hello jar nazwy i nazwy klasy hello jako parametry. Jeśli używasz tych kroków z komputerem z systemem Windows, przy użyciu pliku wejściowego jest hello zalecane podejście.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Witaj parametrów w pliku hello **dane_wejściowe.txt zgodnie** są zdefiniowane w następujący sposób:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Powinny pojawić się dane wyjściowe podobne toohello po fragment kodu:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Zwróć uwagę, jak ostatni wiersz danych wyjściowych hello hello mówi **stanu: uruchamianie**. Również mówi, **identyfikator: 0**. W tym miejscu **0** jest identyfikator hello wsadu.

3. Teraz można pobrać stanu hello tej partii określone przy użyciu identyfikatora hello partii.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Powinny pojawić się dane wyjściowe podobne toohello po fragment kodu:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Witaj danych wyjściowych teraz wyświetlone **stanu: Sukces**, które sugeruje to zadanie hello zostało wykonane pomyślnie.

4. Jeśli chcesz, można usunąć hello partii.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Powinny pojawić się dane wyjściowe podobne toohello po fragment kodu:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    ostatni wiersz danych wyjściowych hello Hello pokazuje tej partii hello zostało pomyślnie usunięte. Również usunięcie zadania, gdy jest on uruchomiony, kasuje hello zadania. W przypadku usunięcia zadania, które zostało zakończone pomyślnie, lub w przeciwnym razie usuwa informacje o zadaniu hello całkowicie.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Przy użyciu programu Livy Spark w klastrach HDInsight 3.5

Klaster HDInsight 3.5 domyślnie wyłącza pliki danych przykładowych tooaccess ścieżki pliku lokalnego lub słoików. Firma Microsoft zachęca toouse hello `wasb://` ścieżka zamiast słoików tooaccess lub przykładowych danych plików z hello klastra. Jeśli chcesz toouse ścieżki lokalnej, należy zaktualizować hello Ambari konfiguracji odpowiednio. toodo tak:

1. Odwiedź portal Ambari toohello hello klastra. Witaj Interfejsu sieci Web Ambari jest dostępna w klastrze usługi HDInsight w https://**CLUSTERNAME**. azurehdidnsight.net, gdzie CLUSTERNAME jest nazwą hello klastra.

2. Lewy pasek nawigacyjny hello, kliknij **Livy**, a następnie kliknij przycisk **Configs**.

3. W obszarze **domyślne livy** Dodaj nazwę właściwości hello `livy.file.local-dir-whitelist` i ustawić jej wartości także**"/"** Jeśli chcesz tooallow pełny dostęp toofile systemu. Jeśli chcesz tooallow dostępu tylko tooa określonego katalogu, podaj hello ścieżka toothat katalog jako wartość hello.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Przesyłanie zadań Livy klastra w ramach sieci wirtualnej platformy Azure

Jeśli łączysz się tooan klastra Spark w usłudze HDInsight z wewnątrz sieci wirtualnej platformy Azure, możesz połączyć bezpośrednio tooLivy w klastrze hello. W takim przypadku hello adres URL dla punktu końcowego programu Livy jest `http://<IP address of hello headnode>:8998/batches`. W tym miejscu **8998** jest hello port, na którym jest uruchomiony Livy na powitania headnode klastra. Aby uzyskać więcej informacji na uzyskiwanie dostępu do usług na portach niepubliczne, zobacz [porty używane przez usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Poniżej przedstawiono niektóre problemy, które możesz napotkać podczas przy użyciu programu Livy zdalnego zadania przesyłania tooSpark klastrów.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>Za pomocą zewnętrznego jar z hello dodatkowego magazynu nie jest obsługiwane.

**Problem:** zadania Livy Spark odwołuje się do zewnętrznego jar z konta magazynu dodatkowe hello skojarzony z klastrem hello, hello zadanie nie powiedzie się.

**Rozwiązanie:** upewnij się, że jar hello ma toouse jest dostępna w magazynie domyślne hello skojarzony z klastrem usługi HDInsight hello.





## <a name="next-step"></a>Następny krok

* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

