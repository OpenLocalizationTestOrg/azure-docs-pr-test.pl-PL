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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="4f412-103">Mostek iOS widoku sieci Web z natywnego Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="4f412-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f412-104">Mostek systemu android</span><span class="sxs-lookup"><span data-stu-id="4f412-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="4f412-105">Mostek z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="4f412-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="4f412-106">Niektóre aplikacje mobilne są zaprojektowane jako aplikacji hybrydowych, gdy aplikacja hello jest utworzony przy użyciu opracowywania aplikacji systemu iOS natywnego języka Objective-C, ale niektóre lub nawet wszystkich ekranów powitalnych są renderowane w widoku sieci Web z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="4f412-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="4f412-107">Możesz nadal korzystać z usługi Mobile Engagement iOS SDK w ramach tych aplikacji i w tym samouczku opisano sposób toogo o tej czynności.</span><span class="sxs-lookup"><span data-stu-id="4f412-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="4f412-108">Istnieją dwa podejścia tooachieve to chociaż są nieudokumentowanej:</span><span class="sxs-lookup"><span data-stu-id="4f412-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="4f412-109">Najpierw jeden opisane w tym [łącze](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) który obejmuje rejestrowanie `UIWebViewDelegate` w widoku sieci web i catch i natychmiast Anuluj zmiany lokalizacji wykonywane w języku Javascript.</span><span class="sxs-lookup"><span data-stu-id="4f412-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="4f412-110">Drugi jedną opiera się na tym [sesji WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615), podejście, które jest bardziej czytelny niż hello najpierw i firma Microsoft przestrzega tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="4f412-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="4f412-111">Należy pamiętać, że ta metoda działa tylko w systemie iOS7 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="4f412-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="4f412-112">Wykonaj poniższe kroki hello dla hello iOS zestawiania próbki:</span><span class="sxs-lookup"><span data-stu-id="4f412-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="4f412-113">Przede wszystkim należy tooensure, który ma przeszli naszych [Wprowadzenie — samouczek](mobile-engagement-ios-get-started.md) hello toointegrate Mobile Engagement iOS SDK w aplikacji hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="4f412-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="4f412-114">Opcjonalnie można również włączyć, testu w następujący sposób rejestrowania, aby mogli przeglądać hello SDK metod, zgodnie z ich wyzwalana hello widok sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4f412-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="4f412-115">Teraz upewnij się, że aplikacji hybrydowych ma ekran z widoku sieci Web na nim.</span><span class="sxs-lookup"><span data-stu-id="4f412-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="4f412-116">Można dodać toohello `Main.storyboard` aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4f412-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="4f412-117">Skojarz ten widok sieci Web z Twojej **ViewController** klikając i przeciągając hello widoku sieci Web z hello sceny kontrolera widoku toohello `ViewController.h` Edytuj ekranu umieszczenia go poniżej hello `@interface` wiersza.</span><span class="sxs-lookup"><span data-stu-id="4f412-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="4f412-118">Po wykonaniu tej czynności okno dialogowe będzie wyskakujące monitowania o nazwę.</span><span class="sxs-lookup"><span data-stu-id="4f412-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="4f412-119">Podaj nazwę hello jako **webView**.</span><span class="sxs-lookup"><span data-stu-id="4f412-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="4f412-120">Twoje `ViewController.h` plik powinien wyglądać jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="4f412-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="4f412-121">Firma Microsoft będzie aktualizować hello `ViewController.m` pliku później, ale najpierw utworzymy hello Mostek pliku, który tworzy otokę przez niektóre typowe Mobile Engagement iOS SDK metody.</span><span class="sxs-lookup"><span data-stu-id="4f412-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="4f412-122">Utwórz nowy plik nagłówka o nazwie **EngagementJsExports.h** , który używa hello `JSExport` mechanizm opisane w wyżej wymienionym hello [sesji](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello natywnego iOS metody.</span><span class="sxs-lookup"><span data-stu-id="4f412-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="4f412-123">Następnie utworzymy hello drugiej części hello Mostek pliku.</span><span class="sxs-lookup"><span data-stu-id="4f412-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="4f412-124">Utwórz plik o nazwie **EngagementJsExports.m** zawierający implementację hello tworzenia otoki rzeczywiste hello wywoływania hello Mobile Engagement iOS SDK metod.</span><span class="sxs-lookup"><span data-stu-id="4f412-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="4f412-125">Należy także zauważyć, że firma Microsoft hello są analizowania `extras` przekazywany z hello webview javascript i który do umieszczania `NSMutableDictionary` toobe obiektu przekazany z hello metodę Engagement SDK wywołania.</span><span class="sxs-lookup"><span data-stu-id="4f412-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="4f412-126">Teraz możemy następnie wróć toohello **ViewController.m** i zaktualizować go z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="4f412-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="4f412-127">Uwaga hello następujące kwestie dotyczące hello **ViewController.m** pliku:</span><span class="sxs-lookup"><span data-stu-id="4f412-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="4f412-128">W hello `loadWebView` metody, możemy ładowania lokalnego pliku o nazwie **LocalPage.html** którego kod Zapoznamy się obok.</span><span class="sxs-lookup"><span data-stu-id="4f412-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="4f412-129">W hello `webViewDidFinishLoad` metody, możemy są dane hello `JsContext` i kojarzenie z nim naszej klasy otoki.</span><span class="sxs-lookup"><span data-stu-id="4f412-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="4f412-130">Umożliwi to wywołanie naszych otoki metod SDK przy użyciu dojścia hello **EngagementJs** hello widok sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4f412-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="4f412-131">Utwórz plik o nazwie **LocalPage.html** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="4f412-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
10. <span data-ttu-id="4f412-132">Uwaga hello następujące kwestie dotyczące pliku HTML hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="4f412-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="4f412-133">Zawiera zestaw wejściowy pól, w którym można podać toobe danych używane jako nazwy dla zdarzeń, zadania, błąd, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="4f412-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="4f412-134">Po kliknięciu hello przycisku Dalej tooit toohello Javascript, który ostatecznie wywołuje metody hello z hello Mostek pliku toopass toohello to wywołanie usługi Mobile Engagement iOS SDK jest nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="4f412-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="4f412-135">Czy firma Microsoft znakowanie na niektóre zdarzenia toohello statycznych dodatkowe informacje, zadań i nawet błędy toodemonstrate jak można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="4f412-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="4f412-136">Te dodatkowe informacje są wysyłane jako JSON ciąg, który w hello `EngagementJsExports.m` pliku, jest analizowana i przekazywane wraz ze zdarzeń, zadań, błędy wysyłania.</span><span class="sxs-lookup"><span data-stu-id="4f412-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="4f412-137">Zadanie Mobile Engagement zostało rozpoczęte o nazwie hello określonej w polu wejściowym hello, uruchom na 10 sekund i zamknąć.</span><span class="sxs-lookup"><span data-stu-id="4f412-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="4f412-138">Mobile Engagement appinfo lub znacznik jest przekazywany z "customer_name" hello statyczny klucz i wartość hello, wprowadzone w danych wejściowych hello jako wartość hello hello tagu.</span><span class="sxs-lookup"><span data-stu-id="4f412-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="4f412-139">Hello wykonywania aplikacji i zobaczą hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="4f412-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="4f412-140">Teraz niektóre nazwy zdarzenie testowe, takich jak powitania po i kliknij przycisk **wysyłania** tooit dalej.</span><span class="sxs-lookup"><span data-stu-id="4f412-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="4f412-141">Obecnie przejście toohello **Monitor** kartę aplikacji i wyglądu w obszarze **zdarzenia -> Szczegóły**, zobaczysz tego zdarzenia wyświetlane wraz z hello statyczne informacje o aplikacji, które firma Microsoft wysyłania.</span><span class="sxs-lookup"><span data-stu-id="4f412-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
