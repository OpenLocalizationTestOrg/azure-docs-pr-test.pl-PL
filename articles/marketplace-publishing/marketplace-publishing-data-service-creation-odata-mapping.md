---
title: "toocreating aaaGuide usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrożyć usługę Data zakupu na hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Mapowanie istniejących tooOData usługi sieci web za pomocą pliku CSDL
> [!IMPORTANT]
> **W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.** Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners). Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Ten artykuł zawiera omówienie dotyczące toouse toomap CSDL tooan istniejącej usługi zgodne usługi OData. Wyjaśniono, jak toocreate hello dokumentu mapowania (CSDL) przekształcającą żądanie wejściowe hello z powitania klienta za pośrednictwem wywołania usługi i hello output (dane) ponownie toohello klienta za pośrednictwem zgodne źródła strumieniowego OData. Microsoft Azure Marketplace udostępnia użytkownikom końcowym toohello usług przy użyciu protokołu OData hello. Usługi, które są udostępniane przez dostawców zawartości (właścicielom danych) są widoczne w różnych formularzy, takich jak REST protokołu SOAP, itp.

## <a name="what-is-a-csdl-and-its-structure"></a>Co to jest plik CSDL, a jego struktury?
CSDL (koncepcyjnej Schema Definition Language) jest specyfikacją określające, jak bazy danych lub usługa sieci web toodescribe wspólnych usługi XML wyrażenia toohello portalu Azure Marketplace.

Proste omówienie hello **żądania przepływu:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Witaj **przepływ danych** znajduje się w hello przeciwne kierunek:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Rysunek 1** diagramy jak klienta może uzyskiwać dane z dostawcy zawartości (usługi) za pośrednictwem hello Azure Marketplace.  Hello CSDL jest używany przez hello mapowania/przekształcenia składnika toohandle hello żądania i przekazywania danych między hello zawartości dostawcy usług i hello żądania klienta.

