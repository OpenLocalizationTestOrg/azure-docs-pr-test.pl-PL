---
title: "Wdrażanie aplikacji ASP.NET MVC 5 sieci web urządzeń przenośnych w usłudze Azure App Service"
description: "Samouczek, który jest przedstawienie sposobu wdrażania aplikacji sieci web w usłudze Azure App Service przy użyciu funkcji mobilnych w aplikacji sieci web platformy ASP.NET MVC 5."
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
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Wdrażanie aplikacji ASP.NET MVC 5 sieci web urządzeń przenośnych w usłudze Azure App Service
Ten samouczek pokazuje podstawy do tworzenia aplikacji sieci web platformy ASP.NET MVC 5 jest przyjaznych dla urządzeń przenośnych i wdrożyć ją w usłudze Azure App Service. W tym samouczku potrzebne [programu Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] lub programu Visual Studio, jeśli masz już który wersji professional. Można użyć [programu Visual Studio 2015] , ale zrzuty ekranu będzie różna i należy użyć szablonów ASP.NET 4.x.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Jakie będzie kompilacji
W tym samouczku, warto Funkcje mobilne prostą aplikację konferencji listę, która znajduje się w [projektu starter][StarterProject]. Poniższy zrzut ekranu przedstawia sesji platformy ASP.NET w ukończona aplikacja, jak pokazano w emulatorze przeglądarki w narzędziach developer F12 programu Internet Explorer 11.

![][FixedSessionsByTag]

Korzystając z narzędzi deweloperskich programu Internet Explorer 11 F12 i [narzędzie Fiddler] [ Fiddler] do debugowania aplikacji. 

## <a name="skills-youll-learn"></a>Dowiesz się umiejętności
Oto dowiesz się:

* Jak opublikować aplikację sieci web bezpośrednio do aplikacji sieci web w usłudze Azure App Service przy użyciu programu Visual Studio 2013.
* Jak szablony ASP.NET MVC 5 za pomocą architektury CSS Bootstrap zwiększające wyświetlania na urządzeniach przenośnych
* Jak tworzyć widoki specyficzne dla mobile pod kątem określonych przeglądarki dla urządzeń przenośnych, takich jak urządzenia iPhone i Android
* Jak tworzyć widoki dynamiczne (widoki, które odpowiadają na różnych przeglądarkach różnych urządzeń)

## <a name="set-up-the-development-environment"></a>Konfigurowanie środowiska deweloperskiego
Konfigurowanie środowiska programowania przez zainstalowanie zestawu Azure SDK dla platformy .NET 2.5.1 lub nowszej. 

1. Aby zainstalować zestaw Azure SDK dla platformy .NET, kliknij poniższe łącze. Jeśli nie masz jeszcze zainstalowany program Visual Studio 2013, zostanie zainstalowany przez to łącze. Ten samouczek wymaga programu Visual Studio 2013. [Zestaw Azure SDK dla programu Visual Studio 2013][AzureSDKVs2013]
2. W oknie Instalatora platformy sieci Web kliknij **zainstalować** i kontynuować instalację.

Należy również emulatora przeglądarkę dla telefonów. Działa jedną z następujących czynności:

* Emulator przeglądarki w [narzędzi deweloperskich programu Internet Explorer 11 F12] [ EmulatorIE11] (używane na wszystkich przeglądarkę dla telefonów zrzutach ekranu). Ma ona predefiniowane ciąg agenta użytkownika dla systemu Windows Phone 8, Windows Phone 7 i iPad firmy Apple.
* Emulator przeglądarki w [DevTools Google Chrome][EmulatorChrome]. Zawiera ustawienia dla wielu urządzeń z systemem Android, a także Apple iPhone, iPad firmy Apple oraz Amazon Kindle Fire. Emuluje on również zdarzenia touch.
* [Opera emulatorze przenośnym][EmulatorOpera]

Projekty Visual Studio z C\# kodu źródłowego są dostępne powiązany z tym tematem:

