---
title: "aaaGet Started with Azure Mobile Engagement Unity Android wdrożenia"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Unity wdrażanych tooiOS urządzeń."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Wprowadzenie do usługi Azure Mobile Engagement na potrzeby wdrożenia aplikacji platformy Unity na urządzeniu z systemem Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji platformy Unity podczas wdrażania tooan urządzenia z systemem Android.
Ten samouczek używa hello klasycznego Przywróć Unity samouczek piłka jako punkt początkowy hello. Należy wykonać kroki hello na tym [samouczek](mobile-engagement-unity-roll-a-ball.md) przed kontynuowaniem hello integracji usługi Mobile Engagement, która została przedstawiona w samouczku hello poniżej. 

Ten samouczek wymaga następujących hello:

* [Edytor platformy Unity](http://unity3d.com/get-unity)
* [Zestaw SDK platformy Unity usługi Mobile Engagement](https://aka.ms/azmeunitysdk)
* Zestaw SDK systemu Google Android

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
### <a name="import-hello-unity-package"></a>Importowanie pakietu Unity hello
1. Pobierz hello [pakiet Unity usługi Mobile Engagement](https://aka.ms/azmeunitysdk) i zapisz go tooyour komputera lokalnego. 
2. Przejdź za**zasoby -> Importuj pakiet -> Pakiet niestandardowy** i wybierz hello pakietu pobranego w hello powyżej kroku. 
   
    ![][70] 
3. Upewnij się, że są zaznaczone wszystkie pliki, a następnie kliknij przycisk **Import** (Importuj). 
   
    ![][71] 
4. Gdy Import zakończy się pomyślnie, zobaczysz hello zaimportowane pliki zestawu SDK w projekcie.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Aktualizacja hello EngagementConfiguration
1. Otwórz hello **EngagementConfiguration** pliku skryptu z zestawu SDK hello hello folderu i zaktualizuj **ANDROID\_połączenia\_ciąg** parametrami połączenia hello uzyskanymi wcześniej z hello portalu Azure.  
   
    ![][73]
2. Zapisz plik hello 
3. Wykonaj polecenie **File -> Engagement -> Generate Android Manifest** (Plik -> Engagement -> Generowanie manifestu systemu Android). Jest to hello wtyczka dodana przez zestaw SDK usługi Mobile Engagement hello i kliknięcie jej automatycznie spowoduje zaktualizowanie ustawień projektu. 
   
    ![][74]

> [!IMPORTANT]
> Upewnij się, że tooexecute to za każdym razem, gdy hello **EngagementConfiguration** pliku, w przeciwnym razie zmiany nie zostaną odzwierciedlone w aplikacji hello. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Konfigurowanie aplikacji hello na potrzeby śledzenia podstawowego
1. Otwórz hello **PlayerController** skrypt dołączony obiektu Player toohello. 
2. Dodaj następujące hello instrukcję using:
   
        using Microsoft.Azure.Engagement.Unity;
3. Dodaj następujące toohello hello `Start()` — metoda
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Wdrażanie i uruchamianie aplikacji hello
Upewnij się, że zestaw SDK systemu Android zainstalowane na komputerze przed podjęciem próby wykonania toodeploy to urządzenie tooyour aplikacji platformy Unity. 

1. Podłącz urządzenie z systemem Android tooyour maszynę. 
2. Wybierz pozycję **File -> Build Settings** (Plik -> Ustawienia kompilacji). 
   
    ![][40]
3. Wybierz pozycję **Android** a następnie kliknij pozycję **Switch Platform** (Przełącz platformę).
   
    ![][51]
   
    ![][52]
4. Kliknij pozycję **Player settings** (Ustawienia odtwarzacza) i podaj prawidłowy identyfikator pakietu. 
   
    ![][53]
5. Na koniec kliknij pozycję **Build And Run** (Kompiluj i uruchom).
   
    ![][54]
6. Może być zadawane tooprovide folderu nazwa toostore hello pakietu systemu Android. 
7. Jeśli wszystko odbędzie poprawnie, pakiet hello zostaną wdrożone tooyour połączone urządzenia i powinien być widoczny gry środowiska Unity w telefonie! 

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Aktualizacja hello EngagementConfiguration
1. Otwórz hello **EngagementConfiguration** pliku skryptu z zestawu SDK hello hello folderu i zaktualizuj **ANDROID\_GOOGLE\_numer** z hello **projektu Google Numer** uzyskanymi wcześniej z portalu Google Cloud Developer hello. Jest to ciąg wartości, dlatego upewnij się, że tooenclose ją w podwójny cudzysłów. 
   
    ![][75]
2. Zapisz plik hello. 
3. Wykonaj polecenie **File -> Engagement -> Generate Android Manifest** (Plik -> Engagement -> Generowanie manifestu systemu Android). Jest to hello wtyczka dodana przez zestaw SDK usługi Mobile Engagement hello i kliknięcie jej automatycznie spowoduje zaktualizowanie ustawień projektu. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Konfigurowanie powiadomień tooreceive aplikacji hello
1. Otwórz hello **PlayerController** skrypt dołączony obiektu Player toohello. 
2. Dodaj następujące toohello hello `Start()` — metoda
   
        EngagementReachAgent.Initialize();
3. Teraz, gdy hello aplikacja jest zaktualizowana, wdrażanie i uruchamianie aplikacji hello na urządzeniu na powitania poniższymi instrukcjami. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
