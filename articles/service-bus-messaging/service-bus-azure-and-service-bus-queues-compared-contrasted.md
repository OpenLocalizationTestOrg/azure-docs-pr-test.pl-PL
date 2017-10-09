---
title: "aaaAzure magazynu kolejek i kolejek usługi Service Bus - porównywane i odróżniające | Dokumentacja firmy Microsoft"
description: "Analizuje różnice i podobieństwa między dwoma typami kolejek oferowanych na platformie Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Magazyn kolejek i kolejek usługi Service Bus - porównywane i odróżniające
W tym artykule analizuje hello różnice i podobieństwa między hello dwa typy kolejek oferowanych przez system Microsoft Azure obecnie: magazyn kolejek i kolejek usługi Service Bus. Za pomocą tych informacji, można porównać i kontrastu hello odpowiednich technologii i być może toomake więcej świadomej decyzji o które rozwiązanie najlepiej odpowiada Twoim potrzebom.

## <a name="introduction"></a>Wprowadzenie
Azure obsługuje dwa typy mechanizmów kolejki: **magazynu kolejek** i **kolejek usługi Service Bus**.

**Magazyn kolejek**, które są częścią hello [magazynu Azure](https://azure.microsoft.com/services/storage/) infrastruktury, funkcja prostego interfejsu opartego na interfejsie REST GET/PUT/PEEK, zapewniając niezawodne, trwałe wiadomości w obrębie i między usługami.

**Kolejki usługi Service Bus** są częścią szerszego [Azure messaging](https://azure.microsoft.com/services/service-bus/) infrastruktury obsługuje kolejkowania wiadomości oraz publikowania/subskrypcji i bardziej zaawansowane wzorce integracji. Aby uzyskać więcej informacji na temat usługi Service Bus kolejek/tematy/subskrypcji, zobacz hello [Omówienie usługi Service Bus](service-bus-messaging-overview.md).

Istnieją obie Kolejkowanie technologie współbieżnie, kolejek magazynu zostały wprowadzone najpierw mechanizmu magazynowania dedykowanych kolejki, oparty na usługach Azure Storage. Kolejki usługi Service Bus są wbudowane hello szerszych "wiadomości" przeznaczony infrastruktury toointegrate aplikacji lub składników aplikacji, które może obejmować wiele protokołów komunikacyjnych, kontraktów danych, zaufania domen lub w środowiskach sieci.

## <a name="technology-selection-considerations"></a>Zagadnienia dotyczące wyboru technologii
Kolejki magazynu i kolejek usługi Service Bus są implementacji usługi dostępne w systemie Microsoft Azure kolejkowania wiadomości powitania. Każdy ma zestaw nieco innych funkcji, co oznacza, wybierz jedną lub innych hello lub korzystać z obu w zależności od potrzeb hello konkretnego rozwiązania lub są rozwiązywania problemu firm/techniczne.

Podczas określania Kolejkowanie technologie pasuje do celu powitania dla danego rozwiązania, rozwiązanie architektów i deweloperów należy rozważyć poniższe zalecenia hello. Aby uzyskać więcej informacji zobacz hello następnej sekcji.

Jako rozwiązanie architektów/deweloperów **należy rozważyć użycie magazynu kolejek** po:

* Aplikacja ponad 80 GB wiadomości muszą być przechowywane w kolejce, w której wiadomości powitania mają okres istnienia krótszy niż 7 dni.
* Aplikacja potrzebuje tootrack postępu dla przetwarzania komunikatu w kolejce hello. Jest to przydatne w przypadku awarii procesu roboczego hello przetwarzania komunikatu. Kolejne pracownik może następnie użyć tego toocontinue informacje, z którym przerwał hello poprzedniego procesu roboczego.
* Wymagane jest dzienników po stronie serwera wszystkich transakcji hello wykonywane z kolejki.

Jako rozwiązanie architektów/deweloperów **należy rozważyć użycie kolejek usługi Service Bus** po:

* Rozwiązania musi być komunikaty o stanie tooreceive bez konieczności toopoll hello kolejki. Z usługą Service Bus, można to osiągnąć poprzez hello Użyj hello long sondowania odbierania operację przy użyciu hello TCP protokołów opartych na obsługiwanych przez usługę Service Bus.
* Rozwiązanie wymaga tooprovide kolejki hello gwarantowane pierwszy — w pierwszej — ruch wychodzący dostarczania uporządkowanego (FIFO).
* Ma symetrycznego środowisko na platformie Azure i w systemie Windows Server (Chmura prywatna). Aby uzyskać więcej informacji, zobacz [Usługa Service Bus dla systemu Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* Rozwiązania musi być możliwe toosupport automatycznego wykrywania duplikatów.
* Chcesz, aby wiadomości tooprocess aplikacji jako równoległych strumieni długotrwałe (komunikaty są skojarzone z strumień, używając hello [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) właściwości wiadomości powitania). W tym modelu każdy węzeł w korzystanie z aplikacji hello konkuruje dla strumieni, jako min. toomessages. Gdy strumień jest tooa korzystanie z węzła, węzeł hello można sprawdzić stan hello stan strumienia aplikacji hello przy użyciu transakcji.
* Rozwiązanie wymaga zachowanie transakcyjnego i niepodzielność przy wysyłaniu lub odbieraniu wiele komunikatów z kolejki.
* Witaj time to live (TTL) charakterystyczne dla obciążenia specyficzne dla aplikacji hello może przekroczyć hello 7-dniowego okresu.
* Aplikacji obsługi wiadomości, które może być dłuższa niż 64 KB, ale będzie prawdopodobnie nie podejście hello 256 KB limit.
* Praca z tooprovide wymaganie toohello modelu dostępu opartej na rolach kolejki oraz różne prawa/uprawnienia do nadawcy i odbiorcy.
* Rozmiar kolejki nie będzie rosnąć większa niż 80 GB.
* Ma toouse hello protokołu AMQP 1.0 opartych na standardach obsługi wiadomości protokołu. Aby uzyskać więcej informacji na temat protokołu AMQP, zobacz [Omówienie protokołu AMQP magistrali usługi](service-bus-amqp-overview.md).
* Mogą traktować ewentualnej migracji z kolejki na podstawie point-to-point komunikacji tooa wymiany komunikatów, który umożliwia bezproblemową integrację odbiorcy dodatkowego (subskrybentów), z których każdy otrzymuje niezależne kopie niektórych lub wszystkich Komunikaty wysyłane toohello kolejki. ostatnie Hello odwołuje się możliwości publikowania/subskrypcji toohello natywnie udostępniane przez usługi Service Bus.
* Rozwiązanie do obsługi komunikatów muszą być stanie toosupport hello "większość-jednocześnie" dostarczania gwarancji bez hello trzeba toobuild hello infrastruktury dodatkowe składniki.
* Chcesz toopublish stanie toobe i zużywać partie wiadomości.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Porównanie magazynu kolejek i kolejek usługi Service Bus
tabele Hello w hello następujące sekcje umożliwiają logiczne grupowanie funkcji kolejki i pozwalają porównać jeden rzut oka, hello funkcji dostępnych w kolejki magazynu i kolejek usługi Service Bus.

## <a name="foundational-capabilities"></a>Podstawowych możliwości
Ta sekcja porównuje niektóre hello podstawowych kolejkowania możliwości magazynu kolejek i kolejek usługi Service Bus.

| Kryteria porównania | Magazyn kolejek | Kolejki usługi Service Bus |
| --- | --- | --- |
| Porządkowanie gwarancji |**Nie** <br/><br>Aby uzyskać więcej informacji zobacz hello pierwszą notatkę hello sekcja "Informacje dodatkowe".</br> |**Tak — pierwszy w pierwszym Out (FIFO)**<br/><br>(przy użyciu hello wiadomości sesji) |
| Gwarancji dostarczenia |**W najmniej jednokrotne** |**W najmniej jednokrotne**<br/><br/>**Większość jednocześnie** |
| Obsługa niepodzielną operację |**Nie** |**Tak**<br/><br/> |
| Działanie odbierania |**Blokowanie inne niż**<br/><br/>(zakończeniu natychmiast przypadku nieznalezienia nie nowej wiadomości) |**Blokowanie z lub bez limitu czasu**<br/><br/>(udostępnia długo sondowania lub hello ["Kometa techniki"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Blokowanie inne niż**<br/><br/>(za pośrednictwem hello Użyj programu .NET zarządzanego interfejsu API tylko) |
| Styl wypychania interfejsu API |**Nie** |**Tak**<br/><br/>[OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) i **OnMessage** sesji interfejsu API platformy .NET. |
| Tryb odbierania |**Peek & dzierżawy** |**Peek & blokady**<br/><br/>**Usuń & Odbierz** |
| Tryb wyłączności |**Na podstawie dzierżawy** |**Na podstawie blokady** |
| Czas trwania dzierżawy/blokady |**30 sekund (ustawienie domyślne)**<br/><br/>**7 dni (maksymalnie)** (możesz odnowić lub zwolnienia dzierżawy wiadomości przy użyciu hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) interfejsu API.) |**60 sekund (ustawienie domyślne)**<br/><br/>Możesz odnowić blokady wiadomości przy użyciu hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) interfejsu API. |
| / Blokady dokładności |**Poziom komunikatu**<br/><br/>(każdy komunikat może mieć wartości różnych limitu czasu, który można zaktualizować zgodnie z potrzebami podczas przetwarzania wiadomości powitania przy użyciu hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) interfejsu API) |**Poziom kolejki**<br/><br/>(każdej kolejki ma tooall dokładności stosowane blokady, jego wiadomości, ale mogą odnowić blokady hello przy użyciu hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) interfejsu API.) |
| Umieścić w zadaniu wsadowym odbierania |**Tak**<br/><br/>(jawne określenie liczby komunikatów podczas pobierania wiadomości w górę tooa maksymalnie 32 wiadomości) |**Tak**<br/><br/>(niejawnie włączając właściwość pobierania wstępnego lub jawnie używać za pośrednictwem hello transakcji) |
| Wyślij wsadów |**Nie** |**Tak**<br/><br/>(przy użyciu hello transakcji lub przetwarzanie wsadowe po stronie klienta) |

### <a name="additional-information"></a>Dodatkowe informacje
* Komunikaty w kolejkach magazynu są zwykle pierwszy — w pierwszej — ruch wychodzący, ale czasami może być uszkodzony; na przykład komunikat widoczność limitu czasu wygaśnięcia (na przykład w wyniku awarii podczas przetwarzania aplikacji klienckiej). Po upływie limitu czasu widoczności hello wiadomość hello staje się widoczna ponownie dla kolejki hello innego procesu roboczego toodequeue go. W tym momencie nowo widoczne wiadomość hello mogą być umieszczane w kolejce hello (toobe usuniętej ponownie) po komunikat, który został pierwotnie umieszczonych w kolejce po nim.
* Witaj gwarantowane FIFO wzorzec kolejek usługi Service Bus wymaga użycia hello sesji komunikacji. W hello zdarzenie, które aplikacji hello ulega awarii podczas przetwarzania komunikatów otrzymanych w hello **wgląd & Zablokuj** tryb, hello następnym odbiornika kolejki akceptuje sesji obsługi wiadomości, zostanie ona rozpoczęta z niepowodzeniem wiadomości powitania po jego okres czasu wygaśnięcia (TTL) wygaśnie.
* Magazyn kolejek są zaprojektowane toosupport standardowe kolejkowania scenariusze, takie jak oddzielenie skalowalności tooincrease składniki aplikacji i tolerancję błędów, obciążenia wyrównywanie i przepływy pracy procesu kompilacji.
* Kolejki usługi Service Bus obsługują hello *na najmniej jednokrotne* gwarancji dostarczenia. Ponadto hello *większość-jednocześnie* semantycznego może być obsługiwany przy użyciu stan aplikacji hello toostore stanu sesji przy użyciu transakcji tooatomically odbierania komunikatów i zaktualizować hello stanu sesji.
* Magazyn kolejek udostępnianie uniform i spójny model programowania w kolejek, tabel i obiektów blob — zarówno dla deweloperów i zespołów operacyjnych.
* Kolejki usługi Service Bus zapewniają obsługę transakcji lokalnych w kontekście hello pojedynczej kolejki.
* Witaj **odbieranie i usuwanie** tryb obsługiwany przez usługi Service Bus udostępnia hello tooreduce możliwości hello liczbę operacji (i skojarzone koszt) do obsługi komunikatów zamian gwarancji dostarczenia obniżony.
* Magazyn kolejek udostępnianie dzierżaw z hello możliwości tooextend hello dzierżawy dla wiadomości. Pracowników hello dzięki temu toomaintain krótkich dzierżawy na komunikaty. W związku z tym jeśli pracownik ulegnie awarii, wiadomość hello mogą być szybko przetwarzane ponownie przez inny proces roboczy. Ponadto pracownika można rozszerzyć dzierżawę wiadomość hello wymaga tooprocess raczej dzierżawienie dłuższy niż hello bieżącego czasu.
* Magazyn kolejek oferują widoczność przekroczenie limitu czasu można ustawić podczas umieszczania hello lub usuwania komunikatów. Ponadto można zaktualizować komunikat o wartości innej dzierżawy w czasie wykonywania, a aktualizacja różne wartości w wiadomości powitania takie same kolejki. Limity czasu blokady usługi Service Bus są zdefiniowane w metadanych kolejki hello; Jednak możesz odnowić blokady hello przez wywołanie hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) metody.
* Hello maksymalny limit czasu operacji blokowania odbioru w kolejek usługi Service Bus jest 24 dni. Jednak opartego na interfejsie REST limitów czasu mieć maksymalną wartość 55 sekund.
* Przetwarzanie wsadowe po stronie klienta udostępniane przez usługi Service Bus umożliwia toobatch klienta kolejki wiele komunikatów do operacji wysyłania pojedynczego. Tworzenie plików wsadowych jest dostępna tylko dla operacji asynchronicznego wysyłania.
* Funkcje, takie jak hello 200 TB limitu kolejki magazynu (więcej podczas wirtualizacji kont) i nieograniczoną liczbę kolejek był idealną platformą dla dostawców w modelu SaaS.
* Magazyn kolejek zapewniają elastyczne i wydajności delegowane mechanizmu kontroli dostępu.

