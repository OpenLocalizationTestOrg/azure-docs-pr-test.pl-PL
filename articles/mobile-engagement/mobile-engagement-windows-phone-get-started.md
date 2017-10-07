---
title: "aaaGet pracy z aplikacjami usługi Azure Mobile Engagement dla Windows Phone Silverlight"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Wprowadzenie do usługi Azure Mobile Engagement na potrzeby aplikacji platformy Silverlight systemu Windows Phone
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse Twoje użycie aplikacji i wysyłania powiadomień użytkowników toosegmented aplikacji Windows Phone Silverlight push.
W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement. W ramach tego samouczka utworzona zostanie pusta aplikacja platformy Silverlight systemu Windows Phone, za pomocą której będą zbierane podstawowe dane i odbierane powiadomienia wypychane przy użyciu Usługi powiadomień systemu Windows.

> [!NOTE]
> Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów. Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

> [!NOTE]
> Projekty systemu Windows Phone 8.1 i wcześniejszych nie są obsługiwane w programie Visual Studio 2017 r.  Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Jeśli ma być przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), zapoznaj się z pomocą techniczną firmy toohello [samouczek aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Ten samouczek wymaga następujących hello:

* Program Visual Studio 2013
* Pakiet NuGet [MicrosoftAzure.MobileEngagement]

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Windows Phone
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. Witaj kompletna dokumentacja integracji znajduje się w hello [integracji zestawu SDK usługi Mobile Engagement Windows Phone](mobile-engagement-windows-phone-sdk-overview.md)

Utworzymy podstawową aplikację z integracją hello toodemonstrate programu Visual Studio.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Tworzenie nowego projektu platformy Silverlight systemu Windows Phone
Hello następujących krokach założono użycie hello programu Visual Studio 2015 chociaż hello kroki są podobne we wcześniejszych wersjach programu Visual Studio. 

1. Uruchom program Visual Studio w hello **Home** ekranu wybierz **nowy projekt**.
2. W oknie podręcznym hello wybierz **systemu Windows 8** -> **Windows Phone** -> **pusta aplikacja (Windows Phone Silverlight)**. Wypełnij aplikacji hello **nazwa** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.
   
    ![][1]
3. Można wybrać tootarget albo **Windows Phone 8.0** lub **Windows Phone 8.1**.

Teraz utworzono nową aplikację systemu Windows Phone Silverlight, w którym zostanie zintegrowany zestaw SDK usługi Azure Mobile Engagement hello.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
1. Zainstaluj hello [MicrosoftAzure.MobileEngagement] pakietu nuget w projekcie.
2. Otwórz `WMAppManifest.xml` (znajduje się w folderze właściwości hello) i upewnij się, że zadeklarowany następujący hello (dodać je, gdy nie są one) w hello `<Capabilities />` tagu:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Teraz Wklej parametry połączenia hello, które wcześniej zostały skopiowane dla aplikacji usługi Mobile Engagement i wklej go w hello `Resources\EngagementConfiguration.xml` plików między hello `<connectionString>` i `</connectionString>` tagów:
   
    ![][3]
4. W hello `App.xaml.cs` pliku:
   
    a. Dodaj hello `using` instrukcji:
   
            using Microsoft.Azure.Engagement;
   
    b. Inicjowanie hello zestawu SDK w hello `Application_Launching` metody:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Wstaw następujące hello w hello `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym
W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).

1. W hello MainPage.xaml.cs Dodaj hello `using` instrukcji:
   
        using Microsoft.Azure.Engagement;
2. Zastąp klasę podstawową hello **MainPage**, czyli przed **PhoneApplicationPage**, z **EngagementPage**.
   
        class MainPage : EngagementPage 
3. W pliku `MainPage.xml`:
   
    a. Dodaj deklaracje przestrzeni nazw tooyour:
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Zastąp `phone:PhoneApplicationPage` w nazwie tagu XML hello z `engagement:EngagementPage`.

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract i użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście hello kampanii. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi MPNS
Dodaj nowe możliwości tooyour `WMAppManifest.xml` pliku:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inicjowanie hello OSIĄGNĄĆ zestawu SDK
1. W `App.xaml.cs`, wywołaj `EngagementReach.Instance.Init();` w hello **Application_Launching** bezpośrednio po zainicjowaniu agenta hello:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. W `App.xaml.cs`, wywołaj `EngagementReach.Instance.OnActivated(e);` w hello **Application_Activated** bezpośrednio po zainicjowaniu agenta hello:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

Wszystko jest gotowe. Teraz zostanie zweryfikowane, czy podstawowa integracja została przeprowadzona prawidłowo.

## <a id="send"></a>Wyślij aplikacji tooyour powiadomień
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Powinien zostać wyświetlony powiadomienia na urządzeniu, które będzie widoczne jako powiadomienie w aplikacji, jeśli aplikacja hello jest otwarty jako powiadomienie wyskakujące, takie jak następujące hello: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
