---
title: aaaBridge Android widoku sieci Web z natywnego Mobile Engagement zestawu SDK systemu Android
description: "Opisuje sposób toocreate mostka między WebView uruchomione Javascript i hello zestaw macierzysty Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="772d3-103">Mostek Android widoku sieci Web z natywnego Mobile Engagement zestawu SDK systemu Android</span><span class="sxs-lookup"><span data-stu-id="772d3-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="772d3-104">Mostek systemu android</span><span class="sxs-lookup"><span data-stu-id="772d3-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="772d3-105">Mostek z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="772d3-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="772d3-106">Niektóre aplikacje mobilne są zaprojektowane jako aplikacji hybrydowych, gdy aplikacja hello jest utworzony przy użyciu natywnych systemu Android, ale niektóre lub nawet wszystkich ekranów powitalnych są renderowane w widoku sieci Web dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="772d3-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="772d3-107">Może nadal używać zestaw Mobile Engagement Android SDK w ramach tych aplikacji i w tym samouczku opisano sposób toogo o tej czynności.</span><span class="sxs-lookup"><span data-stu-id="772d3-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="772d3-108">Poniższy kod przykładowy Hello jest oparta na hello dokumentację dla systemu Android [tutaj](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="772d3-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="772d3-109">Opisuje, jak można użyć tej metody udokumentowane tooimplement hello takie same dla zestaw Mobile Engagement Android SDK dla często używanych metod tak, aby Webview z aplikacji hybrydowych można także zainicjować zdarzenia tootrack żądania, zadań, błędów, informacje o aplikacji, podczas ich przez przekazanie w potoku naszego zestawu SDK systemu Android.</span><span class="sxs-lookup"><span data-stu-id="772d3-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="772d3-110">Przede wszystkim należy tooensure, który ma przeszli naszych [Wprowadzenie — samouczek](mobile-engagement-android-get-started.md) toointegrate hello zestaw Mobile Engagement Android SDK w aplikacji hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="772d3-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="772d3-111">Gdy to zrobisz, Twoje `OnCreate` metoda będzie wyglądać hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="772d3-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="772d3-112">Teraz upewnij się, że aplikacji hybrydowych ma ekran z widoku sieci Web na nim.</span><span class="sxs-lookup"><span data-stu-id="772d3-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="772d3-113">Witaj kod dla niego będzie podobne następujące toohello gdzie czy ładowanie lokalnego pliku **Sample.html** w hello widoku sieci Web w hello `onCreate` metodę ekranu.</span><span class="sxs-lookup"><span data-stu-id="772d3-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="772d3-114">Teraz Utwórz plik Mostek o nazwie **WebAppInterface** który tworzy otokę w niektóre często używane metody zestaw Mobile Engagement Android SDK za pomocą hello `@JavascriptInterface` podejścia opisanego w hello [dokumentację dla systemu Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="772d3-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="772d3-115">Gdy utworzono hello powyżej Mostek pliku, potrzebujemy tooensure, że jest on skojarzony z naszych widoku sieci Web.</span><span class="sxs-lookup"><span data-stu-id="772d3-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="772d3-116">Dla tego toohappen należy tooedit Twojego `SetWebview` metodę, tak że wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="772d3-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="772d3-117">W hello powyżej fragment, dzwoniliśmy `addJavascriptInterface` tooassociate naszych Mostek klasy z naszych widoku sieci Web, a także utworzony uchwyt o nazwie **EngagementJs** toocall hello metody z hello Mostek pliku.</span><span class="sxs-lookup"><span data-stu-id="772d3-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="772d3-118">Teraz utworzyć następującego pliku o nazwie hello **Sample.html** w projekcie w folderze o nazwie **zasoby** który jest ładowany do hello Webview i którym firma Microsoft będzie wywoływać metod hello z pliku Mostek hello.</span><span class="sxs-lookup"><span data-stu-id="772d3-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="772d3-119">Uwaga hello następujące kwestie dotyczące pliku HTML hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="772d3-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="772d3-120">Zawiera zestaw wejściowy pól, w którym można podać toobe danych używane jako nazwy dla zdarzeń, zadania, błąd, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="772d3-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="772d3-121">Po kliknięciu hello przycisku Dalej tooit toohello Javascript, który ostatecznie wywołuje metody hello z hello Mostek pliku toopass toohello tego wywołania zestaw Mobile Engagement Android SDK jest nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="772d3-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="772d3-122">Czy firma Microsoft znakowanie na niektóre zdarzenia toohello statycznych dodatkowe informacje, zadań i nawet błędy toodemonstrate jak można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="772d3-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="772d3-123">Te dodatkowe informacje są wysyłane jako JSON ciąg, który w hello `WebAppInterface` pliku, jest analizowana i umieść w systemie Android `Bundle` i jest przekazywany wraz ze zdarzeń, zadań, błędy wysyłania.</span><span class="sxs-lookup"><span data-stu-id="772d3-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="772d3-124">Zadanie Mobile Engagement zostało rozpoczęte o nazwie hello określonej w polu wejściowym hello, uruchom na 10 sekund i zamknąć.</span><span class="sxs-lookup"><span data-stu-id="772d3-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="772d3-125">Mobile Engagement appinfo lub znacznik jest przekazywany z "customer_name" hello statyczny klucz i wartość hello, wprowadzone w danych wejściowych hello jako wartość hello hello tagu.</span><span class="sxs-lookup"><span data-stu-id="772d3-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="772d3-126">Hello wykonywania aplikacji i zobaczą hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="772d3-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="772d3-127">Teraz niektóre nazwy zdarzenie testowe, takich jak powitania po i kliknij przycisk **wysyłania** poniżej.</span><span class="sxs-lookup"><span data-stu-id="772d3-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="772d3-128">Obecnie przejście toohello **Monitor** kartę aplikacji i wyglądu w obszarze **zdarzenia -> Szczegóły**, zobaczysz tego zdarzenia wyświetlane wraz z hello statyczne informacje o aplikacji, które firma Microsoft wysyłania.</span><span class="sxs-lookup"><span data-stu-id="772d3-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
