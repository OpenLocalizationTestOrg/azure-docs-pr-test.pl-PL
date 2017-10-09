---
title: "aaaHow tooUse iOS SDK dla usługi Azure Mobile Apps"
description: "Jak tooUse iOS SDK dla usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Jak iOS tooUse biblioteki klienta usługi Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Ten przewodnik zawiera wskazówki, tooperform typowych scenariuszy przy użyciu hello najnowszych [iOS Azure Mobile Apps SDK][1]. W przypadku nowych aplikacji mobilnej tooAzure najpierw zakończyć [Azure Mobile Apps Szybki Start] toocreate zaplecza, Utwórz tabelę i Pobierz projektu wbudowanych systemu iOS w programie Xcode. W tym przewodniku możemy skupić się na powitania klienta z systemem iOS SDK. toolearn więcej na temat hello SDK po stronie serwera na powitania wewnętrznej bazy danych, zobacz powitania serwera SDK HOWTOs.

## <a name="reference-documentation"></a>Dokumentacja referencyjna
Witaj dokumentacji dla powitania klienta z systemem iOS SDK jest zlokalizowana tutaj: [iOS Azure Mobile Apps odwołanie klienta][2].

## <a name="supported-platforms"></a>Obsługiwane platformy
Hello iOS SDK obsługuje projekty języka Objective-C, Swift 2.2 projektów i Swift 2.3 projektów dla systemu iOS w wersji 8.0 lub nowszej.

Hello "serwer flow" uwierzytelnianie przy użyciu widoku sieci Web dla hello przedstawione interfejsu użytkownika.  W przypadku hello urządzenie nie jest możliwe toopresent WebView interfejsu użytkownika, innej metody uwierzytelniania jest wymagane, który jest poza zakresem hello hello produktu.  
Zestaw SDK w związku z tym nie jest odpowiedni dla typu czujki lub podobnie ograniczeniami urządzeń.

## <a name="Setup"></a>Instalacji i wymagania wstępne
W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli. W tym przewodniku przyjęto założenie, że ta tabela hello ma ten sam schemat jako tabele hello w tych samouczkach. W tym przewodniku założono, że w kodzie, można się odwołać `MicrosoftAzureMobile.framework` i zaimportować `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Porady: Tworzenie klienta
Utwórz tooaccess zaplecza Azure Mobile Apps w projekcie, `MSClient`. Zastąp `AppUrl` z adresem URL aplikacji hello. Można pozostawić `gatewayURLString` i `applicationKey` puste. Skonfigurowanie bramy uwierzytelniania wypełnić `gatewayURLString` o hello bramy w adresie URL.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Kod SWIFT**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Porady: Tworzenie tabeli odwołania
dane tooaccess lub aktualizacji, tworzy tabelę odwołania toohello wewnętrznej bazy danych. Zastąp `TodoItem` o nazwie hello tabeli

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Kod SWIFT**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Porady: zapytania na danych
toocreate kwerendę bazy danych zapytania hello `MSTable` obiektu. Witaj następujące zapytanie pobiera wszystkie elementy hello w `TodoItem` i dzienniki hello tekst każdego elementu.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Kod SWIFT**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Porady: Filtr zwrócił danych
wyniki toofilter, istnieje wiele dostępnych opcji.

używając predykatu, użyj toofilter `NSPredicate` i `readWithPredicate`. następujące Hello filtruje dane zwrotne toofind tylko niezakończonych elementów Todo.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Kod SWIFT**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Porady: Użyj MSQuery
tooperform Tworzenie złożonego zapytania (w tym sortowanie i stronicowanie), `MSQuery` obiekt bezpośrednio lub za pomocą predykat:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Kod SWIFT**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery`Umożliwia sterowanie różne zachowania zapytania.

* Określ kolejność wyników
* Limit, które pola tooreturn
* Ogranicz liczbę rekordów tooreturn
* Określ liczbę całkowitą w odpowiedzi
* Określ parametry ciągu zapytania niestandardowe w żądaniu
* Zastosuj dodatkowe funkcje

Wykonanie `MSQuery` zapytania przez wywołanie metody `readWithCompletion` hello obiektu.

## <a name="sorting"></a>Porady: sortowanie danych za pomocą MSQuery
wyniki toosort Przyjrzyjmy się przykładem. Wywołanie toosort rosnącej pola 'text', a następnie "Pełna" malejąco `MSQuery` w następujący sposób:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Kod SWIFT**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Porady: ograniczyć pól i parametrów ciągu zapytania z MSQuery rozwiń
toobe pola toolimit zwracane w zapytaniu, określ hello nazwy pól hello w hello **selectFields** właściwości. W tym przykładzie zwraca tylko tekst hello i wypełnionego pola:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**Kod SWIFT**:

