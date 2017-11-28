---
title: Mostek iOS widoku sieci Web z natywnego Mobile Engagement iOS SDK
description: "Opisuje sposób tworzenia mostka między systemem obsługi języka Javascript i natywnego Mobile Engagement iOS SDK widoku sieci Web"
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
ms.openlocfilehash: 35f7bdbeb480122513ae2a0b04a6d8cfd426802a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="1d3f2-103">Mostek iOS widoku sieci Web z natywnego Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="1d3f2-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d3f2-104">Mostek systemu android</span><span class="sxs-lookup"><span data-stu-id="1d3f2-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="1d3f2-105">Mostek z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="1d3f2-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="1d3f2-106">Niektóre aplikacje mobilne są zaprojektowane jako aplikacji hybrydowych, gdy aplikacja jest utworzony przy użyciu opracowywania aplikacji systemu iOS natywnego języka Objective-C, ale niektóre lub nawet wszystkich ekranów są renderowane w widoku sieci Web z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native iOS Objective-C development but some or even all of the screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="1d3f2-107">Możesz nadal korzystać z usługi Mobile Engagement iOS SDK w ramach tych aplikacji i w tym samouczku opisano sposób Przejdź o tej czynności.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how to go about doing this.</span></span> 

<span data-ttu-id="1d3f2-108">Istnieją dwie metody, można to osiągnąć, chociaż są nieudokumentowanej:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-108">There are two approaches to achieve this though both are undocumented:</span></span>

* <span data-ttu-id="1d3f2-109">Najpierw jeden opisane w tym [łącze](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) który obejmuje rejestrowanie `UIWebViewDelegate` w widoku sieci web i catch i natychmiast Anuluj zmiany lokalizacji wykonywane w języku Javascript.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="1d3f2-110">Drugi jedną opiera się na tym [sesji WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615), podejście, które jest bardziej czytelny niż pierwszy i firma Microsoft przestrzega tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than the first and which we will follow for this guide.</span></span> <span data-ttu-id="1d3f2-111">Należy pamiętać, że ta metoda działa tylko w systemie iOS7 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="1d3f2-112">Dla systemu iOS zestawiania próbki, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-112">Follow the steps below for the iOS bridge sample:</span></span>

