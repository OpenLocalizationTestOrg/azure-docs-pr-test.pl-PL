---
title: iOS aaaBridge widoku sieci Web z natywnego Mobile Engagement iOS SDK
description: "Opisuje sposób toocreate mostka między systemem obsługi języka Javascript i hello natywnego Mobile Engagement iOS SDK w widoku sieci Web"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Mostek iOS widoku sieci Web z natywnego Mobile Engagement iOS SDK
> [!div class="op_single_selector"]
> * [Mostek systemu android](mobile-engagement-bridge-webview-native-android.md)
> * [Mostek z systemem iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Niektóre aplikacje mobilne są zaprojektowane jako aplikacji hybrydowych, gdy aplikacja hello jest utworzony przy użyciu opracowywania aplikacji systemu iOS natywnego języka Objective-C, ale niektóre lub nawet wszystkich ekranów powitalnych są renderowane w widoku sieci Web z systemem iOS. Możesz nadal korzystać z usługi Mobile Engagement iOS SDK w ramach tych aplikacji i w tym samouczku opisano sposób toogo o tej czynności. 

Istnieją dwa podejścia tooachieve to chociaż są nieudokumentowanej:

* Najpierw jeden opisane w tym [łącze](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) który obejmuje rejestrowanie `UIWebViewDelegate` w widoku sieci web i catch i natychmiast Anuluj zmiany lokalizacji wykonywane w języku Javascript. 
* Drugi jedną opiera się na tym [sesji WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615), podejście, które jest bardziej czytelny niż hello najpierw i firma Microsoft przestrzega tego przewodnika. Należy pamiętać, że ta metoda działa tylko w systemie iOS7 i nowszych. 

Wykonaj poniższe kroki hello dla hello iOS zestawiania próbki:

1. Przede wszystkim należy tooensure, który ma przeszli naszych [Wprowadzenie — samouczek](mobile-engagement-ios-get-started.md) hello toointegrate Mobile Engagement iOS SDK w aplikacji hybrydowych. Opcjonalnie można również włączyć, testu w następujący sposób rejestrowania, aby mogli przeglądać hello SDK metod, zgodnie z ich wyzwalana hello widok sieci Web. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Teraz upewnij się, że aplikacji hybrydowych ma ekran z widoku sieci Web na nim. Można dodać toohello `Main.storyboard` aplikacji hello. 
3. Skojarz ten widok sieci Web z Twojej **ViewController** klikając i przeciągając hello widoku sieci Web z hello sceny kontrolera widoku toohello `ViewController.h` Edytuj ekranu umieszczenia go poniżej hello `@interface` wiersza. 
4. Po wykonaniu tej czynności okno dialogowe będzie wyskakujące monitowania o nazwę. Podaj nazwę hello jako **webView**. Twoje `ViewController.h` plik powinien wyglądać jak poniżej hello:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Firma Microsoft będzie aktualizować hello `ViewController.m` pliku później, ale najpierw utworzymy hello Mostek pliku, który tworzy otokę przez niektóre typowe Mobile Engagement iOS SDK metody. Utwórz nowy plik nagłówka o nazwie **EngagementJsExports.h** , który używa hello `JSExport` mechanizm opisane w wyżej wymienionym hello [sesji](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello natywnego iOS metody. 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. Następnie utworzymy hello drugiej części hello Mostek pliku. Utwórz plik o nazwie **EngagementJsExports.m** zawierający implementację hello tworzenia otoki rzeczywiste hello wywoływania hello Mobile Engagement iOS SDK metod. Należy także zauważyć, że firma Microsoft hello są analizowania `extras` przekazywany z hello webview javascript i który do umieszczania `NSMutableDictionary` toobe obiektu przekazany z hello metodę Engagement SDK wywołania.  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. Teraz możemy następnie wróć toohello **ViewController.m** i zaktualizować go z hello następującego kodu: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. Uwaga hello następujące kwestie dotyczące hello **ViewController.m** pliku:
   
   * W hello `loadWebView` metody, możemy ładowania lokalnego pliku o nazwie **LocalPage.html** którego kod Zapoznamy się obok. 
   * W hello `webViewDidFinishLoad` metody, możemy są dane hello `JsContext` i kojarzenie z nim naszej klasy otoki. Umożliwi to wywołanie naszych otoki metod SDK przy użyciu dojścia hello **EngagementJs** hello widok sieci Web. 
9. Utwórz plik o nazwie **LocalPage.html** z hello następującego kodu:
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. Uwaga hello następujące kwestie dotyczące pliku HTML hello powyżej:
    
    * Zawiera zestaw wejściowy pól, w którym można podać toobe danych używane jako nazwy dla zdarzeń, zadania, błąd, AppInfo. Po kliknięciu hello przycisku Dalej tooit toohello Javascript, który ostatecznie wywołuje metody hello z hello Mostek pliku toopass toohello to wywołanie usługi Mobile Engagement iOS SDK jest nawiązane połączenie. 
    * Czy firma Microsoft znakowanie na niektóre zdarzenia toohello statycznych dodatkowe informacje, zadań i nawet błędy toodemonstrate jak można to zrobić. Te dodatkowe informacje są wysyłane jako JSON ciąg, który w hello `EngagementJsExports.m` pliku, jest analizowana i przekazywane wraz ze zdarzeń, zadań, błędy wysyłania. 
    * Zadanie Mobile Engagement zostało rozpoczęte o nazwie hello określonej w polu wejściowym hello, uruchom na 10 sekund i zamknąć. 
    * Mobile Engagement appinfo lub znacznik jest przekazywany z "customer_name" hello statyczny klucz i wartość hello, wprowadzone w danych wejściowych hello jako wartość hello hello tagu. 
11. Hello wykonywania aplikacji i zobaczą hello poniżej. Teraz niektóre nazwy zdarzenie testowe, takich jak powitania po i kliknij przycisk **wysyłania** tooit dalej. 
    
     ![][1]
12. Obecnie przejście toohello **Monitor** kartę aplikacji i wyglądu w obszarze **zdarzenia -> Szczegóły**, zobaczysz tego zdarzenia wyświetlane wraz z hello statyczne informacje o aplikacji, które firma Microsoft wysyłania. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
