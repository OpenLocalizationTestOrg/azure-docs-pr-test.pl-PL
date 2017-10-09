---
title: aaaCreate platformy ASP.NET sieci web aplikacji na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorun aplikacje sieci web w usłudze Azure App Service, wdrażając domyślne hello ASP.NET web app."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Tworzenie aplikacji sieci Web platformy ASP.NET na platformie Azure

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.  Ta opcja szybkiego startu przedstawia sposób toodeploy tooAzure aplikacji sieci Web aplikacji sieci web programu ASP.NET pierwszy. Po zakończeniu będzie istnieć grupa zasobów składająca się z planu usługi App Service i aplikacji internetowej platformy Azure wraz z wdrożoną aplikacją internetową.

Obejrzyj toosee wideo hello tego przewodnika Szybki Start w akcji, a następnie wykonaj hello kroki samodzielnie toopublish pierwszej aplikacji .NET na platformie Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

* Zainstaluj [programu Visual Studio 2017](https://www.visualstudio.com/downloads/) z hello następujące obciążenia:
    - **Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych**
    - **Tworzenie aplikacji na platformie Azure**

    ![Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych oraz tworzenie aplikacji na platformie Azure (w ramach Internetu i chmury)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Tworzenie aplikacji sieci Web platformy ASP.NET

W programie Visual Studio utwórz nowy projekt, wybierając pozycję **Plik > Nowy > Projekt**. 

W hello **nowy projekt** okno dialogowe, wybierz opcję **Visual C# > sieci Web > Aplikacja sieci Web ASP.NET (.NET Framework)**.

Nadaj nazwę aplikacji hello _myFirstAzureWebApp_, a następnie wybierz **OK**.
   
![Okno dialogowe Nowy projekt](./media/app-service-web-get-started-dotnet/new-project.png)

Możesz wdrożyć dowolny typ tooAzure aplikacji sieci web ASP.NET. Dla tego przewodnika Szybki Start, wybierz hello **MVC** szablonu i upewnij się, że uwierzytelnianie zostanie ustawiona zbyt**bez uwierzytelniania**.
      
Kliknij przycisk **OK**.

![Okno dialogowe Nowy projekt ASP.NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Wybierz z hello menu **debugowania > Uruchom bez debugowania** aplikacji sieci web hello toorun lokalnie.

![Uruchamianie aplikacji lokalnie](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>Publikowanie tooAzure

W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **myFirstAzureWebApp** projekt i wybierz **publikowania**.

![Publikowanie z Eksploratora rozwiązań](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Upewnij się, że pozycja **Microsoft Azure App Service** jest zaznaczona, a następnie kliknij przycisk **Publikuj**.

![Publikowanie ze strony przeglądu projektu](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Spowoduje to otwarcie hello **Tworzenie usługi App Service** okno dialogowe, które pomaga w utworzeniu wszystkich aplikacji sieci web serwera hello niezbędnych zasobów Azure toorun hello ASP.NET na platformie Azure.

## <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

W hello **Tworzenie usługi App Service** okno dialogowe, wybierz opcję **Dodaj konto**i zaloguj się na tooyour subskrypcji platformy Azure. Jeśli użytkownik jest już zarejestrowany, konto wybierz hello zawierające hello żądana subskrypcję z listy rozwijanej hello.

> [!NOTE]
> Jeśli przeprowadzono już logowanie, nie wybieraj jeszcze pozycji **Utwórz**.
>
>
   
![Zaloguj się tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Następny zbyt**grupy zasobów**, wybierz pozycję **nowy**.

Nazwa grupy zasobów hello **myResourceGroup** i wybierz **OK**.

## <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Następny zbyt**planu usługi App Service**, wybierz pozycję **nowy**. 

W hello **Konfigurowanie planu usługi App Service** okna dialogowego, użyj ustawień hello w tabeli powitania po hello zrzut ekranu.

![Tworzenie planu usługi App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Ustawienie | Sugerowana wartość | Opis |
|-|-|-|
|Plan usługi App Service| myAppServicePlan | Nazwa planu usługi aplikacji hello. |
| Lokalizacja | Europa Zachodnia | gdzie jest hostowana aplikacja sieci web hello Hello centrum danych. |
| Rozmiar | Bezpłatna | [Warstwa cenowa](https://azure.microsoft.com/pricing/details/app-service/) określa funkcje hostowania. |

Kliknij przycisk **OK**.

## <a name="create-and-publish-hello-web-app"></a>Tworzenie i publikowanie aplikacji sieci web hello

W **Nazwa aplikacji sieci Web**, wpisz unikatowej nazwy aplikacji (prawidłowe znaki to `a-z`, `0-9`, i `-`), lub zaakceptuj hello są generowane automatycznie unikatową nazwę. adres URL aplikacji sieci web hello Hello jest `http://<app_name>.azurewebsites.net`, gdzie `<app_name>` oznacza nazwę aplikacji sieci web.

Wybierz **Utwórz** toostart tworzenie hello zasobów platformy Azure.

![Konfigurowanie nazwy aplikacji sieci Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

Po zakończeniu pracy Kreatora hello, powoduje ona publikowanie tooAzure aplikacji sieci web ASP.NET hello, a następnie spowoduje uruchomienie hello aplikacji hello domyślnej przeglądarki.

![Opublikowana aplikacja sieci Web platformy ASP.NET na platformie Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

Nazwa aplikacji sieci web Hello określona w hello [tworzenie i publikowanie krok](#create-and-publish-the-web-app) jest używany jako prefiksu adresu URL w formacie hello hello `http://<app_name>.azurewebsites.net`.

Gratulacje, Twoja aplikacja internetowa ASP.NET działa w usłudze Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Aktualizacja aplikacji hello i utwórz je ponownie

Z hello **Eksploratora rozwiązań**, otwórz _Views\Home\Index.cshtml_.

Znajdź hello `<div class="jumbotron">` HTML tag górze hello i Zastąp cały element hello hello następującego kodu:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooAzure tooredeploy, kliknij prawym przyciskiem myszy hello **myFirstAzureWebApp** projektu w **Eksploratora rozwiązań** i wybierz **publikowania**.

W hello strona publikowania, wybierz **publikowania**.

Po zakończeniu publikowania, Visual Studio spowoduje uruchomienie przeglądarki toohello adres URL aplikacji sieci web hello.

![Zaktualizowana aplikacja sieci Web platformy ASP.NET na platformie Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Zarządzanie hello aplikacji sieci web platformy Azure

Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage.

Wybierz z menu po lewej stronie powitania **usługi aplikacji**, a następnie wybierz nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-dotnet/access-portal.png)

Zostanie wyświetlona strona Omówienie aplikacji internetowej. Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. 

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Platforma .ASP.NET z usługą SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md)
