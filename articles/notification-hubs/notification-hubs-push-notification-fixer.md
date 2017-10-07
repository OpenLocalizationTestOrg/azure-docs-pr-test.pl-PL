---
title: "aaaAzure Notification Hubs — wytyczne diagnostyki"
description: "Wytyczne dotyczące sposobu toodiagnose typowe problemy związane z usługi Azure Notification Hubs."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Centra powiadomień Azure - wytyczne diagnostyki
## <a name="overview"></a>Omówienie
Jednym z często zadawane pytania hello Otrzymaliśmy od klientów usługi Azure Notification Hubs jest wygląd toofigure się, dlaczego nie widzisz powiadomienia wysyłane z ich zaplecza aplikacji na urządzeniu klienckim hello — gdy i Dlaczego usunięto powiadomień i w jaki sposób toofix to. W tym artykule firma Microsoft będzie przejście przez hello różnych powodów, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach hello. Firma Microsoft będzie wyglądać za pośrednictwem metod można analizować i ustalić przyczynę hello. 

Przede wszystkim jest toounderstand krytycznych, jak usługi Azure Notification Hubs wypycha się urządzeń toohello powiadomienia.
![][0]

Do typowych wysyłania powiadomień przepływu, wiadomość hello są wysyłane z hello **zaplecza aplikacji** za**Centrum powiadomień Azure (NH)** która z kolei działa przetwarza wszystkie rejestracji hello, biorąc pod hello konta skonfigurowane tagi & toodetermine wyrażenia tag "cele" tzn. wszystkie rejestracje hello, wymagające powiadomień wypychanych hello tooreceive. Te mogą znajdować się w całości lub części naszych obsługiwanych platform - iOS, Google, Windows, Windows Phone urządzeń Kindle i Baidu dla Chin systemu Android. Po są elementy docelowe hello NH, a następnie umieszcza powiadomień, podzielić na wiele partii rejestracji, toohello urządzenia platformy **Push Notification Service (PNS)** -np. usługi APNS do firmy Apple, usługi GCM dla Google itp. NH jest uwierzytelniany w usłudze powitalne odpowiednich systemu powiadomień platformy na podstawie hello poświadczeń ustawiona w hello klasycznego portalu Azure na stronie Konfigurowanie Centrum powiadomień hello. Hello systemu powiadomień platformy przekazuje następnie toohello powiadomienia hello odpowiednich **urządzeń klienckich**. Jest to platforma hello zalecane powiadomień wypychanych toodeliver sposób i należy pamiętać, że hello końcowej gałęzi dostarczania powiadomień o zapytaniach odbywa się między hello Platforma systemu powiadomień platformy i hello urządzenia. W związku z tym mamy czterech głównych elementów - *klienta*, *zaplecza aplikacji*, *centra powiadomień Azure (NH)* i *Push Notification Services (PNS)* i któregoś z powyższych może spowodować powiadomienia porzucane. Więcej informacji na temat tej architektury jest dostępna w [omówienie centra powiadomień].

Toodeliver awarii, może się zdarzyć powiadomienia podczas początkowej hello, że test/przemieszczania fazy, co może oznaczać problem z konfiguracją lub może się tak zdarzyć w środowisku produkcyjnym, w którym wszystkie lub niektóre z hello powiadomienia mogą być porzucane wskazujący niektórych bardziej aplikacji lub problem wzorzec do obsługi komunikatów. W sekcji hello poniżej przedstawiono różne scenariusze porzuconych powiadomień od typowych toohello rzadkich rodzaju, niektóre z nich może się okazać oczywiste i inne nie wiele. 

## <a name="azure-notifications-hub-mis-configuration"></a>Nieprawidłowa konfiguracja usługi Azure Centrum powiadomień
Centra powiadomień Azure wymaga tooauthenticate się w kontekście hello z hello Deweloper aplikacji toobe toosuccessfully stanie wysyłania powiadomień toohello odpowiednich systemu powiadomień platformy. Jest to możliwe przez dewelopera hello Tworzenie konta dewelopera z hello odpowiednich platform (Google, Apple Windows itp), a następnie rejestrując ich aplikacji, w którym znaleźć poświadczenia, które należy skonfigurować w portalu hello w obszarze powiadomień toobe Sekcja konfiguracyjna koncentratorów. Jeśli żadne powiadomienia dokonywania przez pierwsze tooensure czy hello poprawne poświadczenia są skonfigurowane w hello Centrum powiadomień dopasowywanie ich z aplikacji hello tworzenia ich koncie dewelopera określonej platformy. Znajdziesz nasze [pobierania samouczków dotyczących] przydatne toogo przez ten proces w sposób krok po kroku. Poniżej przedstawiono niektóre typowe konfiguracje niewłaściwa:

