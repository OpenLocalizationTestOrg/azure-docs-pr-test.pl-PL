---
title: "aaaNotification koncentratory fundamentalne wiadomości Samouczek — systemu Android"
description: "Dowiedz się, jak toosend usługi centra powiadomień Azure Service Bus toouse fundamentalne urządzeń tooAndroid powiadomień wiadomości."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Użyj usługi Notification Hubs toosend fundamentalne wiadomości
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób toouse usługi Azure Notification Hubs toobroadcast najważniejszych wiadomości powiadomienia tooan aplikacji systemu Android. Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii. Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.

Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello. Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello. Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej. Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Wymagania wstępne
W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started]. Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Dodaj aplikację toohello wybór kategorii
pierwszym krokiem Hello jest hello tooadd interfejsu użytkownika elementy tooyour istniejącego głównego działania umożliwiające hello użytkownika tooselect kategorii tooregister. Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello. Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.

1. Otwórz plik res/layout/activity_main.xml i Zastąp zawartość hello hello następujący:
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. Otwórz plik res/values/strings.xml i Dodaj hello następujące wiersze:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    Układu graficznego main_activity.xml powinna wyglądać następująco:
   
    ![][A1]
3. Teraz Utwórz klasę **powiadomienia** w hello same pakiety z **MainActivity** klasy.
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    Ta klasa korzysta z hello Magazyn lokalny toostore hello kategorii wiadomości, czy to urządzenie ma tooreceive. Zawiera również metody tooregister dla tych kategorii.
4. W Twojej **MainActivity** klasy Usuń prywatne pól dla **NotificationHub** i **GoogleCloudMessaging**, i Dodaj pole do **powiadomienia**:
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. Następnie w hello **onCreate** metody, Usuń inicjowanie hello hello **Centrum** pola i hello **registerWithNotificationHubs** — metoda. Następnie dodaj następujące wiersze, które inicjuje wystąpienie klasy hello hello **powiadomienia** klasy. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`i `HubListenConnectionString` już powinien być ustawiony z hello `<hub name>` i `<connection string with listen access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.

    > [AZURE.NOTE] Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta. Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia. klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.


1. Następnie należy dodać importuje powitania po i `subscribe` hello toohandle metody subskrypcji przycisk kliknij zdarzenie:
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    Ta metoda tworzy listę kategorii i używa hello **powiadomienia** klasy toostore hello listy w magazynie lokalnym hello i zarejestruj hello odpowiednie tagi w Centrum powiadomień. Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.

Aplikacji jest teraz możliwe toostore zestaw kategorii w lokalnej pamięci masowej na powitania urządzenia i rejestruje hello Centrum powiadomień, gdy wybór kategorii hello hello zmiany wprowadzane przez użytkownika.

## <a name="register-for-notifications"></a>Rejestrowanie się w celu powiadomienia
Następujące kroki, zarejestruj się w Centrum powiadomień hello podczas uruchamiania przy użyciu hello kategorie, które były przechowywane w magazynie lokalnym.

> [!NOTE]
> Ponieważ registrationId hello przypisane przez Google Cloud Messaging (GCM) można zmienić w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów. W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello. Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.
> 
> 

1. Dodaj następującego kodu na końcu hello hello hello **onCreate** metoda hello **MainActivity** klasy:
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Dzięki temu że każdym uruchomieniu aplikacji hello pobiera kategorie hello z magazynu lokalnego i żąda rejestracja dla tych kategorii. 
2. Następnie zaktualizuj hello `onStart()` metody hello `MainActivity` klas w następujący sposób:
   
    @Overridechronione {void onStart()
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    }
   
    Spowoduje to zaktualizowanie hello głównego działania na podstawie stanu hello zapisane wcześniej kategorii.

Aplikacja Hello jest teraz ukończona i może przechowywać zestawu kategorii hello urządzenia magazynu lokalnego używane tooregister hello Centrum powiadomień przy każdym zmiany użytkowników hello hello wybór kategorii. Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać kategorii powiadomienia toothis aplikacji.

## <a name="sending-tagged-notifications"></a>Wysyłanie powiadomień oznakowany
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Uruchamianie aplikacji hello i generować powiadomienia
1. W programie Android Studio tworzenie aplikacji hello, a następnie uruchom go na urządzeniu lub emulatorze.
   
    Należy pamiętać, że przełącza, aplikacja hello, które interfejs użytkownika zawiera zestaw, który umożliwia wybranie hello toosubscribe kategorii do.
2. Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.
   
    Aplikacja Hello konwertuje kategorii hello wybrane tagi i żąda nowej rejestracji urządzenia hello wybrane tagów z Centrum powiadomień hello. Witaj zarejestrowanych kategorie są zwracane i wyświetlane w wyskakujące powiadomienie.
3. Wyślij nowe powiadomienie, uruchamiając hello aplikacji konsoli .NET.  Alternatywnie możesz wysłać oznakowanych szablonu powiadomienia za pomocą karty debugowanie hello Centrum powiadomień w hello [klasycznego portalu Azure].
   
    Powiadomienia o kategoriach hello wybrane są wyświetlane jako wyskakujące powiadomienia.

## <a name="next-steps"></a>Następne kroki
W tym samouczku opisano sposób toobroadcast krytyczne według kategorii wiadomości. Należy rozważyć wykonanie jednej hello następujące samouczki dotyczące innych zaawansowanych scenariuszy centra powiadomień:

* [Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]
  
    Dowiedz się, jak fundamentalne wysyłania tooenable aplikacji wiadomości powitania tooexpand zlokalizowane powiadomienia.

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[klasycznego portalu Azure]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
