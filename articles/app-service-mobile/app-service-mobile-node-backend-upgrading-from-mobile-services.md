---
title: "aaaUpgrade z usługi Mobile Services tooAzure usługi aplikacji - Node.js"
description: "Dowiedz się, jak tooeasily uaktualnienia programu tooan aplikacji usługi Mobile Services aplikację usługi Mobile aplikacji"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Uaktualnij istniejący tooApp usługi mobilnej Azure Node.js usługi
Mobile App Service jest nowy sposób toobuild aplikacji dla urządzeń przenośnych przy użyciu programu Microsoft Azure. toolearn więcej, zobacz [co to są Mobile Apps?].

W tym temacie opisano sposób tooupgrade istniejącej aplikacji zaplecza Node.js z usług Azure Mobile Services tooa nowej aplikacji usługi Mobile Apps. Podczas wykonywania tego uaktualnienia istniejącej aplikacji usługi Mobile Services można nadal toooperate.  Jeśli potrzebujesz tooupgrade aplikacji zaplecza Node.js odwoływać się za[uaktualniania usług Mobile Services dla programu .NET](app-service-mobile-net-upgrading-from-mobile-services.md).

Zaplecze aplikacji mobilnej jest uaktualniony tooAzure usługi aplikacji, ma tooall dostęp do funkcji usługi aplikacji i są rozliczane według zbyt[cennik usługi aplikacji], nie Mobile Services cennik.

