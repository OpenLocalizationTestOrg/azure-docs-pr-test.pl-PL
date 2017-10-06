---
title: "aaaInstall Jupyter lokalnie & połączenia klastra Spark w usłudze HDInsight Azure tooan | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak notesu Jupyter tooinstall lokalnie na komputerze i podłącz go tooan klastra Apache Spark w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Zainstaluj notesu Jupyter na komputerze i połącz tooApache Spark w usłudze HDInsight

W tym artykule dowiesz się, jak notesu Jupyter tooinstall, z hello PySpark niestandardowych (w przypadku języka Python) i jądra Spark (na języku Scala) z Spark magic i Połącz z klastrem usługi HDInsight tooan notesu hello. Może istnieć wiele przyczyn tooinstall Jupyter na komputerze lokalnym i mogą być również pewne wyzwania. Aby uzyskać więcej informacji, zobacz sekcję hello [Dlaczego należy zainstalować oprogramowania Jupyter na tym komputerze](#why-should-i-install-jupyter-on-my-computer) na końcu hello w tym artykule.

Istnieją trzy kroki klucza instalowania Jupyter i hello Spark magic na tym komputerze.

* Zainstaluj notesu Jupyter
* Instalowanie hello PySpark i jądra Spark przy użyciu hello Spark magic
* Skonfiguruj tooaccess magic Spark klastra Spark w usłudze HDInsight

Aby uzyskać więcej informacji o niestandardowych jądra hello i magic Spark hello dostępne dla notesu Jupyter w klastrze z klastrem usługi HDInsight, zobacz [jądra dostępne dla notesu Jupyter klastrze Apache Spark w systemie Linux klastrów HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Wymagania wstępne
Hello wymagania wstępne wymienione w tym miejscu nie dotyczą instalowania Jupyter. Są to łączącego hello Jupyter notebook tooan HDInsight klastra po zainstalowaniu hello notesu.

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Zainstaluj na tym komputerze notesu Jupyter

Python należy zainstalować przed zainstalowaniem notesów Jupyter. Zarówno Python i Jupyter są dostępne jako część hello [Anaconda dystrybucji](https://www.continuum.io/downloads). Po zainstalowaniu Anaconda, należy zainstalować dystrybucji języka Python. Po zainstalowaniu Anaconda, możesz dodać hello Jupyter instalacji za pomocą odpowiednich poleceń.

1. Pobierz hello [Instalator Anaconda](https://www.continuum.io/downloads) dla platformy i hello uruchom Instalatora. Podczas uruchomiony Kreator instalacji hello upewnij się, że wybierz zmiennej PATH tooyour Anaconda tooadd hello opcji.
2. Uruchom następujące polecenie tooinstall Jupyter hello.

        conda install jupyter

    Aby uzyskać więcej informacji na temat instalowania Jupyter, zobacz [Jupyter instalowanie przy użyciu Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).

## <a name="install-hello-kernels-and-spark-magic"></a>Zainstaluj jądra hello i Spark magic

Aby uzyskać instrukcje dotyczące sposobu tooinstall hello Spark magic, hello PySpark i jądra Spark, wykonaj te instrukcje instalacji hello hello [dokumentacji sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) w witrynie GitHub. Hello pierwszy krok w dokumentacji magic Spark hello prośba tooinstall Spark magic. Zastąp hello następujące polecenia, w zależności od wersji hello hello klastra usługi HDInsight, którą będzie łączyć się tym pierwszym etapem hello łącza. Po wykonaniu tej wykonaj pozostałe kroki opisane w dokumentacji magic Spark hello hello. Jeśli chcesz tooinstall hello różnych jądra, należy wykonać krok 3 w hello sekcji instrukcje instalacji magic Spark.

* W przypadku klastrów v3.4 należy zainstalować sparkmagic 0.2.3, wykonując`pip install sparkmagic==0.2.3`

* W przypadku klastrów w wersji 3.5 i v3.6 należy zainstalować sparkmagic 0.11.2, wykonując`pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Konfigurowanie klastra Spark tooHDInsight magic tooconnect Spark

W tej sekcji skonfigurujesz hello magic Spark, zainstalowanej wcześniejszej tooconnect tooan klastra Apache Spark musi już utworzone w usłudze Azure HDInsight.

1. Hello informacje o konfiguracji Jupyter zazwyczaj znajduje się w katalogu macierzystego hello użytkowników. toolocate katalogu macierzystego na dowolnej platformie systemu operacyjnego hello wpisz następujące polecenia.

    Uruchom powłokę Python hello. W oknie polecenia wpisz następujące hello:

        python

    Na hello powłoki Python wprowadź następujące polecenie toofind poza katalogiem macierzystym hello hello.

        import os
        print(os.path.expanduser('~'))

2. Przejdź do katalogu macierzystego toohello i Utwórz folder o nazwie **.sparkmagic** Jeśli jeszcze nie istnieje.
3. W folderze hello, Utwórz plik o nazwie **config.json** i Dodaj powitania po fragment kodu JSON wewnątrz niej.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. SUBSTITUTE **{USERNAME}**, **{CLUSTERDNSNAME}**, i **{BASE64ENCODEDPASSWORD}** z odpowiednie wartości. Liczba narzędzia w ulubionych języka programowania lub zaszyfrowanych haseł online toogenerate base64 służy do rzeczywistego hasła.

5. Konfigurowanie ustawień praw pulsu hello w `config.json`. Należy dodać te ustawienia na powitania sam poziom jako hello `kernel_python_credentials` i `kernel_scala_credentials` wstawki programu dodane wcześniej. Na przykład, w jaki sposób i gdzie tooadd hello ustawienia pulsu, zobacz [config.json próbki](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Aby uzyskać `sparkmagic 0.2.3` (klastrów v3.4), obejmują:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Aby uzyskać `sparkmagic 0.11.2` (klastrów w wersji 3.5 i v3.6), obejmują:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Tooensure nie przedostają sesji są wysyłane impulsy. Gdy komputer przestanie toosleep lub jest wyłączony, pulsu hello nie są wysyłane, co w hello sesji jest wyczyszczone. V3.4 klastrów, w razie potrzeby toodisable to zachowanie można ustawić hello Livy config `livy.server.interactive.heartbeat.timeout` zbyt`0` z hello interfejsu użytkownika narzędzia Ambari. Dla klastrów w wersji 3.5 Jeśli konfiguracja hello 3.5 powyżej, nie należy ustawiać hello sesji nie zostaną usunięte.

6. Uruchom Jupyter. Następujące polecenie w wierszu polecenia hello hello użycia.

        jupyter notebook

7. Sprawdź, czy możesz połączyć toohello klastra za pomocą notesu Jupyter hello i czy za pomocą magic Spark hello dostępne hello jądra. Wykonaj następujące kroki hello.

    a. Utwórz nowy notes. W prawym górnym rogu powitania kliknij **nowy**. Powinny pojawić się hello domyślnego jądra **Python2** i Witaj dwie nowe jądra, których można zainstalować **PySpark** i **Spark**. Kliknij przycisk **PySpark**.

    ![Jądra w notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "jądra w notesu Jupyter")

    b. Uruchom hello następującego fragmentu kodu.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Czy można pomyślnie pobrać dane wyjściowe hello, jest testowany z klastrem usługi HDInsight toohello połączenia.

    >[!TIP]
    >Jeśli chcesz tooupdate hello notesu konfiguracji tooconnect tooa innego klastra należy zaktualizować hello config.json hello nowy zestaw wartości, jak pokazano w kroku 3 powyżej.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Dlaczego Instalacja oprogramowania Jupyter na komputerze?
Może istnieć wiele przyczyn, dlaczego może być tooinstall Jupyter na komputerze, a następnie podłącz je tooa Spark klastra w usłudze HDInsight.

* Mimo że notesów Jupyter są już dostępne na powitania klastra Spark w usłudze Azure HDInsight, zainstalowanie Jupyter na komputerze zapewnia hello toocreate opcji notesy lokalnie, przetestować aplikację na klastrze uruchomione, a następnie przekaż hello notesów toohello klastra. tooupload hello notesów toohello klastra możesz albo przekazać je za pomocą notesu Jupyter hello, w którym jest uruchomiona lub hello klastra lub zapisać je toohello /HdiNotebooks folderu hello konta magazynu skojarzone z klastrem hello. Aby uzyskać więcej informacji dotyczących sposobu przechowywania notesów w klastrze hello, zobacz [notesów Jupyter przechowywania](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Z notesów hello dostępne lokalnie, możesz połączyć toodifferent klastry Spark oparty na wymagań aplikacji.
* Można użyć tooimplement GitHub systemu kontroli źródła i kontroli wersji dla notebooków hello. Może także zawierać środowisku współpracy, gdy wielu użytkowników może współpracować z hello sam notesu.
* Możesz pracować z notesów lokalnie nawet bez klastra. Wystarczy tootest klastra notesy względem, nie toomanually zarządzać notesy lub środowisko deweloperskie.
* Go może być łatwiejsze tooconfigure środowiska deweloperskiego lokalnego niż tooconfigure hello Jupyter instalacji na powitania klastra.  Można korzystać z całego oprogramowania hello zainstalowane lokalnie bez konfigurowania co najmniej jeden klaster zdalnego.

> [!WARNING]
> Za pomocą Jupyter zainstalowany na komputerze lokalnym, wielu użytkowników można uruchomić hello tego samego notesu na powitania Spark tego samego klastra na powitania tym samym czasie. W takiej sytuacji wiele sesji Livy są tworzone. Jeśli wystąpiły problemu i chcesz toodebug, że będzie on tootrack złożonych zadań, w którym sesja programu Livy należy toowhich użytkownika.
>
>

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
