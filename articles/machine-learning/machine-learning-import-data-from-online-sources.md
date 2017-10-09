---
title: "aaaImport danych do usługi Machine Learning Studio ze źródeł danych w trybie online | Dokumentacja firmy Microsoft"
description: "Jak tooimport danych szkoleniowych Azure Machine Learning Studio z różnych źródeł online."
keywords: "Importowanie danych, formatu danych, typy danych, źródła danych, dane szkoleniowe"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Importowanie danych do usługi Azure Machine Learning Studio z różnych źródeł danych w trybie online modułem hello importowanie danych
W tym artykule opisano obsługę hello importowanie danych z różnych źródeł i hello informacje potrzebne toomove danych z tych źródeł do eksperymentu uczenia maszynowego Azure.

> [!NOTE]
> Ten artykuł zawiera informacje ogólne o hello [i zaimportuj dane] [ import-data] modułu. Aby uzyskać szczegółowe informacje o typach hello można uzyskać dostępu do danych, formatów, parametry oraz odpowiedzi na pytania toocommon, temat hello modułu odwołania dla hello [i zaimportuj dane] [ import-data] modułu.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Wprowadzenie
Za pomocą hello [i zaimportuj dane] [ import-data] modułu, są dostępne dane z jednego z wielu źródeł danych w trybie online jest uruchomiona eksperymentu [Azure Machine Learning Studio](https://studio.azureml.net/Home):

* Adres URL sieci Web przy użyciu protokołu HTTP
* Hadoop przy użyciu HiveQL
* Magazyn obiektów blob platformy Azure
* Tabeli platformy Azure
* Azure SQL database lub SQL Server na maszynie Wirtualnej Azure
* Lokalną bazą danych programu SQL Server
* Strumieniowe źródło OData obecnie dostawcy danych
* Azure CosmosDB (wcześniej nazywane usługi DocumentDB)

tooaccess źródeł danych w trybie online w eksperymencie Studio Dodaj hello [i zaimportuj dane] [ import-data] tooyour modułu, wybierz hello **źródła danych**, a następnie wprowadź niezbędne parametry hello tooaccess hello danych. Witaj źródeł danych w trybie online, które są obsługiwane są wymienione w poniższej tabeli hello. Ta tabela zawiera podsumowanie hello formatów plików, które są obsługiwane i parametrów, które są używane tooaccess hello danych.

Należy pamiętać, że ponieważ dane szkoleniowe uzyskiwania dostępu do eksperymentu jest uruchomiona, jest on dostępny tylko w tym eksperymencie. W porównaniu danych przechowywanych w module zestawu danych są dostępne tooany eksperymentu w obszarze roboczym.

> [!IMPORTANT]
> Obecnie hello [i zaimportuj dane] [ import-data] i [eksportowanie danych] [ export-data] modułów może odczytywać i zapisywać dane tylko z usługi Azure storage utworzonych przy użyciu hello Klasycznego modelu wdrażania. Innymi słowy hello nowy typ konta magazynu obiektów Blob Azure oferuje warstwy dostępu do magazynu gorącego lub warstwy dostępu do magazynu chłodnego nie jest jeszcze obsługiwany. 
> 
> Ogólnie rzecz biorąc, wszystkie konta magazynu platformy Azure może być utworzony przed tej opcji usługa stały się dostępne powinien bez zmian. 
> Toocreate nowe konto, należy wybrać **klasycznego** dla hello wdrażania modelu, lub użyj Menedżera zasobów i wybierz **ogólnego przeznaczenia** zamiast **magazynu obiektów Blob** dla **Konta rodzaju**. 
> 
> Aby uzyskać więcej informacji, zobacz [usługi Azure Blob Storage: warstwy magazynu gorącego i chłodnego](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Obsługiwane źródeł danych w trybie online
Usługa Azure Machine Learning **i zaimportuj dane** Moduł obsługuje hello następujące źródła danych:

| Źródło danych | Opis | Parametry |
| --- | --- | --- |
| Adres URL sieci Web za pośrednictwem protokołu HTTP |Odczytuje dane w wartości rozdzielanych przecinkami (CSV), wartości tabulatorami (TSV) relacja atrybutu pliku format (ARFF) i formatów pomocy technicznej wektor maszyny (SVM światła) z adresu URL sieci web, który korzysta z protokołu HTTP |<b>Adres URL</b>: Określa hello Pełna nazwa pliku hello, takich jak adres URL witryny hello i nazwę pliku hello, z dowolnym rozszerzeniem. <br/><br/><b>Format danych</b>: Określa jeden z danych hello obsługiwane formaty: CSV, TSV, ARFF lub SVM-light. Jeśli dane hello jest wiersz nagłówka, jest tooassign używane nazwy kolumn. |
| Hadoop/systemu plików HDFS |Odczytuje dane z rozproszonego magazynu na platformie Hadoop. Należy określić dane hello przy użyciu HiveQL, języka przypominającego SQL zapytań. HiveQL również można tooaggregate używanych danych i wykonaj filtrowanie przed dodaniem hello danych tooMachine w Studio uczenia danych. |<b>Gałąź rejestru, kwerendy bazy danych</b>: Określa zapytanie Hive hello używane toogenerate hello danych.<br/><br/><b>Identyfikator URI serwera HCatalog </b> : hello określonej nazwy klastra przy użyciu formatu hello  *&lt;nazwa klastra&gt;. azurehdinsight.net.*<br/><br/><b>Nazwa konta użytkownika Hadoop</b>: Określa konto użytkownika Hadoop hello nazwa używana tooprovision hello klastra.<br/><br/><b>Hasło konta użytkownika Hadoop</b> : Określa hello poświadczenia używane podczas inicjowania obsługi klastra hello. Aby uzyskać więcej informacji, zobacz [klastrów utworzyć Hadoop w HDInsight](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Lokalizacja danych wyjściowych</b>: Określa, czy dane hello są przechowywane w systemie plików rozproszonych Hadoop (HDFS) lub na platformie Azure. <br/><ul>Jeśli przechowujesz dane wyjściowe w systemie plików HDFS, określ identyfikator URI serwera systemu plików HDFS hello. (Można się, że nazwa klastra usługi HDInsight hello toouse bez hello prefiks HTTPS://). <br/><br/>Jeśli Twoje dane przechowywane na platformie Azure, należy określić nazwę konta magazynu Azure hello, klucz dostępu do magazynu i nazwa kontenera magazynu.</ul> |
| Baza danych SQL |Odczytuje dane przechowywane w bazie danych Azure SQL lub w bazie danych programu SQL Server uruchomiony na maszynie wirtualnej platformy Azure. |<b>Nazwa serwera bazy danych</b>: Określa nazwę hello hello serwera, na którym hello bazy danych jest uruchomiona.<br/><ul>W przypadku bazy danych SQL Azure wprowadź nazwę serwera hello, który jest generowany. Zwykle ma on formularz hello  *&lt;generated_identifier&gt;. database.windows.net.* <br/><br/>W przypadku programu SQL server hostowanych na maszynie wirtualnej Azure wprowadź *tcp:&lt;nazwę DNS maszyny wirtualnej&gt;, 1433*</ul><br/><b>Nazwa bazy danych </b>: Określa nazwę hello hello bazy danych na powitania serwera. <br/><br/><b>Nazwa konta użytkownika serwera</b>: Określa nazwę użytkownika dla konta, które ma uprawnienia dostępu do bazy danych hello. <br/><br/><b>Hasło konta użytkownika serwera</b>: Określa hello hasło dla konta użytkownika hello.<br/><br/><b>Dowolny certyfikat serwera Zaakceptuj</b>: Ta opcja (mniej bezpieczna opcja) Jeśli chcesz tooskip recenzowania hello certyfikatu witryny, przed przeczytaniem danych.<br/><br/><b>Zapytanie bazy danych</b>: wprowadź instrukcję SQL opisujący hello dane, które mają tooread. |
| Lokalną bazą danych SQL |Odczytuje dane, które są przechowywane w lokalnej bazie danych SQL. |<b>Brama danych</b>: Określa nazwę hello hello brama zarządzania danymi zainstalowany na komputerze, gdzie ona dostęp do bazy danych SQL Server. Informacje dotyczące konfigurowania bramy hello, zobacz [zaawansowane analizy przy użyciu usługi Azure Machine Learning przy użyciu danych z lokalnego programu SQL server wykonaj](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Nazwa serwera bazy danych</b>: Określa nazwę hello hello serwera, na którym hello bazy danych jest uruchomiona.<br/><br/><b>Nazwa bazy danych </b>: Określa nazwę hello hello bazy danych na powitania serwera. <br/><br/><b>Nazwa konta użytkownika serwera</b>: Określa nazwę użytkownika dla konta, które ma uprawnienia dostępu do bazy danych hello. <br/><br/><b>Nazwa użytkownika i hasło</b>: kliknij <b>wprowadź wartości</b> tooenter poświadczenia bazy danych. Umożliwia zintegrowane uwierzytelnianie systemu Windows lub uwierzytelniania programu SQL Server, w zależności od konfiguracji serwera SQL lokalnie.<br/><br/><b>Zapytanie bazy danych</b>: wprowadź instrukcję SQL opisujący hello dane, które mają tooread. |
| Tabeli platformy Azure |Odczytuje dane z hello usługi tabel w usłudze Azure Storage.<br/><br/>Jeśli rzadko przeczytanie dużych ilości danych, użyj hello usługi tabel Azure. Zapewnia elastyczne i nierelacyjnych (NoSQL), skalowalna na ogromną skalę, niedrogie i wysokiej dostępności pamięci masowej. |Witaj opcje w hello **i zaimportuj dane** zmiany w zależności od tego, czy dostęp do informacji publicznej lub konto magazynu prywatnych, który wymaga poświadczeń logowania. Jest to określane za pomocą hello <b>typ uwierzytelniania</b> który może mieć wartość "PublicOrSAS" lub "Account", z których każdy ma własny zestaw parametrów. <br/><br/><b>Publiczny lub dostęp sygnatury dostępu Współdzielonego URI</b>: hello parametry są:<br/><br/><ul><b>Tabela URI</b>: Określa hello publicznego lub adres URL SAS hello tabeli.<br/><br/><b>Określa hello tooscan wierszy dla nazw właściwości</b>: hello wartości są <i>TopN</i> tooscan hello określona liczba wierszy, lub <i>ScanAll</i> tooget wszystkie wiersze w tabeli hello. <br/><br/>Jeśli dane hello jednorodne i przewidywalne, zalecane jest wybranie *TopN* i wprowadzić numer N. W przypadku dużych tabel może to spowodować szybsze czasów odczytu.<br/><br/>Jeśli hello danych składa się z zestawami właściwości, które różnią się na podstawie głębokości hello i pozycji hello tabeli, wybierz hello *ScanAll* opcję tooscan wszystkich wierszy. To zapewnia integralność hello właściwość wynikowa i konwersji metadanych.<br/><br/></ul><b>Konto magazynu prywatne</b>: hello parametry są: <br/><br/><ul><b>Nazwa konta</b>: Określa nazwę hello hello konta, które zawiera hello tooread tabeli.<br/><br/><b>Klucz konta</b>: Określa hello klucza magazynu skojarzone z kontem hello.<br/><br/><b>Nazwa tabeli</b> : Określa nazwę hello hello tabeli, która zawiera hello tooread danych.<br/><br/><b>Tooscan wierszy dla nazw właściwości</b>: hello wartości są <i>TopN</i> tooscan hello określona liczba wierszy, lub <i>ScanAll</i> tooget wszystkie wiersze w tabeli hello.<br/><br/>Jeśli dane hello jednorodne i przewidywalne, zaleca się wybranie *TopN* i wprowadzić numer N. W przypadku dużych tabel może to spowodować szybsze czasów odczytu.<br/><br/>Jeśli hello danych składa się z zestawami właściwości, które różnią się na podstawie głębokości hello i pozycji hello tabeli, wybierz hello *ScanAll* opcję tooscan wszystkich wierszy. To zapewnia integralność hello właściwość wynikowa i konwersji metadanych.<br/><br/> |
| Azure Blob Storage |Odczytuje dane przechowywane w usłudze obiektów Blob hello w magazynie Azure, w tym obrazów, bez struktury tekst lub dane binarne.<br/><br/>Można użyć hello obiektu Blob usługi toopublicly Uwidacznianie danych lub tooprivately przechowywania danych aplikacji. Dostęp do danych z dowolnego miejsca przy użyciu połączenia protokołu HTTP lub HTTPS. |Witaj opcje w hello **i zaimportuj dane** modułu zmiany w zależności od tego, czy dostęp do informacji publicznej lub konto magazynu prywatnych, który wymaga poświadczeń logowania. Jest to określane za pomocą hello <b>typ uwierzytelniania</b> który może mieć wartość "PublicOrSAS" lub "Konto".<br/><br/><b>Publiczny lub dostęp sygnatury dostępu Współdzielonego URI</b>: hello parametry są:<br/><br/><ul><b>Identyfikator URI</b>: Określa hello publicznego lub adres URL SAS obiektu blob magazynu hello.<br/><br/><b>Format pliku</b>: Określa format hello danych hello w hello usługi Blob. Witaj obsługiwane formaty to CSV, TSV i ARFF.<br/><br/></ul><b>Konto magazynu prywatne</b>: hello parametry są: <br/><br/><ul><b>Nazwa konta</b>: Określa nazwę hello hello konta, które zawiera blob hello ma tooread.<br/><br/><b>Klucz konta</b>: Określa hello klucza magazynu skojarzone z kontem hello.<br/><br/><b>Ścieżka toocontainer, katalogu lub obiektu blob </b> : Określa nazwę hello hello obiektu blob, zawierający hello tooread danych.<br/><br/><b>Format pliku BLOB</b>: Określa format hello hello danych w usłudze obiektów blob hello. Hello danych obsługiwane formaty są CSV, TSV, ARFF, CSV z określonego kodowania i Excel. <br/><br/><ul>Jeśli hello format jest CSV lub TSV, należy się tooindicate, czy plik hello zawiera wiersz nagłówka.<br/><br/>Można użyć hello Excel opcja tooread danych ze skoroszytów programu Excel. W hello <i>format danych programu Excel</i> , należy wskazać, czy dane hello jest w zakresie arkusza programu Excel lub w tabeli programu Excel. W hello <i>arkuszu programu Excel lub osadzonej tabeli </i>, należy określić nazwę hello hello arkusza lub tabela, która ma tooread z.</ul><br/> |
| Dostawca źródła danych |Odczytuje dane z obsługiwanej dostawcy kanału informacyjnego. Obecnie tylko formacie protokołu Open Data Protocol (OData) hello jest obsługiwana. |<b>Typ zawartości danych</b>: Określa hello OData format.<br/><br/><b>Źródłowy adres URL</b>: Określa hello pełny adres URL strumieniowego źródła danych hello. <br/>Na przykład Witaj poniższych odczyty adres URL z bazy danych Northwind hello: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Następne kroki

[Wdrażanie usługi sieci web uczenie Maszynowe Azure korzystających z modułów danych importowanie i eksportowanie danych](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
