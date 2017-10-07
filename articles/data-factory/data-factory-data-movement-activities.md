---
title: "aaaMove danych za pomocą działania kopiowania | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przenoszenia danych w potokach fabryki danych: migracji danych między magazynami chmury, a także między magazynem lokalnym i magazynu w chmurze. Użyj działania kopiowania."
keywords: Kopiowanie danych, przenoszenia danych migracji danych i transferu danych
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Przenoszenie danych za pomocą działania kopiowania
## <a name="overview"></a>Omówienie
W fabryce danych Azure, możesz użyć działania kopiowania danych toocopy między lokalnymi i w chmurze magazynów danych. Po skopiowaniu danych hello, można go dalej przekształcone i przeanalizowane. Umożliwia także działanie kopiowania toopublish transformacji i wyniki analizy do analizy biznesowej (BI) i użycie aplikacji.

![Rola działanie kopiowania](media/data-factory-data-movement-activities/copy-activity.png)

Działanie kopiowania jest obsługiwany przez usługę bezpieczny, niezawodnych, skalowalnych i [ogólnie dostępna usługa](#global). Ten artykuł zawiera szczegółowe informacje na przenoszenie danych w fabryce danych i działanie kopiowania.

Po pierwsze Zobaczmy, jak migracja danych odbywa się między dwoma magazyny danych chmury oraz między z lokalnym magazynem danych i magazynu danych w chmurze.

> [!NOTE]
> Ogólnie rzecz biorąc, zobacz toolearn o działaniach [potoki zrozumienia i działania](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>Kopiowanie danych między dwa magazyny danych w chmurze
Jeśli źródłowy i odbiorczy magazyny danych znajdują się w chmurze hello, działanie kopiowania przechodzi przez hello poniższych etapów toocopy danych z obiektu sink toohello źródła hello. Usługa Hello obsługującego działanie kopiowania:

1. Odczytuje dane z magazynu danych źródła hello.
2. Przeprowadza serializacji/deserializacji, kompresji i dekompresji, w mapowaniu kolumn, a konwersja typu. Tak, aby te operacje konfiguracji hello hello wejściowy zestaw danych, wyjściowy zestaw danych i działanie kopiowania.
3. Zapisuje magazyn danych docelowy toohello danych.

Usługa Hello automatycznie wybierze przenoszenia danych hello hello optymalne region tooperform. Ten region jest zwykle hello jeden najbliższego toohello ujścia magazynu danych.

![Kopiowania w chmurze na chmurze](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Kopiowanie danych między z lokalnym magazynem danych i magazynu danych w chmurze
toosecurely przenoszenia danych między z lokalnym magazynem danych i magazynu danych w chmurze, zainstalować bramę zarządzania danymi na komputerze lokalnym. Brama zarządzania danymi jest agentem, który umożliwia hybrydowego przenoszenia danych i przetwarzania. Można go zainstalować hello komputera takie same jak dane hello magazynu samego, lub na osobnym komputerze, na którym ma magazyn danych toohello dostępu.

W tym scenariuszu brama zarządzania danymi wykonuje hello serializacji/deserializacji, kompresji i dekompresji, w mapowaniu kolumn, a konwersja typu. Dane nie przepływać przez hello usługi fabryka danych Azure. Brama zarządzania danymi zapisuje zamiast tego należy bezpośrednio Magazyn docelowy toohello danych hello.

![Kopiuj na lokalnym — do chmury](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Zobacz [przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) wprowadzenie i wskazówki. Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) szczegółowe informacje dotyczące tego agenta.

Można również przenosić dane z / magazynów danych toosupported, które są obsługiwane na maszynach wirtualnych Azure IaaS (VM) przy użyciu bramy zarządzania danymi. W takim przypadku możesz zainstalować bramę zarządzania danymi na hello tej samej maszyny Wirtualnej w danych hello sklepu sam lub na oddzielnym maszynę Wirtualną, która ma dostęp do danych toohello przechowywania.

## <a name="supported-data-stores-and-formats"></a>Magazyny danych obsługiwane i formaty
Działanie kopiowania w fabryce danych kopiuje dane z magazynu danych źródła danych magazynu tooa ujścia. Fabryka danych obsługuje powitania po magazynów danych. Obiekt sink tooany można zapisać danych z dowolnego źródła. Kliknij przycisk toolearn magazynu danych, jak toocopy tooand danych z tego magazynu.

> [!NOTE] 
> Jeśli potrzebujesz toomove danych do/z magazynem danych, który nie obsługuje kopiowania działania, użyj **działania niestandardowego** w fabryce danych na własną logikę do kopiowania/przenoszenia danych. Aby uzyskać szczegółowe informacje na temat tworzenia i używania niestandardowego działania, zobacz artykuł [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) (Korzystanie z niestandardowych działań w potoku usługi Azure Data Factory).

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Przechowuje dane z * można lokalnie lub na platformie Azure IaaS i wymaga tooinstall [brama zarządzania danymi](data-factory-data-management-gateway.md) na maszynie IaaS na lokalnym/Azure.

### <a name="supported-file-formats"></a>Obsługiwane formaty plików
Działanie kopiowania można użyć za**skopiuj pliki jako — jest** między magazyny dwóch danych opartych na plikach, możesz pominąć hello [format sekcji](data-factory-create-datasets.md) w zarówno hello dane wejściowe i wyjściowe definicji zestawu danych. Witaj dane są kopiowane wydajnie bez żadnych serializacji/deserializacji.

Działanie kopiowania również odczytuje i zapisuje toofiles określony format: **tekst JSON, Avro, ORC i Parquet**i koder-dekoder kompresji **GZip, Deflate, BZip2 i ZipDeflate** są obsługiwane. Zobacz [obsługiwane formaty plików i kompresji](data-factory-supported-file-and-compression-formats.md) ze szczegółami.

Na przykład można wykonywać następujące hello skopiować działania:

* Kopiowanie danych w lokalnym programie SQL Server i zapisać w formacie ORC tooAzure Data Lake Store.
* Skopiuj pliki w formacie tekstowym (CSV) z lokalnego systemu plików i zapisywanie tooAzure obiektów Blob w formacie Avro.
* Skopiuj pliki zip z lokalnego systemu plików i Dekompresja, a następnie trafić tooAzure Data Lake Store.
* Kopiowanie danych w formacie tekstowym skompresowane (CSV) GZip z obiektów Blob platformy Azure i zapisu tooAzure bazy danych SQL.

## <a name="global"></a>Przenoszenie danych ogólnie dostępna
Fabryka danych Azure jest dostępna tylko w regionach zachodnie stany USA, wschodnie stany USA i Europa Północna, Europa hello. Jednak usługa hello, obsługującego działanie kopiowania jest dostępna globalnie w hello następujące regiony i lokalizacji geograficznych. Topologia dostępnego globalnie Hello zapewnia przenoszenia danych wydajne, który zazwyczaj pozwala uniknąć przeskoków między regionu. Zobacz [usług według regionu](https://azure.microsoft.com/regions/#services) dostępność fabryki danych i przenoszenie danych w regionie.

### <a name="copy-data-between-cloud-data-stores"></a>Kopiowanie danych między magazyny danych w chmurze
Gdy zarówno źródłowy i odbiorczy magazyny danych znajdują się w chmurze hello, fabryki danych używa wdrożenia usługi hello region najbliższy zbiornika toohello w hello tych samych danych hello toomove geograficznych. Można znaleźć w poniższej tabeli mapowania toohello:

| Lokalizacja geograficzna hello miejsce docelowe danych magazynów | Region magazyn danych docelowy hello | Region używane do przenoszenia danych |
|:--- |:--- |:--- |
| Stany Zjednoczone | Wschodnie stany USA | Wschodnie stany USA |
| &nbsp; | Wschodnie stany USA 2 | Wschodnie stany USA 2 |
| &nbsp; | Środkowe stany USA | Środkowe stany USA |
| &nbsp; | Środkowo-północne stany USA | Środkowo-północne stany USA |
| &nbsp; | Środkowo-południowe stany USA | Środkowo-południowe stany USA |
| &nbsp; | Środkowo-zachodnie stany USA | Środkowo-zachodnie stany USA |
| &nbsp; | Zachodnie stany USA | Zachodnie stany USA |
| &nbsp; | Zachodnie stany USA 2 | Zachodnie stany USA |
| Kanada | Kanada Wschodnia | Kanada Środkowa |
| &nbsp; | Kanada Środkowa | Kanada Środkowa |
| Brazylia | Brazylia Południowa | Brazylia Południowa |
| Europa | Europa Północna | Europa Północna |
| &nbsp; | Europa Zachodnia | Europa Zachodnia |
| Wielka Brytania | Zachodnie Zjednoczone Królestwo | Południowe Zjednoczone Królestwo |
| &nbsp; | Południowe Zjednoczone Królestwo | Południowe Zjednoczone Królestwo |
| Azja i Pacyfik | Azja Południowo-Wschodnia | Azja Południowo-Wschodnia |
| &nbsp; | Azja Wschodnia | Azja Południowo-Wschodnia |
| Australia | Australia Wschodnia | Australia Wschodnia |
| &nbsp; | Australia Południowo-Wschodnia | Australia Południowo-Wschodnia |
| Japonia | Japonia Wschodnia | Japonia Wschodnia |
| &nbsp; | Japonia Zachodnia | Japonia Wschodnia |
| Indie | Indie Środkowe | Indie Środkowe |
| &nbsp; | Indie Zachodnie | Indie Środkowe |
| &nbsp; | Indie Południowe | Indie Środkowe |

Można również jawnie można wskazać region hello toobe usługi fabryka danych używane kopiowania hello tooperform `executionLocation` właściwości w działanie kopiowania `typeProperties`. Obsługiwane wartości dla tej właściwości są wymienione w powyżej **Region używane do przenoszenia danych** kolumny. Należy pamiętać, że dane przechodzi przez tego regionu za pośrednictwem hello danych przesyłanych w sieci podczas kopiowania. Na przykład toocopy między Azure są przechowywane w Korei, można określić `"executionLocation": "Japan East"` tooroute za pośrednictwem region Japonii (zobacz [przykładowe JSON](#by-using-json-scripts) jako odwołanie).

> [!NOTE]
> Jeśli region hello hello miejsce docelowe danych magazynu nie jest w powyższej listy lub niewykrywalnym, domyślnie aktywność kopiowania nie powiedzie się zamiast pośrednictwa alternatywnych regionu, chyba że `executionLocation` jest określona. Witaj obsługiwany region listy będą rozszerzane wraz z upływem czasu.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Kopiowanie danych między z lokalnym magazynem danych i magazynu danych w chmurze
Gdy dane są kopiowane między lokalnymi (lub maszyn wirtualnych Azure/IaaS) i w chmurze magazynów, [brama zarządzania danymi](data-factory-data-management-gateway.md) wykonuje przenoszenia danych na lokalnym komputerze lub maszynie wirtualnej. Hello nie przepływu danych za pośrednictwem hello usługi w chmurze hello, chyba że używasz hello [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) możliwości. W takim przypadku dane przechodzi przez hello przemieszczania magazynu obiektów Blob platformy Azure, zanim zostaną zapisane w magazynie danych zbiornika hello.

## <a name="create-a-pipeline-with-copy-activity"></a>Utworzyć potok z działanie kopiowania
Można utworzyć potoku o działanie kopiowania na kilka sposobów:

### <a name="by-using-hello-copy-wizard"></a>Za pomocą Kreatora kopiowania hello
Witaj kreatora kopiowania fabryki danych pomaga toocreate potoku z działanie kopiowania. Tego potoku umożliwia toocopy danych z obsługiwanych źródeł toodestinations *bez pisania JSON* definicje połączone usługi, zestawy danych i potoki. Zobacz [kreatora kopiowania fabryki danych](data-factory-copy-wizard.md) szczegółowe informacje na temat Kreatora hello.  

### <a name="by-using-json-scripts"></a>Za pomocą skryptów JSON
Edytor fabryki danych można używać w hello portalu Azure, programu Visual Studio lub toocreate programu Azure PowerShell definicji JSON dla potoku (za pomocą działania kopiowania). Następnie możesz go wdrożyć toocreate hello potok w fabryce danych. Zobacz [samouczek: użyj kopii działania w potoku fabryki danych Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) samouczek z instrukcjami krok po kroku.    

Właściwości JSON (takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasad) są dostępne dla wszystkich typów działań. Właściwości, które są dostępne w hello `typeProperties` sekcji hello działanie zależy od każdy typ działania.

Dla działania kopiowania hello `typeProperties` sekcji może być różna w zależności od typów hello źródeł i sink. Kliknij źródło/ujście w hello [obsługiwanych źródeł i wychwytywanie](#supported-data-stores-and-formats) toolearn sekcji o typu właściwości, które obsługuje działanie kopiowania dla tego magazynu danych.

Oto przykład definicji JSON:

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
Hello harmonogram, który jest zdefiniowany w hello wyjściowego zestawu danych określa, kiedy zostanie uruchomione działanie hello (na przykład: **codzienne**, częstotliwość jako **dzień**i interwał jako **1**). Witaj działanie kopiuje dane z zestawem danych wejściowych (**źródła**) tooan wyjściowy zestaw danych (**zbiornika**).

Można określić więcej niż jeden wejściowy zestaw danych tooCopy działania. Przed rozpoczęciem wykonywania działania hello są używane tooverify hello zależności. Jednak tylko hello dane z pierwszego zestawu danych hello jest skopiowany toohello docelowym elemencie dataset. Aby uzyskać więcej informacji, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Wydajności i dostosowywanie
Zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md), która opisuje kluczowych czynników wpływających na wydajność hello przepływu danych (działanie kopiowania) w fabryce danych Azure. Również zawiera listę hello obserwowanych wydajność podczas testowania wewnętrznego oraz opisano różne sposoby toooptimize hello wydajności działania kopiowania.

## <a name="fault-tolerance"></a>Odporność na uszkodzenia
Domyślnie działanie kopiowania będzie zatrzymać kopiowanie danych i przywrócenie błąd wystąpi podczas niezgodne dane między źródłowy i odbiorczy; Mimo że możesz skonfigurować jawnie tooskip i wiersze niezgodne hello dziennika i kopię tylko tych kopii hello toomake zgodne danych zakończyło się pomyślnie. Zobacz hello [działanie kopiowania odporność na uszkodzenia](data-factory-copy-activity-fault-tolerance.md) na więcej szczegółów.

## <a name="security-considerations"></a>Zagadnienia związane z zabezpieczeniami
Zobacz hello [zagadnienia dotyczące zabezpieczeń](data-factory-data-movement-security-considerations.md), która opisuje infrastrukturę zabezpieczeń, że usługi przenoszenia danych z fabryki danych Azure używać toosecure danych.

## <a name="scheduling-and-sequential-copy"></a>Kopiowanie planowania i sekwencyjnych
Zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) Aby uzyskać szczegółowe informacje na temat planowania i wykonywania działania w fabryce danych. Jego jest możliwe toorun wiele operacji kopiowania po kolei w sposób sekwencyjnych/uporządkowane. Zobacz hello [skopiuj sekwencyjnie](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) sekcji.

## <a name="type-conversions"></a>Konwersje typów
Magazyny danych różnych ma inny typ macierzysty systemów. Działanie kopiowania wykonuje automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:

1. Konwertować z typu .NET tooa typów natywnych źródła.
2. Konwertować z typu natywnego zbiornika tooa typu .NET.

Mapowanie Hello z typem typu macierzystego systemu tooa .NET dla magazynu danych jest w artykule magazynu odpowiednich danych hello. (Kliknij łącze określonych hello w hello [obsługiwane magazyny danych](#supported-data-stores) tabeli). Te mapowania toodetermine odpowiednich typów służy podczas tworzenia tabel, dzięki czemu konwersje prawo hello wykonuje działanie kopiowania.

## <a name="next-steps"></a>Następne kroki
* toolearn o hello działanie kopiowania więcej, zobacz [skopiować dane z tooAzure magazynu obiektów Blob platformy Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* toolearn dotyczące przenoszenia danych z lokalnego magazynu tooa chmury danych magazynu danych, zobacz [przenieść dane z lokalnych magazynów danych toocloud](data-factory-move-data-between-onprem-and-cloud.md).
