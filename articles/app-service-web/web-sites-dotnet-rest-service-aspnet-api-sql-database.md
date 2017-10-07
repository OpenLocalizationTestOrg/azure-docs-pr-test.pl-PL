---
title: aaaCreate interfejsu API REST na platformie Azure z platformy ASP.NET i bazy danych SQL | Dokumentacja firmy Microsoft
description: "Samouczek który jest przedstawienie sposobu toodeploy aplikacji, która używa hello tooan ASP.NET Web API aplikacji sieci web platformy Azure przy użyciu programu Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Tworzenie usługi REST przy użyciu interfejsu API sieci Web platformy ASP.NET i bazy danych SQL w usłudze Azure App Service
Ten samouczek pokazuje, jak toodeploy platformy ASP.NET sieci web aplikacji tooan [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) za pomocą kreatora Publikowanie w sieci Web hello w Visual Studio 2013 lub Visual Studio 2013 Community Edition. 

Możesz otworzyć bezpłatne konto platformy Azure, a jeśli nie masz jeszcze programu Visual Studio 2013, hello SDK automatycznie instaluje program Visual Studio 2013 for Web Express. Dlatego możesz rozpocząć tworzenie dla platformy Azure i całkowicie bezpłatne.

Ten samouczek zakłada, że nie masz wcześniejszego doświadczenia korzysta z platformy Azure. Na wykonanie kroków tego samouczka, będziesz mieć aplikację sieci web proste górę i w chmurze hello.

Dowiesz się:

* Jak tooenable komputer dla rozwoju platformy Azure, instalując hello Azure SDK.
* Jak toocreate programu Visual Studio ASP.NET MVC 5 projektu, a następnie opublikuj ją tooan aplikacji Azure.
* W jaki sposób toouse hello tooenable interfejsu API sieci Web platformy ASP.NET wywołuje interfejs API Restful.
* Jak toouse SQL bazy danych toostore danych na platformie Azure.
* Jak aplikacja toopublish aktualizuje tooAzure.

Będzie tworzenia aplikacji sieci web proste listy kontaktów, która jest oparty na programie ASP.NET MVC 5 i używa hello ADO.NET Entity Framework dla dostępu do bazy danych. Witaj następującej ilustracji przedstawiono hello ukończone aplikacji:

