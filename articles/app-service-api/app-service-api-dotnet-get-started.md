---
title: "aaaGet wprowadzenie do interfejsu API Apps i platformy ASP.NET w usłudze App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, wdrażanie i korzystanie z aplikacji interfejsu API platformy ASP.NET w usłudze Azure App Service przy użyciu programu Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Wprowadzenie do usługi API Apps, platformy ASP.NET i programu Swagger w usłudze Azure App Service
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Najpierw jest hello w serii samouczków, które pokazują, jak toouse funkcje aplikacji Azure usługi, które są przydatne do projektowania i obsługiwania interfejsy API RESTful.  Ten samouczek obejmuje obsługę metadanych interfejsu API w formacie struktury Swagger.

Dowiesz się:

* Jak toocreate i wdrażanie [aplikacje interfejsu API](app-service-api-apps-why-best-platform.md) w usłudze Azure App Service za pomocą narzędzi wbudowanych w programie Visual Studio 2015.
* W jaki sposób pakiet Swashbuckle NuGet odnajdywania tooautomate interfejsu API za pomocą hello toodynamically Generowanie metadanych programu Swagger interfejsu API.
* Jak tooautomatically metadanych interfejsu API programu Swagger toouse generowanie kodu klienta dla aplikacji interfejsu API.

## <a name="sample-application-overview"></a>Omówienie przykładowej aplikacji
W tym samouczku będziemy pracować z przykładową aplikacją zawierającą prostą listę zadań do wykonania. Aplikacja Hello ma frontonu jednostronicowej aplikacji JEDNOSTRONICOWEJ, warstwę środkową interfejsu API sieci Web platformy ASP.NET i warstwę danych interfejsu API sieci Web ASP.NET.

