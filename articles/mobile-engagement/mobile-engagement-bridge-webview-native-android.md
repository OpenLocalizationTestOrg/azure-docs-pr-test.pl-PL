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
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Mostek Android widoku sieci Web z natywnego Mobile Engagement zestawu SDK systemu Android
> [!div class="op_single_selector"]
> * [Mostek systemu android](mobile-engagement-bridge-webview-native-android.md)
> * [Mostek z systemem iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Niektóre aplikacje mobilne są zaprojektowane jako aplikacji hybrydowych, gdy aplikacja hello jest utworzony przy użyciu natywnych systemu Android, ale niektóre lub nawet wszystkich ekranów powitalnych są renderowane w widoku sieci Web dla systemu Android. Może nadal używać zestaw Mobile Engagement Android SDK w ramach tych aplikacji i w tym samouczku opisano sposób toogo o tej czynności. Poniższy kod przykładowy Hello jest oparta na hello dokumentację dla systemu Android [tutaj](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Opisuje, jak można użyć tej metody udokumentowane tooimplement hello takie same dla zestaw Mobile Engagement Android SDK dla często używanych metod tak, aby Webview z aplikacji hybrydowych można także zainicjować zdarzenia tootrack żądania, zadań, błędów, informacje o aplikacji, podczas ich przez przekazanie w potoku naszego zestawu SDK systemu Android. 

1. Przede wszystkim należy tooensure, który ma przeszli naszych [Wprowadzenie — samouczek](mobile-engagement-android-get-started.md) toointegrate hello zestaw Mobile Engagement Android SDK w aplikacji hybrydowych. Gdy to zrobisz, Twoje `OnCreate` metoda będzie wyglądać hello poniżej.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Teraz upewnij się, że aplikacji hybrydowych ma ekran z widoku sieci Web na nim. Witaj kod dla niego będzie podobne następujące toohello gdzie czy ładowanie lokalnego pliku **Sample.html** w hello widoku sieci Web w hello `onCreate` metodę ekranu. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Teraz Utwórz plik Mostek o nazwie **WebAppInterface** który tworzy otokę w niektóre często używane metody zestaw Mobile Engagement Android SDK za pomocą hello `@JavascriptInterface` podejścia opisanego w hello [dokumentację dla systemu Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
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
4. Gdy utworzono hello powyżej Mostek pliku, potrzebujemy tooensure, że jest on skojarzony z naszych widoku sieci Web. Dla tego toohappen należy tooedit Twojego `SetWebview` metodę, tak że wygląda hello:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. W hello powyżej fragment, dzwoniliśmy `addJavascriptInterface` tooassociate naszych Mostek klasy z naszych widoku sieci Web, a także utworzony uchwyt o nazwie **EngagementJs** toocall hello metody z hello Mostek pliku. 
6. Teraz utworzyć następującego pliku o nazwie hello **Sample.html** w projekcie w folderze o nazwie **zasoby** który jest ładowany do hello Webview i którym firma Microsoft będzie wywoływać metod hello z pliku Mostek hello.
   
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
7. Uwaga hello następujące kwestie dotyczące pliku HTML hello powyżej:
   
   * Zawiera zestaw wejściowy pól, w którym można podać toobe danych używane jako nazwy dla zdarzeń, zadania, błąd, AppInfo. Po kliknięciu hello przycisku Dalej tooit toohello Javascript, który ostatecznie wywołuje metody hello z hello Mostek pliku toopass toohello tego wywołania zestaw Mobile Engagement Android SDK jest nawiązane połączenie. 
   * Czy firma Microsoft znakowanie na niektóre zdarzenia toohello statycznych dodatkowe informacje, zadań i nawet błędy toodemonstrate jak można to zrobić. Te dodatkowe informacje są wysyłane jako JSON ciąg, który w hello `WebAppInterface` pliku, jest analizowana i umieść w systemie Android `Bundle` i jest przekazywany wraz ze zdarzeń, zadań, błędy wysyłania. 
   * Zadanie Mobile Engagement zostało rozpoczęte o nazwie hello określonej w polu wejściowym hello, uruchom na 10 sekund i zamknąć. 
   * Mobile Engagement appinfo lub znacznik jest przekazywany z "customer_name" hello statyczny klucz i wartość hello, wprowadzone w danych wejściowych hello jako wartość hello hello tagu. 
8. Hello wykonywania aplikacji i zobaczą hello poniżej. Teraz niektóre nazwy zdarzenie testowe, takich jak powitania po i kliknij przycisk **wysyłania** poniżej. 
   
    ![][1]
9. Obecnie przejście toohello **Monitor** kartę aplikacji i wyglądu w obszarze **zdarzenia -> Szczegóły**, zobaczysz tego zdarzenia wyświetlane wraz z hello statyczne informacje o aplikacji, które firma Microsoft wysyłania. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
