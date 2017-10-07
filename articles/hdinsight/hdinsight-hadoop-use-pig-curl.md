---
title: "aaaUse Hadoop z języka Pig z REST w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastra toouse REST toorun Pig Latin zadania na platformie Hadoop w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Uruchamianie zadań Pig z usługą Hadoop w usłudze HDInsight przy użyciu REST

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Dowiedz się, jak toorun Pig Latin zadania przez klaster Azure HDInsight tooan żądań REST. Zwinięcie jest używane toodemonstrate sposób można interakcji z usługą HDInsight przy użyciu interfejsu API REST usługi WebHCat hello.

> [!NOTE]
> Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz [porady HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Wymagania wstępne

* Klaster HDInsight Azure (na platformie Hadoop w usłudze HDInsight) (opartych na systemie Linux lub z systemem Windows)

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* [Narzędzie curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Uruchamianie zadań Pig przy użyciu Curl

> [!NOTE]
> Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego dostępu](http://en.wikipedia.org/wiki/Basic_access_authentication). Zawsze tworzyć żądania przy użyciu tooensure HTTP Secure (HTTPS), że poświadczenia są bezpiecznie wysyłane toohello serwera.
>
> Korzystając z polecenia hello w tej sekcji, Zastąp `USERNAME` hello użytkownika tooauthenticate toohello klastra i Zastąp `PASSWORD` hello hasła dla konta użytkownika hello. Zastąp `CLUSTERNAME` o nazwie hello klastra.
>


1. Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Powinien zostać wyświetlony powitania po JSON odpowiedzi:

        {"status":"ok","version":"v1"}

    Parametry Hello używane w tym poleceniu są następujące:

    * **-u**: hello nazwę użytkownika i hasło używane tooauthenticate hello żądania
    * **-G**: wskazuje, że to żądanie jest żądanie pobrania

     Witaj rozpoczęciem powitalne adresu URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest hello takie same dla wszystkich żądań. Ścieżka Hello **/status**, oznacza to Żądanie hello stan hello tooreturn WebHCat (znanej także jako Templeton) powitania serwera.

2. Użyj następującego kodu toosubmit klastra toohello zadania Pig Latin hello:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    Parametry Hello używane w tym poleceniu są następujące:

    * **-d**: ponieważ `-G` nie jest używany, domyślnie przyjmowana jest hello żądania metody POST toohello. `-d`Określa hello wartości danych, które są wysyłane z żądania hello.

    * **User.name**: hello użytkownik, który uruchamia polecenie hello
    * **wykonanie**: hello Pig Latin tooexecute — instrukcje
    * **statusdir**: hello katalogu, w którym hello stanu dla tego zadania jest zapisywany

    > [!NOTE]
    > Zwróć uwagę, hello spacje w instrukcjach Pig Latin zastępuje hello `+` znak, gdy jest używany z Curl.

    To polecenie powinny zostać zwrócone identyfikator zadania, które mogą być używane toocheck hello stan zadania hello, na przykład:

        {"id":"job_1415651640909_0026"}

3. Stan hello toocheck hello zadania, hello Użyj następującego polecenia

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Zastąp `JOBID` z wartością hello zwracane w poprzednim kroku hello. Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie `JOBID` jest `job_1415651640909_0026`.

    Jeśli hello zadanie zostało zakończone, stan hello jest **zakończyło się pomyślnie**.

    > [!NOTE]
    > To żądanie Curl zwraca dokumentu JavaScript Object Notation (JSON), informacje o zadaniu hello i jq jest używane tooretrieve hello tylko wartość stanu.

## <a id="results"></a>Wyświetl wyniki

Gdy stan hello hello zadania został zmieniony zbyt**zakończyło się pomyślnie**, można pobrać wyników hello hello zadania. Witaj `statusdir` przekazany parametr zapytania o hello zawiera lokalizację hello hello pliku wyjściowego; w takim przypadku `/example/pigcurl`.

HDInsight można użyć usługi Azure Storage lub usługi Azure Data Lake Store jako hello domyślnego magazynu danych. Istnieją różne sposoby tooget hello danych, w zależności od tego, która z nich korzystać. Aby uzyskać więcej informacji, zobacz hello magazynu część hello [informacji opartą na systemie Linux usługą HDInsight](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) dokumentu.

## <a id="summary"></a>Podsumowanie

Jak pokazano w tym dokumencie, można użyć raw toorun żądania HTTP, monitor i wyświetlić wyniki hello zadań Pig w klastrze usługi HDInsight.

Aby uzyskać więcej informacji na temat interfejsu REST hello używane w tym artykule, zobacz hello [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Następne kroki

Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)