## <a name="migrate-vs-upgrade"></a>Migrowanie i uaktualnianie
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Zaleca się że [przeprowadzenie migracji](app-service-mobile-migrating-from-mobile-services.md) przed rozpoczęciem uaktualnienia. W ten sposób można umieścić obie wersje aplikacji hello tego samego planu usługi App Service i pociągnąć za sobą nie dodatkowych kosztów.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Ulepszenia w Mobile Apps Node.js server SDK
Uaktualnianie toohello nowe [zestaw SDK usługi Mobile Apps](https://www.npmjs.com/package/azure-mobile-apps) zawiera wiele udoskonaleń, w tym:

* Oparte na powitania [Express framework](http://expressjs.com/en/index.html), hello nowego węzła zestawu SDK jest lekki i zaprojektowany jako zaczynają do nowych wersji węzła tookeep się. Można dostosować zachowanie aplikacji hello z oprogramowania pośredniczącego Express.
* Znaczący wzrost wydajności porównywana toohello zestawu SDK usług mobilnych.
* Można hostować witrynę sieci Web wraz z zaplecza aplikacji mobilnych; Podobnie jest łatwe tooadd hello zestaw SDK usługi Azure Mobile tooany istniejących express.v4 aplikacja.
* Skompilowany dla rozwoju i platform i lokalnego, hello zestaw SDK usługi Mobile Apps można opracowany i uruchom lokalnie na platformach Windows, Linux lub OS x. Teraz jest łatwe toouse wspólnego węzła metody takie jak uruchamianie [Mocha](https://mochajs.org/) toodeployment poprzednich testów.

## <a name="overview"></a>Ogólne omówienie uaktualnienia
tooaid do uaktualniania zaplecza Node.js usługi Azure App Service oferuje pakietu zgodności.  Po uaktualnieniu będziesz mieć witrynę niew, które mogą być wdrożone tooa nowej lokacji usługi aplikacji.

są zestawy SDK klienta usługi Mobile Services Hello **nie** zgodny z hello nowy serwer Mobile Apps SDK. W kolejności tooprovide ciągłości usługi dla aplikacji nie należy opublikować zmian tooa lokacji aktualnie obsługujący opublikowanych klientów. Zamiast tego należy utworzyć nowej aplikacji mobilnej, która służy jako duplikat. Możesz też zaznaczyć tę aplikację na powitania same usługi aplikacji — planowanie tooavoid ponoszenia dodatkowych kosztów finansowych.

Następnie będzie mieć dwie wersje aplikacji hello: hello, który pozostaje takie same służy opublikowane aplikacje w hello symbole i zwolnij innych, które następnie można uaktualnić i miejsce docelowe z nowego klienta. Można przenieść i testowanie kodu w tempie użytkownika, ale należy się upewnić, że wszelkie poprawki wprowadzone pobrać tooboth zastosowane. Po uważasz, że odpowiednią liczbę klienta aplikacji w symbole zostały zaktualizowane toohello najnowszej wersji, można usunąć oryginalny zmigrowana aplikacja hello, jeśli jest to wymagane. Go nie pociągnąć za sobą dodatkowe koszty pieniężnego, jeśli jest hostowany w hello planowanie same usługi aplikacji jako aplikacji mobilnej.

Pełna konspekt procesu uaktualniania hello Hello jest następujący:

1. Pobierz istniejącej usługi mobilnej Azure (migrowanych).
2. Konwertuj hello tooan projekt aplikacji mobilnej Azure przy użyciu hello zgodność pakietu.
3. Rozwiąż wszystkie problemy dotyczące różnic (na przykład ustawienia uwierzytelniania).
4. Wdrażanie z przekonwertowanego tooa projekt aplikacji mobilnej Azure nowej aplikacji usługi.
5. Zwolnij nowej wersji aplikacji klienckiej czy Użyj hello nowej aplikacji mobilnej.
6. (Opcjonalnie) Usuń zmigrowane usługi mobilnej oryginalnej aplikacji.

Usuwanie może wystąpić, gdy nie jest widoczny cały ruch w oryginalnej zmigrowane usługi mobilnej.

## <a name="install-npm-package"></a>Zainstaluj wymagania wstępne hello
[Node] należy zainstalować na komputerze lokalnym.  Należy również zainstalować hello zgodność pakietu.  Po zainstalowaniu węzła można uruchomić następujące polecenie z nowego cmd lub w wierszu polecenia programu PowerShell hello:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a>Uzyskaj skrypty usług Azure Mobile Services
* Zaloguj się za toohello [Azure Portal].
* Przy użyciu **wszystkie zasoby** lub **usługi aplikacji**, odnalezienie witryny usług Mobile Services.
* W ramach lokacji powitania kliknij **narzędzia** -> **Kudu** -> **Przejdź** tooopen hello Kudu lokacji.
* Polecenie **konsoli debugowania** -> **PowerShell** tooopen hello debugowania konsoli.
* Przejdź do zbyt`site/wwwroot/App_Data/config` , klikając kolejno w każdym katalogu
* Kliknij na powitania pobierania ikona dalej toohello `scripts` katalogu.

To spowoduje pobranie hello skryptów w formacie ZIP.  Utwórz nowy katalog na komputerze lokalnym i Rozpakuj hello `scripts.ZIP` pliku w katalogu hello.  Spowoduje to utworzenie `scripts` katalogu.

## <a name="scaffold-app"></a>Tworzenie szkieletu hello nowego zaplecza Azure Mobile Apps
Uruchom następujące polecenie z katalogu hello zawierającym katalog skrypty hello hello:

```scaffold-mobile-app scripts out```

Spowoduje to utworzenie szkieletu zaplecza Azure Mobile Apps w hello `out` katalogu.  Mimo że nie jest to wymagane, jest hello toocheck dobrze `out` katalogu do repozytorium kodu źródłowego, wybranych przez użytkownika.

## <a name="deploy-ama-app"></a>Wdrażanie z poziomu zaplecza Azure Mobile Apps
Podczas wdrażania potrzebne są następujące hello toodo:

1. Tworzenie nowej aplikacji mobilnej w hello [Azure Portal].
2. Uruchom hello `createViews.sql` skryptu połączenia bazy danych.
3. Łącze hello bazy danych tooyour połączonej usługi mobilnej tooyour nowej aplikacji usługi.
4. Link innych toohello zasobów (takich jak usługi Notification Hubs) nowej aplikacji usługi.
5. Wdróż hello wygenerowany kod tooyour nowej lokacji.

### <a name="create-a-new-mobile-app"></a>Tworzenie nowej aplikacji mobilnej
1. Zaloguj się w hello [Azure Portal].
2. Kliknij kolejno opcje **+NOWE** > **Sieci Web i mobilność** > **Aplikacja mobilna**, a następnie podaj nazwę zaplecza aplikacji mobilnej.
3. Dla hello **grupy zasobów**, wybierz istniejącą grupę zasobów lub Utwórz nową (używając hello tej samej nazwie co aplikacja).

    Możesz wybrać inny plan usługi App Service lub utworzyć nowy. Aby uzyskać więcej informacji na temat planów usługi aplikacji i jak toocreate nowego planu w różnych cen warstwy, a w preferowanej lokalizacji, zobacz [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Dla hello **planu usługi aplikacji**, hello plan domyślny (w hello [warstwy standardowa](https://azure.microsoft.com/pricing/details/app-service/)) jest zaznaczone. Możesz również wybrać inny plan lub [utworzyć nowy](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Witaj planu usługi aplikacji określają ustawienia hello [lokalizację, funkcje, koszt i zasoby obliczeniowe](https://azure.microsoft.com/pricing/details/app-service/) skojarzone z aplikacją.

    Po podjęciu decyzji o hello planu, kliknij przycisk **Utwórz**. Spowoduje to utworzenie zaplecza aplikacji mobilnej hello.

### <a name="run-createviewssql"></a>Uruchom CreateViews.SQL
szkieletu aplikacji Hello zawiera plik o nazwie `createViews.sql`.  Ten skrypt musi zostać wykonana względem docelowej bazy danych.  Parametry połączenia Hello hello docelowej bazy danych można uzyskać z usługą mobilną zmigrowanych z hello **ustawienia** bloku w obszarze **parametry połączenia**.  Szablon ma nazwę `MS_TableConnectionString`.

Możesz uruchomić ten skrypt w programie SQL Server Management Studio lub Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Łącze hello tooyour bazy danych usługi aplikacji
Połącz hello istniejącej bazy danych tooyour usługi aplikacji:

* W hello [Azure Portal], Otwórz aplikację usługi.
* Wybierz **wszystkie ustawienia** -> **połączenia danych**.
* Polecenie **+ Dodaj**.
* Witaj listy rozwijanej wybierz **bazy danych SQL**
* W obszarze **bazy danych SQL**, wybierz istniejącą bazę danych, a następnie kliknij pozycję **wybierz**.
* W obszarze **ciąg połączenia**, wprowadź hello użytkownika i hasło dla hello bazy danych, a następnie kliknij pozycję **OK**.
* W hello **dodać połączenia danych** bloku, kliknij polecenie **OK**.

wyświetlając hello parametry połączenia dla hello docelowej bazy danych w usłudze Mobile migrowanych można znaleźć Hello nazwy użytkownika i hasła.

### <a name="set-up-authentication"></a>Konfigurowanie uwierzytelniania
Aplikacje mobilne platformy Azure pozwala uwierzytelniania usługi Azure Active Directory, Facebook, Google, Microsoft i Twitter tooconfigure w ramach usługi hello.  Niestandardowe uwierzytelnianie będzie toobe opracowany oddzielnie.  Zapoznaj się hello [pojęć dotyczących uwierzytelniania] dokumentacji i [uwierzytelniania szybkiego startu] dokumentacji, aby uzyskać więcej informacji.  

## <a name="updating-clients"></a>Aktualizowanie klientów mobilnych
Po utworzeniu operacyjną zaplecza aplikacji mobilnej, można pracować na nowej wersji aplikacji klienta, która go wykorzystuje. Aplikacje mobilne zawiera również nową wersję klienta hello zestawy SDK i podobne uaktualnienie serwera toohello powyżej, należy tooremove wszystkie odwołania zestawów SDK usługi Mobile toohello przed zainstalowaniem wersji Mobile Apps.

Jedną z głównych zmian hello między wersjami hello jest czy konstruktorów hello nie wymagają już klucz aplikacji.
Możesz teraz po prostu Przekaż hello adres URL aplikacji mobilnej. Na przykład na powitania klientów platformy .NET, hello `MobileServiceClient` Konstruktor jest teraz:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Informacje o instalacji hello nowe zestawy SDK i przy użyciu nowej struktury hello za pośrednictwem łącza hello poniżej:

* [Wersja systemu android 2,2 lub nowszy](app-service-mobile-android-how-to-use-client-library.md)
* [System iOS w wersji 3.0.0 lub nowszej](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (system Windows/Xamarin) w wersji 2.0.0 lub nowszej](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova w wersji 2.0 lub nowszej](app-service-mobile-cordova-how-to-use-client-library.md)

Czy aplikacja sprawia, że użycie powiadomień wypychanych, zwróć uwagę na powitania określonej rejestracji instrukcje dotyczące każdej platformy, jak nie zostały niektóre zmiany również.

Jeśli masz hello nową wersję klienta gotowa wypróbuj go na uaktualnionym serwerze projektu. Po weryfikacji, czy działa, można zwolnić nowej wersji toocustomers Twojej aplikacji. Po pewnym czasie po klientów miało tooreceive szansy te aktualizacje, można usunąć usługi Mobile Services hello wersji aplikacji. W tym momencie uaktualnieniu tooan aplikację usługi Mobile aplikacji przy użyciu najnowszych hello serwera Mobile Apps SDK.

<!-- URLs. -->

[Witryna Azure Portal]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[co to są Mobile Apps?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[cennik usługi aplikacji]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[pojęć dotyczących uwierzytelniania]: ../app-service/app-service-authentication-overview.md
[uwierzytelniania szybkiego startu]: app-service-mobile-auth.md

[Azure Portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
