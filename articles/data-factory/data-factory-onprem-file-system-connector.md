---
title: "aaaCopy danych do/z systemem plików przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy tooand danych z lokalnego systemu plików przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Skopiuj tooand danych z lokalnego systemu plików przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toocopy danych z lokalnego systemu plików. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z lokalnego systemu plików** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **tooan lokalnego systemu plików**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Aktywność kopiowania nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego. Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, Utwórz plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello. 

## <a name="enabling-connectivity"></a>Włączenie łączności
Fabryka danych obsługuje tooand nawiązujący połączenie z lokalnego systemu plików za pomocą **brama zarządzania danymi**. Należy zainstalować hello brama zarządzania danymi w środowisku lokalnym dla hello fabryki danych usługi tooconnect tooany obsługiwanych na lokalnym magazynem danych w tym systemie plików. Zobacz toolearn o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md). Oprócz brama zarządzania danymi inne pliki binarne muszą tooand toocommunicate toobe zainstalowane z lokalnego systemu plików. Należy zainstalować i używać hello brama zarządzania danymi, nawet jeśli hello systemu plików jest maszyn wirtualnych IaaS platformy Azure. Aby uzyskać szczegółowe informacje na temat bramy hello, zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md).

Zainstaluj toouse udział plików Linux [Samba](https://www.samba.org/) na serwerze Linux i instalacja bramy zarządzania danymi w systemie Windows server. Instalowanie bramy zarządzania danymi na serwerze z systemem Linux nie jest obsługiwane.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działaniem kopiowania przenoszenia danych w systemie plików przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z system plików lokalnych tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączone usługi lokalnego systemu plików i fabryki danych tooyour konta magazynu platformy Azure. Dla właściwości połączonej usługi, które są tooan określonych lokalnego systemu plików, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.
3. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych. I utworzeniu innego zestawu danych toospecify hello folder i nazwę pliku (opcjonalnie) w systemie plików. Dla właściwości zestawu danych, które są określonych tooon lokalnego systemu plików, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.
4. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i FileSystemSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z lokalnego pliku system tooAzure magazynu obiektów Blob, należy użyć FileSystemSource i BlobSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania określonych firmą tooon systemu plików, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z systemu plików, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-file-system) sekcji tego artykułu.

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek toofile określonego systemu:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Możesz połączyć fabrykę danych Azure lokalnego pliku system tooan z hello **na lokalnym serwerze plików** połączonej usługi. Witaj w poniższej tabeli przedstawiono opis elementów JSON, które są określone toohello połączony serwer plików lokalnej usługi.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |Sprawdź, czy właściwość type hello jest ustawiony za**OnPremisesFileServer**. |Tak |
| Host |Określa ścieżkę katalogu głównego hello folderu hello, które mają toocopy. Użyj znaku ucieczki hello ' \ ' znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady. |Tak |
| Nazwa użytkownika |Określ identyfikator hello hello użytkownik, który ma dostęp do serwera toohello. |Nie (Jeśli wybierzesz encryptedCredential) |
| hasło |Określ hasło hello hello użytkownika (nazwa użytkownika). |Nie (Jeśli wybierzesz encryptedCredential |
| encryptedCredential |Określ poświadczenia hello zaszyfrowane, które można uzyskać, uruchamiając polecenie cmdlet hello AzureRmDataFactoryEncryptValue nowy. |Nie (Jeśli wybierzesz toospecify identyfikatora użytkownika i hasła w postaci zwykłego tekstu) |
| gatewayName |Określa nazwę hello hello bramy, że fabryka danych powinien używać serwera plików lokalnych toohello tooconnect. |Tak |


### <a name="sample-linked-service-and-dataset-definitions"></a>Przykładowe połączonej usługi i definicji zestawu danych
| Scenariusz | Host w definicji usługi połączonej | folderPath w definicji zestawu danych |
| --- | --- | --- |
| Folder lokalny na komputerze bramy zarządzania danymi: <br/><br/>Przykłady: D:\\ \* lub D:\folder\subfolder\\* |D:\\ \\ (dla danych zarządzania bramy 2.0 i nowsze wersje) <br/><br/> localhost (dla starszych niż 2.0 bramy zarządzania danych) |. \\ \\ lub folderu\\\\podfolder (dla danych zarządzania bramy 2.0 i nowsze wersje) <br/><br/>D:\\ \\ lub D:\\\\folderu\\\\podfolder (dla wersji bramy poniżej 2.0) |
| Zdalny folder udostępniony: <br/><br/>Przykłady: \\ \\MójSerwer\\udostępnianie\\ \* lub \\ \\MójSerwer\\udostępnianie\\folderu\\podfolderu\\* |\\\\\\\\MójSerwer\\\\udziału |. \\ \\ lub folderu\\\\podfolderu |


### <a name="example-using-username-and-password-in-plain-text"></a>Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Przykład: Użycie encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md). Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych. Zawiera informacje, takie jak lokalizacja hello i format hello danych w magazynie danych hello. Hello typeProperties sekcja dla zestawu danych hello typu **FileShare** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Określa folder toohello podrzędną hello. Użyj znaku ucieczki hello ' \' znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania hello nazwa hello wygenerowany plik jest zgodny z formatem hello: <br/><br/>`Data.<Guid>.txt`(Przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Nie |
| obiektu fileFilter |Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików. <br/><br/>Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).<br/><br/>Przykład 1: "obiektu"fileFilter: "* .log"<br/>Przykład 2: "obiektu"fileFilter: 2014 - 1-?. txt"<br/><br/>Należy pamiętać, że tego obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików. |Nie |
| partitionedBy |Toospecify partitionedBy dynamiczne folderPath/fileName służącego do dane szeregów czasowych. Przykładem jest folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

