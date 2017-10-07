---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procedury uaktualniania
Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK. Na przykład w przypadku migracji z 1.4.0 too1.6.0 masz toofirst wykonaj hello "z 1.4.0 too1.5.0" procedury, a następnie hello "z 1.5.0 too1.6.0" procedury.

Uaktualnienie z wersji hello masz tooreplace hello `mobile-engagement-VERSION.jar` z hello nową.

## <a name="from-420-too421"></a>Z 4.2.0 too4.2.1
Ten krok faktycznie można zrobić w dowolnej wersji hello zestawu SDK, jest poprawy zabezpieczeń po zintegrowaniu Reach działań.

Teraz należy dodać `exported="false"` tooall Reach działań.

Działania reach powinna wyglądać tak jak to Twojej `AndroidManifest.xml`:

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a>Z 4.0.0 too4.1.0
Hello SDK teraz dojścia nowe uprawnienia modelu z systemem Android M.

Jeśli lokalizacja funkcji lub powiadomienia szerszej przeczytaj [w tej sekcji](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

Ponadto nowy model uprawnień toohello obsługujemy teraz konfigurowania lokalizacji funkcji w czasie wykonywania.
Firma Microsoft są nadal zgodne z parametrami manifestu hello lokalizacji, ale jest już przestarzały. Konfiguracja środowiska uruchomieniowego toouse, Usuń hello poniższych sekcjach przedstawiono z Twojej ``AndroidManifest.xml``:

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

i odczytu [to zaktualizowane procedury](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse Konfiguracja środowiska uruchomieniowego zamiast tego.

## <a name="from-300-too400"></a>Z 3.0.0 too4.0.0
### <a name="native-push"></a>Natywnych powiadomień wypychanych
Natywnych powiadomień wypychanych (GCM/ADM) teraz służy także do w powiadomieniach wewnętrznych aplikacji, musisz skonfigurować poświadczenia natywnych powiadomień wypychanych powitania dla dowolnego typu wypychania kampanii.

Jeśli nie jest już wykonaj [tej procedury](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Integracja reach został zmodyfikowany w ``AndroidManifest.xml``.

Zastąp to:

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

Od

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

Brak prawdopodobnie ekranu ładowania teraz kliknięcie powiadomienia (tekstu/sieci web z zawartością) lub sonda.
Masz tooadd to dla tych toowork kampanii w 4.0.0:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Zasoby
Osadź hello nowe `res/layout/engagement_loading.xml` plik do projektu.

## <a name="from-240-too300"></a>Z 2.4.0 too3.0.0
Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement. W przypadku migracji z wcześniejszej wersji, należy najpierw zapoznać się hello Capptain witryny sieci web toomigrate too2.4.0, a następnie Zastosuj hello procedury.

> [!IMPORTANT]
> Capptain Mobile Engagement są takie same usługi nie hello i hello procedury przedstawionej poniżej tylko highlights jak toomigrate hello aplikacji klienckiej. Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów.
> 
> 

### <a name="jar-file"></a>Plik JAR
Zastąp `capptain.jar` przez `mobile-engagement-VERSION.jar` w Twojej `libs` folderu.

### <a name="resource-files"></a>Pliki zasobów
Każdy plik zasobu podaliśmy (poprzedzony `capptain_`) ma toobe zastąpione przez nowe hello (prefiksem `engagement_`).

Jeśli dostosowano te pliki mają toore — zastosować dostosowanie hello nowych plików, **zmieniono również wszystkie identyfikatory hello w plikach zasobów hello**.

### <a name="application-id"></a>Identyfikator aplikacji
Teraz zaangażowania używa połączenia ciąg tooconfigure hello SDK takie identyfikatory jak identyfikator aplikacji hello.

Masz toouse `EngagementAgent.init` metody w działanie uruchamiania następująco:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Parametry połączenia Hello aplikacji jest wyświetlana w portalu Azure.

Usuń wszystkie wywołania zbyt`CapptainAgent.configure` jako `EngagementAgent.init` zastępuje tę metodę.

Witaj `appId` nie będzie można skonfigurować przy użyciu `AndroidManifest.xml`.

Usuń w tej sekcji z Twojej `AndroidManifest.xml` Jeśli została ona:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>Interfejs API języka Java
Co wywołanie tooany Klasa Java naszego zestawu SDK ma toobe zmieniona; na przykład `CapptainAgent.getInstance(this)` można zmienić nazwy `EngagementAgent.getInstance(this)`, `extends CapptainActivity` można zmienić nazwy `extends EngagementActivity` itp...

Jeśli zostały zintegrowany z domyślnych plików preferencji agenta, hello domyślna nazwa pliku jest teraz `engagement.agent` , klucz hello `engagement:agent`.

Podczas tworzenia sieci web anonsów, hello integratora Javascript jest teraz `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Wiele zmian się stało, hello usługi nie jest już udostępniony i wiele odbiorników nie są już możliwy do eksportu.

Deklaracja usługi Hello jest teraz prostsze; Usuń filtr konwersji hello i wszystkie metadane w nim, a następnie dodaj `exportable=false`.

Oprócz wszystko, co jest zaangażowania toouse zmienioną nazwę.

Teraz wygląda następująco:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Tooenable dzienników testu, należy hello meta-data została przeniesiona toohello aplikacji tagu i została zmieniona:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Zmieniono tylko wszystkie inne metadane, w tym miejscu jest pełna lista hello (oczywiście rename tylko hello te używasz):

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

Śledzenie Google Play i SmartAd została usunięta z pakietu SDK wystarczy tooremove to bez zastępowania:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

działania Reach Hello są obecnie deklarowane następująco:

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

Jeśli masz działań niestandardowych Reach albo należy tylko toochange hello konwersji akcje toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` lub `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Hello emisji odbiorniki zmieniono plus teraz dodać `exported=false`. Poniżej przedstawiono pełną listę hello hello odbiorcy z hello nowej specyfikacji (oczywiście rename tylko hello te używasz):

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

Śledzenie odbiornika zostały usunięte, tak aby było tooremove w tej sekcji:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Należy pamiętać, że deklaracja hello implementacji hello emisji odbiornika **EngagementMessageReceiver** została zmieniona w hello `AndroidManifest.xml`. To jest ponieważ toosend hello interfejsu API i usunięcie dowolnego XMPP komunikaty z dowolnego jednostek XMPP i hello toosend interfejsu API i odbierania wiadomości między urządzeniami zostały usunięte. W związku z tym również masz hello toodelete następujące wywołania zwrotne z Twojej **EngagementMessageReceiver** implementacji:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

i

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

Usuń wszystkie wywołania na **EngagementAgent** dla:

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

i

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Proguard konfiguracji może mieć wpływ rebranding powitalne reguły teraz chce się dowiedzieć, jak:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

