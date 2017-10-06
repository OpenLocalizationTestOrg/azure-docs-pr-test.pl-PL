---
title: "aaaCreate aplikacji Azure — biznesowych, przy użyciu uwierzytelniania usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate ASP.NET MVC — biznesowych aplikacji w usłudze Azure App Service który jest uwierzytelniany w usłudze Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="436b4-103">Tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="436b4-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="436b4-104">W tym artykule opisano sposób toocreate .NET — biznesowych aplikacji w [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) przy użyciu hello [uwierzytelniania / autoryzacji](../app-service/app-service-authentication-overview.md) funkcji.</span><span class="sxs-lookup"><span data-stu-id="436b4-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="436b4-105">Zawiera także sposób toouse hello [interfejsu API usługi Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery katalogu danych w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="436b4-106">dzierżawy usługi Azure Active Directory Hello, którego używasz, może być katalogu tylko do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="436b4-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="436b4-107">Lub może być [synchronizowane z lokalnej usługi Active Directory](../active-directory/active-directory-aadconnect.md) toocreate pojedynczego jednokrotnego pracowników, które są lokalne i zdalne.</span><span class="sxs-lookup"><span data-stu-id="436b4-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="436b4-108">W tym artykule używa hello domyślny katalog dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="436b4-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="436b4-109">Zostanie utworzona</span><span class="sxs-lookup"><span data-stu-id="436b4-109">What you will build</span></span>
<span data-ttu-id="436b4-110">Będzie utworzyć prostą aplikację Utwórz-odczytu-aktualizowania i usuwania (CRUD)-biznesowych w aplikacji usługi sieci Web aplikacji czy śledzi elementy robocze z hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="436b4-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="436b4-111">Uwierzytelnia użytkowników w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="436b4-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="436b4-112">Wysyła zapytanie do katalogu użytkowników i grup za pomocą [interfejsu API usługi Azure Active Directory Graph](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="436b4-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="436b4-113">Użyj hello ASP.NET MVC *bez uwierzytelniania* szablonu</span><span class="sxs-lookup"><span data-stu-id="436b4-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="436b4-114">Jeśli potrzebujesz kontroli dostępu opartej na rolach (RBAC) dla aplikacji biznesowych z platformy Azure, zobacz [następnego kroku](#next).</span><span class="sxs-lookup"><span data-stu-id="436b4-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="436b4-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="436b4-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="436b4-116">Po toocomplete muszą hello w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="436b4-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="436b4-117">Dzierżawy usługi Azure Active Directory z użytkownikami w różnych grupach</span><span class="sxs-lookup"><span data-stu-id="436b4-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="436b4-118">Uprawnienia aplikacji toocreate na powitania dzierżawy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="436b4-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="436b4-119">Visual Studio 2013 Update 4 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="436b4-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="436b4-120">Zestaw Azure SDK 2.8.1 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="436b4-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="436b4-121">Tworzenie i wdrażanie tooAzure aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="436b4-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="436b4-122">W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="436b4-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="436b4-123">Wybierz **aplikacji sieci Web ASP.NET**, nazwę projektu i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="436b4-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="436b4-124">Wybierz hello **MVC** szablonu, zmień uwierzytelnianie hello zbyt**bez uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="436b4-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="436b4-125">Upewnij się, że **hosta w chmurze hello** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="436b4-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="436b4-126">W hello **Tworzenie usługi App Service** okna dialogowego, kliknij przycisk **Dodaj konto** (i następnie **Dodaj konto** w listy rozwijanej hello) toolog w tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="436b4-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="436b4-127">Po zalogowaniu skonfigurować aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="436b4-127">Once logged in configure your web app.</span></span> <span data-ttu-id="436b4-128">Utwórz grupę zasobów i nowy plan usługi aplikacji, klikając hello odpowiednich **nowy** przycisku.</span><span class="sxs-lookup"><span data-stu-id="436b4-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="436b4-129">Kliknij przycisk **Eksploruj dodatkowych usług Azure** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="436b4-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="436b4-130">W hello **usług** , kliknij pozycję  **+**  tooadd bazy danych SQL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="436b4-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="436b4-131">W **Konfigurowanie bazy danych SQL**, kliknij przycisk **nowy** toocreate wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="436b4-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="436b4-132">W **Konfiguruj serwer SQL**, skonfiguruj wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="436b4-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="436b4-133">Następnie kliknij przycisk **OK**, **OK**, i **Utwórz** tookick poza tworzenie aplikacji hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="436b4-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="436b4-134">W **działanie usługi Azure App Service**, zobacz temat po zakończeniu tworzenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="436b4-135">Kliknij przycisk  **publikowania &lt;* appname*> toothis aplikacji sieci Web teraz **, następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="436b4-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="436b4-136">Po zakończeniu pracy programu Visual Studio zostanie otwarte hello opublikować aplikację w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="436b4-137">Konfigurowanie uwierzytelniania i katalog dostępu</span><span class="sxs-lookup"><span data-stu-id="436b4-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="436b4-138">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="436b4-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="436b4-139">W menu po lewej stronie powitania kliknij **usługi aplikacji** > **&lt;*appname*> ** > **uwierzytelniania / autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="436b4-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="436b4-140">Włącz uwierzytelnianie usługi Azure Active Directory, klikając **na** > **usługi Azure Active Directory** > **Express**  >   **OK**.</span><span class="sxs-lookup"><span data-stu-id="436b4-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="436b4-141">Kliknij przycisk **zapisać** na pasku poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="436b4-142">Ustawienia uwierzytelniania hello są zapisane pomyślnie, spróbuj Nawigacja aplikacji tooyour ponownie w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="436b4-143">Domyślnych ustawień wymusić uwierzytelnianie na powitania całej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="436b4-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="436b4-144">Jeśli użytkownik nie jest już zalogowany, to przekierowanego tooa ekran logowania.</span><span class="sxs-lookup"><span data-stu-id="436b4-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="436b4-145">Po zalogowaniu, zapoznaj się aplikacji zabezpieczonej przez protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="436b4-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="436b4-146">Następnie należy tooenable dostępu toodirectory danych.</span><span class="sxs-lookup"><span data-stu-id="436b4-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="436b4-147">Przejdź toohello [klasyczny portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="436b4-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="436b4-148">W menu po lewej stronie powitania kliknij **usługi Active Directory** > **katalog domyślny** > **aplikacji**  >   **&lt;* appname*> **.</span><span class="sxs-lookup"><span data-stu-id="436b4-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="436b4-149">To jest aplikacja hello Azure Active Directory, usługi aplikacji utworzony dla możesz tooenable hello autoryzacji / funkcji uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="436b4-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="436b4-150">Kliknij przycisk **użytkowników** i **grup** toomake się, że niektóre użytkowników i grup w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="436b4-151">Jeśli nie, należy utworzyć kilka użytkowników testowych i grup.</span><span class="sxs-lookup"><span data-stu-id="436b4-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="436b4-152">Kliknij przycisk **Konfiguruj** tooconfigure tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="436b4-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="436b4-153">Przewiń w dół toohello **klucze** sekcji, a następnie dodaj klucz wybierając czas trwania.</span><span class="sxs-lookup"><span data-stu-id="436b4-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="436b4-154">Następnie kliknij przycisk **delegowane uprawnienia** i wybierz **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="436b4-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="436b4-155">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="436b4-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="436b4-156">Po zapisaniu ustawień przewiń Utwórz kopię zapasową toohello **klucze** sekcji, a następnie kliknij przycisk hello **kopiowania** przycisk toocopy powitania klienta klucza.</span><span class="sxs-lookup"><span data-stu-id="436b4-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="436b4-157">Jeśli opuścisz tę stronę teraz, nie będzie możliwe tooaccess tego klienta klucza kiedykolwiek ponownie.</span><span class="sxs-lookup"><span data-stu-id="436b4-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="436b4-158">Następnie należy tooconfigure aplikacji sieci web przy użyciu tego klucza.</span><span class="sxs-lookup"><span data-stu-id="436b4-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="436b4-159">Zaloguj się za toohello [Eksploratora zasobów Azure](https://resources.azure.com) z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="436b4-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="436b4-160">U góry hello hello strony, kliknij przycisk **odczytu/zapisu** toomake zmiany hello Eksploratora zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="436b4-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="436b4-161">Znajdź hello ustawienia uwierzytelniania dla aplikacji, znajdujący się w subskrypcji >  **&lt;* Nazwa subskrypcji*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **dostawców** > **Microsoft.Web**  >  **witryny** > **&lt;*appname*> ** > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="436b4-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="436b4-162">Kliknij pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="436b4-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="436b4-163">W hello edycji okienku, ustaw hello `clientSecret` i `additionalLoginParams` właściwości w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="436b4-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="436b4-164">Kliknij przycisk **Put** na hello top toosubmit zmiany.</span><span class="sxs-lookup"><span data-stu-id="436b4-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="436b4-165">Teraz, tootest, jeśli masz autoryzacji hello token tooaccess hello Azure Active Directory interfejsu API programu Graph, przejdź do  **https://&lt;*appname*>.azurewebsites.net/.auth/me** w sieci Przeglądarka.</span><span class="sxs-lookup"><span data-stu-id="436b4-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="436b4-166">Jeśli skonfigurowano wszystko poprawnie, powinny pojawić się hello `access_token` właściwości w hello odpowiedź w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="436b4-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="436b4-167">Hello `~/.auth/me` ścieżki adresu URL jest zarządzana przez aplikację usługi uwierzytelniania / autoryzacji toogive możesz wszystkich hello informacje dotyczące sesji tooyour uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="436b4-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="436b4-168">Aby uzyskać więcej informacji, zobacz [uwierzytelnianie i autoryzację w usłudze Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="436b4-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="436b4-169">Witaj `access_token` ma okres ważności.</span><span class="sxs-lookup"><span data-stu-id="436b4-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="436b4-170">Jednak aplikacja usługi uwierzytelniania / autoryzacji zawiera token odświeżania funkcji z `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="436b4-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="436b4-171">Aby uzyskać więcej informacji na temat toouse, zobacz [sklepu z aplikacjami usługi tokenu](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="436b4-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="436b4-172">Następnie zostanie Zrób coś, które są przydatne w przypadku danych katalogu.</span><span class="sxs-lookup"><span data-stu-id="436b4-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="436b4-173">Dodaj aplikację tooyour biznesowych — funkcja</span><span class="sxs-lookup"><span data-stu-id="436b4-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="436b4-174">Można teraz utworzyć prosty śledzenia elementów roboczych CRUD.</span><span class="sxs-lookup"><span data-stu-id="436b4-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="436b4-175">W folderze ~\Models hello, Utwórz plik klasy o nazwie WorkItem.cs i Zastąp `public class WorkItem {...}` z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="436b4-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="436b4-176">przy użyciu System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="436b4-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="436b4-177">Klasa publiczna {elementu pracy</span><span class="sxs-lookup"><span data-stu-id="436b4-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="436b4-178">}</span><span class="sxs-lookup"><span data-stu-id="436b4-178">}</span></span>
   
     <span data-ttu-id="436b4-179">Wyliczenie publiczne WorkItemStatus {</span><span class="sxs-lookup"><span data-stu-id="436b4-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="436b4-180">}</span><span class="sxs-lookup"><span data-stu-id="436b4-180">}</span></span>
2. <span data-ttu-id="436b4-181">Tworzenie toomake projektu hello nowego modelu dostępny toohello szkieletów logiki w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="436b4-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="436b4-182">Dodaj nowy element szkieletu `WorkItemsController` toohello ~\Controllers folder (kliknij prawym przyciskiem myszy **kontrolerów**, punktu zbyt**Dodaj**i wybierz **nowy element szkieletu**).</span><span class="sxs-lookup"><span data-stu-id="436b4-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="436b4-183">Wybierz **kontroler MVC 5 z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="436b4-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="436b4-184">Wybierz hello modelu, który został utworzony, następnie kliknij przycisk  **+**  , a następnie **Dodaj** tooadd kontekstu danych, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="436b4-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="436b4-185">W ~\Views\WorkItems\Create.cshtml (element automatycznie szkieletu), Znajdź hello `Html.BeginForm` metody pomocniczej i wprowadź następujące zmiany wyróżnione hello:</span><span class="sxs-lookup"><span data-stu-id="436b4-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="436b4-186">Należy pamiętać, że `token` i `tenant` są używane przez hello `AadPicker` toomake obiektu wywołuje interfejs API usługi Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="436b4-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="436b4-187">Należy dodać `AadPicker` później.</span><span class="sxs-lookup"><span data-stu-id="436b4-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="436b4-188">Równie dobrze Ci `token` i `tenant` z powitania po stronie klienta z `~/.auth/me`, ale ten będzie wywołanie dodatkowego serwera.</span><span class="sxs-lookup"><span data-stu-id="436b4-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="436b4-189">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="436b4-189">For example:</span></span>
   > 
   > <span data-ttu-id="436b4-190">$.ajax ({typ danych: "json", adres url: "/.auth/me", powodzenia: funkcji (dane) {var token = danych [0] .access_token; var dzierżawy = .find .user_claims danych [0] (c = > c.typ === "http://schemas.microsoft.com/identity/claims/tenantid") .val;}});</span><span class="sxs-lookup"><span data-stu-id="436b4-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="436b4-191">Zmiany hello tego samego z ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="436b4-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="436b4-192">Witaj `AadPicker` obiektu jest zdefiniowana w skrypcie konieczność tooadd tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="436b4-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="436b4-193">Kliknij prawym przyciskiem myszy hello ~\Scripts folder, wskaż zbyt**Dodaj**i kliknij przycisk **plik JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="436b4-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="436b4-194">Typ `AadPickerLibrary` hello nazwę pliku, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="436b4-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="436b4-195">Skopiuj zawartość hello [tutaj](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) do ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="436b4-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="436b4-196">W skrypcie hello hello `AadPicker` obiektu wywołania [interfejsu API usługi Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch dla użytkowników i grup spełniających hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="436b4-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="436b4-197">~\Scripts\AadPickerLibrary.js używa również hello [widget autouzupełniania interfejsu użytkownika jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="436b4-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="436b4-198">Należy więc projekt tooyour interfejsu użytkownika jQuery tooadd.</span><span class="sxs-lookup"><span data-stu-id="436b4-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="436b4-199">Kliknij prawym przyciskiem myszy projekt w, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="436b4-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="436b4-200">W hello Menedżera pakietów NuGet, kliknij przycisk Przeglądaj, typ **interfejsu użytkownika jquery** w hello pasek wyszukiwania i kliknij przycisk **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="436b4-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="436b4-201">W okienku po prawej stronie powitania, kliknij przycisk **zainstalować**, następnie kliknij przycisk **OK** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="436b4-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="436b4-202">Otwórz ~\App_Start\BundleConfig.cs i wprowadź następujące zmiany wyróżnione hello:</span><span class="sxs-lookup"><span data-stu-id="436b4-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="436b4-203">Istnieje więcej toomanage sposoby wydajności JavaScript i plików CSS w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="436b4-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="436b4-204">Jednak dla uproszczenia chcesz po prostu zacząć toopiggyback na powitania pakiety, które są ładowane z każdego widoku.</span><span class="sxs-lookup"><span data-stu-id="436b4-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="436b4-205">Ponadto w ~ \Global.asax, Dodaj powitania po wierszu kodu w hello `Application_Start()` metody.</span><span class="sxs-lookup"><span data-stu-id="436b4-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="436b4-206">`Ctrl`+`.`na każdym nazewnictwa błędów rozpoznawania nazw za napraw go.</span><span class="sxs-lookup"><span data-stu-id="436b4-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="436b4-207">Należy ten wiersz kodu, ponieważ korzysta z domyślnego szablonu MVC hello <code>[ValidateAntiForgeryToken]</code> decoration w przypadku niektórych działań hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="436b4-208">Ze względu na zachowanie toohello opisanego przez [Allen firmy Brock](https://twitter.com/BrockLAllen) w [MVC 4, AntiForgeryToken i oświadczeń](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) Twojego HTTP POST może zakończyć się niepowodzeniem sprawdzania poprawności tokenu zabezpieczającego przed sfałszowaniem, ponieważ:</span><span class="sxs-lookup"><span data-stu-id="436b4-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="436b4-209">Usługa Azure Active Directory nie wysyła http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, co jest wymagane domyślnie przez token zabezpieczający przed sfałszowaniem hello.</span><span class="sxs-lookup"><span data-stu-id="436b4-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="436b4-210">Jeśli usługi Azure Active Directory jest katalogiem zsynchronizowane z usługami AD FS, zaufania hello usług AD FS domyślnie nie wysyła oświadczeń http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello albo, mimo że można ręcznie skonfigurować toosend usług AD FS to oświadczenie.</span><span class="sxs-lookup"><span data-stu-id="436b4-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="436b4-211">`ClaimTypes.NameIdentifies`Określa oświadczeń hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, której zapewnić usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="436b4-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="436b4-212">Teraz Opublikuj zmiany.</span><span class="sxs-lookup"><span data-stu-id="436b4-212">Now, publish your changes.</span></span> <span data-ttu-id="436b4-213">Kliknij prawym przyciskiem myszy projekt i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="436b4-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="436b4-214">Kliknij przycisk **ustawienia**, upewnij się, że istnieje tooyour ciąg połączenia bazy danych SQL, wybierz **aktualizacji bazy danych** toomake hello zmiany schematu dla modelu, a następnie kliknij przycisk **publikowania** .</span><span class="sxs-lookup"><span data-stu-id="436b4-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="436b4-215">W przeglądarce hello Przejdź toohttps: / /&lt;*appname*>.azurewebsites.net/workitems, a następnie kliknij przycisk **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="436b4-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="436b4-216">Kliknij hello **AssignedToName** pole.</span><span class="sxs-lookup"><span data-stu-id="436b4-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="436b4-217">Powinna zostać wyświetlona użytkowników i grup z dzierżawy usługi Azure Active Directory na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="436b4-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="436b4-218">Wpisz toofilter lub użyj hello `Up` lub `Down` klucza, lub kliknij przycisk tooselect hello użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="436b4-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="436b4-219">Kliknij przycisk **Utwórz** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="436b4-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="436b4-220">Następnie kliknij przycisk **Edytuj** elementu pracy hello utworzony tooobserve hello takie samo zachowanie.</span><span class="sxs-lookup"><span data-stu-id="436b4-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="436b4-221">Gratulacje teraz używasz aplikacji biznesowych z platformy Azure z dostępem do katalogu!</span><span class="sxs-lookup"><span data-stu-id="436b4-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="436b4-222">Istnieje wiele można zrobić za pomocą hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="436b4-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="436b4-223">Zobacz [dokumentacja interfejsu API Azure AD Graph](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="436b4-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="436b4-224">Następny krok</span><span class="sxs-lookup"><span data-stu-id="436b4-224">Next Step</span></span>
<span data-ttu-id="436b4-225">Jeśli potrzebujesz kontroli dostępu opartej na rolach (RBAC) dla aplikacji biznesowych z platformy azure, zobacz [aplikacji sieci Web-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) przykładowe hello przez zespół usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="436b4-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="436b4-226">Jak przedstawiono tooenable role w aplikacji usługi Azure Active Directory, a następnie Autoryzuj użytkownikom hello `[Authorize]` decoration.</span><span class="sxs-lookup"><span data-stu-id="436b4-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="436b4-227">Jeśli aplikacji biznesowych z wymaga dostępu do danych lokalnych tooon, zobacz [dostępu do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="436b4-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="436b4-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="436b4-228">Further resources</span></span>
* [<span data-ttu-id="436b4-229">Uwierzytelnianie i autoryzację w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="436b4-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="436b4-230">Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="436b4-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="436b4-231">Tworzenie aplikacji biznesowych z uwierzytelniania usług AD FS na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="436b4-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="436b4-232">Aplikacja usługi uwierzytelniania i hello Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="436b4-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="436b4-233">Microsoft Azure Active Directory przykłady i dokumentacja</span><span class="sxs-lookup"><span data-stu-id="436b4-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="436b4-234">Usługa Azure Active Directory obsługiwane tokeny i oświadczenia</span><span class="sxs-lookup"><span data-stu-id="436b4-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