```
query.selectFields = ["text", "complete"]
```

parametrów ciągu zapytania dodatkowe tooinclude Server hello żądania (na przykład, ponieważ używa niestandardowego skryptu po stronie serwera, ich), wypełnij `query.parameters` w następujący sposób:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Kod SWIFT**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Porady: Konfigurowanie rozmiar strony
Z usługą Azure Mobile Apps formantów rozmiar strony hello hello liczba rekordów, które są pobierane w czasie z hello tabel wewnętrznej bazy danych. A wywołać zbyt`pull` zapasową danych na podstawie tej strony rozmiaru, dopóki nie ma żadnych więcej rekordów toopull następnie partii danych.

Jest możliwe tooconfigure rozmiar strony przy użyciu **MSPullSettings** jak pokazano poniżej. Domyślny rozmiar strony Hello wynosi 50, a w poniższym przykładzie hello zmienia too3.

Można skonfigurować inny rozmiar strony ze względu na wydajność. Jeśli masz dużą liczbę rekordów danych mały rozmiar strony wysokiej zmniejsza hello liczbę operacji serwera.

To ustawienie określa tylko rozmiar strony hello na powitania po stronie klienta. Jeśli hello klient żąda większy rozmiar strony nie obsługuje hello zaplecza aplikacji mobilnej, rozmiar strony hello jest ograniczona do maksymalnej hello hello wewnętrznej bazy danych jest toosupport skonfigurowany.

To ustawienie jest również hello *numer* rekordów danych nie hello *rozmiar w bajtach*.

Zwiększenie rozmiaru strony powitania klienta, należy również zwiększyć rozmiar strony hello na powitania serwera. Zobacz ["porady: dopasowywanie hello tabeli stronicowania"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) dla hello kroki toodo to.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Kod SWIFT**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Porady: wstawianie danych
Utwórz tooinsert nowego wiersza tabeli, `NSDictionary` i wywoływać `table insert`. Jeśli [dynamiczne schematu] jest włączona, hello zaplecza aplikacji mobilnych usługi aplikacji Azure automatycznie generuje nowe kolumny oparte na powitania `NSDictionary`.

Jeśli `id` nie zostanie podany, zaplecza hello automatycznie generuje nowy unikatowy identyfikator. Podaj własny `id` toouse e-mail adresy, nazwy użytkowników lub własne wartości jako identyfikatora. Własnego Identyfikatora zapewnienie może ułatwić sprzężenia i logiki firmowe bazy danych.

