---
title: "tooiOS powiadomienia wypychane aaaSending przy użyciu usługi Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse wypychanych aplikacji dla systemu iOS tooan powiadomienia."
services: notification-hubs
documentationcenter: ios
keywords: powiadomienie wypychane, powiadomienia wypychane, powiadomienia wypychane w systemie ios
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>Wysyłanie tooiOS powiadomień wypychanych przy użyciu usługi Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanych aplikacji dla systemu iOS tooan powiadomienia. Utworzysz aplikację iOS puste, która odbiera powiadomienia wypychane przy użyciu hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.

## <a name="before-you-begin"></a>Przed rozpoczęciem
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Kod ukończyć powitalnych dla tego samouczka można znaleźć [w serwisie GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* [usług Mobile Services systemu iOS SDK w wersji 1.2.4]
* Najnowsza wersja środowiska [Xcode]
* Urządzenie zgodne z systemem iOS 8 (lub nowszą wersją)
* Członkostwo w [programie dla deweloperów firmy Apple](https://developer.apple.com/programs/)
  
  > [!NOTE]
  > Ze względu na wymagania dotyczące konfiguracji powiadomień wypychanych należy wdrożyć i przetestować powiadomienia wypychane na urządzenie fizyczne z systemem iOS (iPhone i iPad) zamiast hello symulatora systemu iOS.
  > 
  > 

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Konfigurowanie centrum powiadomień dla powiadomień wypychanych systemu iOS
Ta sekcja przeprowadzi Cię przez proces tworzenia nowego centrum powiadomień i konfigurowania uwierzytelniania w usłudze APNS przy użyciu hello **.p12** utworzony certyfikat wypychania. Jeśli chcesz toouse Centrum powiadomień, które zostały już utworzone, możesz pominąć toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Kliknij przycisk hello <b>usługi powiadomień</b> przycisku na powitania <b>ustawienia</b> bloku, następnie wybierz <b>Apple (APNS)</b>. Polecenie <b>Przekaż certyfikat</b> i wybierz hello <b>.p12</b> wcześniej wyeksportowany plik. Upewnij się, że należy także określić hello poprawne hasło.</p>

<p>Upewnij się, że tooselect <b>piaskownicy</b> trybu, ponieważ jest to do tworzenia aplikacji. Używaj tylko hello <b>produkcji</b> Chcąc toosend toousers powiadomień wypychanych, którzy kupili twoją aplikację w sklepie hello.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Konfigurowanie usługi APNS w portalu Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Konfigurowanie certyfikacji APNs w witrynie Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

Centrum powiadomień jest teraz skonfigurowany toowork przy użyciu usługi APNS i mieć tooregister ciągów połączenia hello aplikacji oraz wysyłać powiadomienia wypychane.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Połącz z tooNotification aplikacji systemu iOS koncentratory
1. W środowisku Xcode Utwórz nowy projekt dla systemu iOS, a następnie wybierz hello **pojedynczą aplikacją widoku** szablonu.
   
    ![Xcode — aplikacja z jednym widokiem][8]
    
2. Podczas ustawiania opcji hello nowego projektu, upewnij się, toouse hello sam **nazwa produktu** i **identyfikator organizacji** które zostały użyte podczas wcześniejszego ustawiania Identyfikatora pakietu hello na powitania deweloperów firmy Apple Portal.
   
    ![Xcode — opcje projektu][11]
    
3. W obszarze **elementy docelowe**, kliknij nazwę projektu, kliknij przycisk hello **ustawieniach kompilacji** karcie i rozwiń **tożsamość podpisywania kodu**, a następnie w obszarze **debugowania**, ustaw swoją tożsamość podpisywania kodu. Przełącz **poziomy** z **podstawowe** za**wszystkie**i ustaw **profilu inicjowania obsługi administracyjnej** toohello profil utworzony wcześniej inicjowania obsługi administracyjnej .
   
    Jeśli nie widzisz hello nowych inicjowania obsługi profilu utworzonego w programie Xcode, spróbuj odświeżyć hello profile dla Twojej tożsamości podpisywania. Kliknij przycisk **Xcode** hello paska menu, kliknij przycisk **preferencje**, kliknij hello **konta** , kliknij pozycję hello **Wyświetl szczegóły** , kliknij użytkownika tożsamość podpisywania, a następnie kliknij przycisk Odśwież hello hello prawym dolnym rogu.
   
    ![Xcode — profil aprowizowania][9]
4. Pobierz hello [usług Mobile Services systemu iOS SDK w wersji 1.2.4] i rozpakuj plik hello. W programie Xcode, kliknij prawym przyciskiem myszy projekt i kliknij przycisk hello **Dodaj pliki do** hello tooadd opcji **WindowsAzureMessaging.framework** projektu Xcode tooyour folderu. Wybierz pozycję **Copy items if needed** (Skopiuj elementy w razie potrzeby), a następnie kliknij pozycję **Add** (Dodaj).
   
   > [!NOTE]
   > centra powiadomień Hello zestawu SDK nie obsługuje obecnie kodu bitowego w programie Xcode 7.  Należy ustawić **włączyć Bitcode** za**nr** w hello **opcji kompilacji** dla projektu.
   > 
   > 
   
    ![Rozpakowywanie zestawu SDK platformy Azure][10]
5. Dodawanie nowego nagłówka pliku tooyour projektu o nazwie `HubInfo.h`. Ten plik będzie zawierać hello stałe dla Centrum powiadomień.  Dodaj następujące definicje hello i Zastąp hello symbole zastępcze literału ciągu z Twojej *nazwy centrum* i hello *DefaultListenSharedAccessSignature* zanotowany wcześniej.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Otwórz z `AppDelegate.h` pliku Dodaj następujące dyrektywy importu hello:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. W Twojej `AppDelegate.m file`, Dodaj hello następującego kodu w hello `didFinishLaunchingWithOptions` zależnie od wersji systemu iOS. Ten kod rejestruje dojście do urządzenia w usłudze APNs:
   
    Dla systemu iOS 8:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Dla too8 wcześniejsze wersje systemu iOS:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. W hello tego samego pliku, Dodaj następujące metody hello. Ten kod łączy toohello Centrum powiadomień przy użyciu hello informacji o połączeniu określonych w pliku HubInfo.h. Następnie przekazuje Centrum powiadomień token toohello urządzenia hello tak, aby hello Centrum powiadomień może wysyłać powiadomienia:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. W hello tego samego pliku, Dodaj następujące metody toodisplay hello **UIAlert** w przypadku otrzymania powiadomienia hello, gdy aplikacja hello jest aktywna:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Tworzenie i uruchamianie aplikacji hello na tooverify Twojego urządzenia, czy nie występują żadne błędy.

## <a name="send-test-push-notifications"></a>Wysyłanie testowych powiadomień wypychanych
Możesz przetestować odbieranie powiadomień w aplikacji przez wysyłanie powiadomień wypychanych w hello [Azure Portal] za pośrednictwem hello **Rozwiązywanie problemów** sekcji w bloku Centrum hello (Użyj hello *Wysyłanietestowe* opcja).

![Portal Azure — wysyłanie testowe][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Opcjonalnie) Wysyłanie powiadomień wypychanych z aplikacji hello
> [!IMPORTANT]
> Przykładem wysyłania powiadomień z powitania klienta aplikacji jest dostępna dla tylko do celów szkoleniowych. Ponieważ wymaga to hello `DefaultFullSharedAccessSignature` toobe na powitania klienta aplikacji, opisuje czy użytkownik może uzyskać powiadomienia toosend nieautoryzowany dostęp tooyour klientów ryzyko toohello Centrum powiadomień.
> 
> 

Jeśli chcesz toosend powiadomień wypychanych z poziomu aplikacji, ta sekcja zawiera przykładowy sposób toodo to przy użyciu hello interfejsu REST.

1. Otwórz w programie Xcode, `Main.storyboard` i dodaj następujące składniki interfejsu użytkownika z hello obiekt bibliotece tooallow hello użytkownika toosend powiadomień wypychanych w aplikacji hello hello:
   
   * Etykieta bez tekstu etykiety. Będzie ona używana tooreport błędów wysyłania powiadomień. Witaj **wierszy** właściwość powinna być ustawiona zbyt**0** tak, aby automatycznie zmieni rozmiar, prawo ograniczonego toohello i prawego marginesu oraz góry hello hello widoku.
   * Pole tekstowe **symbolu zastępczego** tekst jest ustawiany za**wprowadź komunikat powiadomienia**. Ogranicz pole hello poniżej hello etykiety, jak pokazano poniżej. Ustaw hello kontroler widoku jako delegat gniazda hello.
   * Przycisk zatytułowany **Wyślij powiadomienie E-mail** ograniczony bezpośrednio poniżej pola tekstowego hello i w poziomie Centrum hello.
     
     Widok Hello powinna wyglądać następująco:
     
     ![Projektant programu Xcode][32]
2. [Dodaj gniazda](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) dla hello etykiety i pola tekstowego połączonych z widokiem i zaktualizuj Twojej `interface` toosupport definicji `UITextFieldDelegate` i `NSXMLParserDelegate`. Dodaj hello trzy deklaracje właściwości przedstawione poniżej toohelp obsługę wywoływania hello interfejsu API REST i analizowanie odpowiedzi hello.
   
    Plik ViewController.h powinien wyglądać następująco:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Otwórz `HubInfo.h` i Dodaj hello następujące ograniczenia, które będą używane do wysyłania powiadomień tooyour koncentratora. Zamień na powitania symbol zastępczy literału ciągu rzeczywistymi *DefaultFullSharedAccessSignature* parametry połączenia.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Dodaj następujące hello `#import` tooyour instrukcje `ViewController.h` pliku.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. W `ViewController.m` dodać powitania po implementacji interfejsu toohello kodu. Ten kod będzie analizować parametry połączenia *DefaultFullSharedAccessSignature*. Jak wspomniano w hello [dokumentacji interfejsu API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), te przeanalizowane informacje będą używane toogenerate token sygnatury dostępu współdzielonego dla hello **autoryzacji** nagłówek żądania.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. W `ViewController.m`, hello aktualizacji `viewDidLoad` metody tooparse hello ciągu połączenia podczas ładowania widoku hello. Dodaj również metody narzędziowe hello, pokazano poniżej, toohello implementacji interfejsu.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. W `ViewController.m`, Dodaj hello następującego kodu toohello interfejsu implementacji toogenerate hello tokenu sygnatury dostępu współdzielonego autoryzacji zapewnianej w hello **autoryzacji** nagłówka, jak wspomniano w hello [interfejsu API REST Odwołanie](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL i przeciągnij od hello **Wyślij powiadomienie E-mail** przycisk zbyt`ViewController.m` tooadd akcji o nazwie **SendNotificationMessage** dla hello **Touch Down** zdarzeń. Zaktualizuj metodę przy hello następujące powiadomienia hello toosend kodu za pomocą hello interfejsu API REST.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. W `ViewController.m`, Dodaj powitania od zamknięcia hello klawiatury dla pola tekstowego hello toosupport metody delegata. CTRL i przeciągnij od hello tekst pola toohello ikony kontrolera widoku w hello interfejsu tooset projektanta hello wyświetlić kontroler jako delegat gniazda hello.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. W `ViewController.m`, Dodaj następujące hello delegować metody toosupport podczas analizowania odpowiedzi hello za pomocą `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Skompiluj projekt hello i sprawdź, czy nie ma żadnych błędów.

> [!NOTE]
> Jeśli wystąpi błąd kompilacji w Xcode7 dotyczące obsługi kodu bitowego, należy zmienić hello **ustawieniach kompilacji** > **włączyć Bitcode (ENABLE_BITCODE)** za**nr** w środowisku Xcode. Witaj zestaw SDK usługi Notification Hubs nie obsługuje obecnie kodu bitowego. 
> 
> 

Wszystkie hello możliwe ładunki powiadomień można znaleźć w hello Apple [lokalnych i wypychanych Podręcznik programowania powiadomień].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Sprawdzanie, czy aplikacja może odbierać powiadomienia wypychane
tootest powiadomienia wypychane w systemie iOS, należy wdrożyć urządzenie fizyczne z systemem iOS tooa aplikacji hello. Nie można wysłać powiadomień wypychanych firmy Apple przy użyciu hello symulatora systemu iOS.

1. Uruchamianie aplikacji hello i sprawdź, czy rejestracja zakończy się powodzeniem, a następnie naciśnij **OK**.
   
    ![Test rejestracji powiadomień wypychanych aplikacji dla systemu iOS][33]
2. Testowe powiadomienie wypychane możesz wysłać z hello [Azure Portal], zgodnie z powyższym opisem. Jeśli dodano kod umożliwiający wysyłanie powiadomień wypychanych w aplikacji hello, dotknij w tooenter pole tekstowe hello komunikatu powiadomienia. Następnie naciśnij klawisz hello **wysyłania** przycisk hello klawiatury lub hello **Wyślij powiadomienie E-mail** przycisku na powitania widoku toosend hello powiadomienie.
   
    ![Test wysyłania powiadomienia wypychanego z aplikacji dla systemu iOS][34]
3. Witaj powiadomienie wypychane zostanie wysłane tooall urządzeń, które są zarejestrowane tooreceive hello powiadomień z hello określonego Centrum powiadomień.
   
    ![Test odbierania powiadomienia wypychanego z aplikacji dla systemu iOS][35]

## <a name="next-steps"></a>Następne kroki
W tym prostym przykładzie wysłano tooall powiadomień wypychanych urządzeń z systemem iOS w zarejestrowany. Sugerujemy jako kolejny krok zapoznanie się czy kontynuować toohello [Azure Notification Hubs Powiadom użytkowników dla systemu iOS z zaplecza programu .NET] samouczek, który przeprowadzi Cię przez proces tworzenia wypychania toosend zaplecza powiadomienia przy użyciu tagów. 

Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz również przejść toohello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka. 

Ogólne informacje o usłudze Notification Hubs zawiera temat [Wskazówki dotyczące usługi Notification Hubs].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[usług Mobile Services systemu iOS SDK w wersji 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs Powiadom użytkowników dla systemu iOS z zaplecza programu .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[lokalnych i wypychanych Podręcznik programowania powiadomień]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