![Diagram przedstawiający przykładową aplikację usługi API Apps](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Poniżej przedstawiono zrzut ekranu: hello [AngularJS](https://angularjs.org/) frontonu.

![Lista toodo aplikacji przykładowej aplikacji interfejsu API](./media/app-service-api-dotnet-get-started/todospa.png)

Witaj rozwiązania Visual Studio zawiera trzy projekty:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -hello fronton: aplikacja JEDNOSTRONICOWA AngularJS, która wywołuje warstwę środkową hello.
* **ToDoListAPI** -hello warstwa środkowa: projekt interfejsu API sieci Web platformy ASP.NET, który wywołuje warstwę danych hello tooperform operacji CRUD na zadaniach do wykonania.
* **ToDoListDataAPI** -warstwy danych hello: projekt interfejsu API sieci Web platformy ASP.NET, który wykonuje operacje CRUD na zadaniach do wykonania.

architektury trójwarstwowej Hello jest wiele konfiguracji, które można wdrożyć przy użyciu usługi API Apps i jest tu używany tylko w celach demonstracyjnych. Kod Hello w poszczególnych warstwach jest tak proste, jak funkcji API Apps możliwe toodemonstrate; na przykład warstwa danych hello używa pamięci serwera, a nie bazy danych jako mechanizmu stanu trwałego.

Na wykonanie kroków tego samouczka, będziesz mieć hello dwa projekty interfejsu API sieci Web w górę i w chmurze hello w aplikacjach interfejsu API usługi aplikacji.

Następny samouczek Hello w serii hello wdraża hello SPA frontonu toohello chmury.

## <a name="prerequisites"></a>Wymagania wstępne
* Interfejs API sieci Web platformy ASP.NET — hello instrukcjach samouczka założono, że masz podstawową wiedzę na temat tego, jak toowork ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) w programie Visual Studio.
* Konto platformy Azure — możesz [utworzyć konto bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/). W tej lokalizacji możesz od razu utworzyć początkową aplikację o krótkim okresie istnienia w usłudze App Service — **bez karty kredytowej** i bez zobowiązań.
* Visual Studio 2015 z hello [zestawu Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK instaluje automatycznie programu Visual Studio 2015, jeśli nie masz jeszcze go.
  
  * W programie Visual Studio kliknij menu Pomoc -> Informacje o programie Microsoft Visual Studio i upewnij się, że zainstalowano „Narzędzia usługi Azure App Service 2.9.1” lub nowsze.
    
    ![Wersja narzędzi usługi Azure App Service](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > W zależności od tego, jak wiele zależności zestawu SDK hello już istnieje na tym komputerze hello Instalowanie zestawu SDK może zająć dużo czasu, od kilku minut tooa pół godziny lub dłużej.
    > 
    > 

## <a name="download-hello-sample-application"></a>Pobierz hello przykładowej aplikacji
1. Pobierz hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repozytorium.
   
    Możesz kliknąć hello **Pobierz ZIP** przycisk lub sklonować repozytorium hello na komputerze lokalnym.
2. Otwórz rozwiązanie ToDoList hello w Visual Studio 2015 lub 2013.
   
   1. Konieczne będzie tootrust poszczególnych rozwiązań.
         ![Ostrzeżenie o zabezpieczeniach](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Tworzenie pakietów hello rozwiązania (CTRL + SHIFT + B) toorestore hello NuGet.
   
    Jeśli chcesz korzystać z aplikacji hello toosee w operacji przed wdrożeniem, możesz uruchomić je lokalnie. Upewnij się, że ToDoListDataAPI jest projekt startowy, a rozwiązanie hello wykonywania. Błąd HTTP 403 toosee spodziewać w przeglądarce.

## <a name="use-swagger-api-metadata-and-ui"></a>Korzystanie z interfejsu użytkownika oraz metadanych interfejsu API programu Swagger
Usługa Azure App Service zapewnia wbudowaną obsługę metadanych interfejsu API programu [Swagger](http://swagger.io/) 2.0. Każdej aplikacji interfejsu API można określić adres URL punktu końcowego, który zwraca metadane dla hello interfejsu API w formacie JSON programu Swagger. Witaj metadanych zwróconych z tego punktu końcowego może być używany toogenerate kodu klienta.

Projekt interfejsu API sieci Web platformy ASP.NET można dynamicznie generować metadane programu Swagger za pomocą hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pakietu NuGet. Witaj pakietu Swashbuckle NuGet jest już zainstalowana w projektach ToDoListDataAPI i ToDoListAPI hello pobranych.

W tej sekcji samouczka hello przyjrzeć się hello wygenerowany metadane programu Swagger 2.0, a następnie spróbuj można test interfejsu użytkownika, który jest oparty na powitania metadanych struktury Swagger.

1. Ustaw projekt ToDoListDataAPI hello (**nie** hello projekt ToDoListAPI) jako projekt startowy hello.
   
    ![Ustawianie ToDoDataAPI jako projektu startowego](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Naciśnij klawisz F5 lub kliknij przycisk **Debuguj > Rozpocznij debugowanie** toorun hello projektu w trybie debugowania.
   
    Przeglądarka Hello otwiera i pokazuje stronę błędu HTTP 403 hello.
3. Na pasku adresu przeglądarki Dodaj `swagger/docs/v1` koniec toohello hello wiersza i naciśnij klawisz Return. (adres URL jest hello `http://localhost:45914/swagger/docs/v1`.)
   
    Jest to hello domyślny adres URL używany przez pakiet Swashbuckle tooreturn JSON programu Swagger 2.0 metadanych dla hello interfejsu API.
   
    Jeśli używasz programu Internet Explorer, przeglądarka hello monituje toodownload *v1.json* pliku.
   
    ![Pobieranie metadanych JSON w programie Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Jeśli używasz programu Chrome, Firefox lub Microsoft Edge, hello przeglądarka wyświetla hello JSON na powitania okna przeglądarki. Różnych przeglądarkach inaczej obsługi formatu JSON i okna przeglądarki może wyglądać tak samo jak przykład Witaj.
   
    ![Metadane JSON w programie Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Witaj poniższy przykład zawiera pierwszą sekcję hello hello metadanych struktury Swagger dla interfejsu API, hello z definicji hello hello Get, metoda. Te metadane stanowią, jakie hello dysków interfejs użytkownika programu Swagger używane w hello następujące kroki, i użyć go w dalszej części tego samouczka tooautomatically hello generowanie kodu klienta.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Zamknij przeglądarkę hello i Zatrzymaj debugowanie programu Visual Studio.
5. W hello ToDoListDataAPI projektu w **Eksploratora rozwiązań**, otwórz hello *App_Start\SwaggerConfig.cs* plik, a następnie przewiń w dół tooline 174 i usuń znaczniki komentarza hello następującego kodu.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Witaj *SwaggerConfig.cs* pliku jest tworzona podczas instalowania pakietu Swashbuckle hello w projekcie. Plik Hello oferuje następujące sposoby tooconfigure Swashbuckle.
   
    Kod Hello zostały odkomentowana powitalne umożliwia interfejs użytkownika programu Swagger używanego w hello następujące kroki. Podczas tworzenia projektu interfejsu API sieci Web za pomocą szablonu projektu aplikacji hello interfejsu API ten kod jest domyślnie opatrzony ze względów bezpieczeństwa.
6. Uruchom ponownie hello projektu.
7. Na pasku adresu przeglądarki Dodaj `swagger` koniec toohello hello wiersza i naciśnij klawisz Return. (adres URL jest hello `http://localhost:45914/swagger`.)
8. Po wyświetleniu strony interfejs użytkownika programu Swagger powitania kliknij **ToDoList** toosee hello metod.
   
    ![Dostępne metody interfejsu użytkownika programu Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. Najpierw kliknij hello **uzyskać** przycisku hello liście.
10. W hello **parametry** wprowadź gwiazdkę jako wartość hello hello `owner` parametr, a następnie kliknij przycisk **wypróbować jej możliwości**.
    
    Po dodaniu uwierzytelniania w kolejnych samouczkach warstwa środkowa hello będzie udostępniać warstwy danych toohello hello użytkownika rzeczywisty identyfikator. Obecnie wszystkie zadania ma gwiazdki identyfikator właściciela, gdy aplikacja hello działa bez włączonego uwierzytelniania.
    
    ![Próba wyświetlenia interfejsu użytkownika programu Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Hello interfejs użytkownika programu Swagger wywołuje hello metodę Get rozwiązania ToDoList i wyświetla kod odpowiedzi hello i wyniki JSON.
    
    ![Wyniki próby wyświetlenia interfejsu użytkownika programu Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Kliknij przycisk **Post**, a następnie kliknij pole hello w obszarze **schematu modelu**.
    
    Klikając przycisk hello modelu schematu prefills hello pole wprowadzania której można określić wartość parametru hello hello metody Post. (Jeśli to nie pomoże w programie Internet Explorer, użyj innej przeglądarki lub ręcznie wprowadzić wartość parametru hello w następnym kroku hello).  
    
    ![Klikanie przycisku Post podczas próby wyświetlenia interfejsu użytkownika programu Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. Zmień hello JSON w hello `todo` wejściowym parametru, dzięki czemu wygląda hello poniższy przykład lub Zastąp tekst opisu:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Kliknij pozycję **Try it out** (Wypróbuj to).
    
    Witaj interfejs API ToDoList zwraca kod odpowiedzi HTTP 204, co oznacza Powodzenie.
14. Najpierw kliknij hello **uzyskać** przycisk, a następnie w tej sekcji stronie powitania kliknij hello **wypróbować jej możliwości** przycisku.
    
    Witaj odpowiedź metody Get zawiera teraz nowy element toodo hello.
15. Opcjonalnie: Wypróbuj również hello Put, Delete i Get by ID..
16. Zamknij przeglądarkę hello i Zatrzymaj debugowanie programu Visual Studio.

Pakiet Swashbuckle współdziała z dowolnym projektem interfejsu API sieci Web platformy ASP.NET. Tooadd Swagger metadanych generowania tooan istniejący projekt należy zainstalować pakiet Swashbuckle hello.

> [!NOTE]
> Metadane programu Swagger zawierają unikatowy identyfikator dla każdej operacji interfejsu API. Domyślnie pakiet Swashbuckle może generować zduplikowane identyfikatory operacji programu Swagger dla metod kontrolera interfejsu API sieci Web. Dzieje się tak, jeśli kontroler ma skonfigurowane przeciążone metody HTTP, takie jak `Get()` i `Get(id)`. Informacje o sposobie overloads toohandle znajdują się w temacie [definicje API generowanych przez dostosowanie Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md). Jeśli tworzysz projekt interfejsu API sieci Web w programie Visual Studio przy użyciu szablonu aplikacji interfejsu API Azure hello kod służący do generowania unikatowych identyfikatorów operacji jest automatycznie dodawany toohello *SwaggerConfig.cs* pliku.  
> 
> 

## <a id="createapiapp"></a>Tworzenie aplikacji interfejsu API na platformie Azure i wdrażanie tooit kodu
W tej sekcji, użyj narzędzi platformy Azure zintegrowanych z hello Visual Studio **publikowanie w sieci Web** Kreatora aplikacji toocreate nowy interfejs API na platformie Azure. Następnie Wdróż hello ToDoListDataAPI projektu toohello nowej aplikacji interfejsu API i wywołania interfejsu API hello uruchamiając hello interfejs użytkownika programu Swagger.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt ToDoListDataAPI hello, a następnie kliknij przycisk **publikowania**.
   
    ![Klikanie polecenia Opublikuj w programie Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. W hello **profilu** krok hello **publikowanie w sieci Web** kreatora, kliknij przycisk **Microsoft Azure App Service**.
   
   ![Klikanie pozycji Usługa Azure App Service w kreatorze Publikowanie w sieci Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Zaloguj się w tooyour konto platformy Azure, jeśli nie ma jeszcze zrobione, lub Odśwież swoje poświadczenia, jeśli wygasły.
4. W hello usługi aplikacji — okno dialogowe, wybierz hello Azure **subskrypcji** toouse, a następnie kliknij przycisk **nowy**.
   
    ![Klikanie pozycji Nowy w oknie dialogowym App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Witaj **hostingu** kartę hello **Tworzenie usługi App Service** zostanie wyświetlone okno dialogowe.
   
    Ponieważ jest wdrażany projekt interfejsu API sieci Web, z zainstalowanym pakietem swashbuckle, program Visual Studio założono, że toocreate aplikacji interfejsu API. Jest to określane przez hello **Nazwa aplikacji interfejsu API** tytuł i przez hello fakt tego hello **Zmień typ** listy rozwijanej jest ustawiona zbyt**aplikacji interfejsu API**.
   
    ![Typ aplikacji w oknie dialogowym usługi App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. Wprowadź **Nazwa aplikacji interfejsu API** jest unikatowa w hello *azurewebsites.net* domeny. Możesz zaakceptować nazwę domyślną hello sugerowaną przez program Visual Studio.
   
    Wprowadź nazwę, która ktoś inny już użyta, zobaczysz prawo toohello czerwony wykrzyknik.
   
    Witaj adres URL aplikacji hello interfejsu API będzie `{API app name}.azurewebsites.net`.
6. W hello **grupy zasobów** listy rozwijanej kliknij **nowy**, a następnie wprowadź "ToDoListGroup" lub inną nazwę, jeśli wolisz.
   
    Grupa zasobów to kolekcja zasobów platformy Azure, takich jak aplikacje interfejsu API, bazy danych i maszyny wirtualne.    W tym samouczku jest najlepszym toocreate nową grupę zasobów, ponieważ w ten sposób można łatwo toodelete w jednym kroku wszystkich hello zasobów platformy Azure utworzonych w samouczku hello.
   
    To pole pozwala wybrać istniejącą [grupę zasobów](../azure-resource-manager/resource-group-overview.md) lub utworzyć nową przez wpisanie nazwy, która różni się od wszystkich istniejących nazw grup zasobów w subskrypcji użytkownika.
7. Kliknij przycisk hello **nowy** przycisku Dalej toohello **planu usługi App Service** listy rozwijanej.
   
    Witaj zrzut ekranu przedstawia przykładowe wartości **Nazwa aplikacji interfejsu API**, **subskrypcji**, i **grupy zasobów** — wartości będą się różnić.
   
    ![Okno dialogowe Tworzenie usługi App Service](./media/app-service-api-dotnet-get-started/createas.png)
   
    Następujące kroki hello służy do tworzenia planu usługi App Service dla nowej grupy zasobów hello. Plan usługi aplikacji określa hello zasoby obliczeniowe, których używa aplikacja interfejsu API na. Na przykład jeśli wybierzesz warstwę bezpłatna hello, aplikacja interfejsu API będzie działać na udostępnionych maszynach w przypadku niektórych warstw płatnych będzie ona działać na dedykowanych maszyn wirtualnych. Aby uzyskać informacje o planach usługi App Service, zobacz temat [Omówienie planów usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. W hello **Konfigurowanie planu usługi aplikacji** okna dialogowego, jeśli wolisz należy wprowadzić "ToDoListPlan" lub inną nazwę.
9. W hello **lokalizacji** listy rozwijanej wybierz hello lokalizacji, która jest najbliższym tooyou.
   
    To ustawienie służy do określania, w którym centrum danych Azure aplikacja zostanie uruchomiona. Wybierz lokalizację zamknąć tooyou toominimize [opóźnienia](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. W hello **rozmiar** listy rozwijanej kliknij **wolne**.
    
    W tym samouczku hello warstwa cenowa bezpłatna zapewni wystarczającą wydajność.
11. W hello **Konfigurowanie planu usługi App Service** okna dialogowego, kliknij przycisk **OK**.
    
    ![Klikanie przycisku OK w oknie dialogowym Konfigurowanie planu usługi App Service](./media/app-service-api-dotnet-get-started/configasp.png)
12. W hello **Tworzenie usługi App Service** okno dialogowe, kliknij przycisk **Utwórz**.
    
    ![Klikanie przycisku Utwórz w oknie dialogowym Tworzenie usługi App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Program Visual Studio tworzy hello aplikacji interfejsu API i profil publikowania, który zawiera wszystkie ustawienia hello wymagane dla aplikacji hello interfejsu API. Następnie zostanie otwarty hello **publikowanie w sieci Web** kreatora, który zostanie użyty toodeploy hello projektu.
    
    Witaj **publikowanie w sieci Web** na powitania zostanie otwarty Kreator **połączenia** (pokazana poniżej).
    
    Na powitania **połączenia** karcie hello **serwera** i **nazwa witryny** aplikacji interfejsu API punktu tooyour ustawienia. Witaj **nazwy użytkownika** i **hasło** zawierają poświadczenia wdrażania, które tworzy Azure. Po wdrożeniu programu Visual Studio otworzy toohello przeglądarki **docelowy adres URL** (który jest jedynym celem powitania dla **docelowy adres URL**).  
13. Kliknij przycisk **Dalej**.
    
    ![Klikanie przycisku Dalej na karcie Połączenie kreatora Publikowanie w sieci Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    Następna karta Hello jest hello **ustawienia** (pokazana poniżej). W tym miejscu możesz zmienić hello kompilacji konfiguracji kartę toodeploy kompilację debugowania dla [zdalnego debugowania](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Witaj karcie jest również wyświetlonych kilka **opcji publikowania pliku**:
    
    * Usunięcie dodatkowych plików w lokalizacji docelowej
    * Wstępna kompilacja podczas publikowania
    * Wyklucz pliki z folderu App_Data hello
    
    Czynności wykonywane w ramach tego samouczka nie wymagają użycia żadnej z tych opcji. Aby uzyskać szczegółowe wyjaśnienie działania tych opcji, zobacz artykuł [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (Porady: wdrażanie projektu sieci Web przy użyciu publikowania jednym kliknięciem w programie Visual Studio).
14. Kliknij przycisk **Dalej**.
    
    ![Klikanie przycisku Dalej na karcie Ustawienia kreatora Publikowanie w sieci Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    Następnie jest hello **Podgląd** kartę (pokazana poniżej), która umożliwia toosee możliwości, które pliki zostaną skopiowane z projektu aplikacji interfejsu API toohello toobe. Podczas wdrażania projektu aplikacji tooan interfejsu API, już wdrożony tooearlier tylko zmienione pliki są kopiowane. Jeśli chcesz toosee listę, które zostaną skopiowane, możesz kliknąć hello **Uruchom Podgląd** przycisku.
15. Kliknij przycisk **Opublikuj**.
    
    ![Klikanie przycisku Opublikuj na karcie Podgląd kreatora Publikowanie w sieci Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Program Visual Studio wdroży hello ToDoListDataAPI projektu toohello nowej aplikacji interfejsu API. Witaj **dane wyjściowe** okna Dzienniki pomyślne wdrożenie i zostanie wyświetlona strona "został pomyślnie utworzony" w adresie URL toohello otwarte okno przeglądarki w aplikacji hello interfejsu API.
    
    ![Okno danych wyjściowych z informacją o pomyślnym wdrożeniu](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pomyślnie utworzona strona nowej usługi interfejsu API](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Dodaj adres URL toohello "swagger" na pasku adresu przeglądarki hello, a następnie naciśnij klawisz Enter. (adres URL jest hello `http://{apiappname}.azurewebsites.net/swagger`.)
    
    Przeglądarka Hello Wyświetla hello sam interfejs użytkownika programu Swagger, który był wyświetlany poprzednio, ale teraz działa w chmurze hello. Wypróbuj hello metody Get i zobaczysz, że jesteś wstecz toohello domyślne 2 wykonania. zmiany Hello, wprowadzone wcześniej zostały zapisane w pamięci w komputerze lokalnym hello.
17. Otwórz hello [portalu Azure](https://portal.azure.com/).
    
    Hello portalu Azure to interfejs sieci web do zarządzania zasobów platformy Azure, takich jak aplikacje interfejsu API.
18. Kliknij przycisk **Więcej usług > App Services**.
    
    ![Przeglądanie usług App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. W hello **usługi aplikacji** bloku, Znajdź i kliknij nowej aplikacji interfejsu API. (W hello portalu Azure, są nazywane otwartym prawo toohello *bloków*.)
    
    ![Blok App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Zostaną otwarte dwa bloki. Omówienie aplikacji interfejsu API hello ma jednego bloku, a drugi zawiera długą listę ustawień, które można wyświetlać i zmieniać.
20. W hello **ustawienia** bloku, Znajdź hello **interfejsu API** sekcji, a następnie kliknij przycisk **definicji interfejsu API**.
    
    ![Definicja interfejsu API w bloku ustawień](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Witaj **definicji interfejsu API** bloku umożliwia określenie adresu URL hello, która zwraca metadane programu Swagger 2.0 w formacie JSON. W Visual Studio tworzy aplikacji hello interfejsu API, ustawia wartość domyślną toohello adres URL definicji hello interfejsu API podczas Swashbuckle metadanych wygenerowanych był wyświetlany poprzednio, czyli aplikacji hello interfejsu API podstawowy adres URL plus `/swagger/docs/v1`.
    
    ![Adres URL definicji interfejsu API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Po wybraniu kodu klienta interfejsu API aplikacji toogenerate dla niego Visual Studio pobiera metadane hello z tego adresu URL.

## <a id="codegen"></a>Generowanie kodu klienta dla warstwy danych hello
Jedną z zalet integracji programu Swagger interfejsu API Azure aplikacji hello jest automatyczne generowanie kodu. Wygenerowane klasy klienta umożliwiają łatwiejsze toowrite kodu, który wywołuje aplikację interfejsu API.

Projekt ToDoListAPI Hello ma już hello wygenerowany kod klienta, ale w hello następujące kroki będzie ją usunąć i ponownie go wygenerować toosee jak toodo hello generowanie kodu.

1. W programie Visual Studio **Eksploratora rozwiązań**, w hello ToDoListAPI projektu, Usuń hello *ToDoListDataAPI* folderu. **Ostrzeżenie: Usuń tylko folder hello, nie projekt ToDoListDataAPI hello.**
   
    ![Usuwanie wygenerowanego kodu klienta](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Ten folder został utworzony przy użyciu hello proces generowania kodu, który zajmie około toogo za pośrednictwem.
2. Kliknij prawym przyciskiem myszy projekt ToDoListAPI hello, a następnie kliknij przycisk **Dodaj > Klient interfejsu API REST**.
   
    ![Dodawanie klienta interfejsu API REST w programie Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. W hello **Dodawanie klienta interfejsu API REST** okno dialogowe, kliknij przycisk **Swagger URL**, a następnie kliknij przycisk **zasobów Azure wybierz**.
   
    ![Wybieranie elementu zawartości platformy Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. W hello **usługi aplikacji** okno dialogowe, rozwiń grupę zasobów hello używaną na potrzeby tego samouczka i wybierz aplikację interfejsu API, a następnie kliknij **OK**.
   
    ![Wybieranie aplikacji interfejsu API w celu generowania kodu](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Zwróć uwagę, że po powrocie toohello **Dodawanie klienta interfejsu API REST** dialogowym hello pole tekstowe zostało wypełnione definicji interfejsu API hello wartość adresu URL, która była widoczna wcześniej w portalu hello.
   
    ![Adres URL definicji interfejsu API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Metadane tooget alternatywny sposób generowania kodu jest adresem URL hello tooenter bezpośrednio zamiast przechodzenia za pomocą okna dialogowego przeglądania hello. Lub jeśli chcesz toogenerate kod klienta przed wdrożeniem tooAzure można uruchomić lokalnie projekt interfejsu API sieci Web hello, przejdź do adresu URL toohello, który zawiera plik JSON programu Swagger hello, Zapisz plik hello, i użyj hello **wybierz istniejący plik metadanych struktury Swagger**opcji.
   > 
   > 
5. W hello **Dodawanie klienta interfejsu API REST** okno dialogowe, kliknij przycisk **OK**.
   
    Visual Studio tworzy folder o nazwie po aplikacji hello interfejsu API i wygeneruje klasy klienta.
   
    ![Pliki kodu dla wygenerowanego klienta](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. W projekcie ToDoListAPI hello Otwórz *Controllers\ToDoListController.cs* toosee hello kodu w wierszu 40, który wywołuje interfejs API hello za pomocą klienta hello generowane.
   
    powitania po fragment kodu przedstawia sposób hello kod tworzy wystąpienie obiektu klienta hello i wywołania hello metody Get.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    Witaj parametr konstruktora pobiera adres URL punktu końcowego hello z hello `toDoListDataAPIURL` ustawienia aplikacji. W pliku Web.config hello ta wartość jest toohello zestaw lokalnych usług IIS Express adres URL hello interfejsu API projektu, co umożliwia uruchamianie aplikacji hello lokalnie. W przypadku pominięcia parametru konstruktora hello, hello domyślny punkt końcowy jest adres URL hello wygenerowany kod hello z.
7. Zostanie wygenerowana klasa klienta z inną nazwą oparte na nazwę aplikacji interfejsu API; Zmień kod hello w *Controllers\ToDoListController.cs* aby odpowiadały hello Nazwa typu co został wygenerowany w projekcie. Jeśli na przykład aplikacja interfejsu API nosi nazwę ToDoListDataAPI071316, w kodzie:
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Tworzenie aplikacji toohost hello warstwę środkową interfejsu API
Wcześniej należy [utworzeniu aplikacji interfejsu API warstwy danych hello i wdrożeniu tooit kod](#createapiapp).  Po wykonaniu hello tę samą procedurę dla aplikacji interfejsu API warstwy środkowej hello.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello warstwy środkowej ToDoListAPI projektu (nie hello projekt ToDoListDataAPI warstwy danych), a następnie kliknij przycisk **publikowania**.
   
    ![Klikanie polecenia Opublikuj w programie Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. W hello **profilu** kartę hello **publikowanie w sieci Web** kreatora, kliknij przycisk **Microsoft Azure App Service**.
3. W hello **usługi aplikacji** okno dialogowe, kliknij przycisk **nowy**.
4. W hello **hostingu** kartę hello **Tworzenie usługi App Service** okna dialogowego Zaakceptuj domyślne hello **Nazwa aplikacji interfejsu API** lub wprowadź nazwę, która jest unikatowa w hello  *azurewebsites.NET* domeny.
5. Wybierz hello Azure **subskrypcji** był używany.
6. W hello **grupy zasobów** listy rozwijanej, wybierz hello utworzoną wcześniej tej samej grupie zasobów.
7. W hello **Plan usługi App Service** listy rozwijanej, wybierz hello wcześniej utworzony plan. Domyślnie zostanie ustawiona wartość toothat.
8. Kliknij przycisk **Utwórz**.
   
    Visual Studio utworzy aplikację interfejsu API hello, tworzy profil publikowania dla niego i wyświetla hello **połączenia** krok hello **publikowanie w sieci Web** kreatora.
9. W hello **połączenia** krok hello **publikowanie w sieci Web** kreatora, kliknij przycisk **publikowania**.
   
   Visual Studio wdroży hello ToDoListAPI projektu toohello nowej aplikacji interfejsu API i otworzy w przeglądarce toohello adres URL aplikacji interfejsu API hello. zostanie wyświetlona strona powitania "Pomyślnie utworzono".

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Skonfiguruj hello warstwy środkowej toocall hello danych warstwy
Jeśli aplikacji interfejsu API warstwy środkowej hello są teraz nazywane, czy spróbuj użyć warstwę danych hello toocall przy użyciu hello URL localhost, który jest nadal w pliku Web.config hello. W tej sekcji należy wprowadzić adres URL aplikacji interfejsu API warstwy danych hello w ustawień środowiska aplikacji interfejsu API warstwy środkowej hello. Jeśli hello kodu w aplikacji interfejsu API warstwy środkowej hello pobiera ustawienia adresu URL warstwy danych hello, hello ustawienie środowiska zastąpi, co znajduje się w pliku Web.config hello.

1. Przejdź toohello [portalu Azure](https://portal.azure.com/), a następnie przejdź toohello **aplikacji interfejsu API** bloku utworzony projekt TodoListAPI (warstwy środkowej) hello toohost aplikacji hello interfejsu API.
2. W hello aplikacji interfejsu API **ustawienia** bloku, kliknij przycisk **ustawienia aplikacji**.
3. W hello aplikacji interfejsu API **ustawienia aplikacji** bloku, przewiń w dół toohello **ustawień aplikacji** i dodaj następujące hello klucz i wartość. wartość Hello będzie URL hello pierwszy hello opublikowane w tym samouczku aplikacji interfejsu API.
   
   | **Klucz** | toDoListDataAPIURL |
   | --- | --- |
   | **Wartość** |https://{nazwa aplikacji interfejsu API warstwy danych}.azurewebsites.net |
   | **Przykład** |https://todolistdataapi.azurewebsites.net |
4. Kliknij pozycję **Zapisz**.
   
    ![Klikanie pozycji Zapisz w ustawieniach aplikacji](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Witaj kod działa na platformie Azure, ta wartość zastępują teraz hello URL localhost, który znajduje się w pliku Web.config hello.

## <a name="test"></a>Testowanie
1. W oknie przeglądarki przeglądać toohello adres URL hello warstwy środkowej nowej aplikacji interfejsu API, który właśnie utworzony dla projektu ToDoListAPI. Możesz uzyskać klikając adres URL hello w głównym bloku aplikacji hello interfejsu API w portalu hello.
2. Dodaj adres URL toohello "swagger" na pasku adresu przeglądarki hello, a następnie naciśnij klawisz Enter. (adres URL jest hello `http://{apiappname}.azurewebsites.net/swagger`.)
   
    Witaj przeglądarka wyświetla hello sam interfejs użytkownika programu Swagger wyświetlane wcześniej todolistdataapi, ale teraz `owner` nie jest polem wymaganym dla operacji Get hello, ponieważ aplikacja interfejsu API warstwy środkowej hello wysyła tej aplikacji interfejsu API warstwy danych wartości toohello dla Ciebie. (Gdy hello samouczkami dotyczącymi uwierzytelniania, warstwy środkowej hello wysyła rzeczywistych identyfikatorów użytkowników dla hello `owner` parametru; w przypadku teraz go są zakodowane na stałe gwiazdkę.)
3. Wypróbuj hello metody Get i hello toovalidate innych metod, które hello aplikacji interfejsu API warstwy środkowej pomyślnie wywołuje warstwę danych hello aplikacji interfejsu API.
   
    ![Metoda Get interfejsu użytkownika programu Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
W przypadku napotkania problemów podczas pracy z tym samouczkiem skorzystaj z poniższych sugestii dotyczących ich rozwiązywania:

* Upewnij się, że używasz najnowszej wersji hello hello [zestawu Azure SDK dla platformy .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Dwie nazwy projektu hello są podobne (ToDoListAPI i ToDoListDataAPI). Jeśli nie wygląd zgodnie z opisem w instrukcjach hello podczas pracy z projektem, upewnij się, że hello właściwy projekt został otwarty.
* Jeśli komputer znajduje się w sieci firmowej i próbujesz toodeploy tooAzure App Service przez zaporę, upewnij się, że porty 443 i 8172 są otwarte dla narzędzia Web Deploy. W przypadku braku możliwości otwarcia tych portów można użyć innych metod wdrażania.  Zobacz [wdrażanie tooAzure Twojej aplikacji usługi App Service](../app-service-web/web-sites-deploy.md).
* "Nazwy tras muszą być unikatowe" komunikaty o błędach mogą wystąpić, jeśli przypadkowo wdrożono hello niewłaściwy projekt tooan interfejsu API aplikacji, a następnie wdrożono tooit jeden poprawny hello. toocorrect, Wdróż go ponownie hello właściwy projekt toohello interfejsu API aplikacji, a na powitania **ustawienia** kartę hello **publikowanie w sieci Web** kreatora wybierz opcję **Usuń dodatkowe pliki w miejscu docelowym**.

Po utworzeniu aplikacji interfejsu API platformy ASP.NET uruchomionych w usłudze Azure App Service można toolearn więcej informacji na temat funkcji programu Visual Studio, które ułatwiają rozwiązywanie problemów. Aby uzyskać informacje na temat rejestrowania, zdalnego debugowania i innych funkcji, zobacz temat [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) (Rozwiązywanie problemów z aplikacjami Azure App Service w programie Visual Studio).

## <a name="next-steps"></a>Następne kroki
Przedstawiono sposób toodeploy istniejącego interfejsu API sieci Web projektów tooAPI aplikacji, generowanie kodu klienta dla aplikacji interfejsu API i aplikacji interfejsu API przez klientów platformy .NET. Hello następny samouczek z tej serii przedstawiono sposób zbyt[korzystanie z aplikacji interfejsu API tooconsume CORS od klientów JavaScript](app-service-api-cors-consume-javascript.md).

Aby uzyskać więcej informacji na temat generowania kodu klienta, zobacz hello [Azure/AutoRest](https://github.com/azure/autorest) repozytorium w witrynie GitHub.com. Aby uzyskać pomoc dotyczącą problemów za pomocą wygenerowany powitania klienta, otwórz [problemu w repozytorium AutoRest hello](https://github.com/azure/autorest/issues).

Toocreate nowego interfejsu API aplikacji projektów od początku, należy użyć hello **aplikacji interfejsu API Azure** szablonu.

![Szablon aplikacji interfejsu API w programie Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Witaj **aplikacji interfejsu API Azure** szablon projektu jest równoważne toochoosing hello **pusty** ASP.NET 4.5.2 szablonu, klikając hello pole wyboru tooadd interfejsu API sieci Web obsługi i instalowanie hello pakietu Swashbuckle NuGet. Ponadto szablon hello dodaje niektórych Swashbuckle konfiguracji kod tooprevent hello utworzenia zduplikowanych identyfikatorów operacji programu Swagger. Po utworzeniu projektu aplikacji interfejsu API, można ją wdrożyć tooan interfejsu API aplikacji hello sposób opisany w tym samouczku.

