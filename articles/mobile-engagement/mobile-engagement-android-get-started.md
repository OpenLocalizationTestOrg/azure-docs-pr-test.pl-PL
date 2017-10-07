---
title: "aaaGet pracy z systemem Android aplikacje usługi Azure Mobile Engagement"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji systemu Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji systemu Android.
W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement. W tym samouczku zostanie utworzona pusta aplikacja systemu Android służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).

## <a name="prerequisites"></a>Wymagania wstępne
Wykonanie kroków tego samouczka wymaga hello [Android Developer Tools](https://developer.android.com/sdk/index.html), w tym hello Android Studio zintegrowane środowisko programistyczne oraz najnowszej platformy Android hello.

Wymagany jest również hello [zestaw Mobile Engagement Android SDK](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete tego samouczka potrzebne aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. Utworzeniu Podstawowa aplikacja za pomocą integracji hello toodemonstrate Android Studio.

Witaj kompletna dokumentacja integracji znajduje się w hello [zestaw Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Tworzenie projektu systemu Android
1. Uruchom **Android Studio**i wybierz w oknie podręcznym hello **Utwórz nowy projekt Android Studio**.

    ![][1]
2. Podaj nazwę aplikacji i domenę firmy. Zanotuj te informacje, ponieważ będą one potrzebne później. Kliknij przycisk **Dalej**.

    ![][2]
3. Wybierz hello docelowy typ urządzeń i poziom interfejsu API, a następnie kliknij przycisk **dalej**.

   > [!NOTE]
   > Usługa Mobile Engagement wymaga co najmniej interfejsu API na poziomie 10 (Android 2.3.3).
   >
   >

    ![][3]
4. Wybierz **puste działanie** miejsca, czyli hello jedynym ekranem dla tej aplikacji i kliknij pozycję **dalej**.

    ![][4]
5. Na koniec, pozostaw domyślne hello jest, a następnie kliknij przycisk **Zakończ**.

    ![][5]

Android Studio zostanie utworzona aplikacja demonstracyjna hello, w której zostanie zintegrowana usługa Mobile Engagement.

### <a name="include-hello-sdk-library-in-your-project"></a>Uwzględnione hello Biblioteka zestawu SDK w projekcie
1. Pobierz hello [zestaw Mobile Engagement Android SDK](https://aka.ms/vq9mfn).
2. Wyodrębnij hello archiwum pliku tooa folderu na swoim komputerze.
3. Identyfikowanie hello bibliotekę JAR dla bieżącej wersji hello tego zestawu SDK i skopiuj go toohello Schowka.

      ![][6]
4. Przejdź toohello **projektu** sekcji (1) i Wklej hello JAR w folderze libs hello (2).

      ![][7]
5. tooload hello biblioteki projektu hello synchronizacji.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Uzyskuj zapleczu swojej aplikacji tooMobile zaangażowania hello parametry połączenia
1. Skopiuj następujące wiersze kodu do tworzenia działania hello (należy to zrobić tylko w jednym miejscu aplikacji, zwykle hello głównym działaniu) hello. Dla tej aplikacji przykładowej Otwórz zapasowej hello MainActivity w folderze src -> main -> java i dodaj następujące hello:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Rozpoznać odwołań hello, naciskając klawisze Alt + Enter lub dodając następujące instrukcje importu hello:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Przejdź wstecz toohello klasycznego portalu Azure w Twojej aplikacji **informacje o połączeniu** hello strony i skopiuj **ciąg połączenia**.

      ![][9]
4. Wklej go do hello `setConnectionString` parametru, zastępując cały ciąg hello pokazano hello następującego kodu:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Dodawanie uprawnień i deklaracji usługi
1. Dodaj te uprawnienia toohello Manifest.xml projektu bezpośrednio przed lub po hello `<application>` tagu:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare hello Usługa agenta, Dodaj ten kod między hello `<application>` i `</application>` tagów:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. W kodzie hello wklejonych, Zastąp `"<Your application name>"` hello etykiety, który jest wyświetlany w hello **ustawienia** menu, w którym można zobaczyć usługi uruchomione na urządzeniu hello. Na przykład możesz dodać hello wyraz "Usługa" w tej etykiecie.

### <a name="send-a-screen-toomobile-engagement"></a>Wysyłanie ekranu tooMobile zaangażowania
toostart wysyłanie danych i upewnij się, że hello użytkownicy są aktywni, konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).

Przejdź za**MainActivity.java** i Dodaj powitania po tooreplace hello klasa podstawowa **MainActivity** za**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Jeśli nie jest klasą podstawową *działania*, zapoznaj się [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) jak tooinherit z różnych klas.
>
>

Komentarz powitania po wierszu dla tym prostym scenariuszu przykładowym:

    // setSupportActionBar(toolbar);

Jeśli chcesz, aby tookeep hello `ActionBar` w aplikacji, zobacz [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
W czasie kampanii usługa Mobile Engagement umożliwia interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
powitania po sekcji konfiguruje tooreceive Twojej aplikacji je.

### <a name="copy-sdk-resources-in-your-project"></a>Kopiowanie zasobów zestawu SDK w projekcie
1. Przejdź wstecz tooyour SDK pobierania zawartości i skopiuj hello **res** folderu.

    ![][10]
2. Przejdź wstecz tooAndroid Studio, wybierz hello **głównego** katalogu plików projektu, a następnie wklej go tooadd hello zasobów tooyour projektu.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Następne kroki
Przejdź za[zestawu SDK systemu Android](mobile-engagement-android-sdk-overview.md) tooget szczegółowych informacji o hello integracji zestawu SDK.

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