*Rysunek 1: Szczegółowy przepływ żądaniom dostawca toocontent klienta za pośrednictwem portalu Azure Marketplace*

  ![Rysowanie](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

W tle na Atom, protokołu Atom i hello protokołu OData, na które hello kompilacji rozszerzenia portalu Azure Marketplace, zapoznaj się z tematem: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Fragment powyższego łącza: *"hello hello protokołu Open Data (OData poniżej określonego tooas) służy protokół tooprovide opartego na interfejsie REST dla operacji CRUD stylu (tworzenia, odczytu, aktualizacji i usuwania) względem zasobów udostępniony jako usługi danych. "Usługa danych" jest punktem końcowym w przypadku, gdy dane widoczne z co najmniej jeden "kolekcji" każdego z zero lub więcej "pozycje", które składają się z pary wartości o nazwie wpisany. OData jest opublikowane przez firmę Microsoft w obszarze standardów języka OASIS (organizacji hello przejścia z strukturalnych informacji standardów) tak, aby każdy użytkownik, który chce toocan kompilacji serwerów, klientów lub narzędzia bez ograniczeń lub opłat licencyjnych. "*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Są trzy najistotniejsze mających toobe zdefiniowane przez hello CSDL:
* Witaj **punktu końcowego** z hello usługodawcy hello sieci Web adres URI hello usługi
* Witaj **parametry danych** przekazywany jako wejściowych toohello usługodawcy definicje hello parametrów hello wysyłane usługi toohello dostawcy zawartości w dół toohello — typ danych.
* **Schemat** hello danych zwracanych schematu hello żądanie usługi toohello hello dane są dostarczane przez usługę hello dostawcy zawartości, w tym kontenerze, kolekcje/tabel, kolumn/zmiennych i typy danych.

powitania po diagram zawiera omówienie przepływu hello, z którym powitania klienta wprowadza hello OData instrukcji (usługa sieci web wywołania toohello dostawcy zawartości) toogetting hello wyników/dane ponownie.

  ![Rysowanie](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>kroki:
1. Klient wysyła żądanie za pośrednictwem wywołania usługi z parametry wejściowe zdefiniowane w XML toohello portalu Azure Marketplace
2. Plik CSDL jest używane toovalidate hello wywołania usługi.
   * Witaj sformatowany zgłoszenia serwisowego jest następnie wysyłana toohello usługi dostawców zawartości przez hello Azure Marketplace
3. Witaj Usługa sieci Web wykonuje i preforms hello akcji hello zlecenie Http (tj. GET) hello dane są zwracane, tooAzure Marketplace, gdzie hello żądanych danych (jeżeli istniał) jest ujawnia w formacie XML toohello klienta przy użyciu mapowania zdefiniowane w pliku CSDL hello hello.
4. Klient jest wiadomości powitania hello danych (jeżeli istniał) w formacie XML lub JSON

## <a name="definitions"></a>Definicje
### <a name="odata-atom-pub"></a>Protokołu OData ATOM
Ustaw rozszerzenie protokołu ATOM toohello, gdzie każdy wpis reprezentuje jeden wiersz wyniku. Hello zawartości część wpis hello jest rozszerzony toocontain hello wartości wiersza hello — jako pary wartości klucza. Więcej informacji znajduje się w tym miejscu: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>Plik CSDL - Conceptual Schema Definition Language
Umożliwia zdefiniowanie funkcji (SPROCs) i jednostek, które są dostępne za pośrednictwem bazy danych. Więcej informacji znaleźć tutaj: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Kliknij przycisk hello **inne wersje** listy rozwijanej i wybierz wersję, jeśli nie widzisz hello artykułu.
> 
> 

### <a name="edm---entry-data-model"></a>EDM - wpis modelu danych
* Omówienie: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Podgląd: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Typy danych: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Witaj poniżej pokazano hello szczegółowych przepływu tooRight po lewej stronie, z którym powitania klienta wprowadza hello OData instrukcji (usługa sieci web wywołania toohello dostawcy zawartości) toogetting hello wyników/dane ponownie:

  ![Rysowanie](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>Podstawowe informacje o pliku CSDL
CSDL (koncepcyjnej Schema Definition Language) jest specyfikacją określające, jak bazy danych lub usługa sieci web toodescribe wspólnych usługi XML wyrażenia toohello portalu Azure Marketplace. W tym artykule opisano CSDL kawałków hello krytyczny, który **umożliwia przekazywanie hello danych z toohello źródła danych hello Azure Marketplace.** elementy główne Hello są opisane w tym miejscu:

* Informacje o interfejsie opisem wszystkich funkcji dostępnych publicznie (FunctionImport węzeł)
* Informacje o typie danych dla wszystkich wiadomości requests(input) i responses(outputs) komunikatu (EntityContainer/EntitySet/EntityType węzłów)
* Informacje o toobe protokołu transportu hello powiązania używane (węzeł nagłówka)
* Informacje o adresie do lokalizowania hello określonej usługi (atrybut BaseURI)

Mówiąc hello CSDL reprezentuje kontraktu platformy - i niezależny od języka między żądający usługi hello i hello dostawcy usług. Przy użyciu hello CSDL, klient można zlokalizować usługi bazy danych i usługi sieci web i wywołać żadnego ze swoich publicznie dostępnych funkcji.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>Dotyczących tooa CSDL bazy danych lub kolekcji
**Witaj Specyfikacja pliku CSDL**

Plik CSDL jest opis gramatyki języka XML opisu usługi sieci web. Specyfikacja Hello, sam jest podzielony na 4 główne elementy: EntitySet, FunctionImport; Przestrzeń nazw, a dla obiektu.

toomake toounderstand ułatwia to Abstrakcja umożliwia powiązać tabelę tooa pliku CSDL.

Pamiętaj;

  Kontrakt i język-niezależne od platformy między hello reprezentuje CSDL **obiektu żądającego usługi** i hello **usługodawcy**. Przy użyciu pliku CSDL, **klienta** mogą zlokalizować **usługi bazy danych i usługi sieci web** i wywołać żadnego ze swoich publicznie dostępnych **funkcji.**

Dla hello Usługa danych czterech części pliku CSDL można traktować pod względem bazy danych, tabeli, kolumny i procedura składowana.

Następujący dla usługi danych dotyczących:

* Obiekt EntityContainer ~ = bazy danych
* Obiekt EntitySet ~ = tabeli
* Obiekt EntityType ~ = kolumn
* Element FunctionImport ~ = procedury składowanej

**Dozwolone zlecenia HTTP**

* GET — zwraca wartości z bazy danych hello (zwraca kolekcję)
* POST — używane toopass danych tooand opcjonalne wartości zwracanych z hello bazy danych (Utwórz nowy wpis w kolekcji hello, zwracany identyfikator/URI)
* Usuń — Usuwa dane z hello bazy danych (spowoduje usunięcie kolekcji)
* PUT — aktualizacji danych w bazie danych (Zastąp kolekcji lub utwórz taki)

## <a name="metadatamapping-document"></a>Dokument metadanych/mapowania
Dokument metadanych/mapowanie Hello jest używany toomap, który istniejącą witrynę sieci web dostawcy zawartości usług, dzięki czemu może być udostępniany jako usługi sieci web OData przez system Azure Marketplace hello. Jest on oparty na pliku CSDL i implementuje kilka rozszerzeń tooCSDL tooaccommodate hello potrzeb REST na podstawie usług sieci web za pośrednictwem portalu Azure Marketplace. rozszerzenia Hello znajdują się w hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) przestrzeni nazw.

Przykład Witaj CSDL: (kopiowania i wklejania hello w poniższym przykładzie plik CSDL w edytorze XML i zmień toomatch usługi.  Wklej do mapowania pliku CSDL karcie DataService podczas tworzenia usługi na powitania [publikowania portalu Marketplace Azure](https://publish.windowsazure.com)).

**Warunki:** toohello warunki dotyczące hello CSDL [Portal publikowania](https://publish.windowsazure.com) warunki interfejsu użytkownika (PPUI).

* Oferują "Title" w hello PPUI odnosi się tooMyWebOffer
* Moja firma w hello PPUI odnosi się zbyt**wydawcy, nazwa wyświetlana** w hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) interfejsu użytkownika
* Interfejs API odnosi się tooa sieci Web lub usługi danych (Plan hello PPUI)

**Hierarchia:** oferty, która ma plany właścicielem firmy (dostawcy zawartości), czyli service(s), który wiersz w górę z interfejsem API.

### <a name="webservice-csdl-example"></a>Przykład CSDL usługi sieci Web
Łączy tooa usługi, która jest ujawniany przez punkt końcowy aplikacji sieci web (np. aplikacji C#)

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> Wyświetl więcej przykładów CSDL usługi sieci Web w artykule hello [przykłady mapowania istniejące sieci web tooOData usługi za pośrednictwem CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>Przykład CSDL usługi danych
Łączy tooa usługi, która jest ujawniany tabelę lub widok jako punkt końcowy w poniższym przykładzie przedstawiono dwa interfejsy API dla bazy danych na podstawie pliku CSDL interfejsu API (możesz użyć widoków zamiast tabel).

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a>Zobacz też
* Jeśli interesuje Cię learning oraz opis hello określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.
* Jeśli jesteś zrecenzować przykłady, przeczytaj ten artykuł [przykłady mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee przykładowy kod i zrozumienie Składnia kodu i kontekstu.
* toohello tooreturn określonej ścieżki do publikowania toohello danych usługi Azure Marketplace, przeczytaj ten artykuł [Podręcznik publikowania danych usługi](marketplace-publishing-data-service-creation.md).

