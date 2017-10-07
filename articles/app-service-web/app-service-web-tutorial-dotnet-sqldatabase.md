---
title: "aaaBuild aplikacji ASP.NET na platformie Azure w usłudze SQL Database | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooget ASP.NET aplikacja działa na platformie Azure z tooa połączenia bazy danych SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Tworzenie aplikacji platformy ASP.NET na platformie Azure z bazy danych SQL

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie. W tym samouczku przedstawiono sposób toodeploy platformy ASP.NET opartych na danych aplikacji na platformie Azure w sieci web i połącz go za[bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md). Po zakończeniu, masz aplikację ASP.NET działającą w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) i połączone tooSQL bazy danych.

![Opublikowana aplikacja ASP.NET w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie bazy danych SQL na platformie Azure
> * Połącz tooSQL aplikacji ASP.NET bazy danych
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizacja modelu danych hello i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników z Azure tooyour terminali
> * Zarządzanie aplikacją hello w hello portalu Azure

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

* Zainstaluj [programu Visual Studio 2017](https://www.visualstudio.com/downloads/) z hello następujące obciążenia:
  - **Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych**
  - **Tworzenie aplikacji na platformie Azure**

  ![Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych oraz tworzenie aplikacji na platformie Azure (w ramach Internetu i chmury)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Pobierz przykładowe hello

[Pobierz hello przykładowy projekt](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Wyodrębnij (Rozpakuj) hello *dotnet-sqldb — samouczek master.zip* pliku.

Witaj przykładowy projekt zawiera basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Tworzenie odczytu aktualizowania i usuwania) aplikacji w usłudze [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Uruchamianie aplikacji hello

Otwórz hello *dotnet-sqldb — samouczek — wzorzec/DotNetAppSqlDb.sln* pliku w programie Visual Studio. 

Typ `Ctrl+F5` aplikacji hello toorun bez debugowania. Aplikacja Hello jest wyświetlana w domyślnej przeglądarce. Wybierz hello **Utwórz nowy** link i Utwórz kilka *zadań do wykonania* elementów. 

![Okno dialogowe Nowy projekt ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Test hello **Edytuj**, **szczegóły**, i **usunąć** łącza.

Aplikacja Hello używa tooconnect kontekst bazy danych z bazy danych hello. W tym przykładzie hello kontekst bazy danych używa parametrów połączenia o nazwie `MyDbConnection`. Parametry połączenia Hello jest ustawiany w hello *Web.config* plików i hello zawartymi w *Models/MyDatabaseContext.cs* pliku. Nazwa ciągu połączenia Hello jest używany w dalszej części hello samouczek tooconnect hello Azure web app tooan bazy danych SQL Azure. 

## <a name="publish-tooazure-with-sql-database"></a>Publikowanie tooAzure z bazy danych SQL

W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy użytkownika **DotNetAppSqlDb** projekt i wybierz **publikowania**.

![Publikowanie z Eksploratora rozwiązań](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Upewnij się, że jest zaznaczona usługa **Microsoft Azure App Service**, a następnie kliknij przycisk **Publikuj**.

![Publikowanie ze strony przeglądu projektu](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Publikowanie otwiera hello **Tworzenie usługi App Service** okna dialogowego, które ułatwia tworzenie wszystkich hello zasobów platformy Azure, należy toorun aplikacji sieci web platformy ASP.NET na platformie Azure.

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

W hello **Tworzenie usługi App Service** okna dialogowego, kliknij przycisk **Dodaj konto**, a następnie zaloguj tooyour subskrypcji platformy Azure. Jeśli zalogowano się już do konta Microsoft, upewnij się, że to konto zawiera Twoją subskrypcję platformy Azure. Jeśli hello zalogowanego konta Microsoft nie ma subskrypcji platformy Azure, kliknij go, tooadd hello odpowiedniego konta.
   
![Zaloguj się tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Po zalogowaniu, wszystko jest gotowe toocreate hello wszystkie zasoby, które są potrzebne dla aplikacji sieci web platformy Azure w tym oknie dialogowym.

### <a name="configure-hello-web-app-name"></a>Konfigurowanie nazwy aplikacji sieci web hello

Zachowaj nazwę aplikacji sieci web hello wygenerowany lub zmień ją tooanother unikatową nazwę (prawidłowe znaki to `a-z`, `0-9`, i `-`). Nazwa aplikacji sieci web Hello jest używany jako część hello domyślny adres URL aplikacji (`<app_name>.azurewebsites.net`, gdzie `<app_name>` oznacza nazwę aplikacji sieci web). Nazwa aplikacji sieci web Hello musi toobe unikatowy przez wszystkie aplikacje na platformie Azure. 

![Tworzenie aplikacji usługi z okna dialogowego](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Następny zbyt**grupy zasobów**, kliknij przycisk **nowy**.

![Następny tooResource grupy, kliknij przycisk Nowy.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Nazwa grupy zasobów hello **myResourceGroup**.

> [!NOTE]
> Nie klikaj pozycji **Utwórz**. Należy najpierw tooset bazy danych SQL w późniejszym kroku.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Następny zbyt**planu usługi App Service**, kliknij przycisk **nowy**. 

W hello **Konfigurowanie planu usługi aplikacji** okna dialogowego, skonfigurować nowy plan usługi aplikacji hello hello następujące ustawienia:

![Tworzenie planu usługi App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Ustawienie  | Sugerowana wartość | Aby uzyskać więcej informacji |
| ----------------- | ------------ | ----|
|**Plan usługi aplikacji**| myAppServicePlan | [Plany usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Lokalizacja**| Europa Zachodnia | [Regiony platformy Azure](https://azure.microsoft.com/regions/) |
|**Rozmiar**| Bezpłatna | [Warstwa cenowa](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Utwórz wystąpienie programu SQL Server

Przed utworzeniem bazy danych, należy [serwera logicznego bazy danych SQL Azure](../sql-database/sql-database-features.md). Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa.

Wybierz **Eksploruj dodatkowych usług Azure**.

![Konfigurowanie nazwy aplikacji sieci Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

W hello **usług** , kliknij pozycję hello  **+**  ikona dalej zbyt**bazy danych SQL**. 

![Na karcie usług hello, kliknij przycisk Witaj + ikonę dalej tooSQL bazy danych.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

W hello **Konfigurowanie bazy danych SQL** okna dialogowego, kliknij przycisk **nowy** dalej zbyt**programu SQL Server**. 

Generowany jest unikatową nazwą serwera. Ta nazwa jest używana jako część hello domyślny adres URL dla serwera logicznego, `<server_name>.database.windows.net`. Musi być unikatowa we wszystkich wystąpieniach serwera logicznego w systemie Azure. Możesz zmienić nazwę serwera hello, ale w tym samouczku, należy zachować wartość hello wygenerowany.

Dodaj użytkownika administratora i hasło, a następnie wybierz **OK**. Wymagania dotyczące złożoności hasła, aby zapoznać [zasady haseł](/sql/relational-databases/security/password-policy).

Należy pamiętać, ta nazwa użytkownika i hasło. Należy je serwera logicznego toomanage hello później wystąpienia.

![Utwórz wystąpienie programu SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Tworzenie bazy danych SQL

W hello **Konfigurowanie bazy danych SQL** okna dialogowego: 

* Zachowaj domyślne hello wygenerowany **Nazwa bazy danych**.
* W **Nazwa ciągu połączenia**, typ *MyDbConnection*. Ta nazwa musi być zgodna hello parametry połączenia, do którego odwołuje się w *Models/MyDatabaseContext.cs*.
* Kliknij przycisk **OK**.

![Skonfiguruj bazę danych SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Witaj **Tworzenie usługi App Service** okna dialogowego pokazuje hello zasoby po utworzeniu. Kliknij przycisk **Utwórz**. 

![Witaj zasoby, które zostały utworzone](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Po hello zakończeniu pracy Kreatora tworzenia hello Azure zasobów publikuje tooAzure aplikacji programu ASP.NET. Domyślnej przeglądarki jest uruchomiona z hello adresu URL toohello wdrożonych aplikacji. 

Dodaj kilka elementów do wykonania.

![Opublikowana aplikacja ASP.NET w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Gratulacje! Aplikacja ASP.NET opartych na danych jest uruchomiona na żywo w usłudze Azure App Service.

## <a name="access-hello-sql-database-locally"></a>Dostęp lokalnie hello bazy danych SQL

Program Visual Studio umożliwia Eksplorowanie i zarządzanie nimi z nowej bazy danych SQL, łatwo w hello **Eksplorator obiektów SQL Server**.

### <a name="create-a-database-connection"></a>Utwórz połączenie z bazą danych

Z hello **widoku** menu, wybierz opcję **Eksplorator obiektów SQL Server**.

U góry hello **Eksplorator obiektów SQL Server**, kliknij przycisk hello **dodawania serwera SQL** przycisku.

### <a name="configure-hello-database-connection"></a>Skonfiguruj połączenie bazy danych hello

W hello **Connect** okna dialogowego, rozwiń węzeł hello **Azure** węzła. Swoich wystąpień bazy danych SQL platformy Azure są wyświetlane tutaj.

Wybierz hello `DotNetAppSqlDb` bazy danych SQL. połączenie Hello, utworzony wcześniej jest automatycznie wypełniane u dołu hello.

Wpisz hasło administratora bazy danych hello utworzone wcześniej, a następnie kliknij przycisk **Connect**.

![Skonfiguruj połączenie bazy danych z programu Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Zezwalaj na połączenia klienckie z komputera

Witaj **Utwórz nową regułę zapory** otworzyć okna dialogowego. Domyślnie wystąpienia bazy danych SQL umożliwia tylko połączeń z usługami Azure, takich jak aplikacji sieci web platformy Azure. tooconnect tooyour bazy danych, należy utworzyć regułę zapory w hello wystąpienie bazy danych SQL. Witaj, reguła zapory zezwala na powitania publicznego adresu IP komputera lokalnego.

okno dialogowe Hello jest już wypełniony publiczny adres IP komputera.

Upewnij się, że **Dodaj mój adres IP klienta** jest zaznaczone, a następnie kliknij przycisk **OK**. 

![Ustaw zapory dla wystąpienia bazy danych SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Gdy program Visual Studio zakończy tworzenie hello ustawień zapory dla swojego wystąpienia bazy danych SQL, połączenia zostaną wyświetlone w **Eksplorator obiektów SQL Server**.

W tym miejscu można wykonywać hello najczęściej bazy danych operacji, takich jak wykonywania zapytania, Utwórz widoki i procedury składowane i inne. 

Kliknij prawym przyciskiem myszy na powitania `Todoes` tabeli i wybierz **danych widoku**. 

![Eksploruj obiektów bazy danych SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Aktualizowanie aplikacji z migracje Code First

Można użyć znanych narzędzi hello w Visual Studio tooupdate aplikacji sieci web i bazy danych na platformie Azure. W tym kroku migracje Code First jest używany w toomake Entity Framework zmiany schematu bazy danych tooyour i opublikować go tooAzure.

Aby uzyskać więcej informacji o używaniu migracje Code First Framework jednostki, zobacz [wprowadzenie do programu Entity Framework 6 Code First przy użyciu MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="update-your-data-model"></a>Aktualizacja modelu danych

Otwórz _Models\Todo.cs_ hello edytora kodu. Dodaj następujące właściwości toohello hello `ToDo` klasy:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Uruchom lokalnie migracje Code First

Uruchom kilka poleceń toomake aktualizacje tooyour lokalnej bazy danych. 

Z hello **narzędzia** menu, kliknij przycisk **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**.

W oknie konsoli Menedżera pakietów hello należy włączyć migracje Code First:

```PowerShell
Enable-Migrations
```

Dodaj migracji:

```PowerShell
Add-Migration AddProperty
```

Aktualizacja hello lokalnej bazy danych:

```PowerShell
Update-Database
```

Typ `Ctrl+F5` toorun hello aplikacji. Test hello Edytuj szczegóły i utworzyć łącza.

Jeśli aplikacja hello ładuje bez błędów, następnie migracje Code First zakończyła się pomyślnie. Jednak Twój nadal wygląd strony hello sam ponieważ logiki aplikacji nie korzysta z tej nowej właściwości jeszcze. 

### <a name="use-hello-new-property"></a>Użyj hello nowej właściwości.

Niektóre zmiany w Twojej hello toouse kodu `Done` właściwości. Dla uproszczenia w tym samouczku, tylko będzie toochange hello `Index` i `Create` widoków toosee hello właściwości działania.

Otwórz _Controllers\TodosController.cs_.

Znajdź hello `Create()` — metoda i Dodaj `Done` toohello listę właściwości w hello `Bind` atrybutu. Gdy wszystko będzie gotowe, Twoje `Create()` podpis metody wygląda hello następującego kodu:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Otwórz _Views\Todos\Create.cshtml_.

W kodzie Razor hello, powinna zostać wyświetlona `<div class="form-group">` element, który używa `model.Description`, a następnie inne `<div class="form-group">` element, który używa `model.CreatedDate`. Bezpośrednio po tych dwóch elementów, dodać kolejne `<div class="form-group">` element, który używa `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Otwórz _Views\Todos\Index.cshtml_.

Wyszukaj hello pusty `<th></th>` elementu. Powyżej tego elementu Dodaj następującego kodu Razor hello:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Znajdź hello `<td>` element, który zawiera hello `Html.ActionLink()` metody pomocnicze. Powyżej tego elementu Dodaj następującego kodu Razor hello:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

To już wszystko, czego potrzebujesz toosee zmiany hello hello `Index` i `Create` widoków. 

Typ `Ctrl+F5` toorun hello aplikacji.

Można teraz dodać element do wykonania i sprawdzić **gotowe**. Następnie go powinny być widoczne w strony głównej jako element ukończone. Należy pamiętać, że hello `Edit` widoku nie wyświetla hello `Done` pól, ponieważ nie zmieniły hello `Edit` widoku.

### <a name="enable-code-first-migrations-in-azure"></a>Włącz migracje Code First na platformie Azure

Teraz, gdy kod działa, łącznie z migracji bazy danych zmian opublikowania go w aplikacji sieci web platformy Azure tooyour i zbyt aktualizacji bazy danych SQL z migracje Code First.

Tak jak wcześniej, kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.

Kliknij przycisk **ustawienia** tooopen hello Kreator publikowania.

![Otwórz ustawienia publikowania](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

W Kreatorze powitania kliknij **dalej**.

Sprawdź, czy te parametry połączenia hello w bazie danych SQL została wpisana **MyDatabaseContext (MyDbConnection)**. Może być konieczne tooselect hello **myToDoAppDb** bazy danych z listy rozwijanej hello. 

Wybierz **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**, następnie kliknij przycisk **zapisać**.

![Włącz migracje Code First w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Opublikuj zmiany

Skoro migracje Code First jest włączone w aplikacji sieci web platformy Azure, Opublikuj zmiany kodu.

W hello strona publikowania, kliknij przycisk **publikowania**.

Spróbuj ponownie dodać elementów do wykonania i wybierz **gotowe**, i powinny być widoczne w strony głównej jako element ukończone.

![Aplikacja sieci web platformy Azure po zakończeniu migracji pierwszy kodu](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Nadal wyświetlane są wszystkie istniejące elementy zadań do wykonania. Istniejące dane w bazie danych SQL ponownie opublikować aplikację ASP.NET nie zostaną utracone. Ponadto migracje Code First zmienia tylko schemat danych hello i pozostawienie bez zmian do istniejących danych.


## <a name="stream-application-logs"></a>Strumieniowe przesyłanie dzienników aplikacji

Bezpośrednio z programu tooVisual aplikacji sieci web platformy Azure Studio można przesłać strumieniowo śledzenia wiadomości.

Otwórz _Controllers\TodosController.cs_.

Każda akcja rozpoczyna się od `Trace.WriteLine()` metody. Ten kod jest dodawany tooshow należy jak tooadd śledzenia komunikatów tooyour aplikacji sieci web platformy Azure.

### <a name="open-server-explorer"></a>W Eksploratorze serwera Otwórz

Z hello **widoku** menu, wybierz opcję **Eksploratora serwera**. Można skonfigurować rejestrowanie dla aplikacji sieci web platformy Azure na **Eksploratora serwera**. 

### <a name="enable-log-streaming"></a>Przesyłania strumieniowego dzienników

W **Eksploratora serwera**, rozwiń węzeł **Azure** > **usługi aplikacji**.

Rozwiń węzeł hello **myResourceGroup** grupy zasobów utworzone podczas tworzenia aplikacji sieci web platformy Azure hello.

Kliknij prawym przyciskiem myszy aplikację sieci web platformy Azure i wybierz **Wyświetl dzienniki przesyłania strumieniowego**.

![Przesyłania strumieniowego dzienników](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Witaj dzienniki są teraz przesyłane strumieniowo do hello **dane wyjściowe** okna. 

![Dziennik przesyłania strumieniowego w oknie danych wyjściowych](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Jednak nie widzisz tych wiadomości powitania śledzenia jeszcze. To jest ponieważ najpierw wybranie **Wyświetl dzienniki przesyłania strumieniowego**, aplikacji sieci web platformy Azure ustawia poziom śledzenia hello zbyt`Error`, która rejestruje tylko zdarzenia błędów (z hello `Trace.TraceError()` — metoda).

### <a name="change-trace-levels"></a>Zmień poziomy śledzenia

toochange hello śledzenia poziomy toooutput inne komunikaty śledzenia, przejdź wstecz zbyt**Eksploratora serwera**.

Ponownie kliknij prawym przyciskiem myszy aplikację sieci web platformy Azure i wybierz **ustawienia**.

W hello **rejestrowania aplikacji (w systemie plików)** listy rozwijanej wybierz **pełne**. Kliknij pozycję **Zapisz**.

![TooVerbose poziomu śledzenia zmian](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Możesz eksperymentować z toosee poziomy śledzenia różne rodzaje komunikaty są wyświetlane dla każdego poziomu. Na przykład Witaj **informacji** poziom obejmuje wszystkie dzienniki utworzone przez `Trace.TraceInformation()`, `Trace.TraceWarning()`, i `Trace.TraceError()`, ale nie Dzienniki tworzone przez `Trace.WriteLine()`.
>
>

W przeglądarce spróbuj kliknięcie wokół hello aplikację listy zadań do wykonania na platformie Azure. wiadomości powitania śledzenia są teraz przesyłane strumieniowo toohello **dane wyjściowe** okna w programie Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Zatrzymaj dzienników przesyłania strumieniowego

toostop hello przesyłania strumieniowego dzienników usługi, kliknij przycisk hello **zatrzymać monitorowanie** przycisku na powitania **dane wyjściowe** okna.

![Zatrzymaj dzienników przesyłania strumieniowego](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Zarządzanie aplikacji sieci web platformy Azure

Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toosee został utworzony. 



W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Jest strony aplikacji sieci web. 

Domyślnie hello portal pokazuje hello **omówienie** strony. Ta strona udostępnia widok sposobu działania aplikacji. Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. Witaj w lewej części strony hello hello kartach hello innej konfiguracji stron, które można otworzyć. 

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie bazy danych SQL na platformie Azure
> * Połącz tooSQL aplikacji ASP.NET bazy danych
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizacja modelu danych hello i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników z Azure tooyour terminali
> * Zarządzanie aplikacją hello w hello portalu Azure

Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy toohello aplikacji sieci web.

> [!div class="nextstepaction"]
> [Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-domain.md)
