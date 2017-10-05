---
title: "Ustaw niestandardową stronę główną dla opublikowanych aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zawiera podstawowe informacje dotyczące serwera Proxy aplikacji usługi Azure AD łączników"
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="59c18-103">Ustaw niestandardową stronę główną dla opublikowanych aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59c18-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="59c18-104">W tym artykule omówiono sposób konfigurowania aplikacji, aby kierować użytkowników do niestandardowej strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="59c18-105">Podczas publikowania aplikacji przy użyciu serwera Proxy aplikacji, należy ustawić wewnętrzny adres URL jednak czasami nie będący strony, które należy najpierw widzą użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="59c18-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="59c18-106">Ustawić niestandardową stronę główną, dzięki czemu użytkownicy przejdź do prawej strony, przy uzyskiwaniu dostępu do aplikacji z usługi Azure Active Directory panelu dostępu lub uruchamiania aplikacji usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="59c18-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="59c18-107">Gdy użytkownicy uruchomią aplikację, są one skierowane domyślnie do adresu URL domeny katalogu głównego dla opublikowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59c18-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="59c18-108">Strona docelowa jest zwykle ustawiana jako adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="59c18-109">Użyj modułu Azure AD PowerShell do definiowania adresy URL niestandardową stronę główną, gdy chcesz użytkownikom aplikacji przejście na określonej strony w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59c18-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="59c18-110">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="59c18-110">For example:</span></span>
- <span data-ttu-id="59c18-111">W sieci firmowej użytkownicy przejść do *https://ExpenseApp/login/login.aspx* logować się i uzyskać dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59c18-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="59c18-112">Ponieważ inne zasoby, takie jak obrazy, które serwer Proxy aplikacji musi mieć dostęp na najwyższym poziomie struktury folderów, Opublikuj aplikację z *https://ExpenseApp* jako wewnętrzny adres URL.</span><span class="sxs-lookup"><span data-stu-id="59c18-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="59c18-113">Domyślny adres URL zewnętrznego *https://ExpenseApp-contoso.msappproxy.net*, która nie przyjmuje użytkownikom logowania na stronie.</span><span class="sxs-lookup"><span data-stu-id="59c18-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="59c18-114">Ustaw *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* jako adres URL strony głównej, aby zapewnić użytkownikom bezproblemowe.</span><span class="sxs-lookup"><span data-stu-id="59c18-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="59c18-115">Gdy można udzielać użytkownikom dostępu do opublikowanych aplikacji, aplikacje są wyświetlane w [Panel dostępu usługi Azure AD](active-directory-saas-access-panel-introduction.md) i [uruchamiania aplikacji usługi Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="59c18-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="59c18-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="59c18-116">Before you start</span></span>

