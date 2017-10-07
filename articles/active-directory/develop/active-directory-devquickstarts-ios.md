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
# <a name="integrate-azure-ad-into-an-ios-app"></a>Integrowanie usługi Azure AD do aplikacji systemu iOS
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Spróbuj Podgląd hello nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/iOS) pomaga rozpocząć pracę z usługą Azure Active Directory w ciągu kilku minut!  portalu dla deweloperów Hello prowadzi użytkownika przez proces hello rejestrowanie aplikacji i Integrowanie usługi Azure AD w kodzie.  Po zakończeniu będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie i wewnętrznej bazy danych, które mogą zaakceptować tokeny i sprawdzania poprawności. 
> 
> 

Azure Active Directory (Azure AD) zapewnia hello biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL dla klientów z systemem iOS, którzy potrzebują tooaccess chronione zasoby. Biblioteka ADAL upraszcza proces hello, że Twoja aplikacja korzysta z tokenów dostępu tooobtain. toodemonstrate, jak łatwo jest, w tym artykule budujemy aplikację listy zadań do wykonania Objective C:

* Pobiera dostępu tokenów do wywoływania interfejsu API Azure AD Graph hello przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Przeszukuje katalog dla użytkowników z podanego aliasu.

toobuild hello pełną działającą aplikację, musisz:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Instalowanie i konfigurowanie biblioteki ADAL.
3. Używaj tokenów ADAL tooget z usługi Azure AD.

Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji. Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).


> [!TIP]
> Spróbuj hello Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/iOS) pomaga rozpocząć pracę z usługą Azure AD w ciągu kilku minut. portalu dla deweloperów Hello prowadzi użytkownika przez proces hello rejestrowanie aplikacji i Integrowanie usługi Azure AD w kodzie. Po zakończeniu, będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie, a kończyć kopii, która może zaakceptować tokeny i sprawdzania poprawności. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Ustalić, jakie z przekierowania URI jest przeznaczony dla systemu iOS
toosecurely uruchomić aplikacje w niektórych scenariuszach logowania jednokrotnego, musisz utworzyć *identyfikator URI przekierowania* w określonym formacie. Przekierowanie URI jest używane tooensure, który hello tokenów zwracanych toohello poprawne aplikacji, która wyświetlony monit o podanie ich.


format iOS Hello przekierowanie identyfikator URI jest:

```
<app-scheme>://<bundle-id>
```

* **Schemat aplikacji** -to jest zarejestrowany w projekcie XCode. Jest jak inne aplikacje zadzwonić do Ciebie. Można znaleźć, to w pliku Info.plist -> adres URL identyfikatora -> typy adresu URL. Należy utworzyć jeden, jeśli nie masz jeszcze co najmniej jeden skonfigurowany.
* **Identyfikator pakietu** — jest to identyfikator pakietu omówionych w artykule "identity" hello un ustawień projektu w środowisku XCode.

Przykład dla tego kodu Szybki Start: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Zarejestrować aplikację DirectorySearcher hello
tooset się tokenów tooget aplikacji, należy najpierw tooregister w usługi Azure AD dzierżawy i udzielić jej uprawnienia tooaccess hello Azure AD Graph API:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku powitania kliknij swoje konto. W obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji.
3. Kliknij przycisk **więcej usług** w hello okienka nawigacji po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Wykonaj hello monituje toocreate nowy **natywną aplikację kliencką**.
  * Witaj **nazwa** aplikacji hello opisuje użytkownikom tooend aplikacji.
  * Witaj **identyfikator Uri przekierowania** to kombinacja schemat i ciąg używany tooreturn odpowiedzi tokenu w usłudze Azure AD.  Wprowadź wartość, która jest tooyour określonych aplikacji i jest oparta na powitania poprzednich informacji identyfikator URI przekierowania.
6. Po zakończeniu rejestracji hello Azure AD przypisuje aplikacji identyfikatora aplikacji  Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.
7. Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** , a następnie wybierz **Dodaj**. Wybierz **Microsoft Graph** jako hello interfejsu API, a następnie dodaj hello **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.  Konfiguruje Twoje hello tooquery aplikacji interfejsu API usługi Azure AD Graph dla użytkowników.

