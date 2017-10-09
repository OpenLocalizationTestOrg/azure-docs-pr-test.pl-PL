---
title: "toocreating aaaGuide usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrożyć usługę Data zakupu na hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Opis hello węzłów schematu mapowania istniejących tooOData usługi sieci web za pomocą pliku CSDL
> [!IMPORTANT]
> **W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.** Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners). Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Ten dokument pomaga wyjaśnienie struktury węzła hello mapowania tooCSDL protokołu OData. Jest ważne toonote, że struktura węzła hello jest dobrze sformułowany kod XML. Dlatego schematu głównego, nadrzędne i podrzędne stosuje się podczas projektowania mapowanie OData.

## <a name="ignored-elements"></a>Elementy została zignorowana
Oto Hello hello wysokiego poziomu CSDL elementy (węzłów XML), które nie będą używane przez hello Azure Marketplace wewnętrznej bazy danych podczas importowania hello metadanych usługi sieci web hello toobe. Mogą być obecne, ale zostaną zignorowane.

| Element | Zakres |
| --- | --- |
| Za pomocą elementu |węzeł Hello, podrzędne węzły i wszystkie atrybuty |
| Documentation Element |węzeł Hello, podrzędne węzły i wszystkie atrybuty |
| Element ComplexType |węzeł Hello, podrzędne węzły i wszystkie atrybuty |
| Element skojarzenia |węzeł Hello, podrzędne węzły i wszystkie atrybuty |
| Rozszerzone właściwości |węzeł Hello, podrzędne węzły i wszystkie atrybuty |
| Obiekt EntityContainer |Tylko hello następujące atrybuty są ignorowane: *rozszerza* i *AssociationSet* |
| Schemat |Tylko hello następujące atrybuty są ignorowane: *Namespace* |
| Element FunctionImport |Tylko hello następujące atrybuty są ignorowane: *tryb* (przyjęto wartość domyślną ln) |
| Dla obiektu |Tylko hello następujące węzły podrzędne są ignorowane: *klucza* i *PropertyRef* |

Witaj poniżej opisano toohello zmiany (dodany i zignorowane elementy) hello różnych węzłów CSDL XML szczegółowo.

## <a name="functionimport-node"></a>Element FunctionImport węzła
Węzeł FunctionImport reprezentuje jeden adres URL (punkt wejścia) udostępniający usługi toohello przez użytkownika końcowego. węzeł Hello pozwala, opisujące, jak adres URL hello jest skierowana, które parametry są dostępne toohello przez użytkownika końcowego i jak te parametry są udostępniane.

Szczegółowe informacje o tym węźle znajdują się w [tutaj][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx)

Witaj poniżej przedstawiono dodatkowe atrybuty hello (lub tooattributes dodatków) który są udostępniane przez węzeł elementu FunctionImport hello:

**d:BaseUri** -hello szablon identyfikatora URI dla zasobu REST hello tooMarketplace uwidocznione. Marketplace używa hello szablonu tooconstruct zapytań dotyczących hello usługi sieci web REST. szablon identyfikatora URI Hello zawiera symbole zastępcze hello parametrów w formie hello {parameterName}, gdzie nazwa parametru jest nazwą hello hello parametru. Przykład. apiVersion = {apiVersion}.
Parametry są dozwolone tooappear jako parametry identyfikatora URI lub jako część hello ścieżka identyfikatora URI. W przypadku hello hello wyglądu w ścieżce hello zawsze są obowiązkowe (nie można oznaczyć jako wartości null). *Przykład:*`d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Nazwa** — nazwa hello hello zaimportowane funkcji.  Nie może być hello taki sam jak inne zdefiniowanych nazw w pliku CSDL hello.  Przykład. Name = "GetModelUsageFile"

**Obiekt EntitySet** *(opcjonalnie)* — Jeśli funkcja hello zwraca kolekcję typów jednostek, wartość hello hello **EntitySet** musi być hello jednostki zestaw toowhich hello kolekcji należy. W przeciwnym razie hello **EntitySet** atrybutu nie mogą być używane. *Przykład:*`EntitySet="GetUsageStatisticsEntitySet"`

**Obiekt ReturnType** *(opcjonalnie)* — Określa typ hello elementów zwróconych przez hello identyfikatora URI.  Nie należy używać tego atrybutu, jeśli funkcja hello nie zwraca wartości. Oto Hello hello obsługiwane typy:

* **Kolekcja (<Entity type name>)**: Określa kolekcję typów zdefiniowanych jednostek. Nazwa Hello znajduje się w atrybutu nazwy hello hello obiektu dla węzła. Przykładem jest kolekcją (WXC. HourlyResult).
* **Nieprzetworzona (<mime type>)**: Określa raw dokumentu/blob, zwracana toohello użytkownika. Przykładem jest Raw(image/jpeg) inne przykłady:

  * ReturnType="Raw(text/plain)"
  * Obiekt ReturnType = "kolekcji (sage. DeleteAllUsageFilesEntity) "*

**d:Paging** — określa sposób obsługi stronicowania przez hello zasobu REST. Witaj w nawiasy gałęzi produkcji, używane będą wartości parametrów, np. strony = {$page} & wartość elementu itemsperpage = {$size} hello dostępne opcje to:

* **Brak:** stronicowania nie jest dostępna
* **Pomiń:** stronicowania to wyrazić za pomocą logicznych "Pomiń" i "zajmuje" (u góry). Pomiń tę łódź jeża M elementów i podejmij, a następnie zwraca hello dalej N elementów. Wartość parametru: $skip
* **Podejmij:** podjęcia zwraca hello dalej N elementów. Wartość parametru: $take
* **Wartość PageSize:** stronicowania to wyrazić za pomocą strony logicznej i rozmiaru (elementów na stronie). Strona reprezentuje hello bieżącej strony, która jest zwracana. Wartość parametru: $page
* **Rozmiar:** rozmiar reprezentuje hello liczbę elementów zwróconych dla każdej strony. Wartość parametru: $size

**d:AllowedHttpMethods** *(opcjonalnie)* — Określa, które zlecenie jest obsługiwany przez hello zasobu REST. Ponadto ogranicza toohello zaakceptowane zlecenie określona wartość.  Domyślne = POST.  *Przykład:* `d:AllowedHttpMethods="GET"` hello dostępne opcje to:

* **GET:** zwykle używany tooreturn danych
* **POST:** zwykle używany tooinsert nowych danych.
* **Umieść:** zwykle używany tooupdate danych
* **Usuń:** używane toodelete danych

Węzły podrzędne dodatkowe (nie pasuje do żadnego hello CSDL dokumentacji) w węźle FunctionImport hello są:

**d:RequestBody** *(opcjonalnie)* -toobe treści, wysyłane oczekuje Żądanie hello treść jest używane tooindicate, który hello żądania. Parametry mogą być podawane w treści żądania hello. Są w nawiasach klamrowych, np. wyrażone {parameterName}. Te parametry są zamapowane z hello dane wejściowe użytkownika na powitania treści, która jest przekazywane usługi toohello dostawcy zawartości. Hello requestBody element ma atrybut o nazwie httpMethod. Atrybut Hello umożliwia dwóch wartości:

* **POST:** używane, jeśli hello żądanie jest żądaniem POST protokołu HTTP
* **GET:** używane, jeśli jest hello żądania HTTP GET

    Przykład:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces** i **d:Namespace** — ten węzeł zawiera opis hello przestrzenie nazw, które są zdefiniowane w hello XML, który jest zwracany przez import funkcji hello (identyfikator URI punktu końcowego). Kod XML, który jest zwracany przez usługi zaplecza hello Hello może zawierać dowolną liczbę nazw toodifferentiate hello zawartość, która jest zwracana. **Wszystkie te obszary nazw, jeśli używana d:Map lub d:Match kwerendy XPath muszą toobe na liście.** węzeł d:Namespaces Hello zawiera zestaw/listy węzłów d:Namespace. Każde z nich wymieniono jednej przestrzeni nazw używany w odpowiedzi usługi zaplecza hello. Atrybut hello węzła d:Namespace hello są następujące Hello:

* **d:prefix:** hello prefiksu dla przestrzeni nazw hello, jak pokazano w hello XML wyników zwróconych przez usługę hello, np. f:FirstName, f:LastName, gdzie f jest prefiksem hello.
* **d:URI:** hello pełny identyfikator URI nazw hello używany w dokumencie wynik hello. Reprezentuje wartość hello tego prefiksu hello jest rozwiązany tooat runtime.

**d:ErrorHandling** *(opcjonalnie)* — ten węzeł zawiera warunki do obsługi błędów. Każdy z warunków hello jest weryfikowany pod kątem hello wynik zwracany przez usługę hello dostawcy zawartości. Jeśli warunek zgodny hello proponowane kod błędu HTTP toohello przez użytkownika końcowego jest zwracany komunikat o błędzie.

**d:ErrorHandling** *(opcjonalnie)* i **d:Condition** *(opcjonalnie)* -węzła warunku zawiera jeden warunek, który jest sprawdzany w hello wynik zwracany przez Usługa Hello dostawcy zawartości. Witaj poniżej przedstawiono hello **wymagane** atrybuty:

* **d:match:** wyrażenie XPath, które sprawdza, czy dany węzeł/wartość znajduje się w dostawcy zawartości hello wyjściowy XML. Hello XPath jest wykonywane na powitania danych wyjściowych i powinien zwrócić wartość true, jeśli warunek hello jest dopasowania lub wartość false w przeciwnym razie wartość.
* **d:HttpStatusCode:** hello kod stanu HTTP, który ma zostać zwrócony przez Marketplace hello wielkość hello warunku dopasowań. Marketplace signalizes błędy toohello użytkownika za pomocą kodów stanu HTTP. Listę kodów stanu HTTP są dostępne pod adresem http://en.wikipedia.org/wiki/HTTP_status_code
* **d:ErrorMessage:** hello komunikat o błędzie zwrócony — z kodem stanu hello HTTP — toohello przez użytkownika końcowego. Powinno to być przyjazne komunikat, który nie zawiera żadnych kluczy tajnych.

**d:TITLE** *(opcjonalnie)* — umożliwia opisujące tytuł hello hello funkcji. wartość Hello tytułu hello pochodzi z

* Hello mapy opcjonalny atrybut (xpath) określający, gdzie toofind hello tytuł w odpowiedzi hello zwracanego z żądania usługi hello.
* - Lub - tytuł hello określony jako wartość hello węzła.

**d:Rights** *(opcjonalnie)* — Witaj prawa (np. o prawach autorskich) skojarzone z funkcją hello. wartość Hello prawa hello pochodzi od:

* Hello mapy opcjonalny atrybut (xpath) określający, gdzie toofind hello praw w odpowiedzi hello zwracanego z żądania usługi hello.
* - Lub - prawa hello określony jako wartość hello węzła.

**d:Description** *(opcjonalnie)* — krótki opis funkcji hello. wartość Hello opisu hello pochodzi z

* Hello mapy opcjonalny atrybut (xpath) określający, gdzie opis hello toofind w odpowiedzi hello zwracanego z żądania usługi hello.
* - Lub — opis hello określony jako wartość hello węzła.

**d:EmitSelfLink** - *można znaleźć w powyższym przykładzie "Element FunctionImport"stronicowanie, za pośrednictwem zwrócone dane"*

**d:EncodeParameterValue** -tooOData opcjonalne rozszerzenie

**d:QueryResourceCost** -tooOData opcjonalne rozszerzenie

**d:map** -tooOData opcjonalne rozszerzenie

**d:headers** -tooOData opcjonalne rozszerzenie

**d:headers** -tooOData opcjonalne rozszerzenie

**d:Value** -tooOData opcjonalne rozszerzenie

**d:HttpStatusCode** -tooOData opcjonalne rozszerzenie

**d:ErrorMessage** -tooOData opcjonalne rozszerzenie

## <a name="parameter-node"></a>Parametr węzła
Ten węzeł reprezentuje jeden parametr, który jest udostępniany jako część szablon identyfikatora URI hello / treści, który został określony w węźle FunctionImport hello żądania.

Znaleziono na stronie dokumentu bardzo przydatne szczegółowe informacje o węźle "Parameter Element" hello [tutaj](http://msdn.microsoft.com/library/ee473431.aspx) (Użyj hello **innych wersji** tooselect listy rozwijanej innej wersji, jeśli niezbędne tooview hello dokumentacji). *Przykład:*`<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Atrybut parametru | Jest wymagana | Wartość |
| --- | --- | --- |
| Nazwa |Tak |Nazwa Hello hello parametru. Uwzględniana wielkość liter!  Wielkość liter hello BaseUri. **Przykład:**`<Property Name="IsDormant" Type="Byte" />` |
| Typ |Tak |Typ parametru Hello. Witaj, wartość musi być **EDMSimpleType** lub typ złożony, który znajduje się w zakresie hello hello modelu. Aby uzyskać więcej informacji zobacz "6 właściwość parametru obsługiwane typy".  (Wielkość liter! Pierwszy znak jest wielką, rest są małe litery).  Zobacz też, [koncepcyjny modelu typów (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx). **Przykład:**`<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Tryb |Nie |**W**, Out lub InOut, w zależności od tego, czy parametr hello jest danych wejściowych, wyjściowych lub parametr wejścia/wyjścia. (Tylko "W" są dostępne w portalu Azure Marketplace.) **Przykład:**`<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| Element maxLength |Nie |Witaj maksymalną dozwoloną długość parametru hello. **Przykład:**`<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| dokładność |Nie |Precyzja Hello hello parametru. **Przykład:**`<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Skalowanie |Nie |Skala Hello hello parametru. **Przykład:**`<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Oto Hello hello atrybuty, które zostały dodane Specyfikacja pliku CSDL toohello:

| Atrybut parametru | Opis |
| --- | --- |
| **d:regex** *(opcjonalnie)* |Instrukcja wyrażenia regularnego używane wartości wejściowej hello toovalidate hello parametru. Jeśli hello wartość wejściowa nie jest zgodna hello instrukcji hello wartością się niepowodzeniem. Dzięki temu toospecify także zestaw możliwych wartości, np. ^ [0-9] +? $ tooonly zezwalanie na liczby. **Przykład:** ' < Nazwa parametru = "name" tryb = "In" Type = "String" d: wartości null = "false" d:Regex = "^ [a-zA-Z] * $" d:Description = "A nazwę, która nie może zawierać spacji ani znaków innych niż angielskie innych niż alfanumeryczne" d:SampleValues = "George |
| **d:Enum** *(opcjonalnie)* |Lista wartości jest nieprawidłowa dla parametru hello rozdzielonych potoku. Typ Hello hello wartości musi toomatch hello zdefiniowany typ parametru hello. Przykład: "angielski |
| **d: Nullable** *(opcjonalnie)* |Umożliwia zdefiniowanie, czy parametr może mieć wartości null. Domyślna Hello to: true. Jednak parametry, które są dostępne jako część ścieżki hello hello szablon identyfikatora URI nie może mieć wartości null. Jeśli ustawiono atrybut hello toofalse dla tych parametrów — dane wejściowe użytkownika hello jest wyłączona. **Przykład:**`<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(opcjonalnie)* |Przykładowe wartości toodisplay jako toohello Uwaga klienta w hello interfejsu użytkownika.  Możliwe jest listy tooadd kilka wartości za pomocą potoku oddzielone, tj. " |

## <a name="entitytype-node"></a>Dla obiektu węzła
Ten węzeł reprezentuje jeden z typów hello, które zostaną zwrócone z witryny Marketplace toohello użytkownika. Zawiera ona także hello mapowania z danych wyjściowych hello, zwracane przez wartości toohello usługi hello dostawcy zawartości, które są zwracane toohello przez użytkownika końcowego.

Szczegółowe informacje o tym węźle znajdują się w [tutaj](http://msdn.microsoft.com/library/bb399206.aspx) (Użyj hello **innych wersji** tooselect listy rozwijanej innej wersji, jeśli niezbędne tooview hello dokumentacji.)

| Nazwa atrybutu | Jest wymagana | Wartość |
| --- | --- | --- |
| Nazwa |Tak |Nazwa Hello hello typu jednostki. **Przykład:**`<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| Typ BaseType |Nie |Nazwa Hello innego typu jednostki, który jest typem podstawowym hello hello typu jednostki, który jest definiowany. **Przykład:**`<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Oto Hello hello atrybuty, które zostały dodane Specyfikacja pliku CSDL toohello:

**d:map** -wykonywane względem danych wyjściowych usługi hello wyrażenie XPath. Witaj w tym miejscu jest założenie hello usługi w danych wyjściowych zawiera zestaw elementów, które powtórzyć, jak źródło ATOM, gdzie istnieje zestaw określonych węzłów zapisu Powtarzaj. Każdy z tych powtarzające się węzły zawiera jeden rekord. Witaj XPath jest toopoint określony w poszczególnych węźle powtarzających się hello w wyniku usługi hello dostawcy zawartości, który zawiera wartości hello pojedynczego rekordu. Przykład danych wyjściowych z usługi hello:

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Witaj wyrażenie XPath byłoby /foo/bar, ponieważ każdy węzeł pasek hello jest hello powtarzające się węzeł w hello output i zawiera hello rzeczywistej zawartości, zwracana toohello przez użytkownika końcowego.

**Klucz** -tego atrybutu jest ignorowana przez Marketplace. REST na podstawie usług sieci web, ogólnie rzecz biorąc, nie uwidacznia klucza podstawowego.

## <a name="property-node"></a>Właściwości węzła
Ten węzeł zawiera jedną właściwość hello rekordu.

Szczegółowe informacje o tym węźle znajdują się w [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (Użyj hello **innych wersji** tooselect listy rozwijanej innej wersji, jeśli niezbędne tooview hello dokumentacji.) *Przykład:*`<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | Wymagane | Wartość |
| --- | --- | --- |
| Nazwa |Tak |Nazwa Hello hello właściwości. |
| Typ |Tak |Typ Hello hello wartości właściwości. Typ wartości właściwości Hello musi być **EDMSimpleType** lub typ złożony (wskazywanym przez w pełni kwalifikowaną nazwą), który znajduje się w zakresie hello modelu. Aby uzyskać więcej informacji Zobacz typy modelu koncepcyjnego (CSDL). |
| Dopuszczające wartości zerowe |Nie |**Wartość true,** (wartość domyślna hello) lub **False** w zależności od tego, czy właściwość hello może mieć wartości null. Uwaga: W hello wersji pliku CSDL oznaczone hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) przestrzeni nazw, właściwość typu złożonego musi mieć Nullable = "False". |
| Wartość domyślna |Nie |Wartość domyślna właściwości hello Hello. |
| Element maxLength |Nie |Maksymalna długość Hello hello wartości właściwości. |
| FixedLength |Nie |**Wartość true,** lub **False** w zależności od tego, czy wartość właściwości hello będą przechowywane jako ciąg o długości fiexed. |
| dokładność |Nie |Oznacza maksymalną liczbę cyfr tooretain w wartość liczbową hello toohello. |
| Skalowanie |Nie |Maksymalna liczba miejsc dziesiętnych tooretain w wartość liczbową hello. |
| Unicode |Nie |**Wartość true,** lub **False** w zależności od tego, czy wartość właściwości hello być przechowywane w postaci ciągu Unicode. |
| Sortowanie |Nie |Ciąg określający hello sortowanie używane w źródle danych hello toobe sekwencji. |
| Właściwość ConcurrencyMode |Nie |**Brak** (wartość domyślna hello) lub **stałe**. Jeśli ustawiono wartość hello zbyt**stałe**, zostanie użyta wartość właściwości hello w sprawdzenie optymistycznej współbieżności. |

Oto Hello hello dodatkowe atrybuty, które zostały dodane Specyfikacja pliku CSDL toohello:

**d:map** — wyrażenie XPath wykonywane względem usługi hello output i wyodrębnia jedną właściwość hello danych wyjściowych. Hello XPath określony jest względna toohello powtarzające się węzeł, który wybrano w XPath hello obiektu dla węzła. Możliwe jest również możliwe toospecify bezwzględną tooallow XPath tym statycznych zasobów w każdym hello output węzłów, takich jak na przykład praw autorskich instrukcję, która znajduje się tylko po w hello oryginalnego usługi output, ale powinien znajdować się w każdym wierszy hello w hello OData dane wyjściowe. Przykład z usługi hello:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

wyrażenie XPath Hello będzie ./bar/baz0 tooget hello baz0 węzeł z usługi hello dostawcy zawartości.

**d:CharMaxLength** — dla typu string, można określić hello maksymalną długość. Zobacz przykład CSDL usługi danych

**d:IsPrimaryKey** — wskazuje, czy kolumna hello jest hello klucza podstawowego w tabeli lub widoku hello. Zobacz przykład DataService CSDL.

**d:isExposed** — Określa, czy schemat tabeli hello jest widoczna (zazwyczaj true). Zobacz przykład CSDL usługi danych

**d:IsView** *(opcjonalnie)* — wartość true, jeśli jest oparta na widoku, a nie tabelę.  Zobacz przykład CSDL usługi danych

**d:Tableschema** — Zobacz przykład CSDL usługi danych

**d:ColumnName** — jest nazwą hello hello kolumny w widoku tabeli hello.  Zobacz przykład CSDL usługi danych

**d:IsReturned** — jest hello wartość logiczna określająca, czy hello usługi przedstawia klienta toohello tej wartości.  Zobacz przykład CSDL usługi danych

**d:IsQueryable** — jest hello wartość logiczna określająca, czy można użyć kolumny hello kwerendy bazy danych.   Zobacz przykład CSDL usługi danych

**d:OrdinalPosition** -numeryczne położenie kolumny hello wyglądu, x, hello tabeli lub widoku hello, gdzie x to od 1 toohello liczby kolumn w tabeli hello jest.  Zobacz przykład CSDL usługi danych

**d:DatabaseDataType** -ma typ danych hello hello kolumny w bazie danych hello, tj. typ danych SQL. Zobacz przykład CSDL usługi danych

## <a name="supported-parametersproperty-types"></a>Typy obsługiwane parametry lub właściwości.
Oto Hello hello obsługiwane typy parametrów i właściwości. (Z uwzględnieniem wielkości liter)

| Typy pierwotne | Opis |
| --- | --- |
| Wartość null |Reprezentuje hello braku wartości |
| Wartość logiczna |Reprezentuje hello koncepcji matematycznych logiki przechowywanymi w danych binarnych |
| Bajtów |Niepodpisane 8-bitową liczbę całkowitą |
| Data i godzina |Reprezentuje datę i godzinę z wartości z zakresu od północy 12:00:00, 1 stycznia, 1753 r. N.E. za pomocą 11:59:59 godzinach od, grudnia 9999 r. |
| Decimal |Reprezentuje wartości liczbowych za pomocą stałych precyzję i skalę. Tego typu można opisać liczbowa wartość z zakresu od 10 ujemna ^ 255 + 1 toopositive 10 ^ 255 -1 |
| O podwójnej precyzji |Reprezentuje zmiennoprzecinkowej numer z dokładnością do 15 cyfr, mogącej reprezentować wartości z przybliżonej zakresem granicach 2.23E-308 do 1.79E +308. **Użyj przecinka powodu tooExel eksportu problem** |
| Pojedynczy |Reprezentuje zmiennoprzecinkowej numer 7 cyfr precyzji, mogącej reprezentować wartości z przybliżonej zakresem granicach 1.18e-38 za pomocą 3.40E + 38 |
| Identyfikator GUID |Reprezentuje unikatowy identyfikator (128-bitowy) 16-bajtową wartość |
| Int16 |Reprezentuje wartość całkowita 16-bitowych |
| Int32 |Reprezentuje wartość całkowita 32-bitowa |
| Int64 |Reprezentuje wartość całkowita 64-bitowa |
| Ciąg |Reprezentuje stałej - lub znak danych o zmiennej długości |

## <a name="see-also"></a>Zobacz też
* Jeśli interesuje Cię w uzgodnieniu hello ogólny proces mapowania OData i cel, przeczytaj ten artykuł [danych usługi OData mapowania](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definicje, struktur i instrukcje.
* Jeśli jesteś zrecenzować przykłady, przeczytaj ten artykuł [przykłady mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee przykładowy kod i zrozumienie Składnia kodu i kontekstu.
* toohello tooreturn określonej ścieżki do publikowania toohello danych usługi Azure Marketplace, przeczytaj ten artykuł [Podręcznik publikowania danych usługi](marketplace-publishing-data-service-creation.md).
