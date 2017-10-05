---
title: 'Szybki start: Azure Machine Learning zalecenia API (wersja 1) | Dokumentacja firmy Microsoft'
description: "Azure Machine Learning zalecenia — Przewodnik Szybki Start"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a>Przewodnik szybkiego startu Machine Learning API zalecenia (wersja 1)

> [!NOTE]
> Należy zacząć korzystać [kognitywnych usługi interfejsu API zalecenia](https://www.microsoft.com/cognitive-services/recommendations-api) zamiast tej wersji. Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
>
> Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate).
> 
> 

W tym dokumencie opisano sposób dołączyć daną usługą lub aplikacją do użycia Microsoft Azure Machine Learning zalecenia. Więcej szczegółów można znaleźć w interfejsie API zalecenia w [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>Ogólne omówienie
Aby korzystać z usługi Azure Machine Learning zalecenia, należy wykonać następujące czynności:

* Tworzenie modelu — model jest kontenerem danych użycia, wykaz danych oraz model zalecenia.
* Importuj dane katalogu - katalogu zawiera informacje o metadanych dla elementów. 
* Importowanie danych użycia - dane użycia mogą być przekazywane w jeden z dwóch sposobów (lub obie):
  * Przekazując plik zawierający dane użycia.
  * Wysyła zdarzenia pozyskiwania danych.
    Zwykle możesz przekazać plik użycia, aby można było utworzyć model zalecenie początkowego (bootstrap) i używać go, dopóki system zbiera wystarczającej ilości danych przy użyciu formatu pozyskiwania danych.
* Tworzenie modelu zalecenie — jest to operacja asynchroniczna, w którym system zalecenie pobierze dane użycia i tworzy model zalecenie. Ta operacja może zająć kilka minut lub kilka godzin w zależności od rozmiaru danych i parametry konfiguracji kompilacji. W przypadku wyzwalają kompilacji, otrzyma identyfikatora dla kompilacji. Użyj, aby sprawdzić podczas procesu kompilacji zostało zakończone przed rozpoczęciem korzystania zalecenia.
* Używać zalecenia - Get zalecenia dotyczące określonego elementu lub listy elementów.

Powyższe kroki są wykonywane za pomocą interfejsu API usługi Azure Machine Learning zalecenia.  Możesz pobrać przykładowej aplikacji, która implementuje każdy z tych kroków z [również galerii.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>Ograniczenia
* Maksymalna liczba modeli dla subskrypcji wynosi 10.
* Maksymalna liczba elementów, które mogą zawierać wykaz wynosi 100 000.
* Maksymalna liczba punktów użycia, które są zachowane jest ~ 5,000,000. Najstarszych zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.
* Maksymalny rozmiar danych, które mogą być wysyłane w POST (na przykład importu wykazu danych, importowanie danych użycia) to 200MB.
* Liczba transakcji na sekundę dla kompilacji modelu zalecenie, która nie jest aktywny jest ~ 2TPS. Zalecenie kompilacji modelu, który jest aktywny można przechowywać w do 20TPS.

## <a name="integration"></a>Integracja
### <a name="authentication"></a>Authentication
Microsoft Azure Marketplace obsługuje podstawowe lub OAuth metodę uwierzytelniania. Klucze konta można łatwo znaleźć przechodząc do kluczy w witrynie marketplace w obszarze [ustawienia konta](https://datamarket.azure.com/account/keys). 

#### <a name="basic-authentication"></a>Uwierzytelnianie podstawowe
Dodaj nagłówek autoryzacji:

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

Konwertuj do formatu Base64 (C#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

Konwertuj do formatu Base64 (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>Identyfikator URI usługi
Identyfikator URI dla interfejsów API usługi Azure Machine Learning zalecenia katalogu głównego usługi jest [tutaj.](https://api.datamarket.azure.com/amla/recommendations/v2/)

Pełny identyfikator URI usługi jest wyrażona za pomocą elementów ze specyfikacją OData.

### <a name="api-version"></a>Wersja interfejsu API
Każde wywołanie interfejsu API będzie mieć na końcu, parametr zapytania o nazwie apiVersion, który powinien być ustawiony na "1.0".

### <a name="ids-are-case-sensitive"></a>Identyfikatory jest rozróżniana wielkość liter
Identyfikatory zwrócony przez żadnego z interfejsów API, jest rozróżniana wielkość liter i powinien być używany jako takie, gdy dane są przekazywane jako parametry w kolejnych wywołaniach interfejsu API. Na przykład identyfikatory modelu i identyfikatory katalogu jest rozróżniana wielkość liter.

### <a name="create-a-model"></a>Tworzenie modelu
Tworzenie żądania "Tworzenie modelu":

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelName |Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.<br>Maksymalna długość: 20 |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

* `feed/entry/content/properties/id`-Zawiera identyfikator modelu.
  Należy pamiętać, że identyfikator modelu jest rozróżniana wielkość liter.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a>Importuj dane katalogu
Kilka plików wykazu podczas przesyłania do tego samego modelu z kilka wywołań, firma Microsoft będzie wstawić tylko nowych elementów katalogu. Istniejące elementy pozostanie z oryginalnych wartości.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter) |
| Nazwa pliku |Tekstowy identyfikator katalogu.<br>Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.<br>Długość maksymalna: 50 |
| apiVersion |1.0 |
|  | |
| Treść żądania |Wykazu danych. Format:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Nazwa</th><th>Obowiązkowy</th><th>Typ</th><th>Opis</th></tr><tr><td>Identyfikator elementu</td><td>Tak</td><td>Alfanumeryczne, maksymalna długość 50</td><td>Unikatowy identyfikator elementu</td></tr><tr><td>Nazwa elementu</td><td>Tak</td><td>Alfanumeryczne, maksymalną długość 255 znaków</td><td>Nazwa elementu</td></tr><tr><td>Kategoria elementu</td><td>Tak</td><td>Alfanumeryczne, maksymalną długość 255 znaków</td><td>Kategoria, do którego ten element należy (na przykład gotowania książek teatralne...)</td></tr><tr><td>Opis</td><td>Nie</td><td>Alfanumeryczne, maksymalna długość 4000</td><td>Opis tego elementu</td></tr></table><br>Maksymalny rozmiar pliku to 200MB.<br><br>Przykład:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**Odpowiedź**:

Kod stanu HTTP: 200

* `Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.
* `Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione z powodu błędu.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a>Importowanie danych użycia
#### <a name="uploading-a-file"></a>Przekazywanie pliku
W tej sekcji pokazano, jak przekazywać dane użycia przy użyciu pliku. Można wywołać tego interfejsu API z danych użycia. Wszystkie dane użycia są zapisywane dla wszystkich wywołań.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter) |
| Nazwa pliku |Tekstowy identyfikator katalogu.<br>Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.<br>Długość maksymalna: 50 |
| apiVersion |1.0 |
|  | |
| Treść żądania |Dane użycia. Format:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nazwa</th><th>Obowiązkowy</th><th>Typ</th><th>Opis</th></tr><tr><td>Identyfikator użytkownika</td><td>Tak</td><td>Alfanumeryczne</td><td>Unikatowy identyfikator użytkownika</td></tr><tr><td>Identyfikator elementu</td><td>Tak</td><td>Alfanumeryczne, maksymalna długość 50</td><td>Unikatowy identyfikator elementu</td></tr><tr><td>Time</td><td>Nie</td><td>Data w formacie: RRRR/MM/ddtgg (na przykład 2013/06/20T10:00:00)</td><td>Czas danych</td></tr><tr><td>Wydarzenie</td><td>Nie, jeśli podane, również umieścić daty</td><td>Jeden z następujących czynności:<br>• Kliknij przycisk<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Zakupu</td><td></td></tr></table><br>Maksymalny rozmiar pliku to 200MB.<br><br>Przykład:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Odpowiedź**:

Kod stanu HTTP: 200

* `Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.
* `Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione z powodu błędu.
* `Feed\entry\content\properties\FileId`— Identyfikator pliku.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a>Przy użyciu danych
W tej sekcji przedstawiono sposób wysyłania zdarzeń w czasie rzeczywistym do Azure Machine Learning zalecenia, zazwyczaj z witryny sieci Web.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Treść żądania |Wpis danych zdarzeń dla każdego zdarzenia, które chcesz wysyłać. Należy wysłać do tej samej sesji użytkownika lub przeglądarki ten sam identyfikator w polu identyfikatora sesji. (Zobacz przykład treści zdarzenia poniżej). |

* Przykład dla zdarzenia "Kliknij przycisk":
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Przykład dla zdarzenia "RecommendationClick":
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Przykład dla zdarzenia "AddShopCart":
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Przykład dla zdarzenia "RemoveShopCart":
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Przykład dla zdarzenia "Zakupu":
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* Przykład wysyłania 2 zdarzenia "kliknij" a "AddShopCart":
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Odpowiedź**: kod stanu HTTP: 200

### <a name="build-a-recommendation-model"></a>Tworzenie modelu zalecenia
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter) |
| userDescription |Tekstowy identyfikator katalogu. Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego. Zobacz przykład powyżej.<br>Długość maksymalna: 50 |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Jest to interfejs API asynchronicznego. Otrzymasz identyfikator kompilacji w odpowiedzi. Aby wiedzieć, kiedy Kompilacja została zakończona, należy wywołać interfejs API "Pobierz kompilacje stan modelu" i zlokalizuj identyfikator tej kompilacji w odpowiedzi. Należy pamiętać, że kompilacji może potrwać od minut godzin w zależności od rozmiaru danych.

Nie można używać zalecenia do kompilacji kończy się.

Stan prawidłowy kompilacji:

* Utwórz — Model został utworzony.
* W kolejce — zostało wyzwolone kompilacji modelu i jest w kolejce.
* Kompilowanie — Model została skompilowana.
* Powodzenie — kompilacja zakończyła się pomyślnie.
* Błąd — Kompilacja została zakończona z błędem.
* Anulowane — Kompilacja została anulowana.
* Anulowanie — Kompilacja została anulowana.

Należy pamiętać, że identyfikator kompilacji można znaleźć w następującej ścieżce:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a>Pobierz stan kompilacji modelu
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter) |
| onlyLastBuild |Wskazuje, czy mają być zwracane całą historię kompilacji modelu lub tylko stan ostatniej kompilacji. |
| apiVersion |1.0 |

**Odpowiedź**:

Kod stanu HTTP: 200

Odpowiedź zawiera jednego wpisu na kompilacji. Każdy wpis ma następujące dane:

* `feed/entry/content/properties/UserName`— Nazwa użytkownika.
* `feed/entry/content/properties/ModelName`— Nazwa modelu.
* `feed/entry/content/properties/ModelId`— Unikatowy identyfikator modelu.
* `feed/entry/content/properties/IsDeployed`— Czy kompilacja zostaje wdrożona () aktywne kompilacji).
* `feed/entry/content/properties/BuildId`— Unikatowy identyfikator kompilacji.
* `feed/entry/content/properties/BuildType`— Typ kompilacji.
* `feed/entry/content/properties/Status`— Stan kompilacji. Może być jedną z następujących czynności: błąd, kompilowanie, w kolejce, Cancelling anulowane, Powodzenie
* `feed/entry/content/properties/StatusMessage`— Komunikat szczegółowy stan (dotyczy tylko określone stany).
* `feed/entry/content/properties/Progress`— Utwórz postępu (%).
* `feed/entry/content/properties/StartTime`— Godzina rozpoczęcia kompilacji.
* `feed/entry/content/properties/EndTime`— Czas zakończenia kompilacji.
* `feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.
* `feed/entry/content/properties/ProgressStep`— Szczegóły dotyczące bieżącego etapu należącego do kompilacji w toku.

Stan prawidłowy kompilacji:

* Utworzono — wpis żądanie kompilacji zostało utworzone.
* W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.
* Kompilowanie — kompilacji jest w toku.
* Powodzenie — kompilacja zakończyła się pomyślnie.
* Błąd — Kompilacja została zakończona z błędem.
* Anulowane — Kompilacja została anulowana.
* Anulowanie — Kompilacja została anulowana.

Prawidłowe wartości dla typu kompilacji:

* Ranga - rangę kompilacji. (Rank kompilacji szczegółowe informacje, można znaleźć w dokumencie "Machine Learning zalecenie interfejsu API dokumentacji").
* Zalecenie - zalecenie kompilacji.
* Zmianie wysokości progów - zakupione razem często kompilacji.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a>Uzyskaj zalecenia
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter) |
| identyfikatory elementów |Rozdzielana przecinkami lista elementów zalecanie dla.<br>Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

Odpowiedź zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie rozsądkiem (na przykład zalecenie wyjaśnienia).

OData XML

Przykład odpowiedzi poniżej zawiera 10 elementów zalecane:

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a>Aktualizuj model
Możesz zaktualizować opis modelu lub identyfikator active kompilacji.
*Identyfikator kompilacji Active* -każdej kompilacji dla każdego modelu ma identyfikator kompilacji. Identyfikator active kompilacji jest pomyślnego tworzenia pierwszej kompilacji każdego nowego modelu. Gdy masz identyfikator kompilacji active i wykonaniu dodatkowych kompilacji w ramach tego samego modelu, musisz jawnie ustaw go jako domyślny identyfikator kompilacji Jeśli chcesz. Gdy zalecenia, można korzystać, jeśli nie określisz identyfikator kompilacji, który ma być używany, domyślny zostanie użyty automatycznie.

Mechanizm ten umożliwia — po utworzeniu modelu zalecenia w środowisku produkcyjnym — do tworzenia nowych modeli i testowane przed Przenieś do produkcji.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| UMIEŚĆ |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| id |Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter) |
| apiVersion |1.0 |
|  | |
| Treść żądania |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>Należy pamiętać, że tagi XML, opis i ActiveBuildId są opcjonalne. Jeśli nie chcesz ustawić opis lub ActiveBuildId, usuń cały tag. |

**Odpowiedź**:

Kod stanu HTTP: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>Informacje prawne
Niniejszy dokument jest udostępniany "jako — jest". Informacje i poglądy wyrażone w tym dokumencie, w tym adresy URL i innymi odwołaniami do witryn internetowych, mogą ulec zmianie bez uprzedzenia. Niektóre przedstawione przykłady są udostępniane tylko do celów ilustracyjnych i są fikcyjne. Żadne rzeczywiste skojarzenia ani połączenia jest przeznaczony lub powinny być zakładane. Ten dokument nie daje użytkownikowi żadnych praw do jakiejkolwiek własności intelektualnej związanej z jakimkolwiek produktem firmy Microsoft. Można kopiować i używać tego dokumentu do wewnętrznych celów referencyjnych. © 2014 Microsoft. Wszelkie prawa zastrzeżone. 

