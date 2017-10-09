---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>W jaki sposób Reach usługi Engagement tooIntegrate w systemie Android
> [!IMPORTANT]
> Musisz wykonać procedurę integracji hello opisanego w hello jak tooIntegrate zaangażowania w systemie Android dokumentu przed wykonaniem tego przewodnika.
> 
> 

## <a name="standard-integration"></a>Standardowa integracji

Skopiuj pliki zasobów Reach z hello zestawu SDK w projekcie:

* Skopiuj pliki hello z hello `res/layout` folderu oferowane przez hello zestawu SDK do hello `res/layout` folderu aplikacji.
* Skopiuj pliki hello z hello `res/drawable` folderu oferowane przez hello zestawu SDK do hello `res/drawable` folderu aplikacji.

Edytowanie użytkownika `AndroidManifest.xml` pliku:

* Dodaj następujące sekcji hello (między hello `<application>` i `</application>` tagów):
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* Należy to uprawnienie tooreplay systemu powiadomień, które nie zostały kliknięty przy rozruchu (w przeciwnym razie będą znajdować się na dysku, ale nie będą już wyświetlane, naprawdę masz tooinclude to).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Określanie ikony używany do powiadomień, (zarówno w aplikacji oraz systemowe z nich) przez kopiowanie i edytowania powitania po sekcji (między hello `<application>` i `</application>` tagów):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Ta sekcja ma **obowiązkowe** Jeśli planujesz używanie powiadomień systemowych, tworząc kampanie Zasięgowe. Android uniemożliwia powiadomień systemowych bez ikony wyświetlane. Dlatego w przypadku pominięcia tej sekcji, użytkownicy końcowi nie będą mogli tooreceive je.
> 
> 

