---
title: "aaaHadoop składnikami i wersji - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello składniki platformy Hadoop i wersji w usłudze HDInsight i hello poziomów usług dostępnych w tej chmurze dystrybucji platformie Hortonworks Data Platform."
keywords: "wersje hadoop, składniki ekosystemu platformy hadoop, składniki platformy hadoop, jak wersja hadoop toocheck"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Jakie są składniki platformy Hadoop hello i wersje dostępne w usłudze HDInsight?

Dowiedz się więcej o hello Apache Hadoop ekosystem składników i wersji w usłudze Microsoft Azure HDInsight, a także hello poziomów usług standardowa i Premium. Poznaj także sposób toocheck wersji składników platformy Hadoop w usłudze HDInsight. 

Każda wersja HDInsight jest dystrybucji chmury wersji Hortonworks Data Platform (HDP).

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Składniki platformy Hadoop dostępne z różnych wersji usługi HDInsight
Usługa Azure HDInsight obsługuje wielu wersjach klastra Hadoop, które można wdrożyć w dowolnym momencie. Każdy wybór wersji tworzy określoną wersję hello HDP dystrybucji i zestaw składników, które są zawarte w tej dystrybucji. Począwszy od 17 lutego 2017 r wersji klastra domyślne hello używanego przez usługi Azure HDInsight jest 3.5 i opiera się na HDP 2.5.

w hello w poniższej tabeli wymieniono wersje składnika Hello skojarzone z wersji klastra usługi HDInsight. 

> [!NOTE]
> Witaj wersja domyślna dla hello usługi HDInsight mogą ulec zmianie bez uprzedzenia. Jeśli masz zależność wersji hello wersji usługi HDInsight można określić podczas tworzenia klastrów z hello zestawu .NET SDK z programu Azure PowerShell i interfejsu wiersza polecenia Azure.

