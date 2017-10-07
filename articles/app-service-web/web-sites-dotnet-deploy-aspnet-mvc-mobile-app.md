---
title: "aaaDeploy ASP.NET MVC 5 aplikacji sieci web urządzeń przenośnych w usłudze Azure App Service"
description: "Samouczek opisujący sposób funkcji toodeploy tooAzure aplikacji sieci web usługi aplikacji przy użyciu przenośnych w platformie ASP.NET MVC 5 aplikacji sieci web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Wdrażanie aplikacji ASP.NET MVC 5 sieci web urządzeń przenośnych w usłudze Azure App Service
W tym samouczku udzieli hello podstawy jak toobuild ASP.NET MVC 5 sieci web aplikacji, która jest przyjaznych dla urządzeń przenośnych i wdrożyć ją tooAzure usługi aplikacji. W tym samouczku potrzebne [programu Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] lub w wersji professional hello programu Visual Studio, jeśli masz już który. Można użyć [programu Visual Studio 2015] , ale hello zrzuty ekranu mogą być inne, i musi być hello ASP.NET 4.x szablonów.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Jakie będzie kompilacji
W tym samouczku zostanie dodana Funkcje mobilne toohello proste konferencji listę aplikacji, która znajduje się w hello [projektu starter][StarterProject]. Hello Poniższy zrzut ekranu przedstawia hello sesji programu ASP.NET w aplikacji hello ukończone, jak pokazano w emulatorze przeglądarki hello w narzędzi deweloperskich programu Internet Explorer 11 F12.

![][FixedSessionsByTag]

Można użyć narzędzia dla deweloperów hello F12 programu Internet Explorer 11 i hello [narzędzie Fiddler] [ Fiddler] toohelp debugowania aplikacji. 

## <a name="skills-youll-learn"></a>Dowiesz się umiejętności
Oto dowiesz się:

* Jak toopublish toouse programu Visual Studio 2013 aplikacji sieci web bezpośrednio tooa aplikacji sieci web w usłudze Azure App Service.
* Jak szablony hello ASP.NET MVC 5 za pomocą architektury CSS Bootstrap hello zwiększające wyświetlania na urządzeniach przenośnych
* Jak toocreate mobile określonych widoków tootarget określonych przeglądarki dla urządzeń przenośnych, takich jak hello iPhone i Android
* Jak widoki dynamiczne toocreate (widoki, które odpowiadają toodifferent przeglądarki na urządzeniach)

## <a name="set-up-hello-development-environment"></a>Konfigurowanie środowiska deweloperskiego hello
Konfigurowanie środowiska programowania przez zainstalowanie hello Azure SDK dla platformy .NET 2.5.1 lub nowszej. 

1. Witaj tooinstall zestawu Azure SDK dla platformy .NET, kliknij poniższe łącze hello. Jeśli nie masz jeszcze zainstalowany program Visual Studio 2013, zostanie zainstalowany przez łącze hello. Ten samouczek wymaga programu Visual Studio 2013. [Zestaw Azure SDK dla programu Visual Studio 2013][AzureSDKVs2013]
2. W oknie Instalatora platformy sieci Web powitania kliknij **zainstalować** i kontynuować hello instalacji.

Należy również emulatora przeglądarkę dla telefonów. Jedną z następujących przyczyn hello będzie działać:

* Emulator przeglądarki w [narzędzi deweloperskich programu Internet Explorer 11 F12] [ EmulatorIE11] (używane na wszystkich przeglądarkę dla telefonów zrzutach ekranu). Ma ona predefiniowane ciąg agenta użytkownika dla systemu Windows Phone 8, Windows Phone 7 i iPad firmy Apple.
* Emulator przeglądarki w [DevTools Google Chrome][EmulatorChrome]. Zawiera ustawienia dla wielu urządzeń z systemem Android, a także Apple iPhone, iPad firmy Apple oraz Amazon Kindle Fire. Emuluje on również zdarzenia touch.
* [Opera emulatorze przenośnym][EmulatorOpera]

Projekty Visual Studio z C\# kod źródłowy są dostępne tooaccompany w tym temacie:

* [Początkowy projektem do pobrania][StarterProject]
* [Pobranie projektu zakończone][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Wdrażanie hello starter projektu tooan aplikacji sieci web Azure
1. Pobierz aplikację listy konferencji hello [projektu starter][StarterProject].
2. Następnie w Eksploratorze Windows, kliknij prawym przyciskiem myszy hello pobrany plik ZIP i wybierz *właściwości*.
3. W hello **właściwości** oknie dialogowym Wybierz hello **Odblokuj** przycisku. (Odblokowywania uniemożliwia ostrzeżenie występujący podczas próby toouse *.zip* pliku pobranym z sieci web hello.)
4. Kliknij prawym przyciskiem myszy plik ZIP hello i wybierz **Wyodrębnij wszystkie** rozpakować pliku hello. 
5. W programie Visual Studio Otwórz hello *C#\Mvc5Mobile.sln* pliku.
6. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **publikowania**.
   
   ![][DeployClickPublish]
7. Na publikowanie w sieci Web, kliknij **Microsoft Azure App Service**.
   
   ![][DeployClickWebSites]
8. Jeśli jeszcze nie zostało to jeszcze zalogowania na platformie Azure, kliknij przycisk **Dodaj konto**.
   
   ![][DeploySignIn]
9. Wykonaj toolog monity hello na konto platformy Azure.
10. Witaj w oknie dialogowym App Service powinna zostać wyświetlona zostanie jako zalogowany. Kliknij przycisk **Nowy**.
    
    ![][DeployNewWebsite]  
11. W hello **Nazwa aplikacji sieci Web** określ prefiks nazwy aplikacji unikatowy. Twoje Pełna nazwa aplikacji sieci web będzie  *&lt;prefiks >*. azurewebsites.net. Ponadto wybierz lub określ nazwę nowej grupy zasobów w **grupy zasobów**. Następnie kliknij przycisk **nowy** toocreate nowy plan usługi aplikacji.
    
    ![][DeploySiteSettings]
12. Skonfiguruj nowy plan usługi aplikacji hello, a następnie kliknij przycisk **OK**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. W oknie dialogowym Tworzenie usługi App Service hello, kliknij **Utwórz**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Po hello Azure zasoby są tworzone, hello publikowanie w sieci Web w oknie dialogowym zostanie wypełniony hello ustawienia dla nowej aplikacji. Kliknij przycisk **Opublikuj**.
    
    ![][DeployPublishSite]
    
    Po zakończeniu publikowania aplikacji sieci web platformy Azure toohello projektu hello starter Visual Studio, hello pulpitu przeglądarce zostanie otwarty w aplikacji sieci web na żywo hello toodisplay.
15. Uruchom emulator Twojej przeglądarkę dla telefonów, skopiuj adres URL aplikacji konferencji hello hello (*<prefix>*. azurewebsites.net) w emulatorze hello, a następnie kliknij przycisk prawym górnym rogu i wybierz **Przeglądaj według znaczników**. Jeśli korzystasz z programu Internet Explorer 11 jako hello domyślnej przeglądarki, wystarczy tootype `F12`, następnie `Ctrl+8`, a następnie zmień profilu przeglądarki hello zbyt**Windows Phone**. Na poniższym obrazie pokazano hello *alltags —* widok w trybie portret (wybór **Przeglądaj według znaczników**).
    
    ![][AllTags]

> [!TIP]
> Podczas gdy można debugować aplikacji MVC 5 z poziomu programu Visual Studio, tooAzure aplikacji sieci web można opublikować ponownie tooverify hello na żywo aplikacji sieci web bezpośrednio w przeglądarce przenośnych lub w emulatorze przeglądarki.
> 
> 

Wyświetlanie Hello jest bardzo do odczytu na urządzeniu przenośnym. Można także już widoczne niektóre hello efekty wizualne zastosowane przez platformę Bootstrap CSS hello.
Kliknij przycisk hello **ASP.NET** łącza.

![][SessionsByTagASP.NET]

Witaj widok tagów ASP.NET jest zainstalowane powiększenia toohello ekran, który jest dla Ciebie automatycznie ładowania początkowego. Jednak może poprawić ten widok toobetter koloru hello przeglądarkę dla telefonów. Na przykład Witaj **data** kolumna jest trudny do odczytania. Później w samouczku hello zostanie zmieniona hello *alltags —* wyświetlić toomake go przyjaznych dla urządzeń przenośnych.

## <a name="bkmk_bootstrap"></a>Framework bootstrap CSS
Nowe hello MVC 5 szablon jest wbudowana obsługa ładowania początkowego. Ma już widoczny, jak od razu zwiększa hello różne widoki w aplikacji. Na przykład pasek nawigacyjny hello u góry hello jest zwijany automatycznie, gdy szerokość przeglądarki hello jest mniejsza. W przeglądarce pulpitu hello należy spróbować zmienić rozmiar okna przeglądarki hello i zobacz, jak pasek nawigacyjny hello zmienia jego wygląd i działanie. Jest to hello web elastyczny projekt, który jest wbudowana w ładowania początkowego.

toosee jak hello aplikacji sieci Web będzie wyglądać bez ładowania początkowego, otwórz *aplikacji\_Start\\BundleConfig.cs* ujmij w komentarz hello wierszy, które zawierają *bootstrap.js* i *bootstrap.css*. Witaj poniższy kod przedstawia hello ostatnich dwóch instrukcje hello `RegisterBundles` metody po zmianie hello:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Naciśnij klawisz `Ctrl+F5` toorun hello aplikacji.

Obserwować paska nawigacyjnego zwijanej hello jest teraz wystarczy zwykłe nieuporządkowaną listę. Kliknij przycisk **Przeglądaj według znaczników** ponownie, następnie kliknij przycisk **ASP.NET**.
W widoku emulatorze przenośnym hello widać, nie jest już zainstalowane powiększenia toohello ekranu i musieli przewijać bok w kolejności toosee powitania po prawej stronie powitania tabeli.

![][SessionsByTagASP.NETNoBootstrap]

Cofnij zmiany, a następnie Odśwież tooverify przeglądarkę dla telefonów hello wyświetlana przyjazna hello została przywrócona.

Ładowania początkowego nie jest określonym tooASP.NET MVC 5, a w dowolnej aplikacji sieci web mogą korzystać z tych funkcji. Ale teraz są wbudowane w szablon projektu programu ASP.NET MVC 5, dzięki czemu aplikacja sieci MVC 5 Web można korzystać z Bootstrap domyślnie.

Aby uzyskać więcej informacji na temat ładowania początkowego Przejdź toothe [Bootstrap] [ BootstrapSite] lokacji.

W następnej sekcji hello zobaczysz jak tooprovide mobile przeglądarki konkretnych widoków.

## <a name="bkmk_overrideviews"></a>Zastąpienie hello widoki, układów i widoki częściowe
Można zastąpić dowolnym widoku (w tym układy i widoki częściowe) dla przeglądarki dla urządzeń przenośnych ogólnie rzecz biorąc, poszczególne przeglądarkę dla telefonów lub dowolnej przeglądarki określone. wyświetlanie konkretnego mobile tooprovide, możesz skopiować plik widoku i dodać *. Mobile* toohello nazwę pliku. Na przykład toocreate przenośnym *indeksu* widoku, możesz skopiować *widoków\\Home\\Index.cshtml* do *widoków\\Home\\ Index.Mobile.cshtml*.

W tej sekcji utworzysz plik układu specyficzne dla mobilnych.

toostart, kopiowania *widoków\\Shared\\\_Layout.cshtml* do *widoków\\Shared\\\_Layout.Mobile.cshtml* . Otwórz  *\_Layout.Mobile.cshtml* i Zmień tytuł hello z **aplikacji MVC5** za**MVC5 aplikacji (Mobile)**.

W każdym `Html.ActionLink` wywołać paska nawigacyjnego hello, Usuń "Przeglądaj według", w każdym odnośniku *ActionLink*. Witaj poniższy kod przedstawia ukończyć powitalnych `<ul class="nav navbar-nav">` tag hello przenośnych układ pliku.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Hello kopiowania *widoków\\Home\\AllTags.cshtml* pliku *widoków\\Home\\AllTags.Mobile.cshtml*. Otwórz nowy plik hello i zmień `<h2>` element na podstawie "Tagi" za "tagi (M)":

    <h2>Tags (M)</h2>

Przeglądaj toohello tagi strony w przeglądarce pulpitu i przy użyciu emulatora przeglądarkę dla telefonów. emulator przeglądarkę dla telefonów Hello pokazuje Witaj dwie zmiany wprowadzone (hello tytuł z  *\_Layout.Mobile.cshtml* i tytuł hello z *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Z kolei hello ekranu nie został zmieniony (tytułów z  *\_Layout.cshtml* i *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a>Utwórz widoki specyficzne dla przeglądarki
Ponadto toomobile dotyczące pulpitu i widoki, można tworzyć widoki dla poszczególnych przeglądarki. Na przykład można tworzyć widoki, które są przeznaczone dla hello iPhone lub hello przeglądarki systemu Android. W tej sekcji utworzysz układ hello iPhone przeglądarki i wersji iPhone hello *alltags —* widoku.

Otwórz hello *Global.asax* plik i dodać powitania od dołu toohello kodu `Application_Start` — metoda.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Ten kod definiuje nowy tryb wyświetlania o nazwie "iPhone" pasujących względem każdego żądania przychodzącego. Jeśli hello żądanie przychodzące odpowiada warunku, zdefiniowane przez użytkownika (jeśli agent użytkownika hello zawiera ciąg hello "iPhone"), platformy ASP.NET MVC sprawdza widoki, których nazwa zawiera sufiksu "iPhone".

> [!NOTE]
> Podczas dodawania przenośnych przeglądarki specyficzne dla tryby wyświetlania, takich jak dla urządzenia iPhone i Android, można się tooset hello pierwszy argument zbyt`0` się, że w trybie specyficzne dla przeglądarki hello mają pierwszeństwo przed szablonu przenośnych hello toomake (Wstaw u góry hello hello listy) (*. Mobile.cshtml). Jeśli szablon przenośnych hello jest na początku listy hello hello, zostanie wybrana przez tryb wyświetlania zamierzone (hello pierwszego dopasowania wins i hello przenośnych szablon jest zgodny wszystkie przeglądarki dla urządzeń przenośnych). 
> 
> 

W kodzie hello, kliknij prawym przyciskiem myszy `DefaultDisplayMode`, wybierz **rozwiązać**, a następnie wybierz pozycję `using System.Web.WebPages;`. Spowoduje to dodanie toothe odwołanie `System.Web.WebPages` przestrzeni nazw, czyli gdzie `DisplayModeProvider` i `DefaultDisplayMode` typy zostały zdefiniowane.

![][ResolveDefaultDisplayMode]

Alternatywnie można dodawać tylko ręcznie powitania po wierszu toothe `using` sekcji hello pliku.

    using System.Web.WebPages;

Zapisz zmiany hello. Kopia *widoków\\Shared\\\_Layout.Mobile.cshtml* pliku na *widoków\\współużytkowane\\\_Layout.iPhone.cshtml*. Otwórz nowy plik hello, a następnie zmień tytuł hello z `MVC5 Application (Mobile)` do `MVC5 Application (iPhone)`.

Hello kopiowania *widoków\\Home\\AllTags.Mobile.cshtml* pliku *widoków\\Home\\AllTags.iPhone.cshtml*. W hello nowy plik, zmień hello `<h2>` element z "tagi (M)" za "tagi (iPhone)".

Uruchamianie aplikacji hello. Uruchamianie emulatora przeglądarkę dla telefonów, upewnij się, że jego agenta użytkownika ustawiono zbyt "iPhone", a następnie przejdź toohello *alltags —* widoku. Jeśli używasz emulatora hello w narzędzi deweloperskich programu Internet Explorer 11 naciśnięcia klawisza F12, skonfiguruj emulacji toohello poniżej:

* Profil przeglądarki = **Windows Phone**
* Ciąg agenta użytkownika = **niestandardowe**
* Niestandardowy ciąg = **Apple-iPhone5C1/1001.525**

Witaj Poniższy zrzut ekranu przedstawia hello *alltags —* widok renderowany w emulatorze w narzędzi deweloperskich programu Internet Explorer 11 F12 z hello niestandardowy ciąg agenta użytkownika (jest to ciąg agenta użytkownika iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

W przeglądarce przenośnych hello, wybierz hello **głośniki** łącza. Ponieważ nie jest widokiem dla urządzeń przenośnych (*AllSpeakers.Mobile.cshtml*), wyświetlanie głośniki domyślne hello (*AllSpeakers.cshtml*) jest renderowany przy użyciu widoku układu przenośnych hello ( *\_ Layout.Mobile.cshtml*). Jak pokazano poniżej, tytuł hello **MVC5 aplikacji (Mobile)** jest zdefiniowany w  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Widok domyślny (nieprzenośnych) z renderowania w układzie przenośnych globalnie można wyłączyć, ustawiając `RequireConsistentDisplayMode` do `true` w hello *widoków\\\_ViewStart.cshtml* pliku następująco:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Gdy `RequireConsistentDisplayMode` ustawiono zbyt`true`, układ przenośnych hello (*\_Layout.Mobile.cshtml*) jest używany tylko dla widoków przenośnych (tj. gdy plik widoku ma formę hello  ***ViewName** . Mobile.cshtml*). Może być tooset `RequireConsistentDisplayMode` zbyt`true` Jeśli przenośnych układu nie działa prawidłowo w przypadku widoków przeznaczone dla urządzeń przenośnych. Witaj zrzut ekranu poniżej przedstawiono sposób hello *głośniki* renderowania strony, gdy `RequireConsistentDisplayMode` ustawiono zbyt`true` (bez ciąg hello "(wersja Mobile)" w nawigacji pasków u góry hello hello).

![][AllSpeakers_LayoutMobileOverridden]

Spójnego trybu wyświetlania w określonym widoku można wyłączyć, ustawiając `RequireConsistentDisplayMode` zbyt`false` hello widoku pliku. Następujący kod w hello *widoków\\Home\\AllSpeakers.cshtml* plików zestawów `RequireConsistentDisplayMode` zbyt`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

Możemy w tej sekcji przedstawiono sposób toocreate przenośnych układy i widoki i jak układów toocreate oraz widoki dla konkretnych urządzeń, takich jak hello iPhone.
Główną zaletą framework Bootstrap CSS hello hello jest jednak elastyczny układ, co oznacza, że jednego arkusza stylów mogą być stosowane przez pulpitu, telefon i tablet przeglądarki toocreate spójny wygląd i zachowanie. W następnej sekcji hello zobaczysz, jak tooleverage Bootstrap przyjazna toocreate widoków.

## <a name="bkmk_Improvespeakerslist"></a>Poprawa hello głośniki listy
Jak został wyświetlony, hello *głośniki* widoku jest możliwy do odczytu, ale linki hello są małe i są trudne tootap na urządzeniu przenośnym. W tej sekcji należy podjąć hello *AllSpeakers* głośniki można odnaleźć widoku przyjaznych dla urządzeń przenośnych, która wyświetla dużych, łatwe wybranie łącza i zawiera tooquickly pola wyszukiwania.

Można użyć hello Bootstrap [listy połączonej grupy] [ linked list group] stylów zwiększające hello *głośniki* widoku. W *widoków\\Home\\AllSpeakers.cshtml*, Zastąp zawartość pliku Razor hello hello hello kod poniżej.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Witaj `class="list-group"` atrybutu w hello `<div>` znacznik stosuje style Bootstrap listy i hello `class="input-group-item"` atrybut jest stosowany link tooeach stylów elementu listy ładowania początkowego.

Odśwież przeglądarkę dla telefonów hello. Witaj zaktualizowany widok wygląda następująco:

![][AllSpeakersFixed]

Witaj Bootstrap [listy połączonej grupy] [ linked list group] stylów sprawia, że hello całe okno dla każdego łącza, które są aktywne, czyli znacznie lepsze środowisko użytkownika. Przełącz widok pulpitu toothe i obserwować hello spójny wygląd i zachowanie.

![][AllSpeakersFixedDesktop]

Chociaż hello przeglądarkę dla telefonów widoku została ulepszona i jest trudno hello długą listę głośniki. Ładowania początkowego nie zapewnia wyszukiwania filtr funkcji out-of box, ale można go dodać przy użyciu kilku wierszy kodu. Należy najpierw dodać widok toohello pole wyszukiwania, a następnie podłączanie z hello kod JavaScript hello filtru funkcji. W *widoków\\Home\\AllSpeakers.cshtml*, Dodaj \<formularza\> tag zaraz po hello \<h2\> tagów, jak pokazano poniżej:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Zwróć uwagę, że hello `<form>` i `<input>` tagi zarówno ma hello toothem Bootstrap zastosowane style. Witaj `<span>` element dodaje Bootstrap [glyphicon] [ glyphicon] toothe pola wyszukiwania.

W hello *skryptów* folderu, Dodaj plik JavaScript o nazwie *filter.js*. Otwórz plik hello i Wklej hello następującego kodu do niej:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

Należy również tooinclude filter.js w Twojej zarejestrowanych pakietów. Otwórz *aplikacji\_Start\\BundleConfig.cs* i zmień hello pierwszy pakietów. Zmień pierwsze `bundles.Add` instrukcji (dla hello **jquery** pakietu) tooinclude *skryptów\\filter.js*w następujący sposób:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Witaj **jquery** pakietu jest już renderowana domyślnie hello  *\_układu* widoku. Później, możesz użyć hello JavaScript tego samego kodu tooapply widoki list tooother funkcji filtru.

Odśwież przeglądarkę dla telefonów hello i przejdź toohello *AllSpeakers* widoku. W polu wyszukiwania wpisz "sc". listy głośniki Hello teraz można filtrować według tooyour ciąg wyszukiwania.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Poprawa hello listy tagów
Podobnie jak hello *głośniki* wyświetlić, hello *tagi* widoku jest możliwy do odczytu, ale linki hello są małe i trudne tootap na urządzeniu przenośnym. Można naprawić hello *tagi* widoku hello sam sposób naprawić hello *głośniki* wyświetlić, jeśli używasz zmiany kodu hello opisanego wcześniej, ale przy użyciu następujących hello `Html.ActionLink` składni metody w  *Widoki\\Home\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Hello odświeżyć przeglądarkę dla komputerów wygląda w następujący sposób:

![][AllTagsFixedDesktop]

I hello odświeżyć przeglądarkę dla telefonów wygląda następująco: 

![][AllTagsFixed]

> [!NOTE]
> Jeśli zauważysz oryginalnego formatowania listy hello jest nadal istnieje w hello przeglądarkę dla telefonów i zastanawiasz się, jakie wystąpiły tooyour nieuprzywilejowany stylów Bootstrap, to artefaktu wcześniejszych akcji toocreate przenośnych określonych widoków. Jednak teraz, gdy używasz hello Bootstrap CSS framework toocreate projektu sieci web reakcji Przejdź head i usuń te specyficzne dla mobile widoków i hello układ odpowiedni mobile. Po wykonaniu tego hello odświeżyć przeglądarkę dla telefonów wyświetli hello stylów ładowania początkowego.
> 
> 

## <a name="bkmk_improvedates"></a>Poprawa hello listy dat
Można zwiększyć hello *dat* wyświetlania, takich jak zwiększona hello *głośniki* i *tagi* widoków, jeśli używasz hello zmiany kodu opisanego wcześniej, ale przy użyciu następującego hello `Html.ActionLink` składni metody w *widoków\\Home\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

Otrzymasz widoku odświeżyć przeglądarkę dla telefonów następująco:

![][AllDatesFixed]

Można jeszcze bardziej poprawić hello *dat* widoku poprzez organizowanie wartości daty i godziny hello według daty. Można to zrobić z hello Bootstrap [panele] [ panels] style. Zamień zawartość hello hello *widoków\\Home\\AllDates.cshtml* pliku następującym kodem:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Ten kod tworzy oddzielne `<div class="panel panel-primary">` tagu dla każdej różne daty listy hello i używa hello [listy połączonej grupy] [ linked list group] dla odpowiednich łączy jak poprzednio. Oto przeglądarki przenośnych hello wygląda jak po uruchomieniu tego kodu:

![][AllDatesFixed2]

Przeglądarka pulpitu toohello przełącznika. Ponownie należy zwrócić uwagę spójny wygląd hello.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Poprawa hello SessionsTable widoku
W tej sekcji należy podjąć hello *SessionsTable* wyświetlić więcej przyjaznych dla urządzeń przenośnych. Ta zmiana jest bardziej rozległych hello wcześniejszych zmian.

W przeglądarce przenośnych hello, naciśnij przycisk hello **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.

![][AllTagsFixedSearchByASP]

Wybierz hello **ASP.NET** łącza.

![][SessionsTableTagASP.NET]

Jak widać, wyświetlania hello jest formatowana jako tabelę, która jest obecnie zaprojektowanego toobe w przeglądarce pulpitu hello. Jest jednak nieco trudne tooread na przeglądarkę dla telefonów. toofix, otwórz *widoków\\Home\\SessionsTable.cshtml* , a następnie zastąpić hello zawartość pliku hello następującego kodu:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

Kod Hello wykonuje 3 rzeczy:

* używa hello Bootstrap [niestandardowe listy połączonej grupy] [ custom linked list group] tooformat hello w pionie, informacji o sesji, dzięki czemu te informacje są przeznaczone do odczytu w przeglądarce przenośnych (przy użyciu klas takich jak grupy elementu tekst listy)
* stosuje hello [systemu siatki] [ grid system] układu toothe tak sesji hello elementy przepływu w poziomie w przeglądarce pulpitu hello i w pionie w przeglądarce przenośnych hello (przy użyciu hello klasy col-md-4)
* używa hello [reakcji narzędzia] [ responsive utilities] ukrycia znaczników sesji hello podczas wyświetlania w przeglądarce przenośnych hello (przy użyciu klasy ukryte xs hello)

Możesz także wybrać tytuł łącze toogo toohello odpowiednich sesji. Obraz powitania poniżej odzwierciedla hello zmian w kodzie.

![][FixedSessionsByTag]

Witaj siatki ładowania początkowego systemu, który automatycznie zastosować rozmieszcza sesji w pionie w przeglądarce przenośnych hello. Ponadto należy zauważyć, że hello tagi nie są pokazywane. Przeglądarka pulpitu toohello przełącznika.

![][SessionsTableFixedTagASP.NETDesktop]

W przeglądarce dla komputerów hello zauważyć hello tagi są teraz wyświetlane. Ponadto widać, że hello ładowania początkowego siatki system, który można zastosować Rozmieszcza elementy sesji hello w dwóch kolumnach. Powiększenie przeglądarki przekonasz się, że rozmieszczenie hello zmienia toothree kolumn.

## <a name="bkmk_improvesessionbycode"></a>Poprawa hello SessionByCode widoku
Na koniec będzie naprawić hello *SessionByCode* wyświetlić toomake go przyjaznych dla urządzeń przenośnych.

W przeglądarce przenośnych hello, naciśnij przycisk hello **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.

![][AllTagsFixedSearchByASP]

Wybierz hello **ASP.NET** łącza. Sesje tagu ASP.NET hello są wyświetlane.

![][FixedSessionsByTag]

Wybierz hello **tworzenia aplikacji jednej strony ASP.NET i AngularJS** łącza.

![][SessionByCode3-644]

widok pulpitu domyślny Hello działa poprawnie, ale może poprawić wygląd hello łatwo za pomocą niektórych składników Bootstrap graficznego interfejsu użytkownika.

Otwórz *widoków\\Home\\SessionByCode.cshtml* i Zastąp zawartość hello powitania po znaczników:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

Nowy kod znaczników Hello używa Bootstrap paneli Style tooimprove hello widokiem dla urządzeń przenośnych. 

Odśwież przeglądarkę dla telefonów hello. Witaj poniższy obraz odzwierciedla hello zmiany kodu, które zostały wykonane:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Dobiega końca i przejrzyj
Ten samouczek pokazuje, należy jak aplikacji sieci Web toouse ASP.NET MVC 5 toodevelop przyjaznych dla urządzeń przenośnych. Należą do nich:

* Wdrażanie tooan aplikacji ASP.NET MVC 5 aplikacji sieci web usługi aplikacji
* Użyj Bootstrap toocreate układu reakcji strony sieci web w aplikacji MVC 5
* Zastąpienie układu, widoków i widoki częściowe, globalnie i dla poszczególnych widoku
* Układ formantu i częściowy przesłonić przy użyciu wymuszania `RequireConsistentDisplayMode` właściwości
* Utwórz widoki, które odnoszą się do przeglądarki, takich jak przeglądarki iPhone hello
* Zastosuj style Bootstrap w kodzie Razor

## <a name="see-also"></a>Zobacz też
* [9 podstawowe zasady reakcji projektowanie witryn sieci web](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Ładowania początkowego][BootstrapSite]
* [Oficjalny Blog ładowania początkowego][Official Bootstrap Blog]
* [Twitter Bootstrap samouczek z Republika samouczka][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Witaj Plac zabaw dla ładowania początkowego][hello Bootstrap Playground]
* [W3C zalecenie przenośnych sieci Web aplikacji najlepsze rozwiązania][W3C Recommendation Mobile Web Application Best Practices]
* [Zalecenie Candidate W3C zapytaniami multimediów][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[programu Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