![Zrzut ekranu przedstawiający witryny sieci web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Utwórz projekt hello
1. Uruchom program Visual Studio 2013.
2. Z hello **pliku** kliknij menu **nowy projekt**.
3. W hello **nowy projekt** okna dialogowego rozwiń **Visual C#** i wybierz **Web** , a następnie wybierz **aplikacji sieci Web ASP.NET**. Nadaj nazwę aplikacji hello **ContactManager** i kliknij przycisk **OK**.
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. W hello **nowy projekt ASP.NET** okno dialogowe, wybierz opcję hello **MVC** szablonu, sprawdź **interfejsu API sieci Web** , a następnie kliknij przycisk **Zmień uwierzytelnianie**.
5. W hello **Zmień uwierzytelnianie** okno dialogowe, kliknij przycisk **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.
   
    ![Bez uwierzytelniania](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    Witaj przykładowej aplikacji, które tworzysz, nie będziesz mieć funkcji, które wymagają toolog użytkowników w. Aby uzyskać informacje na temat tooimplement funkcji uwierzytelniania i autoryzacji, zobacz hello [następne kroki](#nextsteps) sekcji na końcu hello tego samouczka. 
6. W hello **nowy projekt ASP.NET** okno dialogowe, upewnij się, że hello **hosta w chmurze hello** jest zaznaczony, a następnie kliknij przycisk **OK**.

Jeśli tooAzure nie zostały wcześniej zalogowany, będzie zostanie wyświetlony monit o toosign w.

1. Kreator konfiguracji Hello sugeruje unikatową nazwę, na podstawie *ContactManager* (zobacz poniższy obraz powitania). Wybierz region w pobliżu. Można użyć [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello najniższy centrum danych opóźnienia. 
2. Jeśli nie utworzono serwera bazy danych przed, wybierz **Utwórz nowy serwer**, wprowadź nazwę bazy danych użytkownika i hasło.
   
    ![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Jeśli masz serwer bazy danych, użyj tego toocreate nową bazę danych. Serwery bazy danych są cenne zasobów i zwykle mają toocreate wielu baz danych na powitania tego samego serwera do badania i rozwój zamiast serwera bazy danych dla bazy danych. Upewnij się, że witryn sieci web i bazy danych znajdują się w hello tego samego regionu.

![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Ustaw hello nagłówku i stopce strony
1. W **Eksploratora rozwiązań**, rozwiń węzeł hello *Views\Shared* folder i otwórz hello *_Layout.cshtml* pliku.
   
    ![_Layout.cshtml w Eksploratorze rozwiązań][newapp004]
2. Zamień zawartość hello hello *Views\Shared_Layout.cshtml* pliku z hello następującego kodu:

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

znaczników Hello powyżej nazwy aplikacji hello zmiany z "Moja aplikacja ASP.NET" za "Skontaktuj się z menedżerem" która usuwa hello łącza zbyt**Home**, **o** i **skontaktuj się z**.

### <a name="run-hello-application-locally"></a>Uruchamianie aplikacji hello lokalnie
1. Naciśnij klawisze CTRL + F5 toorun hello aplikacji.
   Strona główna aplikacji Hello pojawia się w hello domyślnej przeglądarki.
    ![Strona główna tooDo listy](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

To wszystko, czego potrzebujesz toodo dla aplikacji hello toocreate teraz wdrożony tooAzure. Będzie później dodać funkcji bazy danych.

## <a name="deploy-hello-application-tooazure"></a>Wdrażanie tooAzure aplikacji hello
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** i wybierz **publikowania** z menu kontekstowego hello.
   
    ![Opublikuj w menu kontekstowego projektu][PublishVSSolution]
   
    Witaj **publikowanie w sieci Web** zostanie otwarty Kreator.
2. Kliknij przycisk **Opublikuj**.

![Karta Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio rozpoczyna proces hello kopiowania hello pliki toohello serwerem Azure. Witaj **dane wyjściowe** okna pokazuje, jakie akcje wdrażania zostały pobrane i raporty pomyślne zakończenie hello wdrożenia.

1. Hello przeglądarka domyślna automatycznie otwiera toohello adres URL witryny hello wdrożone.
   
   utworzoną aplikację Hello jest teraz uruchomiona w chmurze hello.
   
   ![Strona główna listy tooDo działające na platformie Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Dodaj aplikację toohello bazy danych
Następnie będzie zaktualizować hello MVC aplikacji tooadd hello możliwości toodisplay i Aktualizuj kontakty i zapisania danych hello w bazie danych. Aplikacja Hello hello Entity Framework toocreate hello w bazie danych i tooread i aktualizacji danych w bazie danych hello.

### <a name="add-data-model-classes-for-hello-contacts"></a>Dodawanie klasy modelu danych hello kontaktów
Można rozpocząć od tworzenia modelu danych proste w kodzie.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy folder modeli hello, kliknij przycisk **Dodaj**, a następnie **klasy**.
   
    ![Dodaj klasę w menu kontekstowym folderu modeli][adddb001]
2. W hello **Dodaj nowy element** okno dialogowe, hello nazwę nowego pliku klasy *Contact.cs*, a następnie kliknij przycisk **Dodaj**.
   
    ![Dodaj nowy element — okno dialogowe][adddb002]
3. Zastąp zawartość pliku Contacts.cs hello hello hello następującego kodu.
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

Witaj **skontaktuj się z** klasa definiuje hello dane, które będą przechowywane dla każdego kontakt, a także klucz podstawowy, wartość ContactID wymaganej przez hello bazy danych. Więcej informacji o modelach danych można znaleźć w hello [następne kroki](#nextsteps) sekcji na końcu hello tego samouczka.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Tworzenie stron sieci web, umożliwiające toowork użytkowników aplikacji hello kontaktów
Witaj funkcja szkieletów hello ASP.NET MVC można automatycznie generować kod, który wykonuje tworzenia, odczytu, aktualizacji i usuwania (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Dodawanie kontrolera i widoku hello danych
1. W **Eksploratora rozwiązań**, rozwiń folder kontrolery hello.
2. Tworzenie projektu hello **(Ctrl + Shift + B)**. (Należy utworzyć projekt hello przed przy użyciu mechanizmu szkieletów.) 
3. Kliknij prawym przyciskiem myszy folder kontrolery hello, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.
   
    ![Dodawanie kontrolera w menu kontekstowym folderu kontrolerów][addcode001]
4. W hello **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.
   
   ![Dodawanie kontrolera](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Ustaw nazwę kontrolera hello zbyt**HomeController**. Wybierz **skontaktuj się z** jako klasy modelu. Kliknij przycisk hello **nowy kontekst danych** przycisk i zaakceptuj domyślną hello "ContactManager.Models.ContactManagerContext" hello **nowy typ kontekstu danych**. Kliknij pozycję **Dodaj**.

    Okno dialogowe zostanie wyświetlony monit: "plik o nazwie hello HomeController już kończy działanie. Czy chcesz, aby tooreplace go? ". Kliknij przycisk **Yes** (Tak). Firma Microsoft są zastępowanie hello Home kontrolera utworzony za pomocą hello nowy projekt. Używamy hello nowe narzędzia główne kontrolera do naszej listy kontaktów.

    Program Visual Studio tworzy metod kontrolera oraz widoki dla operacji CRUD bazy danych dla **skontaktuj się z** obiektów.

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Włącz migracji, tworzenie hello bazy danych, Dodawanie przykładowych danych i inicjatora danych
następne zadanie Hello jest tooenable hello [migracje Code First](http://curah.microsoft.com/55220) funkcji w kolejności toocreate hello w bazie danych oparte na modelu danych hello został utworzony.

1. W hello **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** , a następnie **Konsola Menedżera pakietów**.
   
    ![Konsola Menedżera pakietów w menu Narzędzia][addcode008]
2. W hello **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie hello:
   
        enable-migrations 
   
    Witaj **enable-migrations,** polecenie tworzy *migracje* folderu i jego umieszcza w tym folderze *Configuration.cs* plik można edytować tooconfigure migracji. 
3. W hello **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie hello:
   
        add-migration Initial
   
    Witaj **początkowego dodać migracji** polecenie generuje klasę o nazwie  **&lt;date_stamp&gt;początkowej** tworzącą hello bazy danych. Witaj pierwszy parametr ( *początkowej* ) jest nazwą hello toocreate dowolnego i używany hello pliku. Widać hello nowe klasy pliki w **Eksploratora rozwiązań**.
   
    W hello **początkowej** klasy, hello **się** metoda tworzy hello tabeli kontaktów i hello **dół** — metoda (używany, gdy tooreturn toohello poprzedniego stanu) porzuca go.
4. Otwórz hello *Migrations\Configuration.cs* pliku. 
5. Dodaj hello następujące obszary nazw. 
   
         using ContactManager.Models;
6. Zastąp hello *inicjatora* metody z hello następującego kodu:
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    Powyższy kod zostanie zainicjowany bazy danych hello hello informacje kontaktowe. Aby uzyskać więcej informacji na wstępne wypełnianie bazy danych hello, zobacz [bazami danych debugowanie Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. W hello **Konsola Menedżera pakietów** wprowadź polecenie hello:
   
        update-database
   
    ![Polecenia konsoli Menedżera pakietów][addcode009]
   
    Witaj **update-database** uruchamia hello pierwszej migracji, który tworzy hello bazy danych. Domyślnie program hello baza danych została utworzona jako baza danych programu SQL Server Express LocalDB.
8. Naciśnij klawisze CTRL + F5 toorun hello aplikacji. 

Aplikacja Hello zawiera hello inicjatora danych oraz edytowanie, szczegóły i Usuń linki.

![Widok MVC danych][rxz3]

## <a name="edit-hello-view"></a>Edytuj hello widoku
1. Otwórz hello *Views\Home\Index.cshtml* pliku. W następnym kroku hello, możemy spowoduje zamianę znaczników hello wygenerowany kod, który używa [jQuery](http://jquery.com/) i [Knockout.js](http://knockoutjs.com/). Ten kod pobiera hello listy kontaktów z przy użyciu interfejsu API sieci web i JSON, a następnie hello wiązania skontaktuj się z toohello danych interfejsu użytkownika przy użyciu knockout.js. Aby uzyskać więcej informacji, zobacz hello [następne kroki](#nextsteps) sekcji na końcu hello tego samouczka. 
2. Zastąp zawartość pliku hello hello hello następującego kodu.
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Kliknij prawym przyciskiem myszy folder zawartości hello, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element...** .
   
    ![Dodaj arkusz stylów w menu kontekstowym folder zawartości][addcode005]
4. W hello **Dodaj nowy element** okna dialogowego wprowadź **styl** w hello pole wyszukiwania prawy górny, a następnie wybierz **arkusz stylów**.
    ![Dodaj nowy element — okno dialogowe][rxStyle]
5. Nazwa pliku hello *Contacts.css* i kliknij przycisk **Dodaj**. Zastąp zawartość pliku hello hello hello następującego kodu.
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    Układ hello, kolory i style używane w aplikacji kontaktów Menedżerze hello użyjemy tego arkusza stylów.
6. Otwórz hello *App_Start\BundleConfig.cs* pliku.
7. Dodaj następującego kodu tooregister hello hello [Knockout](http://knockoutjs.com/index.html "KO") wtyczki.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Ten przykład przy użyciu odcinania toosimplify dynamiczne JavaScript kod obsługujący szablony ekranów powitalnych.
8. Modyfikowanie hello zawartość/css wpis tooregister hello *contacts.css* arkusza stylów. Zmień powitania po wierszu:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Aby:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. W konsoli Menedżera pakietów hello uruchom następujące polecenie tooinstall odcinania hello.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Dodawanie kontrolera interfejsu Web API Restful hello
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy kontrolerów i kliknij przycisk **Dodaj** , a następnie **kontrolera...** 
2. W hello **Dodawanie szkieletu** okna dialogowego wprowadź **Web Kontroler interfejsu API 2 z akcjami używający narzędzia Entity Framework** , a następnie kliknij przycisk **Dodaj**.
   
    ![Dodaj Kontroler interfejsu API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. W hello **Dodaj kontroler** okna dialogowego wprowadź "ContactsController" jako nazwę kontrolera. Wybierz "Kontaktu (ContactManager.Models)" dla hello **klasa modelu**.  Należy zachować wartość domyślną hello na powitania **klasa kontekstu danych**. 
4. Kliknij pozycję **Dodaj**.

### <a name="run-hello-application-locally"></a>Uruchamianie aplikacji hello lokalnie
1. Naciśnij klawisze CTRL + F5 toorun hello aplikacji.
   
    ![Strona indeksu][intro001]
2. Wprowadź kontaktu, a następnie kliknij przycisk **Dodaj**. Aplikacja Hello zwraca toohello strony głównej i wyświetla hello kontaktu, który został wprowadzony.
   
    ![Strona indeksu z elementów listy zadań do wykonania][addwebapi004]
3. W przeglądarce hello Dołącz **/api/contacts** toohello adresu URL.
   
    adres URL wynikowy Hello będzie podobny http://localhost:1234/api/contacts. RESTful Hello dodaniu interfejsu API sieci web zwraca hello przechowywane kontaktów. Firefox i Chrome wyświetli hello dane w formacie XML.
   
    ![Strona indeksu z elementów listy zadań do wykonania][rxFFchrome]

    Programu Internet Explorer będzie monitować tooopen lub zapisywać kontaktów hello.

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi006]


    Można także otworzyć hello zwrócił kontakty w Notatniku lub w przeglądarce.

    Te dane wyjściowe mogą być używane przez inną aplikację, takich jak przenośnych strony sieci web lub aplikacji.

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi007]

    **Ostrzeżenie o zabezpieczeniach**: W tym momencie aplikacja jest niebezpieczne i narażone tooCSRF ataku. Później w samouczku hello zostanie usunięty tę lukę w zabezpieczeniach. Aby uzyskać więcej informacji, zobacz [ataków interfejsu uniemożliwia Cross-Site żądania Międzywitrynowego (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Dodawanie ochrony XSRF
Sfałszowaniem żądania między witrynami (znanej także jako XSRF lub CSRF) jest atak wykorzystujący aplikacje obsługiwane w sieci web, zgodnie z którymi złośliwą witrynę sieci Web może mieć wpływ hello interakcji między przeglądarką klienta i witryny sieci Web ufa tej przeglądarki. Tego rodzaju ataki są możliwe, ponieważ przeglądarki sieci web wysyła tokeny uwierzytelniania automatycznie z każdej tooa żądania witryny sieci Web. canonical przykład Witaj jest pliku cookie uwierzytelniania, takich jak ASP. Biletu uwierzytelniania formularzy w sieci. Jednak tego rodzaju ataki może być celem witryn sieci Web, którego użyć dowolnego mechanizmu uwierzytelniania trwałe (takich jak uwierzytelnianie systemu Windows, Basic i tak dalej).

Atak XSRF różni się od ataku wyłudzaniem informacji. Wyłudzania wymagają interakcji z ofiara hello. Atak wyłudzaniem informacji złośliwą witrynę sieci Web będzie naśladować hello docelowa witryna sieci Web i ofiara hello jest fooled do ujawnienia atakująca toohello poufne informacje. W atak XSRF nie ma często bez interakcji z ofiara hello niezbędne. Zamiast osoba atakująca hello jest jednostki uzależnionej w przeglądarce hello są automatycznie wysyłane wszystkie odpowiednie pliki cookie toohello docelowej witryny sieci Web.

Aby uzyskać więcej informacji, zobacz hello [Otwórz projekt zabezpieczeń aplikacji sieci Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. W **Eksploratora rozwiązań**, prawy **ContactManager** projekt i kliknij przycisk **Dodaj** , a następnie kliknij przycisk **klasy**.
2. Nazwa pliku hello *ValidateHttpAntiForgeryTokenAttribute.cs* i Dodaj hello następującego kodu:
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. Dodaj następujące hello *przy użyciu* toohello instrukcji umów kontrolera, dlatego należy toohello dostępu **[ValidateHttpAntiForgeryToken]** atrybutu.
   
        using ContactManager.Filters;
4. Dodaj hello **[ValidateHttpAntiForgeryToken]** atrybutu metody Post toohello hello **ContactsController** tooprotect z XSRF zagrożeń. Spowoduje dodanie toohello "PutContact", "PostContact" i **DeleteContact** metody akcji.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Aktualizacja hello *skryptów* sekcji hello *Views\Home\Index.cshtml* pliku tooinclude kodu tooget hello XSRF tokenów.
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Publikowanie tooAzure aktualizacji aplikacji hello i bazy danych SQL
Aplikacja hello toopublish, powtórz procedury hello, a następnie wcześniej.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **publikowania**.
   
    ![Publikowanie][rxP]
2. Kliknij przycisk hello **ustawienia** kartę.
3. W obszarze **ContactsManagerContext(ContactsManagerContext)**, kliknij hello **v** toochange ikona *ciąg połączenia zdalnego* toohello parametry połączenia dla hello kontaktu Baza danych. Kliknij przycisk **ContactDB**.
   
    ![Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Sprawdź pola hello **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**.
5. Kliknij przycisk **dalej** , a następnie kliknij przycisk **Podgląd**. Visual Studio zostanie wyświetlona lista hello pliki, które zostaną dodane lub zaktualizowane.
6. Kliknij przycisk **Opublikuj**.
   Po zakończeniu wdrażania hello hello przeglądarce zostanie otwarty toohello strony głównej aplikacji hello.
   
    ![Strona indeksu z żadnych kontaktów][intro001]
   
    Hello Visual Studio publikuje parametry połączenia hello procesu automatycznie konfigurowane w hello wdrożone *Web.config* pliku toopoint toohello SQL w bazie danych. On również skonfigurowany migracje Code First tooautomatically hello uaktualnienia bazy danych toohello najnowszej wersji hello pierwszej aplikacji hello w czasie uzyskuje dostęp do bazy danych powitania po wdrożeniu.
   
    W wyniku tej konfiguracji Code First utworzył hello bazę danych, uruchamiając kod hello w hello **początkowej** klasy, który został utworzony wcześniej. Po wdrożeniu jak hello pierwszego czasu hello nastąpiła tooaccess hello bazy danych tej aplikacji.
7. Wprowadź kontaktu, jak w przypadku uruchomienia aplikacji hello lokalnie, tooverify, który wdrażania bazy danych zakończyło się pomyślnie.

Po wyświetleniu elementu hello wprowadzany jest zapisywana i pojawia się na stronie kontaktów Menedżerze hello wiadomo, że ma ona przechowywana w bazie danych hello.

![Strona indeksu z kontaktów][addwebapi004]

Aplikacja Hello jest teraz uruchomiona w chmurze hello przy użyciu bazy danych SQL toostore jego dane. Po zakończeniu testowania aplikacji hello na platformie Azure, należy ją usunąć. Aplikacja Hello jest publiczna i nie ma dostępu toolimit mechanizmu.

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="next-steps"></a>Następne kroki
Inny sposób toostore danych w aplikacji Azure jest toouse magazynu Azure, przechowywanie danych nierelacyjnych w formie hello obiekty BLOB i tabelach. Hello następujące linki udostępniają więcej informacji na interfejs API sieci Web, ASP.NET MVC i Windows Azure.

* [Wprowadzenie do korzystania z programu Entity Framework za pomocą MVC][EFCodeFirstMVCTutorial]
* [Wprowadzenie do tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Pierwszy ASP.NET interfejsu API sieci Web](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Debugowanie WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Zapisał tego samouczka i hello przykładowej aplikacji [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) z pomocą Dykstra Tomasz i Dorrans Marcin (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Wystaw opinię, co Ci się podoba lub co chcesz toosee zwiększona, nie tylko o samouczek hello, sam, ale także o produktach hello, przedstawiają go. Twoja opinia pomoże nam priorytety ulepszenia. Dbamy szczególnie w ustaleniu odsetek znajduje się w więcej automatyzacji procesu hello Konfigurowanie i wdrażanie hello bazy danych członkostwa. 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

