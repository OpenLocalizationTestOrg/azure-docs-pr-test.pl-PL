---
title: replikacja klastra HBase aaaConfigure w ramach sieci wirtualnej - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak replikacji bazy danych HBase tooconfigure obciążenia równoważenia wysokiej dostępności, zero przestoju migracji/update z jednego tooanother wersji usługi HDInsight i odzyskiwania po awarii."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Konfigurowanie replikacji bazy danych HBase klastra w ramach sieci wirtualnej

Dowiedz się, jak tooconfigure replikacji bazy danych HBase w jedną sieć wirtualną (VNet) lub między dwiema sieciami wirtualnymi.

Replikacja klastra używa metodologii wypychania źródła. Klaster HBase można źródła lub miejsca docelowego, lub jego jednocześnie spełnić obie role. Replikacja jest asynchroniczne, a celem hello replikacji jest spójność ostateczna. Odebrania źródła hello rodziny kolumn tooa edycji z włączoną replikacją, tej edycji jest propagowany tooall klastrów docelowych. Gdy dane są replikowane z jednego klastra tooanother, hello źródłowego klastra i wszystkich klastrów, które mają już używane dane hello są śledzone tooprevent replikacji pętle.

W tym samouczku skonfigurujesz replikacji źródłowego i docelowego. Dla innych topologiach klastra [Apache HBase podręcznik](http://hbase.apache.org/book.html#_cluster_replication).

HBase replikacji przypadków użycia pojedynczej sieci wirtualnych:

* Równoważenie obciążenia — na przykład uruchomione skanowanie lub zadań MapReduce w klastrze docelowym hello i wprowadzania danych w klastrze źródłowym hello
* Wysoka dostępność
* Migrowanie danych z jednego tooanother klastra HBase
* Uaktualnianie klastra usługi Azure HDInsight z jednej wersji tooanother

HBase przypadków użycia replikacji dla dwóch sieci wirtualnych:

* Odzyskiwanie po awarii
* Równoważenie obciążenia i partycjonowanie aplikacji hello
* Wysoka dostępność

Klastry są replikowane za pomocą [akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md) skrypty znajdujące się w [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Konfigurowanie środowisk hello

Istnieją trzy możliwe konfiguracje:

- Dwoma klastrami HBase w jednej sieci wirtualnej platformy Azure
- Dwoma klastrami HBase w dwóch różnych sieciach wirtualnych w hello tego samego regionu
- Dwoma klastrami HBase w dwóch różnych sieciach wirtualnych w dwóch różnych regionach (replikacja geograficzna)

toomake go łatwiejsze środowisk hello tooconfigure, utworzono niektóre [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Jeśli wolisz tooconfigure hello środowisk przy użyciu innych metod, zobacz:

- [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Tworzenie klastrów HBase w sieci wirtualnej platformy Azure](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Skonfiguruj jedną sieć wirtualną

Kliknij przycisk powitania po obrazu toocreate dwóch klastrów HBase w hello tej samej sieci wirtualnej. Szablon Hello jest przechowywany w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Skonfigurować dwie sieci wirtualne w hello tego samego regionu

Kliknij przycisk powitania po toocreate obrazu dwie sieci wirtualne sieci wirtualnej komunikacji równorzędnej i dwoma klastrami HBase w hello tego samego regionu. Szablon Hello jest przechowywany w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



Ten scenariusz wymaga [sieci wirtualnej komunikacji równorzędnej](../virtual-network/virtual-network-peering-overview.md). Szablon Hello umożliwia sieci wirtualnej komunikacji równorzędnej.   

Replikacja bazy danych HBase korzysta hello dozorcy maszyn wirtualnych adresów IP. Skonfiguruj statyczne adresy IP dla węzły dozorcy HBase docelowego hello.

**tooconfigure statycznych adresów IP**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu po lewej stronie powitania kliknij **grup zasobów**.
3. Kliknij grupę zasobów zawierającą klaster HBase hello docelowego. Jest to grupa zasobów hello określonej stosowania hello Menedżera zasobów szablonu toocreate hello środowiska. Można użyć toonarrow filtru hello pozycji listy hello. Lista zasobów zawiera dwie sieci wirtualne hello jest widoczny.
4. Kliknij przycisk hello sieć wirtualna, która zawiera klastra HBase hello docelowego. Na przykład kliknij pozycję **xxxx vnet2**. Widać trzech urządzeń o nazwach rozpoczynających się od **kart-zookeepermode -**. Te urządzenia są maszyny wirtualne dozorcy hello trzech.
5. Kliknij jeden z hello dozorcy maszyn wirtualnych.
6. Kliknij przycisk **konfiguracje adresów IP**.
7. Kliknij przycisk **ipConfig1** z listy hello.
8. Kliknij przycisk **statycznych**i zanotuj adres IP rzeczywistego hello. Po uruchomieniu replikacji tooenable akcji skryptu hello należy hello adresu IP.

  ![HDInsight HBase replikacji dozorcy statycznego adresu IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Powtórz krok 6 tooset hello statyczny adres IP dla hello innych dwa węzły dozorcy.

W scenariuszu sieci wirtualnej między hello, musisz użyć hello **- ip** przełącznika podczas wywoływania metody hello **hdi_enable_replication.sh** akcji skryptu.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Skonfigurować dwie sieci wirtualne w dwóch różnych regionach.

Kliknij przycisk powitania po toocreate obrazu dwie sieci wirtualne w dwóch różnych regionach. Szablon Hello jest przechowywany w publicznego kontenera obiektów Blob platformy Azure.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Tworzenie bramy sieci VPN między dwiema sieciami wirtualnymi hello. Aby uzyskać instrukcje, zobacz [tworzenie sieci wirtualnej za pomocą połączenia lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Replikacja bazy danych HBase korzysta hello dozorcy maszyn wirtualnych adresów IP. Skonfiguruj statyczne adresy IP dla węzły dozorcy HBase docelowego hello. tooconfigure statycznego adresu IP, zobacz sekcję "Konfigurowanie dwie sieci wirtualne w hello tego samego regionu" hello, w tym artykule.

W scenariuszu sieci wirtualnej między hello, musisz użyć hello **- ip** przełącznika podczas wywoływania metody hello **hdi_enable_replication.sh** akcji skryptu.

## <a name="load-test-data"></a>Danych testu obciążenia

Podczas replikowania klastra, należy określić hello tooreplicate tabel. W tej sekcji zostanie załadowany niektóre dane w klastrze źródłowym hello. W następnej sekcji hello spowoduje włączenie replikacji między dwoma klastrami hello.

Postępuj zgodnie z instrukcjami hello [samouczek HBase: rozpoczęcie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu bazy danych Apache HBase](hdinsight-hbase-tutorial-get-started-linux.md) toocreate **kontaktów** tabeli i wstawić dane do tabeli hello.

## <a name="enable-replication"></a>Włączanie replikacji

Witaj następujące kroki pokazują, jak toocall hello skryptu akcji skryptu z hello portalu Azure. Do uruchomienia akcji skryptu za pomocą programu Azure PowerShell i hello Azure interfejsu wiersza polecenia (CLI), zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

**Replikacja bazy danych HBase tooenable z hello portalu Azure**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Otwórz klaster HBase hello źródła.
3. W menu klastra hello, kliknij **akcji skryptu**.
4. Kliknij przycisk **przesłać nowe** od góry hello hello bloku.
5. Wybierz lub wprowadź hello następujących informacji:

  - **Nazwa**: wprowadź **włączyć replikację**.
  - **Adres URL skryptu bash**: wprowadź **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **HEAD**: wybrane. Wyczyść hello innych typów węzłów.
  - **Parametry**: hello następujące przykładowe parametry. Włączanie replikacji wszystkie istniejące tabele hello i skopiuj wszystkie dane hello z klastra docelowego toohello hello źródła klastra:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Kliknij przycisk **Utwórz**. Witaj skryptu może zająć trochę czasu, szczególnie, gdy argument - COPYDATA: hello jest używany.

Wymagane argumenty:

|Nazwa|Opis|
|----|-----------|
|-s, - src-klaster | Podaj nazwę DNS hello klastra HBase hello źródła. Na przykład: hbsrccluster -s, klaster — src = hbsrccluster |
|-d, klaster — czasu letniego | Podaj nazwę DNS hello hello przeznaczenia (repliki) klastra HBase. Na przykład: dsthbcluster -s, klaster — src = dsthbcluster |
|-sp, w--src hasła narzędzia ambari | Określ hasło administratora hello dla narzędzia Ambari na klaster HBase hello źródła. |
|— punkt dystrybucji, w czasu letniego — hasła narzędzia ambari | Określ hasło administratora hello dla narzędzia Ambari na klaster HBase hello docelowego.|

Argumenty opcjonalne:

|Nazwa|Opis|
|----|-----------|
|-su,--src-ambari-user | Określ nazwy użytkownika administratora hello Ambari na klaster HBase hello źródła. Witaj, wartość domyślna to **admin**. |
|-du, czasu letniego — ambari użytkownika | Podaj nazwę użytkownika administratora hello dla narzędzia Ambari, na klaster HBase hello docelowego. Witaj, wartość domyślna to **admin**. |
|-t,--lista tabeli | Określ toobe tabel hello replikowane. Na przykład:--lista tabeli = "Tabela1; table2 Tabela3". Jeśli nie określisz tabel, replikacja wszystkich istniejących tabel HBase.|
|-m,--maszyny | Określ hello węzła głównego w którym zostanie uruchomiony hello akcji skryptu. wartość Hello jest hn1 lub hn0. Ponieważ hn0 jest zazwyczaj coraz bardziej zajęty, zalecamy używanie hn1. Użyj tej opcji, po uruchomieniu skryptu hello $0 jako akcja skryptu z portalu usługi HDInsight hello lub Azure PowerShell.|
|-ip | Ten argument jest wymagany, gdy w przypadku włączenia replikacji między dwiema sieciami wirtualnymi. Ten argument działa jako przełącznika toouse hello statycznych adresów IP dozorcy węzłów z klastrów repliki zamiast nazw FQDN. Hello statyczne adresy IP muszą toobe wstępnie przed włączeniem replikacji. |
|-cp, - COPYDATA: | Włącz migrację hello istniejące dane w tabelach hello, w którym replikacja jest włączona. |
|-obr. / min, - replikacja-phoenix-meta | Włącz replikację na Phoenix tabel systemowych. <br><br>*Użyj tej opcji z rozwagą.* Firma Microsoft zaleca, ponownie utwórz tabele Phoenix w klastrach repliki przed skorzystaniem z tego skryptu. |
|-h, — pomoc | Wyświetl informacje o użyciu. |

Witaj print_usage() części hello [skryptu](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) zawiera szczegółowy opis parametrów.

Po akcji skryptu hello jest pomyślnie wdrożone, można użyć klastra HBase docelowego toohello tooconnect SSH i sprawdź, czy dane hello zostały zreplikowane.

### <a name="replication-scenarios"></a>Scenariusze replikacji

Hello poniższej liście przedstawiono niektórych przypadków użycia ogólne i ich ustawienia parametru:

- **Włączanie replikacji na wszystkich tabel między klastrami hello dwa**. Ten scenariusz nie wymaga hello kopiowania/migracji istniejących danych w tabelach hello i nie używa Phoenix tabel. Użyj hello następujące parametry:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Włącz replikację na określonych tabel**. Użyj po replikacji tooenable parametry table1 i table2, Tabela3 hello:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Włącz replikację na określonych tabel i skopiuj hello istniejących danych**. Użyj po replikacji tooenable parametry table1 i table2, Tabela3 hello:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Włączanie replikacji na wszystkich tabel z replikacji metadanych phoenix ze źródła toodestination**. Phoenix metadanych replikacji nie jest doskonała i powinno być włączone, należy zachować ostrożność przy.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Skopiuj i przeprowadzić migrację danych

Istnieją dwa skrypty akcji skryptu oddzielne kopiowanie migracji danych po włączeniu replikacji:

- [Skrypt dla małych tabel](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (kilka gigabajtów kopia rozmiarze i ogólną jest toofinish oczekiwanego w mniej niż godzinę)

- [Skrypt dla dużych tabel](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (Oczekiwano tootake dłużej niż godzinę toocopy)

Możesz wykonać hello tej samej procedury w [włączyć replikację](#enable-replication) akcji skryptu hello toocall z hello następujące parametry:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Witaj print_usage() części hello [skryptu](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) zawiera szczegółowy opis parametrów.

### <a name="scenarios"></a>Scenariusze

- **Skopiuj określonych tabel (test1 test2 i test3) dla wszystkich wierszy edytować do tej chwili (bieżąca sygnatura czasowa)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  lub

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Skopiuj określonych tabel z określonego przedziału czasu**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Wyłącz replikację

toodisable replikacji, użyj innego skryptu akcji skryptu znajdujący się w [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Możesz wykonać hello tej samej procedury w [włączyć replikację](#enable-replication) akcji skryptu hello toocall z hello następujące parametry:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Witaj print_usage() części hello [skryptu](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) zawiera szczegółowy opis parametrów.

### <a name="scenarios"></a>Scenariusze

- **Wyłącz replikację dla wszystkich tabel**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  lub

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Wyłącz replikację w określonych tabel (Tabela1 table2 i Tabela3)**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Następne kroki

W tym samouczku można przedstawiono sposób replikacji bazy danych HBase tooconfigure między dwoma centrami danych. toolearn więcej informacji na temat usługi HDInsight i HBase, zobacz:

* [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started]
* [HDInsight HBase — omówienie][hdinsight-hbase-overview]
* [Tworzenie klastrów HBase w sieci wirtualnej platformy Azure][hdinsight-hbase-provision-vnet]
* [Analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase][hdinsight-hbase-twitter-sentiment]
* [Analizowanie danych czujnika za pomocą Storm i bazy danych HBase w usłudze HDInsight (Hadoop)][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
