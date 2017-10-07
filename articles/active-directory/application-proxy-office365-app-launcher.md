---
title: "aaaSet niestandardową stronę główną dla opublikowanych aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje hello podstaw łączniki serwera Proxy aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="b320b-103">Ustaw niestandardową stronę główną dla opublikowanych aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b320b-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="b320b-104">W tym artykule omówiono sposób tooconfigure aplikacji toodirect użytkowników tooa niestandardową stronę główną.</span><span class="sxs-lookup"><span data-stu-id="b320b-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="b320b-105">Podczas publikowania aplikacji przy użyciu serwera Proxy aplikacji ustawić wewnętrzny adres URL, ale czasami nie jest to hello strony, które należy najpierw widzą użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b320b-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="b320b-106">Ustawić niestandardową stronę główną, dzięki czemu użytkownicy Przejdź toohello prawej strony, przy uzyskiwaniu dostępu do aplikacji hello hello Azure Panel dostępu usługi Active Directory lub uruchamiania aplikacji hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="b320b-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="b320b-107">Gdy użytkownicy uruchomią aplikację hello, są zaleceniami adresu URL domeny katalogu głównego toohello domyślne hello opublikowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b320b-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="b320b-108">Strona docelowa Hello zwykle jest ustawiony jako adres URL strony głównej hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="b320b-109">Adresy URL niestandardowej strony głównej toodefine hello Azure AD PowerShell modułu należy używać tooland użytkowników aplikacji w konkretnej strony w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="b320b-110">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b320b-110">For example:</span></span>
- <span data-ttu-id="b320b-111">W sieci firmowej użytkownicy przejść za*https://ExpenseApp/login/login.aspx* toosign w i uzyskiwać dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b320b-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="b320b-112">Ponieważ inne zasoby, takie jak obrazy wymagane przez serwer Proxy aplikacji tooaccess na najwyższym poziomie struktury folderów hello hello, publikowania aplikacji hello z *https://ExpenseApp* jako hello wewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="b320b-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="b320b-113">Witaj domyślne zewnętrzny adres URL jest *https://ExpenseApp-contoso.msappproxy.net*, która nie przyjmuje swojego konta toohello użytkowników na stronie.</span><span class="sxs-lookup"><span data-stu-id="b320b-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="b320b-114">Ustaw *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* jako hello toogive adres URL strony głównej użytkowników nie zakłóca pracy.</span><span class="sxs-lookup"><span data-stu-id="b320b-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="b320b-115">Przyznać dostęp użytkownikom toopublished aplikacji hello aplikacje są wyświetlane w hello [Panel dostępu usługi Azure AD](active-directory-saas-access-panel-introduction.md) i hello [uruchamiania aplikacji usługi Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="b320b-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b320b-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b320b-116">Before you start</span></span>

