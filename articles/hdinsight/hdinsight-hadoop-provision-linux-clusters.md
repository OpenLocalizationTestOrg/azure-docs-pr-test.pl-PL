---
title: Instalator aaaCluster Hadoop, Spark, Kafka, HBase lub R Server - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Ustawianie klastrów platformy Hadoop, Kafka, Spark, HBase, R Server lub Storm dla usługi HDInsight z przeglądarki, hello wiersza polecenia platformy Azure, programu Azure PowerShell, REST lub zestawu SDK."
keywords: "Konfiguracja klastra usługi hadoop, kafka klastra Instalatora, konfiguracja klastra spark, co to jest klaster usługi hadoop"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Ustawianie klastrów w usłudze HDInsight Hadoop, Spark, Kafka i

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Dowiedz się, jak tooset Konfigurowanie i konfigurowania klastrów w usłudze HDInsight Hadoop, Spark, Kafka, interakcyjne Hive, HBase, R Server lub Storm. Ponadto Dowiedz się, jak toocustomize klastrów i dodać zabezpieczeń po dołączeniu do nich tooa domeny.

Klastra usługi Hadoop składa się z kilku maszyn wirtualnych (węzłów), które są używane do przetwarzania rozproszonego zadań. Usługa Azure HDInsight obsługuje szczegóły implementacji instalacji i konfiguracji poszczególnych węzłów, więc wystarczy tooprovide konfiguracji ogólnych informacji. 