* [Początkowy projektem do pobrania][StarterProject]
* [Pobranie projektu zakończone][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Wdrażanie projektu początkową aplikację sieci web platformy Azure
1. Pobierz aplikację listy konferencji [projektu starter][StarterProject].
2. Następnie w Eksploratorze Windows, kliknij prawym przyciskiem myszy pobrany plik ZIP i wybierz *właściwości*.
3. W **właściwości** oknie dialogowym wybierz **Odblokuj** przycisku. (Odblokowywania uniemożliwia ostrzeżenie występuje, gdy użytkownik próbuje użyć *.zip* pliku pobranym z sieci web.)
4. Kliknij prawym przyciskiem myszy plik ZIP, a następnie wybierz **Wyodrębnij wszystkie** aby rozpakować plik. 
5. W programie Visual Studio Otwórz *C#\Mvc5Mobile.sln* pliku.
6. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i kliknij przycisk **publikowania**.
   
   ![][DeployClickPublish]
7. Na publikowanie w sieci Web, kliknij **Microsoft Azure App Service**.
   
   ![][DeployClickWebSites]
8. Jeśli jeszcze nie zostało to jeszcze zalogowania na platformie Azure, kliknij przycisk **Dodaj konto**.
   
   ![][DeploySignIn]
9. Postępuj zgodnie z monitami, aby zalogować się do konta platformy Azure.
10. Usługi aplikacji — okno dialogowe powinna zostać wyświetlona zostanie jako zalogowany. Kliknij przycisk **Nowy**.
    
    ![][DeployNewWebsite]  
11. W **Nazwa aplikacji sieci Web** określ prefiks nazwy aplikacji unikatowy. Twoje Pełna nazwa aplikacji sieci web będzie  *&lt;prefiks >*. azurewebsites.net. Ponadto wybierz lub określ nazwę nowej grupy zasobów w **grupy zasobów**. Następnie kliknij przycisk **nowy** Aby utworzyć nowy plan usługi aplikacji.
    
    ![][DeploySiteSettings]
12. Skonfiguruj nowy plan usługi aplikacji, a następnie kliknij przycisk **OK**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. W oknie dialogowym Tworzenie usługi App Service kliknij **Utwórz**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Po Azure zasoby są tworzone, publikowanie w sieci Web okna dialogowego zostaną wypełnione przy użyciu ustawień dla nowej aplikacji. Kliknij przycisk **Opublikuj**.
    
    ![][DeployPublishSite]
    
    Gdy program Visual Studio zakończy publikowanie projektu starter do aplikacji sieci web platformy Azure, pulpitu przeglądarce zostanie otwarty do wyświetlenia aplikacji sieci web na żywo.
15. Uruchom z emulatora przeglądarkę dla telefonów, skopiuj adres URL dla aplikacji konferencji (*<prefix>*. azurewebsites.net) w emulatorze, a następnie kliknij przycisk prawym górnym rogu i wybierz **Przeglądaj według znaczników**. Jeśli korzystasz z programu Internet Explorer 11 jako domyślnej przeglądarki, wystarczy wpisać `F12`, następnie `Ctrl+8`, a następnie zmień profilu przeglądarki, aby **Windows Phone**. Obraz poniżej przedstawia *alltags —* widok w trybie portret (wybór **Przeglądaj według znaczników**).
    
    ![][AllTags]

> [!TIP]
> Podczas można debugować aplikacji MVC 5 z poziomu programu Visual Studio, możesz opublikować aplikację sieci web Azure ponownie, aby zweryfikować aplikacji sieci web bezpośrednio w przeglądarce przenośnych lub w emulatorze przeglądarki.
> 
> 

Ekran jest bardzo do odczytu na urządzeniu przenośnym. Można także już widoczne niektóre efekty wizualne zastosowane przez platformę Bootstrap CSS.
Kliknij przycisk **ASP.NET** łącza.

![][SessionsByTagASP.NET]

Widok znaczników ASP.NET jest zainstalowane powiększenia do ekranu, która obsługuje można automatycznie ładowania początkowego. Jednak może poprawić ten widok, aby lepiej dopasować przenośnych przeglądarki. Na przykład **data** kolumna jest trudny do odczytania. W dalszej części tego samouczka zostanie zmieniona *alltags —* widok, aby była przyjaznych dla urządzeń przenośnych.

## <a name="bkmk_bootstrap"></a>Framework bootstrap CSS
Nowe MVC 5 szablon jest wbudowana obsługa ładowania początkowego. Ma już widoczny, jak od razu zwiększa różne widoki w aplikacji. Na przykład pasek nawigacyjny u góry jest zwijany automatycznie, gdy szerokość przeglądarki jest mniejsza. W przeglądarce pulpitu należy spróbować zmienić rozmiar okna przeglądarki i zobacz, jak na pasku nawigacyjnym zmienia jego wygląd i działanie. Jest to projekt dynamiczne sieci web, który jest wbudowany w ładowania początkowego.

Aby zobaczyć, jak będzie wyglądać aplikacji sieci Web bez ładowania początkowego, otwórz *aplikacji\_Start\\BundleConfig.cs* ujmij w komentarz wierszy, które zawierają *bootstrap.js* i  *bootstrap.CSS*. Poniższy kod przedstawia dwa ostatnie instrukcje `RegisterBundles` metody po zmianie:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Naciśnij klawisz `Ctrl+F5` do uruchomienia aplikacji.

Sprawdź na pasku nawigacyjnym zwijanej jest teraz wystarczy zwykłe nieuporządkowaną listę. Kliknij przycisk **Przeglądaj według znaczników** ponownie, następnie kliknij przycisk **ASP.NET**.
W widoku emulatorze przenośnym widać, nie jest już zainstalowane powiększenia do ekranu i musieli przewijać bok aby zobaczyć prawej tabeli.

![][SessionsByTagASP.NETNoBootstrap]

Cofnij zmiany i odświeżyć przeglądarkę przenośnych, aby sprawdzić, czy wyświetlana przyjazna została przywrócona.

Ładowania początkowego nie jest specyficzne dla platformy ASP.NET MVC 5, a w dowolnej aplikacji sieci web mogą korzystać z tych funkcji. Ale teraz są wbudowane w szablon projektu programu ASP.NET MVC 5, dzięki czemu aplikacja sieci MVC 5 Web można korzystać z Bootstrap domyślnie.

Aby uzyskać więcej informacji na temat ładowania początkowego, przejdź do [Bootstrap] [ BootstrapSite] lokacji.

W następnej sekcji pojawi się, jak zapewnić konkretnych widoków mobile przeglądarki.

## <a name="bkmk_overrideviews"></a>Zastąpienie widoki, układów i widoki częściowe
Można zastąpić dowolnym widoku (w tym układy i widoki częściowe) dla przeglądarki dla urządzeń przenośnych ogólnie rzecz biorąc, poszczególne przeglądarkę dla telefonów lub dowolnej przeglądarki określone. W celu zapewnienia przeglądu specyficzne dla mobilnych, skopiuj plik widoku i Dodaj *. Mobile* do nazwy pliku. Na przykład, aby utworzyć przenośnym *indeksu* widoku, możesz skopiować *widoków\\Home\\Index.cshtml* do *widoków\\Home\\ Index.Mobile.cshtml*.

W tej sekcji utworzysz plik układu specyficzne dla mobilnych.

Aby rozpocząć, skopiuj *widoków\\Shared\\\_Layout.cshtml* do *widoków\\Shared\\\_Layout.Mobile.cshtml*. Otwórz  *\_Layout.Mobile.cshtml* i Zmień tytuł z **aplikacji MVC5** do **MVC5 aplikacji (Mobile)**.

W każdym `Html.ActionLink` wymagać pasku nawigacyjnym, Usuń "Przeglądaj według", w każdym odnośniku *ActionLink*. Poniższy kod przedstawia ukończonej `<ul class="nav navbar-nav">` tag pliku przenośnych układu.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Kopiuj *widoków\\Home\\AllTags.cshtml* pliku na *widoków\\Home\\AllTags.Mobile.cshtml*. Otwórz nowy plik i zmień `<h2>` element na podstawie "Tagi" do "tagi (M)":

    <h2>Tags (M)</h2>

Przejdź do strony tagów za pomocą przeglądarki pulpitu i przy użyciu emulatora przeglądarkę dla telefonów. Emulator przeglądarkę dla telefonów zawiera dwie zmiany (tytuł z  *\_Layout.Mobile.cshtml* i tytuł z *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Z kolei Monitor nie zmienił się (tytułów z  *\_Layout.cshtml* i *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a>Utwórz widoki specyficzne dla przeglądarki
Oprócz mobile dotyczące pulpitu i widoki można tworzyć widoki dla poszczególnych przeglądarki. Na przykład można tworzyć widoki, które są przeznaczone dla telefonów iPhone lub przeglądarki systemu Android. W tej sekcji utworzysz układu dla przeglądarki iPhone i wersji iPhone *alltags —* widoku.

Otwórz *Global.asax* pliku i Dodaj następujący kod do dołu `Application_Start` metody.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Ten kod definiuje nowy tryb wyświetlania o nazwie "iPhone" pasujących względem każdego żądania przychodzącego. Jeśli żądanie przychodzące odpowiada warunku, zdefiniowane przez użytkownika (jeśli agent użytkownika zawiera ciąg "iPhone"), platformy ASP.NET MVC sprawdza widoki, których nazwa zawiera sufiksu "iPhone".

> [!NOTE]
> Podczas dodawania trybów wyświetlania przeglądarki dotyczące przenośnych, takie jak w przypadku telefonów iPhone i Android, upewnij się ustawić pierwszy argument `0` (Wstaw na początku listy) aby upewnić się, tryb specyficzne dla przeglądarki ma pierwszeństwo przed przenośnych szablonu (*. Mobile.cshtml). Jeśli szablon przenośnych jest na początku listy, zostanie wybrany na tryb wyświetlania zamierzone (pierwszy wins dopasowania i przenośnych szablonu dopasowuje wszystkie przeglądarki dla urządzeń przenośnych). 
> 
> 

W kodzie, kliknij prawym przyciskiem myszy `DefaultDisplayMode`, wybierz **rozwiązać**, a następnie wybierz pozycję `using System.Web.WebPages;`. Spowoduje to dodanie odwołania do `System.Web.WebPages` przestrzeni nazw, czyli gdzie `DisplayModeProvider` i `DefaultDisplayMode` typy zostały zdefiniowane.

![][ResolveDefaultDisplayMode]

Alternatywnie można po prostu ręcznie dodaj następujący wiersz do `using` sekcji pliku.

    using System.Web.WebPages;

Zapisz zmiany. Kopia *widoków\\Shared\\\_Layout.Mobile.cshtml* pliku na *widoków\\współużytkowane\\\_Layout.iPhone.cshtml*. Otwórz nowy plik, a następnie zmień tytuł z `MVC5 Application (Mobile)` do `MVC5 Application (iPhone)`.

Kopiuj *widoków\\Home\\AllTags.Mobile.cshtml* pliku na *widoków\\Home\\AllTags.iPhone.cshtml*. W nowym pliku zmienić `<h2>` element z "tagi (M)" do "Tagów (iPhone)".

Uruchom aplikację. Uruchamianie emulatora przeglądarkę dla telefonów, upewnij się, że jego agenta użytkownika ma ustawioną wartość "iPhone" i przejdź do *alltags —* widoku. Jeśli używasz emulatora w narzędzi deweloperskich programu Internet Explorer 11 naciśnięcia klawisza F12, Konfiguracja funkcji emulacji do następującego:

* Profil przeglądarki = **Windows Phone**
* Ciąg agenta użytkownika = **niestandardowe**
* Niestandardowy ciąg = **Apple-iPhone5C1/1001.525**

Poniższy zrzut ekranu przedstawia *alltags —* widok renderowany w emulatorze w narzędzi deweloperskich programu Internet Explorer 11 F12 z niestandardowy ciąg agenta użytkownika (jest to ciąg agenta użytkownika iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

W przeglądarce przenośnym, wybierz **głośniki** łącza. Ponieważ nie jest widokiem dla urządzeń przenośnych (*AllSpeakers.Mobile.cshtml*), wyświetlanie głośniki domyślne (*AllSpeakers.cshtml*) jest renderowany przy użyciu widoku układu przenośnych ( *\_ Layout.Mobile.cshtml*). Jak pokazano poniżej, tytuł **MVC5 aplikacji (Mobile)** jest zdefiniowany w  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Widok domyślny (nieprzenośnych) z renderowania w układzie przenośnych globalnie można wyłączyć, ustawiając `RequireConsistentDisplayMode` do `true` w *widoków\\\_ViewStart.cshtml* pliku następująco:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Gdy `RequireConsistentDisplayMode` ma ustawioną wartość `true`, przenośnych układu (*\_Layout.Mobile.cshtml*) jest używany tylko dla widoków przenośnych (tj. gdy plik widok jest w formie  ***ViewName**. Mobile.cshtml*). Należy ustawić `RequireConsistentDisplayMode` do `true` Jeśli przenośnych układu nie działa prawidłowo w przypadku widoków przeznaczone dla urządzeń przenośnych. Zrzut ekranu poniżej przedstawiono sposób *głośniki* renderowania strony, gdy `RequireConsistentDisplayMode` ma ustawioną wartość `true` (bez ciąg "(wersja Mobile)" na pasku nawigacji u góry).

![][AllSpeakers_LayoutMobileOverridden]

Spójnego trybu wyświetlania w określonym widoku można wyłączyć, ustawiając `RequireConsistentDisplayMode` do `false` w pliku widoku. Następujący kod w *widoków\\Home\\AllSpeakers.cshtml* plików zestawów `RequireConsistentDisplayMode` do `false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

W tej sekcji możemy przedstawiono sposób tworzenia widoków i układy przenośnych oraz sposobu tworzenia widoków dla konkretnych urządzeń, takich jak telefonów iPhone i układów.
Główną zaletą framework CSS ładowania początkowego jest jednak elastyczny układ, co oznacza, że jednego arkusza stylów mogą być stosowane przez pulpitu, telefon i tablet przeglądarki do utworzenia spójny wygląd i zachowanie. W następnej sekcji pojawi się, jak wykorzystać ładowania początkowego tworzenia widoków przyjaznych dla urządzeń przenośnych.

## <a name="bkmk_Improvespeakerslist"></a>Poprawa listy głośniki
Jak został wyświetlony, *głośniki* widoku jest możliwy do odczytu, ale łącza są małe i są trudne do naciśnij na urządzeniu przenośnym. W tej sekcji należy podjąć *AllSpeakers* wyświetlić przyjaznych dla urządzeń przenośnych, który wyświetla dużych, łatwe wybranie łącza i zawiera pole wyszukiwania, aby szybko znaleźć głośniki.

Można użyć ładowania początkowego programu [listy połączonej grupy] [ linked list group] stylów zwiększające *głośniki* widoku. W *widoków\\Home\\AllSpeakers.cshtml*, Zastąp zawartość pliku Razor przy użyciu poniższego kodu.

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

`class="list-group"` Atrybutu w `<div>` znacznik stosuje style Bootstrap listy i `class="input-group-item"` atrybut dotyczy stylów elementu listy Bootstrap każdego łącza.

Odśwież przeglądarkę dla telefonów. Widok zaktualizowanej wygląda następująco:

![][AllSpeakersFixed]

Ładowania początkowego programu [listy połączonej grupy] [ linked list group] stylów sprawia, że całe okno dla każdego łącza, które są aktywne, czyli znacznie lepsze środowisko użytkownika. Przełącz do widoku pulpitu i obserwować spójny wygląd i zachowanie.

![][AllSpeakersFixedDesktop]

Chociaż widoku przeglądarkę dla telefonów została ulepszona i jest trudno długą listę głośniki. Ładowania początkowego nie zapewnia wyszukiwania filtr funkcji out-of box, ale można go dodać przy użyciu kilku wierszy kodu. Należy najpierw dodać pole wyszukiwania do widoku, a następnie podłączanie z kodu JavaScript dla funkcji filtru. W *widoków\\Home\\AllSpeakers.cshtml*, Dodaj \<formularza\> tuż po tagu \<h2\> tagów, jak pokazano poniżej:

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

Zwróć uwagę, że `<form>` i `<input>` tagi zarówno ma ładowania początkowego stylów zastosowanych do nich. `<span>` Element dodaje Bootstrap [glyphicon] [ glyphicon] do pola wyszukiwania.

W *skryptów* folderu, Dodaj plik JavaScript o nazwie *filter.js*. Otwórz plik i Wklej do niego następujący kod:

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
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

Należy również uwzględnić filter.js w Twojej zarejestrowanych pakietów. Otwórz *aplikacji\_Start\\BundleConfig.cs* i Zmień pierwszy pakietów. Zmień pierwsze `bundles.Add` instrukcji (dla **jquery** pakietu) do uwzględnienia *skryptów\\filter.js*w następujący sposób:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

**Jquery** pakietu jest już renderowana przez domyślny  *\_układu* widoku. Później możesz użyć tego samego kodu JavaScript do zastosowania funkcji filtrowania z innymi widokami listy.

Odśwież przeglądarkę dla telefonów i przejdź do *AllSpeakers* widoku. W polu wyszukiwania wpisz "sc". Na liście głośniki teraz powinny być filtrowane według ciąg wyszukiwania.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Poprawa listy tagów
Podobnie jak *głośniki* widoku *tagi* widoku jest możliwy do odczytu, ale łącza są małe i trudne do naciśnij na urządzeniu przenośnym. Problem można rozwiązać *tagi* wyświetlać ten sam sposób, w rozwiązaniu *głośniki* wyświetlić, korzystając z opisanych wcześniej, ale z następującymi zmian w kodzie `Html.ActionLink` składni metody w *widoków\\ Strona główna\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Odświeżyć przeglądarkę dla komputerów wygląda następująco:

![][AllTagsFixedDesktop]

I odświeżyć przeglądarkę dla telefonów wygląda następująco: 

![][AllTagsFixed]

> [!NOTE]
> Jeśli zauważysz, że oryginalne formatowanie listy nadal znajduje się w przeglądarce przenośnych i zastanawiasz się, co się stało z nieuprzywilejowany Bootstrap związanych ze stylami, to artefaktu użytkownika wcześniejszą akcję w celu utworzenia przenośnych konkretnych widoków. Jednak teraz, aby utworzyć projekt sieci web reakcji przy użyciu framework Bootstrap CSS Przejdź head i usuń te widoki specyficzne dla mobilnych i widoki specyficzne dla mobile układu. Po wykonaniu czynności odświeżyć przeglądarkę dla telefonów wyświetli Bootstrap style.
> 
> 

## <a name="bkmk_improvedates"></a>Poprawa listy dat
Można zwiększyć *dat* wyświetlania, takich jak zwiększona możesz *głośniki* i *tagi* widoków, jeśli używasz zmiany kodu opisanego wcześniej, ale z następującymi `Html.ActionLink` Składnia metody w *widoków\\Home\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

Otrzymasz widoku odświeżyć przeglądarkę dla telefonów następująco:

![][AllDatesFixed]

Można jeszcze bardziej poprawić *dat* widoku poprzez organizowanie wartości daty i godziny według daty. Można to zrobić z ładowania początkowego programu [panele] [ panels] style. Zastąp zawartość *widoków\\Home\\AllDates.cshtml* pliku następującym kodem:

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

Ten kod tworzy oddzielne `<div class="panel panel-primary">` tagu dla każdej różne daty na liście i używa [listy połączonej grupy] [ linked list group] dla odpowiednich łączy jak poprzednio. Oto przeglądarkę dla telefonów wygląd po uruchomieniu tego kodu:

![][AllDatesFixed2]

Przełącz się do pulpitów przeglądarki. Ponownie należy zwrócić uwagę spójny wygląd.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Poprawa widoku SessionsTable
W tej sekcji należy podjąć *SessionsTable* wyświetlić więcej przyjaznych dla urządzeń przenośnych. Ta zmiana jest bardziej rozległych wcześniejszych zmian.

W przeglądarce przenośnym, wybierz **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.

![][AllTagsFixedSearchByASP]

Wybierz **ASP.NET** łącza.

![][SessionsTableTagASP.NET]

Jak widać, ekran jest w formacie tabeli, która obecnie jest przeznaczony do wyświetlania w przeglądarce pulpitu. Jednak nieco trudno jest do odczytu w przeglądarce przenośnych. Aby rozwiązać ten problem, otwórz *widoków\\Home\\SessionsTable.cshtml* i Zastąp zawartość pliku następującym kodem:

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

Kod wykonuje 3 rzeczy:

* używa ładowania początkowego programu [niestandardowe listy połączonej grupy] [ custom linked list group] sformatować informacji o sesji w pionie, tak aby te informacje są przeznaczone do odczytu w przeglądarce przenośnych (przy użyciu klas, takie jak listy grupy elementu tekst)
* stosuje [systemu siatki] [ grid system] do układu, tak aby elementy sesji poziomie przepływu w przeglądarce dla komputerów i w pionie w przeglądarce przenośnych (przy użyciu klasy col-md-4)
* używa [reakcji narzędzia] [ responsive utilities] ukrycia znaczników sesji podczas wyświetlania w przeglądarce przenośnych (przy użyciu klasy xs ukryte)

Można również wybrać link tytuł można przejść do odpowiedniej sesji. Na poniższym obrazie odzwierciedla zmiany kodu.

![][FixedSessionsByTag]

System ładowania początkowego siatki, który automatycznie zastosować rozmieszcza sesji w pionie w przeglądarce przenośnych. Zauważ również, że tagi nie są pokazywane. Przełącz się do pulpitów przeglądarki.

![][SessionsTableFixedTagASP.NETDesktop]

W przeglądarce pulpitu Zwróć uwagę, znaczniki są teraz wyświetlane. Ponadto widać, że system ładowania początkowego siatki zastosowane Rozmieszcza elementy sesji w dwóch kolumnach. Powiększenie przeglądarki, zobaczysz, że rozmieszczenia zmienia się na trzy kolumny.

## <a name="bkmk_improvesessionbycode"></a>Poprawa widoku SessionByCode
Na koniec będzie naprawić *SessionByCode* widok, aby była przyjaznych dla urządzeń przenośnych.

W przeglądarce przenośnym, wybierz **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.

![][AllTagsFixedSearchByASP]

Wybierz **ASP.NET** łącza. Sesje dla tagu ASP.NET są wyświetlane.

![][FixedSessionsByTag]

Wybierz **tworzenia aplikacji jednej strony ASP.NET i AngularJS** łącza.

![][SessionByCode3-644]

Domyślny widok pulpitu działa poprawnie, ale może poprawić wygląd łatwo za pomocą niektórych składników Bootstrap graficznego interfejsu użytkownika.

Otwórz *widoków\\Home\\SessionByCode.cshtml* i Zastąp zawartość następujący kod:

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

Znaczników nowej używa Bootstrap paneli Style zwiększające widokiem dla urządzeń przenośnych. 

Odśwież przeglądarkę dla telefonów. Poniższa ilustracja odzwierciedla zmiany kodu, które zostały wykonane:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Dobiega końca i przejrzyj
W tym samouczku ma pokazano, jak używać programu ASP.NET MVC 5 do tworzenia aplikacji sieci Web przyjaznych dla urządzeń przenośnych. Należą do nich:

* Wdrażanie aplikacji ASP.NET MVC 5 do aplikacji sieci web usługi aplikacji
* Użyj Bootstrap, aby utworzyć układ dynamiczne sieci web w aplikacji MVC 5
* Zastąpienie układu, widoków i widoki częściowe, globalnie i dla poszczególnych widoku
* Układ formantu i częściowy przesłonić przy użyciu wymuszania `RequireConsistentDisplayMode` właściwości
* Utwórz widoki, które odnoszą się do przeglądarki, takich jak przeglądarki iPhone
* Zastosuj style Bootstrap w kodzie Razor

## <a name="see-also"></a>Zobacz też
* [9 podstawowe zasady reakcji projektowanie witryn sieci web](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Ładowania początkowego][BootstrapSite]
* [Oficjalny Blog ładowania początkowego][Official Bootstrap Blog]
* [Twitter Bootstrap samouczek z Republika samouczka][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Bootstrap Plac zabaw dla][The Bootstrap Playground]
* [W3C zalecenie przenośnych sieci Web aplikacji najlepsze rozwiązania][W3C Recommendation Mobile Web Application Best Practices]
* [Zalecenie Candidate W3C zapytaniami multimediów][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

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
[The Bootstrap Playground]: http://www.bootply.com/
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