<span data-ttu-id="59c18-117">Aby ustawić adres URL strony głównej, należy pamiętać, następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="59c18-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="59c18-118">Upewnij się, że ścieżkę, którą określisz jest ścieżką poddomeny domeny głównego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="59c18-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="59c18-119">W przypadku adresu URL domeny głównej, na przykład https://apps.contoso.com/app1/, adres URL strony głównej, które można skonfigurować musi rozpoczynać się od https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="59c18-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="59c18-120">Jeśli wprowadzisz zmiany w opublikowanej aplikacji, zmiana może zresetować wartość adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="59c18-121">Podczas aktualizacji aplikacji w przyszłości, należy ponownie sprawdzić i, w razie potrzeby zaktualizuj adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="59c18-122">Zmienianie strony głównej w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="59c18-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="59c18-123">Zaloguj się do witryny [Azure Portal](https://portal.azure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="59c18-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="59c18-124">Przejdź do **usługi Azure Active Directory** > **rejestracji aplikacji** i wybierz aplikację z listy.</span><span class="sxs-lookup"><span data-stu-id="59c18-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="59c18-125">Wybierz **właściwości** z ustawień.</span><span class="sxs-lookup"><span data-stu-id="59c18-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="59c18-126">Aktualizacja **adres URL strony głównej** pole z nowej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="59c18-126">Update the **Home page URL** field with your new path.</span></span> 

   ![Podaj adres URL nowej strony głównej](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="59c18-128">Wybierz **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="59c18-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="59c18-129">Zmienianie strony głównej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="59c18-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="59c18-130">Zainstaluj moduł programu PowerShell usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59c18-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="59c18-131">Przed zdefiniowaniem adres URL niestandardowej strony głównej przy użyciu programu PowerShell, należy zainstalować moduł Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59c18-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="59c18-132">Możesz pobrać pakiet ze [galerii programu PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), która wykorzystuje punkt końcowy interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="59c18-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="59c18-133">Aby zainstalować pakiet, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59c18-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="59c18-134">Otwórz okno programu PowerShell standard, a następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="59c18-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="59c18-135">Jeśli używasz polecenia jako bez uprawnień administratora, użyj `-scope currentuser` opcji.</span><span class="sxs-lookup"><span data-stu-id="59c18-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="59c18-136">Podczas instalacji wybierz **Y** zainstalować dwóch pakietów z Nuget.org. Oba pakiety są wymagane.</span><span class="sxs-lookup"><span data-stu-id="59c18-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="59c18-137">Znajdź identyfikator obiektu aplikacji</span><span class="sxs-lookup"><span data-stu-id="59c18-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="59c18-138">Uzyskaj identyfikator obiektu aplikacji, a następnie wyszukaj aplikację przez jego strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="59c18-139">Otwórz program PowerShell i zaimportuj moduł usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59c18-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="59c18-140">Zaloguj się do modułu Azure AD jako administrator dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="59c18-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="59c18-141">Znajdź na podstawie jego adresu URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="59c18-142">Adres URL można znaleźć w portalu, przechodząc do **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59c18-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="59c18-143">W tym przykładzie użyto *sharepoint iddemo*.</span><span class="sxs-lookup"><span data-stu-id="59c18-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="59c18-144">Należy uzyskać wynik, który jest podobny do pokazanego poniżej.</span><span class="sxs-lookup"><span data-stu-id="59c18-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="59c18-145">Skopiuj identyfikator GUID ObjectID do użycia w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="59c18-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="59c18-146">Aktualizacja adresu URL strony głównej</span><span class="sxs-lookup"><span data-stu-id="59c18-146">Update the home page URL</span></span>

<span data-ttu-id="59c18-147">W tym samym module środowiska PowerShell, który został użyty w kroku 1 wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59c18-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="59c18-148">Potwierdź prawidłowe aplikacji i Zastąp *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* z ObjectID skopiowanego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="59c18-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="59c18-149">Po potwierdzeniu aplikacji możesz zaktualizować strony głównej w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="59c18-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="59c18-150">Utwórz obiekt pusta aplikacja do zmiany, które mają być przechowywane.</span><span class="sxs-lookup"><span data-stu-id="59c18-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="59c18-151">Ta zmienna przechowuje wartości, które chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="59c18-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="59c18-152">Nic nie jest tworzony w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="59c18-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="59c18-153">Ustaw adres URL strony głównej na żądaną wartość.</span><span class="sxs-lookup"><span data-stu-id="59c18-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="59c18-154">Wartość musi być ścieżką poddomeny opublikowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59c18-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="59c18-155">Na przykład zmień adres URL strony głównej z *https://sharepoint-iddemo.msappproxy.net/* do *https://sharepoint-iddemo.msappproxy.net/hybrid/*, użytkownicy aplikacji przejść bezpośrednio do strony głównej niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="59c18-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="59c18-156">Tworzenie aktualizacji przy użyciu identyfikatora GUID (identyfikator obiektu) skopiowany w "krok 1: znajdowanie ObjectID aplikacji."</span><span class="sxs-lookup"><span data-stu-id="59c18-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="59c18-157">Aby upewnić się, że zmiana zakończyła się pomyślnie, uruchom ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="59c18-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="59c18-158">Wszelkie zmiany wprowadzone do aplikacji może zresetować adres URL strony głównej.</span><span class="sxs-lookup"><span data-stu-id="59c18-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="59c18-159">Jeśli adres URL strony głównej resetuje, powtórz krok 2.</span><span class="sxs-lookup"><span data-stu-id="59c18-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59c18-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59c18-160">Next steps</span></span>

- [<span data-ttu-id="59c18-161">Włączenie dostępu zdalnego do programu SharePoint przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59c18-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="59c18-162">Włącz serwer Proxy aplikacji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="59c18-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
