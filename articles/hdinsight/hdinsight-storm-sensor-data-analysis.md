---
title: "dane czujników aaaAnalyze z systemu Apache Storm i bazy danych HBase | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooApache Storm z siecią wirtualną. Używać systemu Storm danych czujnika tooprocess HBase z Centrum zdarzeń i wizualizację go z D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Analizowanie danych czujnika z systemu Apache Storm, Centrum zdarzeń i bazy danych HBase w usłudze HDInsight (Hadoop)

Dowiedz się, jak toouse Apache Storm w dane czujników tooprocess HDInsight z Centrum zdarzeń platformy Azure. Witaj danych będzie przechowywany do bazy danych Apache HBase w usłudze HDInsight i wizualizowane za pomocą D3.js.

Szablon usługi Azure Resource Manager Hello używany w tym dokumencie przedstawiono sposób toocreate wielu zasobów platformy Azure w grupie zasobów. Szablon Hello tworzy sieci wirtualnej platformy Azure, dwa klastry usługi HDInsight (Storm oraz bazy danych HBase) i aplikacji sieci Web platformy Azure. Implementacja node.js pulpit nawigacyjny sieci web w czasie rzeczywistym jest toohello automatycznie wdrożonej aplikacji sieci web.

> [!NOTE]
> Witaj informacje w tym dokumencie i przykład, w tym dokumencie wymagają HDInsight wersji 3,6.
>
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure.
* [Node.js](http://nodejs.org/): pulpitu nawigacyjnego sieci web hello toopreview używane lokalnie na środowiska deweloperskiego.
* [Java i hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): używane topologii Storm hello toodevelop.
* [Maven](http://maven.apache.org/what-is-maven.html): używanych projektów hello toobuild i kompilacji.
* [Git](http://git-scm.com/): toodownload używane hello projektu z usługi GitHub.
* **SSH** klienta: używane tooconnect toohello opartych na systemie Linux klastrów usługi HDInsight. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Nie trzeba istniejącego klastra usługi HDInsight. kroki Hello w tym dokumencie Utwórz hello następujące zasoby:
> 
> * Sieć wirtualna platformy Azure
> * Storm w klastrze usługi HDInsight (opartych na systemie Linux dwóch węzłów procesu roboczego)
> * Baza danych HBase w klastrze usługi HDInsight (opartych na systemie Linux dwóch węzłów procesu roboczego)
> * Aplikacji sieci Web platformy Azure obsługuje hello pulpit nawigacyjny z sieci web

## <a name="architecture"></a>Architektura

![diagram architektury](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

W tym przykładzie składa się z hello następujące składniki:

* **Usługa Azure Event Hubs**: zawiera dane, które mają być zbierane z czujników.
* **STORM w usłudze HDInsight**: udostępnia w czasie rzeczywistym przetwarzania danych z Centrum zdarzeń.
* **Baza danych HBase w usłudze HDInsight**: udostępnia trwałym magazynem danych NoSQL dla danych po przetworzeniu przez Storm.
* **Usługi sieci wirtualnej Azure**: umożliwia bezpieczną komunikację między hello Storm w usłudze HDInsight i bazy danych HBase w klastrach usługi HDInsight.
  
  > [!NOTE]
  > Sieć wirtualna jest wymagany, korzystając z interfejsu API klienta Java HBase hello. Nie jest widoczne za pośrednictwem bramy publicznego hello w przypadku klastrów HBase. Instalowanie bazy danych HBase i Storm klastrów w tej samej sieci wirtualnej umożliwia hello hello klastra Storm (lub inne systemy w sieci wirtualnej hello) toodirectly dostęp do bazy danych HBase przy użyciu interfejsu API klienta.

* **Witryny sieci Web pulpitu nawigacyjnego**: przykładowy pulpit nawigacyjny, który wykresy danych w czasie rzeczywistym.
  
  * witryny sieci Web Hello jest zaimplementowany w środowisku Node.js.
  * [Użyciu biblioteki Socket.IO](http://socket.io/) jest używany w czasie rzeczywistym komunikacji między hello topologii Storm i hello witryny sieci Web.
    
    > [!NOTE]
    > Przy użyciu biblioteki Socket.io komunikacji jest szczegóły implementacji. Możesz użyć dowolnej architektury komunikacji, takie jak Websocket raw lub SignalR.

  * [D3.js](http://d3js.org/) jest używane toograph hello dane są przesyłane toohello witryny sieci Web.

> [!IMPORTANT]
> Dwa klastry są wymagane, ponieważ nie ma żadnych obsługiwana metoda toocreate jednego klastra usługi HDInsight Storm i bazy danych HBase.

Witaj topologii odczytuje dane z Centrum zdarzeń za pomocą hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) klasy i zapisuje dane do bazy danych HBase przy użyciu hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) Klasa. Komunikacja z witryny sieci Web hello odbywa się przy użyciu [client.java użyciu biblioteki socket.io](https://github.com/nkzawa/socket.io-client.java).

powitania po diagram wyjaśniono hello układ topologii hello:

![diagram topologii](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Ten diagram jest uproszczona prezentacja hello topologii. Dla każdej partycji w Centrum zdarzeń jest tworzone wystąpienie każdego składnika. Te wystąpienia są rozproszone na powitania węzłów w klastrze hello, a dane są przesyłane między nimi w następujący sposób:
> 
> * Dane z analizatora toohello spout hello jest równoważone.
> * Dane z toohello analizator hello pulpitu nawigacyjnego i HBase są grupowane według Identyfikatora urządzenia, tak, aby zawsze hello wiadomości z tym samym urządzeniu przepływ toohello tego składnika.

### <a name="topology-components"></a>Składniki topologii

* **Elementów Spout Centrum zdarzeń**: hello spout jest podana jako część systemu Apache Storm w wersji 0.10.0 lub nowszej.
  
  > [!NOTE]
  > w tym przykładzie spout Centrum zdarzeń Hello wymaga platformy Storm w klastrze usługi HDInsight w wersji 3.5 lub 3,6.

* **ParserBolt.java**: hello dane, które są emitowane przez hello spout jest nieprzetworzone dane JSON, a czasami więcej niż jedno zdarzenie jest emitowany naraz. Dany element bolt odczytuje hello danych emitowanych przez hello spout i analizuje wiadomości powitania JSON. Hello bolt następnie emituje hello danych jako spójnej kolekcji, która zawiera wiele pól.
* **DashboardBolt.java**: ten składnik pokazano, jak toouse hello użyciu biblioteki Socket.io biblioteki klienta dla programu Java toosend danych w czasie rzeczywistym toohello sieci web z pulpitu nawigacyjnego.
* **nie hbase.yaml**: hello definicji topologii używany podczas pracy w trybie lokalnym. Nie używa składników bazy danych HBase.
* **z hbase.yaml**: hello definicji topologii używany, gdy działa w klastrze hello hello topologii. Wykorzystuje ona składników bazy danych HBase.
* **dev.Properties**: hello informacji o konfiguracji dla hello spout Centrum zdarzeń, HBase bolt i składniki pulpitu nawigacyjnego.

## <a name="prepare-your-environment"></a>Przygotowywanie środowiska

Przed skorzystaniem z tego przykładu, należy utworzyć usługi Azure Event Hub, które topologii Storm hello odczytuje z.

### <a name="configure-event-hub"></a>Konfigurowanie Centrum zdarzeń

Centrum zdarzeń jest hello źródła danych w tym przykładzie. Użyj hello następujące kroki toocreate Centrum zdarzeń.

1. Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy** -> **Internetu rzeczy** -> **usługi Event Hubs**.
2. W hello **utworzyć Namespace** sekcji, wykonaj następujące zadania hello:
   
   1. Wprowadź **nazwa** hello przestrzeni nazw.
   2. Wybierz warstwę cenową. **Podstawowe** jest wystarczająca dla tego przykładu.
   3. Wybierz hello Azure **subskrypcji** toouse.
   4. Wybierz istniejącą grupę zasobów lub Utwórz nową.
   5. Wybierz hello **lokalizacji** dla hello Centrum zdarzeń.
   6. Wybierz **toodashboard numeru Pin**, a następnie kliknij przycisk **Utwórz**.

3. Po ukończeniu procesu tworzenia hello hello informacji centra zdarzeń w przestrzeni nazw jest wyświetlany. W tym miejscu, wybierz **+ Dodaj Centrum zdarzeń**. W hello **tworzenia Centrum zdarzeń** sekcji, wprowadź nazwę **sensordata**, a następnie wybierz **Utwórz**. Pozostaw hello innych pól na powitania wartości domyślne.
4. Z centrów zdarzeń hello wyświetlić obszar nazw, wybierz opcję **usługi Event Hubs**. Wybierz hello **sensordata** wpisu.
5. Witaj sensordata Centrum zdarzeń, zaznacz **zasady dostępu współużytkowanego**. Użyj hello **+ Dodaj** hello tooadd łącze następujące zasady:

    | Nazwa zasad | Oświadczenia |
    | ----- | ----- |
    | urządzenia | Send |
    | STORM | Nasłuchiwanie |

1. Zaznacz obie zasady i zanotuj hello **klucz podstawowy** wartość. Należy hello wartość dla obu zasad w przyszłości czynności.

## <a name="download-and-configure-hello-project"></a>Pobierz i skonfiguruj hello projektu

Użyj powitania po toodownload hello projektu z usługi GitHub.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Po zakończeniu wykonywania polecenia hello masz powitania po strukturę katalogów:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Ten dokument nie przechodzi w szczegółach toofull hello kodu zawarte w tym przykładzie. Jednak kod hello jest całkowicie oznaczone jako.

tooconfigure hello projektu tooread z Centrum zdarzeń, otwórz hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` plik i dodać Twojego toohello informacje o Centrum zdarzeń następujące wiersze:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Kompilowanie i testowanie lokalnie

> [!IMPORTANT]
> Lokalnie przy użyciu topologii hello wymaga działającego środowiska deweloperskiego Storm. Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) w serwisie Apache.org.

> [!WARNING]
> Jeśli używasz środowiska projektowego systemu Windows może zostać wyświetlony `java.io.IOException` podczas uruchamiania topologii hello lokalnie. Jeśli tak, przesuń w topologii hello toorunning w usłudze HDInsight.

Przed przeprowadzeniem jej testów, należy uruchomić hello pulpitu nawigacyjnego tooview hello dane wyjściowe hello topologii i generowanie toostore danych w Centrum zdarzeń.

> [!IMPORTANT]
> składnik HBase Hello Ta topologia nie jest aktywne podczas testowania lokalnie. Witaj interfejsu API języka Java dla klastra HBase hello nie są dostępne z hello zewnętrznej sieci wirtualnej platformy Azure, zawierającą hello klastrów.

### <a name="start-hello-web-application"></a>Uruchom aplikację sieci web hello

1. Otwórz wiersz polecenia i zmień katalogi zbyt`hdinsight-eventhub-example/dashboard`. Użyj następującej zależności hello tooinstall polecenia wymagane przez aplikację sieci web hello hello:
   
    ```bash
    npm install
    ```

2. Użyj następującej aplikacji sieci web hello toostart polecenia hello:
   
    ```bash
    node server.js
    ```
   
    Zostanie wyświetlony komunikat toohello podobne, następującego tekstu:
   
        Server listening at port 3000

3. Otwórz przeglądarkę sieci web, a następnie wprowadź `http://localhost:3000/` jako adres hello. Jest wyświetlana strona toohello podobne, po obrazu:
   
    ![pulpit nawigacyjny sieci Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Ten wiersz polecenia pozostaw otwarte. Po zakończeniu testowania, Użyj serwera sieci web hello toostop Ctrl-C.

### <a name="generate-data"></a>Generowanie danych

> [!NOTE]
> Witaj w tej sekcji użycia środowiska Node.js, dzięki czemu mogą być używane na dowolnej platformie. Inne przykłady języka można znaleźć w temacie hello `SendEvents` katalogu.

1. Otwórz nowy wiersz, powłokę lub terminal i zmień katalogi zbyt`hdinsight-eventhub-example/SendEvents/nodejs`. zależności hello tooinstall wymagane przez aplikację hello, hello Użyj następującego polecenia:

    ```bash
    npm install
    ```

2. Otwórz hello `app.js` plik w edytorze tekstów i Dodaj hello uzyskanymi wcześniej informacji Centrum zdarzeń:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > W tym przykładzie przyjęto założenie, że użyto `sensordata` jako hello nazwę Centrum zdarzeń. Oraz że `devices` jako nazwa hello zasady hello `Send` oświadczeń.

3. Użyj następującego polecenia tooinsert nowe wpisy w Centrum zdarzeń hello:
   
    ```bash
    node app.js
    ```
   
    Pojawić kilka wierszy danych wyjściowych, które zawierają hello danych wysłanych tooEvent Centrum:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Skompilować i uruchomić hello topologii

1. Otwórz nowy wiersz polecenia i zmień katalogi zbyt`hdinsight-eventhub-example/TemperatureMonitor`. toobuild i pakietu hello topologii, należy użyć następującego polecenia hello: 

    ```bash
    mvn clean package
    ```

2. Topologia hello toostart w trybie lokalnym hello Użyj następującego polecenia:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`Topologia hello jest uruchamiany w trybie lokalnym.
    * `--filter`używa hello `dev.properties` parametry toopopulate plików w definicji topologii hello.
    * `resources/no-hbase.yaml`używa hello `no-hbase.yaml` definicji topologii.
 
   Po rozpoczęciu topologii hello odczytuje wpisów z Centrum zdarzeń, a następnie wysyła je pulpitu nawigacyjnego toohello uruchomiony na komputerze lokalnym. Powinny pojawić się wiersze są wyświetlane na pulpicie nawigacyjnym z sieci web hello, podobne toohello po obrazu:
   
    ![pulpit nawigacyjny z danymi](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Pulpit nawigacyjny hello jest uruchomiona, użyj hello `node app.js` polecenie z poprzedniego hello kroki toosend nowych danych tooEvent koncentratorów. Ponieważ wartości temperatury hello są losowo generowany, wykres hello należy zaktualizować tooshow dużych zmian w temperatury.
   
   > [!NOTE]
   > Musi być w hello **hdinsight-eventhub — przykład/SendEvents/Nodejs** katalogu przy użyciu hello `node app.js` polecenia.

3. Po zweryfikowaniu tego pulpitu nawigacyjnego hello aktualizacji topologii hello Zatrzymaj przy użyciu klawiszy Ctrl + C. Możesz również używać serwera web lokalne powitania toostop klawisze Ctrl + C.

## <a name="create-a-storm-and-hbase-cluster"></a>Tworzenie klastra Storm oraz bazy danych HBase

Witaj kroki opisane w tej sekcji używają [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate klastra sieci wirtualnej platformy Azure i Storm oraz bazy danych HBase na powitania sieci wirtualnej. Szablon Hello również utworzenie aplikacji sieci Web platformy Azure i wdraża kopię hello pulpitu nawigacyjnego do niego.

> [!NOTE]
> Sieć wirtualna jest używana, co topologii hello uruchomiona w klastrze Storm hello mogą bezpośrednio komunikować się z hello klastra HBase przy użyciu interfejsu API języka Java HBase hello.

Szablon usługi Resource Manager Hello używane w tym dokumencie znajduje się w publicznym kontenerze obiektów blob w **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Kliknij przycisk hello toosign przycisk w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Z hello **wdrożenie niestandardowe** wprowadź hello następujące wartości:
   
    ![Parametry HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello w przypadku klastrów Storm oraz bazy danych HBase hello. Na przykład wprowadzenie **abc** jest tworzony klaster Storm o nazwie **storm abc** i klaster HBase o nazwie **hbase abc**.
   * **Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello hello klastrów Storm oraz bazy danych HBase.
   * **Hasło logowania klastra**: hello hasła użytkownika administratora w przypadku klastrów Storm oraz bazy danych HBase hello.
   * **Nazwa użytkownika SSH**: hello toocreate użytkownika SSH hello klastrów Storm oraz bazy danych HBase.
   * **Hasło SSH**: hello hasło użytkownika SSH hello hello klastrów Storm oraz bazy danych HBase.
   * **Lokalizacja**: hello region klastrów hello są tworzone w.
     
     Kliknij przycisk **OK** toosave hello parametrów.

3. Użyj hello **podstawy** sekcji toocreate grupę zasobów lub wybierz istniejący.
4. W hello **lokalizacja grupy zasobów** menu rozwijanego wybierz hello tej samej lokalizacji, ponieważ wybrane dla hello **lokalizacji** parametru w hello **ustawienia** sekcji.
5. Przeczytaj hello warunków i postanowień, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.
6. Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**. Trwa około 20 minut toocreate hello klastrów.

Po utworzeniu hello zasobów wyświetlane są informacje o grupie zasobów hello.

![Grupa zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ storm** i **nazwę BAZOWĄ hbase**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu. Użyjesz tych nazw w kolejnym kroku podczas łączenia klastrów toohello. Należy pamiętać, że hello nazwę hello pulpitu nawigacyjnego witryny jest również **pulpitu nawigacyjnego nazwę bazową**. Ta wartość jest używana w dalszej części tego dokumentu.

## <a name="configure-hello-dashboard-bolt"></a>Skonfiguruj hello bolt pulpitu nawigacyjnego

toosend danych toohello pulpitu nawigacyjnego wdrożony jako aplikacja sieci web, należy zmodyfikować powitania po wierszu hello `dev.properties`pliku:

```yaml
dashboard.uri: http://localhost:3000
```

Zmień `http://localhost:3000` zbyt`http://BASENAME-dashboard.azurewebsites.net` i Zapisz plik hello. Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello podany w poprzednim kroku hello. Można również użyć grupy zasobów hello utworzone wcześniej tooselect hello pulpitu nawigacyjnego i widoku hello adresu URL.

## <a name="create-hello-hbase-table"></a>Tworzenie tabeli HBase hello

toostore danych w bazie danych HBase, należy najpierw utworzymy tabelę. Wstępne tworzenie zasobów, które Storm musi toowrite do, jak w trakcie zasobów toocreate z wewnątrz topologii Storm może doprowadzić do wielu wystąpień w trakcie toocreate hello tego samego zasobu. Utwórz zasoby hello poza hello topologii i używać systemu Storm do odczytu/zapisu i analiza.

1. Użyj SSH tooconnect toohello klastra HBase przy użyciu hello SSH użytkownika i hasło podane toohello szablonu podczas tworzenia klastra. Na przykład, jeśli połączenie przy użyciu hello `ssh` polecenia, należy użyć następującej składni hello:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Zastąp `sshuser` z nazwą użytkownika SSH hello podane podczas tworzenia klastra hello. Zastąp `clustername` o nazwie klastra HBase hello.

2. W sesji SSH hello Uruchom hello powłoki HBase.
   
    ```bash
    hbase shell
    ```
   
    Po załadowaniu hello powłoki, zobacz `hbase(main):001:0>` wiersza.

3. Z powłoki HBase hello wprowadź hello następujące polecenia toocreate danych czujnika hello toostore tabeli:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Sprawdź, czy tabela hello został utworzony za pomocą następującego polecenia hello:
   
    ```hbase
    scan 'SensorData'
    ```
   
    To polecenie zwróci informacje toohello podobnie poniższy przykład, wskazując, że istnieją 0 wierszy w tabeli hello.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Wprowadź `exit` tooexit hello powłoki HBase:

## <a name="configure-hello-hbase-bolt"></a>Skonfiguruj hello HBase bolt

tooHBase toowrite z klastra Storm hello, musisz podać hello HBase bolt hello szczegóły konfiguracji klastra HBase.

1. Użyj jednej z hello następujące przykłady tooretrieve hello dozorcy kworum dla klastra HBase:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Zastąp `your_HDInsight_cluster_name` o nazwie hello klastra usługi HDInsight. Aby uzyskać więcej informacji na temat instalowania hello `jq` narzędzie, zobacz [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Po wyświetleniu monitu wprowadź hasło hello logowania administratora HDInsight hello.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Zastąp "your_HDInsight_cluster_name o nazwie hello klastra usługi HDInsight. Po wyświetleniu monitu wprowadź hasło hello logowania administratora HDInsight hello.
    >
    > W tym przykładzie wymaga programu Azure PowerShell. Aby uzyskać więcej informacji na temat używania programu Azure PowerShell, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    informacje Hello zwrócone przez te przykłady są podobne toohello następującego tekstu:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Te informacje jest używany przez toocommunicate Storm hello klastra HBase.

2. Modyfikowanie hello `dev.properties` plik i dodać hello dozorcy kworum informacji toohello po wierszu:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Tworzenie pakietu i wdrażanie hello tooHDInsight rozwiązania

W środowisku projektowania Użyj powitania po klaster storm toohello topologii Storm kroki toodeploy hello.

1. Z hello `TemperatureMonitor` katalogu, użyj następujących hello polecenia tooperform nowej kompilacji i utworzyć pakiet JAR z projektu:
   
        mvn clean package
   
    To polecenie tworzy plik o nazwie `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `docelowego "katalogu projektu.

2. Użyj scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` i `dev.properties` klaster Storm tooyour plików. Poniższy przykład, Zastąp w hello `sshuser` hello użytkownika SSH podana podczas tworzenia klastra hello i `clustername` o nazwie hello klastra Storm. Po wyświetleniu monitu wprowadź hasło hello hello użytkownika SSH.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Może upłynąć kilka minut tooupload hello plików.

    Aby uzyskać więcej informacji na temat używania hello `scp` i `ssh` poleceń z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Po przekazaniu pliku hello, Połącz klaster Storm toohello przy użyciu protokołu SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Zastąp `sshuser` z nazwą użytkownika SSH hello. Zastąp `clustername` o nazwie klastra Storm hello.

4. toostart hello topologii, użyj następującego polecenia w sesji SSH hello hello:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`przesyła hello topologii toohello Nimbus usługi, która dystrybuuje ją toohello przełożonego węzłów w klastrze hello.
    * `--filter`używa hello `dev.properties` parametry toopopulate plików w definicji topologii hello.
    * `-R /with-hbase.yaml`używa hello `with-hbase.yaml` zawarte w pakiecie hello topologii.

5. Po uruchomieniu hello topologii, otwórz toohello przeglądarki witrynę sieci Web została opublikowana na platformie Azure, a następnie użyj hello `node app.js` polecenia toosend danych tooEvent koncentratora. Informacje o hello sieci web pulpitu nawigacyjnego aktualizacji toodisplay hello powinna zostać wyświetlona.
   
    ![pulpit nawigacyjny](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Wyświetlanie danych HBase

Użyj hello następujące kroki tooconnect tooHBase i sprawdź, czy hello danych zostało zapisanych toohello tabeli:

1. Użyj klastra HBase toohello tooconnect SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Zastąp `sshuser` z nazwą użytkownika SSH hello. Zastąp `clustername` o nazwie klastra HBase hello.

2. W sesji SSH hello Uruchom hello powłoki HBase.
   
    ```bash
    hbase shell
    ```
   
    Po załadowaniu hello powłoki, zobacz `hbase(main):001:0>` wiersza.

3. Widok wierszy z tabeli hello:
   
    ```hbase
    scan 'SensorData'
    ```
   
    To polecenie zwraca informacje o podobnych toohello następującego tekstu, wskazujące, że w tabeli hello jest danych.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Ta operacja skanowania zwraca maksymalnie 10 wierszy z tabeli hello.

## <a name="delete-your-clusters"></a>Usuwanie klastrów

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toodelete hello klastrów, magazynu i aplikacji sieci web w tym samym czasie, Usuń grupę zasobów hello, który je zawiera.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej przykładów dotyczących topologii Storm z usługą HDInsight, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

Aby uzyskać więcej informacji na temat systemu Apache Storm, zobacz hello [Apache Storm](https://storm.incubator.apache.org/) lokacji.

Aby uzyskać więcej informacji dotyczących bazy danych HBase w usłudze HDInsight, zobacz hello [HBase HDInsight Przegląd](hdinsight-hbase-overview.md).

Aby uzyskać więcej informacji o użyciu biblioteki Socket.io, zobacz hello [użyciu biblioteki socket.io](http://socket.io/) lokacji.

Aby uzyskać więcej informacji o D3.js, zobacz [D3.js — danych na dokumentach](http://d3js.org/).

Aby uzyskać informacje o tworzeniu topologii w języku Java, zobacz [Java opracowywania topologii Apache STORM w usłudze HDInsight](hdinsight-storm-develop-java-topology.md).

Aby uzyskać informacji o tworzeniu topologii w środowisku .NET, zobacz [topologii opracowywania C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
