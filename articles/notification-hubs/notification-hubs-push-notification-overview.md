---
title: "aaaAzure centra powiadomień"
description: "Dowiedz się, jak tooadd push możliwości powiadomienia za pomocą usługi Azure Notification Hubs."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Azure Notification Hubs
## <a name="overview"></a>Omówienie
Centra powiadomień Azure zapewniają aparat wypychania łatwy w użyciu, obejmującego wiele platform, skalowalnych w poziomie. Wywołanie interfejsu API jednym i platform umożliwia łatwe wysyłanie platform przenośnych tooany powiadomień wypychanych docelowych i spersonalizowaną z poziomu dowolnego zaplecza w chmurze lub lokalnie.

Centra powiadomień działa Wielkiej dla firm i konsumentów scenariuszy. Oto kilka przykładów, których klienci używają usługi Notification Hubs dla:

* Wysyłanie najważniejszych wiadomości powiadomienia toomillions z niskim opóźnieniem.
* Wysyłaj kupony oparte na lokalizacji toointerested segmentów użytkowników.
* Wysyła powiadomienia związane ze zdarzeniami toousers lub grup dla aplikacji media/sportowych/finance/gier.
* Wypchnij toocustomers rynku i tooengage tooapps promocyjna zawartość.
* Powiadom użytkowników o zdarzeniach dotyczących przedsiębiorstwa takie jak nowe wiadomości i elementów roboczych.
* Wyślij kody uwierzytelniania wieloskładnikowego.

## <a name="what-are-push-notifications"></a>Co to są powiadomienia wypychane?
Powiadomień wypychanych jest formę komunikacji aplikacji do użytkownika, gdy powiadamiania użytkowników aplikacji mobilnych niektórych informacji żądaną, zazwyczaj w oknie podręcznym lub okno dialogowe. Użytkownicy zazwyczaj można wybrać tooview lub odrzucić wiadomości powitania i wybierając była hello spowoduje otwarcie hello aplikacją mobilną, które były przekazywane hello powiadomień.

Wysyłanie powiadomień wypychanych jest zwiększenie zaangażowania i użycia aplikacji w aplikacjach dla użytkowników indywidualnych i aplikacje przedsiębiorstwa w komunikacji biznesowej aktualne informacje. Jest on hello najlepszą komunikację aplikacji do użytkownika, ponieważ jest zużyciu energii dla urządzeń przenośnych, elastyczne dla nadawców powiadomienia hello i dostępne, gdy odpowiednie aplikacje nie są aktywne.

Aby uzyskać więcej informacji na powiadomienia wypychane dla kilku popularnych platform:
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Sposób działania powiadomień wypychanych
Powiadomienia wypychane są dostarczane przy użyciu infrastruktur dla poszczególnych platform o nazwie *systemów powiadomień platformy* (PNSes). Oferują funkcje wypychania barebone toodelivery komunikat tooa urządzenia z podanych obsługi i nie ma wspólnego interfejsu. toosend powiadomienia klientów tooall między hello iOS, Android i Windows wersje aplikacji, Projektant hello należy skontaktować się z APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging) i usługi WNS (Windows Notification Service), podczas przetwarzania wsadowego wysyła Hello.

Na wysokim poziomie poniżej przedstawiono, jak działa wypychania:

1. Aplikacja kliencka Hello stwierdza, że chce się, że tooreceive wypchnięcia dlatego hello kontaktów odpowiadającego tooretrieve systemu powiadomień platformy uchwytu wypychania unikatowy i tymczasowych. typ dojścia Hello zależy od systemu hello (np. usługi WNS ma identyfikatory URI, podczas gdy APNS ma tokenów).
2. Hello aplikacja kliencka przechowuje to dojście w zaplecze aplikacji hello lub dostawcy.
3. toosend powiadomienia wypychanego zaplecze aplikacji hello kontaktuje się hello systemu powiadomień platformy przy użyciu tootarget dojście hello aplikacji określonego klienta.
4. Witaj systemu powiadomień platformy przekazuje urządzenia toohello powiadomień hello określonego przez dojście hello.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Witaj trudności z powiadomień wypychanych
Gdy PNSes są wydajne, opuszczają Deweloper aplikacji toohello dużo pracy w kolejności tooimplement nawet typowe scenariusze dotyczące powiadomień wypychanych, takie jak emitowanie lub wysyłanie użytkowników toosegmented powiadomień wypychanych.

Wypychania jest jednym z hello najpopularniejszych funkcji przenośnych usług w chmurze, ponieważ jego funkcjonowania wymaga infrastrukturach złożonych, które są aplikacji niezwiązanych ze sobą toohello główną logiką biznesową. Niektóre wyzwania infrastrukturalne hello są:

* **Zależności dotyczące platformy**: 

  * Hello wewnętrznej bazy danych musi toohave złożone i twardych Obsługa logiki zależny od platformy toosend powiadomienia toodevices na różnych platformach, jak PNSes nie są unified.
* **Skala**:

  * Zgodnie z zaleceniami tokeny urządzeń muszą zostać odświeżone przy każdym uruchomieniu aplikacji. Oznacza to hello wewnętrznej bazy danych zajmuje się dużą ilość ruchu sieciowego i tylko tookeep hello tokeny aktualne dostęp do bazy danych. Podczas hello liczby urządzeń rozwojem toohundreds i tysiące miliony hello koszt tworzenia i obsługi tej infrastruktury jest masowych.
  * Większość PNSes nie obsługują urządzeń toomultiple emisji. Oznacza to proste tooa emisji milionów urządzeń powoduje miliony wywołań toohello PNSes. Skalowanie tej ilość ruchu sieciowego z minimalnym opóźnieniem jest proste.
* **Routing**:
  
  * Chociaż PNSes zapewniają sposób toosend wiadomości toodevices, większości aplikacji Powiadomienia są przeznaczone do użytkowników lub grup zainteresowań. Oznacza to, że hello wewnętrznej bazy danych musi odpowiadać za utrzymanie urządzeń tooassociate rejestru, z grup zainteresowań, użytkowników, właściwości, itd. Ten narzut zwiększa toohello czasu toomarket oraz koszty obsługi aplikacji.

## <a name="why-use-notification-hubs"></a>Dlaczego warto używać usługi Notification Hubs?
Notification Hubs eliminuje wszystkich skomplikowanych elementów, skojarzonego z włączeniem push własnych. Jego infrastruktury powiadomień wypychanych obejmującego wiele platform, skalowalnych w poziomie zmniejsza wypychania związane z kodami i upraszcza z wewnętrzną bazą danych. Z usługą Notification Hubs urządzenia są jedynie odpowiedzialny za rejestrację ich dojść systemu powiadomień platformy przy użyciu koncentratora, gdy hello wewnętrznej bazy danych wysyła wiadomości toousers lub grup zainteresowań, jak pokazano w następującej ilustracji hello:

![][1]

Centra powiadomień jest aparat wypychania gotowe do użycia z hello następujące korzyści:

* **Dla wielu platform**

  * Obsługę wszystkich platform głównych wypychania z systemami iOS, Android, Windows i urządzeń Kindle i Baidu.
  * Wspólnego interfejsu toopush tooall platform w formatach specyficzne dla platformy lub niezależne od platformy z żadne czynności specyficzne dla platformy.
  * Urządzenie obsłudze w jednym miejscu.
* **Krzyżowe zapleczy**
  
  * Chmurze lub lokalnie
  * .NET, Node.js, Java,... itd.
* **Bogaty zestaw wzorców dostarczania**:

  * *Emisji tooone lub wielu platform*: można natychmiast emisji toomillions urządzenia na platformach przy użyciu jednego wywołania interfejsu API.
  * *Wypychanie toodevice*: można kierować powiadomienia tooindividual urządzeń.
  * *Wypychanie toouser*: tagi i szablony funkcji pomóc Ci zrealizować wszystkich urządzeń i platform użytkownika.
  * *Push toosegment tagami dynamiczne*: tagi funkcja pomaga segment urządzenia i push toothem zgodnie z potrzebami tooyour, czy wysyłania tooone segmentu, czy wyrażenie segmenty (np. active życie i w Seattle nie nowego użytkownika). Zamiast ograniczeniami sub toopub, możesz zaktualizować dowolnym tagi urządzenia i w czasie.
  * *Zlokalizowane wypychania*: szablony pomaga osiągnąć lokalizacji bez wpływu na kod zaplecza.
  * *Dyskretnej wypychania*: wzorzec do wypychania hello można umożliwia przez wysłanie powiadomienia dyskretnej toodevices i wyzwalania ich toocomplete niektórych ściąga lub akcji.
  * *Zaplanowane wypychania*: w każdej chwili można zaplanować toosend powiadomień.
  * *Bezpośrednie wypychania*: można pominąć, rejestrowania urządzenia z usługi i bezpośrednio partii wypychania tooa listę dojść urządzeń.
  * *Spersonalizowanych wypychania*: zmienne wypychania urządzenia spersonalizowanych pomaga wysyłania urządzenia wypychanie powiadomień z dostosowanych pary klucz wartość.
