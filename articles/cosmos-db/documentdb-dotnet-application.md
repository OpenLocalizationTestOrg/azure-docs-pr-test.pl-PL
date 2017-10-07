---
title: "Samouczek platformy ASP.NET MVC dla usługi Azure Cosmos DB: opracowywanie aplikacji internetowych | Microsoft Docs"
description: "Samouczek platformy ASP.NET MVC toocreate aplikacji sieci web MVC przy użyciu bazy danych Azure rozwiązania Cosmos. Zapiszesz dane w postaci kodu JSON i uzyskasz do nich dostęp za pomocą aplikacji listy rzeczy do zrobienia hostowanej w usłudze Azure Websites — szczegółowy samouczek dla platformy ASP.NET MVC."
keywords: samouczek asp.net mvc, programowanie aplikacji sieci web, aplikacja sieci web mvc, samouczek krok po kroku asp.net mvc
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>Samouczek platformy ASP.NET MVC: Opracowywanie aplikacji internetowych za pomocą usługi Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight sposób mogą efektywnie korzystać z bazy danych Azure rozwiązania Cosmos toostore i wykonywać zapytania dokumentów JSON, w tym artykule przedstawiono end-to-end Przewodnik jak toobuild aplikacji todo, przy użyciu bazy danych Azure rozwiązania Cosmos. Witaj zadania będą przechowywane jako dokumenty JSON w usłudze Azure DB rozwiązania Cosmos.

