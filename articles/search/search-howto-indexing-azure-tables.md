---
title: "aaaIndexing magazynu tabel Azure z usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooindex dane przechowywane w magazynie tabel platformy Azure z usługi Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Magazyn tabel Azure indeksu z usługi Azure Search
W tym artykule opisano, jak toouse usługi Azure Search tooindex danych przechowywanych w magazynie tabel Azure.

## <a name="set-up-azure-table-storage-indexing"></a>Konfigurowanie indeksowania magazynu tabel Azure

Można skonfigurować indeksator magazynu tabel Azure przy użyciu tych zasobów:

* [Witryna Azure Portal](https://ms.portal.azure.com)
* Usługa Azure Search [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Usługa Azure Search [zestawu .NET SDK](https://aka.ms/search-sdk)

W tym miejscu przedstawiony przepływu hello przy użyciu hello interfejsu API REST. 

### <a name="step-1-create-a-datasource"></a>Krok 1: Utworzenie źródła danych

Źródło danych określa, które tooindex danych hello poświadczeń potrzebnych tooaccess hello danych i zasady hello, umożliwiających wyszukiwanie Azure tooefficiently identyfikować zmiany danych hello.

Dla tabeli indeksowania, hello datasource musi mieć hello następujące właściwości:

- **Nazwa** jest hello unikatową nazwę źródła danych hello w ramach usługi wyszukiwania.
- **Typ** musi być `azuretable`.
- **poświadczenia** parametr zawiera parametry połączenia konta magazynu hello. Zobacz hello [Określ poświadczenia](#Credentials) sekcji, aby uzyskać szczegółowe informacje.
- **kontener** hello ustawia nazwę tabeli i opcjonalnie zapytania.
    - Określ nazwę tabeli hello przy użyciu hello `name` parametru.
    - Opcjonalnie określ zapytania przy użyciu hello `query` parametru. 

> [!IMPORTANT] 
> Jeśli to możliwe, użyj filtru na PartitionKey w celu poprawy wydajności. Inne zapytania wykonuje skanowanie pełne tabeli, co spowoduje niską wydajność dużych tabel. Zobacz hello [zagadnienia dotyczące wydajności](#Performance) sekcji.


toocreate źródła danych:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Aby uzyskać więcej informacji na powitania Utwórz źródło danych interfejsu API, zobacz [utworzyć źródło danych](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Sposoby toospecify poświadczeń ####

Możesz podać poświadczenia hello hello tabeli w jeden z następujących sposobów: 

- **Parametry połączenia konta magazynu pełny dostęp**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` można uzyskać hello parametry połączenia z hello portalu Azure będzie toohello **bloku konto magazynu** > **ustawienia**   >  **Klucze** (dla kont magazynu classic) lub **ustawienia** > **klucze dostępu** (dla zasobów Azure Menedżer kont magazynu).
- **Konto magazynu udostępnionego ciąg połączenia podpisu dostępu**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` sygnatury dostępu współdzielonego hello powinny mieć hello listę i uprawnienia do odczytu z kontenerów (tabele w tym przypadku) i obiektów (wiersze tabeli).
-  **Sygnatury dostępu współdzielonego tabeli**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` sygnatury dostępu współdzielonego hello powinni mieć uprawnienia zapytania (odczyt) w tabeli hello.

Aby uzyskać więcej informacji w magazynie udostępnionym sygnatur dostępu, zobacz [używanie sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Korzystając z poświadczeń sygnatury dostępu współdzielonego, konieczne będzie poświadczenia źródła danych hello tooupdate okresowo z tooprevent odnowionego podpisów ich wygaśnięciem. Po wygaśnięciu poświadczeń sygnatury dostępu współdzielonego, indeksatora hello zakończy się niepowodzeniem z komunikatem o błędzie podobny zbyt "poświadczenia dostarczone w parametrach połączenia hello są nieprawidłowe lub wygasły."  

### <a name="step-2-create-an-index"></a>Krok 2: Tworzenie indeksu
Indeks Hello określa hello pola w dokumencie atrybuty hello oraz innych konstrukcji środowiska wyszukiwania hello kształtu.

toocreate indeksu:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Aby uzyskać więcej informacji na temat tworzenia indeksów, zobacz [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Krok 3: Utwórz indeksator
Indeksator połączenie źródła danych z indeksem wyszukiwania docelowych i udostępnia zaplanowanym odświeżaniu danych hello tooautomate. 

Po utworzeniu hello indeks i źródło danych, wszystko jest gotowe toocreate hello indeksatora:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Ten indeksator jest uruchamiane co dwie godziny. (hello Interwał harmonogramu jest ustawiona zbyt "PT2H".) toorun indeksatora co 30 minut, ustawić interwał powitania także "PT30M". Witaj najkrótszy obsługiwany interwał to pięć minut. Harmonogram Hello jest opcjonalna. Pominięcie indeksatora działa tylko wtedy, gdy po jego utworzeniu. Można jednak uruchomić indeksatora na żądanie w dowolnym momencie.   

Aby uzyskać więcej informacji na powitania Utwórz indeksator interfejsu API, zobacz [Utwórz indeksator](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Postępowania w przypadku nazwy innego pola
Czasami hello nazwy pól w indeksie istniejących różnią się od nazwy właściwości hello w tabeli. Pole nazwy właściwości hello toomap mapowania z nazw pól toohello tabeli hello można użyć w indeksie wyszukiwania. toolearn więcej informacji na temat mapowania pól, zobacz [mapowań pól indeksator usługi Azure Search zestawiania hello różnice między źródeł danych i wyszukiwania indeksów](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Obsługa kluczy dokumentu
W usłudze Azure Search klucz dokumentu hello unikatowo identyfikuje dokumentu. Każdy indeks musi mieć dokładnie jedno pole klucza typu `Edm.String`. pole klucza Hello jest wymagane dla każdego dokumentu, który jest dodawany toohello indeksu. (W rzeczywistości jego hello tylko wymagane pola.)

Ponieważ wiersze tabeli klucza złożonego, usługi Azure Search generuje syntetycznych pole o nazwie `Key` jest złączeniem klucza i wiersza wartości kluczy partycji. Na przykład, jeśli wiersz PartitionKey jest `PK1` i RowKey `RK1`, następnie hello `Key` jest wartość pola `PK1RK1`.

> [!NOTE]
> Witaj `Key` wartość może zawierać znaków, które są nieprawidłowe w dokumencie kluczy, takich jak łączniki. Nieprawidłowe znaki mogą dotyczyć przy użyciu hello `base64Encode` [funkcja mapowania pól](search-indexer-field-mappings.md#base64EncodeFunction). Jeśli to zrobisz, pamiętaj tooalso użycie bezpiecznego adresu URL w formacie Base64 kodowania podczas przekazywania dokumentów kluczy w interfejsie API wywołuje takie jak wyszukiwanie.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Przyrostowe wykrywania indeksowanie i usuwaniem.
Po skonfigurowaniu toorun indeksatora tabeli, zgodnie z harmonogramem reindexes go tylko nowe lub zaktualizowane wierszy, zgodnie z wiersza `Timestamp` wartość. Nie masz toospecify zasady wykrywania zmian. Indeksowanie przyrostowe jest włączona automatycznie.

tooindicate to pewność, że dokumenty muszą zostać usunięte z indeksu hello, możesz użyć strategii usuwania nietrwałego. Zamiast usuwać wiersza, Dodaj tooindicate właściwości, który został usunięty i skonfigurować zasady usuwania nietrwałego wykrywania na powitania źródła danych. Na przykład następujące zasady hello uzna, że wiersz został usunięty, jeśli hello wiersz zawiera właściwości `IsDeleted` z wartością hello `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Zagadnienia dotyczące wydajności

Domyślnie usługi Azure Search korzysta powitania po Filtr kwerendy: `Timestamp >= HighWaterMarkValue`. Ponieważ na powitania w tabelach platformy Azure nie ma pomocniczy indeks `Timestamp` pola tego typu zapytań wymaga skanowania pełnego tabeli i dlatego jest wolny dla dużych tabel.


Poniżej przedstawiono dwa możliwe podejścia do zwiększania wydajności indeksowania tabeli. Obie metody zależy od używania partycji tabeli: 

- Jeśli dane mogą być partycjonowane naturalnie do kilku zakresów partycji, Utwórz źródło danych i odpowiedniego indeksatora dla każdego zakresu partycji. Każdy indeksator ma tooprocess tylko określonej partycji zakres, co zapewnia lepszą wydajność kwerend. Jeśli dane hello musi toobe indeksowane ma niewielkiej liczby partycji stały, jeszcze bardziej poprawić jakość: każdego indeksatora jest tylko skanowanie partycji. Na przykład toocreate źródła danych do przetwarzania zakres partycji z kluczy z `000` zbyt`100`, użyj zapytania następująco: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Jeśli dane jest podzielona na partycje według czasu (na przykład możesz utworzyć nową partycję, każdego dnia lub tygodnia), należy wziąć pod uwagę następujące podejście hello: 
    - Kwerenda formularza hello: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Monitorować postęp indeksatora za pomocą [uzyskać indeksatora API stanu](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)i co pewien czas zaktualizować hello `<TimeStamp>` warunku zapytania hello na podstawie hello najnowszych pomyślne-znacznik limitu górnego wartości. 
    - Z tej metody należy tootrigger pełną indeksowanie, należy najpierw tooreset hello źródła danych zapytania w dodanie tooresetting hello indeksatora. 


## <a name="help-us-make-azure-search-better"></a>Pomóż nam udoskonalić usługę Azure Search
Jeśli masz żądania funkcji lub pomysły dotyczące ulepszeń przesłać je w naszym [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