1. **Ogólne**
   
    ) upewnij się, że nazwą Centrum powiadomień (bez błędów pisowni) jest hello same:
   
   * Gdzie rejestracji od klienta hello 
   * Gdzie są wysyłanie powiadomień z zaplecza hello  
   * Jeżeli skonfigurowano hello poświadczeń systemu powiadomień platformy i 
   * Poświadczenia SAS, których skonfigurowano na hello klienta i hello wewnętrznej bazy danych. 
     
     b) upewnij się, że na powitania klienta i serwera aplikacji hello są używane hello prawidłowe ciągi konfiguracji sygnatury dostępu Współdzielonego. Jako zasadą, muszą używać hello **DefaultListenSharedAccessSignature** na powitania klienta i **DefaultFullSharedAccessSignature** hello aplikacji wewnętrznej bazy danych, (zapewniający toobe uprawnień toohello powiadomienia stanie toosend NH)
2. **Konfiguracja Notification Service (APNS, Apple Push)**
   
    Trzeba zachować dwóch różnych koncentratory — jedną w środowisku produkcyjnym i drugiego do testowania celu. Oznacza to, przekazywanie hello certyfikatów ma toouse w izolowanym środowisku tooa osobnego koncentratora oraz certyfikatów hello ma toouse w produkcji tooa osobnego koncentratora. Nie próbuj tooupload różnych typów certyfikatów toohello tym samym Centrum, ponieważ może powodować błędy powiadomień hello wiersz w dół. Jeśli okaże się, że w miejscu, gdzie przypadkowo zostały przekazane różnego rodzaju toohello certyfikatu tego samego Centrum, zalecane jest toodelete hello koncentratora i rozpocząć nową. Jeśli dla jakiegoś powodu nie Centrum hello toodelete może następnie na powitania bardzo najmniej, należy usunąć wszystkich rejestracji istniejących hello z hello koncentratora. 
3. **Konfiguracja usługi Google Cloud Messaging (GCM)** 
   
    ) upewnij się, że jest włączane "Google Cloud Messaging dla systemu Android" w obszarze projektu w chmurze. 
   
    ![][2]
   
    b) upewnij się, że podczas uzyskania poświadczeń hello NH, które będą używać tooauthenticate z usługą GCM utworzona klucz"serwera". 
   
    ![][3]
   
    c) upewnij się, że zostały skonfigurowane "Identyfikator projektu" na powitania klienta, który jest całkowicie numeryczny jednostka, którą można uzyskać z pulpitu nawigacyjnego hello:
   
    ![][1]

## <a name="application-issues"></a>Problemy z aplikacji
1) **Znaczniki / tagu wyrażenia**

Jeśli używasz znaczników lub tagu wyrażenia toosegment odbiorców, zawsze jest możliwe, że wysyłając powiadomienia hello, Brak elementu docelowego znaleziono oparte na wyrażeniach tagi/tag hello, którą określisz połączenia wysyłania. Najlepiej jest tooreview tooensure Twojego rejestracji, które są tagi które dopasowania, gdy wysyłanie powiadomień, a następnie sprawdź hello potwierdzenia tylko z klientom Witaj tych rejestracji. Na przykład Jeśli powiedzieć wszystkich rejestracji z NH zostały odbywa się za pomocą znacznika "Polityka" i wysyłania powiadomień z tagiem "Sport", jego nie będą wysyłane tooany urządzenia. Złożonych przypadkach może obejmować wyrażeń tagów, gdzie można zarejestrować tylko z "Tag A" lub "Tag B", ale podczas wysyłania powiadomienia, przeznaczonych "Tag A & & Tag B". W hello własnym diagnozowania porady poniżej, sposoby, w którym można przejrzeć rejestracji wraz z tagami hello, które mają. 

2) **Problemy dotyczące szablonu**

Jeśli są używane szablony, upewnij się, że znajdują się wytyczne hello w sposób opisany w [wskazówki szablonu]. 

3) **Nieprawidłowy rejestracji**

Zakładając, że powitalne Centrum powiadomień zostało poprawnie skonfigurowane oraz żadnych wyrażeń tagów/tag używane są poprawnie powodujące hello Znajdź prawidłową elementów docelowych toowhich hello powiadomienia wymagają toobe wysyłane, NH generowane poza partie przetwarzanie równoległe - każdej partii Wysyłanie wiadomości tooa zestawu rejestracji. 

