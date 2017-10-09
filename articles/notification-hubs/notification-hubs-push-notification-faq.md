---
title: "Centra powiadomień Azure: Często zadawane pytania (FAQ) | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące projektowania/implementacji rozwiązań dotyczących usługi Notification Hubs"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: "powiadomienia wypychane, powiadomień wypychanych, powiadomień wypychanych systemu iOS, powiadomień wypychanych systemu android, ios push, wypychanych systemu android"
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Wypychanie powiadomień z usług Azure Notification Hubs: często zadawane pytania
## <a name="general"></a>Ogólne
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>Co to jest struktura zasobów hello centra powiadomień?

Centra powiadomień Azure ma dwa poziomy zasobu: koncentratorów i przestrzenie nazw. Koncentrator jest wypychania pojedynczego zasobu, który może zawierać informacje wypychania i platform hello jednej aplikacji. Przestrzeń nazw jest kolekcją koncentratory w jednym regionie.

Mapowanie zalecane odpowiada jednej przestrzeni nazw z jedną aplikacją. W przypadku przestrzeni nazw może mieć produkcji koncentratora, który współpracuje z aplikacjami produkcji, testowania koncentratora, który współpracuje z testowania aplikacji i tak dalej.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>Co to jest model cen hello centra powiadomień?
Witaj najnowsze szczegóły cennika znajduje się na powitania [Notification Hubs — cennik] strony. Centra powiadomień jest on rozliczany na poziomie przestrzeni nazw hello. (Aby hello definicję przestrzeni nazw, zobacz "Co to jest struktura zasobów hello centra powiadomień?") Centra powiadomień oferuje trzy warstwy:

* **Bezpłatne**: Ta warstwa jest dobry punkt wyjścia do eksploracji możliwości wypychania. Nie zaleca się w przypadku aplikacji produkcyjnej. Pobierz 500 urządzeń i 1 milion wypchnięcia uwzględnione na przestrzeni nazw na miesiąc, z żadnej gwarancji, Umowa dotycząca poziomu (SLA) usługi.
* **Podstawowe**: Ta warstwa (lub warstwy standardowa hello) jest zalecane w przypadku mniejszych aplikacji produkcyjnych. Pobierz 200 000 urządzeń i 10 milionów wypchnięcia uwzględnione na przestrzeni nazw na miesiąc, jako linii bazowej. Opcje przydziału wzrostu są uwzględniane.
* **Standardowe**: Ta warstwa jest zalecane w przypadku aplikacji produkcyjnej toolarge średnia. Możesz uzyskać 10 milionów urządzeń i 10 milionów wypchnięcia uwzględnione na przestrzeni nazw na miesiąc, jako linii bazowej. Przydział wzrost opcje i rozbudowane dane telemetryczne możliwości są uwzględniane.

Funkcje warstwy standardowa:
* **Rozbudowane informacje telemetryczne**: tootrack centra powiadomień na komunikat Telemetrii można użyć dowolnego push żądań i opinie systemu powiadomień platformy dla debugowania.
* **Obsługa wielu podmiotów**: możesz pracować z poświadczeń systemu powiadomień platformy na poziomie przestrzeni nazw. Ta opcja umożliwia tooeasily można podzielić koncentratory w hello dzierżaw tego samego obszaru nazw.
* **Zaplanowane wypychania**: można zaplanować toobe powiadomienia wysyłane w dowolnym momencie.

