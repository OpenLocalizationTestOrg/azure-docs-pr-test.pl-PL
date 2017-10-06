---
title: "aaaMove danych ze źródła HTTP - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z lokalnego lub w chmurze HTTP źródła przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Przenoszenie danych ze źródła HTTP przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z tooa punktu końcowego HTTP na lokalnej/w chmurze obsługiwana ujścia magazynu danych. W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych kopię działania i hello listy magazynów danych są obsługiwane jako źródła/sink.

Fabryka danych aktualnie obsługuje tylko przenoszenia danych z HTTP źródła tooother magazyny danych, ale nie przenoszenia danych z innych danych przechowuje docelowego tooan HTTP.

## <a name="supported-scenarios-and-authentication-types"></a>Obsługiwane scenariusze i typy uwierzytelniania
Można użyć tych danych tooretrieve łącznika HTTP z **zarówno w chmurze, jak i dla lokalnego punktu końcowego protokołu HTTP/s** przy użyciu protokołu HTTP **UZYSKAĆ** lub **POST** metody. obsługiwane są następujące typy uwierzytelniania Hello: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, i  **ClientCertificate**. Należy zwrócić uwagę hello różnicę między tym łącznika i hello [łącznika sieci Web w tabeli](data-factory-web-table-connector.md) jest: hello ostatnie jest używane tooextract tabeli zawartości ze strony HTML sieci web.

Podczas kopiowania danych z lokalnego punktu końcowego HTTP, należy zainstalować bramę zarządzania danymi w środowisku lokalnymi hello/Azure maszyny Wirtualnej. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła HTTP przy użyciu różnych narzędzi/interfejsów API.

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

- Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. Dla formatu JSON przykłady toocopy danych z tooAzure źródła HTTP magazynu obiektów Blob, zobacz [przykłady JSON](#json-examples) części w tym artykule.

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooHTTP połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type | musi mieć ustawioną właściwość type Hello: `Http`. | Tak |
| adres URL | Podstawowa toohello adres URL serwera sieci Web | Tak |
| Typ authenticationType | Określa typ uwierzytelniania hello. Dozwolone wartości to: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, **ClientCertificate**. <br><br> Dotyczą odpowiednio toosections pod tą tabelą więcej właściwości i przykłady JSON dla tych typów uwierzytelniania. | Tak |
| enableServerCertificateValidation | Określ, czy tooenable serwera SSL certyfikatu weryfikacji, jeśli źródło jest serwer sieci Web protokołu HTTPS | Nie, domyślna to true |
| gatewayName | Nazwa tooan tooconnect brama zarządzania danymi hello lokalnego źródła HTTP. | Tak, jeśli kopiowanie danych z lokalnego źródła HTTP. |
| encryptedCredential | Zaszyfrowane poświadczenia tooaccess hello punkt końcowy HTTP. Wygenerowany automatycznie podczas konfigurowania hello informacje o uwierzytelnianiu w kopii kreatora lub hello ClickOnce podręcznego okna dialogowego. | Nie. Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera HTTP. |

Zobacz [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) szczegółowe informacje na temat ustawiania poświadczeń dla źródła danych łącznika HTTP lokalnymi.

### <a name="using-basic-digest-or-windows-authentication"></a>Uwierzytelnianie podstawowe, szyfrowane lub systemu Windows

Ustaw `authenticationType` jako `Basic`, `Digest`, lub `Windows`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| nazwa użytkownika | Nazwa użytkownika tooaccess hello punkt końcowy HTTP. | Tak |
| hasło | Hasło dla użytkownika hello (nazwa_użytkownika). | Tak |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Przykład: uwierzytelnianie podstawowe, szyfrowane lub systemu Windows

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>Przy użyciu uwierzytelniania ClientCertificate

Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `ClientCertificate`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| embeddedCertData | zawartość algorytmem Base64 Hello danych binarnych hello pliku wymiany informacji osobistych (PFX). | Określ albo hello `embeddedCertData` lub `certThumbprint`. |
| certThumbprint | Witaj odcisk palca certyfikatu hello, który został zainstalowany na komputerze bramy magazynu certyfikatów. Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego źródła HTTP. | Określ albo hello `embeddedCertData` lub `certThumbprint`. |
| hasło | Hasło skojarzone z certyfikatem hello. | Nie |

Jeśli używasz `certThumbprint` dla certyfikatu uwierzytelniania i hello jest zainstalowany w magazynie osobistym hello hello komputera lokalnego, należy Usługa bramy toohello toogrant hello uprawnienia do odczytu:

1. Uruchom program Microsoft Management Console (MMC). Dodaj hello **certyfikaty** tego hello cele przystawki **komputera lokalnego**.
2. Rozwiń węzeł **certyfikaty**, **osobistych**i kliknij przycisk **certyfikaty**.
3. Kliknij prawym przyciskiem myszy hello certyfikatu z magazynu osobistego hello, a następnie wybierz **wszystkie zadania**->**Zarządzaj kluczami prywatnymi...**
3. Na powitania **zabezpieczeń** , Dodaj konto użytkownika hello, pod którą jest uruchomiona usługa hosta bramy zarządzania danymi w certyfikatem toohello hello dostęp do odczytu.  

#### <a name="example-using-client-certificate"></a>Przykład: przy użyciu certyfikatu klienta
To połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web. Używa certyfikatu klienta, który jest zainstalowany na komputerze hello z zainstalowana brama zarządzania danymi.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Przykład: przy użyciu certyfikatu klienta w pliku
To połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web. Za pomocą pliku certyfikatu klienta na powitania maszyny i zainstalować bramę zarządzania danymi.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu **Http** ma następujące właściwości hello

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Określony typ hello hello zestawu danych. musi być ustawiona zbyt`Http`. | Tak |
| relativeUrl | Względny adres URL toohello zasób zawierający dane hello. Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany. <br><br> tooconstruct dynamicznego adresu URL, można użyć [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md), np. "relativeUrl": "$$Text.Format (" / Moje/raport? miesiąca = {0: yyyy}-{0:MM} & formatowaniu = csv ", SliceStart)". | Nie |
| requestMethod | Metoda HTTP. Dozwolone wartości to **UZYSKAĆ** lub **POST**. | Nie. Domyślnie jest `GET`. |
| additionalHeaders | Dodatkowych nagłówków żądania HTTP. | Nie |
| requestBody | Treść żądania HTTP. | Nie |
| Format | Jeśli chcesz, aby toosimply **pobrać hello danych z punktu końcowego HTTP jako — jest** bez podczas analizowania, Pomiń ten ustawienia formatu. <br><br> Należy odpowiedzi hello HTTP tooparse zawartości podczas kopiowania są obsługiwane następujące typy format hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

### <a name="example-using-hello-get-default-method"></a>Przykład: hello metoda GET (ustawienie domyślne)

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Przykład: przy użyciu metody POST hello

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w hello **typeProperties** sekcji aktywności hello na powitania drugiej zależą od każdego typu działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Obecnie, gdy hello źródła w przypadku działania kopiowania jest typu **HttpSource**, hello następujące właściwości są obsługiwane.

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| httpRequestTimeout | Witaj limitu czasu (TimeSpan) dla tooget żądania HTTP hello odpowiedzi. Jest tooget hello limitu czasu odpowiedzi, hello limitu czasu tooread odpowiedzi danych. | Nie. Wartość domyślna: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Obsługiwane formaty plików i kompresji
Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.

## <a name="json-examples"></a>Przykłady JSON
Poniższy przykład Hello Podaj definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób źródła danych toocopy z protokołu HTTP, tooAzure magazynu obiektów Blob. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Przykład: Kopiowanie danych z tooAzure źródła HTTP magazynu obiektów Blob
Witaj fabryki danych rozwiązania dla tego przykładu zawiera powitania po jednostek fabryki danych:

1. Połączonej usługi typu [HTTP](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [Http](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [HttpSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z tooan źródła HTTP obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

### <a name="http-linked-service"></a>Usługa HTTP połączone
W przykładzie używa hello HTTP połączonej usługi przy użyciu uwierzytelniania anonimowego. Zobacz [HTTP połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="http-input-dataset"></a>Zestaw danych wejściowych HTTP
Ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>W potoku z działanie kopiowania

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**HttpSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.

Zobacz [HttpSource](#copy-activity-properties) hello listę obsługiwanych przez hello HttpSource właściwości.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