![Zrzut ekranu: Lista czynności do wykonania hello aplikacji sieci web MVC utworzone przez tego samouczka — samouczek platformy Asp.net MVC ASP krok po kroku](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Ten przewodnik przedstawia, jak toouse hello Azure DB rozwiązania Cosmos usługi toostore i danymi dostępu z aplikacji sieci web platformy ASP.NET MVC hostowanej na platformie Azure. Jeśli szukasz samouczka, który koncentruje się tylko dla bazy danych rozwiązania Cosmos Azure, a nie hello ASP.NET MVC, zobacz [tworzenie aplikacji konsoli Azure rozwiązania Cosmos DB C#](documentdb-get-started.md).

> [!TIP]
> Ten samouczek zakłada, że masz już pewne doświadczenie w korzystaniu z platformy ASP.NET MVC i usługi Azure Websites. W przypadku nowych tooASP.NET lub hello [wstępnie wymaganych narzędzi](#_Toc395637760), zalecamy pobranie hello kompletnego przykładowego projektu z [GitHub] [ GitHub] i instrukcjami hello w w przykładzie. Po jego skompilowaniu, możesz przejrzeć ten artykuł wglądu toogain na powitania kod w kontekście hello hello projektu.
> 
> 

## <a name="_Toc395637760"></a>Wymagania wstępne dotyczące tego samouczka bazy danych
Przed rozpoczęciem powitalne instrukcje w tym artykule, należy upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 

    LUB

    Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK dla platformy .NET dla programu Visual Studio 2017 r, dostępne za pośrednictwem hello Instalator programu Visual Studio.

Wszystkie zrzuty ekranu hello w tym artykule wykonano za pomocą programu Microsoft Visual Studio Community 2017. Jeśli system jest skonfigurowany za pomocą innej wersji jest możliwe, że Twoje ekrany i opcje nie będą całkiem zgodne, lecz jeśli spełniasz hello powyżej wymagań wstępnych to rozwiązanie powinno działać.

## <a name="_Toc395637761"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB
Zacznijmy od utworzenia konta usługi Azure Cosmos DB. Jeśli już masz konto SQL (DocumentDB) dla bazy danych Azure rozwiązania Cosmos lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[Tworzenie nowej aplikacji ASP.NET MVC](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Teraz przejdziemy przez jak toocreate nowej aplikacji ASP.NET MVC z hello podstaw. 

## <a name="_Toc395637762"></a>Krok 2. Tworzenie nowej aplikacji platformy ASP.NET MVC

1. W programie Visual Studio na powitania **pliku** menu punktu zbyt**nowy**, a następnie kliknij przycisk **projektu**. Witaj **nowy projekt** zostanie wyświetlone okno dialogowe.

2. W hello **typy projektów** okienku rozwiń **szablony**, **Visual C#**, **sieci Web**, a następnie wybierz **aplikacji sieci Web ASP.NET** .

      ![Zrzut ekranu przedstawiający okno dialogowe Nowy projekt hello z wyróżnionym typem projektu aplikacja sieci Web ASP.NET hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. W hello **nazwa** okno, nazwa typu hello hello projektu. W tym samouczku używana hello nazwa "todo". Jeśli wybierzesz toouse coś innego niż ten, wszędzie tam, gdzie wspomniana przestrzeń nazw todo hello, należy tooadjust hello podany kod przykłady toouse nazwy aplikacji. 
4. Kliknij przycisk **Przeglądaj** toonavigate toohello folderu zawierającego czy toocreate hello projektu, takich jak, a następnie kliknij przycisk **OK**.
   
      Witaj **nowej aplikacji sieci Web ASP.NET** zostanie wyświetlone okno dialogowe.
   
    ![Zrzut ekranu przedstawiający okno dialogowe hello nowej aplikacji sieci Web platformy ASP.NET z wyróżnionym szablonem aplikacji MVC hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Wybierz w okienku szablonów hello **MVC**.

6. Kliknij przycisk **OK** program Visual Studio przygotowanie wokół szkieletów hello pustego szablonu platformy ASP.NET MVC. 

          
7. Po zakończeniu programu Visual Studio, tworzenie aplikacji MVC umożliwiającego hello masz pustą aplikację ASP.NET, który można uruchomić lokalnie.
   
    Pominiemy projektu hello uruchomionych lokalnie, ponieważ wiem, zablokowaliśmy wszystkich widziany powitania "Hello World" platformy ASP.NET aplikacji. Przejdźmy proste tooadding bazy danych Azure rozwiązania Cosmos toothis projektu i tworzenia aplikacji.

## <a name="_Toc395637767"></a>Krok 3: Dodaj projekt aplikacji sieci web MVC tooyour bazy danych Azure rozwiązania Cosmos
Teraz, gdy mamy większość hello ASP.NET MVC potrzebnych dla tego rozwiązania, załóż toohello rzeczywistego celu tego samouczka, Dodawanie aplikacji sieci web MVC tooour bazy danych Azure rozwiązania Cosmos.

1. Witaj zestawu .NET SDK usługi Azure rozwiązania Cosmos DB zostaje spakowany i dystrybuowanych jako pakietu NuGet. tooget hello pakietu NuGet w programie Visual Studio, użyj Menedżera pakietów NuGet hello w programie Visual Studio, klikając prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie klikając polecenie **Zarządzaj pakietami NuGet**.
   
    ![Zrzut ekranu przedstawiający powitania kliknij prawym przyciskiem myszy opcje hello projektu aplikacji sieci web w Eksploratorze rozwiązań z Zarządzaj pakietami NuGet wyróżnione.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Witaj **Zarządzaj pakietami NuGet** zostanie wyświetlone okno dialogowe.
2. W hello NuGet **Przeglądaj** wpisz ***Azure DocumentDB***. (nazwa pakietu hello nie został zaktualizowany tooAzure DB rozwiązania Cosmos.)
   
    Wyniki hello zainstalować hello **Microsoft.Azure.DocumentDB przez firmę Microsoft** pakietu. To pobierze i zainstaluje hello Azure DB rozwiązania Cosmos pakietu, a także wszystkie zależności, takich jak Newtonsoft.Json. Kliknij przycisk **OK** w hello **Podgląd** okno i **akceptuję** w hello **akceptacji licencji** okna toocomplete hello instalacji.
   
    ![Zrzut ekranu okna Zarządzanie pakietami NuGet hello z hello Microsoft Azure DocumentDB wyróżnioną pozycją Biblioteka kliencka](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      Możesz też użyć hello pakietu hello tooinstall Konsola Menedżera pakietów. toodo tak na powitania **narzędzia** menu, kliknij przycisk **Menedżera pakietów NuGet**, a następnie kliknij przycisk **Konsola Menedżera pakietów**. W wierszu hello wpisz następujące hello.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Po zainstalowaniu pakietu hello rozwiązania Visual Studio powinno przypominać następujące hello z dwoma odwołaniami: Microsoft.Azure.Documents.Client i Newtonsoft.Json.
   
    ![Zrzut ekranu hello dwa odwołania dodane projektu danych JSON toohello w Eksploratorze rozwiązań](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Krok 4: Konfigurowanie hello aplikacji ASP.NET MVC
Teraz Dodajmy hello modele, widoki i kontrolery toothis aplikacji MVC:

* [Dodaj model](#_Toc395637764).
* [Dodaj kontroler](#_Toc395637765).
* [Dodaj widoki](#_Toc395637766).

### <a name="_Toc395637764"></a>Dodawanie modelu danych JSON
Zacznijmy od utworzenia hello **M** w nazwie wzorca MVC, hello modelu. 

1. W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **modele** folderu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.
   
      Witaj **Dodaj nowy element** zostanie wyświetlone okno dialogowe.
2. Nadaj nowej klasie nazwę **Item.cs** i kliknij polecenie **Dodaj**. 
3. W nowym **Item.cs** plików, Dodaj następujące powitania po hello ostatnio *za pomocą instrukcji*.
   
        using Newtonsoft.Json;
4. Teraz zastąp ten kod 
   
        public class Item
        {
        }
   
    z hello następującego kodu.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Wszystkie dane w usłudze Azure DB rozwiązania Cosmos jest przekazywana hello przewodowy i zapisane w formacie JSON. toocontrol hello sposób obiekty są serializacji/deserializacji przez JSON.NET, możesz użyć hello **JsonProperty** jak przedstawiono w hello **elementu** klasy właśnie utworzyliśmy. Nie musisz **ma** toodo to ale mają tooensure, że właściwości są zgodne z konwencji nazewnictwa hello JSON (camelcase). 
   
    Mogą kontrolować nie tylko możesz hello format nazwy właściwości hello trafia do postaci JSON, ale należy całkowicie zmienić nazwy właściwości platformy .NET, tak jak to zrobiono z hello **opis** właściwości. 

### <a name="_Toc395637765"></a>Dodawanie kontrolera
Która zajmuje się hello **M**, teraz Utwórzmy hello **C** w nazwie wzorca MVC, klasę kontrolera.

1. W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **kontrolerów** folderu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.
   
    Witaj **Dodawanie szkieletu** zostanie wyświetlone okno dialogowe.
2. Wybierz pozycję **Kontroler MVC 5 — pusty**, a następnie kliknij polecenie **Dodaj**.
   
    ![Zrzut ekranu przedstawiający okno dialogowe Dodawanie szkieletu hello z hello kontroler MVC 5 — pusty wyróżnioną opcją](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Nadaj nowemu kontrolerowi nazwę **ItemController**.
   
    ![Zrzut ekranu: okno dialogowe Dodaj kontroler hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Po utworzeniu pliku hello rozwiązania Visual Studio powinno przypominać następujące hello z nowym plikiem ItemController.cs hello w **Eksploratora rozwiązań**. Witaj nowy plik Item.cs utworzony wcześniej jest także pokazany.
   
    ![Zrzut ekranu przedstawiający hello Eksploratora rozwiązań z hello nowym plikiem ItemController.cs i Item.cs rozwiązania Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    Możesz zamknąć plik ItemController.cs, wrócimy tooit później. 

### <a name="_Toc395637766"></a>Dodawanie widoków
Teraz Utwórzmy hello **V** w nazwie wzorca MVC, hello widoków:

* [Dodaj widok indeksu elementów](#AddItemIndexView).
* [Dodaj widok nowego elementu](#AddNewIndexView).
* [Dodaj widok edycji elementu](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Dodawanie widoku indeksu elementów
1. W **Eksploratora rozwiązań**, rozwiń węzeł hello **widoków** folder, kliknij prawym przyciskiem myszy hello pusty **elementu** folderu, który Visual Studio utworzone po dodaniu hello  **ItemController** , kliknij polecenie **Dodaj**, a następnie kliknij przycisk **widoku**.
   
    ![Zrzut ekranu przedstawiający Eksploratora rozwiązań przedstawiający folder Item hello utworzony za pomocą polecenia Dodaj widok hello wyróżnione Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. W hello **Dodaj widok** okna dialogowego pozycję hello następujące:
   
   * W hello **nazwy widoku** wpisz ***indeksu***.
   * W hello **szablonu** wybierz opcję ***listy***.
   * W hello **klasa modelu** wybierz opcję ***elementu (todo. Modele)***.
   * W polu strony układu hello wpisz ***~/Views/Shared/_Layout.cshtml***.
     
   ![Okno dialogowe dodawania widoku zrzut ekranu przedstawiający hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Gdy wszystkie te wartości są ustawione, kliknij przycisk **Dodaj**. Program Visual Studio utworzy nowy widok szablonu. Po zakończeniu otworzy utworzony plik cshtml hello. Możemy zamknąć ten plik w programie Visual Studio, ponieważ wrócimy tooit później.

#### <a name="AddNewIndexView"></a>Dodawanie widoku nowego elementu
Podobne toohow utworzyliśmy **indeks elementu** widoku teraz utworzymy nowy widok na potrzeby tworzenia nowych **elementów**.

1. W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **elementu** ponownie, kliknij folder **Dodaj**, a następnie kliknij przycisk **widoku**.
2. W hello **Dodaj widok** okna dialogowego pozycję hello następujące:
   
   * W hello **nazwy widoku** wpisz ***Utwórz***.
   * W hello **szablonu** wybierz opcję ***Utwórz***.
   * W hello **klasa modelu** wybierz opcję ***elementu (todo. Modele)***.
   * W polu strony układu hello wpisz ***~/Views/Shared/_Layout.cshtml***.
   * Kliknij pozycję **Dodaj**.
   
#### <a name="_Toc395888515"></a>Dodawanie widoku edycji elementu
I w końcu dodaj ostatni widok edycji **elementu** w hello tak samo jak wcześniej.

1. W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **elementu** ponownie, kliknij folder **Dodaj**, a następnie kliknij przycisk **widoku**.
2. W hello **Dodaj widok** okna dialogowego pozycję hello następujące:
   
   * W hello **nazwy widoku** wpisz ***Edytuj***.
   * W hello **szablonu** wybierz opcję ***Edytuj***.
   * W hello **klasa modelu** wybierz opcję ***elementu (todo. Modele)***.
   * W polu strony układu hello wpisz ***~/Views/Shared/_Layout.cshtml***.
   * Kliknij pozycję **Dodaj**.

Po zakończeniu zamknij wszystkie dokumenty cshtml hello w programie Visual Studio, wrócimy toothese widoków później.

## <a name="_Toc395637769"></a>Krok 5. Podłączanie usługi Azure Cosmos DB
Teraz, gdy jest poświęcony na obsługę hello standard MVC rzeczy, możemy zacząć tooadding hello kodu dla bazy danych Azure rozwiązania Cosmos. 

W tej sekcji dodamy kod toohandle hello poniżej:

* [Wyświetlanie niezakończonych elementów](#_Toc395637770).
* [Dodawanie elementów](#_Toc395637771).
* [Edytowanie elementów](#_Toc395637772).

### <a name="_Toc395637770"></a>Wyświetlanie niezakończonych elementów w aplikacji sieci Web MVC
Witaj pierwszy toodo operacją tutaj jest dodać klasę, która zawiera wszystkie hello logiki tooconnect tooand Użyj bazy danych Azure rozwiązania Cosmos. W ramach tego samouczka umieściliśmy całą tę logikę w klasie repozytorium tooa o nazwie DocumentDBRepository. 

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy na powitania projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**. Nazwa nowej klasy hello **DocumentDBRepository** i kliknij przycisk **Dodaj**.
2. W nowo utworzony hello **DocumentDBRepository** klasy i dodaj następujące hello *instrukcje using* powyżej hello *przestrzeni nazw* deklaracji
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Teraz zastąp ten kod 
   
        public class DocumentDBRepository
        {
        }
   
    z hello następującego kodu.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Firma Microsoft czytanej zawartości niektórych wartości z konfiguracji, otwórz hello **Web.config** pliku aplikacji i dodaj następujące wiersze w obszarze hello hello `<AppSettings>` sekcji.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Teraz zaktualizuj wartości hello *punktu końcowego* i *authKey* za pomocą bloku klucze hello hello portalu Azure. Użyj hello **URI** z hello bloku klucze jako wartości hello hello ustawienia punktu końcowego i użyj hello **klucza podstawowego**, lub **klucza POMOCNICZEGO** z hello bloku klucze jako wartości hello hello Ustawienia authKey.

    Czy zajmuje opieki podłączyliśmy repozytorium Azure DB rozwiązania Cosmos hello, teraz załóżmy dodać logikę aplikacji.

1. Witaj po pierwsze chcemy toobe stanie toodo z aplikację listy zadań do wykonania jest toodisplay hello niezakończonych elementów.  Skopiuj i Wklej hello następującego fragmentu kodu w obrębie hello **DocumentDBRepository** klasy.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Otwórz hello **ItemController** możemy dodany wcześniej i dodaj następujące hello *instrukcje using* powyżej hello deklaracji przestrzeni nazw.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Jeśli projekt nie ma nazwy "todo", następnie należy tooupdate za pomocą "todo. Modele"; Nazwa hello tooreflect Twojego projektu.
   
    Teraz zastąp ten kod
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    z hello następującego kodu.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Otwórz **Global.asax.cs** i Dodaj powitania po wierszu toohello **Application_Start** — metoda 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

W tym momencie rozwiązanie powinno być możliwe toobuild bez żadnych błędów.

W przypadku uruchomienia aplikacji hello teraz przejdzie toohello **HomeController** i hello **indeksu** tego kontrolera. Jest to hello domyślne zachowanie dla projektu szablonu MVC hello wybranych na początku hello, ale nie! Zmieńmy routing na tym tooalter aplikacji MVC to zachowanie hello.

Otwórz ***aplikacji\_Start\RouteConfig.cs*** i odszukaj wiersz hello począwszy od "wartości domyślne:" i zmień je po hello tooresemble.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

To teraz poinformuje platformę ASP.NET MVC, że jeśli nie określono wartości w toocontrol adres URL hello hello zachowania routingu, to zamiast elementu **Home**, użyj **elementu** jako kontroler hello i użytkownika **indeksu** jako hello widoku.

Teraz po uruchomieniu aplikacji hello zostanie wywołany z **ItemController** który wywoła w klasie repozytorium toohello i użyj wszystkich toohello niezakończonych elementów hello tooreturn metody GetItems hello **widoków** \\ **Elementu**\\**indeksu** widoku. 

Jeśli skompilujesz i uruchomisz projekt teraz, zobaczysz stronę podobną do następującej.    

![Zrzut ekranu przedstawiający hello todo listy aplikacji sieci web utworzone przez tego samouczka bazy danych](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Dodawanie elementów
Umieśćmy kilka elementów w naszej bazie danych, dzięki czemu będziemy mogli zobaczyć coś więcej niż pustą siatkę toolook w.

Dodajmy trochę kodu zbyt DBRepository rozwiązania Cosmos Azure i ItemController toopersist hello rekord w usłudze Azure DB rozwiązania Cosmos.

1. Dodaj następujące metody tooyour hello **DocumentDBRepository** klasy.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Ta metoda po prostu przyjmuje przekazany tooit obiekt i utrwala go w usłudze Azure DB rozwiązania Cosmos.
2. Otwórz plik ItemController.cs hello i Dodaj hello następującego fragmentu kodu w klasie hello. Jest to, jak platformy ASP.NET MVC wie, jakiego toodo dla hello **Utwórz** akcji. W takim przypadku tylko renderowanie Witaj skojarzony widok Create.cshtml utworzony wcześniej.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Teraz potrzebujemy kodu w tym kontrolerze, który będzie akceptować przesyłanie hello z hello **Utwórz** widoku.
3. Dodaj hello kolejny blok kodu toohello klasy ItemController.cs, który poinformuje platformę ASP.NET MVC, jakie toodo z formularzem POST dla tego kontrolera.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Ten kod wywołuje w toohello DocumentDBRepository i używa hello CreateItemAsync metody toopersist hello nowe todo elementu toohello bazy danych. 
   
    **Uwaga dotycząca zabezpieczeń**: hello **ValidateAntiForgeryToken** atrybut jest używany w tym miejscu toohelp ochrony aplikacji przed fałszerstwie żądania międzywitrynowego. Brak tooit więcej niż tylko dodanie tego atrybutu, widoków musi toowork z ten token zabezpieczający przed sfałszowaniem. Aby uzyskać więcej informacji na temat hello i przykłady sposobu tooimplement to poprawnie, zobacz [zapobieganie fałszowaniu żądań Cross-Site][Preventing Cross-Site Request Forgery]. Witaj kod źródłowy dostępny w [GitHub] [ GitHub] ma pełnej implementacji hello w miejscu.
   
    **Uwaga dotycząca zabezpieczeń**: korzystamy również hello **powiązać** atrybutu toohelp parametru metody hello ochronę przed zbyt księgowej ataków. Aby poznać więcej szczegółów, zobacz [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] (Podstawowe operacje CRUD na platformie ASP.NET MVC).

Zakończenie hello kod wymagany tooadd nowe elementy tooour bazy danych.

### <a name="_Toc395637772"></a>Edytowanie elementów
Brak ostatnia rzecz do nas toodo i jest tooadd hello możliwości tooedit **elementów** hello bazy danych i toomark je jako zakończenie. Witaj widok edycji został już dodany projekt toohello, dlatego potrzebujemy tooadd niektóre kod tooour kontrolera i toohello **DocumentDBRepository** ponownie.

1. Dodaj następujące toohello hello **DocumentDBRepository** klasy.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    Witaj pierwsza z tych metod **GetItem** pobiera element z rozwiązania Cosmos bazy danych Azure, który jest przekazywany wstecz toohello **ItemController** , a następnie na toohello **Edytuj** widoku.
   
    Witaj sekundę metody hello właśnie dodaliśmy, zastępuje hello **dokumentu** w usłudze Azure DB rozwiązania Cosmos z wersją hello hello **dokumentu** przekazany z hello **ItemController**.
2. Dodaj następujące toohello hello **ItemController** klasy.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Witaj pierwszy dojścia metody hello GET protokołu Http, która jest wywoływana po kliknięciu hello na powitania **Edytuj** łącza z hello **indeksu** widoku. Ta metoda pobiera [ **dokumentu** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) z bazy danych usługi Azure rozwiązania Cosmos i przekazuje je toohello **Edytuj** widoku.
   
    Witaj **Edytuj** widoku wykona następnie toohello Http POST **IndexController**. 
   
    Druga metoda Hello dodaliśmy uchwytów przekazywanie hello zaktualizowany obiekt tooAzure DB rozwiązania Cosmos toobe trwale hello bazy danych.

To wszystko, że wszystko, co jest potrzebne toorun naszej aplikacji jest, listy niekompletne **elementów**, Dodaj nowy **elementów**i edytować **elementów**.

## <a name="_Toc395637773"></a>Krok 6: Uruchamianie aplikacji hello lokalnie
Aplikacja hello tootest na komputerze lokalnym hello następujące:

1. Naciśnij klawisz F5 w programie Visual Studio toobuild hello aplikacji w trybie debugowania. Powinna tworzenia aplikacji hello i przeglądarkę ze strony hello pustą siatką, którą widzieliśmy wcześniej:
   
    ![Zrzut ekranu przedstawiający hello todo listy aplikacji sieci web utworzone przez tego samouczka bazy danych](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Kliknij przycisk hello **Utwórz nowy** link i Dodaj wartości toohello **nazwa** i **opis** pola. Pozostaw hello **Ukończono** hello w przeciwnym razie nowy niezaznaczone pole wyboru **elementu** zostanie dodany jako zakończony i nie będą wyświetlane na liście początkowej hello.
   
    ![Zrzut ekranu przedstawiający hello Utwórz widok](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Kliknij przycisk **Utwórz** i są przekierowane wstecz toohello **indeksu** widoku i **elementu** jest widoczna na liście hello.
   
    ![Zrzut ekranu przedstawiający hello widoku indeksu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Możesz wolnego tooadd kilka kolejnych **elementów** tooyour lista czynności do wykonania.
    
4. Kliknij przycisk **Edytuj** dalej tooan **elementu** na liście hello, są pobierane toohello **Edytuj** widok, w którym można zaktualizować dowolną właściwość obiektu, w tym hello  **Ukończono** flagi. Po zaznaczeniu hello **Complete** Flaga, a następnie kliknij przycisk **zapisać**, hello **elementu** zostanie usunięty z listy niezakończonych zadań hello.
   
    ![Zrzut ekranu przedstawiający widok indeksu z zaznaczonym polem Completed hello hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Po przetestowaniu aplikacji hello, naciśnij klawisze Ctrl + F5 toostop debugowania aplikacji hello. Wszystko jest gotowe toodeploy!

## <a name="_Toc395637774"></a>Krok 7: Wdrażanie tooAzure aplikacji hello usługi aplikacji 
Teraz, gdy masz hello kompletna aplikacja działa poprawnie z bazy danych Azure rozwiązania Cosmos zamierzamy toodeploy tego tooAzure aplikacji sieci web usługi aplikacji.  

1. Kliknij prawym przyciskiem myszy na projekt hello w jest tej aplikacji wszystkie potrzebne toodo toopublish **Eksploratora rozwiązań** i kliknij przycisk **publikowania**.
   
    ![Zrzut ekranu przedstawiający hello opcji Publikuj w Eksploratorze rozwiązań](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. W hello **publikowania** okno dialogowe, kliknij przycisk **Microsoft Azure App Service**, a następnie wybierz pozycję **Utwórz nowy** toocreate usługę aplikacji profilu, lub kliknij przycisk **wybierz Istniejące** toouse istniejącego profilu.

    ![Opublikuj okno dialogowe w programie Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Jeśli masz istniejący profil usługi Azure App Service, wprowadź nazwę subskrypcji. Użyj hello **widoku** filtrować toosort przez grupę zasobów lub typ zasobu, a następnie wybierz usłudze Azure App Service. 
   
    ![Usługi aplikacji — okno dialogowe w programie Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. Kliknij toocreate nowy profil usługi Azure App Service, **Utwórz nowy** w hello **publikowania** okno dialogowe. W hello **Tworzenie usługi App Service** okna dialogowego, wprowadź nazwę aplikacji sieci Web i odpowiednie subskrypcji, grupy zasobów i plan usługi aplikacji, a następnie kliknij przycisk **Utwórz**.

    ![Tworzenie aplikacji usługi — okno dialogowe w programie Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

W ciągu kilku sekund program Visual Studio zakończy publikowanie aplikacji sieci web i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!



## <a name="_Toc395637775"></a>Następne kroki
Gratulacje! Po prostu wbudowany Twojego pierwszego ASP.NET MVC aplikacji sieci web przy użyciu bazy danych Azure rozwiązania Cosmos i opublikować ją tooAzure. Witaj kodu źródłowego dla pełnej aplikacji hello, w tym hello szczegółów i usuwania funkcji, które nie zostały uwzględnione w tym samouczku można pobrać lub sklonować z [GitHub][GitHub]. Więc jeśli chcesz dodać, aplikacja tooyour, wystarczy pobrać kod hello i dodać toothis aplikacji.

tooadd dodatkowe funkcje tooyour aplikacji, przejrzyj hello interfejsami API dostępnymi w hello [biblioteki .NET DB rozwiązania Cosmos Azure](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) i uważasz toohello wolnego toocontribute biblioteki .NET DB rozwiązania Cosmos Azure na [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
