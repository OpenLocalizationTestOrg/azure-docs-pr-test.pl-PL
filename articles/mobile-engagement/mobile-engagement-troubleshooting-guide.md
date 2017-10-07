---
title: "aaaAzure Mobile Engagement Rozwiązywanie problemów z przewodników"
description: "Podręcznik rozwiązywania problemów dotyczących usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement — przewodnik rozwiązywania problemów
## <a name="introduction"></a>Wprowadzenie
Witaj czynności przedstawione w przewodniku rozwiązywania problemów pomoże poznać głównych przyczyn niektóre często spotykanych problemów i spowoduje włączenie tootroubleshoot samodzielnie. 

## <a name="general"></a>Ogólne
Ogólnie rzecz biorąc zawsze należy hello poniżej:

1. Upewnij się, że przeszły kroków hello wszystkich wymaganych do integracji, zgodnie z opisem w naszym [samouczki dotyczące rozpoczynania pracy](mobile-engagement-windows-store-dotnet-get-started.md)
2. Używasz hello najnowszą wersję platformy hello zestawów SDK. 
3. Test na rzeczywistego urządzenia i emulatora, ponieważ niektóre problemy są tylko określone tooemulator. 
4. Czy nie osiągnięto żadnych limitów/limity z usługi Mobile Engagement opisanych [tutaj](../azure-subscription-service-limits.md)
5. Jeśli nie jest możliwe toohello tooconnect Mobile Engagement usługi wewnętrznej bazy danych lub wyświetlać dane nie ładowany stale, upewnij się, że nie ma żadnych zdarzeń usługi trwającą sprawdzając [tutaj](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>Problemy z "Monitora"
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Nie widzę urządzenie pojawia się na karcie monitorowanie hello
Karta monitor przedstawia platformy Mobile Engagement tooyour podłączonego urządzenia hello w czasie rzeczywistym. Debugowania na emulator i urządzeń, należy zobacz co najmniej jedną sesję w tym miejscu. Jeśli aplikacja hello został rozesłany, będą widzieć hello aktywne sesje miernika odzwierciedlają hello urządzeń, które są połączone toohello platformą w czasie rzeczywistym. 

Jeśli nie widzisz urządzenia na karcie Monitor hello jest prawdopodobnie problem w integracji zestawu SDK. Niektóre typowe tootroubleshoot tootake kroki są następujące:

1. Upewnij się, że używasz hello prawidłowych parametrów połączenia w aplikacji mobilnej hello i jest z hello klucze zestawu SDK i nie hello sekcji klucze interfejsu API. ciąg połączenia Hello łączy aplikację usługi Mobile Engagement hello, w którym Twoje urządzenie będzie widoczne na karcie Monitor hello wystąpieniem toohello aplikacji mobilnej. 
2. Dla platformy systemu Windows — Jeśli strona zastępuje hello `OnNavigatedTo` metoda, upewnij się, że toocall `base.OnNavigatedTo(e)`.
3. Jeśli usługa Mobile Engagement są integracji istniejących aplikacji mobilnej, można także zapewnić, że nie brakuje żadnych kroków analizując hello zaawansowane kroki integracji [tutaj](mobile-engagement-windows-store-integrate-engagement.md)
4. Upewnij się, co najmniej jednego ekranu/działania są wysyłane przez zastąpienie hello strony z EngagementActivity w zależności od platformy hello działają zgodnie z opisem w hello [samouczki dotyczące rozpoczynania pracy](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>Widzę kartę Monitor hello przedstawiający sesji nawet gdy zostały odłączone lub zamknięty Moja aplikacja / emulatora.
Jeśli w tym momencie są tylko jedną platformę połączonych toohello hello i za pomocą aplikacji hello tooopen emulatora następnie jest prawdopodobnie z powodu tooemulator Osobliwości. Ogólnie rzecz biorąc należy tooensure, że możesz wrócić ekran toohello głównej na powitania emulator toodisconnect sesji aplikacji hello pomyślnie. Ponadto na platformie systemu Windows podczas debugowania w programie Visual Studio, może być konieczne tooensure w programie Visual Studio, należy przejść toohello **zdarzenia cyklu życia** paska menu i kliknij pozycję **zawieszenia** tooreally Zamknij Witaj sesji. Zobacz [Samouczek Windows](mobile-engagement-windows-store-dotnet-get-started.md) szczegółowe informacje. 

## <a name="analytics-issues"></a>Problemy z "Analytics"
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>I nie zwróciła żadnych danych / odświeżenia danych na karcie analityka
Dane analityczne są przeliczane regularnie i może potrwać maksymalnie 24 godziny na odświeżenie nie powiedzie się. Te dane nie są w czasie rzeczywistym i zobaczysz, że są one odświeżane w ramach tego 24-godzinnym przedziale czasu.
Upewnij się, mimo że wysyłasz co najmniej jednego ekranu lub działania toohello platforma wewnętrznej bazy danych o albo zastępowanie co najmniej jedną stronę z `EngagementActivity` lub wywoływania `SendActivity` explcitly. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Na karcie Analytics hello widzę niepoprawnie przechwyconych daty i godziny dla urządzenia
Hello okresu Analytics jest oparty na hello dat od użytkowników hello ustawień urządzenia. Dlatego upewnij się, że hello urządzenie ma datę hello prawidłowo ustawione. 

## <a name="segment-issues"></a>Problemy z "Segmentu"
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>Utworzono segment i jest wyświetlana jako nieaktywna lub nie są wyświetlane wszystkie dane
Tworzenie segmentu nie jest w czasie rzeczywistym w chwili hello. Jest ona obliczana na powitania się, że czas takie same jak dane analityczne hello jest agregowana w związku z czym może potrwać maksymalnie 24 godziny. Należy sprawdzić ponownie później, ale w tym samym czasie należy upewnić się, że aplikacje mobilne w rzeczywistości wysyłania danych hello na podstawie hello, w których są tworzące hello segmentów. Na przykład Jeśli zdarzenie powiedzieć "foo" nie jest wysyłane przez wszystkich urządzeń przenośnych, a następnie byłoby żadnych danych segmentu dla segmentu utworzony o nazwie EventName = foo jako kryterium hello. Należy także sprawdzić tooensure integracji z zestawem SDK aplikacji mobilnej wysyła dane hello poprawnie. 

## <a name="reach-or-push-notifications-issues"></a>Problemy z "Zasięg" lub powiadomień wypychanych
### <a name="my-push-messages-are-not-being-delivered"></a>Nie są dostarczane wiadomości wypychanych
1. Spróbuj wysłać tooensure pierwszego powiadomienia tooa testu urządzenia, czy wszystkie składniki hello - aplikacji mobilnej, usługa zestawu SDK i hello są poprawnie połączony i stanie toodeliver powiadomień wypychanych. 
2. Zawsze wysyłaj najprostszym do hello "powiadomienie poza aplikacji" najpierw za pośrednictwem kampanii, które nie zostało zaplanowane i ani dowolnego kryterium odbiorców określony. To jest ponownie tooprove, czy powiadomienia połączenie działa poprawnie. 
3. Jeśli występują problemy z dostarczanie powiadomień w aplikacji, a następnie jest bardzo pierwszy krok tootry najpierw wysyła powiadomienie poza aplikacji. 
4. Upewnij się, że powitalne "Natywnych powiadomień wypychanych" jest poprawnie skonfigurowany dla aplikacji mobilnej. W zależności od platformy hello albo obejmuje się kluczy (Android i Windows) lub certyfikatów (iOS). Zobacz [interfejsu użytkownika — ustawienia](mobile-engagement-user-interface-settings.md)
5. Poza aplikacją powiadomienia można również zablokowany przez hello użytkownika za pośrednictwem hello przenośnego systemu operacyjnego więc upewnij się, to nie jest hello. 
6. Upewnij się, że nie konfigurujesz hello *Ignoruj odbiorców, wypychane będą wysyłane toousers za pośrednictwem interfejsu API hello* opcję hello **kampanii** sekcji Reach kampanii, ponieważ daje to pewność, że wypychania powiadomień może być wysyłane tylko za pośrednictwem interfejsów API. 
7. Upewnij się, zarówno urządzenia z systemem połączonych za pośrednictwem sieci Wi-Fi i phone operatora sieci tooeliminate hello połączenia sieciowego w postaci źródłem problemów testowania kampanii wypychania.
8. Upewnić się, że system hello daty/godziny na urządzeniu/emulatorze jest poprawna, ponieważ wszystkie urządzenia zsynchronizowane również zakłóca powiadomienia toodeliver możliwości hello Push Notification Service Portal firmy. 

Więcej platformy Rozwiązywanie problemów z instrukcjami poniżej:

1. **iOS** 
   
   * Upewnij się, że certyfikaty hello są prawidłowe i niewygasłe dla powiadomień wypychanych systemu iOS. 
   * Upewnij się, poprawne skonfigurowanie *produkcji* certyfikatu w aplikacji usługi Mobile Engagement. 
   * Upewnij się, że testowania na *prawdziwe, fizyczne urządzenie.* Witaj symulatora systemu iOS nie można przetworzyć wiadomości wypychanych.
   * Upewnij się, hello, że identyfikator pakietu jest poprawnie skonfigurowany na powitania aplikacji mobilnej. Zobacz instrukcje hello [tutaj](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Podczas testowania, przy użyciu dystrybucji "Ad Hoc" w profilu inicjowania obsługi administracyjnej przenośnych. Nie będzie powiadomienia o stanie tooreceive Jeśli aplikacja jest skompilowana przy użyciu "Debug"
2. **Android**
   
   * Upewnij się, że określono poprawny numer projektu hello w pliku AndroidManifest.xml aplikację mobilną, której następuje znak \n. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Upewnij się, czy nie są brakujące lub nieprawidłowo skonfigurowane wszystkie uprawnienia w pliku manifestu systemu Android hello 
   * Upewnij się, czy w przypadku dodawania aplikacji klienckiej tooyour numer projektu hello pochodzi z tego samego konta, gdzie masz hello klucz serwera GCM Server hello. Wszelkie niezgodność między hello dwa uniemożliwi Twojej wypchnięć przejście. 
   * W przypadku otrzymania systemu powiadomień, ale nie w aplikacji następnie przejrzyj hello [Określanie ikony dla powiadomień sekcji](mobile-engagement-android-get-started.md) jako prawdopodobnie nie określisz ikony jest poprawna hello w pliku manifestu systemu Android hello. 
   * Jeśli wysyłania powiadomień BigPicture, upewnij się, że jeśli masz serwery obrazów zewnętrznych, a następnie muszą toosupport stanie toobe HTTP "GET" i "HEAD".
3. **Windows**
   
   * Upewnij się, że aplikacja hello został skojarzony z prawidłową aplikację ze Sklepu Windows. W programie Visual Studio — będzie mieć tooright kliknij hello projektu i wybierz opcję "Kojarzenie aplikacji z magazynu" i aplikacja hello wybierz utworzony w Sklepie Windows hello. Ta aplikacja ze Sklepu Windows należy hello samym kluczem, z którym masz tooconfigure poświadczenia natywnych powiadomień wypychanych hello w portalu Mobile Engagement hello.
   * W przypadku otrzymania powiadomienia wypychane w poziomie aplikacji, ale powiadomienia nie w aplikacji przy użyciu `EngagementOverlay` integracji następnie upewnij się, Brak elementu głównego siatki na stronie. EngagementOverlay używa hello pierwszy "Siatki" elementu znalezionych w Twojej xaml pliku tooadd dwa widoki sieci web na stronie. Jeśli chcesz toolocate, w którym można ustawić widoki sieci web, można zdefiniować siatki o nazwie "EngagementGrid" podobny do tego, jednak będą miały tooensure jest wystarczające wysokość i szerokość dla hello dwa kolejne sieci web widoków, które będą Pokaż powiadomienia hello i hello po anonsie jako powiadomienie w aplikacji:
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>Po utworzeniu powiadomień wypychanych/anonsu/kampanii i nawet po ona wysłana do mnie powiadomienie hello, jest wyświetlany jako "Aktywny". Co to znaczy?
Witaj **kampanii** utworzony w usłudze Mobile Engagement jest wywoływana, długotrwałą znaczenie powiadomień wypychanych jako platforma usługi mobile engagement tooyour połączenia nowych urządzeń, dlatego zostaną automatycznie wysłane powiadomienie hello Możesz skonfigurować, ile spełniają one kryterium hello, ustawionych w hello kampanii. To nie jest plikiem zrzut pojedyncze powiadomienia Instalatora. Konieczne będzie toomanually kliknij hello **Zakończ** przycisk tooterminate hello kampanii nie go wysyłanie dalszych powiadomienia. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>Po utworzeniu kampanii wypychania i otrzymuję powiadomień pomyślnie jednak przy każdym otwarciu zapasowej aplikacji hello uzyskać hello tego samego powiadomienia nawet wtedy, gdy użytkownik miał których wykonano akcje go przed?
Jest to prawdopodobnie toohappen podczas testowania i jeśli używasz emulatory lub niektóre struktury testowej, takich jak TestFlight. Co dzieje się w tym miejscu jest na wszystkie aplikacje uruchomione wystąpienie jest uzyskiwanie nowego DeviceID i wysłaniem tooour wewnętrznej bazy danych, które powoduje tootreat platformy Mobile Engagement hello go jako nowe urządzenie i wysyłania powiadomień hello. 

## <a name="getting-support"></a>Uzyskiwanie pomocy technicznej
Jeśli wszystko jest problem hello tooresolve następnie możesz:

1. Wyszukaj problemu w wątkach istniejących hello na StackOverflow forum i [MSDN forum](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) i jeśli nie następnie zadać pytanie. 
2. Jeśli okaże się funkcja brak następnie dodać/głos dla żądania hello na naszych [forum usługi UserVoice](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Jeśli masz Microsoft obsługują otwarte zdarzenia pomocy technicznej przez zapewnienie hello poniższe informacje: 
   * Identyfikator subskrypcji platformy Azure
   * Platforma (np. systemy iOS, Android itp.)
   * Identyfikator aplikacji
   * Identyfikator kampanii (w przypadku problemów powiadomienia wypychane)
   * Identyfikator urządzenia
   * Wersja zestawu SDK usługi Mobile Engagement (np. v2.1.0 zestawu SDK systemu Android)
   * Szczegóły błędu z dokładną komunikat i scenariusza