Witaj `result` zawiera hello nowy element, który został wstawiony. Zależnie od logiki serwera mogą mieć dodatkowe lub zmodyfikowane dane w porównaniu toowhat przekazano toohello serwera.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Kod SWIFT**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Porady: modyfikowanie danych
tooupdate istniejącego wiersza, zmodyfikuj element i wywołanie `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Kod SWIFT**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

Można również podać identyfikator wiersza hello i pola hello zaktualizowane:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Kod SWIFT**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

Co najmniej hello `id` należy ustawić podczas wprowadzania aktualizacji.

## <a name="deleting"></a>Porady: usuwanie danych
Wywołanie toodelete element, `delete` z elementem hello:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Kod SWIFT**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Alternatywnie usunięcia, podając identyfikator wiersza:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Kod SWIFT**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Co najmniej hello `id` atrybut musi być ustawiony w przypadku usunięcia wprowadzania.

## <a name="customapi"></a>Porady: wywołanie niestandardowego interfejsu API
Z niestandardowego interfejsu API pozwala udostępnić wszystkie funkcje wewnętrznej bazy danych. Nie ma operacji tabeli tooa toomap. Nie tylko możesz uzyskać większą kontrolę nad wiadomości, można nawet odczytu/ustawiania nagłówków i zmień format treści odpowiedzi hello. toolearn, w jaki sposób odczytać toocreate niestandardowego interfejsu API hello wewnętrznej bazy danych, [niestandardowych interfejsów API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

Wywołanie toocall niestandardowego interfejsu API `MSClient.invokeAPI`. Witaj żądań i odpowiedzi zawartości są traktowane jako JSON. toouse inne typy nośników [Użyj hello inne przeciążenia `invokeAPI` ] [ 5].  toomake `GET` żądania zamiast `POST` żądania, ustaw parametr `HTTPMethod` za`"GET"` i parametru `body` zbyt`nil` (ponieważ żądania GET nie ma treści wiadomości.) Niestandardowy interfejs API obsługuje inne zleceń HTTP, zmiana `HTTPMethod` odpowiednio.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Kod SWIFT**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Porady: rejestr wypychania szablony toosend wieloplatformowych powiadomienia
Szablony tooregister przekazać szablony z Twojej **client.push registerDeviceToken** metody w aplikacji klienta.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Kod SWIFT**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Szablony typu NSDictionary i mogą zawierać wiele szablonów w hello następującego formatu:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Kod SWIFT**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Wszystkie tagi są usuwane z żądania hello zabezpieczeń.  znaczniki tooadd tooinstallations lub szablonów w ramach instalacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][4].  toosend powiadomienia za pomocą tych szablonów zarejestrowanych pracować z [interfejsów API centra powiadomień][3].

## <a name="errors"></a>Porady: obsługa błędów
Podczas wywoływania zaplecze aplikacji mobilnej Azure App Service zawiera bloku ukończenia hello `NSError` parametru. Gdy wystąpi błąd, ten parametr jest tokenem nil. W kodzie należy sprawdzić ten parametr i obsługi błędu hello zgodnie z potrzebami, jak pokazano w hello poprzedzających fragmentów kodu.

Plik Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definiuje stałe hello `MSErrorResponseKey`, `MSErrorRequestKey`, i `MSErrorServerItemKey`. tooget toohello błąd związany z większej ilości danych:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Kod SWIFT**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Ponadto plik hello definiuje stałe dla każdego kod błędu:

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**Kod SWIFT**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Porady: uwierzytelniać użytkowników za pomocą hello biblioteki uwierzytelniania usługi Active Directory
Witaj Active Directory Authentication Library (ADAL) toosign użytkowników służy do aplikacji przy użyciu usługi Azure Active Directory. Przepływ uwierzytelnianie przy użyciu dostawcy tożsamości zestawu SDK jest preferowana toousing hello `loginWithProvider:completion:` metody.  Uwierzytelnianie klienta przepływu zapewnia bardziej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.

1. Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD przez następujące hello [jak tooconfigure aplikacji usługi dla usługi Active Directory logowania] [ 7] samouczka. Upewnij się, że toocomplete hello opcjonalny krok rejestrowania aplikację native client. Dla systemu iOS, zaleca się tym przekierowania hello URI ma formę hello `<app-scheme>://<bundle-id>`. Aby uzyskać więcej informacji, zobacz hello [ADAL dla systemu iOS — Szybki Start][8].
2. Instalowanie przy użyciu programu Cocoapods biblioteki ADAL. Edytuj hello tooinclude Podfile po definicji, zastępując **YOUR PROJECT** o nazwie hello projektu Xcode:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   i hello Pod:

        pod 'ADALiOS'
3. Przy użyciu hello Terminal, uruchom `pod install` z katalogu hello zawierający projektu, a następnie otwórz wygenerowany hello obszaru roboczego Xcode (nie projekt hello).
4. Dodaj hello następującego kodu tooyour aplikacji, zgodnie z toohello język, którego używasz. W każdym należy te elementy zastępcze:

   * Zastąp **INSERT urzędu tutaj** o nazwie hello hello dzierżawy, w którym są udostępniane aplikacji. Format powinien być https://login.microsoftonline.com/contoso.onmicrosoft.com. Ta wartość może zostać skopiowany z hello kartę domeny w usłudze Azure Active Directory w hello [klasyczny portal Azure].
   * Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta powitania dla zaplecza aplikacji mobilnej. Identyfikator klienta można uzyskać z hello **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu hello.
   * Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta hello skopiowany z hello aplikację native client.
   * Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS. Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Kod SWIFT**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Porady: uwierzytelniać użytkowników za pomocą hello Facebook zestawu SDK dla systemu iOS
Witaj zestawu SDK usługi Facebook dla użytkowników systemu iOS toosign służy do aplikacji za pomocą usługi Facebook.  Przy użyciu uwierzytelniania przepływu klienta jest preferowana toousing hello `loginWithProvider:completion:` metody.  powitania klienta przepływ uwierzytelniania zapewnia bardziej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.