| Składnik | HDInsight 3,6 (ustawienie domyślne) | HDInsight 3.5 | HDInsight w wersji 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight w wersji 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop i YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive i HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Zakres Apache | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (tylko w systemie Linux) |1.6.2 + 2.0 (tylko w systemie Linux) |1.6.0 (tylko w systemie Linux) |1.5.2 (Linux tylko eksperymentalne kompilacji) |1.3.1 (tylko system Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Sprawdź, czy bieżące informacje o wersji składnika usługi Hadoop

Hello Hadoop ekosystem składników wersje skojarzone z wersji klastra usługi HDInsight można zmienić za pomocą tooHDInsight aktualizacji. Składniki platformy Hadoop hello toocheck i tooverify, które wersje są używane przez klaster, użyj hello interfejsu API REST Ambari. Witaj **GetComponentInformation** polecenie pobiera informacje o składnikach usługi. Aby uzyskać więcej informacji, zobacz hello [dokumentacji Ambari][ambari-docs].

W przypadku klastrów systemu Windows inny sposób toocheck hello wersja składnika jest toolog tooa klastra przy użyciu pulpitu zdalnego i sprawdź zawartość hello hello C:\apps\dist\ katalogu.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [wycofanie systemu Windows w usłudze HDInsight](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Informacje o wersji

Zobacz [informacje o wersji usługi HDInsight](hdinsight-release-notes.md) dodatkowe informacje o wersji programu na powitania najnowszej wersji usługi HDInsight.

## <a name="supported-hdinsight-versions"></a>Obsługiwane wersje usługi HDInsight
Witaj poniższej tabeli wymieniono wersje hello HDInsight, które są aktualnie dostępne w hello portalu Azure. Hello HDP wersji, które odpowiadają tooeach usługi HDInsight w wersji są wyświetlane wraz z daty wydania produktu hello. Obsługa Hello daty wygaśnięcia i wycofania podawane są również, gdy są one znane.

> [!NOTE]
> Po pomocy technicznej dla wersji, może nie być dostępne za pośrednictwem klasycznego portalu Microsoft Azure hello. Jednak nadal toobe dostępnych za pośrednictwem hello w wersjach klastra `Version` parametru w hello środowiska Windows PowerShell [AzureRmHDInsightCluster nowy](https://msdn.microsoft.com/library/mt619331.aspx) poleceń i hello zestawu .NET SDK do wersji hello dacie wycofania.
> 
> Klastry wysokiej dostępności z dwóch węzłów głównych są wdrażane domyślnie dla usługi HDInsight w wersji 2.1 i nowszymi. Nie są one dostępne dla klastrów usługi HDInsight w wersji 1.6.

| Wersja usługi HDInsight | Wersja HDP | SYSTEM OPERACYJNY MASZYNY WIRTUALNEJ | Wysoka dostępność | Data wydania | Dostępność na powitania portalu Azure | Data wygaśnięcia pomocy technicznej | Dacie wycofania |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3,6 |HDP 2.6 |Ubuntu 16 |Tak |4 kwietnia 2017 r. |Tak | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |Tak |30 września 2016 roku. |Tak |5 września 2017 r. |31 maja 2018 |
| HDInsight w wersji 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |Tak |29 marca 2016 r. |Tak |29 grudnia 2016 r. |9 stycznia 2018 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |Tak |2 grudnia 2015 r. |Tak |27 czerwca 2016 r. |31 lipca 2018 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |Tak |2 grudnia 2015 r. |Tak |27 czerwca 2016 r. |31 lipca 2017 r. |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS lub Windows Server 2012 R2 |Tak |18 lutego 2015 |Nie |1 marca 2016 r. |1 kwietnia 2017 r. |
| HDInsight w wersji 3.1 |HDP 2.1 |Windows Server 2012 R2 |Tak |24 czerwca 2014 r. |Nie |18 maja 2015 r. |30 czerwca 2016 r. |
| HDInsight 3.0 |HDP 2.0 |Windows Server 2012 R2 |Tak |11 lutego 2014 r. |Nie |17 września 2014 r. |30 czerwca 2015 |
| HDInsight 2.1 |HDP 1.3 |Windows Server 2012 R2 |Tak |28 października 2013 |Nie |12 maja 2014 r. |31 maja 2015 r. |
| HDInsight w wersji 1.6 |HDP 1.1 | |Nie |28 października 2013 |Nie |26 kwietnia 2014 r. |31 maja 2015 r. |

## <a name="hdinsight-windows-retirement"></a>Wycofanie usługi HDInsight w systemie Windows
Microsoft Azure HDInsight w wersji 3.3 został hello ostatniej wersji usługi hdinsight w systemie Windows. Witaj dacie wycofania dla usługi HDInsight w systemie Windows jest 31 lipca 2018. Jeśli wszystkie klastry usługi HDInsight w 3.3 systemu Windows lub starszym, przed 31 lipca 2018 należy przeprowadzić migrację tooHDInsight w systemie Linux (usługi HDInsight w wersji 3.5 lub nowszej). Migracja toohello systemu operacyjnego Linux pozwala tooretain hello możliwości toocreate lub zmień rozmiar klastrów usługi HDInsight. Pomocy technicznej dla usługi HDInsight w wersji 3.3 w systemie Windows wygasła w dniu 27 czerwca 2016 r.

Począwszy od usługi HDInsight w wersji 3.4, firma Microsoft wydała HDInsight tylko na powitania systemu operacyjnego Linux. W związku z tym niektóre składniki hello w ramach usługi HDInsight są dostępne dla systemu Linux tylko. Obejmują one zakres Apache, Kafka, interakcyjne Hive, Spark, aplikacje usługi HDInsight i Azure Data Lake Store jako hello plik podstawowy system. W przyszłych wydaniach systemu HDInsight są dostępne tylko na powitania systemu operacyjnego Linux. Nie będzie żadnych kolejnych publikowanych wersjach usługi hdinsight w systemie Windows. 

## <a name="faqs"></a>Często zadawane pytania

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Jaka jest oś czasu hello wycofywania HDInsight w systemie Windows?
31 lipca 2018 jest hello dacie wycofania dla usługi HDInsight w systemie Windows. Jeśli planowane hello dacie wycofania różni się w danym regionie, otrzymasz powiadomienie oddzielnie. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Jaki jest wpływ hello wycofanie HDInsight w systemie Windows dla istniejących klientów?
Po wycofaniu HDInsight w systemie Windows nie może Utwórz nowy klaster usługi HDInsight w systemie Windows lub zmień rozmiar istniejącego klastra usługi HDInsight w systemie Windows. Pomocy technicznej dla usługi HDInsight w wersji 3.3 wygasła w dniu 27 czerwca 2016 r. W związku z tym nie jest brak obsługi ani poprawek usterek HDInsight 3.3 i jego wcześniejsze wersje. W przyszłych wydaniach systemu HDInsight są dostępne tylko na powitania systemu operacyjnego Linux. Nie będzie żadnych kolejnych publikowanych wersjach usługi hdinsight w systemie Windows.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Problem dotyczy które wersji usługi HDInsight w systemie Windows?
Usługa Azure HDInsight wersji 3.3 jest hello ostatniej wersji usługi HDInsight dla systemu Windows. Przed HDInsight w systemie Windows jest wycofywany, wszystkie usługi HDInsight systemu Windows musi być w wersji klastrów 3.3 lub starszym migracji tooHDInsight w systemie Linux w wersji 3.5 lub nowszej. Migrowanie tooHDInsight sieci klastrów w systemie Linux umożliwia tooretain hello możliwości toocreate nowych klastrów lub zmienianie rozmiaru istniejących klastrów. 

### <a name="what-do-i-need-toodo"></a>Czego potrzebuję toodo?
Migrowanie klastra HDInsight Linux obsługiwane tooa klastrów usługi HDInsight w systemie Windows przed 31 lipca 2018. Dowiedz się więcej hello [dokumentu migracji HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Szczegółowe informacje o wersji usługi Azure HDInsight, zobacz listę hello [obsługiwane wersje](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Gdzie można znaleźć typu systemu operacyjnego klastra hello?
W hello portalu Azure, przejdź do pozycji toohello strony Przegląd klastra usługi HDInsight i Znajdź **typ klastra** w obszarze **Essentials**. typy systemu operacyjnego klastra Hello są wyświetlane na tej stronie. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>Nie można przeprowadzić migrację tooan klastra usługi HDInsight Linux przez 31 lipca 2018. Co to jest toomy wpływ hello klastra usługi HDInsight w systemie Windows?
Witaj klastra usługi HDInsight w systemie Windows działa jako-, ale nie można utworzyć nowego klastra usługi HDInsight w systemie Windows, lub zmień rozmiar istniejącego klastra usługi HDInsight w systemie Windows. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>Moje klastra ma zależność .NET. Jak usunąć tę zależność w systemie Linux?
Zależność klaster systemu Linux można rozwiązać za pomocą hello [Mono projektu](http://www.mono-project.com/). Ta implementacja typu open source, platformy .NET jest dostępna w przypadku klastrów HDInsight Linux. Dowiedz się więcej hello [dokumentu migracji HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Jestem nowego klienta dla usługi HDInsight w systemie Windows. Jak utworzyć klaster usługi HDInsight w systemie Windows?
Począwszy od 3 lipca 2017 tylko istniejących klientów systemu Windows w usłudze HDInsight mogą tworzyć nowe okna HDInsight klastrów. Nowi klienci nie można utworzyć klastra usługi HDInsight w systemie Windows hello portalu Azure za pomocą programu PowerShell lub hello zestawu SDK. Zaleca się nowych klientów tworzenia klastra usługi HDInsight w systemie Linux. Istniejący klienci mogą tworzyć nowe okna HDInsight klastrów do hello HDInsight w systemie Windows dacie wycofania. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Czy istnieje cenową wpływu, skojarzony z przejściem z HDInsight tooHDInsight systemu Windows w systemie Linux?
Nie, ceny hello jest hello tego samego dla usługi HDInsight w obu systemu operacyjnego. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Jakie są zalety klienta hello skojarzone z hello przenieść tooonly za pomocą usługi HDInsight w systemie Linux?
* Szybsze czas na rynek technologii danych big data typu open source za pośrednictwem hello usługi HDInsight
* Duże społeczności i ekosystemem pomocy technicznej
* Możliwość tooexercise active rozwoju hello Otwórz społeczności źródła dla platformy Hadoop i inne technologie danych big data

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>HDInsight w systemie Linux oferuje dodatkowe funkcje oprócz co to jest dostępne w usłudze HDInsight w systemie Windows?
Począwszy od usługi HDInsight w wersji 3.4, firma Microsoft wydała HDInsight tylko na powitania systemu operacyjnego Linux. W związku z tym niektóre składniki hello w ramach usługi HDInsight są dostępne dla systemu Linux tylko. Obejmują one zakres Apache, Kafka, interakcyjne Hive, Spark, aplikacje usługi HDInsight i Azure Data Lake Store jako hello plik podstawowy system. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Umowa dotycząca poziomu usług, w wersjach klastra usługi HDInsight
Hello Umowa dotycząca poziomu usług (SLA) jest zdefiniowany w postaci liczby _okna obsługi_. okno obsługi Hello jest hello okres czasu, przez który wersja klastra usługi HDInsight jest obsługiwany przez dział obsługi klienta firmy Microsoft i pomocy technicznej. Jeśli wersja hello _obsługuje Data wygaśnięcia_ , których ma się powodzeniem, klaster usługi HDInsight hello jest poza oknem obsługi hello. Aby uzyskać więcej informacji o obsługiwanych wersjach, zobacz listę hello [obsługiwane wersje klastra usługi HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Data wygaśnięcia pomocy technicznej powitania dla określonej usługi HDInsight w wersji X (po dostępna jest nowsza wersja X + 1) jest obliczany jako hello później z:  

* Formuła 1: Dodaj datę toohello 180 dni, kiedy wersja klastra usługi HDInsight hello X został zwolniony.
* Formuła 2: Dodaj datę toohello 90 dni, gdy wersja klastra usługi HDInsight hello X + 1 jest udostępniona w portalu Azure.

Witaj _dacie wycofania_ jest data powitania po upływie którego hello klastra w wersji nie można utworzyć w usłudze HDInsight. Uruchamianie 31 lipca 2017 rozmiary nie mogą klastra usługi HDInsight po dacie wycofania. 

> [!NOTE]
> Klastry HDInsight systemu Windows (takie jak wersje 2.1, 3.0, 3.1, 3.2 i 3.3) uruchom rodziny systemów operacyjnych gościa Azure w wersji 4, który używa hello 64-bitowej wersji systemu Windows Server 2012 R2. Rodzina systemów operacyjnych gościa Azure w wersji 4 obsługuje hello wersje programu .NET Framework 4.0, 4.5 i 4.5.1 oraz 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Hortonworks wersji skojarzony z wersji usługi HDInsight

sekcja Hello łącza uwagi toorelease hello dystrybucje platformie Hortonworks Data Platform i Apache składników, które są używane z usługą HDInsight.
* Wersja klastra usługi HDInsight 3,6 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* Klaster usługi HDInsight w wersji 3.5 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). Klaster usługi HDInsight w wersji 3.5 jest hello _domyślne_ klastra Hadoop, który jest tworzony w hello portalu Azure.
* Klaster usługi HDInsight w wersji 3.4 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* Wersja klastra usługi HDInsight 3.3 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Informacje o wersji systemu Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) są dostępne w witrynie sieci Web hello Apache.
  * [Apache Hive wersji](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) są dostępne w witrynie sieci Web hello Apache.
* Klaster usługi HDInsight w wersji 3.2 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 2.2][hdp-2-2].

  * Informacje o wersji dla konkretnych składnikach Apache są dostępne w następujący sposób: [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [typowe](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112), i [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* Klaster usługi HDInsight w wersji 3.1 używa dystrybucji Hadoop, która jest oparta na [platformie Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Klastry HDInsight 3.1 utworzone zanim listopad, 7 2014, są oparte na [platformie Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* Klaster usługi HDInsight w wersji 3.0 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 2.0][hdp-2-0-8].
* Klaster usługi HDInsight w wersji 2.1 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 1.3][hdp-1-3-0].
* Wersja klastra usługi HDInsight w wersji 1.6 używa dystrybucji Hadoop, która jest oparta na [Hortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard i HDInsight Premium

Usługa Azure HDInsight zapewnia oferty chmury danych big data hello w dwóch różnych kategoriach: _standardowe_ i _Premium_. Witaj Poniższa tabela zawiera listę funkcji, które są dostępne _tylko_ w HDInsight Premium. Funkcje, które nie zostały jawnie opisane w tabeli hello są dostępne w HDInsight Standard i Premium.

> [!NOTE]
> Witaj HDInsight Premium oferty jest obecnie w wersji zapoznawczej i jest dostępna tylko w przypadku klastrów systemu Linux.

| Funkcja HDInsight Premium | Opis |
| --- | --- |
| Klastry HDInsight przyłączonych do domeny |Dołącz do domen usługi Active Directory (Azure AD) tooAzure HDInsight klastrów, zabezpieczenia na poziomie przedsiębiorstwa. W HDInsight Premium można skonfigurować listę pracowników w przedsiębiorstwie, który może uwierzytelniać za pośrednictwem usługi Azure AD toolog w klastrze usługi HDInsight tooan. Witaj, Administratorze przedsiębiorstwa można skonfigurować kontroli dostępu opartej na rolach zabezpieczeń Hive za pomocą [zakres Apache](http://hortonworks.com/apache/ranger/) i ograniczyć toouse dostępu do danych tylko tyle potrzebne. Na koniec Witaj, Administratorze można przeprowadzać inspekcję dane używane przez pracowników i tooaccess zmiany kontrolowanie zasad, a tym samym osiągnięcie wysoki stopień ładu ich zasobów firmy. Aby uzyskać więcej informacji, zobacz [skonfigurować przyłączonych do domeny w usłudze hdinsight](hdinsight-domain-joined-configure.md). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Typy klastrów, które są obsługiwane w HDInsight Premium
Witaj poniższej tabeli wymieniono hello klastra typów, które są obsługiwane w usłudze HDInsight w warstwie Premium.

| Typ klastra | Standardowa | Premium (wersja zapoznawcza) |
| --- | --- | --- |
| Usługa Hadoop |Tak |Tak (tylko HDInsight 3,6) |
| platforma Spark |Tak |Nie |
| HBase |Tak |Nie |
| Storm |Tak |Nie |
| R Server |Tak |Nie |
| Gałąź interakcyjne (wersja zapoznawcza) |Tak |Nie |
| Kafka (wersja zapoznawcza) |Tak |Nie | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Obsługa usługi Azure Data Lake Store w HDInsight Premium

Klastry HDInsight Premium nie obsługują przy użyciu usługi Azure Data Lake Store jako podstawowy magazyn. Można jednak użyć usługi Azure Data Lake Store, jako dodatek do magazynowania z klastrami HDInsight Premium.

### <a name="pricing-and-sla"></a>Cennik i umowy SLA
Aby uzyskać informacje o cenach i umowy dotyczącej poziomu usług HDInsight Premium, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Domyślne rozmiary maszyn wirtualnych i konfiguracji węzła klastrów
powitania po rozmiary maszyny wirtualnej (VM) domyślne hello listy tabel dla klastrów usługi HDInsight.

> [!IMPORTANT]
> Jeśli potrzebujesz więcej niż 32 węzłami procesu roboczego w klastrze, należy wybrać rozmiar węzła głównego z co najmniej 8 rdzeniami i 14 GB pamięci RAM.
> 
> 

* Wszystkie obsługiwane regiony, z wyjątkiem Brazylia Południowa i Japonia Zachodnia:

  | Typ klastra | Usługa Hadoop | HBase | Storm | platforma Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | HEAD: domyślny rozmiar maszyny Wirtualnej |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | HEAD: zalecane rozmiary maszyn wirtualnych |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3 I A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Pracownik: domyślny rozmiar maszyny Wirtualnej |D3 v2 |D3 v2 |D3 v2 |System Windows: D12 v2; Systemu Linux: V2 D4 |System Windows: D12 v2; Systemu Linux: V2 D4 |
  | Pracownik: zalecane rozmiary maszyn wirtualnych |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | Dozorcy: domyślny rozmiar maszyny Wirtualnej | |A3 |A2 | | |
  | Dozorcy: zalecane rozmiary maszyn wirtualnych | |A3 I A4, A5 |A2 DO A3, A4 | | |
  | Krawędź: domyślny rozmiar maszyny Wirtualnej | | | | |System Windows: D12 v2; Systemu Linux: V2 D4 |
  | Krawędź: zalecany rozmiar maszyny Wirtualnej | | | | |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* Brazylia Południowa i Japonii tylko zachodnie (nie rozmiary v2):

  | Typ klastra | Usługa Hadoop | HBase | Storm | platforma Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | HEAD: domyślny rozmiar maszyny Wirtualnej |D3 |D3 |A3 |D12 |D12 |
  | HEAD: zalecane rozmiary maszyn wirtualnych |D12 D3, D4, |D12 D3, D4, |A3 I A4, A5 |D14 D12, D13, |D14 D12, D13, |
  | Pracownik: domyślny rozmiar maszyny Wirtualnej |D3 |D3 |D3 |System Windows: D12; Linux: D4 |System Windows: D12; Linux: D4 |
  | Pracownik: zalecane rozmiary maszyn wirtualnych |D12 D3, D4, |D12 D3, D4, |D12 D3, D4, |System Windows: D12, D13, D14; Linux: D4, D14 D12, D13, |System Windows: D12, D13, D14; Linux: D4, D14 D12, D13, |
  | Dozorcy: domyślny rozmiar maszyny Wirtualnej | |A2 |A2 | | |
  | Dozorcy: zalecane rozmiary maszyn wirtualnych | |A2 DO A3, A4 |A2 DO A3, A4 | | |
  | Krawędź: rozmiary maszyny Wirtualnej domyślne | | | | |System Windows: D12; Linux: D4 |
  | Krawędź: zalecane rozmiary maszyn wirtualnych | | | | |System Windows: D12, D13, D14; Linux: D4, D14 D12, D13, |

> [!NOTE]
> - HEAD nosi nazwę *Nimbus* hello Storm typ klastra.
> - Proces roboczy jest nazywany *przełożonego* hello Storm typ klastra.
> - Proces roboczy jest nazywany *Region* hello HBase typ klastra.

## <a name="next-steps"></a>Następne kroki
- [Klaster Instalatora platformy Hadoop, Spark i więcej informacji na temat usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Praca w Hadoop w usłudze HDInsight z Komputerami z systemem Windows](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
