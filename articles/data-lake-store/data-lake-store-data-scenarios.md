---
title: "scenariusze aaaData dotyczących usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello różnych scenariuszy i narzędzi przy użyciu danych można pozyskanych, przetwarzane pobrane i wizualizowane w Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Za pomocą usługi Azure Data Lake Store wymagania danych big data
Istnieją cztery etapy klucza podczas przetwarzania danych big:

* Wprowadzania dużych ilości danych do magazynu danych, w czasie rzeczywistym lub w partiach
* Przetwarzanie danych hello
* Pobieranie danych hello
* Wizualizacja danych hello

W tym artykule przyjrzymy się etapy te o zakresie tooAzure usługi Data Lake Store toounderstand hello narzędzi i opcji dostępnych toomeet potrzeb danych big data.

## <a name="ingest-data-into-data-lake-store"></a>Pozyskiwania danych w usłudze Data Lake Store
W tej sekcji przedstawiono hello różnych źródeł danych i hello różne sposoby, w którym można pozyskanych danych, do konta usługi Data Lake Store.

![Pozyskiwania danych w usłudze Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "pozyskiwania danych w usłudze Data Lake Store")

### <a name="ad-hoc-data"></a>Ad hoc danych
Ta pozycja reprezentuje mniejszych zestawów danych, które są używane do tworzenia prototypów aplikacji danych big data. Istnieją różne sposoby wprowadzania danych ad hoc w zależności od hello źródło danych hello.