1. Konfigurowanie zaplecza aplikacji mobilnej dla logowania w witrynie Facebook, wykonując [jak tooconfigure aplikacji usługi Facebook logowania] [ 9] samouczka.
2. Zainstaluj hello Facebook zestawu SDK dla systemu iOS przez następujące hello [Facebook SDK dla systemu iOS — wprowadzenie] [ 10] dokumentacji. Zamiast tworzenia aplikacji, można dodać hello iOS platform tooyour istniejącej rejestracji.
3. Dokumentacja w serwisie Facebook zawiera kod języka Objective-C w hello delegata aplikacji. Jeśli używasz **Swift**, można użyć następującego tłumaczenia AppDelegate.swift hello:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. W dodatku tooadding `FBSDKCoreKit.framework` tooyour projektu, również dodać odwołanie za`FBSDKLoginKit.framework` w hello tak samo.
5. Dodaj hello następującego kodu tooyour aplikacji, zgodnie z toohello język, którego używasz.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Kod SWIFT**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Porady: uwierzytelniać użytkowników za pomocą usługi Twitter sieci szkieletowej dla systemu iOS
Sieci szkieletowej dla użytkowników systemu iOS toosign służy do aplikacji przy użyciu usługi Twitter. Uwierzytelnianie przepływu klienta jest preferowanym toousing hello `loginWithProvider:completion:` metody, ponieważ zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.

1. Konfigurowanie zaplecza aplikacji mobilnej dla logowania w serwisie Twitter przy powitania po [jak tooconfigure aplikacji usługi Twitter logowania](app-service-mobile-how-to-configure-twitter-authentication.md) samouczka.
2. Dodaj projekt tooyour sieci szkieletowej przez następujące hello [sieci szkieletowej dla systemu iOS — wprowadzenie] dokumentacji i konfigurując TwitterKit.

   > [!NOTE]
   > Domyślnie sieci szkieletowej tworzy aplikację usługi Twitter dla Ciebie. Można uniknąć tworzenia aplikacji, rejestrując hello klucz klienta i klucz tajny klienta został utworzony wcześniej przy użyciu powitania po wstawki kodu.    Alternatywnie można zastąpić hello konsumenta i tooApp usługi z hello wartości, należy podać wartości klucz tajny klienta, zobacz w hello [pulpitu nawigacyjnego sieci szkieletowej]. Jeśli wybierzesz tę opcję, należy się tooset hello wywołania zwrotnego adresu URL tooa wartości symbolu zastępczego, takich jak `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Jeśli wybierzesz toouse hello klucze tajne, utworzony wcześniej, Dodaj następujące tooyour kodu delegata aplikacji hello:

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Kod SWIFT**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Dodaj hello następującego kodu tooyour aplikacji, zgodnie z toohello język, którego używasz.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Kod SWIFT**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Porady: uwierzytelniać użytkowników za pomocą hello Google logowania zestawu SDK dla systemu iOS
Hello Google logowania zestawu SDK dla systemu iOS toosign użytkowników służy do aplikacji przy użyciu konta Google.  Google zapowiedziała niedawno zasady zabezpieczeń OAuth tootheir zmiany.  Te zmiany zasad wymaga stosowania hello zestaw SDK Google w przyszłości hello.

1. Konfigurowanie zaplecza aplikacji mobilnej dla logowania w witrynie Google przez następujące hello [jak tooconfigure aplikacji usługi Google logowania](app-service-mobile-how-to-configure-google-authentication.md) samouczka.
2. Zainstaluj hello Google zestawu SDK dla systemu iOS przez następujące hello [Google logowania dla systemu iOS — rozpocząć integrowanie](https://developers.google.com/identity/sign-in/ios/start-integrating) dokumentacji. Możesz pominąć hello sekcji "Uwierzytelnianie z serwera wewnętrznej bazy danych".
3. Dodaj powitania po delegata tooyour `signIn:didSignInForUser:withError:` metody, zgodnie z toohello języka.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Kod SWIFT**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Upewnij się, że można również dodać powitania po zbyt`application:didFinishLaunchingWithOptions:` w aplikacji delegować, zastępując "SERVER_CLIENT_ID" hello sam identyfikator tej należy używać tooconfigure App Service w kroku 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Kod SWIFT**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Dodaj następującego kodu aplikacji tooyour UIViewController, który implementuje hello hello `GIDSignInUIDelegate` protokołu, zgodnie z toohello języka.  Zalogowano przed Trwa logowanie ponownie, a mimo że nie ma potrzeby tooenter poświadczenia ponownie, zobacz okno dialogowe zgody.  Tę metodę należy wywoływać tylko wtedy, gdy wygaśnie hello tokenu sesji.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Kod SWIFT**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure Mobile Apps Szybki Start]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[dynamiczne schematu]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[pulpitu nawigacyjnego sieci szkieletowej]: https://www.fabric.io/home
[sieci szkieletowej dla systemu iOS — wprowadzenie]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
