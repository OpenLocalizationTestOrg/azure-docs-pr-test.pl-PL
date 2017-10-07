---
title: "toowork aaaHow z serwera wewnętrznej bazy danych hello Node.js SDK for Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toowork z hello serwera zaplecza Node.js SDK dla usługi Azure App Service Mobile Apps."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Jak toouse hello Azure Mobile Apps Node.js SDK
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Ten artykuł zawiera szczegółowe informacje i przykłady przedstawiający sposób toowork z zaplecza Node.js w usłudze Azure App Service Mobile Apps.

## <a name="Introduction"></a>Wprowadzenie
Usługa Azure App Service Mobile Apps udostępnia hello możliwości tooadd mobile zoptymalizowane danych aplikacji sieci web tooa interfejsu API sieci Web.  Witaj zestaw SDK aplikacji mobilnych usługi aplikacji Azure jest dostępna dla aplikacji sieci web ASP.NET i Node.js.  Witaj SDK udostępnia hello następujące operacje:

* Operacje tabeli (Odczyt, Insert, Update, Delete) dla dostępu do danych
* Operacje niestandardowego interfejsu API

Obie operacje zapewnienia uwierzytelniania przez wszystkich dostawców tożsamości dozwolone w usłudze Azure App Service, w tym dostawców tożsamości społecznościowych, takich jak Facebook, Twitter, Google i Microsoft, jak również usługi Azure Active Directory dla tożsamości organizacji.

Można znaleźć przykłady dla każdego przypadku użycia w hello [katalogu przykładów w witrynie GitHub].

## <a name="supported-platforms"></a>Obsługiwane platformy
Witaj zestaw SDK usługi Azure Mobile Apps węzła obsługuje powitalne wersji LTS bieżącego węzła i nowszych.  Począwszy od zapisu, najnowsza wersja LTS hello jest v4.5.0 węzła.  Inne wersje węzeł może działać, ale nie są obsługiwane.

zestaw SDK usługi Azure Mobile Apps węzła Hello obsługuje dwa sterowniki bazy danych — hello mssql węzła sterownik obsługuje SQL Azure i lokalnego wystąpienia programu SQL Server.  Sterownik sqlite3 Hello obsługuje bazy danych SQLite na tylko jedno wystąpienie.

### <a name="howto-cmdline-basicapp"></a>Porady: tworzenie przy użyciu wiersza polecenia hello zaplecza Node.js podstawowe
Jako aplikacja ExpressJS rozpoczyna się co wewnętrznej bazy danych usługi Azure App Service Mobile aplikacji Node.js.  ExpressJS jest hello najpopularniejszych platforma sieci web usługi dostępne dla środowiska Node.js.  Można utworzyć basic [Express] aplikacji w następujący sposób:

1. Polecenie lub oknie programu PowerShell należy utworzyć katalog w projekcie.

        mkdir basicapp
2. Uruchom npm init tooinitialize hello pakietu struktury.

        cd basicapp
        npm init

    polecenie init npm Hello zapyta zestaw pytań tooinitialize hello projektu.  Zobacz hello przykładowe dane wyjściowe:

    ![Witaj npm init w danych wyjściowych][0]
3. Zainstaluj biblioteki hello express i aplikacje w przypadku mobilne platformy azure z repozytorium npm hello.

        npm install --save express azure-mobile-apps
4. Tworzenie app.js tooimplement hello podstawowe przenośnych serwera plików.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Ta aplikacja tworzy zoptymalizowanych pod kątem mobile WebAPI z jednym punktem końcowym (`/tables/TodoItem`) zapewnia tooan nieuwierzytelnionym dostępem jest podstawowy magazyn danych SQL przy użyciu dynamicznych schematu.  Jest ona odpowiednia dla następującego Szybki Start biblioteki klienta:

* [Szybki Start kliencką dla systemu android]
* [Apache Cordova klienta — Szybki Start]
* [iOS — Szybki Start klienta]
* [Szybki Start klienta Sklepu Windows]
* [Szybki Start klienta platformy Xamarin.iOS]
* [Szybki Start klienta platformy Xamarin.Android]
* [Szybki Start klienta platformy Xamarin.Forms]

Dla tej aplikacji w warstwie podstawowa w hello można znaleźć kod hello [basicapp przykładem w witrynie GitHub].

### <a name="howto-vs2015-basicapp"></a>Porady: tworzenie zaplecza węzła z programem Visual Studio 2015
Visual Studio 2015 wymaga rozszerzenia toodevelop Node.js aplikacji w obrębie hello IDE.  toostart, zainstaluj hello [Node.js Tools 1.1 dla programu Visual Studio].  Po zainstalowaniu hello Node.js Tools for Visual Studio tworzy aplikację 4.x Express:

1. Otwórz hello **nowy projekt** okna dialogowego (z **pliku** > **nowy** > **projektu...** ).
2. Rozwiń węzeł **szablony** > **JavaScript** > **Node.js**.
3. Wybierz hello **Azure Node.js Express 4 aplikacji w warstwie podstawowa**.
4. Wprowadź nazwę projektu hello.  Kliknij przycisk *OK*.

    ![Nowy projekt programu Visual Studio 2015][1]
5. Kliknij prawym przyciskiem myszy hello **npm** a następnie wybierz węzeł **zainstalować nowych pakietów npm...** .
6. Może być konieczne toorefresh hello npm katalogu na tworzenie pierwszej aplikacji Node.js.  Kliknij przycisk **Odśwież** w razie potrzeby.
7. Wprowadź *apps w usłudze azure-mobile* hello pola wyszukiwania.  Kliknij przycisk hello **usługi azure mobile apps 2.0.0** pakietu, a następnie kliknij przycisk **zainstaluj pakiet**.

    ![Zainstaluj nowych pakietów npm][2]