<span data-ttu-id="b320b-117">Aby ustawić adres URL strony głównej hello, należy hello uwzględnić następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="b320b-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="b320b-118">Upewnij się, że w tej ścieżce hello jest ścieżką poddomeny adresu URL domeny katalogu głównego hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="b320b-119">W przypadku adresu URL domeny głównej hello, na przykład https://apps.contoso.com/app1/, hello strony głównej skonfigurowanego adresu URL musi rozpoczynać się od https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="b320b-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="b320b-120">Jeśli wprowadzisz zmiany toohello aplikacja opublikowana, zmiany hello może zresetować wartość hello hello adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="b320b-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="b320b-121">Podczas aktualizacji aplikacji hello w przyszłości hello, należy ponownie sprawdzić i, w razie potrzeby zaktualizuj hello adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="b320b-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="b320b-122">Zmień stronę główną hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b320b-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="b320b-123">Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b320b-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="b320b-124">Przejdź za**usługi Azure Active Directory** > **rejestracji aplikacji** i wybierz aplikację z listy hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="b320b-125">Wybierz **właściwości** z hello ustawień.</span><span class="sxs-lookup"><span data-stu-id="b320b-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="b320b-126">Aktualizacja hello **adres URL strony głównej** pole z nowej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b320b-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Podaj adres URL nowej strony głównej](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="b320b-128">Wybierz **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="b320b-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="b320b-129">Zmień stronę główną hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b320b-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="b320b-130">Zainstaluj moduł programu PowerShell usługi Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="b320b-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="b320b-131">Przed zdefiniowaniem adres URL niestandardowej strony głównej przy użyciu programu PowerShell, należy zainstalować moduł programu PowerShell usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="b320b-132">Możesz pobrać pakiet hello z hello [galerii programu PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), która używa hello punkt końcowy interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="b320b-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="b320b-133">Witaj tooinstall pakiet, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b320b-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="b320b-134">Otwórz okno programu PowerShell standard, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b320b-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="b320b-135">Jeśli używasz polecenia hello jako bez uprawnień administratora, użyj hello `-scope currentuser` opcji.</span><span class="sxs-lookup"><span data-stu-id="b320b-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="b320b-136">Podczas instalacji hello wybierz **Y** tooinstall dwa pakiety z Nuget.org. Oba pakiety są wymagane.</span><span class="sxs-lookup"><span data-stu-id="b320b-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="b320b-137">Znajdź hello ObjectID aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b320b-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="b320b-138">Uzyskaj hello ObjectID aplikacji hello, a następnie wyszukaj aplikacji hello przez jego strony głównej.</span><span class="sxs-lookup"><span data-stu-id="b320b-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="b320b-139">Otwórz program PowerShell i zaimportować moduł hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b320b-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="b320b-140">Zaloguj się toohello modułu Azure AD jako administrator dzierżawy hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="b320b-141">Znajdź aplikacji hello na podstawie jego adresu URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="b320b-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="b320b-142">Adres URL hello można znaleźć w portalu hello przechodząc zbyt**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b320b-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="b320b-143">W tym przykładzie użyto *sharepoint iddemo*.</span><span class="sxs-lookup"><span data-stu-id="b320b-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="b320b-144">Należy uzyskać wynik, który jest podobne toohello, co pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b320b-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="b320b-145">Skopiuj hello toouse ObjectID identyfikator GUID w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="b320b-146">Adres URL strony głównej hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="b320b-146">Update hello home page URL</span></span>

<span data-ttu-id="b320b-147">W hello tego samego modułu PowerShell, który został użyty w kroku 1, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b320b-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="b320b-148">Upewnij się, że masz hello Popraw aplikacji i Zastąp *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* z hello ObjectID skopiowany w hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="b320b-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="b320b-149">Po potwierdzeniu aplikacji hello, należy się Strona główna hello tooupdate gotowy, w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b320b-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="b320b-150">Utwórz toohold obiektu pusta aplikacja hello zmiany, które mają toomake.</span><span class="sxs-lookup"><span data-stu-id="b320b-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="b320b-151">Ta zmienna przechowuje hello wartości, które mają tooupdate.</span><span class="sxs-lookup"><span data-stu-id="b320b-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="b320b-152">Nic nie jest tworzony w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="b320b-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="b320b-153">Ustaw wartość toohello adres URL strony głównej hello, która ma.</span><span class="sxs-lookup"><span data-stu-id="b320b-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="b320b-154">wartość Hello musi być ścieżką poddomeny hello opublikowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b320b-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="b320b-155">Na przykład, jeśli zmienisz hello adres URL strony głównej z *https://sharepoint-iddemo.msappproxy.net/* za*https://sharepoint-iddemo.msappproxy.net/hybrid/*, użytkownicy aplikacji bezpośrednio przejść toohello niestandardowe Strona główna.</span><span class="sxs-lookup"><span data-stu-id="b320b-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="b320b-156">Upewnij się, hello aktualizacji przy użyciu hello GUID (identyfikator obiektu), który został skopiowany w "krok 1: znajdowanie hello ObjectID aplikacji hello."</span><span class="sxs-lookup"><span data-stu-id="b320b-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="b320b-157">tooconfirm, że zmiany hello zakończyło się powodzeniem, ponownie uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b320b-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="b320b-158">Wszelkie zmiany dokonane w aplikacji toohello może zresetować hello adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="b320b-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="b320b-159">Jeśli adres URL strony głównej resetuje, powtórz krok 2.</span><span class="sxs-lookup"><span data-stu-id="b320b-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b320b-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b320b-160">Next steps</span></span>

- [<span data-ttu-id="b320b-161">Włącz tooSharePoint dostępu zdalnego z serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b320b-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="b320b-162">Włącz serwer Proxy aplikacji w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="b320b-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
