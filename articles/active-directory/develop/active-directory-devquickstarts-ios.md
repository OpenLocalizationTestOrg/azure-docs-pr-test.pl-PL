---
title: "Integrowanie usługi Azure AD do aplikacji systemu iOS | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia aplikacji systemu iOS, która integruje się z usługą Azure AD, logowania i wywołania usługi Azure AD chronione interfejsów API przy użyciu uwierzytelniania OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="971d7-103">Integrowanie usługi Azure AD do aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="971d7-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="971d7-104">Spróbuj Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/iOS) pomaga rozpocząć pracę z usługą Azure Active Directory w ciągu kilku minut!</span><span class="sxs-lookup"><span data-stu-id="971d7-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="971d7-105">Portalu dla deweloperów prowadzi użytkownika przez proces rejestracji aplikacji i Integrowanie usługi Azure AD w kodzie.</span><span class="sxs-lookup"><span data-stu-id="971d7-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="971d7-106">Po zakończeniu będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie i wewnętrznej bazy danych, które mogą zaakceptować tokeny i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="971d7-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="971d7-107">Azure Active Directory (Azure AD) udostępnia biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL dla klientów z systemem iOS, które wymagają dostępu do chronionych zasobów.</span><span class="sxs-lookup"><span data-stu-id="971d7-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="971d7-108">ADAL upraszcza proces Twoja aplikacja korzysta z umożliwiające uzyskanie tokenów dostępu.</span><span class="sxs-lookup"><span data-stu-id="971d7-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="971d7-109">Aby zademonstrować, jak łatwo jest, w tym artykule mamy utworzyć aplikację listy zadań do wykonania Objective C który:</span><span class="sxs-lookup"><span data-stu-id="971d7-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="971d7-110">Pobiera dostępu tokenów do wywoływania za pomocą interfejsu API programu Azure AD Graph [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="971d7-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="971d7-111">Przeszukuje katalog dla użytkowników z podanego aliasu.</span><span class="sxs-lookup"><span data-stu-id="971d7-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="971d7-112">Aby utworzyć pełną działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="971d7-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="971d7-113">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="971d7-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="971d7-114">Instalowanie i konfigurowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="971d7-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="971d7-115">Użyj biblioteki ADAL, aby uzyskać tokenów z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="971d7-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="971d7-116">Aby rozpocząć, [pobrać szkielet aplikacji](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) lub [Pobieranie ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="971d7-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="971d7-117">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="971d7-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="971d7-118">Jeśli nie masz już dzierżawę, [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="971d7-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="971d7-119">Spróbuj Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/iOS) pomaga rozpocząć pracę z usługą Azure AD w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="971d7-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="971d7-120">Portalu dla deweloperów prowadzi użytkownika przez proces rejestracji aplikacji i Integrowanie usługi Azure AD w kodzie.</span><span class="sxs-lookup"><span data-stu-id="971d7-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="971d7-121">Po zakończeniu, będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie, a kończyć kopii, która może zaakceptować tokeny i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="971d7-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="971d7-122">1. Ustalić, jakie z przekierowania URI jest przeznaczony dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="971d7-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="971d7-123">Można bezpiecznie uruchomić aplikacje w niektórych scenariuszach logowania jednokrotnego, musisz utworzyć *identyfikator URI przekierowania* w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="971d7-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="971d7-124">Identyfikator URI przekierowania jest używany, aby upewnić się, że tokeny powrócić do właściwej aplikacji, która wyświetlony monit o podanie ich.</span><span class="sxs-lookup"><span data-stu-id="971d7-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="971d7-125">Format systemu iOS dla przekierowania jest identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="971d7-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="971d7-126">**Schemat aplikacji** -to jest zarejestrowany w projekcie XCode.</span><span class="sxs-lookup"><span data-stu-id="971d7-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="971d7-127">Jest jak inne aplikacje zadzwonić do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="971d7-127">It is how other applications can call you.</span></span> <span data-ttu-id="971d7-128">Można znaleźć, to w pliku Info.plist -> adres URL identyfikatora -> typy adresu URL.</span><span class="sxs-lookup"><span data-stu-id="971d7-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="971d7-129">Należy utworzyć jeden, jeśli nie masz jeszcze co najmniej jeden skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="971d7-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="971d7-130">**Identyfikator pakietu** — jest to identyfikator pakietu omówionych w artykule "identity" un ustawień projektu w środowisku XCode.</span><span class="sxs-lookup"><span data-stu-id="971d7-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="971d7-131">Przykład dla tego kodu Szybki Start: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="971d7-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="971d7-132">2. Zarejestrować aplikację DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="971d7-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="971d7-133">Aby skonfigurować aplikację, aby uzyskać tokeny, należy najpierw zarejestrować ją w dzierżawie usługi Azure AD i udzielić jej uprawnienia dostępu do interfejsu API programu Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="971d7-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="971d7-134">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="971d7-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="971d7-135">Na górnym pasku kliknij konto.</span><span class="sxs-lookup"><span data-stu-id="971d7-135">On the top bar, click your account.</span></span> <span data-ttu-id="971d7-136">W obszarze **katalogu** wybierz dzierżawy usługi Active Directory, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="971d7-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="971d7-137">Kliknij przycisk **więcej usług** w okienku nawigacji po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="971d7-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="971d7-138">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="971d7-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="971d7-139">Postępuj zgodnie z monitami, aby utworzyć nową **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="971d7-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="971d7-140">**Nazwa** aplikacji opisuje aplikacji dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="971d7-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="971d7-141">**Identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, korzystającą z usługi Azure AD w celu zwracać odpowiedzi tokenu.</span><span class="sxs-lookup"><span data-stu-id="971d7-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="971d7-142">Wprowadź wartość, która jest specyficzna dla aplikacji i opierają się na poprzedniej informacyjne URI przekierowania.</span><span class="sxs-lookup"><span data-stu-id="971d7-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="971d7-143">Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="971d7-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="971d7-144">Ta wartość jest potrzebny w kolejnych sekcjach, dlatego skopiuj go na karcie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="971d7-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="971d7-145">Z **ustawienia** wybierz pozycję **wymagane uprawnienia** , a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="971d7-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="971d7-146">Wybierz **Microsoft Graph** jako interfejsu API, a następnie dodaj **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="971d7-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="971d7-147">Konfiguruje aplikację do zapytania interfejsu API programu Azure AD Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="971d7-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="971d7-148">3. Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="971d7-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="971d7-149">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="971d7-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="971d7-150">Dotyczące biblioteki ADAL do komunikowania się z usługą Azure AD należy dostarczyć informacji o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="971d7-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="971d7-151">Rozpocznij, dodając biblioteki ADAL do projektu DirectorySearcher przy użyciu programu CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="971d7-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="971d7-152">Dodaj następujący kod do tego pliku podfile:</span><span class="sxs-lookup"><span data-stu-id="971d7-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="971d7-153">Teraz załadować podfile przy użyciu programu CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="971d7-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="971d7-154">Spowoduje to utworzenie nowego obszaru roboczego XCode, że zostały załadowane.</span><span class="sxs-lookup"><span data-stu-id="971d7-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="971d7-155">W projekcie szybkiego startu, otwórz plik plist `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="971d7-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="971d7-156">Zastąp wartości elementów w sekcji do wartości, które zostały wprowadzone w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="971d7-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="971d7-157">Kod odwołuje się do tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="971d7-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="971d7-158">`tenant` Jest domeny dzierżawy usługi Azure AD, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="971d7-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="971d7-159">`clientId` Jest identyfikator klienta aplikacji, który został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="971d7-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="971d7-160">`redirectUri` Jest adres URL przekierowania, który został zarejestrowany w portalu.</span><span class="sxs-lookup"><span data-stu-id="971d7-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="971d7-161">4.    Aby uzyskać tokenów z usługi Azure AD, użyj biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="971d7-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="971d7-162">Zasada podstawowa za ADAL jest, że zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje completionBlock `+(void) getToken : `, a reszta biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="971d7-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="971d7-163">W `QuickStart` otwarciu projektu `GraphAPICaller.m` i Znajdź `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` komentarz u góry.</span><span class="sxs-lookup"><span data-stu-id="971d7-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="971d7-164">Jest to, gdy przekazujesz ADAL współrzędne za pośrednictwem CompletionBlock, aby komunikować się z usługą Azure AD i poinformuj go, jak pamięci podręcznej tokenów.</span><span class="sxs-lookup"><span data-stu-id="971d7-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="971d7-165">Teraz należy użyć tego tokenu wyszukać użytkowników na wykresie.</span><span class="sxs-lookup"><span data-stu-id="971d7-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="971d7-166">Znajdź `// TODO: implement SearchUsersList` komentarza.</span><span class="sxs-lookup"><span data-stu-id="971d7-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="971d7-167">Ta metoda zgłasza żądanie GET interfejsu API Azure AD Graph zapytania dla użytkowników, których nazwy UPN rozpoczyna się od danego wyszukiwanego.</span><span class="sxs-lookup"><span data-stu-id="971d7-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="971d7-168">Aby wykonać zapytania interfejsu API Azure AD Graph, należy uwzględnić ' access_token ' w `Authorization` nagłówka żądania.</span><span class="sxs-lookup"><span data-stu-id="971d7-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="971d7-169">Jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="971d7-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="971d7-170">Gdy aplikacja żąda token przez wywołanie metody `getToken(...)`, ADAL próbuje zwrócić token bez monitowania użytkownika o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="971d7-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="971d7-171">Jeśli ADAL Określa, czy użytkownik powinien logować się do pobrania tokenu, go będą wyświetlane jest okno dialogowe dla logowania, zbieranie poświadczeń użytkownika, a następnie wróć tokenu po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="971d7-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="971d7-172">Jeśli ADAL nie będzie mógł zwrócić token jakiegokolwiek powodu, zgłasza `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="971d7-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="971d7-173">`AuthenticationResult` Zawiera obiekt `tokenCacheStoreItem` obiektu, który może służyć do zbierania informacji, które może wymagać Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="971d7-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="971d7-174">Z opcją szybkiego startu `tokenCacheStoreItem` służy do określania, czy uwierzytelnianie jest już wykonywane.</span><span class="sxs-lookup"><span data-stu-id="971d7-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="971d7-175">5. Kompilowanie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="971d7-175">5. Build and run the application</span></span>
<span data-ttu-id="971d7-176">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="971d7-176">Congratulations!</span></span> <span data-ttu-id="971d7-177">Masz teraz działającą aplikację systemu iOS, która może uwierzytelniać użytkowników, bezpiecznie wywoływania interfejsów API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="971d7-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="971d7-178">Jeśli nie jest jeszcze nadszedł czas do wypełnienia dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="971d7-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="971d7-179">Uruchom aplikację Szybki Start, a następnie zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="971d7-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="971d7-180">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="971d7-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="971d7-181">Zamknij aplikację, a następnie uruchom go ponownie.</span><span class="sxs-lookup"><span data-stu-id="971d7-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="971d7-182">Zwróć uwagę, że sesja pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="971d7-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="971d7-183">Biblioteka ADAL można łatwo zastosować wszystkie te typowe funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="971d7-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="971d7-184">Go zajmuje się pracy dirty, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający użytkownika z interfejsu użytkownika do zalogowania się i odświeżanie wygasła tokenów.</span><span class="sxs-lookup"><span data-stu-id="971d7-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="971d7-185">Tak naprawdę trzeba wiedzieć jednego wywołania interfejsu API, jest `getToken`.</span><span class="sxs-lookup"><span data-stu-id="971d7-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="971d7-186">Odwołania, ukończonych próbka (bez wartości konfiguracji) znajduje się na [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="971d7-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="971d7-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="971d7-187">Next steps</span></span>
<span data-ttu-id="971d7-188">Możesz teraz przejść do dodatkowe scenariusze.</span><span class="sxs-lookup"><span data-stu-id="971d7-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="971d7-189">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="971d7-189">You may want to try:</span></span>

* [<span data-ttu-id="971d7-190">Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web Node.JS</span><span class="sxs-lookup"><span data-stu-id="971d7-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="971d7-191">Dowiedz się [jak włączyć logowanie Jednokrotne wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="971d7-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

