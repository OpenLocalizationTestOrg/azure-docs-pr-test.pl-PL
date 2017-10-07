---
title: "Przykłady aaaStorm starter Apache Storm w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak analizy danych big data toodo i przetwarzania danych w czasie rzeczywistym za pomocą platformy Apache Storm i hello przykłady z projektu storm starter w usłudze HDInsight."
keywords: "projekt Storm Starter, przykład z platformy Apache Storm"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Wprowadzenie do Apache Storm w usłudze HDInsight przy użyciu hello storm-starter przykłady

Dowiedz się, jak toouse Apache Storm w usłudze HDInsight przy użyciu hello przykłady z projektu storm starter.

Apache Storm to skalowalny, odporny na błędy, rozproszony system obliczeniowy działający w czasie rzeczywistym do przetwarzania strumieni danych. Dzięki platformie Storm w usłudze Azure HDInsight można utworzyć oparty na chmurze klaster Storm do wykonywania analizy danych big data w czasie rzeczywistym.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Znajomość protokołów SSH i SCP**. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Tworzenie klastra Storm

Użyj hello następujące kroki toocreate platformy Storm w klastrze usługi HDInsight:

1. Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy**, **analizy i analiza**, a następnie wybierz **HDInsight**.

    ![Tworzenie klastra usługi HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. Z hello **podstawy** bloku, wprowadź hello następujących informacji:

    * **Nazwa klastra**: Nazwa hello hello klastra usługi HDInsight.
    * **Subskrypcja**: Wybierz hello toouse subskrypcji.
    * **Nazwa użytkownika logowania klastra** i **hasło logowania klastra**: hello logowania podczas uzyskiwania dostępu do klastra hello za pośrednictwem protokołu HTTPS. Korzystania z tych usług tooaccess poświadczeń, takich jak hello Interfejsu sieci Web Ambari lub interfejsu API REST.
    * **Secure Shell (SSH) username**: hello logowania używany podczas uzyskiwania dostępu do klastra hello za pomocą protokołu SSH. Domyślnie jest hello takie samo jak hasło logowania klastra hello hello hasła.
    * **Grupa zasobów**: hello klastra hello toocreate grupy zasobów w.
    * **Lokalizacja**: hello regionu Azure toocreate hello klastra w.

    ![Wybieranie subskrypcji](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Wybierz **typ klastra**, a następnie hello ustaw następujące wartości na powitania **konfiguracji klastra** bloku:

    * **Typ klastra**: Storm

    * **System operacyjny**: Linux

    * **Wersja**: Storm 1.1.0 (HDI 3.6)

    * **Warstwa klastra**: Standardowa

    Na koniec użyj hello **wybierz** przycisk toosave ustawienia.

    ![Wybieranie typu klastra](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Po wybraniu typu klastra hello, użyj hello __wybierz__ tooset hello klastra typ przycisku. Następnie użyj hello __dalej__ przycisk toofinish podstawową konfigurację.

5. Z hello **magazynu** bloku, wybierz lub Utwórz konto magazynu. Hello czynności w tym dokumencie pozostaw hello innych pól w tym bloku na powitania wartości domyślne. Użyj hello __dalej__ przycisk toosave magazynu konfiguracji.

    ![Ustaw hello ustawienia konta magazynu dla usługi HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. Z hello **Podsumowanie** bloku, Przejrzyj konfigurację hello hello klastra. Użyj hello __Edytuj__ łączy toochange wszystkie ustawienia, które są nieprawidłowe. Na koniec użyj the__Create__ przycisk toocreate hello klastra.

    ![Podsumowanie konfiguracji klastra](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Może potrwać too20 minut toocreate hello klastra.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Uruchamianie przykładu z projektu Storm Starter w usłudze HDInsight

1. Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Jeśli użyto toosecure hasło konta użytkownika SSH, to zostanie wyświetlony monit o tooenter go. Jeśli używasz klucza publicznego, należy posłużyć hello `-i` toospecify parametru hello odpowiedniego klucza prywatnego. Na przykład `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj następującego polecenia toostart przykładową topologię hello:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > W poprzednich wersjach usługi HDInsight, nazwa klasy hello topologii hello jest `storm.starter.WordCountTopology` zamiast `org.apache.storm.starter.WordCountTopology`.

    To polecenie uruchamia hello przykładową topologię WordCount w klastrze hello o przyjaznej nazwie "wordcount". Losowo generuje on zdań i hello liczby wystąpień poszczególnych wyrazów w zdaniach hello.

    > [!NOTE]
    > Podczas przesyłania własnego klastra toohello topologie, należy najpierw skopiować plik jar hello zawierający hello klastra przed użyciem hello `storm` polecenia. Użyj hello `scp` pliku hello toocopy polecenia. Na przykład: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > przykład Witaj WordCount i inne przykłady storm-starter znajdują się już w klastrze na `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Jeśli interesuje Cię wyświetlanie źródła hello hello storm-starter przykłady, można znaleźć kod hello na [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Ten link dotyczy platformy Storm 1.1.x, która jest dostarczana z usługą HDInsight 3.6. W przypadku innych wersji systemu Storm, użyj hello __gałęzi__ przycisk u góry hello tooselect strony hello z innej wersji systemu Storm.

## <a name="monitor-hello-topology"></a>Monitor hello topologii

Hello interfejsu użytkownika platformy Storm udostępnia interfejs sieci web do pracy z uruchomionymi topologiami i znajduje się w klastrze usługi HDInsight.

Użyj następujących topologii hello toomonitor czynności przy użyciu interfejsu użytkownika platformy Storm hello hello:

1. Witaj toodisplay interfejsu użytkownika platformy Storm, otwórz toohttps://CLUSTERNAME.azurehdinsight.net/stormui przeglądarki sieci web. Zastąp **CLUSTERNAME** o nazwie hello klastra.

    > [!NOTE]
    > Jeśli pojawi się monit tooprovide nazwy użytkownika i hasła, wprowadź hello administratora klastra (admin) i hasło użyte podczas tworzenia klastra hello.

2. W obszarze **podsumowanie topologii**, wybierz pozycję hello **wordcount** wpisu w hello **nazwa** kolumny. Informacje o topologii hello są wyświetlane.

    ![Pulpit nawigacyjny platformy Storm z informacjami o topologii przykładu z projektu Storm Starter o nazwie WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Ta strona zawiera hello następujących informacji:

    * **Statystyka topologii** — podstawowe informacje na temat wydajności topologii hello podzielone na okna czasowe.

        > [!NOTE]
        > Wybór określonego okna zmiany hello czas okna czasowego informacji wyświetlanych w innych sekcjach strony hello.

    * **Spouts** — podstawowe informacje o elementach spout, łącznie hello ostatnim błędem zwróconym przez poszczególne elementy spout.

    * **Bolts** (Elementy bolt) — podstawowe informacje o elementach bolt.

    * **Topologia konfiguracji** — szczegółowe informacje o konfiguracji topologii hello.

    Ta strona zawiera również akcje, które można podjąć w topologii hello:

    * **Activate** (Aktywuj) — wznowienie przetwarzania dezaktywowanej topologii.

    * **Deactivate** (Dezaktywuj) — wstrzymanie uruchomionej topologii.

    * **Rebalance** — można dostosować równoległość hello hello topologii. Po zmianie hello liczby węzłów w klastrze hello, należy przeprowadzić ponowne równoważenie uruchomionych topologii. Ponowne równoważenie można dostosować równoległość toocompensate hello zwiększonej/zmniejszonej liczby węzłów w klastrze hello. Aby uzyskać więcej informacji, zobacz [opis hello równoległości topologii Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **Kasowanie** -kończy topologii Storm po hello określony limit czasu.

3. Na tej stronie, wybierz pozycję z hello **Spouts** lub **Bolts** sekcji. Zostaną wyświetlone informacje o hello wybranego składnika.

    ![Pulpit nawigacyjny Storm z informacjami o wybranych składnikach.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Ta strona wyświetla hello następujących informacji:

    * **Spout/Bolt stats** — podstawowe informacje na temat wydajności składników hello podzielone na okna czasowe.

        > [!NOTE]
        > Wybór określonego okna zmiany hello czas okna czasowego informacji wyświetlanych w innych sekcjach strony hello.

    * **Wprowadź statystykę** (tylko dla elementów bolt) — informacje na temat składników, które tworzą dane używane przez hello bolt.

    * **Output stats** (Statystyki danych wyjściowych) — informacje na temat danych emitowanych przez dany element bolt.

    * **Executors** (Wykonawcy) — informacje dotyczące wystąpień danego składnika.

    * **Errors** (Błędy) — błędy generowane przez dany składnik.

4. Podczas wyświetlania szczegółowych informacji hello spout lub bolt, zaznacz wpis hello **portu** kolumny w hello **modułów** sekcji Szczegóły tooview dla określonego wystąpienia hello składnika.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    W tym przykładzie hello word **siedmiu** wystąpił 1493957 razy. Ta liczba jest ile razy napotkano word powitania od momentu uruchomienia tej topologii.

## <a name="stop-hello-topology"></a>Zatrzymywanie topologii hello

Zwraca toohello **podsumowanie topologii** dla topologii WordCount hello, a następnie wybierz hello **Kill** przycisk od hello **akcje topologii** sekcji. Po wyświetleniu monitu wprowadź 10 hello toowait sekund przed zatrzymaniem topologii hello. Po upływie okresu czasu hello hello topologia nie będzie już wyświetlany podczas odwiedzania hello **interfejsu użytkownika platformy Storm** sekcji hello pulpitu nawigacyjnego.

## <a name="delete-hello-cluster"></a>Usuń klaster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

W razie problemów podczas tworzenia klastra usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Następne kroki

W tym samouczku platformy Apache Storm znasz już podstawy hello pracy z systemu Storm w usłudze HDInsight. Następnie Dowiedz się, jak za[topologie oparte na opracowanie Java za pomocą programu Maven](hdinsight-storm-develop-java-topology.md).

Jeśli znasz już opracowywania topologii opartych na języku Java i chcesz toodeploy istniejących tooHDInsight topologii, zobacz [wdrażanie topologii Apache Storm w usłudze HDInsight oraz zarządzania nimi](hdinsight-storm-deploy-monitor-topology-linux.md).

Jeśli jesteś deweloperem platformy .NET, możesz tworzyć topologie C# lub hybrydowe topologie C#/Java za pomocą programu Visual Studio. Aby uzyskać więcej informacji na ten temat, zobacz [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu narzędzi Hadoop dla programu Visual Studio).

Na przykład topologie, które mogą być używane z systemu Storm w usłudze HDInsight, zobacz temat hello następujące przykłady:

* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