## <a name="advanced-capabilities"></a>Funkcje zaawansowane
Ta sekcja porównuje zaawansowane możliwości oferowane przez wersję magazynu kolejek i kolejek usługi Service Bus.

| Kryteria porównania | Magazyn kolejek | Kolejki usługi Service Bus |
| --- | --- | --- |
| Dostarczania zaplanowanych |**Tak** |**Tak** |
| Automatyczne martwy litery |**Nie** |**Tak** |
| Zwiększenie wartości time-to-live kolejki |**Tak**<br/><br/>(za pomocą aktualizacji w miejscu limitu czasu widoczności) |**Tak**<br/><br/>(udostępnione za pośrednictwem dedykowanej funkcja interfejsu API) |
| Obsługa komunikatów zanieczyszczonych |**Tak** |**Tak** |
| Aktualizacja w miejscu |**Tak** |**Tak** |
| Dziennik transakcji po stronie serwera |**Tak** |**Nie** |
| Metryki magazynu |**Tak**<br/><br/>**Minuty metryki**: zapewnia metryk w czasie rzeczywistym dla interfejsu API dostępności, TPS, wywołaj liczby, liczby błędów i więcej, w czasie rzeczywistym (zagregowane na minutę i zgłaszanych w ciągu kilku minut od naturę tylko w środowisku produkcyjnym. Aby uzyskać więcej informacji, zobacz [o metryki analityka magazynu](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Tak**<br/><br/>(zbiorcze zapytań przez wywołanie metody [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Stan zarządzania |**Nie** |**Tak**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Automatyczne przekazywanie komunikatów |**Nie** |**Tak** |
| Przeczyścić kolejki — funkcja |**Tak** |**Nie** |
| Komunikat grup |**Nie** |**Tak**<br/><br/>(przy użyciu hello wiadomości sesji) |
| Stan aplikacji dla każdej grupy wiadomości |**Nie** |**Tak** |
| Wykrywanie duplikatów |**Nie** |**Tak**<br/><br/>(można konfigurować na stronie nadawcy hello) |
| Przeglądanie grup wiadomości |**Nie** |**Tak** |
| Pobieranie wiadomości sesje według Identyfikatora |**Nie** |**Tak** |

### <a name="additional-information"></a>Dodatkowe informacje
* Obie Kolejkowanie technologie Włącz toobe wiadomości, zaplanowane w celu dostarczania w późniejszym czasie.
* Automatyczne przekazywanie kolejki umożliwia tysiące kolejek wiadomości powitania zużywa ich wiadomości tooa pojedynczej kolejki, z których aplikacja odbierająca hello na następny tooauto. Służy to mechanizm tooachieve zabezpieczeń, przepływ sterowania i odizolowanego magazynu między każdy wydawca wiadomości.
* Magazyn kolejek zapewnia obsługę aktualizowanie zawartości wiadomości. Tej funkcji można używać dla trwałych informacje o stanie i aktualizacje przyrostowe postępu na wiadomość powitania dzięki czemu mogą być przetwarzane z hello ostatniego znanego punktu kontrolnego, zamiast od podstaw. W przypadku kolejek usługi Service Bus, można włączyć hello sytuacji przy użyciu sesji wiadomość hello. Sesje pozwalają toosave i pobrać stan przetwarzania aplikacji hello (przy użyciu [metoda SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) i [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Martwych drukiem](service-bus-dead-letter-queues.md), który jest obsługiwany tylko przez kolejek usługi Service Bus, może być przydatna do izolowania wiadomości, które nie może pomyślnie przetworzone przez aplikację odbierającą hello lub gdy wiadomości nie docierają do miejsca docelowego, które powinny przejść tooan wygasł Właściwość Time to live (TTL). wartość TTL Hello Określa, jak długo pozostaje wiadomości w kolejce hello. Z usługą Service Bus wiadomość hello będzie przeniesionego tooa kolejki specjalne o nazwie $DeadLetterQueue, po wygaśnięciu okresu TTL hello.
* toofind "" wiadomości we wszystkich kolejkach magazynu, podczas usuwania aplikacji hello komunikat sprawdza hello  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  właściwości wiadomości powitania. Jeśli **DequeueCount** jest większy niż podany próg aplikacji hello przenosi hello komunikat tooan zdefiniowanym przez aplikację "kolejki utraconych wiadomości".
* Magazyn kolejek Włącz tooobtain szczegółowy dziennik wszystkich transakcji hello wykonane na powitania kolejki, a także zagregowane metryki. Obie te opcje są przydatne w przypadku debugowania i zrozumienie, jak aplikacja korzysta z magazynu kolejek. Są one również przydatne w przypadku aplikacji dostrajanie wydajności i zmniejszenie kosztów hello korzystanie z kolejek.
* Hello pojęcie "sesje komunikat" obsługiwane przez usługi Service Bus umożliwia komunikatów, które należy tooa niektórych toobe grupy logiczne skojarzone z danym odbiornik, który z kolei tworzy koligację przypominającej sesji, między wiadomości i ich odpowiednich odbiorców. Możesz je włączyć, zaawansowanych funkcji w usłudze Service Bus przez ustawienie hello [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) właściwości wiadomości. Odbiorcy mogą następnie nasłuchiwanie na identyfikatorze określonej sesji i odbierania wiadomości, mających hello określony identyfikator sesji.
* Witaj funkcji wykrywania duplikatów obsługiwane przez kolejek usługi Service Bus automatycznie usuwa zduplikowane wiadomości wysłane tooa kolejka lub temat, na podstawie wartości hello hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) właściwości.

## <a name="capacity-and-quotas"></a>Pojemności i przydziałów
Ta sekcja porównuje magazynu kolejek i kolejek usługi Service Bus z punktu widzenia hello [pojemności i przydziałów](service-bus-quotas.md) , mogą być stosowane.

| Kryteria porównania | Magazyn kolejek | Kolejki usługi Service Bus |
| --- | --- | --- |
| Maksymalny rozmiar kolejki |**500 TB.**<br/><br/>(ograniczone tooa [pojemności konta magazynu z jednym](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(zdefiniowane podczas tworzenia kolejki i [włączenie partycjonowania](service-bus-partitioning.md) — zobacz sekcja "Informacje dodatkowe" hello) |
| Maksymalny rozmiar wiadomości |**64 KB**<br/><br/>(48 KB, korzystając z **Base64** kodowanie)<br/><br/>Azure obsługuje dużych wiadomości, łącząc kolejek i obiektów blob — w takim przypadku można umieścić w kolejce zapasowej too200GB dla pojedynczego elementu. |**256 KB** lub **1 MB**<br/><br/>(w tym zarówno nagłówek i treść, rozmiar maksymalny nagłówka: 64 KB).<br/><br/>Zależy od hello [warstwy usług](service-bus-premium-messaging.md). |
| Maksymalny czas wygaśnięcia wiadomości. |**7 dni** |**`TimeSpan.Max`** |
| Maksymalna liczba kolejek |**Unlimited (nieograniczony)** |**10,000**<br/><br/>(na przestrzeni nazw, można zwiększyć) |
| Maksymalna liczba jednoczesnych klientów |**Unlimited (nieograniczony)** |**Unlimited (nieograniczony)**<br/><br/>(100 limit równoczesnych połączeń dotyczy tylko komunikacja oparta na protokole tooTCP) |

### <a name="additional-information"></a>Dodatkowe informacje
* Magistrala usług wymusza limity rozmiaru kolejki. Witaj maksymalny rozmiar kolejki jest określany podczas tworzenia kolejki hello i może mieć wartość z zakresu od 1 do 80 GB. Po osiągnięciu wartości rozmiar kolejki hello ustawionej tworzenia kolejki hello dodatkowych komunikatów przychodzących zostanie odrzucone i wyjątek zostanie odebrana przez hello wywołanie kodu. Aby uzyskać więcej informacji na temat przydziały w usłudze Service Bus, zobacz [przydziały magistrali usługi](service-bus-quotas.md).
* W hello [warstwy standardowa](service-bus-premium-messaging.md), można utworzyć kolejki usługi Service Bus w rozmiarze 1, 2, 3, 4 lub 5 GB (domyślnie hello jest 1 GB). W warstwie Premium hello można utworzyć kolejki się rozmiar too80 GB. W standardzie warstwy z partycjonowania włączone (który jest domyślnym hello), usługi Service Bus tworzy 16 partycji dla każdego Gigabajta określisz. Tak, można utworzyć kolejkę o rozmiarze 5 GB, z 16 partycji hello maksymalny rozmiar kolejki staje się (5 * 16) = 80 GB. Widać hello maksymalny rozmiar kolejki podzielonym na partycje lub tematu, analizując jego wpis na powitania [portalu Azure][Azure portal]. W warstwie Premium hello tylko 2 partycjach są tworzone dla kolejki.
* W przypadku magazynu kolejek, jeśli hello treść wiadomości powitania nie jest bezpieczne XML, a następnie musi być **Base64** zakodowany. Jeśli użytkownik **Base64**-kodowania wiadomości powitania, hello ładunku użytkownika może być zapasowej too48 KB, zamiast 64 KB.
* W przypadku kolejek usługi Service Bus, każdy komunikat przechowywane w kolejce składa się z dwóch części: Nagłówek i treść. Całkowity rozmiar wiadomości powitania Hello nie może przekraczać hello komunikat maksymalny rozmiar obsługiwany przez hello warstwy usług.
* Gdy klienci komunikują się z kolejek usługi Service Bus za pośrednictwem hello protokołu TCP, hello maksymalną liczbę równoczesnych połączeń tooa pojedynczej kolejki usługi Service Bus jest ograniczona too100. Ta liczba jest udostępniana między nadawcami a odbiornikami. Po osiągnięciu tego limitu przydziału, kolejne żądania dotyczące dodatkowych połączeń zostaną odrzucone i wyjątek zostanie odebrana przez hello wywołanie kodu. Ten limit jest nie nakłada na klientów łączących się za pomocą opartego na interfejsie REST API kolejek toohello.
* Jeśli potrzebujesz więcej niż 10000 kolejek w jednej przestrzeni nazw usługi Service Bus, można skontaktuj się z zespołem pomocy technicznej platformy Azure hello i zwiększenia. tooscale ponad 10 000 kolejki z usługą Service Bus, można również utworzyć dodatkowe przestrzenie nazw przy użyciu hello [portalu Azure][Azure portal].

## <a name="management-and-operations"></a>Zarządzanie i operacje
Ta sekcja porównuje hello funkcji zarządzania dostarczanych przez magazyn kolejek i kolejek usługi Service Bus.

| Kryteria porównania | Magazyn kolejek | Kolejki usługi Service Bus |
| --- | --- | --- |
| Protokół zarządzania |**REST za pośrednictwem protokołu HTTP/HTTPS** |**Zatrzymaj przy użyciu protokołu HTTPS** |
| Protokół środowiska wykonawczego |**REST za pośrednictwem protokołu HTTP/HTTPS** |**Zatrzymaj przy użyciu protokołu HTTPS**<br/><br/>**Protokół AMQP 1.0 Standard (TCP z protokołem TLS)** |
| Interfejs API .NET |**Tak**<br/><br/>(.NET magazynu klienta interfejsu API) |**Tak**<br/><br/>(.NET usługi Service Bus interfejsu API) |
| Natywnych języka C++ |**Tak** |**Tak** |
| Interfejs API języka Java |**Tak** |**Tak** |
| INTERFEJS API PHP |**Tak** |**Tak** |
| Interfejsu API środowiska node.js |**Tak** |**Tak** |
| Obsługa dowolnego metadanych |**Tak** |**Nie** |
| Reguły nazewnictwa kolejki |**Zapasowej too63 znaków**<br/><br/>(Litery w nazwie kolejki muszą być małe litery). |**Zapasowej too260 znaków**<br/><br/>(Nazwy i ścieżki kolejki jest rozróżniana wielkość liter.) |
| Get — funkcja długość kolejki |**Tak**<br/><br/>(Przybliżony wartość, jeśli wiadomości wygasają poza hello TTL bez usuwany.) |**Tak**<br/><br/>(Wartość dokładne, w momencie.) |
| Peek — funkcja |**Tak** |**Tak** |

### <a name="additional-information"></a>Dodatkowe informacje
* Magazyn kolejek zapewnia obsługę dowolnego atrybuty, które mogą być zastosowane toohello opis kolejki, w postaci hello par nazwa/wartość.
* Obu tych technologii kolejki oferują toopeek możliwości hello wiadomość bez konieczności toolock it, które mogą być przydatne podczas wdrażania narzędzia przeglądarki/explorer kolejki.
* Witaj .NET magistrali usług obsługiwanych przez brokera obsługi komunikatów interfejsów API wykorzystać pełnego dupleksu połączeń TCP zwiększonej wydajności podczas porównaniu tooREST za pośrednictwem protokołu HTTP i obsługują standardowy protokół hello protokołu AMQP 1.0.
* Nazwy kolejki magazynu może mieć 3 do 63 znaków długości, mogą zawierać małe litery, cyfry i łączniki. Aby uzyskać więcej informacji, zobacz [nazewnictwo kolejek i metadanych](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Nazwy kolejki usługi Service Bus można się too260 znaków i mieć mniej restrykcyjnych reguł nazewnictwa. Nazwy kolejki usługi Service Bus może zawierać litery, cyfry, kropki, łączniki i podkreślenia.

## <a name="authentication-and-authorization"></a>Uwierzytelnianie i autoryzacja
W tej sekcji omówiono funkcji uwierzytelniania i autoryzacji hello są obsługiwane przez magazyn kolejek i kolejek usługi Service Bus.

| Kryteria porównania | Magazyn kolejek | Kolejki usługi Service Bus |
| --- | --- | --- |
| Authentication |**Klucz symetryczny** |**Klucz symetryczny** |
| Model zabezpieczeń |Delegowane dostęp za pośrednictwem tokeny sygnatury dostępu Współdzielonego. |SYGNATURY DOSTĘPU WSPÓŁDZIELONEGO |
| Federacyjnych dostawca tożsamości |**Nie** |**Tak** |

### <a name="additional-information"></a>Dodatkowe informacje
* Każdy tooeither żądania z usługi kolejkowania wiadomości technologii hello musi zostać uwierzytelniony. Kolejek publicznych z dostęp anonimowy nie są obsługiwane. Przy użyciu [SAS](service-bus-sas.md), w tym scenariuszu można rozwiązać przez publikowanie tylko do zapisu dysków SAS, SAS tylko do odczytu lub nawet SAS pełnego dostępu.
* Witaj schemat uwierzytelniania podany przez magazyn kolejek obejmuje hello użycie klucza symetrycznego, które jest oparte na wyznaczania wartości skrótu wiadomości kodu uwierzytelniania (HMAC), obliczana z algorytmu SHA-256 hello i zakodowane jako **Base64** ciągu. Aby uzyskać więcej informacji na temat protokołu odpowiednich hello, zobacz [uwierzytelniania dla usług magazynu Azure hello](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Kolejek usługi Service Bus obsługują model podobne przy użyciu kluczy symetrycznych. Aby uzyskać więcej informacji, zobacz [uwierzytelniania podpisu dostępu udostępnionych za pomocą usługi Service Bus](service-bus-sas.md).

## <a name="conclusion"></a>Podsumowanie
Przejmując lepiej zrozumieć Witaj dwie technologie będzie być może toomake więcej świadomych decyzji, na którym kolejka toouse technologii i po. Witaj decyzji w sprawie po toouse magazynu kolejek lub usługi Service Bus kolejki wyraźnie zależy od wielu czynników. Te czynniki mogą stopniu zależne od hello indywidualnych potrzeb aplikacji i jej architektury. Jeśli aplikacja już używa hello podstawowych możliwości platformy Microsoft Azure, możesz toochoose magazynu kolejek, zwłaszcza jeśli wymagają komunikacja podstawowa i wysyłanie komunikatów między usług lub kolejek na potrzeby, które może być większy niż rozmiar 80 GB.

Ponieważ kolejek usługi Service Bus zapewniają zaawansowane funkcje, takie jak sesje, transakcje, zduplikowany wykrywania automatycznego Obsługa utraconych komunikatów i trwałe możliwości publikowania/subskrybowania, mogą one być preferowanym rozwiązaniem budowania aplikacji hybrydowych, lub jeśli w przeciwnym razie aplikacja wymaga tych funkcji.

## <a name="next-steps"></a>Następne kroki
Witaj następujące artykuły zawierają więcej wskazówki i informacje o używaniu magazynu kolejki lub kolejek usługi Service Bus.

* [Wprowadzenie do kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Jak tooUse hello usługi magazynu kolejek](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Najlepsze rozwiązania dotyczące poprawy wydajności przy użyciu usługi Service Bus obsługiwanych przez brokera obsługi komunikatów](service-bus-performance-improvements.md)
* [Wprowadzenie do kolejek i tematów w magistrali usługi Azure (wpis w blogu)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Witaj tooService przewodnik dewelopera magistrali](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Przy użyciu usługi kolejkowania wiadomości powitania na platformie Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

