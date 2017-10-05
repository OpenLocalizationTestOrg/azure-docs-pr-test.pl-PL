---
title: Mostek Android widoku sieci Web z natywnego Mobile Engagement zestawu SDK systemu Android
description: "Opisuje sposób tworzenia mostka między systemem obsługi języka Javascript i natywny zestaw Mobile Engagement Android SDK widoku sieci Web"
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="bd596-103">Mostek Android widoku sieci Web z natywnego Mobile Engagement zestawu SDK systemu Android</span><span class="sxs-lookup"><span data-stu-id="bd596-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd596-104">Mostek systemu android</span><span class="sxs-lookup"><span data-stu-id="bd596-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="bd596-105">Mostek z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="bd596-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="bd596-106">Niektóre aplikacje mobilne są zaprojektowane jako aplikacji hybrydowych, gdy aplikacja jest utworzony przy użyciu natywnych systemu Android, ale niektóre lub nawet wszystkich ekranów są renderowane w widoku sieci Web dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="bd596-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="bd596-107">Może nadal używać zestaw Mobile Engagement Android SDK w ramach tych aplikacji i w tym samouczku opisano sposób Przejdź o tej czynności.</span><span class="sxs-lookup"><span data-stu-id="bd596-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="bd596-108">Poniższy przykładowy kod jest oparta na dokumentację dla systemu Android [tutaj](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="bd596-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="bd596-109">Opisuje, jak takie podejście udokumentowane może posłużyć do wykonania takie same dla zestaw Mobile Engagement Android SDK dla często używanych metod tak, aby Webview z aplikacji hybrydowych można także zainicjować żądań śledzenia zdarzeń, zadań, błędów, informacje o aplikacji podczas ich przez przekazanie w potoku naszych Zestaw SDK systemu android.</span><span class="sxs-lookup"><span data-stu-id="bd596-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="bd596-110">Po pierwsze, należy się upewnić, że przeszły naszych [Wprowadzenie — samouczek](mobile-engagement-android-get-started.md) zintegrować zestaw Mobile Engagement Android SDK w aplikacji hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="bd596-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="bd596-111">Gdy to zrobisz, Twoje `OnCreate` metoda będzie wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="bd596-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="bd596-112">Teraz upewnij się, że aplikacji hybrydowych ma ekran z widoku sieci Web na nim.</span><span class="sxs-lookup"><span data-stu-id="bd596-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="bd596-113">Kod dla niego będzie podobny do następującego gdzie czy ładowanie lokalnego pliku **Sample.html** w widoku sieci Web w `onCreate` metodę ekranu.</span><span class="sxs-lookup"><span data-stu-id="bd596-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="bd596-114">Teraz Utwórz plik Mostek o nazwie **WebAppInterface** który tworzy otokę w niektóre często używane przy użyciu metody zestaw Mobile Engagement Android SDK `@JavascriptInterface` podejścia opisanego w [Android dokumentacji](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="bd596-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="bd596-115">Gdy utworzono plik Mostek powyżej, musimy upewnij się, że jest on skojarzony z naszych widoku sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bd596-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="bd596-116">W tym celu należy edytować Twojej `SetWebview` metody, dzięki czemu wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="bd596-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="bd596-117">We fragmencie powyżej dzwoniliśmy `addJavascriptInterface` do skojarzenia klasy Nasze mostek z naszych widoku sieci Web, a także utworzony uchwyt o nazwie **EngagementJs** do wywołania metody z pliku mostek.</span><span class="sxs-lookup"><span data-stu-id="bd596-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="bd596-118">Teraz utworzyć następującego pliku o nazwie **Sample.html** w projekcie w folderze o nazwie **zasoby** który jest ładowany do widoku sieci Web i gdzie możemy wywoływać metody z pliku mostek.</span><span class="sxs-lookup"><span data-stu-id="bd596-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="bd596-119">Należy uwzględnić następujące kwestie dotyczące pliku w formacie HTML powyżej:</span><span class="sxs-lookup"><span data-stu-id="bd596-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="bd596-120">Zawiera zestaw wejściowy pól, w którym można podać dane mają być używane jako nazwy dla zdarzeń, zadania, błąd, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="bd596-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="bd596-121">Po kliknięciu przycisku Dalej, aby go połączenie jest nawiązywane w przypadku Javascript, który ostatecznie wywołuje metody z pliku mostek do przekazania to wywołanie zestaw Mobile Engagement Android SDK.</span><span class="sxs-lookup"><span data-stu-id="bd596-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="bd596-122">Firma Microsoft są znakowanie na niektórych statycznych dodatkowe informacje do zdarzeń, zadania i nawet błędów, aby zademonstrować, jak można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="bd596-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="bd596-123">Te dodatkowe informacje są wysyłane jako JSON ciąg, który w `WebAppInterface` pliku, jest analizowana i umieść w systemie Android `Bundle` i jest przekazywany wraz ze zdarzeń, zadań, błędy wysyłania.</span><span class="sxs-lookup"><span data-stu-id="bd596-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="bd596-124">Zadanie Mobile Engagement zostało rozpoczęte o nazwie określonej w polu wejściowym, uruchom na 10 sekund i zamknąć.</span><span class="sxs-lookup"><span data-stu-id="bd596-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="bd596-125">Usługa Mobile Engagement appinfo lub znacznik jest przekazywany z "customer_name" jako statyczny klucz i wartość wprowadzona w danych wejściowych jako wartość tagu.</span><span class="sxs-lookup"><span data-stu-id="bd596-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="bd596-126">Uruchom aplikację i pojawi się poniżej.</span><span class="sxs-lookup"><span data-stu-id="bd596-126">Run the app and you will see the following.</span></span> <span data-ttu-id="bd596-127">Teraz niektóre nazwy zdarzenie testowe, podobnie jak poniżej i kliknij przycisk **wysyłania** poniżej.</span><span class="sxs-lookup"><span data-stu-id="bd596-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="bd596-128">Teraz, jeśli przejdziesz do **Monitor** kartę aplikacji i wyglądu w obszarze **zdarzenia -> Szczegóły**, zobaczysz tego zdarzenia wyświetlane wraz ze statycznego aplikacji — informacje, które firma Microsoft wysyłania.</span><span class="sxs-lookup"><span data-stu-id="bd596-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