### <a name="what-is-hello-notification-hubs-sla"></a>Co to jest hello SLA centra powiadomień?
W warstwach Basic i Standard Notification Hubs poprawnego skonfigurowania aplikacji można wysyłać powiadomienia wypychane lub wykonywać operacje zarządzania rejestracji co najmniej 99,9% czasu hello. więcej informacji na temat umowy SLA hello, przejdź toohello toolearn [SLA centra powiadomień](https://azure.microsoft.com/support/legal/sla/notification-hubs/) strony.

> [!NOTE]
> Ponieważ powiadomienia wypychane są zależne od innych firm systemy powiadomień platformy (na przykład Apple APNS i Google FCM), nie ma żadnej gwarancji SLA, w celu dostarczania hello tych wiadomości. Po centra powiadomień wysyła partie hello systemów powiadomień tooPlatform (gwarancji SLA), jest to, że odpowiedzialność hello hello systemów powiadomień platformy toodeliver hello wypycha (nie gwarancji SLA).

### <a name="which-customers-are-using-notification-hubs"></a>Którzy użytkownicy korzystają z usługi Notification Hubs?
Wielu klientów używać usługi Notification Hubs. Poniżej przedstawiono niektóre z nich ważne:

* Sochi 2014: Setki grup zainteresowań, 3 milionów urządzeń i 150 + milionów powiadomienia wysyłane w dwóch tygodni. [Analiza przypadku: Sochi]
* Skanska: [— analiza przypadków: Skanska]
* Czas Seattle: [— analiza przypadków: razy Seattle]
* Mural.LY: [— analiza przypadków: Mural.ly]
* 7Digital: [— analiza przypadków: 7Digital]
* Aplikacje usługi Bing: Dziesiątki milionów urządzeń wysyłać powiadomienia 3 milionów na dzień.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>Jak uaktualnić lub starszą wersję mojej koncentratora lub przestrzeni nazw tooa inną warstwę?
Przejdź toohello  **[portalu Azure]** > **centra powiadomień w przestrzeni nazw** lub **usługi Notification Hubs**. Wybierz zasób hello tooupdate, a następnie przejdź zbyt**warstwy cenowej**. Należy zwrócić uwagę hello następujące wymagania:

* Hello zaktualizowano warstwę cenową stosuje zbyt*wszystkie* koncentratory w pracy z nazw hello.
* Liczba urządzeń przekracza limit hello warstwy hello, który jest powrót do subskrypcji, należy najpierw toodelete urządzeń przed można obniżyć.


## <a name="design-and-development"></a>Projektowania i opracowywania
### <a name="which-server-side-platforms-do-you-support"></a>Platformy po stronie serwera, w których są obsługiwane?
Zestawy SDK serwera są dostępne dla platformy .NET, Java, Node.js, PHP i Python. Interfejsy API centra powiadomień są oparte na interfejsy REST, więc może współpracować bezpośrednio z interfejsów API REST, jeśli używasz różnych platform lub nie chcesz, dodatkowe zależności. Aby uzyskać więcej informacji, przejdź toohello [interfejsów API REST centra powiadomień] strony.

### <a name="which-client-platforms-do-you-support"></a>Które platformy klienta są obsługiwane?
Powiadomienia wypychane są obsługiwane w przypadku [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [uniwersalnych systemu Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android Chin (za pośrednictwem usługi Baidu)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) i [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md), i [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Aby uzyskać więcej informacji, przejdź toohello [samouczków usługi Notification Hubs wprowadzenie] strony.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>Są obsługiwane wiadomości SMS, wiadomości e-mail lub powiadomienia w sieci web?
Centra powiadomień jest głównie zaprojektowane toosend powiadomienia toomobile aplikacji. Nie dostarcza adres e-mail lub tekst wiadomości możliwości. Jednak platformy innych firm, które zapewniają następujące możliwości można zintegrować z usługi Notification Hubs toosend natywnych powiadomień wypychanych powiadomienia za pomocą [Mobile Apps].

Centra powiadomień nie udostępniają usługi dostarczania powiadomień wypychanych w przeglądarce fabrycznej hello. Klientów można zaimplementować tę funkcję za pomocą SignalR na powitania obsługiwanych platform po stronie serwera. Toosend powiadomienia toobrowser aplikacji w piaskownicy Chrome hello, zobacz hello [samouczek aplikacji dla programu Chrome].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>W jaki sposób aplikacje mobilne i powiązane usługi Azure Notification Hubs i kiedy ich używać?
Jeśli masz istniejącą przenośnych zakończyć aplikację ponownie i ma tooadd tylko hello możliwości toosend powiadomień wypychanych, możesz użyć usługi Azure Notification Hubs. Jeśli chcesz tooset się Twojej aplikacji mobilnej zaplecza od początku, należy wziąć pod uwagę przy użyciu funkcji Mobile Apps hello Azure App Service. Aplikacji mobilnej automatycznie inicjuje Centrum powiadomień, dzięki czemu umożliwia łatwe wysyłanie powiadomień wypychanych z zaplecza aplikacji mobilnej hello. Cennik Mobile Apps zawiera hello opłaty podstawowej dla Centrum powiadomień. Płaci się tylko gdy przekracza hello uwzględnione wypchnięcia. Aby uzyskać więcej szczegółów kosztów Przejdź toohello [App Service — ceny] strony.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>Ile urządzeń strony I obsługuje I wysyłania powiadomień wypychanych przy użyciu usługi Notification Hubs?
Zobacz toohello [Notification Hubs — cennik] strony szczegółowe informacje na temat hello liczby obsługiwanych urządzeń.

Jeśli potrzebujesz pomocy technicznej dla zarejestrowanych urządzeń więcej niż 10 milionów [skontaktuj się z nami](https://azure.microsoft.com/overview/contact-us/) bezpośrednio, a pomożemy Ci skalować rozwiązania.

### <a name="how-many-push-notifications-can-i-send-out"></a>Jak wiele powiadomień wypychanych można wysłać?
W zależności od wybranej warstwy hello usługi Azure Notification Hubs jest automatycznie skalowany na podstawie liczby hello przepływających przez hello system powiadomienia.

> [!NOTE]
> Witaj całkowity koszt użytkowania może zwiększyć oparte na powitania liczby obsługiwanej powiadomień wypychanych. Upewnij się, że masz świadomość limity warstwy hello opisane na powitania [Notification Hubs — cennik] strony.
> 
> 

Naszym klientom używać usługi Notification Hubs toosend miliony powiadomień wypychanych codziennie. Nie masz toodo żadnych specjalnych tooscale hello zasięg powiadomień wypychanych tak długo, jak używasz usługi Azure Notification Hubs.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>Jak długo jej podjęcia dla wysyłane tooreach powiadomień wypychanych urządzenie?
W przypadku użycia normalny, gdzie hello przychodzące obciążenie jest zgodne, a nawet, usługi Azure Notification Hubs może przetworzyć co najmniej *minutę wysyła powiadomienia wypychane 1 milion*. Tego kursu mogą się różnić w zależności od hello liczbę tagów, rodzaj hello hello wysyła przychodzące i inne czynniki zewnętrzne.

Podczas hello szacowany czas dostawy usługa hello oblicza hello elementy docelowe, dla każdej platformy i kieruje toohello wiadomości, Push Notification Service (PNS) na podstawie znaczników hello zarejestrowany lub wyrażeń tagów. Jest odpowiedzialny za hello hello systemu powiadomień platformy toosend powiadomienia toohello urządzenia.

Hello systemu powiadomień platformy nie gwarantuje wszystkie umowy SLA do dostarczania powiadomień. Jednak większość powiadomienia wypychane są dostarczane tootarget urządzenia w ciągu kilku minut (zazwyczaj w ciągu 10 minut) z hello razem, gdy są one wysyłane tooNotification koncentratorów. Kilka powiadomień może zająć więcej czasu.

> [!NOTE]
> Centra powiadomień Azure ma zasady w miejscu toodrop wszystkie powiadomienia wypychane, które nie są dostarczane toohello systemu powiadomień platformy w ciągu 30 minut. To opóźnienie może się tak dziać istnieje wiele możliwych przyczyn, ale większość często, ponieważ hello systemu powiadomień platformy jest ograniczanie aplikacji.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>Istnieje już żadnych gwarancji opóźnienia?
Z powodu charakter hello powiadomień wypychanych (są dostarczane przez zewnętrznych, specyficzne dla platformy systemu powiadomień platformy) należy nie ma żadnej gwarancji opóźnienia. Zazwyczaj większość hello powiadomienia wypychane są dostarczane w ciągu kilku minut.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>Czego potrzebuję tooconsider podczas projektowania rozwiązania z koncentratorami obszary nazw i powiadomień?
#### <a name="mobile-appenvironment"></a>Środowisko/aplikacji mobilnych
* Użyj jednego centrum powiadomień dla aplikacji mobilnej na środowisko.
* W scenariuszu wielodostępnym każdy dzierżawca powinien mieć osobnego koncentratora.
* Nigdy nie udziału hello na tym samym Centrum powiadomień dla środowisk produkcyjnych i testowych. Takie rozwiązanie może spowodować problemy podczas wysyłania powiadomień. (Apple oferuje piaskownicy i produkcji Push punktów końcowych, każda z osobnych poświadczeń).
* Domyślnie można wysyłać testu powiadomienia tooyour zarejestrowanych urządzeń za pośrednictwem portalu Azure hello lub hello Azure składnika zintegrowane w programie Visual Studio. Próg Hello wartość too10 urządzeń, które są losowo dobierane spośród hello rejestracji puli.

> [!NOTE]
> Jeśli Centrum był oryginalnie skonfigurowany za pomocą certyfikatu piaskownicy firmy Apple, a następnie został ponownie skonfigurowanych toouse certyfikatu produkcyjnego firmy Apple, tokeny urządzeń oryginalnego hello są nieprawidłowe. Nieprawidłowy tokeny spowodować toofail wypchnięć. Oddzielne środowiska produkcyjnego i testowego, a przy użyciu różnych hubs dla różnych środowisk.
> 
> 

#### <a name="pns-credentials"></a>Poświadczenia systemu powiadomień platformy
Po zarejestrowaniu aplikacji mobilnej z portalu dla deweloperów platformy (na przykład firmy Apple lub Google) są wysyłane tokenów identyfikator i zabezpieczeń aplikacji. zaplecze aplikacji Hello te zapewniają systemu powiadomień platformy tokeny toohello platformy, aby powiadomienia wypychane mogą być wysyłane toodevices. Tokeny zabezpieczające może być w formie hello certyfikaty (na przykład system Apple iOS lub Windows Phone) lub kluczy zabezpieczeń (na przykład systemu Google Android lub Windows). Muszą zostać skonfigurowane w usłudze notification hubs. Konfiguracja jest zazwyczaj wykonywane na poziomie Centrum powiadomień hello, ale można także przeprowadzić na poziomie przestrzeni nazw hello w scenariuszu wielodostępnym.

#### <a name="namespaces"></a>Przestrzenie nazw
Przestrzenie nazw może służyć do grupowania wdrożenia. Mogą to być również używane toorepresent wszystkie centra powiadomień dla wszystkich dzierżawców z tej samej aplikacji w wielodostępnym scenariuszu hello.

#### <a name="geo-distribution"></a>Dystrybucja geograficzna
Geograficznie dystrybucji nie zawsze jest krytyczne w scenariuszach powiadomień wypychanych. Różne PNSes (na przykład usługi APNS lub GCM), które dostarczają toodevices powiadomienia wypychane nie są równomiernie.

Jeśli masz aplikację, która jest używana globalnie, można utworzyć koncentratory w różnych przestrzeniach nazw przy użyciu usługi Notification Hubs hello w różnych regionach platformy Azure wokół hello world.

> [!NOTE]
> Nie zaleca się to rozmieszczenie ponieważ zwiększa koszt zarządzania, szczególnie w przypadku rejestracji. Należy to zrobić tylko wtedy, gdy istnieje potrzeba jawnego.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>Zrobić rejestracje z zaplecza aplikacji hello lub bezpośrednio za pomocą klienta urządzenia?
Rejestracje z zaplecza aplikacji hello są przydatne, gdy masz tooauthenticate klientów przed utworzeniem hello rejestracji. Są one również przydatne w przypadku tagi, które zostały utworzone lub zmodyfikowane przez hello aplikacji zaplecza opartych na logice aplikacji. Aby uzyskać więcej informacji, przejdź toohello [wskazówki wewnętrznej bazy danych rejestracji] i [wskazówki wewnętrznej bazy danych rejestracji 2] stron.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Co to jest model zabezpieczeń dostarczania powiadomień wypychanych hello?
Centra powiadomień Azure używa [sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md)— na podstawie modelu zabezpieczeń. Tokeny sygnatury dostępu hello udostępnione można użyć na poziomie przestrzeni nazw głównego hello lub na poziomie koncentratora hello szczegółowe powiadomienia. Tokeny sygnatury dostępu współdzielonego może być zestaw toofollow innej reguły autoryzacji, na przykład uprawnienia wiadomości toosend toolisten uprawnienia powiadomień. Aby uzyskać więcej informacji, zobacz hello [model zabezpieczeń usługi Notification Hubs] dokumentu.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>Jak obsługiwać poufnych ładunku w powiadomieniach wypychanych?
Wszystkie powiadomienia są dostarczane urządzeń tootarget za hello platformy systemu powiadomień platformy. Jeśli powiadomienie jest wysyłane tooAzure Notification Hubs, jest przetwarzany i przekazany toohello odpowiednich systemu powiadomień platformy.

Wszystkie połączenia z hello nadawcy toohello usługi Azure Notification Hubs toohello PNS, używać protokołu HTTPS.

> [!NOTE]
> Centra powiadomień Azure nie rejestruje ładunku hello wiadomości w dowolny sposób.
> 
> 

toosend ładunki poufne, zalecamy użycie bezpiecznego Push wzorca. nadawca Hello zapewnia powiadomienie ping z urządzeniem toohello identyfikator komunikatu bez hello poufnych ładunku. Aplikacja hello na urządzeniu hello odebrania hello ładunku aplikacji hello wywołuje bezpiecznego interfejsu API bezpośrednio toofetch hello szczegóły komunikatu. Przewodnik w sposób tooimplement to wzorzec Przejdź toohello [powiadomienia Push Secure koncentratory samouczek] strony.

## <a name="operations"></a>Operacje
### <a name="what-support-is-provided-for-disaster-recovery"></a>Jakie jest obsługiwane dla odzyskiwania po awarii?
Udostępniamy pokrycia odzyskiwania po awarii metadanych po naszej stronie (nazwa usługi Notification Hubs hello, hello parametry połączenia i innych ważnych informacji). Po wyzwoleniu scenariusza odzyskiwania po awarii, dane rejestracji jest hello *tylko segment* hello centra powiadomień infrastruktury, które zostaną utracone. Te dane będą potrzebne tooimplement toorepopulate rozwiązania do nowego po odzyskiwaniu Centrum:

1. Tworzenie Centrum powiadomień dodatkowej w różnych centrach danych. Zaleca się utworzenie jednego z tooshield rozpoczęciem powitalne z zdarzenie odzyskiwania po awarii, które mogą mieć wpływ na możliwości zarządzania. Można również utworzyć w czasie hello zdarzenia odzyskiwania po awarii hello.

2. Wypełnij Centrum powiadomień dodatkowej hello hello rejestracji z Centrum powiadomień podstawowego. Nie zaleca się, próby rejestracji toomaintain na obu koncentratorów i ich synchronizowania jako rejestracji są dostępne w. Takie rozwiązanie nie działa również ze względu na powitania związanego z używaniem tendencję tooexpire rejestracji na powitania po stronie systemu powiadomień platformy. Centra powiadomień czyści je jako odbierze systemu powiadomień platformy swoją opinię na temat rejestracji wygasły lub nieprawidłowy.  

Firma Microsoft ma dwa zalecenia dla zaplecza aplikacji:

* Użyj aplikacji zaplecza przechowującą danego zestawu rejestracje jego końcem. Następnie można przeprowadzić wstawiania zbiorczego w Centrum powiadomień dodatkowej hello.

* Za pomocą wewnętrznej bazy aplikacji, która pobiera regularne zrzutu rejestracji z Centrum powiadomień głównej hello jako kopia zapasowa. Następnie można przeprowadzić wstawiania zbiorczego w Centrum powiadomień dodatkowej hello.

> [!NOTE]
> Funkcja eksportu/importu rejestracji dostępne w warstwie standardowa hello jest opisana w hello [rejestracje eksportu/importu] dokumentu.
> 
> 

Jeśli nie masz zaplecze, po uruchomieniu aplikacji hello na urządzeniach docelowych, wykonują nowej rejestracji w Centrum powiadomień dodatkowej hello. Po pewnym czasie hello Centrum powiadomień dodatkowej będzie miał hello active urządzeniom zarejestrowany.

Będą w czasie, gdy urządzenia z aplikacjami nieotwarte nie będą otrzymywać powiadomienia.

### <a name="is-there-audit-log-capability"></a>Istnieje możliwość dziennika inspekcji?
Wszystkie operacje zarządzania usługi Notification Hubs Przejdź dzienniki toooperation, które są widoczne w hello [klasycznego portalu Azure].

## <a name="monitoring-and-troubleshooting"></a>Monitorowanie i rozwiązywanie problemów
### <a name="what-troubleshooting-capabilities-are-available"></a>Jakie funkcje do rozwiązywania problemów są dostępne?
Centra powiadomień Azure zapewnia kilka funkcji rozwiązywania problemów, szczególnie w przypadku najbardziej typowym scenariuszem hello porzuconych powiadomień. Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z usługą Notification Hubs] oficjalny dokument.

### <a name="what-telemetry-features-are-available"></a>Jakie funkcje dane telemetryczne są dostępne?
Azure umożliwia usługi Notification Hubs wyświetlania danych telemetrycznych w hello [klasycznego portalu Azure]. Szczegóły metryki hello są dostępne na powitania [metryki centra powiadomień] strony.

> [!NOTE]
> Powiadomienia o pomyślnym po prostu oznacza, że powiadomienia wypychane dostarczono toohello zewnętrznego systemu powiadomień platformy (na przykład APN do firmy Apple) lub usługi GCM dla usług Google. Jest odpowiedzialny za hello hello systemu powiadomień platformy toodeliver hello powiadomienia tootarget urządzeń. Zazwyczaj hello systemu powiadomień platformy nie ujawnia dostarczania metryki toothird strony.  
> 
> 

Firma Microsoft udostępnia również dane telemetryczne hello możliwości tooexport hello programowo (w warstwie standardowa hello). Aby uzyskać więcej informacji, zobacz hello [Przykładowe metryki centra powiadomień].

[klasycznego portalu Azure]: https://manage.windowsazure.com
[Notification Hubs — cennik]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Analiza przypadku: Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Analiza przypadku: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[— Analiza przypadków: Czasy Seattle]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Analiza przypadku: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Analiza przypadku: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[interfejsów API REST centra powiadomień]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[samouczków usługi Notification Hubs wprowadzenie]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[samouczek aplikacji dla programu Chrome]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[wskazówki wewnętrznej bazy danych rejestracji]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[wskazówki wewnętrznej bazy danych rejestracji 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[model zabezpieczeń usługi Notification Hubs]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[powiadomienia Push Secure koncentratory samouczek]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[Rozwiązywanie problemów z usługą Notification Hubs]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[metryki centra powiadomień]: https://msdn.microsoft.com/library/dn458822.aspx
[Przykładowe metryki centra powiadomień]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[rejestracje eksportu/importu]: https://msdn.microsoft.com/library/dn790624.aspx
[portalu Azure]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[Mobile Apps]: https://azure.microsoft.com/services/app-service/mobile/
[App Service — ceny]: https://azure.microsoft.com/pricing/details/app-service/