> [!NOTE]
> Ponieważ firma Microsoft hello przetwarzanie równoległe, gwarantujemy nie hello kolejności, w których hello powiadomień są dostarczane. 
> 
> 

Centrum powiadomień Azure jest zoptymalizowane pod kątem model dostarczania komunikatu "raz w większości". Oznacza to, możemy podejmować do duplikacji, dzięki czemu powiadomienia nie są dostępne w ramach więcej niż raz tooa urządzenia. tooensure to nasz Przejrzyj hello rejestracji i upewnij się, że tylko jeden komunikat jest wysyłany na identyfikator urządzenia przed faktycznie wysyłania toohello wiadomość hello systemu powiadomień platformy. Każdej z partii jest wysyłany toohello systemu powiadomień platformy, które z kolei akceptuje i sprawdzanie poprawności rejestracji hello, jest to możliwe, że hello systemu powiadomień platformy wykryje błąd co najmniej jednym hello rejestracji w partii, zwraca błąd tooAzure NH i zatrzymuje przetwarzanie co który porzucenie całkowicie partii. Jest to szczególnie ważne przy użyciu usługi APNS, który używa protokołu strumienia TCP. Mimo że firma Microsoft są zoptymalizowane pod kątem w większości raz dostarczania, w tym przypadku usuwamy hello źle działający rejestrację z naszych danych, a następnie ponów próbę dostarczania powiadomień o zapytaniach pozostałej hello hello urządzeń w danej partii.