* **Rozbudowane informacje telemetryczne**
  
  * Ogólne dane telemetryczne wypychania, urządzenia, błąd i działanie jest dostępne w hello portalu Azure i programowo.
  * Na komunikat Telemetrii ścieżki każdego wypychane z usługi tooour wywołania żądania początkowego pomyślnie przetwarzanie wsadowe hello wypycha.
  * Opinie systemu powiadomień platformy komunikuje się wszystkich informacji zwrotnych z systemów powiadomień Platfom tooassist debugowania.
* **Skalowalność** 
  
  * Wysyłanie wiadomości szybkiego toomillions urządzeń bez konieczności ponownego projektowania lub urządzenie dzielenia na fragmenty.
* **Bezpieczeństwo**

  * Udostępniony klucz tajny dostępu (SAS) lub uwierzytelnianie federacyjne.

## <a name="integration-with-app-service-mobile-apps"></a>Integracja z usługą App Service Mobile Apps
toofacilitate łatwego i ujednolicających środowiska w usługach Azure [App Service Mobile Apps] ma wbudowaną obsługę powiadomień wypychanych przy użyciu usługi Notification Hubs. [App Service Mobile Apps] oferuje wysoce skalowalną, globalnie dostępną platformę aplikacji mobilnych programowanie dla deweloperów w przedsiębiorstwach i integratorów systemów. Platforma ta oferuje bogaty zestaw funkcji toomobile deweloperów.

Deweloperzy aplikacji mobilnych mogą korzystać z usługi Notification Hubs z hello następującego przepływu pracy:

1. Pobranie dojścia do urządzenia w systemie powiadomień platformy
2. Rejestrowanie urządzenia z usługą Notification Hubs za pomocą wygodny interfejs API rejestru zestawu SDK klienta usługi Mobile Apps
   * Zauważ, że usługa Mobile Apps usuwa wszystkie tagi rejestracji ze względów bezpieczeństwa. Praca z usługą Notification Hubs z poziomu zaplecza bezpośrednio tooassociate tagi z urządzeniami.
3. Wysyłanie powiadomień z zaplecza aplikacji przy użyciu usługi Notification Hubs

Oto niektóre udogodnienia toodevelopers z tej integracji:

* **Zestawy SDK klientów aplikacji mobilnej**: te wieloplatformowe zestawy SDK zapewniają proste interfejsy API do rejestracji i komunikują się Centrum powiadomień toohello skojarzone z aplikacją mobilną hello automatycznie. Deweloperzy nie muszą toodig poświadczeń usługi Notification Hubs i pracować przy użyciu dodatkowych usług.

  * *Wypychanie toouser*: hello SDK automatycznie dodają tagi hello danego urządzenia w usłudze Mobile Apps uwierzytelniony identyfikator użytkownika tooenable wypychania toouser scenariusza.
  * *Wypychanie toodevice*: hello zestawy SDK automatycznie używają hello identyfikator instalacji Mobile Apps jako identyfikatora GUID tooregister z usługą Notification Hubs, oszczędzając deweloperom pracy hello związanej z obsługą identyfikatorów GUID wielu usług.
* **Model instalacji**: Mobile Apps współpracuje z centra powiadomień w najnowszej wypychania modelu toorepresent wszystkie właściwości skojarzone z urządzeniem w instalacji JSON, które wyrównana z usługami powiadomień wypychanych i łatwe toouse jest w trybie push.
* **Elastyczność**: deweloperzy mogą zawsze włączać toowork z usługą Notification Hubs bezpośrednio nawet w przypadku integracji hello w miejscu.
* **Zintegrowane środowisko w [portalu Azure]**: wypychanie jako możliwość ma wizualną reprezentację w Mobile Apps i deweloperzy mogą z łatwością pracować z hello skojarzonego Centrum powiadomień za pośrednictwem aplikacji mobilnej.

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Notification Hubs można znaleźć w następujących tematach:

* **[W jaki sposób klienci używają usługi Notification Hubs]**
* **[Przewodniki i samouczki dotyczące usługi Notification Hubs]**
* **Samouczki wprowadzenie centra powiadomień**: [iOS], [Android], [uniwersalnych systemu Windows], [Windows Phone], [Kindle], [Xamarin.iOS], [platformy Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[W jaki sposób klienci używają usługi Notification Hubs]: http://azure.microsoft.com/services/notification-hubs
[Przewodniki i samouczki dotyczące usługi Notification Hubs]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[uniwersalnych systemu Windows]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[platformy Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[portalu Azure]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
