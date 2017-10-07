---
title: "aaaInstall Presto w usłudze Azure HDInsight w systemie Linux klastrów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Presto i Airpal na platformie Hadoop, HDInsight opartych na systemie Linux klastrów za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Zainstalować i używać Presto w klastrach HDInsight Hadoop

W tym temacie dowiesz się, jak tooinstall Presto na platformie Hadoop w HDInsight clusters za pomocą akcji skryptu. Możesz także dowiedzieć się, jak tooinstall Airpal w istniejącym klastrze Presto usługi HDInsight.

> [!IMPORTANT]
> Witaj kroki w tym dokumencie wymagają **klastra usługi HDInsight Hadoop 3.5** używającą systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [wersji usługi HDInsight](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>Co to jest Presto?
[Presto](https://prestodb.io/overview.html) jest szybkie rozproszonej aparatu zapytań SQL dla danych big data. Presto nadaje się do interaktywnego kwerend do poziomu petabajtów danych. Aby uzyskać więcej informacji na składniki hello Presto i jak one współdziałają, zobacz [Presto pojęcia](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane i Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.
> 
> Niestandardowe składniki, takie jak Presto, odbierania toohelp uzasadnione ekonomicznie Obsługa toofurther należy rozwiązać problem hello. Może to spowodować nad rozwiązaniem problemu hello lub proszenia tooengage dostępnych kanałów dla hello otwarty technologii źródła wykryto głębokie doświadczenia z tej technologii. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).
> 
> 


## <a name="install-presto-using-script-action"></a>Zainstaluj Presto za pomocą akcji skryptu

Ta sekcja zawiera instrukcje jak toouse hello przykładowy skrypt podczas tworzenia nowego klastra za pomocą hello portalu Azure. 

1. Uruchom inicjowania obsługi klastra za pomocą kroków hello w [klastrów usługi HDInsight opartych na systemie Linux należy](hdinsight-hadoop-create-linux-clusters-portal.md). Upewnij się, że tworzenie klastra hello przy użyciu hello **niestandardowy** przepływu tworzenia klastra. Należy się upewnić się, że tworzenia klastra hello spełnia następujące wymagania hello.

    a. Musi to być klastra usługi Hadoop z usługą HDInsight w wersji 3.5.

    b. Należy użyć usługi Azure Storage hello przechowywania danych. Używanie Presto w klastrze, który używa usługi Azure Data Lake Store jako opcji magazynu hello nie jest jeszcze obsługiwane. 

    ![Tworzenie klastra usługi HDInsight przy użyciu niestandardowych opcji](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. Na powitania **Zaawansowane ustawienia** bloku, wybierz opcję **akcji skryptu**i podaj poniższe informacje hello:
   
   * **Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.
   * **Identyfikator URI skryptu powłoki systemowej**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **HEAD**: Zaznaczenie tego pola wyboru
   * **Proces ROBOCZY**: Zaznaczenie tego pola wyboru
   * **DOZORCY**: wyczyść to pole wyboru
   * **Parametry**: pozostaw to pole puste


3. U dołu hello hello **akcji skryptu** bloku, kliknij przycisk hello **wybierz** przycisk toosave hello konfiguracji. Na koniec kliknij hello **wybierz** u dołu hello hello **Zaawansowane ustawienia** bloku toosave hello — informacje o konfiguracji.

4. Kontynuuj, inicjowania obsługi klastra hello zgodnie z opisem w [klastrów usługi HDInsight opartych na systemie Linux należy](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Program Azure PowerShell, hello Azure CLI, hello zestawu .NET SDK usługi HDInsight lub szablonów usługi Azure Resource Manager może być również używane tooapply akcji skryptu. Można także zastosować tooalready akcji skryptu działające klastry. Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Korzystanie z usługą HDInsight Presto

Wykonaj następujące kroki toouse Presto w klastrze usługi HDInsight, po zainstalowaniu go za pomocą hello opisane powyżej hello.

1. Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Uruchom powłokę Presto hello przy użyciu następującego polecenia hello.
   
        presto --schema default

3. Uruchom zapytania w tabeli próbki **hivesampletable**, który jest dostępny na wszystkich klastrach HDInsight domyślnie.
   
        select count (*) from hivesampletable;
   
    Domyślnie [Hive](https://prestodb.io/docs/current/connector/hive.html) i [TPCH](https://prestodb.io/docs/current/connector/tpch.html) łączników dla Presto są już skonfigurowane. Łącznik hive jest skonfigurowany toouse hello domyślnie zainstalowaną Hive instalacji dlatego wszystkie tabele hello Hive będzie automatycznie wyświetlane w Presto.

    Aby uzyskać szczegółowy opis używania Presto, zobacz [Presto dokumentacji](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Airpal za pomocą Presto

[Airpal](https://github.com/airbnb/airpal#airpal) jest interfejsem open source opartych na sieci web zapytania dla Presto. Aby uzyskać więcej informacji o Airpal, zobacz [dokumentacji Airpal](https://github.com/airbnb/airpal#airpal).

W tej sekcji opisano kroki hello zbyt**zainstalować Airpal na powitania edgenode** klastra usługi HDInsight Hadoop Presto już zainstalowane. Dzięki temu interfejsu zapytania hello Airpal sieci web jest dostępna za pośrednictwem hello Internet.

1. Przy użyciu protokołu SSH, połączenie headnode toohello klastra usługi HDInsight hello, który zainstalował Presto:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Po nawiązaniu połączenia uruchom następujące polecenie hello.

        sudo slider registry  --name presto1 --getexp presto 
   
    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. Z danych wyjściowych hello, zanotuj wartość hello na powitania **wartość** właściwości. Będzie on potrzebny podczas instalowania Airpal na powitania edgenode klastra. Z danych wyjściowych hello powyżej wartości hello, który będzie potrzebny jest **10.0.0.12:9090**.

4. Użyj szablonu hello  **[tutaj](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate HDInsight klastra edgenode i podaj wartości hello, jak pokazano w hello następującego zrzutu ekranu.

    ![HDInsight instalacji Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Kliknij pozycję **Kup**.

6. Po zatwierdzeniu zmian hello zastosowane toohello konfiguracji klastra, mogą korzystać interfejs sieci web Airpal hello za pomocą hello następujące kroki.

    a. W bloku klastra powitania kliknij **aplikacji**.

    ![Uruchamianie usługi HDInsight Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. Z hello **zainstalowane aplikacje** bloku, kliknij przycisk **Portal** przed airpal.

    ![Uruchamianie usługi HDInsight Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. Po wyświetleniu monitu wprowadź poświadczenia administratora hello, które określono podczas tworzenia klastra usługi HDInsight Hadoop hello.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Dostosowanie Presto instalacji w klastrze usługi HDInsight

Po zainstalowaniu Presto w klastrze usługi HDInsight Hadoop, można dostosować hello instalacji toomake zmiany, takie jak ustawienia pamięci aktualizacji, zmień łączniki, itp. Wykonaj hello, więc po toodo czynności.

1. Przy użyciu protokołu SSH, połączenie headnode toohello klastra usługi HDInsight hello, który zainstalował Presto:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Wprowadź zmiany w konfiguracji w pliku hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Aby uzyskać więcej informacji na Presto konfiguracji, zobacz [Presto konfiguracji dla klastrów YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).

3. Zatrzymaj i kasowanie hello bieżącego uruchomione wystąpienie Presto.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Nowe wystąpienie klasy Presto rozpoczynać się hello dostosowania.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Poczekaj, aż hello nowego wystąpienia toobe gotowy i zanotuj adres presto koordynatora.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Generowanie wyników testów dla klastrów usługi HDInsight, które są uruchamiane Presto

TPC DS jest hello branżowy standard do pomiaru wydajności hello wiele systemów wsparcia decyzji, w tym systemy danych big data. Można użyć Presto danych toogenerate klastrów usługi HDInsight i ocenić, jak są porównywane z własnych danych testowych HDInsight. Aby uzyskać więcej informacji, zobacz [tutaj](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Zobacz też
* [Zainstalować i używać Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md). Odcienia, który jest interfejs użytkownika, który umożliwia łatwe toocreate, uruchom w sieci web i Zapisz zadań Pig i Hive, jak również jako Przeglądaj hello domyślny magazyn dla klastra usługi HDInsight.

* [Zainstaluj Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md). Użyj tooinstall dostosowywania klastra, który Giraph na platformie Hadoop w HDInsight clusters. Giraph pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.

* [Zainstaluj Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md). Użyj tooinstall dostosowywania klastra, który Solr na platformie Hadoop w HDInsight clusters. Solr umożliwia operacji wyszukiwania zaawansowanego tooperform na przechowywanych danych.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
