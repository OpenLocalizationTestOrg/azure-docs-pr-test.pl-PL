---
title: aaaMachine dokumentacji interfejsu API uczenia zalecenia | Dokumentacja firmy Microsoft
description: "Dokumentacji platformy Azure Machine Learning API zalecenia dla aparatu zalecenia, dostępne w hello Microsoft Azure Marketplace."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Dokumentacja dotycząca interfejsu API zaleceń usługi Azure Machine Learning
> [!NOTE]
> Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji. Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)
> 
> 

Ten dokument przedstawia interfejsów API firmy Microsoft usługi Azure Machine Learning zalecenia.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Ogólne omówienie
Ten dokument jest odwołanie do interfejsu API. Należy rozpocząć hello "Azure Machine Learning zalecenie — Szybki Start" dokumentu.

Hello Azure Machine Learning zalecenia API można podzielić na następujące grupy logiczne hello:

* <ins>Ograniczenia</ins> — ograniczenia interfejsu API zalecenia.
* <ins>Informacje ogólne</ins> -informacji dotyczących uwierzytelniania, z identyfikatora URI i przechowywania wersji.
* <ins>Model Basic</ins> -interfejsów API, które umożliwiają toodo hello podstawowe operacje na modelu (np. Tworzenie, aktualizowanie i usuwanie modelu).
* <ins>Model zaawansowane</ins> -interfejsów API, które umożliwiają tooget zaawansowane wgląd w danych na powitania modelu.
* <ins>Model reguły biznesowe</ins> -interfejsów API, które umożliwiają toomanage reguły biznesowe na powitania modelu zalecenie wyniki.
* <ins>Katalog</ins> -interfejsów API, które umożliwiają toodo podstawowe operacje w wykazie modelu. Katalog zawiera informacje o metadanych na elementach hello hello danych użycia.
* <ins>Funkcja</ins> -interfejsy API umożliwiające tooget wgląd w elemencie do katalogu hello i w jaki sposób toouse zalecenia lepsze toobuild informacji.
* <ins>Dane użycia</ins> -interfejsów API, które umożliwiają toodo podstawowe operacje na danych użycia hello modelu. Dane użycia w podstawowej postaci hello składa się z wierszy, które obejmują pary &#60; userId &#62; &#60; identyfikator elementu &#62;.
* <ins>Tworzenie</ins> — Tworzenie interfejsów API, które umożliwiają tootrigger modelu i czy podstawowe operacje, które są powiązane toothis kompilacji. Po utworzeniu użycia cennych danych, można wyzwolić kompilację modelu.
* <ins>Zalecenie</ins> -interfejsów API, które umożliwiają zalecenia tooconsume po zakończeniu kompilacji hello modelu.
* <ins>Dane użytkownika</ins> -interfejsów API, które umożliwiają toofetch informacji na temat danych użycia hello użytkownika.
* <ins>Powiadomienia</ins> -tooyour interfejsu API operacji związanych z interfejsów API, które umożliwiają powiadomienia tooreceive problemów. (Na przykład możesz są raportowania danych użycia przez gromadzenia danych i większość zdarzeń hello przetwarzania kończą się niepowodzeniem. Powiadomienie o błędzie zostanie wygenerowany.)

## <a name="2-limitations"></a>2. Ograniczenia
* Maksymalna liczba modeli na subskrypcję Hello wynosi 10.
* Maksymalna liczba kompilacji na model w Hello wynosi 20.
* Hello maksymalną liczbę elementów, które mogą zawierać wykaz wynosi 100 000.
* Maksymalna liczba punktów użycia, które są zachowane w Hello jest ~ 5,000,000. Hello najstarsze zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.
* Maksymalny rozmiar danych, które mogą być wysyłane w POST (np. import wykazu danych, importowanie danych użycia) Hello jest 200MB.
* Maksymalna liczba elementów, które może zostać wyświetlony monit o podanie podczas pobierania zalecenia Hello wynosi 150.

## <a name="3-apis---general-information"></a>3. Interfejsy API — informacje ogólne
### <a name="31-authentication"></a>3.1. Authentication
Wykonaj hello Microsoft Azure Marketplace wytyczne dotyczące uwierzytelniania. Hello marketplace obsługuje każdej hello Basic lub OAuth z metod uwierzytelniania.

