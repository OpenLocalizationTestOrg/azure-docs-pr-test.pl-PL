---
title: "aaaUse MapReduce i Curl z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooremotely uruchamiania zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight za pomocą usługi REST

Dowiedz się, jak toouse hello interfejsu API REST usługi WebHCat toorun MapReduce zadania na platformie Hadoop w klastrze usługi HDInsight. Zwinięcie jest używane toodemonstrate, jak można interakcję z usługą HDInsight przy użyciu raw zadań MapReduce toorun żądania HTTP.

> [!NOTE]
> Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz hello [potrzebnych tooknow o opartych na systemie Linux platformą Hadoop w HDInsight](hdinsight-hadoop-linux-information.md) dokumentu.


## <a id="prereq"></a>Wymagania wstępne

* Usługi w klastrze usługi HDInsight Hadoop
* [Narzędzie curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Uruchamianie zadań MapReduce przy użyciu programu Curl

> [!NOTE]
> Użycie Curl lub innego połączenia REST z usługą WebHCat, muszą uwierzytelnić żądania hello przez podanie nazwy użytkownika administratora klastra usługi HDInsight hello i hasła. Należy użyć nazwy klastra hello jako część hello identyfikator URI, który jest używany toosend hello żądań toohello serwera.
>
> Hello poleceń w tej sekcji, Zastąp **USERNAME** hello użytkownika tooauthenticate toohello klastra i **hasło** hello hasła dla konta użytkownika hello. Zastąp **CLUSTERNAME** o nazwie hello klastra.
>
> Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego dostępu](http://en.wikipedia.org/wiki/Basic_access_authentication). Należy zawsze tworzyć żądania przy użyciu tooensure HTTPS, że poświadczenia są bezpiecznie wysyłane toohello serwera.


1. Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Powinien zostać wyświetlony podobne toohello o następujące JSON odpowiedzi:

        {"status":"ok","version":"v1"}

    Parametry Hello używane w tym poleceniu są następujące:

   * **-u**: wskazuje hello nazwę użytkownika i hasło używane tooauthenticate hello żądania
   * **-G**: oznacza, że ta operacja jest żądanie pobrania

     Witaj, początek hello identyfikatora URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest hello takie same dla wszystkich żądań.

2. toosubmit zadania MapReduce, hello Użyj następującego polecenia:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    koniec Hello hello identyfikatora URI (/ mapreduce/jar) określa, że usługi WebHCat to żądanie rozpoczęcia zadania MapReduce z klasy w pliku jar. Parametry Hello używane w tym poleceniu są następujące:

   * **-d**: `-G` nie jest używana, więc żądania hello domyślne toohello metody POST. `-d`Określa hello wartości danych, które są wysyłane z żądania hello.
    * **User.name**: hello użytkownik, który uruchamia polecenie hello
    * **JAR**: uruchomiono hello lokalizacji pliku jar hello, który zawiera toobe klasy
    * **Klasa**: hello klasy, która zawiera logikę MapReduce hello
    * **ARG**: hello toobe Argumenty przekazane toohello zadania MapReduce. W takim przypadku hello wejściowych katalogu plików i hello tekst, który są używane dla danych wyjściowych hello

     Identyfikator zadania, które mogą być używane toocheck hello stan zadania hello powinny zostać zwrócone przez to polecenie:

       {"id": "job_1415651640909_0026"}

3. Stan hello toocheck hello zadania, hello Użyj następującego polecenia:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Zastąp hello **JOBID** z wartością hello zwracane w poprzednim kroku hello. Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie hello byłoby JOBID `job_1415651640909_0026`.

    Jeśli zakończeniu zadania hello hello stanu zwrócony `SUCCEEDED`.

   > [!NOTE]
   > To żądanie Curl zwraca informacje o zadaniu hello dokumentu JSON. Służy Jq tooretrieve hello tylko wartość stanu.

4. Gdy stan hello hello zadania został zmieniony zbyt`SUCCEEDED`, hello wyników zadania hello można pobrać z magazynu obiektów Blob platformy Azure. Witaj `statusdir` parametr przekazywany z zapytaniem hello zawiera lokalizację hello hello pliku wyjściowego. W tym przykładzie lokalizacji hello jest `/example/curl`. Ten adres przechowuje hello dane wyjściowe zadania hello w magazynie domyślne klastrów hello na `/example/curl`.

Można wyświetlić listę i takie pliki należy pobierać za pomocą hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Aby uzyskać więcej informacji na temat pracy z obiektami blob z hello wiersza polecenia platformy Azure, zobacz hello [hello Using Azure CLI 2.0 z usługą Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) dokumentu.

## <a id="nextsteps"></a>Następne kroki

Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:

* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)

Aby uzyskać więcej informacji na temat interfejsu REST hello, który jest używany w tym artykule, zobacz hello [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
