---
title: "aaaCopy tooand danych z usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy tooand danych z usługi Data Lake Store przy użyciu fabryki danych Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Skopiuj tooand danych z usługi Data Lake Store przy użyciu fabryki danych
W tym artykule opisano sposób toouse działanie kopiowania w fabryce danych Azure toomove danych tooand z usługi Azure Data Lake Store. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykuł Omówienie przenoszenia danych z działania kopiowania.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z usługi Azure Data Lake Store** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **tooAzure usługi Data Lake Store**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Przed utworzeniem potoku z działania kopiowania, należy utworzyć konto usługi Data Lake Store. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Typy obsługiwane uwierzytelniania
Łącznik usługi Data Lake Store Hello obsługuje następujące typy uwierzytelniania:
* Uwierzytelnianie jednostki usługi
* Uwierzytelnianie użytkownika poświadczeń (OAuth) 

Firma Microsoft zaleca korzystanie z uwierzytelniania głównej usługi, zwłaszcza w przypadku kopiowania danych zaplanowane. Zachowanie wygaśnięcia tokenu może wystąpić przy użyciu uwierzytelniania poświadczeń użytkownika. Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#linked-service-properties) sekcji.

## <a name="get-started"></a>Rozpoczęcie pracy
Można utworzyć potok z działania kopiowania, który przenosi dane z usługi Azure Data Lake Store za pomocą różnych narzędzi/interfejsów API.

Witaj najprostszy sposób toocreate danych toocopy potoku jest toouse hello **kreatora kopiowania**. Samouczek dotyczący tworzenia za pomocą Kreatora kopiowania hello potoku, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z tooan magazynu obiektów blob platformy Azure, Azure Data Lake Store, tworzenia dwóch toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour magazynu usługi Azure Data Lake. Dla właściwości połączonej usługi, które są określone tooAzure usługi Data Lake Store, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji. 
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych. I utwórz inny zestaw danych toospecify hello folderu i ścieżce pliku w magazynie usługi Data Lake hello, który przechowuje dane hello skopiowane z magazynu obiektów blob hello. Dla właściwości zestawu danych, które są określone tooAzure usługi Data Lake Store, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i AzureDataLakeStoreSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z usługi Azure Data Lake Store tooAzure magazynu obiektów Blob, należy użyć AzureDataLakeStoreSource i BlobSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania, które są określone tooAzure usługi Data Lake Store, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.  

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z usługi Azure Data Lake Store, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) sekcji tego artykułu.

Witaj następujące sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane toodefine fabryki danych jednostek określonych tooData Lake Store.

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Połączona usługa łączy fabryki danych tooa magazynu danych. Tworzenie połączonej usługi typu **AzureDataLakeStore** toolink fabrykę danych tooyour danych Data Lake Store. Witaj w poniższej tabeli opisano określonych usług tooData Lake Store połączone elementy JSON. Można wybrać usługę podmiotu zabezpieczeń i uwierzytelniania poświadczeń użytkownika.

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **Typ** | zbyt należy ustawić właściwość typu Hello**AzureDataLakeStore**. | Tak |
| **dataLakeStoreUri** | Informacje o hello konta usługi Azure Data Lake Store. Informacja ta ma jeden z następujących formatów hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` lub `adl://[accountname].azuredatalakestore.net/`. | Tak |
| **Identyfikator subskrypcji** | Należy hello toowhich identyfikator subskrypcji platformy Azure konta usługi Data Lake Store. | Wymagany dla odbiorcy |
| **grupy zasobów o nazwie** | Należy zasobów platformy Azure grupy nazwa toowhich hello konta usługi Data Lake Store. | Wymagany dla odbiorcy |

### <a name="service-principal-authentication-recommended"></a>Uwierzytelnianie główna usługi (zalecane)
główne uwierzytelnianie usługi toouse rejestru jednostki aplikacji w usłudze Azure Active Directory (Azure AD) i udziel go hello dostępu tooData Lake Store. Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Zwróć uwagę na powitania następujące wartości, których używasz toodefine hello połączonej usługi:
* Identyfikator aplikacji
* Klucz aplikacji 
* Identyfikator dzierżawy

