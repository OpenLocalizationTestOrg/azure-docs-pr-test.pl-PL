---
title: "aaaIntegrate usługi Azure AD do aplikacji systemu iOS | Dokumentacja firmy Microsoft"
description: "Jak toobuild aplikacji systemu iOS, która integruje się z usługą Azure AD, logowania i wywołania usługi Azure AD chronione interfejsów API przy użyciu uwierzytelniania OAuth."
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
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="7f2ba-103">Integrowanie usługi Azure AD do aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="7f2ba-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="7f2ba-104">Spróbuj Podgląd hello nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/iOS) pomaga rozpocząć pracę z usługą Azure Active Directory w ciągu kilku minut!</span><span class="sxs-lookup"><span data-stu-id="7f2ba-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="7f2ba-105">portalu dla deweloperów Hello prowadzi użytkownika przez proces hello rejestrowanie aplikacji i Integrowanie usługi Azure AD w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="7f2ba-106">Po zakończeniu będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie i wewnętrznej bazy danych, które mogą zaakceptować tokeny i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="7f2ba-107">Azure Active Directory (Azure AD) zapewnia hello biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL dla klientów z systemem iOS, którzy potrzebują tooaccess chronione zasoby.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="7f2ba-108">Biblioteka ADAL upraszcza proces hello, że Twoja aplikacja korzysta z tokenów dostępu tooobtain.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="7f2ba-109">toodemonstrate, jak łatwo jest, w tym artykule budujemy aplikację listy zadań do wykonania Objective C:</span><span class="sxs-lookup"><span data-stu-id="7f2ba-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="7f2ba-110">Pobiera dostępu tokenów do wywoływania interfejsu API Azure AD Graph hello przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f2ba-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="7f2ba-111">Przeszukuje katalog dla użytkowników z podanego aliasu.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="7f2ba-112">toobuild hello pełną działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="7f2ba-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="7f2ba-113">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="7f2ba-114">Instalowanie i konfigurowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="7f2ba-115">Używaj tokenów ADAL tooget z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="7f2ba-116">Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7f2ba-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="7f2ba-117">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="7f2ba-118">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7f2ba-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="7f2ba-119">Spróbuj hello Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/iOS) pomaga rozpocząć pracę z usługą Azure AD w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="7f2ba-120">portalu dla deweloperów Hello prowadzi użytkownika przez proces hello rejestrowanie aplikacji i Integrowanie usługi Azure AD w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="7f2ba-121">Po zakończeniu, będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie, a kończyć kopii, która może zaakceptować tokeny i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="7f2ba-122">1. Ustalić, jakie z przekierowania URI jest przeznaczony dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="7f2ba-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="7f2ba-123">toosecurely uruchomić aplikacje w niektórych scenariuszach logowania jednokrotnego, musisz utworzyć *identyfikator URI przekierowania* w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="7f2ba-124">Przekierowanie URI jest używane tooensure, który hello tokenów zwracanych toohello poprawne aplikacji, która wyświetlony monit o podanie ich.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="7f2ba-125">format iOS Hello przekierowanie identyfikator URI jest:</span><span class="sxs-lookup"><span data-stu-id="7f2ba-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="7f2ba-126">**Schemat aplikacji** -to jest zarejestrowany w projekcie XCode.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="7f2ba-127">Jest jak inne aplikacje zadzwonić do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-127">It is how other applications can call you.</span></span> <span data-ttu-id="7f2ba-128">Można znaleźć, to w pliku Info.plist -> adres URL identyfikatora -> typy adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="7f2ba-129">Należy utworzyć jeden, jeśli nie masz jeszcze co najmniej jeden skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="7f2ba-130">**Identyfikator pakietu** — jest to identyfikator pakietu omówionych w artykule "identity" hello un ustawień projektu w środowisku XCode.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="7f2ba-131">Przykład dla tego kodu Szybki Start: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="7f2ba-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="7f2ba-132">2. Zarejestrować aplikację DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="7f2ba-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="7f2ba-133">tooset się tokenów tooget aplikacji, należy najpierw tooregister w usługi Azure AD dzierżawy i udzielić jej uprawnienia tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="7f2ba-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="7f2ba-134">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f2ba-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f2ba-135">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-135">On hello top bar, click your account.</span></span> <span data-ttu-id="7f2ba-136">W obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="7f2ba-137">Kliknij przycisk **więcej usług** w hello okienka nawigacji po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7f2ba-138">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="7f2ba-139">Wykonaj hello monituje toocreate nowy **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="7f2ba-140">Witaj **nazwa** aplikacji hello opisuje użytkownikom tooend aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="7f2ba-141">Witaj **identyfikator Uri przekierowania** to kombinacja schemat i ciąg używany tooreturn odpowiedzi tokenu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="7f2ba-142">Wprowadź wartość, która jest tooyour określonych aplikacji i jest oparta na powitania poprzednich informacji identyfikator URI przekierowania.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="7f2ba-143">Po zakończeniu rejestracji hello Azure AD przypisuje aplikacji identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="7f2ba-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="7f2ba-144">Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="7f2ba-145">Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** , a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="7f2ba-146">Wybierz **Microsoft Graph** jako hello interfejsu API, a następnie dodaj hello **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="7f2ba-147">Konfiguruje Twoje hello tooquery aplikacji interfejsu API usługi Azure AD Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="7f2ba-148">3. Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="7f2ba-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="7f2ba-149">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="7f2ba-150">Aby ADAL toocommunicate z usługą Azure AD, należy tooprovide go niektóre informacje o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="7f2ba-151">Rozpocznij, dodając ADAL toohello DirectorySearcher projektu przy użyciu programu CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="7f2ba-152">Dodaj następujące toothis podfile hello:</span><span class="sxs-lookup"><span data-stu-id="7f2ba-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="7f2ba-153">Teraz załadować hello podfile przy użyciu programu CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="7f2ba-154">Spowoduje to utworzenie nowego obszaru roboczego XCode, że zostały załadowane.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="7f2ba-155">Projekt szybkiego startu hello, otwórz plik plist hello `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="7f2ba-156">Zastąp wartości hello elementów hello na powitania sekcji tooreflect hello wprowadzone wartości w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="7f2ba-157">Kod odwołuje się do tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="7f2ba-158">Witaj `tenant` jest hello domeny dzierżawy usługi Azure AD, na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="7f2ba-159">Witaj `clientId` jest hello identyfikator klienta aplikacji, który został skopiowany z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="7f2ba-160">Witaj `redirectUri` jest hello adres URL przekierowania, który został zarejestrowany w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="7f2ba-161">4.    Używaj tokenów ADAL tooget z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f2ba-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="7f2ba-162">Witaj podstawową zasadą za ADAL jest czy zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje completionBlock `+(void) getToken : `, i ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="7f2ba-163">W hello `QuickStart` otwarciu projektu `GraphAPICaller.m` i Znajdź hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` komentarzem hello top.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="7f2ba-164">Jest to, gdzie przekazać współrzędne ADAL hello za pośrednictwem CompletionBlock, toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="7f2ba-165">Teraz potrzebujemy toouse ten token toosearch dla użytkowników w hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="7f2ba-166">Znajdź hello `// TODO: implement SearchUsersList` komentarza.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="7f2ba-167">Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania GET do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="7f2ba-168">tooquery hello Azure AD Graph API, należy tooinclude ' access_token ' w hello `Authorization` nagłówka żądania hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="7f2ba-169">Jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-169">This is where ADAL comes in.</span></span>

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

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
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