> [!IMPORTANT]
>Karta klastra usługi HDInsight zaczyna się po klastra jest tworzony i zatrzymywana, gdy klaster hello jest usunięty. Są naliczane proporcjonalnie za minutę, więc zawsze należy usunąć klaster, gdy nie jest już używana. Dowiedz się, jak za[usunąć klaster.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Metody instalacji klastra
Witaj poniższej tabeli przedstawiono hello różne metody, których można użyć tooset zapasowej klastra usługi HDInsight.

| Klastry utworzone za pomocą | Przeglądarki sieci Web | Wiersz polecenia | Interfejs API REST | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Witryna Azure Portal](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Interfejs wiersza polecenia platformy Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [Zestaw SDK platformy .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Szablony usługi Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Szybkie tworzenie: Konfiguracja podstawowa klastra
W tym artykule przedstawiono w hello za pośrednictwem ustawień [portalu Azure](https://portal.azure.com), w którym można utworzyć klastra usługi HDInsight przy użyciu *szybkie tworzenie* lub *niestandardowy*. 

Postępuj zgodnie instrukcje na toodo ekranie powitania instalacji podstawowy klaster. Szczegółowe informacje znajdują się poniżej dla:

* [Nazwa grupy zasobów](#resource-group-name)
* [Typy klastrów i konfiguracji](#cluster-types) 
* [Logowania do klastra i nazwy użytkownika SSH](#cluster-login-and-ssh-username)
* [Lokalizacja](#location)

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [wycofanie HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Nazwa grupy zasobów 

[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) pomaga w pracy z zasobami hello w aplikacji jako tooas grupy, określonej grupy zasobów platformy Azure. Można wdrożyć, zaktualizować, monitorować lub usunąć wszystkie zasoby hello aplikacji w ramach jednej skoordynowanej operacji.

## <a name="cluster-types"></a>Typy klastrów i konfiguracji
Usługa Azure HDInsight zawiera obecnie następujące hello klastra typy, każdy zestaw składników tooprovide niektórych funkcji.

> [!IMPORTANT]
> Klastry HDInsight są dostępne w różnych typów, z których każdy pojedyncze obciążenie lub technologii. Brak toocreate nie obsługiwaną metodą klastra, który łączy wiele typów, takie jak Storm i bazy danych HBase w jednym klastrze. Jeśli rozwiązanie wymaga technologie, które są rozkładane między wieloma typy klastrów usługi HDInsight, [sieci wirtualnej platformy Azure](https://docs.microsoft.com/azure/virtual-network) można połączyć hello wymagane typy klastrów. 
>
>

| Typ klastra | Funkcjonalność |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Partii zapytań i analizy przechowywanych danych |
| [HBase](hdinsight-hbase-overview.md) |Przetwarzanie dużych ilości danych NoSQL schematu, |
| [STORM](hdinsight-storm-overview.md) |Przetwarzanie zdarzeń w czasie rzeczywistym |
| [Spark](hdinsight-apache-spark-overview.md) |Przetwarzanie w pamięci, interakcyjnych zapytań przetwarzania wsadowego micro strumienia |
| [Kafka (wersja zapoznawcza)](hdinsight-apache-kafka-introduction.md) | Rozproszone platformy przesyłania strumieniowego, które mogą być używane toobuild potoki danych przesyłania strumieniowego w czasie rzeczywistym i aplikacji |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Różne statystyki danych big data, modelowania predykcyjnego i możliwości uczenia maszynowego |
| [Gałąź interakcyjne (wersja zapoznawcza)](hdinsight-hadoop-use-interactive-hive.md) |Buforowanie w pamięci dla zapytań programu Hive interakcyjne i szybsze |

### <a name="number-of-nodes-for-each-cluster-type"></a>Liczba węzłów dla każdego typu klastra
Każdy typ klastra ma własną liczba węzłów, terminologii dla węzłów i domyślny rozmiar maszyny Wirtualnej. W poniższej tabeli hello hello liczba węzłów dla każdego typu węzła jest w nawiasach.

| Typ | Węzły | Diagram |
| --- | --- | --- |
| Usługa Hadoop |Nagłówek węzła (2), węzeł danych (1 +) |![Węzły klastra usługi HDInsight Hadoop](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |HEAD serwer (2), region (1 +), węzeł główny/dozorcy (3) |![Węzły klastra HDInsight HBase](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Węzeł nimbus (2), serwer przełożonego (1 +), dozorcy węzła (3) |![Węzły klastra Storm w usłudze HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| platforma Spark |HEAD węzła (2), węzłem procesu roboczego (1 +), węzeł dozorcy (3) (bezpłatnie dla rozmiaru maszyna wirtualna A1 dozorcy) |![Węzły klastra Spark w usłudze HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Aby uzyskać więcej informacji, zobacz [domyślne rozmiary maszyn wirtualnych i konfiguracja węzła klastrów](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) w "Jakie są składniki platformy Hadoop hello i wersji w usłudze HDInsight?"

### <a name="hdinsight-version"></a>Wersja usługi HDInsight
Wybierz wersję hello HDInsight dla tego klastra. Aby uzyskać więcej informacji, zobacz [HDInsight obsługiwane wersje](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Warstwy klastrów: warstwy usługi HDInsight

Usługa Azure HDInsight zapewnia oferty chmury danych big data hello w dwóch warstwach usług: Standard i Premium.  Aby uzyskać więcej informacji, zobacz [HDInsight Standard i HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Witaj Poniższy zrzut ekranu przedstawia hello informacje o portalu Azure dotyczące wybierania typów klastra.

![HDInsight premium konfiguracji](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Logowania do klastra i nazwy użytkownika SSH
Z klastrami usługi HDInsight można skonfigurować dwa konta użytkownika, podczas tworzenia klastra:

* Użytkownik HTTP: hello domyślna nazwa użytkownika jest *admin*. Używa konfiguracji podstawowej hello na powitania portalu Azure. Czasem jest nazywana "Klastra użytkownika".
* Użytkownik SSH (klastry z systemem Linux): używane tooconnect toohello klastra za pośrednictwem protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Lokalizacja (regiony) dla klastrów i magazynu

Nie trzeba jawnie lokalizacji klastra hello toospecify: hello klaster znajduje się w hello tej samej lokalizacji co magazyn domyślny hello. Aby uzyskać listę obsługiwanych regionów, kliknij przycisk hello **Region** listy rozwijanej na [cennik usługi HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Punkty końcowe magazynu dla klastrów

Mimo że instalacji lokalnej platformy Hadoop używa hello systemu Distributed plików Hadoop (HDFS) do magazynu w klastrze hello, chmura Użyj punkty końcowe usługi storage w hello połączona toocluster. Klastry HDInsight użyć [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) lub [obiekty BLOB w usłudze Azure Storage](hdinsight-hadoop-use-blob-storage.md). Użycie magazynu Azure lub usługi Data Lake Store oznacza, że można bezpiecznie usunąć hello klastrów usługi HDInsight używane do obliczeń przy jednoczesnym zachowaniu danych. 

> [!WARNING]
> Przy użyciu konta, dodatkowe miejsce do magazynowania w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.

Podczas konfigurowania punktu końcowego magazynu domyślne hello należy określić kontener obiektów blob z konta magazynu Azure lub usługi Data Lake Store. Witaj domyślny magazyn zawiera aplikacji i systemu dzienników. Opcjonalnie można określić dodatkowe połączonych kontach magazynu Azure i konta usługi Data Lake Store, które hello klastra może uzyskać dostęp. klaster usługi HDInsight Hello i hello magazynu zależnego konta musi być w hello tej samej lokalizacji platformy Azure.

![Ustawienia magazynu klastra: zgodnego systemem plików HDFS punkty końcowe usługi storage](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Magazyny opcjonalne
Można utworzyć opcjonalne magazyny Oozie lub gałąź. Jednak nie wszystkie typy klastrów obsługują magazyny i magazyn danych SQL Azure nie jest zgodna z magazynów metadanych. 

> [!IMPORTANT]
> Podczas tworzenia niestandardowego potrzeby magazynu metadanych, nie używaj łączniki łączniki i spacje w nazwie bazy danych hello. Może to spowodować toofail procesu tworzenia klastra hello.

### <a name="use-hiveoozie-metastore"></a>Potrzeby magazynu metadanych hive

Tooretain tabele programu Hive po usunięciu klastra usługi HDInsight, należy użyć niestandardowego potrzeby magazynu metadanych. Następnie można dołączyć klastra usługi HDInsight tooanother potrzeby magazynu metadanych hello.

Nie można udostępnić potrzeby magazynu metadanych usługi HDInsight, utworzonego dla jednego wersja klastra usługi HDInsight w różnych wersjach klastra usługi HDInsight. Aby uzyskać listę wersji usługi HDInsight, zobacz [HDInsight obsługiwane wersje](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Potrzeby magazynu metadanych Oozie

wydajność tooincrease przy użyciu Oozie, użyć niestandardowego potrzeby magazynu metadanych. Potrzeby magazynu metadanych może także umożliwić uzyskiwanie dostępu do danych zadania tooOozie po usunięciu klastra. 

> [!IMPORTANT]
> Nie można ponownie użyć niestandardowego potrzeby magazynu metadanych Oozie. toouse niestandardowych potrzeby magazynu metadanych Oozie, musisz podać pustej bazy danych SQL Azure podczas tworzenia klastra usługi HDInsight hello.

## <a name="configure-cluster-size"></a>Skonfiguruj rozmiar klastra

Rozliczenie jest użycie węzła tak długo, jak istnieje hello klaster. Rozliczanie zaczyna się po utworzeniu klastra i zatrzymuje po usunięciu hello klastra. Klastrów nie można deserializować przydzielone lub wstrzymane.

Koszt Hello klastrów usługi HDInsight jest określana przez hello liczba węzłów i hello rozmiary maszyn wirtualnych dla węzłów hello. 

Różne typy klastrów ma inny węzeł typów, liczby węzłów i rozmiary węzła:
* Domyślny typ klastra usługi Hadoop: 
    * Dwa *węzły główne*  
    * Cztery *węzły danych*
* Domyślny typ klastra STORM: 
    * Dwa *węzłów Nimbus*
    * Trzy *węzły dozorcy*
    * Cztery *przełożonego węzłów* 

Jeśli właśnie próbujesz się HDInsight, firma Microsoft zaleca korzystanie z jednego węzła danych. Aby uzyskać więcej informacji na temat cen usługi HDInsight, zobacz [cennik usługi HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> limit rozmiaru Hello klastra jest zależny od używanej subskrypcji platformy Azure. Skontaktuj się z [Azure pomocy dotyczącej rozliczeń](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello limit.
>

Gdy używasz hello Azure tooconfigure portalu hello klastra rozmiaru węzła hello jest dostępna za pośrednictwem hello **warstw cenowych węzłów** bloku. W portalu hello można również zobaczyć hello koszt związany z hello rozmiary innego węzła. 

![Rozmiary węzła HDInsight maszyn wirtualnych](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Rozmiary maszyn wirtualnych 
Podczas wdrażania klastrów, wybierz zasoby obliczeniowe oparte na rozwiązaniu hello planujesz toodeploy. Witaj następujące maszyny wirtualne są używane w przypadku klastrów usługi HDInsight:
* A i maszyny wirtualne z serii D1 4: [rozmiary General-purpose maszyny Wirtualnej systemu Linux](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* Seria D11 14 maszyny Wirtualnej: [rozmiary zoptymalizowanych pod kątem pamięci maszyny Wirtualnej systemu Linux](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind limit jaka wartość należy używać toospecify rozmiar maszyny Wirtualnej, podczas tworzenia klastra przy użyciu różnych zestawów SDK hello lub podczas korzystania z programu Azure PowerShell, zobacz [toouse dla klastrów usługi HDInsight rozmiarów maszyny Wirtualnej](../cloud-services/cloud-services-sizes-specs.md#size-tables). Z tego artykułu połączony, użyj wartości hello w hello **rozmiar** kolumnę tabel hello.

> [!IMPORTANT]
> Jeśli potrzebujesz więcej niż 32 węzłami procesu roboczego w klastrze, należy wybrać rozmiar węzła głównego z co najmniej 8 rdzeniami i 14 GB pamięci RAM.
>
>

Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../virtual-machines/windows/sizes.md). Aby uzyskać informacje o cenach z hello różne rozmiary, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Konfiguracja klastra niestandardowych
Niestandardowe klastra konfiguracji kompilacji na powitania szybkie tworzenie ustawień i dodaje hello następujące opcje:
- [Aplikacje usługi HDInsight](#hdinsight-applications)
- [Rozmiar klastra](#cluster-size)
- Ustawienia zaawansowane
  - [Akcje skryptu](#customize-clusters-using-script-action)
  - [Sieć wirtualna](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Instalowanie aplikacji HDInsight w klastrach

Aplikacja usługi HDInsight to aplikacja, którą użytkownicy mogą zainstalować w klastrze usługi HDInsight opartym na systemie Linux. Dostarczony przez firmę Microsoft, stron trzecich lub który opracowanie samodzielnie, możesz użyć aplikacji. Aby uzyskać więcej informacji, zobacz [instalacji aplikacji innych firm Hadoop w usłudze Azure HDInsight](hdinsight-apps-install-applications.md).

Większość aplikacji usługi HDInsight hello są zainstalowane na węzeł krawędzi puste.  Węzeł krawędzi pusty jest maszyny wirtualnej systemu Linux z hello tych samych narzędzi klienta zainstalowany i skonfigurowany tak jak hello węzła głównego. Za pomocą węzła krawędzi hello dla uzyskiwania dostępu do klastra hello, testowanie aplikacji klienckich i hosting aplikacji klienta. Aby uzyskać więcej informacji, zobacz [użycia węzłów pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Ustawienia zaawansowane: działania skryptu

Można zainstalować dodatkowe składniki lub dostosowanie konfiguracji klastra za pomocą skryptów tworzenia. Te skrypty są wywoływane za pośrednictwem **akcji skryptu**, która jest opcja konfiguracji, która może być używana hello portalu Azure, poleceń cmdlet programu Windows PowerShell dla usługi HDInsight lub hello zestawu .NET SDK usługi HDInsight. Aby uzyskać więcej informacji, zobacz [dostosować klastra usługi HDInsight przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

Niektóre składniki natywnego języka Java, takich jak Mahout i usuwania kaskadowego, można uruchomić w klastrze hello jako pliki archiwum Java (JAR). Te pliki JAR mogą być rozproszone tooAzure magazynu i przesłane klastrów tooHDInsight mechanizmy przesyłania zadania usługi Hadoop. Aby uzyskać więcej informacji, zobacz [Hadoop przesyłania zadania programowo](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Jeśli masz problemy wdrażanie klastrów tooHDInsight pliki JAR lub wywoływania pliki JAR w klastrach HDInsight, skontaktuj się z [Microsoft Support](https://azure.microsoft.com/support/options/).
>
> Kaskadowe nie jest obsługiwany przez usługi HDInsight i nie jest uprawniony do firmy Microsoft Support. Aby uzyskać listę obsługiwanych składników, zobacz [nowości w wersjach klastra hello dostarczanych z usługą HDInsight](hdinsight-component-versioning.md).
>
>

Czasami ma hello tooconfigure następujące pliki konfiguracji podczas procesu tworzenia hello:

* clusterIdentity.xml
* Core-site.xml
* Gateway.XML
* hbase env.xml
* hbase-site.xml
* System plików hdfs-site.xml
* env.xml gałęzi
* gałąź site.xml
* mapred lokacji
* oozie-site.xml
* oozie env.xml
* STORM-site.xml
* tez site.xml
* webhcat site.xml
* yarn-site.xml

Aby uzyskać więcej informacji, zobacz [HDInsight dostosować klastry za pomocą początkowego](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Ustawienia zaawansowane: rozszerzenie klastrów z sieci wirtualnej
Jeśli rozwiązanie wymaga technologie, które są rozkładane między wieloma typy klastrów usługi HDInsight, [sieci wirtualnej platformy Azure](https://docs.microsoft.com/azure/virtual-network) można połączyć hello wymagane typy klastrów. Ta konfiguracja pozwala hello klastrów i wdrożeniem toothem kodu, toodirectly komunikują się ze sobą.

Aby uzyskać więcej informacji na temat używania sieci wirtualnej platformy Azure z usługą HDInsight, zobacz [rozszerzenie usługi HDInsight za pomocą sieci wirtualnych platformy Azure](hdinsight-extend-hadoop-virtual-network.md).

Na przykład za pomocą dwóch typów klastra w ramach sieci wirtualnej platformy Azure, zobacz [analizowanie danych czujnika przy użyciu platformy Storm oraz bazy danych HBase](hdinsight-storm-sensor-data-analysis.md). Aby uzyskać więcej informacji o korzystaniu z usługi HDInsight z sieci wirtualnej, łącznie z określonymi wymaganiami konfiguracji hello sieci wirtualnej, zobacz [możliwości rozszerzania HDInsight przy użyciu usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Rozwiązywanie problemów z kontrolą dostępu

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki

- [Co to są HDInsight, hello ekosystemu Hadoop i klastrów platformy Hadoop?](hdinsight-hadoop-introduction.md)
- [Rozpoczęcie korzystania z usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Praca w Hadoop w usłudze HDInsight z Komputerami z systemem Windows](hdinsight-hadoop-windows-tools.md)