1. <span data-ttu-id="1d3f2-113">Po pierwsze, należy się upewnić, że przeszły naszych [Wprowadzenie — samouczek](mobile-engagement-ios-get-started.md) integracja Mobile Engagement iOS SDK w aplikacji hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-113">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) to integrate the Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="1d3f2-114">Opcjonalnie można również włączyć, testu w następujący sposób rejestrowania, dzięki czemu można wyświetlić metody zestawu SDK, jak wyzwalana je z widoku sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-114">Optionally, you can also enable test logging as follows so that you can see the SDK methods as we trigger them from the webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="1d3f2-115">Teraz upewnij się, że aplikacji hybrydowych ma ekran z widoku sieci Web na nim.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="1d3f2-116">Można dodać go do `Main.storyboard` aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-116">You can add it to the `Main.storyboard` of the app.</span></span> 
3. <span data-ttu-id="1d3f2-117">Skojarz ten widok sieci Web z Twojej **ViewController** klikając i przeciągając widoku sieci Web z scenę kontrolera widoku w celu `ViewController.h` ekranu umieszczenia go edytować tylko poniżej `@interface` wiersza.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-117">Associate this webview with your **ViewController** by clicking and dragging the webview from the View Controller Scene to the `ViewController.h` edit screen, placing it just below the `@interface` line.</span></span> 
4. <span data-ttu-id="1d3f2-118">Po wykonaniu tej czynności okno dialogowe będzie wyskakujące monitowania o nazwę.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="1d3f2-119">Podaj nazwę jako **webView**.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-119">Provide the name as **webView**.</span></span> <span data-ttu-id="1d3f2-120">Twoje `ViewController.h` pliku powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-120">Your `ViewController.h` file should look like the following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="1d3f2-121">Firma Microsoft będzie aktualizować `ViewController.m` pliku później, ale najpierw utworzymy pliku mostek, który tworzy otokę przez niektóre typowe Mobile Engagement iOS SDK metody.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-121">We will update the `ViewController.m` file later but first we will create the bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="1d3f2-122">Utwórz nowy plik nagłówka o nazwie **EngagementJsExports.h** używający `JSExport` mechanizm opisane w powyższym formularzu [sesji](https://developer.apple.com/videos/play/wwdc2013/615) do udostępnienia metody natywnej dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-122">Create a new header file called **EngagementJsExports.h** which uses the `JSExport` mechanism described in the aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) to expose the native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="1d3f2-123">Następnie utworzymy drugiej części pliku mostek.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-123">Next we will create the second part of the bridge file.</span></span> <span data-ttu-id="1d3f2-124">Utwórz plik o nazwie **EngagementJsExports.m** zawierający implementację tworzenia otoki rzeczywiste przez wywołanie usługi Mobile Engagement iOS SDK metody.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-124">Create a file called **EngagementJsExports.m** which will contain the implementation creating the actual wrappers by calling the Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="1d3f2-125">Należy także zauważyć, że firma Microsoft podczas analizowania `extras` przekazywany z poziomu języka javascript widoku sieci Web i który do umieszczania `NSMutableDictionary` obiekt przekazywany z wywołań metody Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-125">Also note that we are parsing the `extras` being passed from the webview javascript and putting that into an `NSMutableDictionary` object to be passed with the Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="1d3f2-126">Teraz możemy wróć do **ViewController.m** i zaktualizować go następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-126">Now we come back to the **ViewController.m** and update it with the following code:</span></span> 
   
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
8. <span data-ttu-id="1d3f2-127">Należy zwrócić uwagę następujące kwestie dotyczące **ViewController.m** pliku:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-127">Note the following points about the **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="1d3f2-128">W `loadWebView` metody, możemy ładowania lokalnego pliku o nazwie **LocalPage.html** którego kod Zapoznamy się obok.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-128">In the `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="1d3f2-129">W `webViewDidFinishLoad` metody, możemy są dane `JsContext` i kojarzenie z nim naszej klasy otoki.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-129">In the `webViewDidFinishLoad` method, we are grabbing the `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="1d3f2-130">Umożliwi to wywołanie naszych otoki metod SDK przy użyciu dojścia **EngagementJs** z widoku sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-130">This will allow calling our wrapper SDK methods using the handle **EngagementJs** from the webView.</span></span> 
9. <span data-ttu-id="1d3f2-131">Utwórz plik o nazwie **LocalPage.html** następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-131">Create a file called **LocalPage.html** with the following code:</span></span>
   
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
                       // Example of how extras info can be passed with the Engagement logs
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
10. <span data-ttu-id="1d3f2-132">Należy uwzględnić następujące kwestie dotyczące pliku w formacie HTML powyżej:</span><span class="sxs-lookup"><span data-stu-id="1d3f2-132">Note the following points about the HTML file above:</span></span>
    
    * <span data-ttu-id="1d3f2-133">Zawiera zestaw wejściowy pól, w którym można podać dane mają być używane jako nazwy dla zdarzeń, zadania, błąd, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-133">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="1d3f2-134">Po kliknięciu przycisku Dalej, aby go połączenie jest nawiązywane w przypadku Javascript, który ostatecznie wywołuje metody z pliku mostek do przekazania to wywołanie usługi Mobile Engagement iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-134">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="1d3f2-135">Firma Microsoft są znakowanie na niektórych statycznych dodatkowe informacje do zdarzeń, zadania i nawet błędów, aby zademonstrować, jak można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-135">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="1d3f2-136">Te dodatkowe informacje są wysyłane jako JSON ciąg, który w `EngagementJsExports.m` pliku, jest analizowana i przekazywane wraz ze zdarzeń, zadań, błędy wysyłania.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-136">This extra info is sent as a JSON string which, if you look in the `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="1d3f2-137">Zadanie Mobile Engagement zostało rozpoczęte o nazwie określonej w polu wejściowym, uruchom na 10 sekund i zamknąć.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-137">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="1d3f2-138">Usługa Mobile Engagement appinfo lub znacznik jest przekazywany z "customer_name" jako statyczny klucz i wartość wprowadzona w danych wejściowych jako wartość tagu.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
11. <span data-ttu-id="1d3f2-139">Uruchom aplikację i pojawi się poniżej.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-139">Run the app and you will see the following.</span></span> <span data-ttu-id="1d3f2-140">Teraz niektóre nazwy zdarzenie testowe, podobnie jak poniżej i kliknij przycisk **wysyłania** obok niej.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-140">Now provide some name for a test event like the following and click **Send** next to it.</span></span> 
    
     ![][1]
12. <span data-ttu-id="1d3f2-141">Teraz, jeśli przejdziesz do **Monitor** kartę aplikacji i wyglądu w obszarze **zdarzenia -> Szczegóły**, zobaczysz tego zdarzenia wyświetlane wraz ze statycznego aplikacji — informacje, które firma Microsoft wysyłania.</span><span class="sxs-lookup"><span data-stu-id="1d3f2-141">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