## <a name="3-install-and-configure-adal"></a>3. Instalowanie i konfigurowanie biblioteki ADAL
Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.  Aby ADAL toocommunicate z usługą Azure AD, należy tooprovide go niektóre informacje o rejestracji aplikacji.

1. Rozpocznij, dodając ADAL toohello DirectorySearcher projektu przy użyciu programu CocoaPods.

    ```
    $ vi Podfile
    ```
2. Dodaj następujące toothis podfile hello:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Teraz załadować hello podfile przy użyciu programu CocoaPods. Spowoduje to utworzenie nowego obszaru roboczego XCode, że zostały załadowane.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. Projekt szybkiego startu hello, otwórz plik plist hello `settings.plist`.  Zastąp wartości hello elementów hello na powitania sekcji tooreflect hello wprowadzone wartości w hello portalu Azure. Kod odwołuje się do tych wartości, przy każdym użyciu biblioteki ADAL.
  * Witaj `tenant` jest hello domeny dzierżawy usługi Azure AD, na przykład contoso.onmicrosoft.com.
  * Witaj `clientId` jest hello identyfikator klienta aplikacji, który został skopiowany z portalu hello.
  * Witaj `redirectUri` jest hello adres URL przekierowania, który został zarejestrowany w portalu hello.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Używaj tokenów ADAL tooget z usługi Azure AD
Witaj podstawową zasadą za ADAL jest czy zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje completionBlock `+(void) getToken : `, i ADAL hello rest.  

1. W hello `QuickStart` otwarciu projektu `GraphAPICaller.m` i Znajdź hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` komentarzem hello top.  Jest to, gdzie przekazać współrzędne ADAL hello za pośrednictwem CompletionBlock, toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.

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

2. Teraz potrzebujemy toouse ten token toosearch dla użytkowników w hello wykresu. Znajdź hello `// TODO: implement SearchUsersList` komentarza. Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania GET do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.  tooquery hello Azure AD Graph API, należy tooinclude ' access_token ' w hello `Authorization` nagłówka żądania hello. Jest to, gdzie ADAL jest dostarczany.

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


3. Gdy aplikacja żąda token przez wywołanie metody `getToken(...)`, ADAL prób tooreturn token bez monitowania użytkownika hello o poświadczenia.  Jeśli ADAL ustali, że ten użytkownik hello musi toosign w tooget token, go będzie wyświetlać okno dialogowe dla logowania, zbieranie poświadczeń użytkownika hello, a następnie wróć tokenu po pomyślnym uwierzytelnieniu.  Jeśli ADAL nie jest możliwe tooreturn token jakiejkolwiek przyczyny, zgłasza `AdalException`.

> [!Note] 
> Witaj `AuthenticationResult` zawiera obiekt `tokenCacheStoreItem` obiektów, które mogą być używane toocollect hello informacje, które może wymagać Twojej aplikacji. W hello szybkiego startu `tokenCacheStoreItem` jest toodetermine używanych w przypadku uwierzytelniania zostało już przeprowadzone.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Tworzenie i uruchamianie aplikacji hello
Gratulacje! Masz teraz działającą aplikację systemu iOS, która może uwierzytelniać użytkowników, bezpiecznie wywoływania interfejsów API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku hello.  Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.  Uruchom aplikację Szybki Start, a następnie zaloguj się przy użyciu jednej z tych użytkowników.  Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.  Zamknij aplikację hello, a następnie uruchom go ponownie.  Zwróć uwagę, że hello sesja pozostanie niezmieniona.

Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te typowe funkcje tożsamości w aplikacji.  Go odpowiada on za wszystkie hello dirty pracy, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika z toosign interfejsu użytkownika, w i odświeżanie wygaśnięcia tokenów.  Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `getToken`.

Odwołania, znajdujących ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Następne kroki
Możesz teraz przejść na tooadditional scenariuszy.  Można tootry:

* [Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web Node.JS](active-directory-devquickstarts-webapi-nodejs.md)
* Dowiedz się [jak tooenable logowania jednokrotnego wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

