---
title: aaaGet Started with Azure Mobile Engagement dla platformy Xamarin.Android
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Xamarin.Android."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Rozpoczynanie pracy z usługą Azure Mobile Engagement na potrzeby aplikacji platformy Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji platformy Xamarin.Android.
W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement. W ramach tego samouczka zostanie utworzona pusta aplikacja platformy Xamarin.Android służąca do zbierania danych podstawowych i odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).

> [!NOTE]
> Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów. Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Ten samouczek wymaga następujących hello:

* Program [Xamarin Studio](http://xamarin.com/studio). Można również użyć programu Visual Studio z platformą Xamarin, ale w tym samouczku używany jest program Xamarin Studio. Aby uzyskać instrukcje dotyczące instalowania, zobacz [Instalator i instalacja programu Visual Studio i platformy Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* [Zestaw SDK platformy Xamarin usługi Mobile Engagement](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. 

Utworzymy podstawową aplikację w programie Xamarin Studio toodemonstrate hello integracji.

### <a name="create-a-new-xamarinandroid-project"></a>Tworzenie nowego projektu platformy Xamarin.Android
1. Uruchom **Xamarin Studio** Przejdź zbyt**pliku** -> **nowy** -> **rozwiązania** 
   
    ![][1]
2. Wybierz **aplikacji systemu Android** upewnij się, jest język hello wybrane **C#** i kliknij przycisk **dalej**.
   
    ![][2]
3. Wypełnij hello **Nazwa aplikacji** i hello **identyfikator organizacji**. Upewnij się, że toocheckmark **usług Google Play** , a następnie kliknij przycisk **dalej**. 
   
    ![][3]
4. Aktualizacja hello **Nazwa projektu**, **Nazwa rozwiązania** i **lokalizacji** wymagane, a następnie kliknij przycisk **Utwórz**.
   
    ![][4]

Program Xamarin Studio zostanie utworzona aplikacja hello, w której zostanie zintegrowana usługa Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Połącz zapleczu swojej aplikacji tooMobile zaangażowania
1. Kliknij prawym przyciskiem myszy hello **pakiety** folder w systemie windows rozwiązania hello i wybierz **Dodawanie pakietów...**
   
    ![][5]
2. Wyszukaj hello **Microsoft Azure Mobile Engagement Xamarin SDK** i dodaj go tooyour rozwiązania.  
   
    ![][6]
3. Otwórz **MainActivity.cs** i Dodaj hello następujące instrukcje using:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. W hello `OnCreate` metody, Dodaj powitania po tooinitialize hello połączenia z zapleczem usługi Mobile Engagement. Upewnij się, że tooadd Twojego **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Dodawanie uprawnień i deklaracji usługi
1. Otwórz hello **Manifest.xml** plików w folderze właściwości hello. Wybierz kartę źródło, aby bezpośrednio zaktualizować źródło XML hello.
2. Dodaj te uprawnienia toohello Manifest.xml (można go znaleźć w obszarze hello **właściwości** folder) projektu bezpośrednio przed lub po hello `<application>` tagu:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Dodaj następujące hello między hello `<application>` i `</application>` znaczniki toodeclare hello agenta usługi:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. W wklejonym właśnie kodzie hello, Zastąp `"<Your application name>"` hello etykiety. Jest on wyświetlany w hello **ustawienia** menu, w którym użytkownicy mogą zobaczyć usługi uruchomione na urządzeniu hello. Na przykład możesz dodać hello wyraz "Usługa" w tej etykiecie.

### <a name="send-a-screen-toomobile-engagement"></a>Wysyłanie ekranu tooMobile zaangażowania
W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu. Aby to zrobić — upewnij się, że hello `MainActivity` dziedziczy `EngagementActivity` zamiast `Activity`.

    public class MainActivity : EngagementActivity

Alternatywnie jeśli nie możesz dziedziczyć z klasy `EngagementActivity`, musisz dodać metody `.StartActivity` i `.EndActivity` odpowiednio w `OnResume` i `OnPause`.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract z i UŻYTKOWNIKAMI przy użyciu powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
następujące sekcje Hello konfiguruje tooreceive Twojej aplikacji je.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
