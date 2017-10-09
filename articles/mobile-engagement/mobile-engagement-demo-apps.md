---
title: Aplikacja demonstracyjna aaaAzure Mobile Engagement | Dokumentacja firmy Microsoft
description: "Opisuje miejsce toodownload, jak toouse i zalet hello przy użyciu usługi Azure Mobile Engagement demonstracją aplikacji"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Aplikacja demonstracyjna usługi Azure Mobile Engagement
Mamy już opublikowana aplikacja demonstracyjna usługi Azure Mobile Engagement dla **iOS**, **Android**, i **Windows** toohelp platform można toofind przydatne zasoby i Dowiedz się więcej o Mobile Zaangażowania.

Aplikacja Hello ułatwia:

* Łatwo łącza przydatne tooMobile zaangażowania zasobów, takich jak pliki wideo, dokumentację, hello forum pomocy technicznej, i gdy zażąda toogo tooraise funkcji.
* Środowisko próbki powiadomień, które są obsługiwane przez pomysły tooget Mobile Engagement dla aplikacji mobilnych.
* Jak używać toostudy implementacji odwołanie tooimplement Mobile Engagement do własnych aplikacji. Aby dowiedzieć się do:
  
  * Zbierać dane analityczne.
  * Wdrożenie, takie jak zaawansowanych scenariuszy powiadomień typów *pełnoekranowy międzysegmentowe* lub *wyskakujących*.
  * Implementuje ankiet i ankiety.
  * Implementowanie scenariuszy dyskretnej wypychania danych i wypychania.   

## <a name="app-installation"></a>Instalacja aplikacji
Ta aplikacja jest dostępna w powitania po sklepów z aplikacjami:

* **Uniwersalnych systemu Windows aplikacja demonstracyjna**:
  
  * Pobierz aplikację hello na powitania [Sklepu Windows](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * Aplikacja Hello został opracowany jako aplikacji uniwersalnych systemu Windows 10. Kod źródłowy Hello jest dostępne na [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **iOS demonstracją aplikacji**:
  
  * Pobierz aplikację hello na powitania [sklepu Apple](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * Aplikacja Hello został opracowany w systemu iOS w języku Swift. Kod źródłowy Hello jest dostępne na [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Aplikacja demonstracyjna android**:
  
  * Pobierz aplikację hello na powitania [sklepu Google Play](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * Kod źródłowy Hello jest dostępne na [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Aplikacja demonstracyjna uniwersalnych systemu Windows][1]

![iOS demonstracją aplikacji][2]
![aplikacja demonstracyjna systemu Android][3]

## <a name="usage"></a>Sposób użycia
Można użyć tej aplikacji w hello następujące sposoby:

**Pobierz aplikacji hello na urządzeniu z hello aplikacji sklepu łączy (starszych):**

> [!IMPORTANT]
> Nie potrzebujesz konta platformy Azure lub wymagają tooconnect hello aplikacji tooa zaplecza. Aplikacja Hello działa niezależnie.
> 
> 

* Po utworzeniu aplikacji hello na urządzeniu, można przejść za pośrednictwem łączy hello w hello menu po lewej stronie toofind hello przydatne zasoby dotyczące usługi Mobile Engagement.
* Dodaliśmy hello [źródło danych RSS usługi](https://aka.ms/azmerssfeed) do tej aplikacji, aby zawsze jest zaktualizowano o najnowsze aktualizacje produktu hello.
* Można również przejść przez hello przykładowe scenariusze tooexperience hello typ powiadomienia powiadomień, które są obsługiwane przez usługi Mobile Engagement dla każdej platformy. Te powiadomienia mogą być doświadczonym lokalnie — to znaczy, możesz kliknąć przyciski hello na tooshow ekranów powitalnych możesz hello środowiska powiadomienia powiadomienia hello toosending identyczne z hello platformy Mobile Engagement.

![Menu aplikacji dla systemu Windows][4]

![Menu aplikacji dla systemu iOS][5]
![menu aplikacji dla systemu Android][6]

**Pobierz kod źródłowy hello z hello GitHub łączy (starszych):**

* Po pobraniu hello kodu źródłowego, można go otworzyć w środowisku projektowym odpowiednich hello--XCode dla systemu iOS, Android Studio dla systemów Android i Visual Studio dla systemu Windows.
* Następnie należy wykonać naszych [podstawowe kroki integracji zestawu SDK](mobile-engagement-windows-store-dotnet-get-started.md) tak, że wszystko jest w stanie tooconnect tooits tej aplikacji własne wystąpienie zaplecza usługi Mobile Engagement.
  * Należy tooconfigure parametry połączenia w aplikacji hello.
  * Należy również tooconfigure hello wypychania powiadomień platformy dla aplikacji.
* Można zauważyć, że w tej samej aplikacji hello są instrumentowane przy użyciu usługi Mobile Engagement. W związku z tym po otwarciu aplikacji hello po podłączeniu go zaplecza toohello będzie sesji użytkownika hello stanie toosee, działania, zdarzenia i tak dalej, na powitania **Monitor** kartę.
* Również będziesz aplikacji toothis powiadomienia o stanie toosend własnego wystąpienia usługi Mobile Engagement, zamiast lokalnego powiadomienia.
  
  * W tym miejscu można dodać urządzenia jako urządzenia testu za pomocą hello **hello pobranie Identyfikatora urządzenia** element menu w aplikacji hello. Zapewnia to identyfikator urządzenia, które następnie zarejestrować jako urządzenia testu z wystąpieniem platformy zaplecza.
    
    ![Identyfikator urządzenia w systemie Windows][7]
    
    ![Identyfikator urządzenia w systemie iOS][8]
    ![identyfikator urządzenia w systemie Android][9]

## <a name="key-features-of-hello-demo-app"></a>Najważniejsze funkcje aplikacja demonstracyjna hello
* Jak wspomniano wcześniej, z tą aplikacją, masz wszystkie hello kluczowych zasobów dla usługi Mobile Engagement w dłoni. W menu po lewej stronie powitania można przejść za pośrednictwem łącza hello.
* Może wystąpić poza aplikacji powiadomień dla każdej platformy. Te powiadomienia mogą być dostarczane jako **tylko powiadomienie**, gdzie kliknięcie powiadomienia powitania po prostu otwiera natywnego ekranu aplikacji hello (przy użyciu **bezpośrednich połączeń**)--lub jako **sieci Web Zawiadomienie**, gdzie można dostarczyć dodatkową zawartość HTML z hello kończyć powrotem Engagement Mobile toobe wyświetlane po kliknięciu hello powiadomień.
  
    ![Powiadomienia w poziomie aplikacji][29]
* W systemach iOS masz tooclose hello aplikacji toosee hello poza aplikacji lub systemu powiadomień wypychanych. Można przyjrzeć się hello implementację dodawania **przycisków akcji**, takie jak hello te, które są dodane toothis poza aplikacji powiadomienia o *opinii* i *udziału* (dzięki czemu Witaj użytkownika może potrwać akcji bezpośrednio w hello powiadomień, się).
  
    ![Powiadomienia poza aplikacji w systemie iOS][11] ![Wyświetl powiadomienie poza aplikacji w systemie iOS][14]
* Hello opcje, które są obsługiwane w systemie Android, dodawania wielowierszowy tekst (**tekst Big**) lub obraz powiadomienia (**szerszej**) toohello powiadomienia, oraz hello **przycisków akcji** (jak obsługiwane przez system iOS).
  
    ![Powiadomienia poza aplikacji w systemie Android][12] ![Wyświetl powiadomienie poza aplikacji w systemie Android][15]
* W systemie Windows 10 widać wygląd powiadomienia hello na powitania komputera. To powiadomienie również zostaną wyświetlone w hello systemu Windows 10 **Centrum powiadomień**. Nie obsługuje dodawania **przycisków akcji** w chwili hello hello zestaw Windows SDK.
  
    ![Powiadomienia poza aplikacji w systemie Windows][10] ![Wyświetl poza aplikacji w systemie Windows][13]
* Może wystąpić powiadomień "w aplikacji" domyślna dla każdej platformy. To środowisko dwuetapowej gdzie **powiadomień** okno jest wyświetlane jako pierwsze. Po kliknięciu go uruchomi pełny ekran **anonsu**wyświetlane w hello następującego zrzutu ekranu. zawartość Hello tego anonsu pochodzi z wystąpieniem zaplecza usługi Mobile Engagement. Hello zestaw SDK zawiera szablony hello powiadomienia i anonsów. Możesz można łatwo dostosować je, jak pokazano w tej aplikacji demonstracyjnej z dodanie hello kolorowanie i logo firmy Microsoft.  
  
    ![Powiadomienia w aplikacji w systemie Windows][16]
  
    ![Powiadomienia w aplikacji w systemie iOS][17]  ![Powiadomienia w aplikacji w systemie Android][18]
  
    **iOS**, **systemu Android**
* Można również użyć hello **kategorii** funkcji toocustomize Mobile Engagement to środowisko domyślne. W aplikacji demonstracyjnej hello firma Microsoft już zostało to pokazane dwie typowe sposoby toochange hello środowisko hello powiadomienia. Należy pamiętać, że funkcja ta kategoria hello nie jest jeszcze obsługiwana w hello zestaw Windows SDK.
  
    **Pełnoekranowy międzysegmentowe:**
  
    ![Powiadomienie w aplikacji - międzysegmentowe kategorii][30]
  
    ![Kategoria międzysegmentowe w systemie iOS][21]     ![Kategoria międzysegmentowe w systemie Android][22]
  
    **Wyskakujące powiadomienie:**
  
    ![Powiadomienie w aplikacji - kategorii wyskakujących][31]
  
    ![Wyskakujące powiadomienia w systemie iOS][19]    ![Wyskakujące powiadomienia w systemie Android][20]

**iOS**, **systemu Android**

* Usługa Mobile Engagement obsługuje również specjalistyczną odmianą powiadomienie w aplikacji o nazwie **sond**. Dzięki temu toosend użytkowników aplikacji tooyour segmentem szybkie ankiet. Możesz dodać pytania i opcje dla każdego pytania, jak hello następującego zrzutu ekranu. To następnie Uzyskaj wyświetlona jako użytkownik aplikacji toohello powiadomienie w aplikacji.   
  
    ![Powiadomienia sondowania][32]
  
    ![Ankieta w systemie Windows][26]
  
    ![Badanie w systemie iOS][27]   ![Ankieta w systemie Android][28]

**iOS**, **systemu Android**

* Usługa Mobile Engagement obsługuje również wysyłanie dyskretnej **wypychania danych** powiadomienia. Z te powiadomienia można wysyłać dane z usługi (na przykład hello dane JSON w hello poniższy przykład), który może obsługiwać w aplikacji i niektóre reakcję. Przykładem jest sposób Zmieniamy cen hello elementu selektywnie przy użyciu powiadomień wypychanych danych.
  
    ![Powiadomienia wypychane danych][33]
  
    ![Powiadomienia wypychane danych w systemie Windows][23]
  
    ![Powiadomienia wypychane danych w systemie iOS][24]  ![Powiadomienia wypychane danych w systemie Android][25]

**iOS**, **systemu Android**

> [!NOTE]
> Szczegółowe instrukcje krok po kroku dla każdego powiadomienia te można wyświetlić, klikając **kliknij tutaj, aby uzyskać instrukcje dotyczące toosend te powiadomienia z platformy Mobile Engagement** na wszystkie próbki powiadomienia ekranu.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