### <a name="32-service-uri"></a>3.2. Identyfikator URI usługi
główny usługi Hello identyfikatora URI dla interfejsów API usługi Azure Machine Learning zalecenia hello jest [tutaj.](https://api.datamarket.azure.com/amla/recommendations/v3/)

Identyfikator URI usługi pełne Hello jest wyrażona za pomocą elementów hello specyfikację OData.  

### <a name="33-api-version"></a>3.3. Wersja interfejsu API
Każde wywołanie interfejsu API na końcu hello ma parametr zapytania o nazwie apiVersion, który powinien być ustawiony too1.0.

### <a name="34-ids-are-case-sensitive"></a>3.4. Identyfikatory jest uwzględniana wielkość liter
Identyfikatory zwrócony przez żadnego z interfejsów API, hello jest uwzględniana wielkość liter i powinien być używany jako takie, gdy dane są przekazywane jako parametry w kolejnych wywołaniach interfejsu API. Na przykład identyfikatory modelu i identyfikatory katalogu jest uwzględniana wielkość liter.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Zalecenia dotyczące jakości i zimnych elementów
### <a name="41-recommendation-quality"></a>4.1. Zalecenie jakości
Tworzenie modelu zalecenie jest zwykle zalecenia tooprovide za mało tooallow hello systemu. Niemniej jednak jakości zalecenia w zależności od użycia hello przetwarzane i hello pokrycia hello katalogu. Na przykład jeśli masz wiele zimnych elementów (bez użycia znaczących) systemu hello będziesz mieć trudności udostępnia zalecenia dla takiego elementu lub przy użyciu takiego elementu jako zalecana. W kolejności tooovercome hello zimnych elementu problem hello systemu umożliwia wykorzystanie hello metadanych hello elementów tooenhance hello zalecenia. Te metadane stanowią tooas określonej funkcji. Typowe funkcje są książki autora lub filmu aktora. Funkcje są udostępniane za pośrednictwem katalogu hello w postaci hello klucza i wartości ciągów. Hello pełny format pliku wykazu hello, można znaleźć w artykule toohello [zaimportować sekcja katalogu](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. Rank kompilacji
Funkcji można zwiększyć hello zalecenie modelu, ale toodo wymaga hello użycie funkcji łatwy do rozpoznania. W tym celu wprowadzono nową kompilację — rangi kompilacji. Ta kompilacja zostanie rank powitania użyteczność funkcji. Funkcja łatwy do rozpoznania to funkcja z rangę 2 lub nowszej.
Po zrozumienia, które funkcji hello są przydatne, wyzwolić kompilację zalecenie z listy hello (lub podlisty) łatwy do rozpoznania funkcji. Jest to możliwe toouse, tych funkcji do rozszerzenia hello elementów ciepłych i zimnych elementów. W kolejności toouse ich elementów ciepłych hello `UseFeatureInModel` parametru kompilacji powinny zostać skonfigurowane. W funkcji toouse kolejność elementów zimnych, hello `AllowColdItemPlacement` parametru kompilacji powinno być włączone.
Uwaga: Nie jest możliwe tooenable `AllowColdItemPlacement` bez włączania `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Zalecenie logikę
Rozsądkiem zalecenie jest innym aspektem użycie funkcji. W rzeczywistości hello Azure Machine Learning zalecenia aparat można użyć funkcji tooprovide zalecenie wyjaśnienia () uzasadnienie), prowadzące toomore zaufania w hello zalecane elementu z hello zalecenie konsumenta.
tooenable uzasadnienie, hello `AllowFeatureCorrelation` i `ReasoningFeatureList` parametry powinny mieć toorequesting poprzednie ustawienia kompilacji zalecenia.

## <a name="5-model-basic"></a>5. Basic modelu
### <a name="51-create-model"></a>5.1. Tworzenie modelu
Tworzy żądanie "Tworzenie modelu".

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

* `feed/entry/content/properties/id`-Zawiera identyfikator hello modelu.
  **Uwaga**: identyfikator modelu jest rozróżniana wielkość liter.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a>5.2. Pobierz modelu
Tworzy żądanie "get modelu".

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| id |Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter) |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Witaj modelu danych można znaleźć w hello następujące elementy:

* `feed/entry/content/properties/Id`-Model unikatowego identyfikatora.
* `feed/entry/content/properties/Name`-Nazwa modelu.
* `feed/entry/content/properties/Date`-Data utworzenia modelu.
* `feed/entry/content/properties/Status`-Stan modelu. Jedną z następujących hello:
  * Utworzone — Model jest tworzony i nie zawiera katalogu i użycia.
  * ReadyForBuild — Model jest tworzony i zawiera katalog i użycia.
* `feed/entry/content/properties/HasActiveBuild`— Wskazuje, czy hello model został utworzony pomyślnie.
* `feed/entry/content/properties/BuildId`-Identyfikator modelu active kompilacji.
* `feed/entry/content/properties/Mpr`-Model klasyfikacji średniej percentyl (MPR — Aby uzyskać więcej informacji, zobacz ModelInsight).
* `feed/entry/content/properties/UserName`-Nazwa użytkownika wewnętrznego modelu.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Pobierz wszystkie modele
Pobiera wszystkie modele hello bieżącego użytkownika.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

* `feed/entry/content/properties/Id`-Model unikatowego identyfikatora.
* `feed/entry/content/properties/Name`-Nazwa modelu.
* `feed/entry/content/properties/Date`-Data utworzenia modelu.
* `feed/entry/content/properties/Status`-Stan modelu. Jedną z następujących hello:
  * Utworzone — Model jest tworzony i nie zawiera katalogu i użycia.
  * ReadyForBuild — Model jest tworzony i zawiera katalog i użycia.
* `feed/entry/content/properties/HasActiveBuild`— Wskazuje, czy hello model został utworzony pomyślnie.
* `feed/entry/content/properties/BuildId`-Identyfikator modelu active kompilacji.
* `feed/entry/content/properties/Mpr`-Model MPR (więcej informacji zawiera ModelInsight).
* `feed/entry/content/properties/UserName`-Nazwa użytkownika wewnętrznego modelu.
* `feed/entry/content/properties/UsageFileNames`— Lista plików użycia modelu rozdzielonych przecinkami.
* `feed/entry/content/properties/CatalogId`-Identyfikator modelu katalogu.
* `feed/entry/content/properties/Description`-Opis modelu.
* `feed/entry/content/properties/CatalogFileName`-Nazwa pliku katalogu modelu.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Aktualizuj Model
Możesz zaktualizować opis modelu hello lub hello identyfikator active kompilacji.<br>
<ins>Identyfikator kompilacji Active</ins> -każdej kompilacji dla każdego modelu ma identyfikator kompilacji. Identyfikator kompilacji active Hello jest hello pierwszym pomyślnym kompilacji każdego nowego modelu. Gdy masz identyfikator active kompilacji i wykonaj dodatkowe kompilacje dla hello samego modelu należy tooexplicitly ustaw go jako hello domyślne kompilacji identyfikator aby. Jeśli zalecenia, korzystać w sytuacji, jeśli nie określono Identyfikatora kompilacji hello, który ma toouse, domyślne hello, co zostanie użyta automatycznie.<br>
Mechanizm ten umożliwia — po modelu zalecenia w środowisku produkcyjnym — toobuild nowe modele i testowane przed podwyższeniem ich tooproduction.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| UMIEŚĆ |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| id |Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter) |
| apiVersion |1.0 |
|  | |
| Treść żądania |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Należy pamiętać, że hello XML znaczniki opis i ActiveBuildId są opcjonalne. Jeśli nie chcesz, aby tooset opis lub ActiveBuildId, usuń cały tag hello. |

**Odpowiedź**:

Kod stanu HTTP: 200

### <a name="55----delete-model"></a>5.5.    Usuń Model
Usuwa istniejącego modelu według identyfikatora.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| id |Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter) |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Zaawansowane modelu
### <a name="61----model-data-insight"></a>6.1.    Szczegółowe informacje o modelu danych
Zwraca dane statystyczne hello użycia danych, których ten model został skompilowany.

Dostępna tylko w przypadku kompilacji zalecenia.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Witaj, dane są zwracane jako zbiór właściwości.

* `feed/entry/id/content/properties/key`-Zawiera nazwę właściwości hello.
* `feed/entry/id/content/properties/value`-Zawiera wartość właściwości hello.

Witaj w poniższej tabeli przedstawiono hello wartość, która reprezentuje każdy klucz.

| Klucz | Opis |
|:--- |:--- |
| AvgItemLength |Średnia liczba unikatowych użytkowników, dla każdego elementu. |
| AvgUserLength |Średnia liczba unikatowych elementów dla każdego użytkownika. |
| DensificationNumberOfItems |Liczba elementów po elementach oczyszczania, które nie mogą być modelowane. |
| DensificationNumberOfUsers |Liczba punktów użycia po oczyszczania użytkowników i elementy, które nie mogą być modelowane. |
| DensificationNumberOfRecords |Liczba punktów użycia po oczyszczania użytkowników i elementy, które nie mogą być modelowane. |
| MaxItemLength |Liczba unikatowych użytkowników dla elementu najpopularniejszych hello. |
| MaxUserLength |Maksymalna liczba unikatowych elementów dla użytkownika. |
| MinItemLength |Maksymalna liczba różnych użytkowników dla elementu. |
| MinUserLength |Minimalna liczba unikatowych elementów dla użytkownika. |
| RawNumberOfItems |Liczba elementów w plikach użycia hello. |
| RawNumberOfUsers |Liczba punktów użycia przed żadnych oczyszczania. |
| RawNumberOfRecords |Liczba punktów użycia przed żadnych oczyszczania. |
| SamplingNumberOfItems |Nie dotyczy |
| SamplingNumberOfRecords |Nie dotyczy |
| SamplingNumberOfUsers |Nie dotyczy |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Szczegółowe informacje o modelu
Zwraca model szczegółowe informacje o kompilacji active hello lub (jeśli istnieje) w ramach określonej kompilacji.

Dostępna tylko w przypadku kompilacji zalecenia.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |O identyfikatorze active kompilacji:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>O identyfikatorze określonej kompilacji:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| identyfikatora buildId |Opcjonalne — liczba, która identyfikuje pomyślnego utworzenia kompilacji. |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Witaj, dane są zwracane jako zbiór właściwości.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

Witaj w poniższej tabeli przedstawiono hello wartość, która reprezentuje każdy klucz.

| Klucz | Opis |
|:--- |:--- |
| CatalogCoverage |Jaka część hello katalogu może być modelowane z wzorców użycia. Witaj pozostałe elementy hello należy funkcje na podstawie zawartości. |
| MPR |Oznacza klasyfikacji percentyl hello modelu. Dolna jest lepszym rozwiązaniem. |
| NumberOfDimensions |Liczba wymiarów używanych przez algorytm factorization macierzy hello. |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Pobierz przykładowe modelu
Pobiera próbkę hello zalecenie modelu.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>O identyfikatorze określonej kompilacji:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

OData XML

Odpowiedź zostanie zwrócona w formacie tekstowym raw:

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Reguły biznesowe modelu
Są to typy hello reguł obsługiwane:

* <strong>BlockList</strong> -BlockList umożliwia tooprovide listę elementów, które chcesz tooreturn w wynikach zalecenie hello. 
* <strong>FeatureBlockList</strong> — funkcja BlockList umożliwia możesz tooblock elementy na podstawie wartości hello jego funkcje.

*Nie wysyłaj więcej niż 1000 pozycji w regule pojedynczego blocklist lub wywołania mogą limitu czasu. Jeśli potrzebujesz tooblock więcej niż 1000 pozycji, można wprowadzić kilka wywołań blocklist.*

* <strong>Upsale</strong> -Upsale umożliwia tooenforce tooreturn elementów w wynikach zalecenie hello.
* <strong>Lista dozwolonych adresów</strong> — umożliwia białą listę tooonly możesz Sugeruj zalecenia z listy elementów.
* <strong>FeatureWhiteList</strong> — funkcja białą listę umożliwia tooonly zaleca się elementy, które mają wartości określonych funkcji.
* <strong>PerSeedBlockList</strong> — na zablokowanych inicjatora umożliwia tooprovide na element listę elementów, które nie może być zwracany jako wyniki zalecenie.

### <a name="71----get-model-rules"></a>7.1.    Pobieranie reguł modelu
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Przykład:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

* `feed/entry/content/properties/Id`-Unikatowy identyfikator tej reguły.
* `feed/entry/content/properties/Type`-Typ reguły hello.
* `feed/entry/content/properties/Parameter`-Parametr reguły.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Dodaj regułę
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| NAGŁÓWEK |`"Content-Type", "text/xml"` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Treść żądania | |

<ins>Zawsze, gdy w przypadku reguł biznesowych, zapewniając identyfikatory elementów, upewnij się, że toouse hello zewnętrznych identyfikator elementu hello (hello na tym samym identyfikatorze używanego w pliku wykazu hello)</ins><br>
<ins>Reguła BlockList tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>Reguła FeatureBlockList tooadd:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>Reguła Upsale tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd regułę listy dozwolonych adresów IP:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>Reguła FeatureWhiteList tooadd:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>Reguła PerSeedBlockList tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Odpowiedź**:

Kod stanu HTTP: 200

Witaj interfejsu API zwraca hello nowo utworzona reguła z jego szczegółami. Właściwości reguł Hello mogą być pobierane z hello następującej ścieżki:

* `feed/entry/content/properties/Id`-Unikatowy identyfikator tej reguły.
* `feed/entry/content/properties/Type`-Typ reguły hello: BlockList lub Upsale.
* `feed/entry/content/properties/Parameter`-Parametr reguły.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Usuń regułę
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| wartości filterId |Unikatowy identyfikator hello filtru |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

### <a name="74----delete-all-rules"></a>7.4.    Usuń wszystkie reguły
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

## <a name="8-catalog"></a>8. Katalogu
### <a name="81----import-catalog-data"></a>8.1.    Importuj dane katalogu
Po wysłaniu kilka katalogu plików toohello sam model z kilka wywołań możemy zostanie wstawiona tylko hello nowych elementów katalogu. Istniejące elementy pozostanie z hello oryginalnych wartości. Nie można zaktualizować katalogu danych za pomocą tej metody.

dane wykazu Hello należy stosować hello następującego formatu:

* Bez funkcji-`<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* Dzięki funkcjom-`<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Uwaga: hello maksymalny rozmiar pliku to 200MB.

** Formatuj szczegóły **

| Nazwa | Obowiązkowy | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Identyfikator elementu |Tak |[A-z], [a-z], [0-9] [_] &#40; Podkreślenie &#41; [-] &#40; Dash &#41;<br> Długość maksymalna: 50 |Unikatowy identyfikator elementu. |
| Nazwa elementu |Tak |Dowolne znaki alfanumeryczne<br> Maksymalna długość: 255 |Nazwa elementu. |
| Kategoria elementu |Tak |Dowolne znaki alfanumeryczne <br> Maksymalna długość: 255 |Kategoria toowhich ten element należy (np. gotowania książki teatralne...); może być pusta. |
| Opis |Nie, chyba, że funkcje są istnieje (ale nie może być puste) |Dowolne znaki alfanumeryczne <br> Maksymalna długość: 4000 |Opis tego elementu. |
| Lista funkcji |Nie |Dowolne znaki alfanumeryczne <br> Maksymalna długość: 4000; Maksymalna liczba funkcji: 20 |Rozdzielana przecinkami lista nazwy funkcji = wartość funkcji, które mogą być używane tooenhance modelu zalecenia; zobacz [Tematy zaawansowane](#2-advanced-topics) sekcji. |

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| NAGŁÓWEK |`"Content-Type", "text/xml"` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Nazwa pliku |Identyfikator tekstową hello katalogu.<br>Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.<br>Długość maksymalna: 50 |
| apiVersion |1.0 |
|  | |
| Treść żądania |Przykład: (funkcje):<br/>Tworzenie Clara Callan książki, opis książki hello, 2406e770-769c-4189-89de-1c9283f93a96, = Richard Wright publisher = Kanady Flamingo Harper, roku = 2001<br>hello 21bf8088-b6c0-4509-870c-e1c7ac78304a, miejsca Forgetting: A fikcja (książka Byzantium), książki,, autora = Nick Bantock wydawcy = Harpercollins, rok = 1997<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23, Spadework, książki,, autora = Findley Tymotka publisher = Kanada HarperFlamingo roku = 2001<br>552a1940-21e4-4399-82bb-594b46d7ed54, ograniczenia bestii, książki, opis książki hello, tworzyć = młynów Magnus publisher = publikowania gier roku = 1998</pre> |

**Odpowiedź**:

Kod stanu HTTP: 200

Witaj interfejsu API zwraca raportu hello importu.

* `feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.
* `feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione ze względu na błąd tooan.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Pobierz katalogu
Pobiera wszystkie elementy katalogu.
katalogu Hello będzie można pobrać jedną stronę w czasie. Jeśli chcesz elementów tooget od określonego indeksu można użyć parametru odata hello $skip. Na przykład elementów tooget, zaczynając od pozycji 100, należy dodać parametr hello $skip = 100 toohello żądania.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu katalogu. Każdy wpis ma hello następujące dane:

* `feed/entry/content/properties/ExternalId`— Identyfikator zewnętrznego elementu katalogu, hello dostarczonego przez powitania klienta.
* `feed/entry/content/properties/InternalId`-Katalogu wewnętrzny identyfikator elementu hello generowany Azure Machine Learning zalecenia.
* `feed/entry/content/properties/Name`-Nazwa elementu katalogu.
* `feed/entry/content/properties/Category`-Kategoria elementu katalogu.
* `feed/entry/content/properties/Description`-Opis elementu katalogu.
* `feed/entry/content/properties/Metadata`-Katalogu metadanych elementu.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Pobrać elementów wykazu przez Token
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Token |Token nazwy element hello katalogu. Powinien zawierać co najmniej 3 znaki. |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu katalogu. Każdy wpis ma hello następujące dane:

* `feed/entry/content/properties/InternalId`-Katalogu wewnętrzny identyfikator elementu hello generowany Azure Machine Learning zalecenia.
* `feed/entry/content/properties/Name`-Nazwa elementu katalogu.
* `feed/entry/content/properties/Rating`-(do użytku w przyszłości)
* `feed/entry/content/properties/Reasoning`-(do użytku w przyszłości)
* `feed/entry/content/properties/Metadata`-(do użytku w przyszłości)
* `feed/entry/content/properties/FormattedRating`-(do użytku w przyszłości)

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Dane użycia
### <a name="91----import-usage-data"></a>9.1.    Importowanie danych użycia
#### <a name="911-uploading-file"></a>9.1.1. Przekazywanie plików
W tej sekcji przedstawiono sposób tooupload dane użycia przy użyciu pliku. Można wywołać tego interfejsu API z danych użycia. Wszystkie dane użycia są zapisywane dla wszystkich wywołań.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Nazwa pliku |Identyfikator tekstową hello katalogu.<br>Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.<br>Długość maksymalna: 50 |
| apiVersion |1.0 |
|  | |
| Treść żądania |Dane użycia. Format:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nazwa</th><th>Obowiązkowy</th><th>Typ</th><th>Opis</th></tr><tr><td>Identyfikator użytkownika</td><td>Tak</td><td>[A-z], [a-z], [0-9] [_] &#40; Podkreślenie &#41; [-] &#40; Dash &#41;<br> Maksymalna długość: 255 </td><td>Unikatowy identyfikator użytkownika.</td></tr><tr><td>Identyfikator elementu</td><td>Tak</td><td>[A-z], [a-z], [0-9] [&#95;] &#40; Podkreślenie &#41; [-] &#40; Dash &#41;<br> Długość maksymalna: 50</td><td>Unikatowy identyfikator elementu.</td></tr><tr><td>Time</td><td>Nie</td><td>Data w formacie: RRRR/MM/ddtgg (np. 2013/06/20T10:00:00)</td><td>Czas danych.</td></tr><tr><td>Wydarzenie</td><td>Brak; Jeśli podany również umieścić daty</td><td>Jedną z następujących hello:<br>• Kliknij przycisk<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Zakupu</td><td></td></tr></table><br>Maksymalny rozmiar pliku: 200MB<br><br>Przykład:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Odpowiedź**:

Kod stanu HTTP: 200

* `Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.
* `Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione ze względu na błąd tooan.
* `Feed\entry\content\properties\FileId`— Identyfikator pliku.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Przy użyciu danych
W tej sekcji przedstawiono, jak zdarzenia toosend w rzeczywistym czasu tooAzure Machine Learning zalecenia, zazwyczaj z witryny sieci Web.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| NAGŁÓWEK |`"Content-Type", "text/xml"` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| apiVersion |1.0 |
| Treść żądania |Wprowadzanie danych zdarzeń dla każdego zdarzenia mają toosend. Należy wysłać dla hello tej samej sesji użytkownika lub przeglądarki hello tym samym identyfikatorze hello SessionId pola. (Zobacz przykład treści zdarzenia poniżej). |

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
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
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

### <a name="92----list-model-usage-files"></a>9.2.    Pliki użycia modelu listy
Pobiera metadane wszystkie pliki użycia modelu.
Witaj użycia, które pliki są pobierane jedną stronę w czasie. Elementy kasowa 100 każdej strony. Jeśli chcesz elementów tooget od określonego indeksu można użyć parametru odata hello $skip. Na przykład elementów tooget, zaczynając od pozycji 100, należy dodać parametr hello $skip = 100 toohello żądania.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| forModelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera jednego wpisu na użycie pliku. Każdy wpis ma hello następujące dane:

* `feed\entry\content\properties\Id`-Identyfikator użycia pliku.
* `feed\entry\content\properties\Length`— Długość pliku użycie w MB.
* `feed\entry\content\properties\DateModified`-Data utworzenia pliku użycia hello.
* `feed\entry\content\properties\UseInModel`— Czy plik użycia hello jest używany w hello modelu.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Uzyskać statystyki użycia
Pobiera statystyki użycia.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| datą rozpoczęcia |Data rozpoczęcia. Format: RRRR/MM/Ddtgg |
| datą zakończenia |Data zakończenia. Format: RRRR/MM/Ddtgg |
| eventTypes |Ciąg rozdzielony przecinkami zdarzenia typów lub wartość null tooget wszystkie zdarzenia |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Kolekcja elementów klucza i wartości. Każda z nich zawiera sumę hello zdarzeń dla określonego typu zdarzenia pogrupowane wg godziny.

* `feed\entry[i]\content\properties\Key`-Zawiera czas hello (pogrupowane według godzin) i hello typ zdarzenia.
* `feed\entry[i]\content\properties\Value`— Licznik Całkowita liczba zdarzeń.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Pobierz przykładowy plik użycia
Pobiera hello 2KB pierwszego użycia pliku zawartości.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| fileId |Unikatowy identyfikator hello modelu użycia pliku |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Odpowiedź zostanie zwrócona w formacie tekstowym raw:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Pobierz plik użycia modelu
Pobiera hello pełnej zawartości hello użycia pliku.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| MID |Unikatowy identyfikator modelu hello |
| FID |Unikatowy identyfikator hello modelu użycia pliku |
| Pobierz |1 |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

Odpowiedź zostanie zwrócona w formacie tekstowym raw:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Usuń plik użycia
Usuwa plik użycia określonego modelu hello.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| fileId |Unikatowy identyfikator hello toobe plik usunięty |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

### <a name="97----delete-all-usage-files"></a>9.7.    Usuń wszystkie pliki użycia
Usuwa wszystkie pliki użycia modelu.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

## <a name="10-features"></a>10. Funkcje
W tej sekcji przedstawiono sposób tooretrieve funkcji informacji, takich jak funkcje hello zaimportowane i ich wartości, ich stopień i gdy ta pozycja został przydzielony. Funkcje są importowane jako część hello wykazu danych, a następnie ich pozycja jest skojarzony, po zakończeniu kompilacji rangi.
Funkcja rangę można zmienić zgodnie z toohello wzorca użycia danych i typ elementów. Ale rangę hello powinny mieć tylko małe wahania spójne użycia/elementów.
Ranga Hello funkcji jest liczbą nieujemną. Witaj numer 0 oznacza, że nie zajęła tej funkcji hello (się stanie w przypadku wywołać tego interfejsu API zakończenia wcześniejszych toohello pierwszej kompilacji rank powitania). Data Hello jaką została przypisana rangę hello jest nazywany hello wynik świeżości.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. Uzyskać informacje o funkcji (Ostatnia kompilacja rangi)
Pobiera informacje funkcji hello, w tym klasyfikacji dla hello ostatniej kompilacji rangi powiodło się.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| samplingSize |Liczba wartości tooinclude dla każdej funkcji, zgodnie z toohello danych w katalogu hello. <br/>Możliwe wartości:<br> -1 - wszystkie próbki. <br>0 — próbkowanie nie. <br>N - Zwróć N przykłady dla każdej nazwy funkcji. |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera listę wpisów informacji o funkcji. Każdy wpis zawiera:

* `feed/entry/content/m:properties/d:Name`-Funkcja nazwa.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Data na które hello rangę funkcji przydzielone toothis alias wynik świeżości funkcji. Historical Data ("0001-01-01T00:00:00") oznacza, że wykonano nie rangi kompilacji.
* `feed/entry/content/m:properties/d:Rank`— Ranga funkcja (float). Ranga 2.0 lub nowszej jest uznawane za funkcję dobra.
* `feed/entry/content/m:properties/d:SampleValues`-Rozdzielana przecinkami lista wartości żądany rozmiar toohello próbkowania.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. Pobierz informacje funkcji (dla określonej kompilacji rangi)
Pobiera informacje o funkcji hello, w tym klasyfikacji w ramach określonej kompilacji rank powitania.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| samplingSize |Liczba wartości tooinclude dla każdej funkcji, zgodnie z toohello danych w katalogu hello.<br/> Możliwe wartości:<br> -1 - wszystkie próbki. <br>0 — próbkowanie nie. <br>N - Zwróć N przykłady dla każdej nazwy funkcji. |
| rankBuildId |Unikatowy identyfikator kompilacji rank powitania lub -1 dla ostatniej kompilacji rank powitania |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera listę wpisów informacji o funkcji. Każdy wpis zawiera:

* `feed/entry/content/m:properties/d:Name`-Funkcja nazwa.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Data na które hello rangę funkcji przydzielone toothis alias wynik świeżości funkcji. Historical Data ("0001-01-01T00:00:00") oznacza, że wykonano nie rangi kompilacji.
* `feed/entry/content/m:properties/d:Rank`— Ranga funkcja (float). Ranga 2.0 lub nowszej jest uznawane za funkcję dobra.
* `feed/entry/content/m:properties/d:SampleValues`-Rozdzielana przecinkami lista wartości żądany rozmiar toohello próbkowania.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Kompilacja
  W tej sekcji opisano hello toobuilds związane z różnych interfejsów API. Istnieją 3 typy kompilacji: kompilację zalecenie, rangi kompilacji i kompilacji zmianie wysokości progów (często zakupione razem).

Celem Hello zalecenie kompilacji jest toogenerate model zalecenie używany do przewidywania. Prognoz (dla tego typu kompilacji) są dostępne w dwóch odmian:

* I2I - alias Element zalecenia tooItem - danego elementu lub listy elementów tej opcji spowoduje prognozowania listę elementów, które są prawdopodobnie toobe wysoki odsetek.
* U2I - alias Zalecenia dotyczące tooItem użytkownika - podany identyfikator użytkownika (i opcjonalnie listę elementów) ta opcja będzie prognozowania listę elementów, które są prawdopodobnie toobe z niepodłączonych do hello danego użytkownika (i jego dodatkowe wybrane elementy). zalecenia dotyczące U2I Hello są oparte na powitania historii elementów, które były istotnych dla użytkownika hello czasu toohello, konstruowania modelu hello.

Rank kompilacji jest techniczne kompilacji, która pozwala toolearn o użyteczności hello funkcje. Zazwyczaj w kolejności tooget hello najlepszych wyników dla modelu zalecenia dotyczące funkcji, należy podjąć hello następujące kroki:

* Wyzwalanie rangi kompilacji (o ile wynik hello funkcje jest stabilna), a następnie zaczekaj do wyniku funkcji hello.
* Pobrać rangę hello funkcje przez wywołanie hello [Get Info funkcji](#101-get-features-info-for-last-rank-build) interfejsu API.
* Konfigurowanie kompilowania zalecenia za pomocą hello następujące parametry:
  * `useFeatureInModel`-Set tooTrue.
  * `ModelingFeatureList`-Set tooa rozdzielana przecinkami lista funkcji z wynikiem 2.0 lub więcej (według rangi toohello, pobierane w poprzednim kroku hello).
  * `AllowColdItemPlacement`-Set tooTrue.
  * Opcjonalnie można ustawić `EnableFeatureCorrelation` tooTrue i `ReasoningFeatureList` toohello lista funkcji, które chcesz toouse wyjaśnień (zazwyczaj hello tę samą listę funkcje używane w modelowania lub podlisty).
* Wyzwalacz hello zalecenie kompilacji z hello skonfigurowane parametry.

Uwaga: Jeśli nie skonfigurujesz żadnych parametrów (np. wywołać budowania zalecenie hello bez parametrów) lub nie zostanie jawnie wyłączone hello użycia funkcji (np. `UseFeatureInModel` ustawić tooFalse), hello system skonfiguruje hello parametry dotyczące funkcji toohello wyjaśniono powyższych wartości w przypadku, gdy istnieje rangi kompilacji.

Nie podlega ograniczeniom na uruchomioną kompilację rangi i zalecenia kompilacji jednocześnie dla hello sam model. Niemniej jednak nie można uruchomić dwie kompilacje hello tego samego typu na powitania sam model równolegle.

Kompilacja zmianie wysokości progów (często zakupione razem) jest jeszcze inny algorytm zalecenia nazywane czasami "zachowawcze" polecania, co ułatwia katalogi, które nie są jednorodne charakteru (jednorodnych: książek, filmów, niektóre żywności sposób; niejednorodnego: komputerów i urządzeń, między domenami, wysoce zróżnicowany).

Uwaga: Jeśli hello plików do użycia, które zostało przez Ciebie przekazane zawiera pole opcjonalne hello "typ zdarzenia" następnie dla zmianie wysokości progów modelowania tylko zdarzenia "Zakupu" będzie można używać. Jeśli żaden typ zdarzenia jest pod warunkiem, że wszystkie zdarzenia są traktowane jako zakupu.

#### <a name="111-build-parameters"></a>11.1 kompilacji parametrów
Każdy typ kompilacji mogą być konfigurowane przez zestaw parametrów (przedstawione poniżej). Jeśli nie skonfigurujesz parametry hello hello systemu zostanie automatycznie atrybutu wartości parametrów toohello zgodnie z toohello informacje obecnych w chwili hello wyzwolić kompilację.

##### <a name="1111-usage-condenser"></a>11.1.1. Zwrotną użycia
Użytkowników lub elementy o kilka punktów użycia może zawierać więcej szumu niż informacji. Witaj system spróbuje toopredict hello minimalna liczba punktów użycia na użytkownika/elementu toobe używane w modelu. Ta liczba będzie zakresu hello zdefiniowany przez hello ItemCutoffLowerBound i parametrów ItemCutoffUpperBound elementów i hello zakresu zdefiniowanego przez hello UserCutOffLowerBound i UserCutoffUpperBound parametry dla użytkowników. Hello zwrotną wpływu na elementy lub użytkowników, można zminimalizować przez ustawienie co najmniej jeden z odpowiedniego toozero granice hello.

##### <a name="1112-rank-build-parameters"></a>11.1.2. Ranga kompilacji parametrów
Witaj w poniższej tabeli przedstawiono hello parametry kompilacji dla kompilacji rangi.

| Klucz | Opis | Typ | Nieprawidłowa wartość |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |Hello liczby iteracji modelu hello wykonuje, sprawdzając hello obliczeniowe całkowity czas i hello dokładności modelu. większa liczba hello Hello, hello większej dokładności, zostanie wyświetlony, ale hello obliczeń czas będzie trwać dłużej. |Liczba całkowita |10-50 |
| NumberOfModelDimensions |Hello liczby wymiarów wiąże się, że liczba toohello "funkcji" hello modelu spróbuje toofind w danych. Zwiększenie liczby hello wymiarów pozwoli lepiej dostrajanie hello wyniki w mniejszych klastrów. Jednak zbyt dużo wymiarów uniemożliwi modelu hello odnalezienie korelacji między elementami. |Liczba całkowita |10-40 |
| ItemCutOffLowerBound |Definiuje element hello dolna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| ItemCutOffUpperBound |Definiuje element hello górna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| UserCutOffLowerBound |Definiuje hello użytkownika dolna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| UserCutOffUpperBound |Definiuje hello użytkownika górna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Parametry kompilacji zalecenia
Witaj w poniższej tabeli przedstawiono hello parametry kompilacji dla kompilacji zalecenie.

| Klucz | Opis | Typ | Nieprawidłowa wartość |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |Hello liczby iteracji modelu hello wykonuje, sprawdzając hello obliczeniowe całkowity czas i hello dokładności modelu. większa liczba hello Hello, hello większej dokładności, zostanie wyświetlony, ale hello obliczeń czas będzie trwać dłużej. |Liczba całkowita |10-50 |
| NumberOfModelDimensions |Hello liczby wymiarów wiąże się, że liczba toohello "funkcji" hello modelu spróbuje toofind w danych. Zwiększenie liczby hello wymiarów pozwoli lepiej dostrajanie hello wyniki w mniejszych klastrów. Jednak zbyt dużo wymiarów uniemożliwi modelu hello odnalezienie korelacji między elementami. |Liczba całkowita |10-40 |
| ItemCutOffLowerBound |Definiuje element hello dolna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| ItemCutOffUpperBound |Definiuje element hello górna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| UserCutOffLowerBound |Definiuje hello użytkownika dolna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| UserCutOffUpperBound |Definiuje hello użytkownika górna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| Opis |Tworzenie opisu. |Ciąg |Dowolny tekst maksymalne 512 znaków |
| EnableModelingInsights |Umożliwia toocompute metryki na powitania zalecenie modelu. |Wartość logiczna |PRAWDA/FAŁSZ |
| UseFeaturesInModel |Wskazuje, czy funkcje mogą być używane w kolejności tooenhance hello zalecenie modelu. |Wartość logiczna |PRAWDA/FAŁSZ |
| ModelingFeatureList |Rozdzielana przecinkami lista toobe nazwy funkcji używane w hello zalecenie kompilacji, w kolejności tooenhance hello zalecenia. |Ciąg |Nazwy funkcji się too512 znaków |
| AllowColdItemPlacement |Wskazuje, czy zalecenie hello ma również wypychać zimnych elementów za pomocą funkcji podobieństwa. |Wartość logiczna |PRAWDA/FAŁSZ |
| EnableFeatureCorrelation |Wskazuje, czy funkcje mogą być używane w uzasadnienie. |Wartość logiczna |PRAWDA/FAŁSZ |
| ReasoningFeatureList |Rozdzielana przecinkami lista toobe nazwy funkcji używany do wnioskowania zdań (np. zalecenie wyjaśnienia). |Ciąg |Nazwy funkcji się too512 znaków |
| EnableU2I |Zezwalaj na powitania spersonalizowanych zalecenie alias U2I (zalecenia tooitem użytkownika). |Wartość logiczna |PRAWDA/FAŁSZ (domyślna wartość true) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. Parametry kompilacji zmianie wysokości progów
Witaj w poniższej tabeli przedstawiono hello parametry kompilacji dla kompilacji zalecenie.

| Klucz | Opis | Typ | Nieprawidłowa wartość (ustawienie domyślne) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Jak model zachowawcze hello jest. Liczba wystąpień wspólnej toobe elementów brany pod uwagę podczas modelowania. |Liczba całkowita |3-50 (6) |
| FbtMaxItemSetSize |Granice hello liczba elementów w zestawie częste. |Liczba całkowita |2-3 (2) |
| FbtMinimalScore |Wynik minimalnego częste zestaw powinny mieć w kolejności toobe objęte hello zwrócone wyniki. Witaj wyższej Witaj lepiej. |O podwójnej precyzji |0 lub nowszym (0) |
| FbtSimilarityFunction |Definiuje toobe funkcja podobieństwa hello używane przez hello kompilacji. Przyrostu objawach serendipity, wspólnej wystąpienie objawach przewidywalności i Jaccard stanowi dobry kompromis między hello dwa. |Ciąg |cooccurrence przyrostu, jaccard (przyrostu) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Wyzwalacz kompilacji zalecenia
  Domyślnie ten interfejs API wyzwoli kompilacji modelu zalecenia. tootrigger rangę kompilacji (w kolejności tooscore funkcji), hello kompilacji interfejsu API wariant z parametrem typu kompilacji powinien być używany.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| NAGŁÓWEK |`"Content-Type", "text/xml"`(Jeśli wysyła treść żądania) |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| userDescription |Identyfikator tekstową hello katalogu. Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego. Zobacz przykład powyżej.<br>Długość maksymalna: 50 |
| apiVersion |1.0 |
|  | |
| Treść żądania |Jeśli pole pozostanie puste hello kompilacji zostaną wykonane z hello domyślne parametry kompilacji.<br><br>Parametry kompilacji hello tooset, wysłać hello parametrów jako XML na treść hello jak hello następujące przykładowe. (Zobacz sekcji hello "Parametry kompilacji" Aby uzyskać informacje o parametrach hello).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Odpowiedź**:

Kod stanu HTTP: 200

Jest to interfejs API asynchronicznego. Otrzymasz identyfikator kompilacji w odpowiedzi. tooknow po zakończeniu kompilacji hello, należy wywołać interfejs API "Pobierz kompilacje stan modelu" hello i zlokalizuj identyfikator to kompilacji w hello odpowiedzi. Należy pamiętać, że kompilacja może trwać od toohours minut w zależności od wielkości hello hello danych.

Nie można używać zalecenia, dopóki hello kompilacji kończy się.

Stan prawidłowy kompilacji:

* Utwórz — żądanie kompilacji zostało utworzone.
* W kolejce - wysłano żądanie kompilacji i jest w kolejce.
* Trwa kompilowanie - kompilacji.
* Sukces - kompilacja zakończyła się pomyślnie.
* Błąd — Kompilacja została zakończona z błędem.
* Anulowane — Kompilacja została anulowana.
* Anulowanie — wysłano żądanie anulowania kompilacji hello.

Należy zwrócić uwagę tej kompilacji hello identyfikator można znaleźć pod ścieżką hello:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Wyzwalacz kompilacji (zalecenie, pozycja lub zmianie wysokości progów)
| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| NAGŁÓWEK |`"Content-Type", "text/xml"`(Jeśli wysyła treść żądania) |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| userDescription |Identyfikator tekstową hello katalogu. Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego. Zobacz przykład powyżej.<br>Długość maksymalna: 50 |
| buildType |Typ hello tooinvoke kompilacji: <br/> -"Zalecenie" dla kompilacji zalecenia <br> -Klasyfikacji dla rangi kompilacji <br/> -Zmianie wysokości "progów" dla kompilacji zmianie wysokości progów |
| apiVersion |1.0 |
|  | |
| Treść żądania |Jeśli pole pozostanie puste hello kompilacji zostaną wykonane z hello domyślne parametry kompilacji.<br><br>Jeśli chcesz, aby parametry kompilacji tooset, wysyłać je jako XML na treść hello podobnie jak w hello następujące przykładowe. (W sekcji hello "Parametry kompilacji" wyjaśnienie i Pełna lista parametrów hello.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Odpowiedź**:

Kod stanu HTTP: 200

Jest to interfejs API asynchronicznego. Otrzymasz identyfikator kompilacji w odpowiedzi. tooknow po zakończeniu kompilacji hello, należy wywołać interfejs API "Pobierz kompilacje stan modelu" hello i zlokalizuj identyfikator to kompilacji w hello odpowiedzi. Należy pamiętać, że kompilacja może trwać od toohours minut w zależności od wielkości hello hello danych.

Nie można używać zalecenia, dopóki hello kompilacji kończy się.

Stan prawidłowy kompilacji:

* Utwórz — Model został utworzony.
* W kolejce — zostało wyzwolone kompilacji modelu i jest w kolejce.
* Kompilowanie — Model została skompilowana.
* Sukces - kompilacja zakończyła się pomyślnie.
* Błąd — Kompilacja została zakończona z błędem.
* Anulowane — Kompilacja została anulowana.
* Anulowanie - Trwa anulowanie kompilacji.

Należy zwrócić uwagę tej kompilacji hello identyfikator można znaleźć pod ścieżką hello:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a>11.4. Pobierz stan kompilacji modelu
Pobiera kompilacji i ich stanu dla określonego modelu.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| onlyLastBuild |Wskazuje, czy wszystkie hello tooreturn kompilacji tylko stan hello hello ostatniej kompilacji lub historii hello modelu |
| apiVersion |1.0 |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera jednego wpisu na kompilacji. Każdy wpis ma hello następujące dane:

* `feed/entry/content/properties/UserName`-Nazwa hello użytkownika.
* `feed/entry/content/properties/ModelName`-Nazwa hello modelu.
* `feed/entry/content/properties/ModelId`-Unikatowy identyfikator modelu.
* `feed/entry/content/properties/IsDeployed`— Czy kompilacja hello jest wdrożona () aktywne kompilacji).
* `feed/entry/content/properties/BuildId`-Utwórz unikatowy identyfikator.
* `feed/entry/content/properties/BuildType`— Typ hello kompilacji.
* `feed/entry/content/properties/Status`-Stan kompilacji. Może być jedną z następujących hello: błąd, kompilowanie, w kolejce, Cancelling odwołania, Powodzenie.
* `feed/entry/content/properties/StatusMessage`— Komunikat o stanie szczegółowe (dotyczy tylko Stany toospecific).
* `feed/entry/content/properties/Progress`-Kompilacji postępu (%).
* `feed/entry/content/properties/StartTime`-Godzina rozpoczęcia kompilacji.
* `feed/entry/content/properties/EndTime`-Czas zakończenia kompilacji.
* `feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.
* `feed/entry/content/properties/ProgressStep`— Szczegółowe informacje o hello bieżący etap kompilacji w toku.

Stan prawidłowy kompilacji:

* Utworzone — wpis żądanie kompilacji zostało utworzone.
* W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.
* Kompilowanie - kompilacji jest przetwarzane.
* Sukces - kompilacja zakończyła się pomyślnie.
* Błąd — Kompilacja została zakończona z błędem.
* Anulowane — Kompilacja została anulowana.
* Anulowanie - Trwa anulowanie kompilacji.

Prawidłowe wartości dla typu kompilacji:

* Ranga - rangę kompilacji.
* Zalecenie - zalecenie kompilacji.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a>11.5. Pobierz stan kompilacji
Pobiera kompilacji statusy wszystkich modeli użytkownika.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| onlyLastBuild |Wskazuje, czy wszystkie hello tooreturn kompilacji tylko stan hello hello ostatniej kompilacji lub historii hello modelu. |
| apiVersion |1.0 |

**Odpowiedź**:

Kod stanu HTTP: 200

odpowiedź Hello zawiera jednego wpisu na kompilacji. Każdy wpis ma hello następujące dane:

* `feed/entry/content/properties/UserName`-Nazwa hello użytkownika.
* `feed/entry/content/properties/ModelName`-Nazwa hello modelu.
* `feed/entry/content/properties/ModelId`-Unikatowy identyfikator modelu.
* `feed/entry/content/properties/IsDeployed`— Czy hello kompilacja zostaje wdrożona.
* `feed/entry/content/properties/BuildId`-Utwórz unikatowy identyfikator.
* `feed/entry/content/properties/BuildType`— Typ hello kompilacji.
* `feed/entry/content/properties/Status`-Stan kompilacji. Może być jedną z następujących hello: błąd, kompilowanie, w kolejce, odwołania, Cancelling, Powodzenie.
* `feed/entry/content/properties/StatusMessage`— Komunikat o stanie szczegółowe (dotyczy tylko Stany toospecific).
* `feed/entry/content/properties/Progress`-Kompilacji postępu (%).
* `feed/entry/content/properties/StartTime`-Godzina rozpoczęcia kompilacji.
* `feed/entry/content/properties/EndTime`-Czas zakończenia kompilacji.
* `feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.
* `feed/entry/content/properties/ProgressStep`— Szczegółowe informacje o hello bieżący etap kompilacji w toku.

Stan prawidłowy kompilacji:

* Utworzone — wpis żądanie kompilacji zostało utworzone.
* W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.
* Kompilowanie - kompilacji jest przetwarzane.
* Sukces - kompilacja zakończyła się pomyślnie.
* Błąd — Kompilacja została zakończona z błędem.
* Anulowane — Kompilacja została anulowana.
* Anulowanie - Trwa anulowanie kompilacji.

Prawidłowe wartości dla typu kompilacji:

* Ranga - rangę kompilacji.
* Zalecenie - zalecenie kompilacji.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a>11.6. Usuń kompilacji
Usuwa kompilacji.

UWAGA: <br>Nie można usunąć aktywnej kompilacji. Witaj model powinien być zaktualizowany inną kompilację active tooa przed jego usunięciem.<br>Nie można usunąć kompilacji w toku. Należy anulować kompilacji hello najpierw przez wywołanie metody <strong>anulowania kompilacji</strong>.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| identyfikatora buildId |Unikatowy identyfikator hello kompilacji. |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

### <a name="117-cancel-build"></a>11.7. Anulowanie kompilacji
Anuluje kompilacji, która w budynku stanu.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| UMIEŚĆ |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| identyfikatora buildId |Unikatowy identyfikator hello kompilacji. |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

### <a name="118-get-build-parameters"></a>11.8. Pobranie parametrów kompilacji
Pobiera kompilacji parametrów.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| identyfikatora buildId |Unikatowy identyfikator hello kompilacji. |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

Ten interfejs API zwraca kolekcję elementów klucza i wartości. Każdy element reprezentuje parametr i wartość:

* `feed/entry/content/properties/Key`-Nazwa parametru kompilacji.
* `feed/entry/content/properties/Value`— Wartość parametru kompilacji.

Witaj w poniższej tabeli przedstawiono hello wartość, która reprezentuje każdy klucz.

| Klucz | Opis | Typ | Nieprawidłowa wartość |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |Hello liczby iteracji modelu hello wykonuje, sprawdzając hello obliczeniowe całkowity czas i hello dokładności modelu. większa liczba hello Hello, hello większej dokładności, zostanie wyświetlony, ale hello obliczeń czas będzie trwać dłużej. |Liczba całkowita |10-50 |
| NumberOfModelDimensions |Hello liczby wymiarów wiąże się, że liczba toohello "funkcji" hello modelu spróbuje toofind w danych. Zwiększenie liczby hello wymiarów pozwoli lepiej dostrajanie hello wyniki w mniejszych klastrów. Jednak zbyt dużo wymiarów uniemożliwi modelu hello odnalezienie korelacji między elementami. |Liczba całkowita |10-40 |
| ItemCutOffLowerBound |Definiuje element hello dolna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| ItemCutOffUpperBound |Definiuje element hello górna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| UserCutOffLowerBound |Definiuje hello użytkownika dolna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| UserCutOffUpperBound |Definiuje hello użytkownika górna granica zwrotną hello. Zobacz użycie zwrotną powyżej. |Liczba całkowita |co najmniej 2 (zwrotną Wyłącz 0) |
| Opis |Tworzenie opisu. |Ciąg |Dowolny tekst maksymalne 512 znaków |
| EnableModelingInsights |Umożliwia toocompute metryki na powitania zalecenie modelu. |Wartość logiczna |PRAWDA/FAŁSZ |
| UseFeaturesInModel |Wskazuje, czy funkcje mogą być używane w kolejności tooenhance hello zalecenie modelu. |Wartość logiczna |PRAWDA/FAŁSZ |
| ModelingFeatureList |Rozdzielana przecinkami lista toobe nazwy funkcji używane w hello zalecenie kompilacji, w kolejności tooenhance hello zalecenia. |Ciąg |Nazwy funkcji się too512 znaków |
| AllowColdItemPlacement |Wskazuje, czy zalecenie hello ma również wypychać zimnych elementów za pomocą funkcji podobieństwa. |Wartość logiczna |PRAWDA/FAŁSZ |
| EnableFeatureCorrelation |Wskazuje, czy funkcje mogą być używane w uzasadnienie. |Wartość logiczna |PRAWDA/FAŁSZ |
| ReasoningFeatureList |Rozdzielana przecinkami lista toobe nazwy funkcji używany do wnioskowania zdań (np. zalecenie wyjaśnienia). |Ciąg |Nazwy funkcji się too512 znaków |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Zalecenie
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. Uzyskaj element zalecenia (dla active kompilacji)
Pobierz zalecenia hello active kompilacji typu "Zalecenie" lub "Zmianie wysokości progów" na podstawie listy elementów ziarna (dane wejściowe).

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| identyfikatory elementów |Rozdzielana przecinkami lista hello elementów toorecommend dla. <br>Jeśli kompilacja active hello jest wpisz zmianie wysokości progów, a następnie wysłać tylko jeden element. <br>Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników <br> Maksymalna liczba: 150 |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

odpowiedź przykład Hello poniżej zawiera 10 elementów zalecane.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. Pobierz element zalecenia (określonej kompilacji)
Pobierz zalecenia określonej kompilacji typu "Zalecenie" lub "Zmianie wysokości progów".

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| identyfikatory elementów |Rozdzielana przecinkami lista hello elementów toorecommend dla. <br>Jeśli kompilacja active hello jest wpisz zmianie wysokości progów, a następnie wysłać tylko jeden element. <br>Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników <br> Maksymalna liczba: 150 |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| identyfikatora buildId |Witaj kompilacji toouse identyfikator dla tego żądania zalecenia |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

Zobacz przykład odpowiedzi, 12.1

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. Pobierz zalecenia zmianie wysokości progów (dla active kompilacji)
Pobierz zalecenia hello active kompilacji typu "Zmianie wysokości progów" oparta na elemencie inicjatora (dane wejściowe).

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Identyfikator elementu |Element toorecommend dla. <br>Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników <br>Maksymalna liczba: 150 |
| minimalScore |Wynik minimalnego częste zestaw powinny mieć w kolejności toobe objęte hello zwrócone wyniki |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla danego zestawu elementu zalecane (zestaw elementów, które zwykle są kupowane wraz z elementu seed/input hello). Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id1`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name1`-Nazwa elementu hello.
* `Feed\entry\content\properties\Id2`Identyfikator elementu zalecane - 2 (opcjonalnie).
* `Feed\entry\content\properties\Name2`-Nazwa elementu hello 2 (opcjonalnie).
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

przykład odpowiedzi Hello poniżej zawiera 3 zestawy zalecane elementu.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. Pobierz zmianie wysokości progów zalecenia (określonej kompilacji)
Pobierz zalecenia określonej kompilacji typu "Zmianie wysokości progów".

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Identyfikator elementu |Element toorecommend dla. <br>Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników <br>Maksymalna liczba: 150 |
| minimalScore |Wynik minimalnego częste zestaw powinny mieć w kolejności toobe objęte hello zwrócone wyniki |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| identyfikatora buildId |Witaj kompilacji toouse identyfikator dla tego żądania zalecenia |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla danego zestawu elementu zalecane (zestaw elementów, które zwykle są kupowane wraz z elementu seed/input hello). Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id1`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name1`-Nazwa elementu hello.
* `Feed\entry\content\properties\Id2`Identyfikator elementu zalecane - 2 (opcjonalnie).
* `Feed\entry\content\properties\Name2`-Nazwa elementu hello 2 (opcjonalnie).
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

Zobacz przykład odpowiedzi, w 12.3

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Pobierz zalecenia użytkownika (dla active kompilacji)
Pobierz zalecenia użytkownika kompilacji typu "Recommendation" oznaczona jako aktywny kompilacji.

Witaj interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika.

Uwagi: 

1. Nie ma żadnych zalecenie użytkownika dla kompilacji zmianie wysokości progów.
2. Jeśli hello active kompilacji jest zmianie wysokości progów będą ta metoda zwraca błąd.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Nazwa użytkownika |Unikatowy identyfikator użytkownika hello |
| numberOfResults |Liczba wymaganych wyników |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

Zobacz przykład odpowiedzi, 12.1

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Pobierz zalecenia dotyczące użytkownika z listy elementów (dla active kompilacji)
Uzyskaj zalecenia użytkownika kompilacji typu "Recommendation" oznaczona jako aktywny kompilacji z dodatkowych listy elementów

Hello interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika i hello dodatkowe podane elementy.

Uwagi: 

1. Nie ma żadnych zalecenie użytkownika dla kompilacji zmianie wysokości progów.
2. Jeśli hello active kompilacji jest zmianie wysokości progów będą ta metoda zwraca błąd.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Nazwa użytkownika |Unikatowy identyfikator użytkownika hello |
| itemsIds |Rozdzielana przecinkami lista hello elementów toorecommend dla. Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

Zobacz przykład odpowiedzi, 12.1

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. Uzyskaj zalecenia użytkownika (od określonej kompilacji)
Pobierz zalecenia użytkownika określonej kompilacji typu "Recommendation".

Witaj interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika (używane w określonej kompilacji hello).

Uwaga: Jest Brak rekomendacji użytkownika dla kompilacji zmianie wysokości progów.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Nazwa użytkownika |Unikatowy identyfikator użytkownika hello |
| numberOfResults |Liczba wymaganych wyników |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| identyfikatora buildId |Witaj kompilacji toouse identyfikator dla tego żądania zalecenia |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

Zobacz przykład odpowiedzi, 12.1

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Uzyskaj zalecenia użytkownika z listy elementów (o określonej kompilacji)
Pobierz zalecenia użytkownika określonej kompilacji typu "Recommendation" i hello listę dodatkowych elementów.

Hello interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika i hello dodatkowe listy elementów.

Uwaga: Tthere jest Brak rekomendacji użytkownika dla kompilacji zmianie wysokości progów.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| Nazwa użytkownika |Unikatowy identyfikator użytkownika hello |
| identyfikatory elementów |Rozdzielana przecinkami lista hello elementów toorecommend dla. Maksymalna długość: 1024 |
| numberOfResults |Liczba wymaganych wyników |
| includeMetatadata |Użycia w przyszłości, zawsze false |
| identyfikatora buildId |Witaj kompilacji toouse identyfikator dla tego żądania zalecenia |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.
* `Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).

Zobacz przykład odpowiedzi, 12.1

## <a name="13-user-usage-history"></a>13. Historia użycia użytkownika
Po modelu zalecenie został utworzony hello system zezwoli używany dla kompilacji hello tooretrieve hello historię użytkownika (elementy skojarzone tooa określonego użytkownika).
Ten interfejs API umożliwia tooretrieve hello użytkownika historii

Uwaga: hello historię użytkownika jest obecnie dostępny tylko dla kompilacji zalecenia.

### <a name="131-retrieve-user-history"></a>13.1 pobrać historii użytkownika
Pobieranie listy hello element używany w hello active kompilacji lub w hello określonej kompilacji dla hello podany identyfikator użytkownika.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |Pobierz historię użytkownika hello hello active kompilacji.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Pobierz historię użytkownika hello dla hello podane kompilacji`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Przykład:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator Hello hello modelu. |
| Nazwa użytkownika |Unikatowy identyfikator Hello hello użytkownika. |
| identyfikatora buildId |opcjonalny parametr Zezwalaj tooindicate, z których kompilacji hello historię użytkownika powinno być pobierania |
| apiVersion |1.0 |

**Odpowiedź:**

Kod stanu HTTP: 200

odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane. Każdy wpis ma hello następujące dane:

* `Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.
* `Feed\entry\content\properties\Name`-Nazwa elementu hello.
* `Feed\entry\content\properties\Rating`-NIE DOTYCZY.
* `Feed\entry\content\properties\Reasoning`-NIE DOTYCZY.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Powiadomienia
Azure Machine Learning zalecenia tworzy powiadomienia, gdy wystąpi trwałe błędów w systemie hello. Istnieją 3 typy powiadomień:

1. Niepowodzenie kompilacji — to powiadomienie jest wyzwalany dla każdego błędu kompilacji.
2. Uzyskiwanie danych przetwarzania niepowodzenie — to powiadomienie jest wyzwalane, gdy będziemy mieć więcej niż 100 błędów w hello ostatnich 5 minut hello przetwarzania zdarzeń użycia dla modelu.
3. Niepowodzenie zużycie zalecenie — to powiadomienie jest wyzwalane, gdy będziemy mieć więcej niż 100 błędów w hello ostatnich 5 minut hello przetwarzania żądań zalecenie na modelu.

### <a name="141-get-notifications"></a>14.1. Otrzymywać powiadomień
Pobiera wszystkie hello powiadomienia dla wszystkich modeli lub dla pojedynczego modelu.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| POBIERZ |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Pobieranie wszystkich powiadomień dla wszystkich modeli:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Przykład uzyskiwanie powiadomień dla określonego modelu:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Parametr opcjonalny. Gdy pominięty, będą wyświetlane wszystkie powiadomienia dla wszystkich modeli. <br>Prawidłowe wartości: Unikatowy identyfikator hello modelu. |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź:**

Kod stanu HTTP: 200

OData XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Usuwanie modelu powiadomień
Usuwa wszystkie odczytu powiadomienia dla modelu.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Przykład:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| modelId |Unikatowy identyfikator modelu hello |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

### <a name="143-delete-user-notifications"></a>14.3. Usunięcie powiadomienia użytkownika
Usuwa wszystkie powiadomienia dla wszystkich modeli.

| Metoda HTTP | IDENTYFIKATOR URI |
|:--- |:--- |
| USUŃ |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Nazwa parametru | Prawidłowe wartości |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Treść żądania |BRAK |

**Odpowiedź**:

Kod stanu HTTP: 200

## <a name="15-legal"></a>15. Informacje prawne
Niniejszy dokument jest udostępniany "jako — jest". Informacje i poglądy wyrażone w tym dokumencie, w tym adresy URL i inne odsyłacze do witryn internetowych, mogą ulec zmianie bez uprzedzenia.<br><br>
Niektóre przedstawione przykłady są udostępniane tylko do celów ilustracyjnych i są fikcyjne. Żadne rzeczywiste skojarzenia ani połączenia jest przeznaczony lub powinny być zakładane.<br><br>
Ten dokument nie daje użytkownikowi żadnych praw tooany własności intelektualnej związanej z jakimkolwiek produktem firmy Microsoft. Można kopiować i używać tego dokumentu do wewnętrznych celów referencyjnych.<br><br>
© 2015 Microsoft. Wszelkie prawa zastrzeżone.

