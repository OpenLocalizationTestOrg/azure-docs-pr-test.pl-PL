---
title: Tworzenie interfejsu API REST na platformie Azure z bazy danych SQL i programu ASP.NET | Dokumentacja firmy Microsoft
description: "Samouczek opisujący sposób wdrażania aplikacji, która używa interfejsu API sieci Web platformy ASP.NET dla aplikacji sieci web platformy Azure przy użyciu programu Visual Studio."
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
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Tworzenie usługi REST przy użyciu interfejsu API sieci Web platformy ASP.NET i bazy danych SQL w usłudze Azure App Service
Ten samouczek przedstawia sposób wdrażania aplikacji sieci web platformy ASP.NET do [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) za pomocą kreatora Publikowanie w sieci Web w programie Visual Studio 2013 lub Visual Studio 2013 Community Edition. 

Możesz otworzyć bezpłatne konto platformy Azure, a jeśli nie masz jeszcze programu Visual Studio 2013, zestaw SDK automatycznie instaluje program Visual Studio 2013 for Web Express. Dlatego możesz rozpocząć tworzenie dla platformy Azure i całkowicie bezpłatne.

Ten samouczek zakłada, że nie masz wcześniejszego doświadczenia korzysta z platformy Azure. Na wykonanie kroków tego samouczka, będziesz mieć aplikację sieci web proste się działającą w chmurze.

Dowiesz się:

* Jak umożliwić tworzenie aplikacji platformy Azure na komputerze przez zainstalowanie zestawu Azure SDK.
* Jak utworzyć projekt Visual Studio ASP.NET MVC 5 i opublikowania go w usłudze aplikacji Azure.
* Jak użyć interfejsu API sieci Web platformy ASP.NET w celu włączenia wywołania interfejsu API Restful.
* Jak używać bazy danych SQL do przechowywania danych na platformie Azure.
* Jak opublikować aktualizacje aplikacji na platformie Azure.

Proste listy kontaktów aplikacji sieci web, który jest oparty na programie ASP.NET MVC 5 i używa programu ADO.NET Entity Framework dla dostępu do bazy danych będzie kompilacji. Poniższa ilustracja przedstawia gotową aplikację:

