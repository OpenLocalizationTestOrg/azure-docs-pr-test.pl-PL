---
title: "klastry aaaKernels dla notesu Jupyter na Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello jądra PySpark, PySpark3 i Spark dla notesu Jupyter dostępne z klastrami Spark w usłudze Azure HDInsight."
keywords: notesu jupyter na spark, jupyter spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Jądra dla notesu Jupyter w klastrze Spark w usłudze Azure HDInsight 

Klastry HDInsight Spark zapewniają jądra, których można używać do testowania aplikacji z notesu Jupyter hello na Spark. Jądra to program, który uruchamia i interpretuje kodu. są trzy jądra Hello:

- **PySpark** — dla aplikacji napisanych w Python2
- **PySpark3** — dla aplikacji napisanych w Python3
- **Platforma Spark** — dla aplikacji napisanych w języku Scala

W tym artykule dowiesz się, jak toouse te jądra i hello zalety korzystania z nich.

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Tworzenie notesu Jupyter w usłudze HDInsight Spark

1. Z hello [portalu Azure](https://portal.azure.com/), otwórz klastra.  Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) hello instrukcje. klaster Hello jest otwarty w nowym bloku portalu.

2. Z hello **szybkie linki** kliknij **klastra pulpity nawigacyjne** tooopen hello **klastra pulpity nawigacyjne** bloku.  Jeśli nie widzisz **szybkie linki**, kliknij przycisk **omówienie** z menu po lewej stronie powitania na powitania bloku.

    ![Notesu Jupyter na Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "notesu Jupyter na Spark") 

3. Kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.
   
   > [!NOTE]
   > Można również przejść hello notesu Jupyter w klastrze Spark przy hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Kliknij przycisk **nowy**, a następnie kliknij opcję **Pyspark**, **PySpark3**, lub **Spark** toocreate notesu. Użyj hello jądra Spark Scala aplikacji jądra PySpark Python2 aplikacji i PySpark3 jądra dla Python3 aplikacji.
   
    ![Jądra dla notesu Jupyter na Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "jądra dla notesu Jupyter na Spark") 

4. Otwiera notes z hello jądra, które wybrano.

## <a name="benefits-of-using-hello-kernels"></a>Zalety używania hello jądra

Poniżej przedstawiono kilka korzyści wynikające ze stosowania nowych jądra hello z notesu Jupyter w klastrach Spark HDInsight.

- **Ustawienie wstępne kontekstów**. Z **PySpark**, **PySpark3**, lub hello **Spark** jądra, nie trzeba konteksty Spark i Hive hello tooset jawnie przed rozpoczęciem pracy z aplikacjami. Są one dostępne domyślnie. Konteksty te są:
   
   * **sc** — Spark kontekstu
   * **Element sqlContext** — dla kontekstu gałęzi

    Nie masz, instrukcje toorun, takie jak powitania po kontekstów hello tooset:

        sc = element sqlContext SparkContext('yarn-client') = HiveContext(sc)

    Zamiast tego możesz bezpośrednio użyć hello ustawienia wstępnego kontekstów w aplikacji.

- **Komórki poleceń magicznych**. Witaj jądra PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z `%%` (na przykład `%%MAGIC` <args>). polecenie magic Hello musi być hello pierwsze słowo w komórce kodu i mogą zostać w wielu wierszach zawartości. Hello magic word powinna być hello pierwsze słowo w komórce hello. Dodawanie czegokolwiek przed magic hello, nawet komentarzy powoduje błąd.     Aby uzyskać więcej informacji dotyczących poleceń magicznych, zobacz [tutaj](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Witaj poniższej tabeli wymieniono hello różnych poleceń magicznych dostępnych za pośrednictwem hello jądra.

   | Magiczna | Przykład | Opis |
   | --- | --- | --- |
   | Pomoc |`%%help` |Generuje spis wszystkich hello dostępnych poleceń magicznych przykład i opis |
   | Informacje o |`%%info` |Dane wyjściowe informacji o sesji dla punktu końcowego hello bieżącego Livy |
   | Konfigurowanie |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Konfiguruje parametry hello w celu utworzenia sesji. Witaj flagi force (-f) jest wymagane, jeśli sesja została już utworzona, co zapewnia sesji hello jest porzucenia i ponownego utworzenia. Przyjrzyj się [/sessions POST Livy w treści żądania](https://github.com/cloudera/livy#request-body) listę prawidłowych parametrów. Parametry muszą być przekazywane w postaci ciągu JSON i musi być w następnym wierszu powitania po hello magic, jak pokazano w kolumnie przykład hello. |
   | SQL |`%%sql -o <variable name>`<br> `SHOW TABLES` |Wykonuje zapytanie Hive względem element sqlContext hello. Jeśli hello `-o` parametr jest przekazywany, w hello jest trwały hello wynik zapytania hello %% lokalny kontekst Python jako [Pandas](http://pandas.pydata.org/) dataframe. |
   | lokalne |`%%local`<br>`a=1` |Cały kod hello w kolejnych wierszy jest wykonywana lokalnie. Kod musi być prawidłowym kodem Python2 nawet niezależnie od jądra hello, którego używasz. Tak, nawet w przypadku wybrania **PySpark3** lub **Spark** jądra podczas tworzenia notesu hello, jeśli używasz hello `%%local` magic w komórce, tej komórki musi mieć tylko prawidłowy kod Python2... |
   | dzienniki |`%%logs` |Dane wyjściowe hello dzienniki dla bieżącej sesji programu Livy hello. |
   | Usuń |`%%delete -f -s <session number>` |Usuwa określonej sesji hello bieżący punkt końcowy programu Livy. Należy pamiętać, że nie można usunąć sesji hello inicjowane dla jądra hello, sama. |
   | Czyszczenie |`%%cleanup -f` |Usuwa wszystkie sesje hello hello bieżącego Livy punktu końcowego, łącznie z sesji tego notesu. Wymuś Hello flagi -f jest obowiązkowe. |

   > [!NOTE]
   > Ponadto poleceń magicznych toohello dodane przez hello jądra PySpark, można również użyć hello [wbudowanych IPython poleceń magicznych](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), takie jak `%%sh`. Można użyć hello `%%sh` Magiczna toorun skryptów i blok kodu na powitania headnode klastra.
   >
   >
2. **Automatyczna wizualizacja**. Witaj **Pyspark** jądra automatycznie wizualizuje hello dane wyjściowe zapytań Hive i SQL. Można wybrać kilka różnych typów wizualizacji, łącznie z tabeli, kołowego, wiersza, obszar, paska.

## <a name="parameters-supported-with-hello-sql-magic"></a>Parametry są obsługiwane z hello %% sql magic
Witaj `%%sql` magic obsługuje parametry, których można używać typu hello toocontrol wyjściowego, który jest wyświetlany podczas uruchamiania kwerend. Witaj w poniższej tabeli wymieniono hello danych wyjściowych.

| Parametr | Przykład | Opis |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Użyj tego parametru toopersist hello wyniku zapytania hello w hello %% lokalny kontekst Python, jako [Pandas](http://pandas.pydata.org/) dataframe. Nazwa Hello zmiennej dataframe hello jest hello nazwę zmiennej, które określisz. |
| -q |`-q` |Użyj tego tooturn poza wizualizacjami hello komórki. Jeśli nie chcesz tooauto-wizualizacji hello zawartość komórki, a jedynie chcesz toocapture go jako dataframe, następnie użyć `-q -o <VARIABLE>`. Jeśli chcesz tooturn poza wizualizacjami bez Przechwytywanie hello wyników (na przykład do uruchomienia zapytania SQL, tak samo, jak `CREATE TABLE` instrukcji), użyj `-q` bez określania `-o` argumentu. |
| -m |`-m <METHOD>` |Gdzie **— metoda** jest **zająć** lub **próbki** (domyślnie jest **zająć**). Jeśli metoda hello jest **zająć**, jądra hello wybiera elementy z góry hello zestawu danych wyników hello określony przez maksymalna liczba wierszy (opisane w dalszej części tej tabeli). Jeśli metoda hello jest **próbki**, jądra hello losowo przykłady elementy hello zestawu danych zgodnie z zbyt`-r` parametru opisane dalej w tej tabeli. |
| -r |`-r <FRACTION>` |W tym miejscu **UŁAMEK** jest liczba zmiennoprzecinkowa od 0,0 do 1,0. Jeśli hello przykładowej metody dla zapytania SQL hello jest `sample`, a następnie jądra hello losowo przykłady hello określona część hello elementy hello zestawu wyników dla należy. Na przykład, jeśli uruchomienie zapytania SQL z argumentami hello `-m sample -r 0.01`, następnie losowo próbkowanych 1% hello wynik wierszy. |
| -n |`-n <MAXROWS>` |**Maksymalna liczba wierszy** jest wartością całkowitą. jądra Hello ogranicza hello liczby wierszy danych wyjściowych za**maksymalna liczba wierszy**. Jeśli **maksymalna liczba wierszy** jest liczbą ujemną, takich jak **-1**, a następnie hello liczbę wierszy w zestawie wyników hello nie jest ograniczona. |

**Przykład:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

Instrukcja Hello powyżej hello następujące:

* Wybiera wszystkie rekordy z **hivesampletable**.
* Ponieważ używamy - q, wyłącza automatyczne wizualizacji.
* Ponieważ używamy `-m sample -r 0.1 -n 500` losowo przykłady 10% hello wierszy w hello hivesampletable i limity hello rozmiar hello wynik zestaw too500 wierszy.
* Ponadto ponieważ użyliśmy `-o query2` zapisuje dane wyjściowe hello do dataframe, nazywany **kwerenda2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Zagadnienia dotyczące podczas korzystania z nowego jądra hello

Niezależnie od jądra używasz, pozostawiając notesów hello systemem wykorzystuje zasoby klastra hello.  Z tych jądra ponieważ kontekstów hello są zdefiniowane, po prostu Kończenie notesów hello nie kill hello kontekstu i dlatego zasobów klastra hello kontynuować toobe w użyciu. Dobrym rozwiązaniem jest toouse hello **zamknąć i zatrzymuje** opcji z notesu hello **pliku** menu po zakończeniu korzystania notesie hello kasuje hello kontekstu i następnie zamyka hello notesu.     

## <a name="show-me-some-examples"></a>Pokaż niektóre przykłady

Po otwarciu notesu Jupyter wyświetlany dwa foldery dostępna na poziomie głównym hello.

* Witaj **PySpark** znajduje się w nim notesów próbki tego hello Użyj nowego **Python** jądra.
* Witaj **Scala** znajduje się w nim notesów próbki tego hello Użyj nowego **Spark** jądra.

Możesz otworzyć hello **00 — [odczytu w pierwszej kolejności] funkcje jądra Magic Spark** notesu z hello **PySpark** lub **Spark** toolearn folderu o hello różnych poleceń magicznych dostępnych. Można również użyć hello innych dostępnych w ramach hello dwa foldery toolearn notesów przykładowy sposób różnych scenariuszy tooachieve za pomocą notesów Jupyter z klastrami HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>Gdzie są przechowywane notesów hello?

Notesów Jupyter są zapisywane toohello konta magazynu skojarzone z klastrem hello w obszarze hello **/HdiNotebooks** folderu.  Notesów, pliki tekstowe i folderów tworzonych z wewnątrz Jupyter są dostępne z hello konta magazynu.  Na przykład, jeśli używasz Jupyter toocreate folder **MójFolder** i notebook **myfolder/mynotebook.ipynb**, można uzyskać dostępu do tego notesu w `/HdiNotebooks/myfolder/mynotebook.ipynb` w ramach konta magazynu hello.  odwrotnej Hello jest również ma wartość true, oznacza to, bezpośrednio tooyour magazynu konta w przypadku przekazywania Notes `/HdiNotebooks/mynotebook1.ipynb`, notesu hello jest także widoczny Jupyter.  Notesów pozostają na koncie magazynu hello nawet po usunięciu hello klastra.

sposób Hello notesów zapisywania toohello konta magazynu jest zgodny z systemem plików HDFS. Tak, jeśli plik należy SSH do klastra hello, których można używać polecenia zarządzania, pokazane na powitania po fragment kodu:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


W przypadku, gdy występują problemy dotyczące uzyskiwania dostępu do konta magazynu hello hello klastra, notesy hello zostały także zapisane na powitania headnode `/var/lib/jupyter`.

## <a name="supported-browser"></a>Obsługiwana przeglądarka

Notesów Jupyter w klastrze Spark w usłudze HDInsight są obsługiwane tylko w Google Chrome.

## <a name="feedback"></a>Opinia
nowe jądra Hello znajdują się w rozwijającymi etap i będzie dojrzałych wraz z upływem czasu. Może to również oznaczać, że interfejsy API można zmienić, ponieważ te jądra dla dorosłych. Czy Dziękujemy za opinię, czy masz podczas korzystania z tych nowych jądra. Jest to przydatne w tworzeniu hello ostatecznej wersji programu te jądra. Możesz pozostawić komentarzy/opinii w obszarze hello **komentarze** sekcji hello dolnej części tego artykułu.

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
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
