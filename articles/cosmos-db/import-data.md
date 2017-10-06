---
title: "Narzędzie migracji aaaDatabase dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak otworzyć toouse hello źródłowej bazy danych Azure rozwiązania Cosmos danych migracji narzędzia tooimport danych tooAzure rozwiązania Cosmos bazy danych z różnych źródeł, takich jak pliki bazy danych MongoDB, SQL Server tabeli magazynu, Amazon DynamoDB, CSV i JSON. Konwersja tooJSON CSV."
keywords: "toojson CSV, narzędzi migracji bazy danych, przekonwertować csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Jak tooimport danych do bazy danych rozwiązania Cosmos Azure dla hello interfejsu API usługi DocumentDB?

Ten samouczek zawiera instrukcje dotyczące używania hello Azure DB rozwiązania Cosmos: narzędzia migracji danych interfejsu API usługi DocumentDB, które można importować dane z różnych źródeł, takich jak pliki w formacie JSON, CSV pliki, SQL, bazy danych MongoDB, Magazyn tabel Azure, Amazon DynamoDB oraz opcji Azure DocumentDB DB rozwiązania Cosmos Użyj interfejsu API kolekcji do kolekcji dla z bazy danych Azure rozwiązania Cosmos i hello interfejsu API usługi DocumentDB. narzędzia migracji danych Hello można również podczas migracji z kolekcji wielu partycji tooa Kolekcja jednej partycji dla hello interfejsu API usługi DocumentDB.

narzędzia migracji danych Hello działa tylko importowania danych do bazy danych rozwiązania Cosmos Azure do użycia z hello interfejsu API usługi DocumentDB. Importowanie danych do użycia z hello API tabeli lub interfejsu API programu Graph nie jest obsługiwane w tej chwili. 

tooimport dane do użycia z hello API bazy danych MongoDB, zobacz [bazy danych Azure rozwiązania Cosmos: jak dane toomigrate hello API bazy danych MongoDB?](mongodb-migrate.md).

Ten samouczek obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Instalacja narzędzia do migracji danych hello
> * Importowanie danych z różnych źródeł danych
> * Eksportowanie z tooJSON bazy danych Azure rozwiązania Cosmos

## <a id="Prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem powitalne instrukcje w tym artykule, upewnij się, że mają zainstalowane następujące hello:

* [Program Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) lub nowszej.

## <a id="Overviewl"></a>Omówienie narzędzia migracji danych hello
Narzędzie migracji danych Hello jest rozwiązaniem typu open source, który importuje dane tooAzure rozwiązania Cosmos bazy danych z różnych źródeł, takich jak:

* Pliki JSON
* MongoDB
* Oprogramowanie SQL Server
* Pliki CSV
* Azure Table Storage
* Amazon DynamoDB
* HBase
* Kolekcje usługi Azure DB rozwiązania Cosmos

Gdy narzędzie importowania hello zawiera graficzny interfejs użytkownika (dtui.exe), mogą być określane również z wiersza polecenia hello (dt.exe). W rzeczywistości istnieje opcja toooutput hello skojarzone polecenia po skonfigurowaniu importu za pośrednictwem hello interfejsu użytkownika. Tabelaryczne źródła danych (np. programu SQL Server lub plików CSV) można je przekształcać w taki sposób, że relacje hierarchiczne (dokumentów podrzędnych) można utworzyć podczas importowania. Zachowaj odczytywania toolearn więcej informacji na temat opcji źródła, przykładowe wiersze poleceń tooimport z każdego źródła, target — opcje i wyświetlić wyniki importu.