> [!IMPORTANT]
> Jeśli używasz hello kreatora kopiowania tooauthor danych potoki, upewnij się, przyznanie nazwy głównej usługi hello co najmniej **czytnika** roli w kontroli dostępu (Zarządzanie tożsamościami i dostępem) dla konta usługi Data Lake Store hello. Ponadto udzielić co najmniej nazwy głównej usługi hello **Odczyt i wykonywanie** głównym usługi Data Lake Store tooyour uprawnień ("/") i jej funkcji podrzędnych. W przeciwnym razie można napotkać wiadomości powitania "hello, podane poświadczenia są nieprawidłowe."<br/><br/>
Po utworzeniu lub zaktualizować nazwy głównej usługi w usłudze Azure AD, może upłynąć kilka minut, aż hello zmiany tootake efekt. Sprawdź nazwę główną usługi hello i konfiguracjami listę kontroli dostępu (ACL) kontroli dostępu do usługi Data Lake Store. Jeśli widzisz nadal wiadomości powitania "hello, podane poświadczenia są nieprawidłowe", zaczekaj chwilę i spróbuj ponownie.

Uwierzytelnianie usługi głównej określając hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **servicePrincipalId** | Określ identyfikator aplikacji hello klienta. | Tak |
| **servicePrincipalKey** | Określ klucz aplikacji hello. | Tak |
| **dzierżawy** | Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja. Można go pobrać aktywowania hello myszy w prawym górnym narożniku hello hello portalu Azure. | Tak |

**Przykład: Usługa podmiotu zabezpieczeń uwierzytelniania**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Uwierzytelnianie poświadczeń użytkownika
Alternatywnie można użyć toocopy uwierzytelniania poświadczeń użytkownika z lub tooData Lake Store, określając hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **autoryzacji** | Kliknij przycisk hello **autoryzacji** przycisku na powitania Edytor fabryki danych i wprowadź Twoje poświadczenia przypisującej właściwość toothis hello wygenerowana automatycznie autoryzacji URL. | Tak |
| **Identyfikator sesji** | Identyfikator sesji OAuth z sesji autoryzacji OAuth hello. Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz. To ustawienie jest automatycznie generowany, gdy używasz hello Edytor fabryki danych. | Tak |

**Przykład: Użytkownik poświadczeń uwierzytelniania**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Witaj kod autoryzacji, który generuje za pomocą hello **autoryzacji** przycisk wygasa po określonym czasie. następujące wiadomość Hello oznacza, że wygasł token uwierzytelniania hello:

Poświadczeń błąd operacji: invalid_grant - AADSTS70002: błąd podczas sprawdzania poprawności poświadczeń. AADSTS70008: hello podać Udziel dostępu jest wygasnąć lub zostać odwołane. Identyfikator śledzenia: Identyfikator korelacji d18629e8-af88-43c5-88e3-d8419eb1fca1: sygnatura czasowa fac30a0c-6be6-4e02-8d69-a776d2ffefd7: 2015-12-15 21-09-31Z.

Witaj poniższej tabeli przedstawiono czas wygaśnięcia hello różnych typów kont użytkowników:


| Typ użytkownika | Wygasa po |
|:--- |:--- |
| Konta użytkowników *nie* zarządzane przez usługę Azure Active Directory (na przykład @hotmail.com lub @live.com) |12 godzin |
| Konta użytkowników zarządzanych przez usługę Azure Active Directory |Uruchom 14 dni od ostatniego wycinek hello <br/><br/>90 dni, jeśli wycinek oparte na podstawie OAuth połączonej usługi jest uruchamiana co najmniej raz na 14 dni |

Jeśli zmienisz hasło wcześniejszy niż czas wygaśnięcia tokenu hello hello token wygasa natychmiast. Zostanie wyświetlony komunikat hello wymienione wcześniej w tej sekcji.

