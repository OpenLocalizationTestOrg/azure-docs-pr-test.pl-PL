---
title: "aaaGet Started with Azure Mobile Engagement dla wdrożenia iOS Unity"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Unity wdrażanych tooiOS urządzeń."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Wprowadzenie do usługi Azure Mobile Engagement na potrzeby wdrożenia aplikacji platformy Unity na urządzeniu z systemem iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji platformy Unity podczas wdrażania tooan urządzenie z systemem iOS.
Ten samouczek używa hello klasycznego Przywróć Unity samouczek piłka jako punkt początkowy hello. Należy wykonać kroki hello na tym [samouczek](mobile-engagement-unity-roll-a-ball.md) przed kontynuowaniem hello integracji usługi Mobile Engagement, która została przedstawiona w samouczku hello poniżej. 

Ten samouczek wymaga następujących hello:

* [Edytor platformy Unity](http://unity3d.com/get-unity)
* [Zestaw SDK platformy Unity usługi Mobile Engagement](https://aka.ms/azmeunitysdk)
* Edytor XCode

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS
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
1. Otwórz hello **EngagementConfiguration** pliku skryptu z zestawu SDK hello hello folderu i zaktualizuj **IOS\_połączenia\_ciąg** z hello parametry połączenia uzyskanymi wcześniej z hello portalu Azure.  
   
    ![][73]
2. Zapisz plik hello. 

### <a name="configure-hello-app-for-basic-tracking"></a>Konfigurowanie aplikacji hello na potrzeby śledzenia podstawowego
1. Otwórz hello **PlayerController** skrypt dołączony obiektu Player toohello. 
2. Dodaj następujące hello instrukcję using:
   
        using Microsoft.Azure.Engagement.Unity;
3. Dodaj następujące toohello hello `Start()` — metoda
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Wdrażanie i uruchamianie aplikacji hello
1. Podłącz maszynę tooyour urządzenia z systemem iOS. 
2. Wybierz pozycję **File -> Build Settings** (Plik -> Ustawienia kompilacji). 
   
    ![][40]
3. Wybierz pozycję **iOS**, a następnie kliknij pozycję **Switch Platform** (Przełącz platformę).
   
    ![][41]
   
    ![][42]
4. Kliknij pozycję **Player settings** (Ustawienia odtwarzacza) i podaj prawidłowy identyfikator pakietu. 
   
    ![][53]
5. Na koniec kliknij pozycję **Build And Run** (Kompiluj i uruchom).
   
    ![][54]
6. Może być zadawane tooprovide pakietu systemu iOS hello toostore nazwę folderu. 
   
    ![][43]
7. Jeśli wszystko odbędzie się poprawnie, hello projekt zostanie skompilowany i należy otwierać w aplikacji XCode. 
8. Upewnij się, że hello **identyfikator pakietu** jest prawidłowa w projekcie hello.  
   
    ![][75]
9. Teraz uruchamianie aplikacji hello w środowisku XCode, dzięki czemu pakietów hello jest tooyour wdrożony na podłączonym urządzeniu i na telefonie będzie widoczna gry środowiska Unity! 

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract z użytkownikami i ZASIĘGU z powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Nie można znaleźć toodo żadnej dodatkowej konfiguracji powiadomienia tooreceive aplikacji i jest już skonfigurowana.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
