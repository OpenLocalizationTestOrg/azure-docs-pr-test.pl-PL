---
title: "aaaInstall i używać Giraph w usłudze HDInsight (Hadoop) - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Giraph na HDInsight opartych na systemie Linux klastrów za pomocą akcji skryptu. Akcje skryptu zezwalaj klastrowi hello toocustomize podczas tworzenia, zmieniając konfigurację klastra lub instalowania usług i narzędzi."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Zainstaluj Giraph w klastrach HDInsight Hadoop i użyj Giraph tooprocess dużych wykresów

Dowiedz się, jak tooinstall Apache Giraph w klastrze usługi HDInsight. Hello funkcji Akcja skryptu HDInsight umożliwia toocustomize klastra przez uruchomienie skryptu bash. Skrypty można klastrów toocustomize używane podczas i po utworzeniu klastra.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="whatis"></a>Co to jest Giraph

[Apache Giraph](http://giraph.apache.org/) pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight. Wykresy modelu relacje między obiektami. Na przykład hello połączeń między routerami w dużych sieci, takich jak hello Internet lub relacje między osób w sieciach społecznościowych. Wykres przetwarzania pozwala tooreason o hello relacje między obiektami na wykresie, takich jak:

* Identyfikuje potencjalne znajomych oparte na bieżącej relacji.

* Identyfikowanie hello najkrótszy trasy między dwoma komputerami w sieci.

* Obliczanie rangę strony hello stron sieci Web.

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane - Microsoft Support pomaga tooisolate i rozwiązać problemy toothese powiązane składniki.
>
> Niestandardowe składniki, takie jak Giraph, odbierania toohelp uzasadnione ekonomicznie Obsługa toofurther należy rozwiązać problem hello. Microsoft Support może być możliwe tooresolving hello problem. Jeśli nie, należy zapoznać się z Wspólnot typu open source wykryto głębokie doświadczenia z tej technologii. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>Jakie skrypt hello wykonuje

Ten skrypt wykonuje hello następujące akcje:

* Instaluje Giraph zbyt`/usr/hdp/current/giraph`

* Witaj kopie `giraph-examples.jar` pliku magazynu toodefault (WASB) dla klastra:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Zainstaluj Giraph za pomocą akcji skryptu

Przykładowy skrypt tooinstall Giraph w klastrze usługi HDInsight jest dostępna w hello w następującej lokalizacji:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Ta sekcja zawiera instrukcje jak toouse hello przykładowy skrypt podczas tworzenia klastra hello za pomocą hello portalu Azure.

> [!NOTE]
> Akcja skryptu można zastosować za pomocą jednej z następujących metod hello:
> * Azure PowerShell
> * Witaj wiersza polecenia platformy Azure
> * Witaj zestawu .NET SDK usługi HDInsight
> * Szablony usługi Azure Resource Manager
> 
> Można także zastosować tooalready akcji skryptu działające klastry. Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

1. Rozpocznij tworzenie klastra przy użyciu kroków hello [klastrów usługi HDInsight opartych na tworzenie Linux](hdinsight-hadoop-create-linux-clusters-portal.md), kroków tworzenia.

2. Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **akcji skryptu**i podaj hello następujących informacji:

   * **Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.

   * **Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**: Sprawdź tego wpisu

   * **Proces ROBOCZY**: ten wpis należy pozostawić niezaznaczone

   * **DOZORCY**: ten wpis należy pozostawić niezaznaczone

   * **Parametry**: pozostaw to pole puste

3. U dołu hello hello **akcji skryptu**, użyj hello **wybierz** przycisk toosave hello konfiguracji. Na koniec użyj hello **wybierz** u dołu hello hello **konfiguracji opcjonalnej** bloku toosave hello konfiguracji opcjonalnej informacji.

4. Kontynuuj tworzenie klastra hello zgodnie z opisem w [klastrów usługi HDInsight opartych na tworzenie Linux](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Jak używać Giraph w usłudze HDInsight?

Po utworzeniu klastra hello Użyj hello następujące kroki toorun SimpleShortestPathsComputation przykład Witaj dołączonego Giraph. W tym przykładzie użyto hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementacji do znajdowania hello najkrótszy ścieżki między obiektami na wykresie.

1. Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj hello następujące polecenie toocreate plik o nazwie **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Użyj hello następującego tekstu jako hello zawartość tego pliku:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Te dane w tym artykule opisano relacje między obiektami w ukierunkowanego wykresu, używając formatu hello `[source_id, source_value,[[dest_id], [edge_value],...]]`. Każdy wiersz zawiera relację między `source_id` obiektu i co najmniej jeden `dest_id` obiektów. Witaj `edge_value` można traktować jako siły hello lub odległość hello połączenie między `source_id` i `dest\_id`.

    Rysowane, i przy użyciu hello wartości (lub wagi) jako hello odległość między obiektami, hello danych może wyglądać powitania po diagramu:

    ![tiny_graph.txt rysowane jako okręgi wiersze z różnymi odległość między](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. toosave hello pliku, użyj **Ctrl + X**, następnie **Y**, a na końcu **Enter** nazwę pliku hello tooaccept.

4. Użyj powitania po toostore hello danych na podstawowy magazyn dla klastra usługi HDInsight:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Uruchom przykład SimpleShortestPathsComputation Witaj przy użyciu hello następujące polecenie:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    Parametry Hello używane w tym poleceniu są opisane w hello w poniższej tabeli:

   | Parametr | Wyniki działania |
   | --- | --- |
   | `jar` |Witaj plik jar zawierający hello przykłady. |
   | `org.apache.giraph.GiraphRunner` |Klasa Hello używana toostart hello przykłady. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |przykład Witaj, który jest używany. W tym przykładzie oblicza hello najkrótszy ścieżki między ID 1 i innych identyfikatorów w grafie hello. |
   | `-ca mapred.job.tracker` |Witaj headnode hello klastra. |
   | `-vif` |toouse format wejściowy Hello hello danych wejściowych. |
   | `-vip` |plik danych wejściowych Hello. |
   | `-vof` |format danych wyjściowych Hello. W tym przykładzie, Identyfikatora i wartości w postaci zwykłego tekstu. |
   | `-op` |Witaj lokalizacji wyjściowej. |
   | `-w 2` |Liczba Hello toouse pracowników. W tym przykładzie 2. |

    Aby uzyskać więcej informacji na temat tych i innych parametrów używane z próbek Giraph, zobacz hello [szybkiego startu Giraph](http://giraph.apache.org/quick_start.html).

6. Po zakończeniu zadania hello hello wyniki są przechowywane w hello **/example/out/shotestpaths** katalogu. Hello nazwy pliku wyjściowego rozpoczynać się od **części-m -** i kończyć liczbę określającą hello pierwszy, drugi, itp. plik. Użyj następujących danych wyjściowych polecenia tooview hello hello:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    dane wyjściowe Hello powinna zostać wyświetlona podobne toohello następującego tekstu:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    przykład Witaj SimpleShortestPathComputation jest zakodowany toostart z obiektem ID 1 i Znajdź hello najkrótszy ścieżki tooother obiektów. dane wyjściowe Hello jest w formacie hello `destination_id` i `distance`. Witaj `distance` jest wartość hello (lub wagi) krawędzi hello pokonać między obiektu ID 1 i identyfikatora hello docelowej.

    Wizualizacja danych, można sprawdzić wyniki hello za podróży hello najkrótszy ścieżek między 1 Identyfikatora i wszystkie inne obiekty. Najkrótszy ścieżki Hello między ID 1 i 4 identyfikator wynosi 5. Ta wartość jest hello całkowita odległość między <span style="color:orange">ID 1 i 3</span>, a następnie <span style="color:red">identyfikator 3 i 4</span>.

    ![Rysowanie obiektów jako kółka za pomocą najmniejszej ścieżek między](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Następne kroki

* [Zainstalować i używać Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md).

* [Zainstaluj Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md).