Można ponownie autoryzować hello konta przy użyciu hello **autoryzacji** przycisk wygaśnięcia tokenu hello tooredeploy hello połączonej usługi. Można również tworzyć wartości hello **sessionId** i **autoryzacji** właściwości programowo przy użyciu hello następujący kod:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Aby uzyskać szczegółowe informacje o klasach fabryki danych hello używane w kodzie hello, zobacz hello [klasy AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [klasy AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), i [ Klasa AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tematów. Dodaj tooversion odwołanie `2.9.10826.1824` z `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` dla hello `WindowsFormsWebAuthenticationDialog` klasa używana w kodzie hello.

## <a name="dataset-properties"></a>Właściwości zestawu danych
toospecify danych wejściowych toorepresent zestawu danych w usłudze Data Lake Store, ustaw hello **typu** właściwości zestawu danych hello zbyt**AzureDataLakeStore**. Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello usługi Data Lake Store połączonej usługi. Aby uzyskać pełną listę właściwości JSON sekcje i dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zestawu danych w formacie JSON, takich jak **struktury**, **dostępności**, i **zasad**, są podobne dla wszystkich typów obiektów dataset (Azure SQL database, obiektów blob platformy Azure i tabeli platformy Azure, na przykład). Witaj **typeProperties** sekcja zawiera informacje, takie jak lokalizacja i format hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. 

Witaj **typeProperties** sekcja dla zestawu danych typu **AzureDataLakeStore** zawiera hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **folderPath** |Ścieżka toohello kontenera i folderu w usłudze Data Lake Store. |Tak |
| **Nazwa pliku** |Nazwa pliku hello w usłudze Azure Data Lake Store. Witaj **fileName** właściwość jest opcjonalna i z uwzględnieniem wielkości liter. <br/><br/>Jeśli określisz **fileName**, hello działania (w tym kopiowania) działa na powitania określonego pliku.<br/><br/>Gdy **fileName** nie zostanie określony, kopia zawiera wszystkie pliki w **folderPath** hello danych wejściowych.<br/><br/>Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania hello hello wygenerowany plik nosi nazwę w formacie hello danych. _Identyfikator GUID_txt ". Na przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Nie |
| **partitionedBy** |Witaj **partitionedBy** właściwość jest opcjonalna. Służy on toospecify dynamiczne ścieżkę i nazwę pliku dla dane szeregów czasowych. Na przykład **folderPath** mogą nadać parametry dla każdej godziny danych. Aby uzyskać szczegółowe informacje i przykłady, zobacz [hello właściwości partitionedBy](#using-partitionedby-property). |Nie |
| **Format** | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, i  **ParquetFormat**. Zestaw hello **typu** właściwości w **format** tooone tych wartości. Aby uzyskać więcej informacji, zobacz hello [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) części hello [formatów plików i ich kompresji, obsługiwanych przez usługi fabryka danych Azure](data-factory-supported-file-and-compression-formats.md) artykułu. <br><br> Pliki toocopy "jako — jest" między opartych na plikach magazynów (kopia binarnego), Pomiń hello `format` sekcji w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| **Kompresja** | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy są **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formatów plików i ich kompresji, obsługiwanych przez usługi fabryka danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

### <a name="hello-partitionedby-property"></a>Właściwość partitionedBy Hello
Można określić dynamiczne **folderPath** i **fileName** właściwości dane szeregów czasowych z hello **partitionedBy** właściwości, funkcje fabryki danych i systemu zmienne. Aby uzyskać więcej informacji, zobacz hello [fabryki danych Azure — funkcje i zmienne systemu](data-factory-functions-variables.md) artykułu.


W hello poniższy przykład `{Slice}` zostanie zastąpiona wartością hello hello fabryki danych systemu zmiennej `SliceStart` w formacie hello określonym (`yyyyMMddHH`). Nazwa Hello `SliceStart` odwołuje się czas rozpoczęcia toohello hello wycinka. Witaj `folderPath` właściwość jest różne dla każdego wycinka jako w `wikidatagateway/wikisampledataout/2014100103` lub `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

W powitania po przykład, hello rok, miesiąc, dzień i czas `SliceStart` są wyodrębniane do oddzielnych zmiennych, które są używane przez hello `folderPath` i `fileName` właściwości:
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
Więcej szczegółów na zestawy danych szeregu czasowego, planowania i wycinków, zobacz hello [zestawów danych w fabryce danych Azure](data-factory-create-datasets.md) i [fabryki danych planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułów. 


## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Witaj właściwości dostępne w hello **typeProperties** sekcji działanie zależy od każdego typu działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

**AzureDataLakeStoreSource** obsługuje następujące właściwości w hello hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| **cykliczne** |Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu. |TRUE, False (wartość domyślna) |Nie |


**AzureDataLakeStoreSink** obsługuje następujące właściwości w hello hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| **copyBehavior** |Określa zachowanie kopii hello. |<b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello. Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.<br/><br/><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom hello folderu docelowego. pliki docelowe Hello są tworzone z nazwami wygenerowana automatycznie.<br/><br/><b>MergeFiles</b>: scala wszystkie pliki z pliku tooone folderu źródłowego hello. Witaj nazwę pliku lub obiektu blob jest określony, nazwa scalony plik hello będzie hello określonej nazwy. W przeciwnym razie hello nazwa pliku zostanie wygenerowana automatycznie. |Nie |

### <a name="recursive-and-copybehavior-examples"></a>Przykłady cyklicznego i copyBehavior
W tej sekcji opisano hello efekty hello operacji kopiowania dla różnych kombinacji wartości cyklicznej i copyBehavior.

| Cykliczne | copyBehavior | Efekty |
| --- | --- | --- |
| Wartość true |preserveHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello takie same struktury jako źródło hello<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| Wartość true |flattenHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>docelowy Hello Folder1 jest tworzony z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5 |
| Wartość true |mergeFiles |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>docelowy Hello Folder1 jest tworzony z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie generowanych automatycznie |
| wartość false |preserveHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/><br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |
| wartość false |flattenHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/><br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |
| wartość false |mergeFiles |Dla folderu źródłowego Folder1 z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie wygenerowany automatycznie. Nazwa wygenerowana automatycznie Plik1<br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |

## <a name="supported-file-and-compression-formats"></a>Obsługiwane formaty plików i kompresji
Aby uzyskać więcej informacji, zobacz hello [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykułu.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Przykłady JSON kopiowania tooand danych z usługi Data Lake Store
Następujące przykłady Hello zawierają definicje JSON. Te przykładowe definicje toocreate potoku można użyć przy użyciu hello [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Witaj przykładach pokazano, jak toocopy tooand danych z magazynu usługi Data Lake Store i obiektów Blob platformy Azure. Jednak dane mogą być kopiowane _bezpośrednio_ za pomocą dowolnego hello tooany źródeł z wychwytywanie hello obsługiwane. Aby uzyskać więcej informacji, zobacz sekcja hello "obsługiwane magazyny danych i formaty" w hello [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md) artykułu.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Przykład: Kopiowanie danych z magazynu obiektów Blob Azure tooAzure usługi Data Lake Store
Witaj przykładowy kod w tej sekcji przedstawiono:

* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Połączonej usługi typu [AzureDataLakeStore](#linked-service-properties).
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureDataLakeStore](#dataset-properties).
* A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [AzureDataLakeStoreSink](#copy-activity-properties).

Witaj przykładach pokazano, jak szeregów czasowych dane z magazynu obiektów Blob platformy Azure są kopiowane tooData Lake Store co godzinę. 

**Połączona usługa Azure Storage**

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

**Azure Data Lake Store połączona usługa**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#linked-service-properties) sekcji.
>

**Wejściowy zestaw danych obiektów blob platformy Azure**

W hello poniższy przykład, danych jest pobierana z obiektu blob nowe co godzinę (`"frequency": "Hour", "interval": 1`). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa hello rok, miesiąc i dzień część hello czas rozpoczęcia. Nazwa pliku Hello używa godzina hello część hello godzinę rozpoczęcia. Witaj `"external": true` ustawienie informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

**Azure Data Lake Store wyjściowy zestaw danych**

powitania po przykład kopii tooData usługi data Lake Store. Nowe dane są kopiowane tooData Lake Store co godzinę.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Działanie kopiowania w potoku źródła obiektów blob i ujście usługi Data Lake Store**

Poniższy przykład hello, potoku hello zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych. działanie kopiowania Hello jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello `source` typu ustawiono zbyt`BlobSource`i hello `sink` typu ustawiono zbyt`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Przykład: Kopiowanie danych z usługi Azure Data Lake Store tooan obiektów blob platformy Azure
Witaj przykładowy kod w tej sekcji przedstawiono:

* Połączonej usługi typu [AzureDataLakeStore](#linked-service-properties).
* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureDataLakeStore](#dataset-properties).
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [AzureDataLakeStoreSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Kod Hello kopiuje dane szeregów czasowych z tooan Data Lake — magazyn obiektów blob platformy Azure co godzinę. 

**Azure Data Lake Store połączona usługa**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#linked-service-properties) sekcji.
>

**Połączona usługa Azure Storage**

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
**Usługa Azure Data Lake wejściowy zestaw danych**

W tym przykładzie ustawienie `"external"` zbyt`true` informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
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
**Wyjściowy zestaw danych obiektów blob platformy Azure**

W hello poniższy przykład, dane są zapisywane nowego obiektu blob tooa co godzinę (`"frequency": "Hour", "interval": 1`). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa hello roku, miesiąc, dzień i godziny część hello czas rozpoczęcia.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Działanie kopiowania w potoku ze źródłem Azure Data Lake Store i ujście obiektów blob**

Poniższy przykład hello, potoku hello zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych. działanie kopiowania Hello jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello `source` typu ustawiono zbyt`AzureDataLakeStoreSource`i hello `sink` typu ustawiono zbyt`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

W definicji działania kopiowania hello można również mapować kolumn z powitania źródło zestawu danych toocolumns w zestawie hello ujścia danych. Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajności i dostosowywanie
toolearn czynniki hello, które mają wpływ na wydajność działania kopiowania i w jaki sposób toooptimize, zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) artykułu.