## <a id="Install"></a>Zainstaluj narzędzia migracji danych hello
Kod źródłowy narzędzia migracji Hello jest dostępna w witrynie GitHub w [to repozytorium](https://github.com/azure/azure-documentdb-datamigrationtool) i jest dostępny w wersji skompilowanej [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). Może skompilować rozwiązanie hello lub po prostu pobierać i wyodrębniać hello skompilowanej wersji tooa katalogu. Następnie uruchom dowolne:

* **Dtui.exe**: wersja interfejsu graficznego narzędzia hello
* **DT.exe**: wersja wiersza polecenia narzędzia hello

## <a name="import-data"></a>Importowanie danych

Po zainstalowaniu narzędzia hello jest czas tooimport danych. Jakiego typu dane chcesz tooimport?

* [Pliki w formacie JSON](#JSON)
* [MongoDB](#MongoDB)
* [Pliki eksportu bazy danych MongoDB](#MongoDBExport)
* [SQL Server](#SQL)
* [Pliki CSV](#CSV)
* [Azure Table storage](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Obiekt blob](#BlobImport)
* [Kolekcje usługi Azure DB rozwiązania Cosmos](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Importowania zbiorczego w usłudze Azure DB rozwiązania Cosmos](#DocumentDBBulkImport)
* [Importowania platformy Azure kolejny rekord DB rozwiązania Cosmos](#DocumentDSeqTarget)


## <a id="JSON"></a>pliki w formacie JSON tooimport
Witaj opcję importera źródło pliku JSON umożliwia tooimport jeden lub więcej plików JSON pojedynczego dokumentu lub pliki JSON, że każdy zawierać tablicę dokumentów JSON. Podczas dodawania folderów zawierających tooimport pliki JSON, dostępna jest opcja hello rekursywnie szukania plików w podfolderach.

![Opcje źródłowego pliku zrzut ekranu JSON - narzędzia migracji bazy danych](./media/import-data/jsonsource.png)

Poniżej przedstawiono niektóre pliki JSON tooimport przykłady wiersza polecenia:

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a>tooimport z bazy danych MongoDB

> [!IMPORTANT]
> Jeśli importujesz konto bazy danych Azure rozwiązania Cosmos tooan z obsługą bazy danych MongoDB, postępuj zgodnie z następującymi [instrukcje](mongodb-migrate.md).
> 
> 

Hello opcja importera źródłowej bazy danych MongoDB pozwala tooimport z poszczególnych kolekcji bazy danych MongoDB i opcjonalnie filtrować dokumentów za pomocą zapytania i/lub modyfikowanie hello strukturę dokumentu przy użyciu projekcji.  

![Zrzut ekranu MongoDB Opcje źródła](./media/import-data/mongodbsource.png)

ciąg połączenia Hello jest w formacie bazy danych MongoDB hello:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych MongoDB określony w polu Parametry połączenia hello są dostępne.
> 
> 

Wprowadź nazwę hello hello kolekcji, w którym dane zostaną zaimportowane. Opcjonalnie możesz określić lub udostępnić plik dla zapytania (np. {pop: {$gt: 5000}}) i/lub projekcji (np. {loc:0}) tooboth filtru i kształt hello danych toobe zaimportowane.

Poniżej przedstawiono niektóre tooimport przykłady wiersza polecenia z bazy danych MongoDB:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>pliki eksportu tooimport bazy danych MongoDB

> [!IMPORTANT]
> Jeśli importujesz konto bazy danych Azure rozwiązania Cosmos tooan z obsługą bazy danych MongoDB, postępuj zgodnie z następującymi [instrukcje](mongodb-migrate.md).
> 
> 

Hello opcję importera źródło pliku bazy danych MongoDB eksportu JSON umożliwia tooimport jeden lub więcej plików JSON wyprodukowane z hello mongoexport narzędzia.  

![Opcje źródła eksportu zrzut ekranu z bazy danych MongoDB](./media/import-data/mongodbexportsource.png)

Podczas dodawania foldery zawierające pliki w formacie JSON eksportu bazy danych MongoDB do zaimportowania, dostępna jest opcja hello rekursywnie szukania plików w podfolderach.

Oto tooimport przykładowy wiersz polecenia z bazy danych MongoDB eksportu pliki w formacie JSON:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport z programu SQL Server
Hello opcji importera źródła SQL pozwala tooimport z poszczególnych bazy danych programu SQL Server i opcjonalnie filtrować toobe rekordów hello zaimportowany za pomocą zapytania. Ponadto można zmodyfikować hello strukturę dokumentu, określając zagnieżdżenia separatora (więcej informacji na temat którego za chwilę).  

![Zrzut ekranu SQL źródła opcji - narzędzia migracji bazy danych](./media/import-data/sqlexportsource.png)

format Hello hello ciągu połączenia jest format parametrów połączenia SQL hello standardowa.

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie serwera SQL określony w polu Parametry połączenia hello są dostępne.
> 
> 

Hello zagnieżdżania właściwości separatora jest używane toocreate hierarchicznych (podrzędne dokumenty) podczas importowania. Należy wziąć pod uwagę następujące zapytanie SQL hello:

*Wybierz RZUTOWANIA (BusinessEntityID AS varchar) jako identyfikator, nazwę, typ adresu jako [Address.AddressType], AddressLine1 jako [Address.AddressLine1], miasta jako [Address.Location.City], StateProvinceName jako [Address.Location.StateProvinceName], KodPocztowy jako [Address.PostalCode], CountryRegionName jako [Address.CountryRegionName] z Sales.vStoreWithAddresses gdzie typ adresu = "Urząd główny"*

Polecenie to zwraca hello następujące wyniki (częściowe):

![Zrzut ekranu SQL wyników zapytania](./media/import-data/sqlqueryresults.png)

Należy zwrócić uwagę hello aliasy, takie jak Address.AddressType i Address.Location.StateProvinceName. Określając zagnieżdżenia separatora z ".", narzędzia importu hello tworzy adres i zaimportować dokumenty podrzędne Address.Location podczas hello. Oto przykład wynikowy dokumentu w usłudze Azure DB rozwiązania Cosmos:

*{"id": "956", "Name": "Bardziej precyzyjną sprzedaży i usługa", "Adres": {"Typ adresu": "Urząd główny", "AddressLine1": "#500 75 O'Connor ulicy", "Lokalizacja": {"Miasto": "Ottawie", "StateProvinceName": "Ontario"}, "KodPocztowy": "K4B 1S2", "CountryRegionName": "Kanada"}}*

Poniżej przedstawiono niektóre wiersza polecenia tooimport przykłady z programu SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>pliki CSV tooimport i przekonwertować tooJSON CSV
Hello opcję importera źródło pliku CSV umożliwia możesz tooimport jeden lub więcej plików CSV. Podczas dodawania foldery zawierające pliki CSV do zaimportowania, dostępna jest opcja hello rekursywnie szukania plików w podfolderach.

![Zrzut ekranu CSV źródła opcji - CSV tooJSON](media/import-data/csvsource.png)

Podobne toohello SQL źródło hello zagnieżdżania separatora właściwości może być używane toocreate hierarchicznych (podrzędne dokumenty) podczas importowania. Należy wziąć pod uwagę hello wiersz nagłówka CSV i wierszy danych:

![Zrzut ekranu CSV przykładowych rekordów - CSV tooJSON](./media/import-data/csvsample.png)

Należy zwrócić uwagę hello aliasy, takie jak DomainInfo.Domain_Name i RedirectInfo.Redirecting. Określając zagnieżdżenia separatora z ".", narzędzia importu hello utworzy DomainInfo i zaimportować dokumenty podrzędne RedirectInfo podczas hello. Oto przykład wynikowy dokumentu w usłudze Azure DB rozwiązania Cosmos:

*{"DomainInfo": {"Nazwa_domeny": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Federalne agencji":"Administracyjne konferencji hello Stanów Zjednoczonych","RedirectInfo": {"Przekierowywanie":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*

Narzędzie importu Hello podejmie tooinfer informacji o typie wartości bez cudzysłowów w plikach CSV (wartości w cudzysłowie zawsze są traktowane jako ciągi).  Typy są identyfikowane w następującej kolejności hello: numer, datetime, boolean.  

Istnieją dwa inne toonote zagadnienia dotyczące importowania danych CSV:

1. Domyślnie bez cudzysłowów wartości są zawsze usuwane dla kart i spacje, gdy wartości w cudzysłowie są zachowywane jako — jest. To zachowanie może zostać zastąpiona przez powitalne przycinanie podane wartości pola wyboru lub hello /s.TrimQuoted opcji wiersza polecenia.
2. Domyślnie bez cudzysłowów wartość null jest traktowana jako wartość null. To zachowanie można przesłonić (tj. Traktuj bez cudzysłowów null jako ciąg "null") z hello Traktuj nienotowane NULL jako ciąg wyboru lub hello /s.NoUnquotedNulls opcji wiersza polecenia.

Oto przykład wiersza polecenia do importowania danych CSV:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport z magazynem tabel Azure
Hello opcji importera źródłowego magazynu tabel Azure pozwala tooimport z pojedynczej tabeli magazynu tabel Azure i opcjonalnie filtrować toobe jednostek tabeli hello zaimportowane. Pamiętaj, że danych magazynu tabel Azure tooimport narzędzia migracji danych hello nie można używać do bazy danych Azure rozwiązania Cosmos do użytku z hello tabeli interfejsu API. Tylko importowanie tooAzure rozwiązania Cosmos DB do użycia z hello interfejsu API usługi DocumentDB jest obsługiwane w tej chwili.

![Opcje źródłowego magazynu tabel zrzut ekranu Azure](./media/import-data/azuretablesource.png)

format Hello hello parametry połączenia magazynu tabel Azure jest:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello określonego w polu Parametry połączenia hello wystąpienia magazynu tabel Azure są dostępne.
> 
> 

Wprowadź nazwę hello hello Azure tabeli, w którym dane zostaną zaimportowane. Opcjonalnie można określić [filtru](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Witaj opcji importera źródłowego magazynu tabel Azure ma hello następujące dodatkowe opcje:

1. Uwzględnij pola wewnętrznego
   1. -Obejmują wszystkie pola wewnętrzne (PartitionKey RowKey i sygnatura czasowa)
   2. Brak — Wyklucz wszystkie pola wewnętrznego
   3. RowKey - zawierać tylko pola RowKey hello
2. Wybierz kolumny
   1. Filtrów magazynu tabel Azure nie obsługuje prognoz. Jeśli chcesz tooonly importu określonych właściwości jednostki tabel Azure, dodać je toohello wybierz kolumny listy. Wszystkie inne właściwości jednostki zostanie zignorowany.

Oto tooimport przykładowy wiersz polecenia z magazynem tabel Azure:

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport z Amazon DynamoDB
Hello opcję importera źródło Amazon DynamoDB pozwala tooimport z pojedynczej tabeli Amazon DynamoDB i opcjonalnie filtrować toobe jednostek hello zaimportowane. Kilka szablonów znajdują się tak, aby ustawienie importu jest równie proste, jak to możliwe.

![Zrzut ekranu Amazon DynamoDB Opcje źródła - narzędzia migracji bazy danych](./media/import-data/dynamodbsource1.png)

![Zrzut ekranu Amazon DynamoDB Opcje źródła - narzędzia migracji bazy danych](./media/import-data/dynamodbsource2.png)

format Hello hello Amazon DynamoDB ciągu połączenia jest:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello Amazon DynamoDB wystąpienia określonego w polu Parametry połączenia hello są dostępne.
> 
> 

Oto tooimport przykładowy wiersz polecenia z Amazon DynamoDB:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>tooimport pliki z magazynu obiektów Blob platformy Azure
Witaj pliku JSON, plik eksportu bazy danych MongoDB i opcje importera źródło pliku CSV pozwala tooimport co najmniej jeden plik z magazynu obiektów Blob platformy Azure. Po określeniu adresu URL kontenera obiektów Blob i klucza konta, wystarczy podać wyrażenie regularne tooselect hello pliki tooimport.

![Opcje źródłowego pliku zrzutu ekranu obiektów Blob](./media/import-data/blobsource.png)

Poniżej przedstawiono pliki JSON tooimport przykładowy wiersz polecenia z magazynu obiektów Blob platformy Azure:

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport z kolekcji interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB
Hello opcja importera źródłowej bazy danych Azure rozwiązania Cosmos pozwala tooimport danych z jednej lub kilku kolekcjach bazy danych Azure rozwiązania Cosmos i opcjonalnie filtrować dokumentów za pomocą zapytania.  

![Opcje źródła zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/documentdbsource.png)

format Hello hello parametry połączenia bazy danych Azure rozwiązania Cosmos jest:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Witaj parametry połączenia bazy danych Azure rozwiązania Cosmos konta można pobrać z bloku klucze hello hello portalu Azure, zgodnie z opisem w [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md), ale nazwa hello hello bazy danych musi toohello toobe dołączone Parametry połączenia w hello następującego formatu:

    Database=<CosmosDB Database>;

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych Azure rozwiązania Cosmos w polu Parametry połączenia hello są dostępne.
> 
> 

tooimport z jednej bazy danych Azure rozwiązania Cosmos kolekcji, wprowadź nazwę hello hello kolekcji, w którym dane zostaną zaimportowane. tooimport z wielu kolekcji bazy danych Azure rozwiązania Cosmos, podaj toomatch wyrażenia regularnego co najmniej jedną nazwę kolekcji (np. collection01 | collection02 | collection03). Może opcjonalnie określić, lub określ plik dla filtru tooboth zapytania i kształtu toobe danych hello zaimportowane.

> [!NOTE]
> Ponieważ pola kolekcji hello akceptuje wyrażeń regularnych, jeśli import odbywa się z jednej kolekcji, których nazwa zawiera znaki wyrażenie regularne, te znaki muszą wyjściowym odpowiednio.
> 
> 

Hello opcja importera źródłowej bazy danych Azure rozwiązania Cosmos ma następujące hello zaawansowane opcje:

1. Obejmują pola wewnętrzne: Określa, czy właściwości systemu dokumentu tooinclude bazy danych Azure rozwiązania Cosmos w hello eksportu (np. _rid, _ts).
2. Liczba ponownych prób w przypadku niepowodzenia: Określa hello liczba tooretry hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).
3. Interwał ponawiania prób: Określa, jak długo toowait między ponawianie próby hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).
4. Tryb połączenia: Określa toouse tryb połączenia hello Azure DB rozwiązania Cosmos. dostępne opcje Hello są DirectTcp, DirectHttps i bramy. tryby bezpośrednie połączenie Hello są szybsze, gdy tryb bramy hello jest więcej zapory przyjazną, ponieważ używa ona tylko port 443.

![Zaawansowane opcje źródła zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> Witaj zaimportować tryb tooconnection domyślne narzędzie DirectTcp. Występują problemy z zaporą, Przełącz tryb tooconnection bramy, ponieważ wymaga ona tylko portu 443.
> 
> 

Poniżej przedstawiono niektóre tooimport przykłady wiersza polecenia z bazy danych rozwiązania Cosmos Azure:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Hello narzędzia importowania danych DB rozwiązania Cosmos Azure obsługuje również importowanie danych z hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md). Podczas importowania danych z lokalnego emulatora, ustaw punkt końcowy hello zbyt`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport z bazy danych HBase
Hello opcję importera źródło HBase pozwala tooimport dane z tabel HBase i opcjonalnie filtrowanie hello danych. Kilka szablonów znajdują się tak, aby ustawienie importu jest równie proste, jak to możliwe.

![Zrzut ekranu HBase Opcje źródła](./media/import-data/hbasesource1.png)

![Zrzut ekranu HBase Opcje źródła](./media/import-data/hbasesource2.png)

format Hello hello parametry połączenia bazy danych HBase Stargate jest:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych HBase w polu Parametry połączenia hello są dostępne.
> 
> 

Oto tooimport przykładowy wiersz polecenia z bazy danych HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>toohello tooimport interfejsu API usługi DocumentDB (importowania zbiorczego)
importer Azure rozwiązania Cosmos DB zbiorczego Hello umożliwia tooimport z dowolnego z opcjami dostępnego źródła hello przy użyciu procedury przechowywane bazy danych rozwiązania Cosmos Azure w celu zwiększenia wydajności. Narzędzie Hello obsługuje importu tooone podzielona na partycje pojedynczej bazy danych Azure rozwiązania Cosmos kolekcji, a także podzielonej importu, zgodnie z którymi danych jest podzielonym na partycje w wielu kolekcji podzielone na partycje pojedynczej bazy danych Azure rozwiązania Cosmos. Aby uzyskać więcej informacji na temat partycjonowania danych, zobacz [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md). Narzędzie Hello będzie utworzyć, wykonanie, a następnie usuń hello przechowywane procedury hello kolekcji docelowej.  

![Opcje zbiorczego zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/documentdbbulk.png)

format Hello hello parametry połączenia bazy danych Azure rozwiązania Cosmos jest:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Witaj parametry połączenia bazy danych Azure rozwiązania Cosmos konta można pobrać z bloku klucze hello hello portalu Azure, zgodnie z opisem w [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md), ale nazwa hello hello bazy danych musi toohello toobe dołączone Parametry połączenia w hello następującego formatu:

    Database=<CosmosDB Database>;

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych Azure rozwiązania Cosmos w polu Parametry połączenia hello są dostępne.
> 
> 

tooimport tooa pojedynczy kolekcji, wprowadź nazwę hello hello kolekcji toowhich dane zostaną zaimportowane i kliknij przycisk Dodaj hello. tooimport toomultiple kolekcje, wprowadź nazwy kolekcji indywidualnie lub użyj następującej składni toospecify hello wielu kolekcji: *collection_prefix*[Indeks - end indeks początkowy]. Podczas określania wielu kolekcji za pomocą składni wyżej wymienione hello, pamiętać o następujących hello:

1. Obsługiwane są tylko liczby całkowitej wzorce nazwy zakresu. Na przykład określenie kolekcji [0-3] utworzy hello następujące kolekcje: collection0, collection1, collection2, collection3.
2. Za pomocą składni skróconej: kolekcji [3] będzie emitować tego samego zestawu kolekcje wymienionych w kroku 1.
3. Można podać więcej niż jeden podstawienia. Na przykład, Kolekcja [0-1] [0-9] wygeneruje 20 nazwy kolekcji z zerami (collection01,... 02... 03).

Po hello kolekcji nazwy zostały określone, wybrać żądaną przepływność hello hello kolekcji (400 RUs too10, 000 RUs). Aby uzyskać najlepszą wydajność importu wybierz wyższej przepustowości. Aby uzyskać więcej informacji na temat poziomów wydajności, zobacz [poziomy wydajności w usłudze Azure DB rozwiązania Cosmos](performance-levels.md).

> [!NOTE]
> Witaj wydajności przepływności ustawienie dotyczy tylko tworzenie toocollection. Witaj określona kolekcja już istnieje, jej przepływności nie zostaną zmodyfikowane.
> 
> 

Podczas importowania toomultiple kolekcje, narzędzia importu hello obsługuje skrótu na podstawie dzielenia na fragmenty. W tym scenariuszu, określ właściwość dokumentu hello mają toouse jako klucza partycji hello (Jeśli klucz partycji jest puste, dokumenty będą podzielonej losowo w kolekcji docelowej hello).

Opcjonalnie można określić które pole w źródle importu hello powinna być używana jako hello właściwość identyfikatora dokumentu bazy danych Azure rozwiązania Cosmos podczas importowania hello (należy pamiętać, że jeśli dokumenty nie zawierają tej właściwości, następnie narzędzia importu hello wygeneruje GUID jako wartość właściwości identyfikator hello).

Brak dostępnych kilka opcji zaawansowanych podczas importowania. Najpierw gdy narzędzie hello zawiera zbiorczego domyślne importowania procedury składowanej (BulkInsert.js), można wybrać toospecify procedura przechowywana importu:

 ![Opcje sproc wstawiania zbiorczego zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/bulkinsertsp.png)

Ponadto podczas importowania typów danych (np. z serwera SQL lub bazy danych MongoDB), można wybrać jedną z trzech opcji importowania:

 ![Opcje importowania czasu Data zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/datetimeoptions.png)

* Ciąg: Wartość ciągu utrzymana
* Epoka: Utrwalić jako wartość liczbową epoka.
* Zarówno: Utrwalanie zarówno ciąg, jak i epoki wartości liczbowe. Ta opcja spowoduje utworzenie podrzędnego, na przykład: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "epoki": 1382390245}

Hello Azure rozwiązania Cosmos DB zbiorczego importer ma hello następujące dodatkowe opcje zaawansowane:

1. Rozmiar partii: hello narzędzia domyślne tooa rozmiar partii 50.  W przypadku dużych toobe dokumenty hello zaimportowane należy wziąć pod uwagę obniżenia hello rozmiar partii. Z drugiej strony w przypadku małych toobe dokumenty hello zaimportowane należy rozważyć zwiększenie rozmiaru partii hello.
2. Maksymalny rozmiar skryptu (w bajtach): narzędzie hello domyślne tooa skryptu Maksymalny rozmiar 512 KB
3. Wyłącz automatyczne generowanie identyfikator: Jeśli każdego toobe dokumentu zaimportowane zawiera pole identyfikatora, wybierając tę opcję można zwiększyć wydajność. Brak pola Unikatowy identyfikator dokumenty nie zostaną zaimportowane.
4. Aktualizacja istniejące dokumenty: hello toonot domyślne narzędzie zastępowanie istniejących dokumentów konflikt identyfikatorów. Wybranie tej opcji pozwoli zastępowanie istniejących dokumentów ze zgodnymi identyfikatorami. Ta funkcja jest przydatne w przypadku migracji danych zaplanowane, które zaktualizować istniejące dokumenty.
5. Liczba ponownych prób w przypadku niepowodzenia: Określa hello liczba tooretry hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).
6. Interwał ponawiania prób: Określa, jak długo toowait między ponawianie próby hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).
7. Tryb połączenia: Określa toouse tryb połączenia hello Azure DB rozwiązania Cosmos. dostępne opcje Hello są DirectTcp, DirectHttps i bramy. tryby bezpośrednie połączenie Hello są szybsze, gdy tryb bramy hello jest więcej zapory przyjazną, ponieważ używa ona tylko port 443.

![Zaawansowane opcje importowania zbiorczego zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> Witaj zaimportować tryb tooconnection domyślne narzędzie DirectTcp. Występują problemy z zaporą, Przełącz tryb tooconnection bramy, ponieważ wymaga ona tylko portu 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>toohello tooimport interfejsu API usługi DocumentDB (sekwencyjnych importowanie rekordów)
importer sekwencyjnych rekordu bazy danych Azure rozwiązania Cosmos Hello umożliwia tooimport z Opcje dostępnego źródła hello na podstawie rekordu na podstawie. Możesz wybrać tę opcję, jeśli importowany tooan istniejącą kolekcję, która osiągnęła limit przydziału procedur składowanych. Witaj narzędzie obsługuje importu tooa pojedynczy kolekcji bazy danych Azure rozwiązania Cosmos (jednej partycji i wielu partycji), a także podzielonej importu, zgodnie z którymi danych jest podzielona na partycje w wielu kolekcjach bazy danych Azure rozwiązania Cosmos jednej partycji i/lub wielu partycji. Aby uzyskać więcej informacji na temat partycjonowania danych, zobacz [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).

![Zrzut ekranu Azure DB rozwiązania Cosmos opcje sekwencyjnych importowania rekordów](./media/import-data/documentdbsequential.png)

format Hello hello parametry połączenia bazy danych Azure rozwiązania Cosmos jest:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Witaj parametry połączenia bazy danych Azure rozwiązania Cosmos konta można pobrać z bloku klucze hello hello portalu Azure, zgodnie z opisem w [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md), ale nazwa hello hello bazy danych musi toohello toobe dołączone Parametry połączenia w hello następującego formatu:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych Azure rozwiązania Cosmos w polu Parametry połączenia hello są dostępne.
> 
> 

tooimport tooa pojedynczy kolekcji, wprowadź nazwę hello hello kolekcji toowhich dane zostaną zaimportowane i kliknij przycisk Dodaj hello. tooimport toomultiple kolekcje, wprowadź nazwy kolekcji indywidualnie lub użyj następującej składni toospecify hello wielu kolekcji: *collection_prefix*[Indeks - end indeks początkowy]. Podczas określania wielu kolekcji za pomocą składni wyżej wymienione hello, pamiętać o następujących hello:

1. Obsługiwane są tylko liczby całkowitej wzorce nazwy zakresu. Na przykład określenie kolekcji [0-3] utworzy hello następujące kolekcje: collection0, collection1, collection2, collection3.
2. Za pomocą składni skróconej: kolekcji [3] będzie emitować tego samego zestawu kolekcje wymienionych w kroku 1.
3. Można podać więcej niż jeden podstawienia. Na przykład, Kolekcja [0-1] [0-9] wygeneruje 20 nazwy kolekcji z zerami (collection01,... 02... 03).

Po hello kolekcji nazwy zostały określone, wybrać żądaną przepływność hello hello kolekcji (400 RUs too250, 000 RUs). Aby uzyskać najlepszą wydajność importu wybierz wyższej przepustowości. Aby uzyskać więcej informacji na temat poziomów wydajności, zobacz [poziomy wydajności w usłudze Azure DB rozwiązania Cosmos](performance-levels.md). Wszelkie zaimportować toocollections o przepływności > 10 000 RUs będzie wymagać klucza partycji. Jeśli wybierzesz toohave więcej niż 250 000 RUs, konieczne będzie toofile żądania w portalu toohave hello zwiększyć Twoje konto.

> [!NOTE]
> Witaj przepływności ustawienie dotyczy tylko tworzenie toocollection. Witaj określona kolekcja już istnieje, jej przepływności nie zostaną zmodyfikowane.
> 
> 

Podczas importowania toomultiple kolekcje, narzędzia importu hello obsługuje skrótu na podstawie dzielenia na fragmenty. W tym scenariuszu, określ właściwość dokumentu hello mają toouse jako klucza partycji hello (Jeśli klucz partycji jest puste, dokumenty będą podzielonej losowo w kolekcji docelowej hello).

Opcjonalnie można określić które pole w źródle importu hello powinna być używana jako hello właściwość identyfikatora dokumentu bazy danych Azure rozwiązania Cosmos podczas importowania hello (należy pamiętać, że jeśli dokumenty nie zawierają tej właściwości, następnie narzędzia importu hello wygeneruje GUID jako wartość właściwości identyfikator hello).

Brak dostępnych kilka opcji zaawansowanych podczas importowania. Po pierwsze podczas importowania typów danych (np. z serwera SQL lub bazy danych MongoDB), można wybrać jedną z trzech opcji importowania:

 ![Opcje importowania czasu Data zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/datetimeoptions.png)

* Ciąg: Wartość ciągu utrzymana
* Epoka: Utrwalić jako wartość liczbową epoka.
* Zarówno: Utrwalanie zarówno ciąg, jak i epoki wartości liczbowe. Ta opcja spowoduje utworzenie podrzędnego, na przykład: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "epoki": 1382390245}

Hello Azure DB rozwiązania Cosmos — importer kolejny rekord ma hello następujące dodatkowe opcje zaawansowane:

1. Liczba żądań równoległych: narzędzie hello domyślne too2 równoległych żądań. W przypadku małych toobe dokumenty hello zaimportowane należy rozważyć zwiększenie numeru hello równoległych żądań. Należy pamiętać, że jeśli ta liczba jest wywoływane zbyt dużo hello importu mogą wystąpić ograniczenia przepustowości.
2. Wyłącz automatyczne generowanie identyfikator: Jeśli każdego toobe dokumentu zaimportowane zawiera pole identyfikatora, wybierając tę opcję można zwiększyć wydajność. Brak pola Unikatowy identyfikator dokumenty nie zostaną zaimportowane.
3. Aktualizacja istniejące dokumenty: hello toonot domyślne narzędzie zastępowanie istniejących dokumentów konflikt identyfikatorów. Wybranie tej opcji pozwoli zastępowanie istniejących dokumentów ze zgodnymi identyfikatorami. Ta funkcja jest przydatne w przypadku migracji danych zaplanowane, które zaktualizować istniejące dokumenty.
4. Liczba ponownych prób w przypadku niepowodzenia: Określa hello liczba tooretry hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).
5. Interwał ponawiania prób: Określa, jak długo toowait między ponawianie próby hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).
6. Tryb połączenia: Określa toouse tryb połączenia hello Azure DB rozwiązania Cosmos. dostępne opcje Hello są DirectTcp, DirectHttps i bramy. tryby bezpośrednie połączenie Hello są szybsze, gdy tryb bramy hello jest więcej zapory przyjazną, ponieważ używa ona tylko port 443.

![Zrzut ekranu z rozwiązania Cosmos bazy danych platformy Azure kolejny rekord importu zaawansowane opcje](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> Witaj zaimportować tryb tooconnection domyślne narzędzie DirectTcp. Występują problemy z zaporą, Przełącz tryb tooconnection bramy, ponieważ wymaga ona tylko portu 443.
> 
> 

## <a id="IndexingPolicy"></a>Określ zasady indeksowania, podczas tworzenia kolekcji bazy danych Azure rozwiązania Cosmos
Jeśli zezwolisz na powitania migracji kolekcji toocreate narzędzie podczas importowania, można określić zasady indeksowania hello hello kolekcji. W hello zaawansowane opcje sekcji hello pomocą importowania zbiorczego DB rozwiązania Cosmos Azure oraz Azure rozwiązania Cosmos DB sekwencyjnych opcje rekordu Przejdź toohello zasady indeksowania sekcji.

![Zrzut ekranu Azure rozwiązania Cosmos DB indeksowania zasad opcje zaawansowane](./media/import-data/indexingpolicy1.png)

Przy użyciu hello opcja zasady indeksowania, zaawansowane, wybierz plik zasady indeksowania, ręcznie wprowadzić zasady indeksowania lub wybierać zestaw domyślnych szablonów (przez kliknięcie prawym przyciskiem myszy w hello indeksowania pola tekstowego zasad).

Szablony zasad Hello, które udostępnia narzędzie hello są:

* Domyślne. Ta zasada jest najlepszy, gdy jest wykonywanie zapytań o równość dotyczących ciągów oraz przy użyciu ORDER BY, zakresu i zapytań o równość dotyczących liczb. Ta zasada ma mniejszy narzut magazynu indeksu niż zakres.
* Zakres. Ta zasada jest najlepszym, że używasz zapytań ORDER BY, o zakres i równości na liczb i ciągów. Ta zasada ma wyższy narzut na przechowywanie indeksu niż domyślne lub wyznaczania wartości skrótu.

![Zrzut ekranu Azure rozwiązania Cosmos DB indeksowania zasad opcje zaawansowane](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Jeśli nie określisz zasady indeksowania, hello domyślne zasady zostaną zastosowane. Aby uzyskać więcej informacji na temat zasad indeksowania, zobacz [Azure DB rozwiązania Cosmos zasady indeksowania](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>Eksportuj plik tooJSON
Hello Azure rozwiązania Cosmos bazy danych JSON eksportera umożliwia tooexport żadnego hello dostępnego źródła opcje tooa pliku JSON, który zawiera tablicę dokumentów JSON. Narzędzie Hello obsłuży hello eksportu dla Ciebie lub polecenie tooview hello wynikowy migracji i uruchom polecenie hello samodzielnie. Wynikowy plik JSON Hello mogą być przechowywane lokalnie lub w magazynie obiektów Blob Azure.

![Opcja eksportowania pliku lokalnego zrzut ekranu z Azure rozwiązania Cosmos bazy danych JSON](./media/import-data/jsontarget.png)

![Opcja eksportowania magazynu zrzut ekranu z rozwiązania Cosmos bazy danych JSON Azure obiektów Blob platformy Azure](./media/import-data/jsontarget2.png)

Opcjonalnie można hello tooprettify wynikowa JSON, który spowoduje zwiększenie rozmiaru hello hello utworzonego dokumentu, podczas wprowadzania hello zawartości więcej do odczytu.

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a>Konfiguracja zaawansowana
Na ekranie konfiguracji zaawansowanej hello Określ lokalizację hello toowhich pliku dziennika hello ma błędy zapisane. następujące reguły Hello stosowanie toothis strony:

1. Jeśli nie podano nazwy pliku, na stronie wyników hello zwracane jest wszystkie błędy.
2. Jeśli nazwa pliku bez katalogu, zostanie następnie hello plik zostanie utworzony (lub zastąpione) w katalogu bieżącego środowiska hello.
3. W przypadku wybrania istniejącego pliku, a następnie hello plik zostanie zastąpiony, nie jest dostępna opcja dołączania.

Następnie wybierz pozycję czy toolog wszystkie, krytyczne, lub żadne komunikaty o błędach. Na koniec zdecyduj, jak często zostaną zaktualizowane hello na ekranie transferu wiadomości o postępie.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Potwierdź ustawienia importowania i widok wiersza polecenia
1. Po określeniu informacji o źródle, informacji o docelowej i konfiguracji zaawansowanej, Przejrzyj podsumowanie migracji hello i, opcjonalnie, widok/kopiowania hello co polecenia migracji (kopiowanie polecenie hello jest przydatne tooautomate operacji importowania):
   
    ![Zrzut ekranu przedstawiający ekran podsumowania](./media/import-data/summary.png)
   
    ![Zrzut ekranu przedstawiający ekran podsumowania](./media/import-data/summarycommand.png)
2. Po zakończeniu opcje źródłowego i docelowego kliknij **importu**. czas, który upłynął Hello, liczba przekazanych i informacje o błędzie (Jeśli nie podasz nazwę pliku w konfiguracji zaawansowanej hello) zaktualizuje importu hello jest w toku. Po wykonaniu tych czynności możesz wyeksportować wyniki hello (np. toodeal o niepowodzeniach import).
   
    ![Zrzut ekranu z Azure rozwiązania Cosmos bazy danych JSON opcji eksportu](./media/import-data/viewresults.png)
3. Może także uruchomić nowy import, albo utrzymywanie hello istniejących ustawień (np. ciąg połączenia wybór informacji, źródłowa i docelowa itp.) lub zresetowanie wszystkich wartości.
   
    ![Zrzut ekranu z Azure rozwiązania Cosmos bazy danych JSON opcji eksportu](./media/import-data/newimport.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Zainstalowane narzędzie migracji danych hello
> * Importowane dane z różnych źródeł danych
> * Wyeksportowane z bazy danych Azure rozwiązania Cosmos tooJSON

Można teraz kontynuować toohello następny samouczek i Dowiedz się, jak tooquery danych przy użyciu bazy danych Azure rozwiązania Cosmos. 

> [!div class="nextstepaction"]
>[Jak tooquery danych?](../cosmos-db/tutorial-query-documentdb.md)