Można uzyskać informacji o błędzie hello próbę dostarczenie nie powiodło się dla rejestracji przy użyciu interfejsów API usługi Azure Notification Hubs REST hello: [na Telemetrii wiadomości: pobrać Telemetrii komunikat powiadomienia](https://msdn.microsoft.com/library/azure/mt608135.aspx) i [opinii systemu powiadomień platformy](https://msdn.microsoft.com/library/azure/mt705560.aspx). Zobacz hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) na przykład kodu.

## <a name="pns-issues"></a>Problemy z systemem powiadomień platformy
Po otrzymaniu komunikatu powiadomienia hello przez hello odpowiednich systemu powiadomień platformy, a następnie jego odpowiedzialność toodeliver hello powiadomień toohello urządzenia. Centra powiadomień Azure jest poza obraz powitania w tym miejscu i nie ma kontroli gdy lub jeśli hello powiadomień będzie toobe dostarczyć toohello urządzenia. Ponieważ usług powiadomień platformy hello są bardzo rozbudowane, powiadomienia zwykle z hello systemu powiadomień platformy urządzeń hello tooreach w ciągu kilku sekund. Jeżeli hello systemu powiadomień platformy jednak jest ograniczanie usługi Azure Notification Hubs zastosowanie wykładniczego wycofywania strategii i jeśli hello systemu powiadomień platformy pozostaje nieosiągalny na 30 minut następnie mamy zasad w umieścić tooexpire i trwale usunąć te wiadomości. 

Jeśli system powiadomień platformy próby toodeliver powiadomienie, ale hello urządzenie jest w trybie offline, powiadomienia hello jest przechowywane przez hello systemu powiadomień platformy przez pewien czas i dostarczyć urządzeniu toohello po ich udostępnieniu. Znajduje się tylko jedno powiadomienie ostatnie dla danej aplikacji. Jeśli wiele powiadomienia są wysyłane, gdy urządzenie hello jest w trybie offline, każde nowe powiadomienie powoduje, że wcześniejszego powiadomienia hello toobe odrzucone. To zachowanie zachowania tylko hello najnowszych powiadomień jest określony tooas odbioru powiadomienia w APNS i zwijanie w GCM (który używa klucza się). Jeśli urządzenie hello pozostanie w trybie offline przez dłuższy czas, powiadomienia są przechowywane dla niego zostaną odrzucone. Source — [wskazówki APNS] & [wskazówki dotyczące usługi GCM]

Przy użyciu usługi Azure Notification Hubs — można przekazać klucza łączącego za pośrednictwem nagłówka HTTP przy użyciu zwykłego hello `SendNotification` interfejsu API (np. dla zestawu .NET SDK — `SendNotificationAsync`) używającą nagłówków HTTP, które są przekazywane jako jest toohello odpowiednich systemu powiadomień platformy. 

## <a name="self-diagnose-tips"></a>Etykietki zdiagnozowania własnym
W tym miejscu zostaną omówione hello różnych toodiagnose możliwości ataku i głównego spowodować problemy Centrum powiadomień:

### <a name="verify-credentials"></a>Weryfikowanie poświadczeń
1. **Portalu dla deweloperów systemu powiadomień platformy**
   
    Sprawdź je na powitania odpowiednich systemu powiadomień platformy developer portal (APN, GCM, itp. WNS) przy użyciu naszych [pobierania samouczków dotyczących].
2. **Klasyczny portal Azure**
   
    Przejdź tooreview kartę Konfiguracja toohello i być zgodne z poświadczeniami hello z identyfikatorami uzyskanymi z portalu dla deweloperów systemu powiadomień platformy hello. 
   
    ![][4]

### <a name="verify-registrations"></a>Weryfikowanie rejestracji
1. **Program Visual Studio**
   
    Jeśli używasz programu Visual Studio do tworzenia aplikacji można połączyć tooMicrosoft Azure i widoku i zarządzać grupy usług Azure, w tym Centrum powiadomień "Eksploratora serwera". Jest to szczególnie przydatne w przypadku środowiska i testowania. 
   
    ![][9]
   
    Można wyświetlać i zarządzać nimi wszystkich rejestracji hello w Centrum, które dobrze są podzielone dla rejestracji platformy, native lub szablonu, tagi, identyfikator systemu powiadomień platformy, Data wygaśnięcia identyfikator i hello rejestracji. Można również edytować rejestracji na bieżąco hello — co przydaje się, że, jeśli chcesz, tooedit dowolne tagi. 
   
    ![][8]
   
   > [!NOTE]
   > Rejestracje tooedit funkcje programu Visual Studio należy używać tylko podczas tworzenia/testowania, z ograniczoną liczbę rejestracji. Jeśli wystąpi toofix potrzeby rejestracji w trybie zbiorczym, należy wziąć pod uwagę przy użyciu funkcji rejestracji eksportu/importu hello opisanych tutaj — [rejestracje eksportu/importu](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Eksplorator usługi Service Bus**
   
    Wielu klientów używa magistrali usług explorer opisane tutaj — [Explorer magistrali usług] umożliwiające wyświetlanie i zarządzanie ich Centrum powiadomień. Jest dostępna z code.microsoft.com - projekt typu open source [kodu Explorer magistrali usług]

### <a name="verify-message-notifications"></a>Sprawdź komunikat powiadomienia
1. **Klasyczny portal Azure**
   
    Możesz toohello "Debugowanie" kartę toosend testu powiadomienia tooyour klientów bez konieczności dowolnego zaplecza usługi zapasowej i uruchamiania. 
   
    ![][7]
2. **Program Visual Studio**
   
    Można również wysłać powiadomienia testowe z comforts hello programu Visual Studio:
   
    ![][10]
   
    Możesz przeczytać więcej na hello Azure Centrum powiadomień programu Visual Studio explorer funkcji tutaj — 
   
   * [Omówienie Eksploratora serwera VS]
   * [Post na blogu Eksploratora serwera VS - 1]
   * [Post na blogu Eksploratora serwera VS - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Debugowanie nie powiodło się powiadomienia / Przejrzyj wyniku powiadomienia
**Właściwość EnableTestSend**

W przypadku wysyłania powiadomień przy użyciu usługi Notification Hubs początkowo ją po prostu pobiera umieszczone w kolejce dla toodo NH przetwarzania toofigure się wszystkie elementy docelowe i następnie ostatecznie NH wysyła go toohello systemu powiadomień platformy. Oznacza to, że używając interfejsu API REST lub dowolnym powitania klienta SDK, hello pomyślne powrotu z wysyłania wywołania tylko oznacza, że wiadomość hello ma zostały pomyślnie umieszczone w kolejce z Centrum powiadomień. Go nie zapewnia wgląd co się stało, gdy NH ostatecznie otrzymano tooPNS wiadomość hello toosend. Jeśli powiadomienia nie jest otrzymywanych powitania klienta urządzenia, istnieje możliwość, że gdy NH nastąpiła tooPNS wiadomość hello toodeliver, wystąpił błąd np. rozmiar ładunku hello przekroczył hello maksymalna wartość dozwolona przez hello systemu powiadomień platformy lub są skonfigurowane w NH poświadczenia hello Nieprawidłowy itp. tooget jako analizę błędów systemu powiadomień platformy hello, zostały wprowadzone właściwość o nazwie [EnableTestSend funkcji]. Ta właściwość jest włączane automatycznie, podczas wysyłania test komunikaty z portalu hello lub klienta programu Visual Studio i w związku z tym umożliwia toosee szczegółowe informacje o debugowaniu. Służy to za pośrednictwem interfejsów API, biorąc hello przykład hello zestawu .NET SDK, gdy są one dostępne teraz i zostanie dodany tooall zestawy SDK klientów po pewnym czasie. toouse to wywołania REST hello, po prostu Dołącz parametr querystring o nazwie "test" na końcu hello wywołania wysyłania np. 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Przykład (.NET SDK)*

Załóżmy, że używasz toosend zestawu SDK programu .NET native wyskakujące powiadomienie:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`będzie po prostu stanu `Enqueued` na końcu hello hello wykonywania bez żadnych wgląd w co się stało tooyour wypychania. Teraz można używać hello `EnableTestSend` właściwości typu boolean podczas inicjowania hello `NotificationHubClient` i uzyskać szczegółowe informacje o hello systemu powiadomień platformy napotkano błędy podczas wysyłania powiadomienia hello. Hello wysyłania tutaj wywołania potrwa tooreturn dodatkowy czas, ponieważ jest to zwracanie tylko po NH wydał hello powiadomień tooPNS toodetermine hello wyniku. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Przykładowe dane wyjściowe*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Ten komunikat oznacza nieprawidłowe poświadczenia są konfigurowane w Centrum powiadomień hello albo wystąpił problem z rejestracji hello na powitania koncentratora i hello zalecane przebiegu może być toodelete tej rejestracji i umożliwić powitania klienta, utwórz go ponownie przed wysłaniem hello Komunikat. 

> [!NOTE]
> Warto zauważyć, że hello użycie tej właściwości jest silnie ograniczany tak tylko w należy użyć tego środowiska i testowania ograniczonym zestawie rejestracji. Tylko wyślemy powiadomienia debugowania too10 urządzeń. Istnieje również limit przetwarzania debugowania wysyła toobe 10 na minutę. 
> 
> 

### <a name="review-telemetry"></a>Przejrzyj telemetrii
1. **Użyj klasycznego portalu Azure**
   
    Witaj portal umożliwia tooget szybki przegląd wszystkich działań hello w Centrum powiadomień. 
   
    ) na karcie "pulpitu nawigacyjnego" hello, można wyświetlić zagregowany widok hello rejestracji, powiadomienia, a także błędów dla każdej platformy. 
   
    ![][5]
   
    (b) można także dodać wiele innych platform określonych metryk z tootake kartę "Monitora" hello głębiej przyjrzeć się szczególnie systemu powiadomień platformy konkretne błędy zwracane, gdy NH próbuje toosend hello powiadomień toohello systemu powiadomień platformy. 
   
    ![][6]
   
    c) należy rozpocząć od sprawdzenia hello **wiadomości przychodzących**, **operacji rejestracji**, **powiadomienia o pomyślnym** , a następnie przejść tooper platformy kartę tooreview hello Określone błędy systemu powiadomień platformy. 
   
    d) Jeśli masz powiadomień hello Centrum niepoprawnie skonfigurowany z ustawieniami uwierzytelniania hello następnie użytkownik zostanie wyświetlony błąd uwierzytelniania systemu powiadomień platformy. To wskazuje toocheck hello systemu powiadomień platformy poświadczeń. 

2) **Programowy dostęp**

W tym miejscu — więcej informacji 

* [Dostęp programistyczny Telemetrii]
* [Dane telemetryczne dostęp za pośrednictwem interfejsów API próbki] 

> [!NOTE]
> Kilka związane z funkcje, takie jak **rejestracje eksportu/importu**, **Telemetrii dostęp za pośrednictwem interfejsów API** itp są dostępne tylko w warstwie standardowa. Jeśli próba toouse tych funkcji, jeśli jest bezpłatna lub warstwy podstawowa następnie możesz otrzyma efekt toothis komunikat wyjątku podczas używania hello zestawu SDK i HTTP 403 (Dostęp zabroniony), korzystając z nimi bezpośrednio z hello interfejsów API REST. Upewnij się, że zostały przeniesione zapasowej warstwy tooStandard za pośrednictwem klasycznego portalu Azure.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[omówienie centra powiadomień]: notification-hubs-push-notification-overview.md (Notification Hubs — omówienie)
[pobierania samouczków dotyczących]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[wskazówki szablonu]: https://msdn.microsoft.com/library/dn530748.aspx 
[wskazówki APNS]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[wskazówki dotyczące usługi GCM]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[Explorer magistrali usług]: http://msdn.microsoft.com/library/dn530751.aspx
[kodu Explorer magistrali usług]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Omówienie Eksploratora serwera VS]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[Post na blogu Eksploratora serwera VS - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[Post na blogu Eksploratora serwera VS - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend funkcji]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Dostęp programistyczny Telemetrii]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Dane telemetryczne dostęp za pośrednictwem interfejsów API próbki]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

