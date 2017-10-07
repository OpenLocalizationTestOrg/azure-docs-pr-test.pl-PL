---
title: "aaaUse akcji skryptu tooinstall Solr w usłudze HDInsight opartych na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Solr na platformie Hadoop, HDInsight opartych na systemie Linux klastrów za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Zainstalować i używać Solr w klastrach HDInsight Hadoop

Dowiedz się, jak tooinstall Solr w usłudze Azure HDInsight za pomocą akcji skryptu. Solr to platforma wyszukiwania zaawansowanego i zapewnia możliwości wyszukiwania na poziomie przedsiębiorstwa na danych zarządzanych przez usługi Hadoop.

> [!IMPORTANT]
    > kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

> [!IMPORTANT]
> Witaj przykładowy skrypt jest używany w tym dokumencie instaluje Solr 4.9 z określonej konfiguracji. Chcąc tooconfigure hello Solr klaster z różnych kolekcji, odłamków, schematów, replik, itp., należy zmodyfikować skrypt hello i Solr plików binarnych.

## <a name="whatis"></a>Co to jest Solr

[Apache Solr](http://lucene.apache.org/solr/features.html) to platforma wyszukiwania przedsiębiorstwa, która umożliwia wydajne wyszukiwanie pełnotekstowe danych. Gdy Hadoop umożliwia przechowywanie i zarządzania nimi czasach ogromne ilości danych, Apache Solr zapewnia możliwości wyszukiwania hello tooquickly pobierania hello danych.

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane przez firmę Microsoft.
>
> Niestandardowe składniki, takie jak Solr, odbierania toohelp uzasadnione ekonomicznie Obsługa toofurther należy rozwiązać problem hello. Pomoc techniczna firmy Microsoft nie może być możliwe tooresolve problemów ze składnikami niestandardowych. Aby uzyskać pomoc może być konieczne tooengage hello typu open source społeczności. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).

## <a name="what-hello-script-does"></a>Jakie skrypt hello wykonuje

Ten skrypt powoduje powitania po klastra usługi HDInsight toohello zmiany:

* Instaluje Solr 4.9 do`/usr/hdp/current/solr`
* Tworzy użytkownika, **solrusr**, która jest używana toorun hello Solr usługi
* Ustawia **solruser** jako właściciel hello`/usr/hdp/current/solr`
* Dodaje [Upstart](http://upstart.ubuntu.com/) konfiguracji, które jest uruchamiane automatycznie Solr.

## <a name="install"></a>Zainstaluj Solr za pomocą akcji skryptu

Przykładowy skrypt tooinstall Solr w klastrze usługi HDInsight jest dostępna w hello w następującej lokalizacji:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate klaster ma zainstalowany Solr, użyj hello etapami hello [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) dokumentu. Podczas procesu tworzenia hello Użyj hello następujące kroki tooinstall Solr:

1. Z hello __klastra Podsumowanie__ bloku, settings__ select__Advanced, następnie __skryptu akcji__. Użyj hello następujące informacje toopopulate hello formularza:

   * **Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.
   * **Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**: Zaznaczenie tego pola wyboru
   * **Proces ROBOCZY**: Zaznaczenie tego pola wyboru
   * **DOZORCY**: Sprawdź tooinstall tej opcji w węźle dozorcy hello
   * **Parametry**: pozostaw to pole puste

2. U dołu hello hello **skryptu akcje** bloku, użyj hello **wybierz** przycisk toosave hello konfiguracji. Na koniec użyj hello **dalej** toohello tooreturn przycisk __podsumowanie klastra__

3. Z hello __klastra Podsumowanie__ wybierz pozycję __Utwórz__ toocreate hello klastra.

## <a name="usesolr"></a>Jak używać Solr w usłudze HDInsight

> [!IMPORTANT]
> Procedura Hello w tej sekcji przedstawia podstawowe funkcje Solr. Aby uzyskać więcej informacji na temat używania Solr, zobacz hello [lokacji Apache Solr](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Dane indeksu

Użyj hello następujące kroki tooadd przykładowe dane tooSolr, a następnie wykonasz zapytania:

1. Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > Kroki opisane w dalszej części tego dokumentu, użyj protokołu SSL tunelu tooconnect toohello Solr interfejsu użytkownika sieci web. toouse tych kroków, musisz ustanowić SSL tunelowania, a następnie skonfiguruj toouse Twojego przeglądarki go.
     >
     > Aby uzyskać więcej informacji, zobacz hello [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.

2. Użyj hello następujące polecenia toohave Solr indeksu przykładowe dane:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Witaj następujące dane wyjściowe są zwracane toohello konsoli:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Witaj `post.jar` narzędzie dodaje hello **solr.xml** i **monitor.xml** dokumenty toohello indeksu.
  
3. Witaj Użyj następującego polecenia tooquery hello Solr interfejsu API REST:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    To polecenie wyszukuje **collection1** dokumenty dopasowania  **\*:\***  (zakodowane jako \*% 3A\* w ciągu zapytania hello). powitania po dokumentu JSON jest przykładem hello odpowiedzi:

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>Przy użyciu pulpitu nawigacyjnego Solr hello

pulpit nawigacyjny Solr Hello jest interfejs użytkownika umożliwiający toowork z Solr za pośrednictwem przeglądarki sieci web. pulpit nawigacyjny Solr Hello nie jest uwidaczniana bezpośrednio na powitania Internet z klastrem usługi HDInsight. Można użyć tooaccess tunelu SSH go. Aby uzyskać więcej informacji na temat używania tunelu SSH, zobacz hello [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.

Po ustanowieniu tunelu SSH, użyj hello następujące kroki toouse hello Solr w pulpicie nawigacyjnym:

1. Określić nazwę hosta hello headnode głównej hello:

   1. Użyj węzła głównego klastra toohello tooconnect SSH. Na przykład `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Użyj hello następujące polecenia tooget hello w pełni kwalifikowana nazwa hosta:

        ```bash
        hostname -f
        ```

        To polecenie zwraca wartość toohello podobne, następujące nazwy hosta:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Zapisz wartość hello zwrócona, ponieważ jest później używany.

2. W przeglądarce, za połączyć**http://HOSTNAME:8983/solr / #/**, gdzie **HOSTNAME** jest nazwą hello określone w poprzednich krokach hello.

    Żądanie hello jest kierowany przez hello SSH tunelu toohello Solr interfejsu użytkownika sieci web w klastrze. podobne toohello po obrazu zostanie wyświetlona strona Hello:

    ![Obraz pulpitu nawigacyjnego Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. W okienku po lewej stronie powitania, użyj hello **selektora Core** tooselect listy rozwijanej **collection1**. Kilka wpisów powinien je są wyświetlane poniżej **collection1**.

4. Z poniższych wpisów hello **collection1**, wybierz pozycję **zapytania**. Użyj hello następujące strony wyszukiwania hello toopopulate wartości:

   * W hello **q** tekst wprowadź  **\*:**\*. To zapytanie zwraca wszystkie dokumenty hello, które są indeksowane w Solr. Jeśli chcesz toosearch dla określonego ciągu w dokumentach hello, można wprowadzić ten ciąg w tym miejscu.
   * W hello **wt** pole tekstowe, hello wybierz format danych wyjściowych. Domyślnie jest **json**.

     Na koniec wybierz hello **wykonywanie zapytania** u dołu hello hello pate wyszukiwania.

     ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     dane wyjściowe Hello zwraca powitalne dwa dokumenty dodania toohello wcześniej indeksu. Witaj danych wyjściowych jest podobne toohello po dokumentu JSON:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Uruchamianie i zatrzymywanie Solr

Użyj następującego polecenia toomanually zatrzymywania i uruchamiania Solr hello:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Indeksowane dane kopii zapasowej

Użyj hello następujące kroki tooback się Solr danych toohello domyślny magazyn dla klastra:

1. Połącz toohello klastra przy użyciu protokołu SSH, a następnie użyj następującego polecenia tooget hello hosta nazwę węzła głównego hello hello:

    ```bash
    hostname -f
    ```

2. Użyj następującego polecenia toocreate migawkę danych hello indeksowane hello. Zastąp **HOSTNAME** o nazwie hello zwrócony z hello poprzednie polecenie:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    odpowiedź Hello jest podobne toohello po XML:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Zmień katalogi zbyt`/usr/hdp/current/solr/example/solr`. Brak podkatalogu każdej kolekcji. Każdy katalog kolekcji zawiera `data` katalogu zawierającego migawkę hello hello kolekcji.

4. toocreate skompresowanego archiwum folder migawki hello, hello Użyj następującego polecenia:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Zastąp hello `snapshot.20150806185338855` wartości o nazwie hello hello migawki kolekcji.

    To polecenie tworzy archiwum o nazwie **snapshot.20150806185338855.tgz**, który zawiera zawartość hello hello **snapshot.20150806185338855** katalogu.

5. Następnie można przechowywać klastra hello archiwum toohello głównej pamięci masowej hello następujące polecenie:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Aby uzyskać więcej informacji na temat pracy z Solr tworzenia kopii zapasowej i przywracania, zobacz [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Następne kroki

* [Zainstaluj Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md). Użyj tooinstall dostosowywania klastra, który Giraph na platformie Hadoop w HDInsight clusters. Giraph pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.

* [Instalowanie aplikacji Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md). Użyj Hue tooinstall dostosowywania klastrowania w klastrach HDInsight Hadoop. HUE jest zestaw aplikacji sieci Web użycia toointeract przy użyciu funkcji klastra usługi Hadoop.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
