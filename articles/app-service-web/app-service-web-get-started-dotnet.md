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
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="3eea7-103">Tworzenie aplikacji sieci Web platformy ASP.NET na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3eea7-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="3eea7-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="3eea7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="3eea7-105">Ta opcja szybkiego startu przedstawia sposób toodeploy tooAzure aplikacji sieci Web aplikacji sieci web programu ASP.NET pierwszy.</span><span class="sxs-lookup"><span data-stu-id="3eea7-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="3eea7-106">Po zakończeniu będzie istnieć grupa zasobów składająca się z planu usługi App Service i aplikacji internetowej platformy Azure wraz z wdrożoną aplikacją internetową.</span><span class="sxs-lookup"><span data-stu-id="3eea7-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="3eea7-107">Obejrzyj toosee wideo hello tego przewodnika Szybki Start w akcji, a następnie wykonaj hello kroki samodzielnie toopublish pierwszej aplikacji .NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3eea7-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="3eea7-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3eea7-108">Prerequisites</span></span>

<span data-ttu-id="3eea7-109">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="3eea7-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="3eea7-110">Zainstaluj [programu Visual Studio 2017](https://www.visualstudio.com/downloads/) z hello następujące obciążenia:</span><span class="sxs-lookup"><span data-stu-id="3eea7-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="3eea7-111">**Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych**</span><span class="sxs-lookup"><span data-stu-id="3eea7-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="3eea7-112">**Tworzenie aplikacji na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="3eea7-112">**Azure development**</span></span>

    ![Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych oraz tworzenie aplikacji na platformie Azure (w ramach Internetu i chmury)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="3eea7-114">Tworzenie aplikacji sieci Web platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3eea7-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="3eea7-115">W programie Visual Studio utwórz nowy projekt, wybierając pozycję **Plik > Nowy > Projekt**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="3eea7-116">W hello **nowy projekt** okno dialogowe, wybierz opcję **Visual C# > sieci Web > Aplikacja sieci Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="3eea7-117">Nadaj nazwę aplikacji hello _myFirstAzureWebApp_, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Okno dialogowe Nowy projekt](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="3eea7-119">Możesz wdrożyć dowolny typ tooAzure aplikacji sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3eea7-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="3eea7-120">Dla tego przewodnika Szybki Start, wybierz hello **MVC** szablonu i upewnij się, że uwierzytelnianie zostanie ustawiona zbyt**bez uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="3eea7-121">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-121">Select **OK**.</span></span>

![Okno dialogowe Nowy projekt ASP.NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="3eea7-123">Wybierz z hello menu **debugowania > Uruchom bez debugowania** aplikacji sieci web hello toorun lokalnie.</span><span class="sxs-lookup"><span data-stu-id="3eea7-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Uruchamianie aplikacji lokalnie](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="3eea7-125">Publikowanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="3eea7-125">Publish tooAzure</span></span>

<span data-ttu-id="3eea7-126">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **myFirstAzureWebApp** projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publikowanie z Eksploratora rozwiązań](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="3eea7-128">Upewnij się, że pozycja **Microsoft Azure App Service** jest zaznaczona, a następnie kliknij przycisk **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publikowanie ze strony przeglądu projektu](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="3eea7-130">Spowoduje to otwarcie hello **Tworzenie usługi App Service** okno dialogowe, które pomaga w utworzeniu wszystkich aplikacji sieci web serwera hello niezbędnych zasobów Azure toorun hello ASP.NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3eea7-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="3eea7-131">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="3eea7-131">Sign in tooAzure</span></span>

<span data-ttu-id="3eea7-132">W hello **Tworzenie usługi App Service** okno dialogowe, wybierz opcję **Dodaj konto**i zaloguj się na tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3eea7-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="3eea7-133">Jeśli użytkownik jest już zarejestrowany, konto wybierz hello zawierające hello żądana subskrypcję z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="3eea7-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="3eea7-134">Jeśli przeprowadzono już logowanie, nie wybieraj jeszcze pozycji **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Zaloguj się tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="3eea7-136">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="3eea7-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="3eea7-137">Następny zbyt**grupy zasobów**, wybierz pozycję **nowy**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="3eea7-138">Nazwa grupy zasobów hello **myResourceGroup** i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="3eea7-139">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3eea7-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="3eea7-140">Następny zbyt**planu usługi App Service**, wybierz pozycję **nowy**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="3eea7-141">W hello **Konfigurowanie planu usługi App Service** okna dialogowego, użyj ustawień hello w tabeli powitania po hello zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="3eea7-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Tworzenie planu usługi App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="3eea7-143">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="3eea7-143">Setting</span></span> | <span data-ttu-id="3eea7-144">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="3eea7-144">Suggested Value</span></span> | <span data-ttu-id="3eea7-145">Opis</span><span class="sxs-lookup"><span data-stu-id="3eea7-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="3eea7-146">Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3eea7-146">App Service Plan</span></span>| <span data-ttu-id="3eea7-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3eea7-147">myAppServicePlan</span></span> | <span data-ttu-id="3eea7-148">Nazwa planu usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eea7-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="3eea7-149">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="3eea7-149">Location</span></span> | <span data-ttu-id="3eea7-150">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="3eea7-150">West Europe</span></span> | <span data-ttu-id="3eea7-151">gdzie jest hostowana aplikacja sieci web hello Hello centrum danych.</span><span class="sxs-lookup"><span data-stu-id="3eea7-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="3eea7-152">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="3eea7-152">Size</span></span> | <span data-ttu-id="3eea7-153">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="3eea7-153">Free</span></span> | <span data-ttu-id="3eea7-154">[Warstwa cenowa](https://azure.microsoft.com/pricing/details/app-service/) określa funkcje hostowania.</span><span class="sxs-lookup"><span data-stu-id="3eea7-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="3eea7-155">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="3eea7-156">Tworzenie i publikowanie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="3eea7-156">Create and publish hello web app</span></span>

<span data-ttu-id="3eea7-157">W **Nazwa aplikacji sieci Web**, wpisz unikatowej nazwy aplikacji (prawidłowe znaki to `a-z`, `0-9`, i `-`), lub zaakceptuj hello są generowane automatycznie unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="3eea7-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="3eea7-158">adres URL aplikacji sieci web hello Hello jest `http://<app_name>.azurewebsites.net`, gdzie `<app_name>` oznacza nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3eea7-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="3eea7-159">Wybierz **Utwórz** toostart tworzenie hello zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3eea7-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Konfigurowanie nazwy aplikacji sieci Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="3eea7-161">Po zakończeniu pracy Kreatora hello, powoduje ona publikowanie tooAzure aplikacji sieci web ASP.NET hello, a następnie spowoduje uruchomienie hello aplikacji hello domyślnej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="3eea7-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Opublikowana aplikacja sieci Web platformy ASP.NET na platformie Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="3eea7-163">Nazwa aplikacji sieci web Hello określona w hello [tworzenie i publikowanie krok](#create-and-publish-the-web-app) jest używany jako prefiksu adresu URL w formacie hello hello `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3eea7-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="3eea7-164">Gratulacje, Twoja aplikacja internetowa ASP.NET działa w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3eea7-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="3eea7-165">Aktualizacja aplikacji hello i utwórz je ponownie</span><span class="sxs-lookup"><span data-stu-id="3eea7-165">Update hello app and redeploy</span></span>

<span data-ttu-id="3eea7-166">Z hello **Eksploratora rozwiązań**, otwórz _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="3eea7-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="3eea7-167">Znajdź hello `<div class="jumbotron">` HTML tag górze hello i Zastąp cały element hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="3eea7-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="3eea7-168">tooAzure tooredeploy, kliknij prawym przyciskiem myszy hello **myFirstAzureWebApp** projektu w **Eksploratora rozwiązań** i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="3eea7-169">W hello strona publikowania, wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="3eea7-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="3eea7-170">Po zakończeniu publikowania, Visual Studio spowoduje uruchomienie przeglądarki toohello adres URL aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="3eea7-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Zaktualizowana aplikacja sieci Web platformy ASP.NET na platformie Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="3eea7-172">Zarządzanie hello aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3eea7-172">Manage hello Azure web app</span></span>

<span data-ttu-id="3eea7-173">Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="3eea7-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="3eea7-174">Wybierz z menu po lewej stronie powitania **usługi aplikacji**, a następnie wybierz nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3eea7-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="3eea7-176">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="3eea7-176">You see your web app's Overview page.</span></span> <span data-ttu-id="3eea7-177">Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="3eea7-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="3eea7-179">menu po lewej stronie powitania zawiera różne strony konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3eea7-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="3eea7-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3eea7-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3eea7-181">Platforma .ASP.NET z usługą SQL Database</span><span class="sxs-lookup"><span data-stu-id="3eea7-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