3. <span data-ttu-id="7f2ba-170">Gdy aplikacja żąda token przez wywołanie metody `getToken(...)`, ADAL prób tooreturn token bez monitowania użytkownika hello o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="7f2ba-171">Jeśli ADAL ustali, że ten użytkownik hello musi toosign w tooget token, go będzie wyświetlać okno dialogowe dla logowania, zbieranie poświadczeń użytkownika hello, a następnie wróć tokenu po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="7f2ba-172">Jeśli ADAL nie jest możliwe tooreturn token jakiejkolwiek przyczyny, zgłasza `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="7f2ba-173">Witaj `AuthenticationResult` zawiera obiekt `tokenCacheStoreItem` obiektów, które mogą być używane toocollect hello informacje, które może wymagać Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="7f2ba-174">W hello szybkiego startu `tokenCacheStoreItem` jest toodetermine używanych w przypadku uwierzytelniania zostało już przeprowadzone.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="7f2ba-175">5. Tworzenie i uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7f2ba-175">5. Build and run hello application</span></span>
<span data-ttu-id="7f2ba-176">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="7f2ba-176">Congratulations!</span></span> <span data-ttu-id="7f2ba-177">Masz teraz działającą aplikację systemu iOS, która może uwierzytelniać użytkowników, bezpiecznie wywoływania interfejsów API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="7f2ba-178">Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="7f2ba-179">Uruchom aplikację Szybki Start, a następnie zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="7f2ba-180">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="7f2ba-181">Zamknij aplikację hello, a następnie uruchom go ponownie.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="7f2ba-182">Zwróć uwagę, że hello sesja pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="7f2ba-183">Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te typowe funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="7f2ba-184">Go odpowiada on za wszystkie hello dirty pracy, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika z toosign interfejsu użytkownika, w i odświeżanie wygaśnięcia tokenów.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="7f2ba-185">Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="7f2ba-186">Odwołania, znajdujących ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7f2ba-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7f2ba-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f2ba-187">Next steps</span></span>
<span data-ttu-id="7f2ba-188">Możesz teraz przejść na tooadditional scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="7f2ba-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="7f2ba-189">Można tootry:</span><span class="sxs-lookup"><span data-stu-id="7f2ba-189">You may want tootry:</span></span>

* [<span data-ttu-id="7f2ba-190">Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web Node.JS</span><span class="sxs-lookup"><span data-stu-id="7f2ba-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="7f2ba-191">Dowiedz się [jak tooenable logowania jednokrotnego wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="7f2ba-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

