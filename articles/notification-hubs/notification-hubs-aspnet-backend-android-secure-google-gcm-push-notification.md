---
title: "aaaSending Secure powiadomień wypychanych przy użyciu usługi Azure Notification Hubs"
description: "Dowiedz się, jak bezpieczne toosend push aplikacji systemu Android tooan powiadomienia z platformy Azure. Przykłady kodu napisane w języku Java i C#."
documentationcenter: android
keywords: "Wypychanie powiadomień, powiadomienia wypychane push wiadomości, powiadomień wypychanych systemu android"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Wysyłanie powiadomień wypychanych bezpiecznego przy użyciu usługi Azure Notification Hubs
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Omówienie
> [!IMPORTANT]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Obsługa powiadomień wypychanych w Microsoft Azure umożliwia tooaccess infrastruktury wiadomości wypychanych łatwy w użyciu, wieloplatformową skalowalnych w poziomie, który jest znacznie ułatwione hello stosowania powiadomienia wypychane dla aplikacji zarówno konsumenckie i korporacyjne dla platformy urządzeń przenośnych.

Czasami ze względu na ograniczenia tooregulatory lub zabezpieczeń, aplikacja może być tooinclude coś w hello powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowe hello. W tym samouczku opisano, jak tooachieve hello tego samego środowiska poprzez wysłanie poufnych informacji za pośrednictwem uwierzytelnionego bezpiecznego połączenia między urządzenia Android powitania klienta i zaplecza aplikacji hello.

Na wysokim poziomie przepływu hello jest następujący:

1. Witaj zaplecze aplikacji:
   * Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.
   * Wysyła identyfikator hello tego powiadomienia toohello urządzenia z systemem Android (nie informacji o są wysyłane).
2. Aplikacja Hello na urządzeniu hello podczas odbierania powiadomień hello:
   * urządzenia z systemem Android Hello kontaktuje się hello zaplecza żądania hello bezpiecznego ładunku.
   * Aplikacja Hello można wyświetlić ładunku hello jako powiadomienie na urządzeniu hello.

Jest ważne toonote, że w hello poprzedzających przepływu (i w tym samouczku) przyjęto założenie, urządzenia hello po zalogowaniu użytkownika hello przechowuje token uwierzytelniania w magazynie lokalnym. Gwarantuje to całkowicie sprawnie, jak urządzenia hello mogą pobierać ładunku bezpiecznego hello powiadomienia za pomocą tego tokenu. Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu hello lub tokeny te mogą wygasnąć, hello aplikacji urządzenia, po otrzymaniu powiadomienia wypychane hello powinien być wyświetlany ogólny powiadomienie aplikacji hello toolaunch użytkownika hello monitowania. Aplikacja Hello następnie uwierzytelnia użytkownika hello i zawiera ładunek powiadomienia hello.

Ten samouczek pokazuje, jak toosend bezpieczne powiadomień wypychanych. Opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) samouczku, dlatego należy wykonać kroki hello w tym samouczku najpierw Jeśli jeszcze.

> [!NOTE]
> Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Modyfikowanie hello projekt systemu Android
Teraz, aby modyfikować tylko aplikacji hello w toosend zaplecza *identyfikator* powiadomienia wypychane, masz toochange Twojego toohandle aplikacji systemu Android, że powiadomienia i wywołania zwrotne Twojej hello tooretrieve zaplecza secure toobe komunikat wyświetlany.
tooachieve ten cel ma toomake się upewnić, że aplikacji systemu Android wie jak tooauthenticate się z poziomu zaplecza, gdy odbiera powiadomienia wypychane hello.

Firma Microsoft będzie teraz zmodyfikować hello *logowania* przepływu w kolejności toosave hello wartości nagłówka uwierzytelniania w hello udostępnionych preferencji aplikacji. Mechanizmy analogiczne mogą być używane toostore żadnych token uwierzytelniania (np. tokenów OAuth), który aplikacja hello ma toouse bez konieczności wprowadzania poświadczeń użytkownika.

1. W projekcie aplikacji systemu Android, Dodaj powitania po stałe u góry hello hello **MainActivity** klasy:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Nadal w hello **MainActivity** klasy, aktualizacja hello `getAuthorizationHeader()` hello toocontain metody następującego kodu:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Dodaj następujące hello `import` instrukcji u góry hello hello **MainActivity** pliku:
   
        import android.content.SharedPreferences;

Teraz zostanie zmieniona hello obsługi, która jest wywoływana po otrzymaniu powiadomienia hello.

1. W hello **MyHandler** klasy zmienić hello `OnReceive()` toocontain metody:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Następnie dodaj hello `retrieveNotification()` metoda zastępuje symbol zastępczy hello `{back-end endpoint}` z punktem końcowym zaplecza hello uzyskane podczas wdrażania sieci wewnętrznej:
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

Ta metoda wywołuje zawartości przy użyciu poświadczeń hello przechowywanych w hello udostępnionych preferencji i wyświetla je jako normalne powiadomienie powiadomienia hello tooretrieve zaplecza aplikacji. powiadomienie Hello wygląda toohello użytkownika aplikacji, dokładnie tak samo jak inne powiadomień wypychanych.

Należy pamiętać, że preferowane toohandle hello przypadków brakujących właściwości nagłówka uwierzytelniania lub odrzucenia przez hello zaplecza. Obsługa określonego Hello powyższych przypadkach zależą od przede wszystkim użytkowników docelowych. Jedną z opcji jest toodisplay powiadomienie z wierszem ogólnego hello użytkownika tooauthenticate tooretrieve hello rzeczywiste powiadomienia o.

## <a name="run-hello-application"></a>Uruchom hello aplikacji
toorun hello aplikacji, hello następujące:

1. Upewnij się, że **AppBackend** jest wdrożona na platformie Azure. Jeśli używasz programu Visual Studio, uruchom hello **AppBackend** aplikacji interfejsu API sieci Web. Zostanie wyświetlona strona sieci web ASP.NET.
2. W środowisku Eclipse uruchamianie aplikacji hello na fizyczne urządzenie lub hello emulator systemu Android.
3. W aplikacji systemu Android hello interfejsu użytkownika wprowadź nazwę użytkownika i hasło. Mogą to być dowolny ciąg, ale muszą one być hello tę samą wartość.
4. W aplikacji systemu Android hello interfejsu użytkownika, kliknij przycisk **Zaloguj**. Następnie kliknij przycisk **wysyłania wypychania**.