8. Kliknij przycisk **Zamknij**.
9. Otwórz hello *app.js* pliku tooadd obsługę hello Azure Mobile Apps SDK.  U dołu hello 6 at wiersza biblioteki hello wymagają instrukcje, Dodaj hello następującego kodu:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    W wierszu około 27 po hello inne instrukcje app.use Dodaj hello następującego kodu:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Zapisz plik hello.
10. Uruchom lokalnie aplikacji hello (powitalne interfejsu API jest obsługiwana na http://localhost: 3000) lub opublikować tooAzure.

### <a name="create-node-backend-portal"></a>Porady: tworzenie zaplecza Node.js przy użyciu hello portalu Azure
Możesz utworzyć prawo zaplecza aplikacji mobilnej w hello [portalu Azure]. Można albo wykonaj hello następujące kroki albo utwórz klienta i serwera razem po hello [tworzenie aplikacji mobilnej](app-service-mobile-ios-get-started.md) samouczka. Samouczek Hello zawiera uproszczonej wersji tych instrukcji i najlepiej stosować do weryfikacji koncepcji projektów.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Po powrocie do hello *wprowadzenie* bloku, w obszarze **Utwórz tabelę interfejsu API**, wybierz **Node.js** jako z **język wewnętrznej bazy danych**.
Sprawdź pola hello "**potwierdzam, że spowoduje to zastąpienie wszystkich lokacji zawartości.**", następnie kliknij przycisk **Utwórz tabelę TodoItem**.

### <a name="download-quickstart"></a>Porady: pobieranie hello Node.js zaplecza projekt szybkiego startu kodu przy użyciu narzędzia Git
Po utworzeniu zaplecza aplikacji mobilnej Node.js przy użyciu portalu hello **szybki start** bloku, tworzony jest projekt środowiska Node.js i wdrożone tooyour lokacji. Można dodać tabele i interfejsów API i edytować pliki kodu dla zaplecza Node.js hello w portalu hello. Umożliwia także różne wdrażania narzędzia toodownload hello wewnętrznej bazy danych projektu tak, aby można dodać lub zmodyfikować tabele i interfejsów API, a następnie ponownie opublikować hello projektu. Aby uzyskać więcej informacji, zobacz [Azure App Service Deployment Guide]. Witaj poniższej procedurze używana jest kod projektu szybkiego startu hello toodownload Git repozytorium.

1. Zainstaluj usługę Git, jeśli jeszcze tego nie zrobiono. tooinstall wymagane kroki Hello Git różnią się między systemami operacyjnymi. Zobacz [instalowanie Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) dystrybucje systemu operacyjnego i instalacji.
2. Wykonaj kroki hello w [hello Włącz repozytorium aplikacji usługi App Service](../app-service-web/app-service-deploy-local-git.md#Step3) repozytorium Git hello tooenable dla witryny sieci wewnętrznej bazy danych, co wiadomości powitania wdrożenia użytkownika i hasło.
3. W bloku hello zaplecza aplikacji mobilnej, zanotuj hello **adres URL klonowania Git** ustawienie.
4. Wykonanie hello `git clone` polecenia przy użyciu hello adres URL klonowania Git, wprowadzania hasła, gdy jest to wymagane, jak w poniższym przykładzie:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Przeglądaj toolocal w hello poprzedzających przykładzie jest to katalog /todolist i zwróć uwagę, że pliki projektu zostały pobrane. Zlokalizuj hello `todoitem.json` pliku w hello `/tables` katalogu.  Ten plik definiuje uprawnienia w tabeli.  Również znaleźć hello `todoitem.js` w pliku hello sam katalog, który określa, że operacji CRUD skrypty hello tabeli.
6. Po dokonaniu zmiany tooproject pliki, wykonaj hello następujące polecenia tooadd, zatwierdzić, a następnie przekaż lokacji toohello zmiany:

        $ git commit -m "updated hello table script"
        $ git push origin master

    Po dodaniu nowego projektu toohello plików, należy najpierw tooexecute hello `git add .` polecenia.

opublikowaniu lokacji Hello za każdym razem, gdy nowy zestaw zatwierdzeń spoczywa toohello lokacji.

### <a name="howto-publish-to-azure"></a>Porady: publikowanie programu tooAzure zaplecza Node.js
Microsoft Azure udostępnia wiele mechanizmów publikowania zaplecza Azure App Service Mobile aplikacji Node.js do hello usługi Azure.  Obejmują one przy użyciu narzędzia wdrażania zintegrowane w programie Visual Studio, narzędzia wiersza polecenia i opcje ciągłego wdrażania w oparciu o kontroli źródła.  Aby uzyskać więcej informacji na ten temat, zobacz [Azure App Service Deployment Guide].

Usługa aplikacji Azure ma poradę należy zapoznać się przed przystąpieniem do wdrażania aplikacji Node.js:

* Jak zbyt[Określ hello wersji węzła]
* Jak zbyt[Użyj modułów węzła]

### <a name="howto-enable-homepage"></a>Porady: Włączanie strony głównej aplikacji
Wiele aplikacji są kombinacją sieci web i aplikacji mobilnych i hello ExpressJS framework umożliwia toocombine dwa aspekty.  Czasami jednak warto zapoznać się z tooonly implementacji interfejsu dla urządzeń przenośnych.  Jest przydatne tooprovide, którą usługą aplikacji docelowej strony tooensure hello jest uruchomiona.  Można podać strony głównej lub włączyć tymczasowe strony głównej.  tooenable tymczasowe strony głównej, użyj powitania po tooinstantiate Azure Mobile Apps:

    var mobile = azureMobileApps({ homePage: true });

Jeśli mają tylko tej opcji, które są dostępne podczas tworzenia lokalnie, możesz dodać tooyour to ustawienie `azureMobile.js` pliku.

## <a name="TableOperations"></a>Operacje tabeli
Hello azure-mobile aplikacji Node.js Server SDK udostępnia mechanizmy tooexpose dane przechowywane w bazie danych SQL Azure jako WebAPI tabel.  Podano pięć operacji.

| Operacja | Opis |
| --- | --- |
| GET /tables/*tablename* |Pobierz wszystkie rekordy w tabeli hello |
| GET /tables/*tablename*/:id |Pobierz określonego rekordu w tabeli hello |
| POST /tables/*tablename* |Utwórz rekord tabeli hello |
| POPRAWKA /tables/*tablename*/:id |Aktualizacja rekordu w tabeli hello |
| Usuń /tables/*tablename*/:id |Usuwanie rekordu w tabeli hello |

Obsługuje ten WebAPI [OData] i rozszerza toosupport schematu tabeli hello [synchronizacji danych w trybie offline].

### <a name="howto-dynamicschema"></a>Porady: Definiowanie tabel za pomocą dynamicznej schematu
Przed użyciem tabeli musi być zdefiniowany.  Tabele mogą być definiowane ze schematem statyczne (gdzie hello developer definiuje hello kolumn w schemacie hello) lub dynamicznie (gdzie hello SDK Określa schemat hello oparty na przychodzące żądania). Ponadto hello deweloper może kontrolować określonych aspekty hello WebAPI przez dodanie definicji toohello kodu Javascript.

Najlepszym rozwiązaniem należy zdefiniować każdej tabeli w pliku Javascript w katalogu tabel hello następnie tabele hello tooimport tables.import() — metoda.  Rozszerzanie hello basic-app, będzie można dostosować pliku app.js hello:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Definiowanie tabeli hello. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

Tabele domyślnie używają schematu dynamicznych.  tooturn poza dynamiczne schematu globalnie, ustawić ustawienia aplikacji hello **MS_DynamicSchema** toofalse w hello portalu Azure.

Pełny przykład można znaleźć w hello [todo przykładem w witrynie GitHub].

### <a name="howto-staticschema"></a>Porady: Definiowanie tabel za pomocą statycznego schematu
Można jawnie definiować hello tooexpose kolumn za pomocą hello WebAPI.  Hello azure-mobile aplikacji Node.js SDK automatycznie dodaje wszystkie dodatkowe kolumny są wymagane dla listy toohello synchronizacji danych w trybie offline, który podasz.  Na przykład wymagać tabeli z kolumnami przez aplikacje klienckie Szybki Start: tekst (ciąg) i ukończyć (wartość logiczna).  
Hello tabeli można zdefiniować w hello tabeli JavaScript pliku definicji (znajdujący się w katalogu tabel hello) w następujący sposób:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Tabel w przypadku definiowania statycznie, następnie należy także wywołać schematu bazy danych hello toocreate hello tables.initialize() — metoda podczas uruchamiania.  Zwraca metodę tables.initialize() Hello [Promise] tak, aby usługi sieci web hello nie obsługiwać żądań przed hello bazy danych został zainicjowany.

### <a name="howto-sqlexpress-setup"></a>Porady: użycie programu SQL Express jako programowanie magazynu danych na komputerze lokalnym
Witaj hello Azure Mobile Apps SDK węzła aplikacje AzureMobile zawiera trzy opcje do obsługi danych fabrycznej hello: zestaw SDK zawiera trzy opcje do obsługi danych fabrycznej hello:

* Użyj hello **pamięci** magazynu przykład tooprovide nietrwałe sterowników
* Użyj hello **mssql** tooprovide sterowników magazynu danych programu SQL Express dla rozwoju
* Użyj hello **mssql** tooprovide sterowników magazynu danych bazy danych SQL Azure dla trybu produkcyjnego

zestaw SDK usługi Azure Mobile Apps Node.js Hello używa hello [mssql Node.js pakietu] tooestablish i użyj programu SQL Express tooboth połączenia i bazy danych SQL.  Ten pakiet wymaga włączenia połączeń TCP w wystąpieniu programu SQL Express.

> [!TIP]
> Sterownik pamięci Hello nie ma kompletnego zestawu urządzenia do testowania.  W razie potrzeby tootest zaplecza lokalnie zaleca użycie hello magazyn danych SQL Express i hello mssql sterownika.
>
>

1. Pobierz i zainstaluj [programu Microsoft SQL Server 2014 Express].  Upewnij się, że hello programu SQL Server 2014 Express jest instalowany z wersji narzędzia.  Chyba że jawnie wymagana jest Obsługa 64-bitowych, hello 32-bitowej wersji zużywa mniej pamięci podczas uruchamiania.
2. Uruchom Menedżera konfiguracji programu SQL Server 2014 hello.

   1. Rozwiń węzeł hello **konfigurację sieci programu SQL Server** węzła w menu drzewa po lewej stronie powitania.
   2. Kliknij przycisk **protokoły dla programu SQLEXPRESS**.
   3. Kliknij prawym przyciskiem myszy **TCP/IP** i wybierz **włączyć**.  Kliknij przycisk **OK** w wyskakującym oknie dialogowym hello.
   4. Kliknij prawym przyciskiem myszy **TCP/IP** i wybierz **właściwości**.
   5. Kliknij przycisk hello **adresów IP** kartę.
   6. Znajdź hello **IPWszystkie** węzła.  W hello **TCP Port** wprowadź **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Kliknij przycisk **OK**.  Kliknij przycisk **OK** w wyskakującym oknie dialogowym hello.
   8. Kliknij przycisk **usług SQL Server** w menu drzewa po lewej stronie powitania.
   9. Kliknij prawym przyciskiem myszy **programu SQL Server (SQLEXPRESS)** i wybierz **ponownego uruchomienia**
   10. Zamknij hello Menedżera konfiguracji programu SQL Server 2014.
3. Uruchom hello SQL Server 2014 Management Studio i połącz tooyour lokalne wystąpienie programu SQL Express

   1. Kliknij prawym przyciskiem myszy wystąpienie w hello Eksplorator obiektów i wybierz **właściwości**
   2. Wybierz hello **zabezpieczeń** strony.
   3. Upewnij się, hello **tryb programu SQL Server i uwierzytelniania systemu Windows** jest zaznaczone
   4. Kliknij przycisk **OK**.

          ![Configure SQL Express Authentication][4]
   5. Rozwiń węzeł **zabezpieczeń** > **logowania** w hello Eksplorator obiektów
   6. Kliknij prawym przyciskiem myszy **logowania** i wybierz **nowe dane logowania...**
   7. Wprowadź nazwę logowania.  Wybierz pozycję **Uwierzytelnianie programu SQL Server**.  Wprowadź hasło, a następnie wprowadź hello tego samego hasła w **Potwierdź hasło**.  Witaj hasło musi spełniać wymagania co do złożoności systemu Windows.
   8. Kliknij przycisk **OK**.

          ![Add a new user tooSQL Express][5]
   9. Kliknij prawym przyciskiem myszy nazwę nowego użytkownika, a następnie wybierz **właściwości**
   10. Wybierz hello **ról serwera** strony
   11. Sprawdź hello pole dalej toohello **dbcreator** roli serwera
   12. Kliknij przycisk **OK**.
   13. Zamknij hello SQL Server 2015 Management Studio

Zapewnić, że hello rekordu nazwy użytkownika i hasła, wybrane.  W zależności od wymagań określonej bazy danych może być konieczne tooassign dodatkowych ról serwera lub uprawnieniami.

Witaj aplikacji Node.js odczytuje hello **SQLCONNSTR_MS_TableConnectionString** zmiennej środowiskowej hello ciągu połączenia dla tej bazy danych.  Można ustawić tę zmienną w danym środowisku.  Na przykład można użyć PowerShell tooset tej zmiennej środowiskowej:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Hello dostępu do bazy danych przy użyciu połączenia TCP/IP i podaj nazwę użytkownika i hasło dla połączenia hello.

### <a name="howto-config-localdev"></a>Porady: Konfigurowanie projektu dla rozwoju lokalnych
Aplikacje mobilne platformy Azure odczytuje plik JavaScript o nazwie *azureMobile.js* z hello lokalnego systemu plików.  Nie używać tego pliku tooconfigure hello zestaw SDK usługi Azure Mobile Apps w środowisku produkcyjnym — Użyj ustawień aplikacji w ramach hello [portalu Azure] zamiast tego.  Witaj *azureMobile.js* plików należy wyeksportować obiekt konfiguracji.  Witaj najczęściej używane ustawienia to:

* Ustawienia bazy danych
* Ustawienia rejestrowania diagnostycznego
* Alternatywne ustawienia mechanizmu CORS

Przykład *azureMobile.js* pliku implementacji hello poprzedzających następujące ustawienia bazy danych:

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

Firma Microsoft zaleca dodanie *azureMobile.js* tooyour *.gitignore* pliku (lub inne Ignoruj pliku kontroli kodu źródłowego) hasła tooprevent znajdują się w chmurze hello.  Zawsze skonfigurować ustawienia produkcji w ustawieniach aplikacji w ramach hello [portalu Azure].

### <a name="howto-appsettings"></a>Instrukcje: Konfigurowanie ustawień aplikacji dla aplikacji mobilnej
Większość ustawień w hello *azureMobile.js* plik ma odpowiednik ustawienia aplikacji w hello [portalu Azure].  W ustawieniach aplikacji, należy użyć powitania po tooconfigure listy aplikacji:

| Ustawienia aplikacji | *azureMobile.js* ustawienie | Opis | Prawidłowe wartości |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |Nazwa aplikacji hello Hello |Ciąg |
| **MS_MobileLoggingLevel** |Logging.level |Poziom dziennika minimalna toolog wiadomości |błąd, ostrzeżenie, informacje o verbose, debug, niemądre |
| **MS_DebugMode** |Debugowania |Włącz lub wyłącz tryb debugowania |wartość true, false |
| **MS_TableSchema** |Data.Schema |Domyślna nazwa schematu dla tabel SQL |ciąg (domyślne: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Włącz lub wyłącz tryb debugowania |wartość true, false |
| **MS_DisableVersionHeader** |Wersja (tooundefined zestaw) |Wyłącza nagłówka X-ZUMO-Server-Version hello |wartość true, false |
| **MS_SkipVersionCheck** |skipversioncheck |Wyłącza sprawdzanie wersji powitania klienta interfejsu API |wartość true, false |

tooset ustawienie aplikacji:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello aplikacji mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello. Jeśli nie kliknij przycisk **ustawienia**.
4. Kliknij przycisk **ustawienia aplikacji** hello ogólne menu.
5. Przewiń toohello w sekcji Ustawienia aplikacji.
6. Jeśli aplikacja, ustawienia już istnieje, kliknij wartość hello hello aplikacji ustawienie tooedit hello wartości.
7. Jeśli ustawienia aplikacji nie istnieje, wprowadź hello ustawienie aplikacji w polu klucza hello a hello wartość w polu wartość hello.
8. Po zakończeniu, kliknij przycisk **zapisać**.

Zmiana większość ustawień aplikacji wymaga ponownego uruchomienia usługi.

### <a name="howto-use-sqlazure"></a>Porady: Użyj bazy danych SQL jako magazyn danych produkcyjnych
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

Przy użyciu bazy danych SQL Azure jako magazynu danych jest identyczne we wszystkich typów aplikacji w usłudze Azure App Service. Jeśli jeszcze tego nie zrobiono, wykonaj te kroki toocreate zaplecza aplikacji mobilnej.

1. Zaloguj się za toohello [portalu Azure].
2. W hello lewym górnym rogu okna hello, kliknij przycisk hello **+ nowy** przycisk > **sieci Web i mobilność** > **aplikacji mobilnej**, następnie podaj nazwę zaplecza aplikacji mobilnej.
3. W hello **grupy zasobów** wprowadź hello takie same nazwy co aplikacja.
4. plan usługi aplikacji — domyślna Hello jest zaznaczone.  Jeśli chcesz toochange planu usługi aplikacji, możesz to zrobić, klikając hello Plan usługi aplikacji > **+ Utwórz nowe**.  Podaj nazwę nowego planu usługi aplikacji hello i wybierz odpowiednią lokalizację.  Kliknij hello warstwa cenowa i wybierz odpowiednią warstwę cenową dla usługi hello. Wybierz **Wyświetl wszystkie** tooview więcej cennik opcje, takie jak **wolne** i **Shared**.  Po wybraniu warstwy cenowej kliknij hello **wybierz** przycisku.  Po powrocie do hello **planu usługi aplikacji** bloku, kliknij przycisk **OK**.
5. Kliknij przycisk **Utwórz**. Inicjowanie obsługi administracyjnej zaplecza aplikacji mobilnej może potrwać kilka minut.  Po zainicjowaniu obsługi zaplecza aplikacji mobilnej hello portalu hello otwiera hello **ustawienia** bloku hello zaplecza aplikacji mobilnej.

Po utworzeniu hello zaplecza aplikacji mobilnej, można wybrać tooeither Połącz istniejące zaplecza aplikacji mobilnej tooyour bazy danych SQL lub Utwórz nową bazę danych SQL.  W tej sekcji utworzymy bazy danych SQL.

> [!NOTE]
> Jeśli masz już bazę danych w hello tej samej lokalizacji co hello zaplecza aplikacji mobilnej, zamiast tego możesz **Użyj istniejącej bazy danych** , a następnie wybrać tę bazę danych. Użycie Hello bazy danych w innej lokalizacji nie jest zalecane z powodu większych opóźnień.
>
>

1. W zaplecze nowej aplikacji mobilnej powitania kliknij **ustawienia** > **aplikacji mobilnej** > **danych** > **+ Dodaj**.
2. W hello **Dodaj połączenie danych** bloku, kliknij przycisk **baza danych SQL — Skonfiguruj wymagane ustawienia** > **Utwórz nową bazę danych**.  Wprowadź nazwę nowej bazy danych hello hello w hello **nazwa** pola.
3. Kliknij przycisk **serwera**.  W hello **nowy serwer** bloku, wprowadź unikatową nazwą serwera w hello **nazwy serwera** pól i zapewnienia odpowiedniej **identyfikator logowania administratora serwera** i **hasło**.  Upewnij się, **Zezwalaj usługom platformy azure tooaccess serwera** jest zaznaczony.  Kliknij przycisk **OK**.

    ![Utwórz bazę danych Azure SQL][6]
4. Na powitania **nową bazę danych** bloku, kliknij przycisk **OK**.
5. Powrót na powitania **Dodaj połączenie danych** bloku, wybierz opcję **ciąg połączenia**, wprowadź hello logowania i hasło podane podczas tworzenia hello bazy danych.  Jeśli używasz istniejącej bazy danych, należy podać poświadczenia logowania powitania dla tej bazy danych.  Po wpisaniu, kliknij przycisk **OK**.
6. Wróć na powitania **Dodaj połączenie danych** bloku ponownie, kliknij przycisk **OK** toocreate hello w bazie danych.

<!--- END OF ALTERNATE INCLUDE -->

Tworzenie bazy danych hello może potrwać kilka minut.  Użyj hello **powiadomienia** obszaru toomonitor hello postęp wdrażania hello.  Nie postępu aż hello bazy danych został wdrożony pomyślnie.  Po pomyślnym wdrożeniu, ciąg połączenia jest tworzony dla wystąpienia bazy danych SQL hello w zapleczu swojej przenośnych ustawień aplikacji.  Można wyświetlić to ustawienie aplikacji hello **ustawienia** > **ustawienia aplikacji** > **parametry połączenia**.

### <a name="howto-tables-auth"></a>Porady: Wymagaj uwierzytelniania tootables dostępu
Jeśli chcesz toouse uwierzytelniania usługi aplikacji z punktem końcowym tabel hello, należy skonfigurować uwierzytelnianie usługi aplikacji w hello [portalu Azure] pierwszy.  Dla więcej szczegółów na temat konfigurowania uwierzytelniania w usłudze Azure App Service, przejrzyj hello przewodnik konfiguracji dla dostawcy tożsamości hello mają toouse:

* [Jak tooconfigure uwierzytelniania usługi Azure Active Directory]
* [Jak tooconfigure uwierzytelniania serwisu Facebook]
* [Jak tooconfigure uwierzytelniania serwisu Google]
* [Jak tooconfigure Authentication firmy Microsoft]
* [Jak tooconfigure uwierzytelniania w usłudze Twitter]

Każda tabela ma właściwość dostępu, które mogą być używane toocontrol dostępu toohello tabeli.  następujące przykładowe Hello jest wyświetlana tabela statycznie zdefiniowanych wymagane uwierzytelnienie.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Hello dostępu do właściwości można wykonać jedną z następujących wartości:

* *anonimowe* wskazuje, czy aplikacja kliencka hello może tooread danych bez uwierzytelniania
* *uwierzytelniony* oznacza, że aplikacja kliencka hello musi wysłany token uwierzytelniania prawidłowe z żądaniem hello
* *wyłączone* wskazuje, że ta tabela jest obecnie wyłączona

Jeśli zdefiniowano właściwość dostępu hello nieuwierzytelnionym dostępem jest dozwolone.

### <a name="howto-tables-getidentity"></a>Porady: Użyj uwierzytelniania oświadczeń z tabel
Można skonfigurować różne oświadczenia, które są wymagane podczas konfigurowania uwierzytelniania.  Te oświadczenia nie są zwykle dostępne za pośrednictwem hello `context.user` obiektu.  Jednak mogą zostać pobrane za pomocą hello `context.user.getIdentity()` metody.  Witaj `getIdentity()` metoda zwraca Promise, który jest rozpoznawany jako obiekt tooan.  Obiekt Hello jest wyznaczaną przez metodę uwierzytelniania (facebook, google, twitter, microsoftaccount lub aad).

Na przykład skonfigurować uwierzytelnianie Microsoft Account i oświadczeń adresów e-mail hello żądania, można dodać rekordu toohello adresu e-mail hello z powitania po kontrolera tabeli:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee jakie oświadczenia są dostępne, użyj hello tooview przeglądarki sieci web `/.auth/me` punktu końcowego witryny.

### <a name="howto-tables-disabled"></a>Porady: wyłączanie dostępu toospecific tabeli operacji
W tooappearing dodawania tabeli hello hello dostępu do właściwości mogą być używane toocontrol poszczególnych działań.  Istnieją cztery operacje:

* *Przeczytaj* jest hello operacji RESTful GET, w tabeli hello
* *Wstaw* jest operację RESTful POST hello na powitania tabeli
* *Zaktualizuj* hello poprawka RESTful operacja jest w tabeli hello
* *Usuń* hello RESTful usunąć operacja jest w tabeli hello

Na przykład możesz tooprovide nieuwierzytelnione tabeli tylko do odczytu:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Porady: dopasowywanie hello kwerendę, która jest używana z operacjami tabeli
Typowe wymagania dotyczące operacji tabeli jest tooprovide ograniczony widok hello danych.  Na przykład musisz podać tabelę, która jest oznaczane hello uwierzytelnianego identyfikator użytkownika w taki sposób, że można tylko do odczytu lub aktualizacji własnych.  oferuje powitania po definicji tabeli:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Operacje, które zwykle wykonać zapytania ma właściwość zapytania, który można dostosować, w której klauzuli. Właściwość kwerendy Hello jest [QueryJS] obiekt może przetwarzać używane tooconvert toosomething zapytania OData, która hello danych zaplecza.  W przypadku prostego równości (na przykład hello poprzedzających jeden) można użyć mapy. Możesz także dodać punkty SQL:

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Porady: Konfigurowanie usuwania nietrwałego dla tabeli
Faktycznie usuwania nietrwałego nie powoduje usunięcia rekordów.  Zamiast tego oznacza je jako usunięte w bazie danych hello przez ustawienie tootrue kolumna usunąć hello.  Hello Azure Mobile Apps SDK automatycznie usuwa wszystkie usunięte nietrwale rekordy z wyników, chyba że IncludeDeleted() używa hello zestawu SDK klienta usługi Mobile.  tooconfigure Usuń tabelę dla elastyczne, ustaw hello `softDelete` właściwość w pliku definicji tabeli hello:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Należy określić mechanizm przeczyszczanie rekordów — od aplikacji klienta, za pomocą zadania WebJob, funkcji platformy Azure lub za pomocą niestandardowego interfejsu API.

### <a name="howto-tables-seeding"></a>Porady: inicjatora bazy danych z danymi
Podczas tworzenia nowej aplikacji, warto zapoznać się z tooseed tabelę z danymi.  Można to zrobić w pliku JavaScript w definicji tabeli hello w następujący sposób:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Wstępne wypełnianie danych jest wykonywane tylko po utworzeniu tabeli hello przez hello Azure Mobile Apps SDK.  Jeśli hello tabela już istnieje w bazie danych hello, żadne dane nie jest dodane do tabeli hello.  Jeśli włączono dynamiczne schematu schematu jest wywnioskować na podstawie danych hello rozpoczęta.

Firma Microsoft zaleca jawnie wywołać hello `tables.initialize()` metody toocreate hello tabeli, gdy usługa hello zacznie działać.

### <a name="Swagger"></a>Porady: Włączanie obsługi programu Swagger
Usługa Azure App Service Mobile Apps jest dostarczany z wbudowanych [Swagger] obsługuje.  tooenable pomocy technicznej programu Swagger, najpierw zainstalować hello interfejsu użytkownika programu swagger jako zależność:

    npm install --save swagger-ui

Po zakończeniu instalacji można włączyć obsługę struktury Swagger w Konstruktorze Azure Mobile Apps hello:

    var mobile = azureMobileApps({ swagger: true });

Możesz tylko prawdopodobnie chcesz tooenable obsługi struktury Swagger w wersjach programowanie.  Można to zrobić przy użyciu `NODE_ENV` ustawienie aplikacji:

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Witaj punktu końcowego struktury swagger znajduje się pod adresem http://*yoursite*.azurewebsites.net/swagger.  Dostęp można uzyskać hello interfejs użytkownika programu Swagger za pośrednictwem hello `/swagger/ui` punktu końcowego.  Jeśli zostanie wybrana opcja uwierzytelniania toorequire w całej aplikacji, struktury Swagger powoduje błąd.  Aby uzyskać najlepsze wyniki, wybierz tooallow nieuwierzytelniony żądań za pośrednictwem hello uwierzytelniania usługi aplikacji Azure / ustawienia autoryzacji, następnie kontrolować uwierzytelnianie przy użyciu hello `table.access` właściwości.

Możesz także dodać hello Swagger opcji tooyour `azureMobile.js` plik, jeśli mają tylko obsługę struktury Swagger podczas opracowywania lokalnie.

## <a name="a-namepushpush-notifications"></a><a name="push">Powiadomienia wypychane
Aplikacje mobilne integruje się z tooenable usługi Azure Notification Hubs można toomillions powiadomień wypychanych toosend docelowych urządzeń we wszystkich głównych platform. Przy użyciu usługi Notification Hubs, możesz wysłać wypychania tooiOS powiadomienia, Android i Windows. toolearn więcej informacji na temat wszystkie opcje, które można wykonać przy użyciu usługi Notification Hubs, zobacz [omówienie centra powiadomień](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Porady: wysyłanie powiadomień wypychanych
Witaj następującego kodu pokazano, jak toouse hello wypychania obiektu toosend emisji push urządzeń z systemem iOS tooregistered powiadomień:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Tworząc rejestracji wypychanych szablonu z powitania klienta, możesz zamiast tego wysłać toodevices wiadomości wypychanych szablonu, na wszystkich obsługiwanych platformach. Witaj następującego kodu pokazuje sposób toosend powiadomienie o szablonie:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Porady: tooan powiadomień wypychanych wysyłania uwierzytelnić użytkownika przy użyciu tagów
Uwierzytelniony użytkownik rejestruje dla powiadomień wypychanych, tag identyfikator użytkownika jest automatycznie dodawany toohello rejestracji. Za pomocą tego tagu, możesz wysłać wypychania powiadomień tooall urządzeń zarejestrowanych przez określonego użytkownika. Hello poniższy kod pobiera identyfikator SID użytkownika zgłaszającego żądanie hello hello i wysyła rejestracji urządzenia tooevery powiadomień wypychanych szablon dla tego użytkownika:

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Podczas rejestrowania dla powiadomień wypychanych z uwierzytelnionego klienta, upewnij się, że przed podjęciem próby wykonania rejestracji zakończeniem uwierzytelniania.

## <a name="CustomAPI"></a>Niestandardowych interfejsów API
### <a name="howto-customapi-basic"></a>Porady: Definiowanie niestandardowego interfejsu API
Ponadto toohello dostępu do danych interfejsu API za pośrednictwem punktu końcowego /tables hello, Azure Mobile Apps zapewniają niestandardowe pokrycia interfejsu API.  Niestandardowych interfejsów API są zdefiniowane w podobne definicji tabeli toohello sposób i uzyskać dostęp do wszystkich hello tego samego urządzenia, włącznie z uwierzytelnianiem.

W razie potrzeby toouse aplikacji usługa uwierzytelniania za pomocą API niestandardowe, należy skonfigurować uwierzytelnianie usługi aplikacji w hello [portalu Azure] pierwszy.  Dla więcej szczegółów na temat konfigurowania uwierzytelniania w usłudze Azure App Service, przejrzyj hello przewodnik konfiguracji dla dostawcy tożsamości hello mają toouse:

* [Jak tooconfigure uwierzytelniania usługi Azure Active Directory]
* [Jak tooconfigure uwierzytelniania serwisu Facebook]
* [Jak tooconfigure uwierzytelniania serwisu Google]
* [Jak tooconfigure Authentication firmy Microsoft]
* [Jak tooconfigure uwierzytelniania w usłudze Twitter]

Niestandardowych interfejsów API są zdefiniowane w taki sam sposób jak hello API tabel hello.

1. Utwórz **interfejsu api** katalogu
2. Utwórz plik JavaScript definicji interfejsu API w hello **interfejsu api** katalogu.
3. Użyj hello importu metody tooimport hello **interfejsu api** katalogu.

Oto definicji interfejsu api prototypu hello na podstawie próbki basic aplikacji hello, którego użyliśmy wcześniej.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Spójrzmy na przykład interfejs API, który zwraca datę serwera hello przy użyciu hello *Date.now()* metody.  Oto hello api/date.js pliku:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Każdy parametr jest jednym z hello RESTful zleceń standardowych - GET, POST, poprawki lub DELETE.  Metoda Hello jest standardem [oprogramowanie pośredniczące ExpressJS] funkcji, który wysyła dane wyjściowe hello wymagane.

### <a name="howto-customapi-auth"></a>Porady: Wymagaj uwierzytelniania niestandardowego interfejsu API tooa dostępu
Azure Mobile Apps SDK implementuje uwierzytelnianie w hello tak samo dla punktu końcowego tabel hello i niestandardowych interfejsów API.  Aby dodać utworzonych w poprzedniej sekcji hello API toohello uwierzytelnianie, Dodaj **dostępu** właściwości:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

Można również określić uwierzytelniania na określonych operacji:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Witaj tego samego tokenu, który jest używany dla punktu końcowego tabel hello należy użyć dla niestandardowych interfejsów API wymaga uwierzytelniania.

### <a name="howto-customapi-auth"></a>Porady: Obsługa wysyłania dużych plików
Azure Mobile Apps SDK używa hello [oprogramowanie pośredniczące analizator treści](https://github.com/expressjs/body-parser) tooaccept i dekodowania zawartości w treści w Twoje zgłoszenie.  Można wstępnie skonfigurować przekazywania plików większych tooaccept analizator treści:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Plik Hello jest algorytmem przed transmisją base-64.  Zwiększa to hello rozmiar rzeczywisty przekazywania hello (i dlatego hello rozmiar, które należy uwzględnić).

### <a name="howto-customapi-sql"></a>Porady: wykonanie niestandardowych instrukcje SQL
Hello zestaw SDK usługi Azure Mobile Apps umożliwia toohello dostęp do całego kontekstu za pośrednictwem obiektu żądania hello, dzięki czemu tooexecute sparametryzowana łatwo dostawcy danych toohello instrukcji SQL:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Debugowanie, łatwe tabel i łatwe interfejsów API
### <a name="howto-diagnostic-logs"></a>Porady: debugowanie, diagnozowanie i rozwiązywanie problemów z usługi Azure Mobile apps
Hello Azure App Service zapewnia kilka debugowania i rozwiązywanie problemów z techniki aplikacji Node.js.
Można znaleźć toohello następujące artykuły tooget uruchomione przy rozwiązywaniu problemów z poziomu zaplecza Node.js Mobile:

* [Monitorowanie usługi aplikacji Azure]
* [Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure]
* [Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio]

Aplikacje środowiska node.js mają dostęp tooa szeroką gamę narzędzi diagnostycznych dziennika.  Wewnętrznie hello korzysta z zestawu SDK usługi Azure Mobile Apps Node.js [Winston] dla rejestrowania diagnostycznego.  Rejestrowanie jest automatycznie włączone, należy włączyć tryb debugowania lub przez ustawienie hello **MS_DebugMode** tootrue ustawienie aplikacji w hello [portalu Azure]. Dzienniki generowane są wyświetlane w hello dzienników diagnostycznych na powitania [portalu Azure].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Porady: Praca z tabelami łatwy w hello portalu Azure
Łatwe tabel w portalu hello umożliwiają tworzenie i Praca z tabelami bezpośrednio w portalu hello. Operacje tabeli za pomocą edytora usługi aplikacji hello nawet można edytować.

Po kliknięciu **łatwe tabel** w ustawieniach wewnętrznej bazy danych lokacji można Dodawanie, modyfikowanie lub usuwanie tabeli. Można również sprawdzić dane w tabeli hello.

![Praca z tabelami łatwe](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Hello są dostępne na pasku poleceń hello tabeli następujące polecenia:

* **Zmienianie uprawnień** — zmodyfikować hello uprawnienie do odczytu, wstawianie, aktualizowanie i usuwanie operacji względem tabeli hello.
  Dostępne są opcje tooallow dostępu anonimowego, uwierzytelniania toorequire lub toodisable wszystkie dostępu toohello operacji.
* **Edytowanie skryptu** -hello pliku skryptu tabeli hello jest otwarty w hello Edytor usług aplikacji.
* **Zarządzanie schematem** — Dodawanie lub usuwanie kolumn lub zmienianie hello indeksu tabeli.
* **Wyczyść tabeli** -obcina istniejącej tabeli jest usunięcie wszystkich wierszy danych, ale pozostawienie schematu hello bez zmian.
* **Usuwanie wierszy** -Usuń poszczególne wiersze danych.
* **Wyświetl podgląd dzienników przesyłanych strumieniowo** -łączy toohello przesyłania strumieniowego usługi rejestrowania dla witryny.

### <a name="work-easy-apis"></a>Porady: pracy z interfejsami API łatwy w hello portalu Azure
Łatwe interfejsów API w portalu hello umożliwiają tworzenie i Praca z niestandardowych bezpośrednio interfejsy API w portalu hello. Można edytować skrypty interfejsu API przy użyciu hello Edytor usług aplikacji.

Po kliknięciu **łatwe interfejsów API** w ustawieniach wewnętrznej bazy danych lokacji można Dodawanie, modyfikowanie lub usuwanie niestandardowych punkt końcowy interfejsu API.

![Praca z łatwe interfejsów API](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

W portalu hello można zmienić hello uprawnienia dostępu dla danej akcji HTTP, Edytuj plik skryptu interfejsu API hello w edytorze usługi aplikacji lub Wyświetl dzienniki przesyłania strumieniowego hello.

### <a name="online-editor"></a>Porady: edytowanie kodu hello Edytor usługi aplikacji
Hello portalu Azure umożliwia edytowanie plików skryptów zaplecza Node.js w hello Edytor usług aplikacji bez konieczności pobierania hello komputera lokalnego tooyour projektu. pliki skryptów tooedit hello edytora online:

1. W bloku zaplecza aplikacji mobilnej, kliknij **wszystkie ustawienia** > albo **łatwe tabel** lub **łatwe interfejsów API**, kliknij tabelę lub interfejsu API, a następnie kliknij przycisk **edytowanie skryptu**. plik skryptu Hello jest otwarty w hello Edytor usług aplikacji.

    ![Edytor usługi aplikacji](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Tworzenie pliku kodu toohello zmiany w hello edytora online. Zmiany zostaną zapisane automatycznie podczas pisania.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Szybki Start kliencką dla systemu android]: app-service-mobile-android-get-started.md
[Apache Cordova klienta — Szybki Start]: app-service-mobile-cordova-get-started.md
[iOS — Szybki Start klienta]: app-service-mobile-ios-get-started.md
[Szybki Start klienta platformy Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Szybki Start klienta platformy Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Szybki Start klienta platformy Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Szybki Start klienta Sklepu Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[synchronizacji danych w trybie offline]: app-service-mobile-offline-data-sync.md
[Jak tooconfigure uwierzytelniania usługi Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Jak tooconfigure uwierzytelniania serwisu Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Jak tooconfigure uwierzytelniania serwisu Google]: app-service-mobile-how-to-configure-google-authentication.md
[Jak tooconfigure Authentication firmy Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Jak tooconfigure uwierzytelniania w usłudze Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md
[Monitorowanie usługi aplikacji Azure]: ../app-service-web/web-sites-monitor.md
[Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[Określ hello wersji węzła]: ../nodejs-specify-node-version-azure-apps.md
[Użyj modułów węzła]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portalu Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp przykładem w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo przykładem w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[katalogu przykładów w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 dla programu Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js pakietu]: https://www.npmjs.com/package/mssql
[programu Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[oprogramowanie pośredniczące ExpressJS]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