> [!NOTE]
> Nie można użyć nazwy pliku i obiektu fileFilter jednocześnie.

### <a name="using-partitionedby-property"></a>Za pomocą właściwości partitionedBy
Jak wspomniano w poprzedniej sekcji hello, można określić folderPath dynamiczne i nazwę pliku dla danych serii czasu z hello **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu hello](data-factory-functions-variables.md).

Zobacz więcej informacji na temat zestawów danych szeregu czasowego, planowanie i wycinków, toounderstand [Tworzenie zbiorów danych](data-factory-create-datasets.md), [planowania i wykonywania](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Przykład 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

W tym przykładzie {wycinka} zostanie zastąpiony wartością hello hello fabryki danych zmiennej systemowej SliceStart w formacie hello (YYYYMMDDHH). SliceStart odwołuje się czas toostart hello wycinka. Witaj folderPath jest różne dla każdego wycinka. Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Przykład 2:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, korzystających z hello folderPath i nazwę właściwości.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań. Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.

Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink. Są przenoszenia danych z lokalnego systemu plików, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**FileSystemSource**. Podobnie jeśli przenosisz dane tooan lokalnego systemu plików, w przypadku działania kopiowania hello ustawić także typ ujścia hello**FileSystemSink**. Ta sekcja zawiera listę obsługiwanych przez FileSystemSource i FileSystemSink właściwości.

**FileSystemSource** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |

**FileSystemSink** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| copyBehavior |Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików. |**PreserveHierarchy:** zachowuje hello hierarchii plików w folderze docelowym hello. Oznacza to, że hello względnej ścieżki folderu źródłowego toohello pliku źródłowego hello jest hello taka sama jak ścieżka względna hello hello docelowego pliku toohello docelowy folderu.<br/><br/>**FlattenHierarchy:** wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom folderu docelowego. pliki docelowe Hello są tworzone z automatycznie generowaną nazwą.<br/><br/>**MergeFiles:** scala wszystkie pliki z pliku tooone folderu źródłowego hello. Jeśli określono hello pliku nazwy/nazwa obiektu blob, hello scalony plik nazwa jest hello określonej nazwy. W przeciwnym razie jest nazwa pliku wygenerowana automatycznie. |Nie |

### <a name="recursive-and-copybehavior-examples"></a>Przykłady cyklicznego i copyBehavior
W tej sekcji opisano hello efekty hello operacji kopiowania dla różnych kombinacji wartości dla właściwości cyklicznego i copyBehavior hello.

| wartości cykliczne | wartość copyBehavior | Efekty |
| --- | --- | --- |
| Wartość true |preserveHierarchy |Dla folderu źródłowego Folder1 z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello takie same struktury jako źródło hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| Wartość true |flattenHierarchy |Dla folderu źródłowego Folder1 z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>docelowy Hello Folder1 jest tworzony z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5 |
| Wartość true |mergeFiles |Dla folderu źródłowego Folder1 z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>docelowy Hello Folder1 jest tworzony z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie pliku wygenerowana automatycznie. |
| wartość false |preserveHierarchy |Dla folderu źródłowego Folder1 z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/><br/>Subfolder1 plik3, File4 i File5 nie zostaje pobrana. |
| wartość false |flattenHierarchy |Dla folderu źródłowego Folder1 z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/><br/>Subfolder1 plik3, File4 i File5 nie zostaje pobrana. |
| wartość false |mergeFiles |Dla folderu źródłowego Folder1 z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie pliku wygenerowana automatycznie.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/><br/>Subfolder1 plik3, File4 i File5 nie zostaje pobrana. |

## <a name="supported-file-and-compression-formats"></a>Obsługiwane formaty plików i kompresji
Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Przykłady JSON do kopiowania tooand danych z systemu plików
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu hello można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy tooand danych z lokalnego systemu plików i magazynu obiektów Blob platformy Azure. Można jednak skopiować dane *bezpośrednio* za pomocą dowolnego hello tooany źródeł z wychwytywanie hello na liście [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Przykład: Kopiowanie danych z tooAzure systemu lokalnego pliku magazynu obiektów Blob
W tym przykładzie pokazano sposób toocopy danych z tooAzure systemu lokalnego pliku magazynu obiektów Blob. przykład Witaj ma powitania po jednostek fabryki danych:

* Połączonej usługi typu [OnPremisesFileServer](#linked-service-properties).
* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

następujące przykładowe Hello kopiuje dane szeregów czasowych z tooAzure systemu lokalnego pliku magazynu obiektów Blob, co godzinę. Witaj JSON właściwości, które są używane w te przykłady są opisane w sekcjach hello po hello próbek.

Pierwszym krokiem skonfigurować bramę zarządzania danymi zgodnie z instrukcjami hello [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md).

**Serwer plików lokalnych połączonej usługi:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Firma Microsoft zaleca używanie hello **encryptedCredential** właściwości zamiast hello **userid** i **hasło** właściwości. Zobacz [serwera plików połączona usługa](#linked-service-properties) szczegółowe informacje o tej połączonej usługi.

**Połączonej usługi magazynu Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Lokalnego pliku zestawu danych wejściowych systemu:**

Dane są pobierane z nowego pliku co godzinę. Witaj folderPath i nazwę pliku, właściwości są określane na podstawie czasu rozpoczęcia hello hello wycinka.  

Ustawienie `"external": "true"` informuje fabryki danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Magazyn obiektów Blob Azure wyjściowy zestaw danych:**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godzinę części hello czas rozpoczęcia.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Działanie kopiowania w potoku z systemu plików źródłowy i odbiorczy obiektów Blob:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource**, i **zbiornika** typu ustawiono zbyt**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Przykład: Skopiuj dane z bazy danych SQL Azure tooan lokalnego systemu plików
następujące przykładowe pokazuje Hello:

* Połączonej usługi typu [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)
* Połączonej usługi typu [OnPremisesFileServer](#linked-service-properties).
* Zestaw danych wejściowych typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Wyjściowy zestaw danych typu [FileShare](#dataset-properties).
* Potok z działania kopiowania, która używa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) i [FileSystemSink](#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych z system plików lokalnych tooan tabeli Azure SQL co godzinę. Witaj JSON właściwości, które są używane w te przykłady zostały opisane w sekcjach po hello próbek.

**Baza danych SQL Azure połączonej usługi:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

**Serwer plików lokalnych połączonej usługi:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Firma Microsoft zaleca używanie hello **encryptedCredential** właściwości zamiast hello **userid** i **hasło** właściwości. Zobacz [System plików połączona usługa](#linked-service-properties) szczegółowe informacje o tej połączonej usługi.

**Azure SQL wejściowy zestaw danych:**

przykład Witaj założono, że po utworzeniu tabeli "MyTable" w języku SQL Azure i zawiera kolumnę o nazwie "timestampcolumn", szeregów czasowych danych.

Ustawienie ``“external”: ”true”`` informuje fabryki danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Lokalnego pliku systemu wyjściowego zestawu danych:**

Dane są kopiowane tooa nowy plik co godzinę. Hello folderPath i nazwę pliku dla obiekt blob hello są określane na podstawie czasu rozpoczęcia hello hello wycinka.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy systemu plików:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource**i hello **zbiornika** typu ustawiono zbyt**FileSystemSink**. Zapytanie SQL Hello określony dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


Można również mapować kolumn z źródła toocolumns zestawu danych z zestawu danych zbiornika w definicji działania kopiowania hello. Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajności i dostosowywanie
 toolearn o kluczu czynniki tego wydajność hello wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize, zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md).