![Zrzut ekranu przedstawiający witryny sieci web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a>Tworzenie projektu
1. Uruchom program Visual Studio 2013.
2. Z **pliku** kliknij menu **nowy projekt**.
3. W **nowy projekt** okna dialogowego rozwiń **Visual C#** i wybierz **Web** , a następnie wybierz **aplikacji sieci Web ASP.NET**. Nazwa aplikacji **ContactManager** i kliknij przycisk **OK**.
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. W **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **MVC** szablonu, sprawdź **interfejsu API sieci Web** , a następnie kliknij przycisk **Zmień uwierzytelnianie**.
5. W oknie dialogowym **Zmienianie uwierzytelniania** kliknij pozycję **Bez uwierzytelniania**, a następnie kliknij przycisk **OK**.
   
    ![Bez uwierzytelniania](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    Przykładowej aplikacji, które tworzysz, nie będziesz mieć funkcji, które wymagają użytkownikom logować się. Aby uzyskać informacje dotyczące sposobu implementowania funkcji uwierzytelniania i autoryzacji, zobacz [następne kroki](#nextsteps) sekcji na końcu tego samouczka. 
6. W **nowy projekt ASP.NET** okna dialogowego upewnij się, **Hostuj w chmurze** jest zaznaczony, a następnie kliknij przycisk **OK**.

Jeśli użytkownik ma nie wcześniej zalogowany na platformie Azure, pojawi się monit do logowania.

1. Kreator konfiguracji sugeruje unikatową nazwę, na podstawie *ContactManager* (zobacz obraz poniżej). Wybierz region w pobliżu. Można użyć [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") można znaleźć Centrum danych najniższym opóźnieniu. 
2. Jeśli nie utworzono serwera bazy danych przed, wybierz **Utwórz nowy serwer**, wprowadź nazwę bazy danych użytkownika i hasło.
   
    ![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Jeśli masz serwer bazy danych, użycie w celu utworzenia nowej bazy danych. Serwery bazy danych są cenne zasobów i zazwyczaj chcesz utworzyć wiele baz danych na tym samym serwerze do badania i rozwój zamiast serwera bazy danych dla bazy danych. Upewnij się, że witryna sieci web i bazy danych są w tym samym regionie.

![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a>Ustaw w nagłówku i stopce strony
1. W **Eksploratora rozwiązań**, rozwiń węzeł *Views\Shared* folderu i Otwórz *_Layout.cshtml* pliku.
   
    ![_Layout.cshtml w Eksploratorze rozwiązań][newapp004]
2. Zastąp zawartość *Views\Shared_Layout.cshtml* pliku następującym kodem:

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

Powyżej znaczników zmienia nazwę aplikacji z "Moja aplikacja ASP.NET" na "Skontaktuj się z menedżerem" i spowoduje usunięcie łącza do **Home**, **o** i **skontaktuj się z**.

### <a name="run-the-application-locally"></a>Uruchamianie aplikacji lokalnie
1. Naciśnij klawisze CTRL+F5, aby uruchomić aplikację.
   Strona główna aplikacji jest wyświetlana w domyślnej przeglądarce.
    ![Do wykonania strony głównej](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Wszystko co należy zrobić to teraz utworzyć aplikację, która będzie wdrażanie na platformie Azure. Będzie później dodać funkcji bazy danych.

## <a name="deploy-the-application-to-azure"></a>Wdrażanie aplikacji na platformie Azure
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **publikowania** z menu kontekstowego.
   
    ![Opublikuj w menu kontekstowego projektu][PublishVSSolution]
   
    **Publikowanie w sieci Web** zostanie otwarty Kreator.
2. Kliknij przycisk **Opublikuj**.

![Karta Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio rozpoczyna proces kopiowania plików na serwer platformy Azure. **Dane wyjściowe** okna pokazuje, jakie akcje wdrażania zostały pobrane i raporty pomyślnego wdrożenia.

1. Przeglądarka domyślna automatycznie otwiera adres URL wdrożonej lokacji.
   
   Utworzoną aplikację jest teraz uruchomiona w chmurze.
   
   ![Do strony głównej listy wykonania działające na platformie Azure][rxz2]

## <a name="add-a-database-to-the-application"></a>Dodaj bazę danych do aplikacji
Następnie będzie aktualizowana aplikacji MVC, aby dodać możliwości, aby wyświetlić i zaktualizować kontaktów i przechowywanie danych w bazie danych. Aplikacja będzie korzystać z programu Entity Framework, można utworzyć bazy danych i na odczytywanie i aktualizowanie danych w bazie danych.

### <a name="add-data-model-classes-for-the-contacts"></a>Dodawanie klasy modelu danych dla kontaktów
Można rozpocząć od tworzenia modelu danych proste w kodzie.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy folder modeli, kliknij przycisk **Dodaj**, a następnie **klasy**.
   
    ![Dodaj klasę w menu kontekstowym folderu modeli][adddb001]
2. W **Dodaj nowy element** okno dialogowe, nazwę nowego pliku klasy *Contact.cs*, a następnie kliknij przycisk **Dodaj**.
   
    ![Dodaj nowy element — okno dialogowe][adddb002]
3. Zastąp zawartość pliku Contacts.cs następującym kodem.
   
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

**Skontaktuj się z** klasa definiuje dane, które będą przechowywane dla każdego kontakt, a także klucz podstawowy, wartość ContactID, który jest wymagany przez bazę danych. Możesz uzyskać więcej informacji o modelach danych w [następne kroki](#nextsteps) sekcji na końcu tego samouczka.

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a>Tworzenie stron sieci web, które umożliwiają użytkownikom aplikacji do pracy z kontaktów
ASP.NET MVC funkcja szkieletów może automatycznie generować kod, który wykonuje tworzenia, odczytu, aktualizacji i usuwania (CRUD).

## <a name="add-a-controller-and-a-view-for-the-data"></a>Dodawanie kontrolera i widoku danych
1. W **Eksploratora rozwiązań**, rozwiń folder kontrolerów.
2. Skompiluj projekt **(Ctrl + Shift + B)**. (Aby można było używać mechanizmu szkieletów musi skompilować projekt). 
3. Kliknij prawym przyciskiem myszy folder kontrolery, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.
   
    ![Dodawanie kontrolera w menu kontekstowym folderu kontrolerów][addcode001]
4. W **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.
   
   ![Dodawanie kontrolera](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Ustaw nazwę kontrolera **HomeController**. Wybierz **skontaktuj się z** jako klasy modelu. Kliknij przycisk **nowy kontekst danych** przycisk i zaakceptuj wartość domyślną "ContactManager.Models.ContactManagerContext" dla **nowy typ kontekstu danych**. Kliknij pozycję **Dodaj**.

    Okno dialogowe zostanie wyświetlony monit: "plik o nazwie HomeController już kończy działanie. Czy chcesz go zastąpić? ". Kliknij przycisk **Yes** (Tak). Firma Microsoft są Zastępowanie kontrolera Narzędzia główne, który został utworzony nowy projekt. Firma Microsoft będzie używać nowego kontrolera Home naszej listy kontaktów.

    Program Visual Studio tworzy metod kontrolera oraz widoki dla operacji CRUD bazy danych dla **skontaktuj się z** obiektów.

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a>Włącz migracji, utworzyć bazę danych, Dodawanie przykładowych danych i inicjatora danych
Następne zadanie jest umożliwienie [migracje Code First](http://curah.microsoft.com/55220) funkcji, aby można było utworzyć bazę danych opartą na modelu danych został utworzony.

1. W **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** , a następnie **Konsola Menedżera pakietów**.
   
    ![Konsola Menedżera pakietów w menu Narzędzia][addcode008]
2. W **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie:
   
        enable-migrations 
   
    **Enable-migrations,** polecenie tworzy *migracje* folderu i jego umieszcza w tym folderze *Configuration.cs* pliku, który można edytować w celu konfigurowania migracji. 
3. W **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie:
   
        add-migration Initial
   
    **Początkowego dodać migracji** polecenie generuje klasę o nazwie  **&lt;date_stamp&gt;początkowej** tworzącą bazy danych. Pierwszy parametr ( *początkowej* ) jest dowolnego i używany do tworzenia nazwy pliku. Widać nowe pliki klasy w **Eksploratora rozwiązań**.
   
    W **początkowej** klasy **się** metoda tworzy tabeli kontaktów i **dół** — metoda (używane, jeśli chcesz powrócić do poprzedniego stanu) porzuca go.
4. Otwórz *Migrations\Configuration.cs* pliku. 
5. Dodaj następujących przestrzeni nazw. 
   
         using ContactManager.Models;
6. Zastąp *inicjatora* metodę z następującym kodem:
   
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
   
    Powyższy kod zostanie zainicjowany bazy danych o informacje kontaktowe. Aby uzyskać więcej informacji dotyczących wstępnego wypełniania bazy danych, zobacz [bazami danych debugowanie Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. W **Konsola Menedżera pakietów** wprowadź polecenie:
   
        update-database
   
    ![Polecenia konsoli Menedżera pakietów][addcode009]
   
    **Update-database** uruchamia pierwszej migracji, które utworzy bazę danych. Domyślnie baza danych została utworzona jako baza danych programu SQL Server Express LocalDB.
8. Naciśnij klawisze CTRL+F5, aby uruchomić aplikację. 

Aplikacja zawiera dane inicjatora i łącza edycji, szczegóły i delete.

![Widok MVC danych][rxz3]

## <a name="edit-the-view"></a>Edytuj widok
1. Otwórz *Views\Home\Index.cshtml* pliku. W następnym kroku możemy spowoduje zamianę znaczników wygenerowanego kodu korzystającego z [jQuery](http://jquery.com/) i [Knockout.js](http://knockoutjs.com/). Ten kod pobiera listy kontaktów z przy użyciu interfejsu API sieci web i JSON i czym wiąże się z działem dane do interfejsu użytkownika przy użyciu knockout.js. Aby uzyskać więcej informacji, zobacz [następne kroki](#nextsteps) sekcji na końcu tego samouczka. 
2. Zastąp zawartość pliku następującym kodem.
   
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
3. Kliknij prawym przyciskiem myszy folder zawartości, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element...** .
   
    ![Dodaj arkusz stylów w menu kontekstowym folder zawartości][addcode005]
4. W **Dodaj nowy element** okna dialogowego wprowadź **styl** w prawym górnym w polu wyszukiwania, a następnie wybierz **arkusz stylów**.
    ![Dodaj nowy element — okno dialogowe][rxStyle]
5. Nadaj nazwę plikowi *Contacts.css* i kliknij przycisk **Dodaj**. Zastąp zawartość pliku następującym kodem.
   
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
   
    Układ, kolory i style używane w aplikacji kontaktów Menedżerze użyjemy tego arkusza stylów.
6. Otwórz *App_Start\BundleConfig.cs* pliku.
7. Dodaj następujący kod, aby zarejestrować [Knockout](http://knockoutjs.com/index.html "KO") wtyczki.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Ten przykład przy użyciu odcinania uprościć dynamiczny kod JavaScript, który obsługuje szablony ekranu.
8. Zmodyfikuj wpis zawartość/css, aby zarejestrować *contacts.css* arkusza stylów. Zmień następujący wiersz:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Aby:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. W konsoli Menedżera pakietów uruchom następujące polecenie, aby zainstalować odcinania.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a>Dodawanie kontrolera dla interfejsu sieci Web interfejsu API Restful.
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy kontrolerów i kliknij przycisk **Dodaj** , a następnie **kontrolera...** 
2. W **Dodawanie szkieletu** okna dialogowego wprowadź **Web Kontroler interfejsu API 2 z akcjami używający narzędzia Entity Framework** , a następnie kliknij przycisk **Dodaj**.
   
    ![Dodaj Kontroler interfejsu API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. W **Dodaj kontroler** okna dialogowego wprowadź "ContactsController" jako nazwę kontrolera. Wybierz "Kontaktu (ContactManager.Models)" dla **klasa modelu**.  Należy zachować wartość domyślną dla **klasa kontekstu danych**. 
4. Kliknij pozycję **Dodaj**.

### <a name="run-the-application-locally"></a>Uruchamianie aplikacji lokalnie
1. Naciśnij klawisze CTRL+F5, aby uruchomić aplikację.
   
    ![Strona indeksu][intro001]
2. Wprowadź kontaktu, a następnie kliknij przycisk **Dodaj**. Aplikacja zwraca do strony głównej i wyświetla kontaktu, który został wprowadzony.
   
    ![Strona indeksu z elementów listy zadań do wykonania][addwebapi004]
3. W przeglądarce, dołącz **/api/contacts** do adresu URL.
   
    Adres URL wynikowy będzie podobny http://localhost:1234/api/contacts. RESTful interfejsu API sieci web dodano zwraca przechowywanych kontaktów. Firefox i Chrome będą wyświetlane dane w formacie XML.
   
    ![Strona indeksu z elementów listy zadań do wykonania][rxFFchrome]

    IE spowoduje wyświetlenie monitu o otworzyć lub zapisać kontaktów.

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi006]


    Możesz otworzyć zwrócony kontakty w Notatniku lub w przeglądarce.

    Te dane wyjściowe mogą być używane przez inną aplikację, takich jak przenośnych strony sieci web lub aplikacji.

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi007]

    **Ostrzeżenie o zabezpieczeniach**: W tym momencie aplikacja jest niebezpieczne i narażone na atak CSRF. W dalszej części tego samouczka zostanie usunięty tę lukę w zabezpieczeniach. Aby uzyskać więcej informacji, zobacz [ataków interfejsu uniemożliwia Cross-Site żądania Międzywitrynowego (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Dodawanie ochrony XSRF
Sfałszowaniem żądania między witrynami (znanej także jako XSRF lub CSRF) jest atak wykorzystujący aplikacje obsługiwane w sieci web, zgodnie z którymi złośliwą witrynę sieci Web może mieć wpływ interakcji między przeglądarką klienta i witryny sieci Web ufa tej przeglądarki. Tego rodzaju ataki są możliwe, ponieważ przeglądarki sieci web wysyła tokeny uwierzytelniania automatycznie z każdym żądaniem do witryny sieci Web. Canonical przykładem jest pliku cookie uwierzytelniania, takich jak ASP. Biletu uwierzytelniania formularzy w sieci. Jednak tego rodzaju ataki może być celem witryn sieci Web, którego użyć dowolnego mechanizmu uwierzytelniania trwałe (takich jak uwierzytelnianie systemu Windows, Basic i tak dalej).

Atak XSRF różni się od ataku wyłudzaniem informacji. Wyłudzania wymagają interakcji z ofiary. Atak phishing złośliwą witrynę sieci Web będzie naśladować docelowa witryna sieci Web i ofiary jest fooled na dostarczanie informacji poufnych dla osoby atakującej. W atak XSRF nie ma często bez interakcji z ofiary niezbędne. Osoba atakująca jest raczej jednostki uzależnionej w przeglądarce, wszystkie odpowiednie pliki cookie są automatycznie wysyłane do docelowej witryny sieci Web.

Aby uzyskać więcej informacji, zobacz [Otwórz projekt zabezpieczeń aplikacji sieci Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. W **Eksploratora rozwiązań**, prawy **ContactManager** projekt i kliknij przycisk **Dodaj** , a następnie kliknij przycisk **klasy**.
2. Nadaj nazwę plikowi *ValidateHttpAntiForgeryTokenAttribute.cs* i Dodaj następujący kod:
   
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
3. Dodaj następujące *przy użyciu* instrukcji do kontrolera kontrakty, musisz mieć dostęp do **[ValidateHttpAntiForgeryToken]** atrybutu.
   
        using ContactManager.Filters;
4. Dodaj **[ValidateHttpAntiForgeryToken]** atrybut do metody Post **ContactsController** do ochrony przed zagrożeniami XSRF. Doda do "PutContact", "PostContact" i **DeleteContact** metody akcji.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Aktualizacja *skryptów* sekcji *Views\Home\Index.cshtml* pliku, aby uwzględnić kod w celu uzyskania XSRF tokenów.
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a>Publikowanie aktualizacji aplikacji na platformie Azure oraz bazy danych SQL
Aby opublikować aplikację, możesz Powtórz procedurę, które zostały wykonane wcześniej.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.
   
    ![Publikowanie][rxP]
2. Kliknij kartę **Ustawienia**.
3. W obszarze **ContactsManagerContext(ContactsManagerContext)**, kliknij przycisk **v** ikonę, aby zmienić *ciąg połączenia zdalnego* w parametrach połączenia dla bazy danych kontaktowych. Kliknij przycisk **ContactDB**.
   
    ![Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Pole wyboru dla **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**.
5. Kliknij przycisk **dalej** , a następnie kliknij przycisk **Podgląd**. Visual Studio zostanie wyświetlona lista plików, które zostaną dodane lub zaktualizowane.
6. Kliknij przycisk **Opublikuj**.
   Po zakończeniu wdrożenia, przeglądarka otworzy się do strony głównej aplikacji.
   
    ![Strona indeksu z żadnych kontaktów][intro001]
   
    Visual Studio automatycznie publikowania procesu skonfigurowanych parametrów połączenia w wdrożone *Web.config* pliku do punktu z bazą danych SQL. On również skonfigurowany migracje Code First automatycznie przy pierwszym aplikacja uzyskuje dostęp do bazy danych po wdrożeniu uaktualnienie do najnowszej wersji bazy danych.
   
    W wyniku tej konfiguracji Code First baza danych utworzona uruchamiając kod na **początkowej** klasy, który został utworzony wcześniej. Jak to aplikacja próbowała dostęp do bazy danych po wdrożeniu po raz pierwszy.
7. Wprowadź kontaktu, tak jak po uruchomieniu aplikacji lokalnie, aby sprawdzić, czy wdrożenie bazy danych zakończyło się pomyślnie.

Gdy pojawi się, że element, który możesz wprowadzić jest zapisywana i jest wyświetlany na stronie kontaktów Menedżerze, wiadomo, że ma ona przechowywana w bazie danych.

![Strona indeksu z kontaktów][addwebapi004]

Aplikacja jest teraz uruchomiona w chmurze przy użyciu bazy danych SQL do przechowywania danych. Po zakończeniu testowania aplikacji na platformie Azure, należy ją usunąć. Aplikacja nie jest publiczny i nie ma mechanizmu, aby ograniczyć dostęp.

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="next-steps"></a>Następne kroki
Inny sposób przechowywania danych w aplikacji Azure jest użycie magazynu Azure, które zapewniają magazynu danych nierelacyjnych w formie obiektów blob i tabelach. Poniższe linki udostępniają więcej informacji na interfejs API sieci Web, ASP.NET MVC i Windows Azure.

* [Wprowadzenie do korzystania z programu Entity Framework za pomocą MVC][EFCodeFirstMVCTutorial]
* [Wprowadzenie do platformy ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Pierwszy ASP.NET interfejsu API sieci Web](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Debugowanie WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

W tym samouczku i przykładowa aplikacja została napisana przy [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) z pomocą Dykstra Tomasz i Dorrans Marcin (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Sprawdź Wystaw opinię, co Ci się podoba lub chcesz zobaczyć zwiększona, nie tylko o samouczka sam, ale także o produktach, które pokazuje go. Twoja opinia pomoże nam priorytety ulepszenia. Dbamy szczególnie w ustaleniu odsetek istnieje więcej automatyzacji procesu, konfigurowanie i wdrażanie bazy danych członkostwa. 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
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

