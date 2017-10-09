---
title: aaaUsing biblioteki klienta elastycznej bazy danych z programu Entity Framework | Dokumentacja firmy Microsoft
description: "Użyj kodowania bazy danych biblioteki klienta elastycznej bazy danych i strukturą Entity Framework"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Biblioteka klienta usługi elastycznej bazy danych z programu Entity Framework
Ten dokument zawiera hello zmian w aplikacji programu Entity Framework, które są potrzebne toointegrate z hello [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md). Witaj koncentruje się na tworzenie [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) i [routingu zależne od danych](sql-database-elastic-scale-data-dependent-routing.md) z hello Entity Framework **Code First** podejście. Witaj [najpierw - Code nową bazę danych](http://msdn.microsoft.com/data/jj193542.aspx) samouczek dotyczący EF służy jako naszym przykładzie uruchomionych w tym dokumencie. Hello przykładowy kod towarzyszące ten dokument jest częścią narzędzi elastycznej bazy danych, ustaw próbek w hello przykłady kodu w usłudze Visual Studio.

## <a name="downloading-and-running-hello-sample-code"></a>Pobieranie i uruchamianie hello przykładowy kod
Kod hello toodownload tego artykułu:

* Visual Studio 2012 lub nowszy jest wymagany. 
* Pobierz hello [elastyczne narzędzia bazy danych dla bazy danych SQL Azure — przykładowy Entity Framework integracji](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) w witrynie MSDN. Rozpakuj hello próbki tooa lokalizacji wybrane.
* Uruchom program Visual Studio. 
* W programie Visual Studio wybierz Plik -> Otwórz projekt/rozwiązanie. 
* W hello **Otwórz projekt** okna dialogowego, przejdź do przykładowej toohello został pobrany i wybierz **EntityFrameworkCodeFirst.sln** tooopen hello próbki. 

toorun hello próbki, należy toocreate trzy pusty bazy danych w bazie danych SQL Azure:

* Bazy danych Menedżera Map niezależnego fragmentu
* 1 niezależnego fragmentu bazy danych
* 2 niezależnego fragmentu bazy danych

Po utworzeniu tych baz danych, wypełnij hello symbole zastępcze w **Program.cs** o nazwę serwera bazy danych SQL Azure, hello nazwy bazy danych i baz danych toohello tooconnect poświadczeń. Utworzenie rozwiązania hello w programie Visual Studio. Program Visual Studio pobierze hello wymaganych pakietów NuGet dla biblioteki klienta elastycznej bazy danych hello, Entity Framework i obsługa jako część procesu kompilacji hello wystąpienia błędu przejściowego. Upewnij się, że trwa przywracanie pakietów NuGet jest włączona dla rozwiązania. To ustawienie zostanie włączone, klikając prawym przyciskiem myszy plik rozwiązania hello w hello Visual Studio Solution Explorer. 

## <a name="entity-framework-workflows"></a>Przepływy pracy programu Entity Framework
Entity Framework deweloperzy polegać na jednym z czterech aplikacji toobuild przepływów pracy i tooensure trwałości dla obiektów aplikacji hello: 

* **Code First (Nowa baza danych)**: hello EF developer tworzy hello model w kodzie aplikacji hello, a następnie EF generuje hello bazy danych z niego. 
* **Code First (istniejącej bazy danych)**: hello developer umożliwia EF generowanie kodu aplikacji hello modelu hello na podstawie istniejącej bazy danych.
* **Model pierwszy**: hello developer tworzy hello model hello EF Designer, a następnie EF tworzy hello bazy danych z modelu hello.
* **Baza danych pierwszej**: hello deweloperów używa EF narzędzi tooinfer hello modelu z istniejącej bazy danych. 

Zarządzanie wszystkich tych sposobów polegać na tootransparently klasy DbContext hello połączenia bazy danych i schemat bazy danych dla aplikacji. Jak będzie omówiono bardziej szczegółowo w dalszej części dokumentu hello różnych konstruktorów w klasie podstawowej DbContext hello pozwolić na różne poziomy kontroli nad utworzenia połączenia bazy danych tworzenia uruchamianie i schematu. Wyzwania wynikają głównie z hello fakt, że zarządzanie połączenia bazy danych hello zapewniane przez EF przecina z możliwościami zarządzania połączenia hello hello danych zależnych interfejsów routingu podane przez biblioteki klienta elastycznej bazy danych hello. 

## <a name="elastic-database-tools-assumptions"></a>Założenia narzędzi elastycznej bazy danych
Aby uzyskać definicje terminów, zobacz [słownik narzędzi elastycznej bazy danych](sql-database-elastic-scale-glossary.md).

Z biblioteki klienta elastycznej bazy danych należy zdefiniować partycji o nazwie shardlets danych aplikacji. Shardlets są identyfikowane za pomocą klucza dzielenia na fragmenty i są mapowane toospecific baz danych. Aplikacja może mieć dowolną liczbę baz danych, zgodnie z potrzebami i dystrybuować hello shardlets tooprovide pojemności lub wydajności danego bieżące wymagania biznesowe. Mapowanie Hello baz danych toohello wartości klucza dzielenia na fragmenty są przechowywane przez mapy niezależnego fragmentu podana przez klienta elastycznej bazy danych hello interfejsów API. Nazywamy tej możliwości **zarządzania mapy niezależnego fragmentu**, lub SMM skrócie. Mapa niezależnego fragmentu Hello służy również jako hello brokera połączeń z bazą danych dla żądań zawierających klucz dzielenia na fragmenty. Firma Microsoft można znaleźć możliwości toothis jako **routingu zależne od danych**. 

Menedżera map niezależnego fragmentu Hello chroni użytkowników z widoków niespójne w shardlet dane, które mogą wystąpić, gdy są wykonywane operacje zarządzania równoczesnych shardlet (takich jak przemieszczenie dane z jednego niezależnego fragmentu tooanother). toodo Witaj, mapy niezależnego fragmentu zarządza powitania klienta biblioteki brokera hello połączenia bazy danych dla aplikacji. Dzięki temu hello niezależnego fragmentu mapy funkcji tooautomatically kill połączenia z bazą danych podczas operacji zarządzania niezależnego fragmentu może mieć wpływ na shardlet hello, utworzony hello połączenia dla. Ta metoda musi toointegrate z niektórych funkcji EF firmy, takich jak tworzenie nowych połączeń z istniejących toocheck jeden istnienie bazy danych. Ogólnie rzecz biorąc, naszych obserwacji została czy hello standardowe konstruktory DbContext tylko działają niezawodnie połączeniach zamkniętego bazy danych, które można bezpiecznie sklonować EF pracy. Zasada projektowania Hello elastycznej bazy danych zamiast tego jest tooonly brokera otwarte połączenia. Jeden wydaje się, że zamknięcie połączenia przeprowadzana przez bibliotekę klienta hello przed przekazaniem ich toohello EF DbContext może rozwiązać ten problem. Jednak zamykanie połączenia hello i polegania na otwieranie toore EF, jeden foregoes hello sprawdzania poprawności i sprawdzanie spójności z zastosowaniem biblioteki hello. Funkcja migracji Hello w EF, jednak wykorzystuje te hello toomanage połączeń podstawowy schemat bazy danych w sposób przezroczysty toohello aplikacji. Firma Microsoft najlepiej, jeśli chcesz tooretain i połączyć wszystkie te funkcje z biblioteki klienta elastycznej bazy danych hello i EF w hello tej samej aplikacji. Witaj następujących sekcji omówiono te właściwości i wymagania bardziej szczegółowo. 

## <a name="requirements"></a>Wymagania
Podczas pracy z biblioteki klienta elastycznej bazy danych hello i interfejsy API programu Entity Framework, chcemy hello tooretain następujące właściwości: 

* **Skalowalny w poziomie**: tooadd lub usuń baz danych z warstwy danych hello podzielonej aplikacji hello odpowiednio do potrzeb pojemności hello aplikacji hello. Oznacza to, kontrolę nad hello hello tworzenie i usuwanie baz danych i przy użyciu hello elastycznej bazy danych niezależnych Mapa Menedżera interfejsów API toomanage baz danych i mapowania shardlets. 
* **Spójność**: dzielenia na fragmenty zatrudnia aplikacji hello i używa hello zależne funkcje routingu danych powitania klienta biblioteki. uszkodzenie tooavoid lub wyników zapytania niewłaściwy połączenia jest przeprowadzana za pośrednictwem Menedżera map hello niezależnego fragmentu. Zachowuje również sprawdzania poprawności i spójność.
* **"Code First"**: tooretain wygodę hello EF przez kod pierwszego modelu. W pierwszym kodu klas w aplikacji hello są mapowane w sposób niewidoczny dla użytkownika toohello podstawowej struktury bazy danych. Kod aplikacji Hello współdziała z DbSets, który zamaskować większości aspektów związanych hello bazowy przetwarzanie bazy danych.
* **Schemat**: Entity Framework obsługuje tworzenie schematu bazy danych początkowej i kolejnych schematu zmiany za pomocą migracji. Zachowując te możliwości dostosowywania aplikacji jest łatwe jak powitalne rozwoju danych. 

Witaj poniższe wskazówki nakazuje jak toosatisfy tych wymagań Code First aplikacji za pomocą narzędzi elastycznej bazy danych. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Dane zależne routingu przy użyciu EF DbContext
Połączenia bazy danych z programu Entity Framework zwykle są zarządzane przez podklasy **DbContext**. Utworzyć te podklasy pochodny **DbContext**. Jest to, gdzie został zdefiniowany z **DbSets** implementują hello kopii bazy danych kolekcji obiektów CLR dla aplikacji. W kontekście hello danych zależnych routingu umożliwi nam poznanie kilka właściwości pomocne, które nie posiadają niekoniecznie dla innych pierwszy scenariuszy aplikacji EF kodu: 

* Witaj bazy danych już istnieje i został zarejestrowany w mapie niezależnego fragmentu elastycznej bazy danych hello. 
* Hello schematu aplikacji hello został już wdrożony toohello bazy danych (co omówiono poniżej). 
* Zależne od danych routingu połączeń toohello w bazie danych są obsługiwane przez brokera przez hello niezależnego fragmentu mapy. 

toointegrate **DbContexts** zależne od danych routingu dla skalowalnego w poziomie:

1. Utwórz połączenia fizycznej bazy danych za pośrednictwem interfejsów klienta elastycznej bazy danych hello Menedżera mapy niezależnego fragmentu hello, 
2. Zawijaj hello połączenia z hello **DbContext** podklasy
3. Przekaż hello połączenia w dół do hello **DbContext** hello przetwarzania po stronie EF hello się stanie, a także tooensure klasy podstawowej. 

Poniższy przykład kodu Hello przedstawiono tej metody. (Ten kod jest również hello towarzyszące projektu Visual Studio)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Główne punkty
* Nowy Konstruktor zastępuje hello domyślnego konstruktora w hello podklasy DbContext 
* Nowy Konstruktor Hello przyjmuje hello argumenty, które są wymagane dla danych zależnych routingu za pomocą biblioteki klienta elastycznej bazy danych:
  
  * Witaj niezależnego fragmentu mapy tooaccess hello interfejsów routingu zależne od danych,
  * Witaj dzielenia na fragmenty klucza tooidentify hello shardlet
  * Parametry połączenia przy użyciu poświadczeń hello na powitania zależne od danych routingu niezależnych toohello połączenia. 
* Konstruktor klasy podstawowej toohello wywołania Hello uwzględnia przekierowania statyczną metodę, która wykonuje wszystkie kroki hello niezbędne dla routingu zależne od danych. 
  
  * Używa hello OpenConnectionForKey wywołania interfejsów hello elastycznej bazy danych klienta na powitania niezależnego fragmentu mapy tooestablish otwartego połączenia.
  * Mapa niezależnego fragmentu Hello tworzy hello otwartego połączenia toohello niezależnych przechowujący hello shardlet dla danego klucza dzielenia na fragmenty hello.
  * To połączenie otwarte jest przekazywany konstruktora klasy podstawowej wstecz toohello tooindicate DbContext, czy to połączenie jest toobe używane przez EF, zamiast czekać na EF automatycznie Utwórz nowe połączenie. To połączenie hello sposób oznakowanym przez interfejs API do powitania klienta elastycznej bazy danych, dzięki czemu może zagwarantować spójności w operacjach zarządzania mapy niezależnego fragmentu.

Użyj hello nowy konstruktor podklasa użytkownika DbContext zamiast hello domyślnego konstruktora w kodzie. Oto przykład: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

Nowy Konstruktor Hello otwiera hello połączenia toohello niezależnych przechowujący dane powitania dla shardlet hello identyfikowane przez wartość hello **tenantid1**. Witaj kodu w hello **przy użyciu** bloku pozostaje niezmieniony tooaccess hello **DbSet** dla blogów za pomocą EF na powitania niezależnych dla **tenantid1**. Spowoduje to zmianę semantyki dla kodu hello w hello przy użyciu bloku w taki sposób, że wszystkie operacje bazy danych są teraz zakres toohello jednego niezależnego fragmentu gdzie **tenantid1** jest przechowywany. Na przykład zapytania LINQ za pośrednictwem blogi hello **DbSet** zwracać tylko blogi przechowywane na powitania bieżący identyfikator niezależnego fragmentu, ale nie hello te są przechowywane w innych fragmentów.  

#### <a name="transient-faults-handling"></a>Obsługa błędów przejściowych
Witaj Microsoft Patterns & rozwiązania zespołu opublikowanych hello [hello bloku aplikacji obsługi błędów przejściowych](https://msdn.microsoft.com/library/dn440719.aspx). Biblioteka Hello jest używany z biblioteki klienta elastycznej skali w połączeniu z EF. Jednak upewnić się, że przejściowy wyjątku zwraca tooa miejscu, gdzie możemy upewnij się, że tego konstruktora new hello jest używany po błędu przejściowego tak, aby wszystkie nowe połączenia podejmowana jest używanie konstruktorów hello, które firma Microsoft ma tweaked. W przeciwnym razie wartość toohello połączenia poprawny identyfikator niezależnego fragmentu nie jest gwarantowana i nie ma żadnych gwarancji połączenia hello jest obsługiwana jako zmiany wystąpić toohello niezależnego fragmentu mapy. 

Hello Poniższy przykładowy kod przedstawia sposób zasady ponawiania SQL może służyć wokół hello nowe **DbContext** podklas: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** w hello powyższy kod jest zdefiniowany jako **SqlDatabaseTransientErrorDetectionStrategy** z liczbą ponowień równą 10 i 5 sekund oczekiwania czasu między kolejnymi próbami. Ta metoda jest podobne wskazówki toohello EF i transakcji inicjowanych przez użytkownika (zobacz [ograniczenia strategiami ponowną próbą wykonania (EF6 i jego nowszych wersjach)](http://msdn.microsoft.com/data/dn307226). Zarówno sytuacje wymagają programu aplikacji hello steruje hello zakresu toowhich hello przejściowej wyjątek zwraca: tooeither ponownie transakcji hello, lub (jak pokazano) ponownie kontekstu hello z prawidłowego konstruktora hello, że używa hello elastycznej bazy danych Biblioteka klienta.

Hello toocontrol potrzeby w przypadku gdy wyjątki przejściowej podjąć nam w zakresie także wyklucza Użyj hello wbudowanych hello **klasy SqlAzureExecutionStrategy** dołączony EF. **Klasy SqlAzureExecutionStrategy** będzie ponownie otworzyć połączenie, ale nie używać **OpenConnectionForKey** ominięcie wszystkich weryfikacji hello wykonywanej jako część hello **OpenConnectionForKey** wywołania. Zamiast tego hello przykładowy kod używa wbudowanego hello **DefaultExecutionStrategy** również dołączony EF. W przeciwieństwie do zbyt**klasy SqlAzureExecutionStrategy**, działa on prawidłowo w połączeniu z hello zasady ponawiania z obsługi błędów przejściowych. zasady wykonywania Hello jest ustawiana w hello **ElasticScaleDbConfiguration** klasy. Należy pamiętać, że zdecydowaliśmy nie toouse **DefaultSqlExecutionStrategy** ponieważ sugeruje toouse **klasy SqlAzureExecutionStrategy** Jeśli wystąpią wyjątki przejściowy — które doprowadziłaby zachowanie toowrong zgodnie z opisem. Aby uzyskać więcej informacji na powitania zasady różnych ponownych prób i EF, zobacz [połączenia odporność EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Konstruktor modyfikacji oprogramowania
Hello kodu powyższych przykładach hello domyślnego konstruktora ponownie zapisuje wymagane przez aplikację w kolejności toouse danych zależnych routingu z hello Entity Framework. w poniższej tabeli Hello stanowi uogólnienie tego podejścia tooother konstruktorów. 

| Bieżący Konstruktor | Konstruktor nowych danych | Konstruktora podstawowego | Uwagi |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext (ShardMap, TKey) |DbContext (DbConnection, wartość logiczna) |połączenie Hello wymaga toobe funkcję mapy niezależnego fragmentu hello i klucz routingu hello zależne od danych. Należy tooby przebiegu połączenie automatyczne tworzenie przez EF i zamiast tego użyć hello niezależnego fragmentu mapy toobroker hello połączenia. |
| MyContext(string) |ElasticScaleContext (ShardMap, TKey) |DbContext (DbConnection, wartość logiczna) |połączenie Hello jest funkcją mapy niezależnego fragmentu hello i klucz routingu hello zależne od danych. Stałej bazy danych nazwa lub parametry połączenia nie będą działać jako ich obejścia weryfikacji przez hello niezależnego fragmentu mapy. |
| MyContext(DbCompiledModel) |ElasticScaleContext (ShardMap, TKey, model DbCompiledModel) |DbContext (DbConnection, model DbCompiledModel, wartość logiczna) |Witaj połączenia zostaną utworzone dla hello podany klucz mapy i dzielenia na fragmenty niezależnego fragmentu z modelem hello podane. Hello skompilowanego modelu zostaną przekazane na toohello c'tor podstawowej. |
| MyContext (DbConnection, wartość logiczna) |ElasticScaleContext (ShardMap, TKey, wartość logiczna) |DbContext (DbConnection, wartość logiczna) |połączenie Hello wymaga toobe wywnioskować na podstawie mapy niezależnego fragmentu hello i hello klucza. Nie można podać jako dane wejściowe, (chyba że te dane wejściowe korzystał już z mapy niezależnego fragmentu hello i klucz hello). wartość logiczna Hello zostaną przekazane. |
| MyContext (ciąg, model DbCompiledModel) |ElasticScaleContext (ShardMap, TKey, model DbCompiledModel) |DbContext (DbConnection, model DbCompiledModel, wartość logiczna) |połączenie Hello wymaga toobe wywnioskować na podstawie mapy niezależnego fragmentu hello i hello klucza. Nie można podać jako dane wejściowe, (chyba że te dane wejściowe używał mapy niezależnego fragmentu hello i klucz hello). model skompilowanych Hello zostaną przekazane. |
| MyContext (ObjectContext, wartość logiczna) |ElasticScaleContext (ShardMap TKey, ObjectContext, wartość logiczna) |DbContext (ObjectContext, wartość logiczna) |Nowy Konstruktor Hello musi tooensure, który dowolnego połączenia, powitalne ObjectContext przekazany jako dane wejściowe jest połączenie przekierowane tooa zarządza elastycznego skalowania. Szczegółowe omówienie ObjectContexts wykracza poza zakres tego dokumentu hello. |
| MyContext (DbConnection, model DbCompiledModel, wartość logiczna) |ElasticScaleContext (ShardMap TKey, model DbCompiledModel, wartość logiczna) |DbContext (DbConnection, model DbCompiledModel, wartość logiczna); |połączenie Hello wymaga toobe wywnioskować na podstawie mapy niezależnego fragmentu hello i hello klucza. Witaj połączenia nie można podać jako danych wejściowych (chyba że te dane wejściowe korzystał już z mapy niezależnego fragmentu hello i klucz hello). Model i wartość logiczną są przekazywane toohello konstruktora klasy podstawowej. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Identyfikator niezależnego fragmentu wdrożenia schematu za pomocą migracji EF
Zarządzanie automatyczne schematu jest udogodnienie podał hello Entity Framework. W kontekście hello aplikacji przy użyciu narzędzi elastycznej bazy danych chcemy tooretain tego odłamków możliwości tooautomatically udostępniania hello schematu toonewly utworzone po dodaniu aplikacji podzielonej toohello baz danych. pierwotnym zastosowaniem Hello jest pojemność tooincrease podzielonej aplikacji przy użyciu EF na powitania warstwy danych. Zależne EF jego możliwości zarządzania schematu powoduje zmniejszenie nakładu pracy administracyjnej bazy danych hello z aplikacją podzielonej EF w oparciu. 

Wdrożenia schematu za pomocą migracji EF najlepiej **bez otwierania połączenia**. Jest to z kolei toohello scenariusz routingu zależnych danych zależy od połączenia hello otworzyć udostępniane przez interfejs API klienta elastycznej bazy danych hello. Inna różnica polega na wymaganie spójności hello: podczas pożądane tooensure spójności dla wszystkich danych zależne od routingu tooprotect połączenia przed manipulowania mapy równoczesnych niezależnego fragmentu, nie jest problemem z początkowej schematu wdrożenia tooa nowej bazy danych mający jeszcze nie został zarejestrowany w mapie niezależnego fragmentu hello i nie zostały jeszcze przydzielona toohold shardlets. Firma Microsoft może w związku z tym polegać na połączenia zwykłej bazy danych dla tego scenariusze jako min. zależne od toodata routingu.  

Prowadzi to podejście tooan gdzie wdrożenia schematu za pomocą migracji EF jest ściśle powiązane ze rejestracji hello hello nowej bazy danych jako niezależnego fragmentu w aplikacji hello niezależnego fragmentu mapy. To opiera się na powitania następujące wymagania wstępne: 

* Witaj bazy danych już istnieje. 
* Witaj baza danych jest pusta — posiada nie użytkowników schematu i danych użytkownika.
* bazy danych Hello jeszcze nie są dostępne za pośrednictwem interfejsów API klienta elastycznej bazy danych hello zależne od danych routingu. 

Z tych wymagań wstępnych w miejscu, możemy utworzyć zwykły bez otwartego **SqlConnection** tookick poza EF migracji wdrożenia schematu. powitania po przykładowy kod przedstawia tej metody. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


W tym przykładzie pokazano metodę hello **RegisterNewShard** czy rejestrów hello niezależnego fragmentu w mapie niezależnego fragmentu hello, wdraża hello schematu za pomocą migracji EF i przechowuje mapowanie niezależnych klucza toohello dzielenia na fragmenty. Zależy od konstruktora hello **DbContext** podklasy (**ElasticScaleContext** w przykładowym hello) pobierającej parametrów połączenia SQL jako dane wejściowe. Kod Hello tego konstruktora jest proste, jako powitania po przykładzie: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Co najmniej jedna może być używana wersja hello konstruktora hello odziedziczona z klasy podstawowej hello. Ale hello tooensure potrzeb kodu, który hello domyślne inicjator dla EF jest używany podczas nawiązywania połączenia. Dlatego hello krótkich przekierowania do metody statycznej hello przed wywołaniem do konstruktora klasy podstawowej hello z hello parametry połączenia. Zauważ, że hello rejestracji odłamków należy uruchomić w aplikacji innej domeny lub proces tooensure, które nie powodują konfliktu ustawień inicjatora hello EF. 

## <a name="limitations"></a>Ograniczenia
Witaj metod opisanych w tym dokumencie pociąga za sobą kilka ograniczeń: 

* EF aplikacji, które używają **LocalDb** najpierw toomigrate tooa zwykłej bazy danych programu SQL Server przed rozpoczęciem korzystania z biblioteki klienta elastycznej bazy danych. Skalowania aplikacji za pośrednictwem dzielenia na fragmenty o elastycznego skalowania nie jest możliwe za pomocą **LocalDb**. Należy pamiętać, że programowanie można nadal używać **LocalDb**. 
* Każda aplikacja toohello zmiany, która oznacza zmiany schematu bazy danych należy toogo za pomocą migracji EF na wszystkich fragmentów. Witaj przykładowy kod dla tego dokumentu nie pokazują, jak toodo to. Należy rozważyć użycie Update-Database z tooiterate parametru ConnectionString za pośrednictwem wszystkich odłamków; Wyodrębnij hello T-SQL skryptu lub dla hello oczekujących migracji Update-Database z użyciem hello - opcja skryptu i zastosować odłamków tooyour skryptu hello T-SQL.  
* Biorąc pod uwagę na żądanie, zakłada się, że wszystkie jego przetwarzanie bazy danych znajduje się w obrębie jednego niezależnego fragmentu określonej za pomocą hello dzielenia na fragmenty klucza udostępnionego przez hello żądania. Jednak to założenie nie zawsze ma wartość true. Na przykład, jeśli nie jest możliwe toomake dostępne klucz dzielenia na fragmenty. tooaddress tego hello biblioteki klienta zawiera hello **MultiShardQuery** klasa implementująca abstrakcji połączenia, na potrzeby zapytań przez kilka fragmentów. Learning toouse hello **MultiShardQuery** w połączeniu z EF wykracza poza zakres tego dokumentu hello

## <a name="conclusion"></a>Podsumowanie
Hello kroków opisanych w tym dokumencie, EF aplikacje mogą używać biblioteki hello elastycznej bazy danych klienta możliwości danych zależnych routingu w ramach refaktoryzacji elementu konstruktorów hello **DbContext** podklasy używane w hello EF aplikacja. Wymagane zmiany hello tego ograniczenia toothose miejsc, gdzie **DbContext** klasy już istnieje. Ponadto aplikacje EF można nadal toobenefit z wdrażania automatycznego schematu łącząc hello kroki, które wywołują hello niezbędne EF migracji z rejestracją hello nowych fragmentów i mapowania hello niezależnego fragmentu mapy. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