* Po utworzeniu kampanii z powiadomień systemowych przy użyciu szerszej należy hello tooadd następujących uprawnień (po hello `</application>` tagu) Jeśli brak:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * W systemie Android M i czy aplikacja korzysta poziom interfejsu API systemu Android 23 lub większą ``WRITE_EXTERNAL_STORAGE`` uprawnienia wymaga zatwierdzenia przez użytkownika. Przeczytaj [w tej sekcji](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Dla powiadomień systemowych, które można również określić hello osiągnięto kampanii, jeśli urządzenie hello pierścienia i/lub należy też. Dla niego toowork, masz toomake się zadeklarowany hello następujące uprawnienia (po hello `</application>` tagu):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Bez tego uprawnienia Android uniemożliwia powiadomienia systemowe z jest pokazywany, gdy zaznaczono pierścień hello lub hello też opcji w Menedżerze osiągnąć kampanii hello.

## <a name="native-push"></a>Natywnych powiadomień wypychanych
Teraz możesz skonfigurować moduł Reach, należy tooconfigure natywnych powiadomień wypychanych toobe tooreceive stanie hello kampanii na urządzeniu hello.

W systemie Android firma Microsoft obsługuje dwie usługi:

* Urządzenia ze sklepu Google Play: Użyj [Google Cloud Messaging] przez następujące hello [jak GCM z Engagement tooIntegrate przewodnik](mobile-engagement-android-gcm-integrate.md) przewodnik.
* Urządzenia firmy Amazon: Użyj [usługi Amazon Device Messaging] przez następujące hello [jak przewodnik tooIntegrate ADM z Engagement](mobile-engagement-android-adm-integrate.md) przewodnik.

Jeśli chcesz, aby tootarget zarówno Amazon, jak i sklepu Google Play urządzenia, jego możliwe toohave cała jego zawartość 1 AndroidManifest.xml/APK do tworzenia aplikacji. Jednak podczas przesyłania tooAmazon, mogą one odrzucić aplikacji, jeśli znajduje się kod usługi GCM.

W takim przypadku należy używać wielu APKs.

**Aplikacja jest teraz gotowy tooreceive i wyświetlanie osiągnąć kampanii!**

## <a name="how-toohandle-data-push"></a>Jak wypychania danych toohandle
### <a name="integration"></a>Integracja
Jeśli chcesz toobe Twojej aplikacji może wypchnięcia tooreceive Reach danych, masz toocreate podklasą klasy `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` i odwoływać w hello `AndroidManifest.xml` pliku (między hello `<application>` i/lub `</application>` tagów):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Następnie można zastąpić hello `onDataPushStringReceived` i `onDataPushBase64Received` wywołań zwrotnych. Oto przykład:

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Kategoria
Witaj kategorii parametr jest opcjonalny, podczas tworzenia kampanii wypychania danych i umożliwia wypychanie danych toofilter. Jest to przydatne, jeśli masz wiele odbiorników emisji obsługi różnych typów wypychania danych, lub jeśli użytkownik chce różnych rodzajów toopush z `Base64` tooidentify danych i chcesz ich typu przed ich analizowania.

### <a name="callbacks-return-parameter"></a>Parametr zwrotnego wywołania zwrotne
Poniżej przedstawiono niektóre wytyczne tooproperly dojście hello parametr zwrotny `onDataPushStringReceived` i `onDataPushBase64Received`:

* Odbiornik emisji powinien zwrócić `null` w hello wywołania zwrotnego, jeśli nie wiadomo, jak push toohandle danych. Należy używać hello toodetermine kategorii, czy odbiornik emisji powinna obsługiwać wypychanie danych hello, lub nie.
* Jeden odbiornik emisji hello powinien zwrócić `true` w hello wywołania zwrotnego, jeśli akceptuje hello wypychanie danych.
* Jeden odbiornik emisji hello powinien zwrócić `false` w hello wywołania zwrotnego, jeśli rozpoznaje hello wypychanie danych, ale odrzuca je z jakiegoś powodu. Na przykład `false` po hello odebrane dane są nieprawidłowe.
* Jeśli emituje jeden odbiornik zwraca `true` podczas drugiego zwraca jedną `false` hello wypychanie danych sam, zachowanie hello jest niezdefiniowana, nigdy nie należy który.

Typ zwracany Hello jest używany tylko dla hello Reach statystyki:

* `Replied`jest zwiększany, jeśli jeden z odbiorców emisji hello albo zwrócony `true` lub `false`.
* `Actioned`zwiększany jest tylko wtedy, gdy jeden hello emisji odbiorniki zwrócił `true`.

## <a name="how-toocustomize-campaigns"></a>Jak toocustomize kampanii
toocustomize kampanie, można zmodyfikować układów hello w hello osiągnąć zestawu SDK.

Należy zachować wszystkie identyfikatory hello używane w układów hello i Zachowaj hello typy widoków hello, korzystających z identyfikatorem, szczególnie w przypadku widoków tekstu i obrazów. Niektóre widoki są używane tylko toohide lub Pokaż obszary, więc ich typ może być zmieniony. Sprawdź, czy kod źródłowy hello zamierzając toochange hello typ widoku w hello podane układów.

### <a name="notifications"></a>Powiadomienia
Istnieją dwa typy powiadomień: powiadomień systemu i w aplikacji, które pliki inny układ.

#### <a name="system-notifications"></a>System powiadomień
należy toouse hello powiadomień systemowych toocustomize **kategorii**. Można przejść za[kategorii](#categories).

#### <a name="in-app-notifications"></a>Powiadomienia w aplikacji
Domyślnie powiadomienia w aplikacji jest widoku, który jest dodawane dynamicznie toohello bieżącego działania użytkownika dzięki toohello Android metody interfejsu `addContentView()`. Jest to nakładce powiadomienia. Nakładki powiadomienia są bardzo szybkiego integracji, ponieważ nie wymagają toomodify można dowolny układ w aplikacji.

wygląd hello toomodify Twojego nakładki powiadomień, wystarczy zmodyfikować plik hello `engagement_notification_area.xml` musi tooyour.

> [!NOTE]
> Plik Hello `engagement_notification_overlay.xml` jest hello jest używany toocreate w nakładce powiadomienia hello plik `engagement_notification_area.xml`. Można również dostosować go toosuit potrzeb (np. dla obszaru powiadomień hello w nakładce hello rozmieszczania).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Obejmują układu powiadomienia w ramach działania układu
Nakładki są bardzo szybkiego integracji, ale można niewygodne lub mieć skutki uboczne w szczególnych przypadkach. można dostosować system nakładki Hello na poziomie działania, dzięki czemu można łatwo tooprevent efekty uboczne specjalnych działań.

Można określić tooinclude naszych układu powiadomień w Twoje istniejące toohello Dziękujemy układu Android **obejmują** instrukcji. Witaj poniżej przedstawiono przykład zmodyfikowanych `ListActivity` układu zawierający tylko `ListView`.

**Przed integracji usługi Engagement:**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Po integracji usługi Engagement:**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

W tym przykładzie dodano kontenera nadrzędnego ponieważ układ oryginalny hello stanowiły hello najwyższego poziomu elementu widoku listy. Dodaliśmy również `android:layout_weight="1"` toobe tooadd stanie skonfigurowano poniżej widoku listy widok `android:layout_height="fill_parent"`.

zestaw SDK Reach usługi Engagement Hello automatycznie wykrywa taki układ powiadomień hello jest dołączony do tego działania, a nie dodają nakładki dla tego działania.

> [!TIP]
> Jeśli używasz ListActivity w aplikacji widoczne nakładki Reach uniemożliwi dające dodatnią reakcję tooclicked elementów w widoku listy hello już. Jest to znany problem. toowork tego problemu zaleca się możesz tooembed hello powiadomień układ własne działania układ listy podobnie jak w poprzednim przykładzie hello.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Wyłączanie aplikacji powiadomienia na działanie
Jeśli nie chcesz hello toobe nakładki dodać działanie tooyour i układu powiadomień hello nie zawiera własny układ, można wyłączyć hello nakładki dla tego działania w hello `AndroidManifest.xml` przez dodanie `meta-data` sekcji, takich jak w następujących hello przykład:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a>Kategorie
Po zmodyfikowaniu hello podane układów możesz zmodyfikować wygląd hello wszystkich powiadomień. Kategorie dopuszczać toodefine możesz przez różne docelowe szuka powiadomienia (prawdopodobnie zachowania). Po utworzeniu kampanii Reach można określić kategorię. Należy pamiętać, że kategorie pozwalają również dostosować anonsów i sond, opisane w dalszej części tego dokumentu.

tooregister kategorii Obsługa powiadomienia, należy tooadd wywołania po zainicjowaniu aplikacji hello.

> [!IMPORTANT]
> Przeczytaj hello ostrzeżenie dotyczące atrybutu android: proces hello \<android-sdk zaangażowania — proces\> w hello jak tooIntegrate zaangażowania na temat Android przed kontynuowaniem.
> 
> 

Witaj poniższym przykładzie założono potwierdzonych poprzedniego ostrzeżenie hello i użyj klasy `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

Witaj `MyNotifier` obiektu jest implementacją hello hello powiadomień kategorii obsługi. Jest implementacja klasy hello `EngagementNotifier` interfejsu lub klasy podrzędnej implementacji domyślnej hello: `EngagementDefaultNotifier`.

Należy pamiętać, że hello tego samego zgłaszający może obsługiwać kilka kategorii, zarejestruj je następująco:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

tooreplace hello domyślną kategorii implementację można zarejestrować implementacji takich jak w hello poniższy przykład:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

Hello bieżącej kategorii używany w procedurze obsługi jest przekazywana jako parametr w większości metod można zastąpić w `EngagementDefaultNotifier`.

Jest przekazywany jako `String` parametru lub pośrednio w `EngagementReachContent` obiektu, który ma `getCategory()` metody.

Można zmienić większość procesu tworzenia powiadomień hello na ponowne definiowanie metody `EngagementDefaultNotifier`dla bardziej zaawansowane dostosowania uznać wolnego tootake poszukaj w dokumentacji technicznej hello i na powitania kodu źródłowego.

##### <a name="in-app-notifications"></a>Powiadomienia w aplikacji
Jeśli chcesz alternatywne układy toouse dla określonej kategorii, można zaimplementować to jak hello poniższy przykład:

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**Przykład `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Jak widać, hello nakładki widoku identyfikator różni się od standardowego hello jeden. Należy pamiętać, że każdego układu dla nakładki używany unikatowy identyfikator.

**Przykład `my_notification_area.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

Jak widać, identyfikator widoku obszaru powiadomień hello jest inny niż standardowe hello jeden. Należy pamiętać, że każdy układ używa unikatowego identyfikatora obszarów powiadomień.

Ten prosty przykład kategorii sprawia, że powiadomienia aplikacji (lub w aplikacji) wyświetlany u góry hello hello ekranu. Nie został zmieniony hello identyfikatory standardowe używane w obszarze powiadomień hello samej siebie.

Jeśli chcesz, aby toochange, że masz tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` metody. Zalecane jest toolook dokumentacji technicznej hello i kod źródłowy hello `EngagementNotifier` i `EngagementDefaultNotifier` Jeśli chcesz to poziomu zaawansowanego dostosowania.

##### <a name="system-notifications"></a>System powiadomień
Rozszerzając `EngagementDefaultNotifier`, można zastąpić `onNotificationPrepared` tooalter hello powiadomienia, który został przygotowany przez hello domyślną implementację.

Na przykład:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

W tym przykładzie powoduje, że powiadomienie systemowe dla zawartości będzie wyświetlany jako zdarzenie uruchomione, gdy kategorii "stałe" hello jest używany.

Jeśli chcesz, aby toobuild hello `Notification` obiekt od początku, można powrócić `false` toohello — metoda i wywołanie `notify` samodzielnie na powitania `NotificationManager`. W takim przypadku należy pamiętać o jest `contentIntent`, `deleteIntent` i hello identyfikator powiadomienia, używany przez `EngagementReachReceiver`.

Oto przykład poprawnego takie implementacji:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>Anonsów zawierających tylko powiadomienia
Hello zarządzania powitania kliknij powiadomienie tylko anonsu można dostosowywać przez zastąpienie `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hello toomodify przygotowane `Intent`. Za pomocą tej metody można łatwo tootune hello flagi.

Na przykład tooadd hello `SINGLE_TOP` flagi:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Dla starszych zaangażowania użytkowników należy pamiętać, że powiadomień systemowych bez akcji adresu URL teraz uruchamia aplikacji hello jeśli było w tle, więc ta metoda może być wywołany z anonsu bez adres URL akcji. Należy rozważyć który w przypadku zamiaru hello dostosowywania.

Można też wdrożyć `EngagementNotifier.executeNotifAnnouncementAction` od początku.

##### <a name="notification-life-cycle"></a>Cykl życia powiadomień
Korzystając z kategorii domyślnej hello, w przypadku niektórych metod cyklu życia są nazywane na powitania `EngagementReachInteractiveContent` obiekt tooreport statystyk i aktualizacji hello kampanii stanu:

* Gdy hello powiadomienia są wyświetlane w aplikacji lub umieść na pasku stanu hello, hello `displayNotification` metoda jest wywoływana (która statystyki) przez `EngagementReachAgent` Jeśli `handleNotification` zwraca `true`.
* Jeśli powiadomienia hello jest odrzucane, hello `exitNotification` metoda jest wywoływana, statystyka jest zgłaszany i dalej kampanii teraz mogą być przetwarzane.
* Po kliknięciu powiadomienia hello `actionNotification` jest nazywane, statystyka jest zgłaszany i celem hello skojarzone jest uruchamiana.

Jeśli implementacji `EngagementNotifier` pomija hello domyślne zachowanie, należy toocall tych metod cyklu życia samodzielnie. Hello następujące przykłady przedstawiają niektórych przypadkach, gdy pomijana jest hello domyślne zachowanie:

* Nie można rozszerzyć `EngagementDefaultNotifier`, np. zaimplementowano obsługi kategorii od początku.
* Dla powiadomień systemowych overrode hello `onNotificationPrepared` i możesz zmodyfikować `contentIntent` lub `deleteIntent` w hello `Notification` obiektu.
* Aby powiadomienia w aplikacji, overrode `prepareInAppArea`, toomap się, że co najmniej `actionNotification` tooone formantów U.I.

> [!NOTE]
> Jeśli `handleNotification` zwraca wyjątek, hello zawartości zostanie usunięty i `dropContent` jest wywoływana. Jest to raportowane w statystykach i dalej kampanii teraz mogą być przetwarzane.
> 
> 

### <a name="announcements-and-polls"></a>Anonsów i sond
#### <a name="layouts"></a>Układy
Można zmodyfikować hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` i `engagement_poll.xml` pliki toocustomize tekst anonsów, web anonsów i sond.

Te pliki mają dwóch typowych układów hello tytuł i hello przycisk obszaru. Układ Hello tytułu hello jest `engagement_content_title.xml` i używa hello gromadzący obiektów drawable plików w tle hello. Witaj układ przycisków akcji i wyjścia hello jest `engagement_button_bar.xml` i używa hello gromadzący obiektów drawable plików w tle hello.

W sondowania hello układ pytanie i ich opcji są dynamicznie zwiększony, przy użyciu hello kilka razy `engagement_question.xml` pliku układu dla hello pytania i hello `engagement_choice.xml` hello wyborów w pliku.

#### <a name="categories"></a>Kategorie
##### <a name="alternate-layouts"></a>Układy alternatywnej
Jak powiadomienia Kategoria kampanii hello mogą być używane toohave alternatywne układy anonsów i sond.

Na przykład toocreate kategorii ogłoszenie tekstu, można rozszerzyć `EngagementTextAnnouncementActivity` i odwołaj hello `AndroidManifest.xml` pliku:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Należy zwrócić uwagę tej kategorii hello w hello zamiar użyć filtru różnica hello toomake z hello domyślne działanie anonsu.

Hello osiągnąć SDK używa hello konwersji system tooresolve hello odpowiednim działaniu dla określonej kategorii i jego powraca na powitania domyślnej kategorii Jeśli rozwiązanie hello nie powiodło się.

Następnie tooimplement `MyCustomTextAnnouncementActivity`, po prostu toochange hello układu (, ale zachować hello tego samego widoku identyfikatorów), wystarczy toodefine hello klasy, jak w hello poniższy przykład:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

tooreplace hello domyślnej kategorii anonsów tekstu, po prostu zastąpić `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` przy implementacji.

W podobny sposób można dostosować Web anonsów i sond.

W przypadku anonsów zawierających sieci web można rozszerzyć `EngagementWebAnnouncementActivity` ani deklarować Twoich działaniach w hello `AndroidManifest.xml` w hello poniższy przykład, takich jak:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Ankiety można rozszerzyć `EngagementPollActivity` ani deklarować użytkownika w hello `AndroidManifest.xml` w hello poniższy przykład, takich jak:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Implementacja od podstaw
Można zaimplementować kategorie działań anonsu (i sondowania) bez rozszerzenie jednej hello `Engagement*Activity` klasy podał hello osiągnąć zestawu SDK. Jest to przydatne na przykład jeśli chcesz toodefine układu, które nie są używane hello sam widoków jako hello standardowych układów.

Podobnie jak dostosowywania powiadomień zaawansowane, zalecane jest toolook na kod źródłowy hello hello standardowej implementacji.

Poniżej przedstawiono niektóre czynności tookeep pamiętać: Reach uruchomi hello działania z określonym profilem (odpowiedniego filtru konwersji toohello) oraz dodatkowy parametr, który jest hello identyfikator zawartości.

tooretrieve hello zawartości obiektu, który zawiera pola hello określony podczas tworzenia hello kampanii w witrynie sieci web hello możesz to zrobić:

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

Statystyki, zgłoś hello zawartość jest wyświetlana w hello `onResume` zdarzeń:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Następnie, nie zapomnij albo toocall `actionContent(this)` lub `exitContent(this)` hello zawartości obiektu przed hello działanie przechodzi w tle.

Nie można wywołać albo `actionContent` lub `exitContent`, statystyki nie zostaną wysłane (tzn. nie analizy kampanii hello) i więcej wszystkim hello dalej kampanii nie zostaną powiadomieni do ponownego uruchomienia procesu aplikacji hello.

Orientacja lub innych zmian konfiguracji można upewnij toodetermine trudnych kodu hello czy hello działanie przechodzi w tle, lub nie, hello sprawia, że standardowej implementacji się, że zawartość hello jest raportowane jako zakończony, jeśli odejdzie użytkownik, hello działania hello, (albo przez Naciśnięcie przycisku `HOME` lub `BACK`), ale nie w przypadku zmiany orientacji hello.

Oto hello interesujące część implementacji hello:

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

Jak widać, jeśli wywołujesz `actionContent(this)` , a następnie Zakończono działanie hello `exitContent(this)` można bezpiecznie wywołać bez żadnego efektu.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[usługi Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