| Źródło danych | Za pomocą pozyskiwania |
| --- | --- |
| Komputer lokalny |<ul> <li>[Azure Portal](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Azure CLI wieloplatformowych 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Obiektu Blob magazynu Azure |<ul> <li>[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[Narzędzie AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Narzędzia DistCp uruchomiona w klastrze usługi HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Strumienia danych
Reprezentuje dane, które mogą być generowane przez różnych źródeł, takich jak aplikacje, urządzeń, czujników, itp. Te dane mogą pozyskanych do usługi Data Lake Store za pomocą różnych narzędzi. Te narzędzia zazwyczaj będzie przechwytywania i przetwarzania danych hello na podstawie zdarzeń przez zdarzenie w czasie rzeczywistym, a następnie zapisać hello zdarzeń w partiach do usługi Data Lake Store, aby mogą być dalej przetwarzane.

Poniżej przedstawiono narzędzia, których można użyć:

* [Usługa Azure Stream Analytics](../stream-analytics/stream-analytics-data-lake-output.md) -zdarzeń pozyskanych w usłudze Event Hubs można pisać tooAzure Data Lake za pomocą usługi Azure Data Lake Store danych wyjściowych.
* [Azure HDInsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) — możesz zapisać dane bezpośrednio tooData Lake Store z hello klaster Storm.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) — można odbieranie zdarzeń z usługi Event Hubs, a następnie zapisz je tooData Lake Store za pomocą hello [zestawu SDK .NET Data Lake Store](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Danych relacyjnych
Może również pobierać dane z relacyjnej bazy danych. W danym okresie czasu relacyjnych baz danych, Zbierz dużych ilości danych, które zapewniają wgląd klucza przetwarzanie przez potok danych big data. Następujące narzędzia toomove hello można użyć tych danych do usługi Data Lake Store.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Dane dziennika serwera sieci Web (przy użyciu niestandardowych aplikacji przekazywania)
Tego typu dataset jest zwrócono szczególną uwagę, ponieważ analizy danych dziennika serwera sieci web jest przypadek użycia typowe dla danych big data aplikacji i wymaga się, że dużych woluminów toobe pliki dzienników przekazano toohello Data Lake Store. Można użyć dowolnego z hello następujące narzędzia toowrite własnych skryptów lub aplikacji tooupload tych danych.

* [Azure CLI wieloplatformowych 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Zestaw .NET SDK usługi Azure Data Lake Store](data-lake-store-get-started-net-sdk.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

Do przekazywania danych dziennika serwera sieci web, a także do przekazywania innych typów danych (np. społecznościowych opinie) jest bardzo podejścia toowrite własnych skryptów niestandardowych/aplikacji, ponieważ umożliwia hello tooinclude elastyczność składnika w ramach przekazywania danych większe aplikacji danych big data. W niektórych przypadkach ten kod może potrwać formę hello skryptu lub narzędzia wiersza polecenia proste. W pozostałych przypadkach hello kod może być używane toointegrate big przetwarzania danych w aplikacji biznesowej lub rozwiązania.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Dane skojarzone z klastrami Azure HDInsight
Większość typów klastra usługi HDInsight (Hadoop, HBase, Storm) obsługuje usługi Data Lake Store jako repozytorium magazynu danych. Klastry HDInsight dostęp do danych z usługi Azure blob Storage (WASB). W celu poprawy wydajności można skopiować danych hello z WASB do konta usługi Data Lake Store skojarzony z klastrem hello. Możesz użyć hello następujące narzędzia toocopy hello danych.

* [Narzędzia DistCp Apache](data-lake-store-copy-data-wasb-distcp.md)
* [Usługa AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Dane przechowywane w lokalnych lub IaaS Hadoop klastrów
Duże ilości danych może być przechowywany w istniejących klastrów platformy Hadoop, lokalnie na komputerach przy użyciu systemu plików HDFS. klastry Hadoop Hello może być we wdrożeniu lokalnymi lub może być w klastrze IaaS na platformie Azure. Może istnieć toocopy wymagania takich danych tooAzure usługi Data Lake Store podejścia jednorazowe lub w sposób cykliczny. Istnieją różne opcje, których można używać tooachieve to. Poniżej znajduje się lista alternatyw i hello skojarzone kompromis.

| Podejście | Szczegóły | Zalety | Zagadnienia do rozważenia |
| --- | --- | --- | --- |
| Użyj danych toocopy fabryki danych Azure (ADF) bezpośrednio z usługi Hadoop clusters tooAzure Data Lake Store |[ADF obsługuje system plików HDFS jako źródła danych](../data-factory/data-factory-hdfs-connector.md) |ADF obsługuje system plików HDFS i pierwszej klasy end-to-end zarządzania i monitorowania poza pole |Wymaga lokalnego wdrożenia bramy zarządzania danymi toobe lub w klastrze IaaS hello |
| Eksportowanie danych z usługi Hadoop jako plików. Następnie skopiuj hello pliki tooAzure Data Lake Store przy użyciu mechanizmu odpowiednie. |Możesz skopiować przy użyciu usługi Data Lake Store tooAzure plików: <ul><li>[Program Azure PowerShell dla systemu operacyjnego Windows](data-lake-store-get-started-powershell.md)</li><li>[Azure CLI wieloplatformowych 2.0 OS z systemem innym niż Windows](data-lake-store-get-started-cli-2.0.md)</li><li>Niestandardowych aplikacji przy użyciu zestawu SDK wszelkich Data Lake Store</li></ul> |Szybkie tooget uruchomiona. Możliwość przekazywania dostosowane |Proces wieloetapowych, która obejmuje wiele technologii. Zarządzanie i monitorowanie wzrośnie toobe żądanie za pośrednictwem hello dostosowane czas podany rodzaj hello narzędzia |
| Użyj narzędzia Distcp toocopy danych z usługi Hadoop tooAzure magazynu. Następnie skopiuj dane z magazynu Azure tooData Lake Store przy użyciu mechanizmu odpowiednie. |Można skopiować danych z magazynu Azure tooData Lake — magazyn przy użyciu: <ul><li>[Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)</li><li>[Narzędzie AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Narzędzia DistCp Apache uruchamianych w klastrach usługi HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |Można użyć narzędzia open source. |Proces wieloetapowych, który obejmuje wiele technologii |

### <a name="really-large-datasets"></a>Naprawdę dużych zestawów danych
Do przekazywania zestawów danych w wielu terabajtów, za pomocą opisanych powyżej metod hello może być czasem powolne i kosztowne. W takich przypadkach można użyć poniższych opcji hello.

* **Za pomocą usługi Azure ExpressRoute**. Usługa Azure ExpressRoute umożliwia tworzenie prywatnych połączeń między centrach danych platformy Azure i infrastruktury lokalnie. To zapewnia niezawodne opcję transferowania dużych ilości danych. Aby uzyskać więcej informacji, zobacz [dokumentacja usługi Azure ExpressRoute](../expressroute/expressroute-introduction.md).
* **"Offline" przekazywanie danych**. Jeśli przy użyciu usługi Azure ExpressRoute nie jest jakiegokolwiek powodu możliwe, można użyć [usługi Import/Eksport Azure](../storage/common/storage-import-export-service.md) tooship dysków twardych z centrum danych Azure tooan danych. Twoje dane są pierwszy przekazany tooAzure obiektów blob magazynu. Następnie można użyć [fabryki danych Azure](../data-factory/data-factory-azure-datalake-connector.md) lub [narzędzie AdlCopy](data-lake-store-copy-data-azure-storage-blob.md) toocopy dane z usługi Azure magazynu obiektów blob tooData Lake Store.

  > [!NOTE]
  > Podczas przy użyciu hello usługi Import/eksport, hello rozmiary plików na powitalne dysków, na potrzeby wysłania danych tooAzure Centrum nie mogą zawierać więcej niż 195 GB.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Przetwarzaj dane przechowywane w usłudze Data Lake Store
Po hello dane są dostępne w usłudze Data Lake Store można uruchamiać analizy na że danych przy użyciu hello obsługiwane aplikacje danych big data. Obecnie można używać zadania analizy danych toorun Azure HDInsight i usługą Azure Data Lake Analytics na powitania danych przechowywanych w usłudze Data Lake Store.

![Analizowanie danych w usłudze Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "analizowanie danych w usłudze Data Lake Store")

Można przyjrzeć się hello następujące przykłady.

* [Tworzenie klastra usługi HDInsight z usługą Data Lake Store jako magazyn](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Pobierz dane z usługi Data Lake Store
Możesz również mają toodownload lub przenieść dane z usługi Azure Data Lake Store w scenariuszach, takich jak:

* Przenoszenie danych tooother repozytoria toointerface z Twoje istniejące potoków przetwarzania danych. Na przykład może być toomove dane z usługi Data Lake Store tooAzure bazy danych SQL lub lokalnego programu SQL Server.
* Pobierz dane tooyour komputera lokalnego do przetwarzania w środowisku IDE podczas kompilowania aplikacji prototypów.

![Wyjściowych danych z usługi Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "wyjściowych danych z usługi Data Lake Store")

W takich przypadkach można użyć dowolnego z hello następujące opcje:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
* [Narzędzia DistCp Apache](data-lake-store-copy-data-wasb-distcp.md)

Umożliwia także hello następujące metody toowrite aplikacji/skryptu toodownload danych użytkownika z usługi Data Lake Store.

* [Azure CLI wieloplatformowych 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Zestaw .NET SDK usługi Azure Data Lake Store](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Wizualizuj dane w usłudze Data Lake Store
Można używać różnych usług toocreate wizualnej reprezentacji danych przechowywanych w usłudze Data Lake Store.

![Wizualizuj dane w usłudze Data Lake Store](./media/data-lake-store-data-scenarios/visualize-data.png "wizualizacji danych w usłudze Data Lake Store")

* Można uruchomić przy użyciu [fabryki danych Azure toomove dane z usługi Data Lake Store tooAzure SQL Data Warehouse](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Następnie można [integracji usługi Power BI z usługą Magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate wizualną reprezentację danych hello.
