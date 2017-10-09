---
title: "aplikacje usługi Azure Service Bus aaaInsulating przed awariami i awarii | Dokumentacja firmy Microsoft"
description: "Opisuje metody można użyć aplikacji tooprotect dla potencjalnych awarii usługi Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Najlepsze rozwiązania dotyczące izolacji aplikacji przed awariami usługi Service Bus i awarii
Kluczowych aplikacji musi działać w sposób ciągły, nawet w obecności hello nieplanowanych przestojów lub awarii. W tym temacie opisano metody można użyć aplikacji usługi Service Bus tooprotect dla potencjalnych awarii usługi lub po awarii.

Awaria jest zdefiniowany jako tymczasowej niedostępności hello Azure Service Bus. Witaj awarii może mieć wpływ na niektórych składników usługi Service Bus, takiego jak magazynie obsługi komunikatów, lub nawet hello całe centrum danych. Po hello problem został rozwiązany, usługi Service Bus znowu dostępne. Zazwyczaj awarii nie powoduje utraty wiadomości lub innych danych. Przykładem awarii składnika jest niedostępność hello określonym magazynie obsługi komunikatów. Przykład awaria sieci centrum danych jest awarii zasilania hello centrum danych lub przełącznik sieciowy błędny centrum danych. Awaria może trwać od kilku minut tooa kilka dni.

Awarii jest zdefiniowany jako trwałą utratę hello jednostki skalowania usługi Service Bus lub datacenter. Witaj w centrum danych może lub nie może stać się dostępne ponownie. Zazwyczaj awarii spowoduje, że niektóre lub wszystkie komunikaty lub innych danych. Przykłady awarii fire, zalewania lub trzęsienie ziemi.

## <a name="current-architecture"></a>Architektura bieżącego
Usługa Service Bus używa wielu komunikatów magazynów toostore wiadomości wysyłanych tooqueues lub tematów. Niepartycjonowany kolejka lub temat przypisano tooone magazynu do obsługi komunikatów. Ten magazyn obsługi komunikatów jest niedostępny, wszystkie operacje dla tej kolejki lub temat zakończy się niepowodzeniem.

Wszystkie jednostki obsługi komunikatów usługi Service Bus (kolejek, tematów, przekaźników) znajdują się w przestrzeni nazw usługi, które jest powiązane z centrum danych. Magistrali usług nie są włączone automatyczne replikacja geograficzna, danych ani jej zezwala toospan przestrzeni nazw wiele centrów danych.

## <a name="protecting-against-acs-outages"></a>Ochrona przed awariami ACS
Jeśli używane są poświadczenia ACS i usług ACS jest niedostępny, klienci nie mogą uzyskać tokeny. Klientów, którzy mają tokenu w czasie hello ACS ulegnie awarii można kontynuować toouse usługi Service Bus do momentu wygaśnięcia tokenów hello. okres istnienia tokenu domyślne Hello jest 3 godziny.

tooprotect względem awarii ACS za pomocą tokenów dostępu sygnatury dostępu Współdzielonego. W takim przypadku klient hello uwierzytelnia bezpośrednio z usługą Service Bus przez podpisywania tokenu własnym minted za pomocą klucza tajnego. TooACS wywołania nie są już wymagane. Aby uzyskać więcej informacji na temat tokeny sygnatury dostępu Współdzielonego, zobacz [uwierzytelniania usługi Service Bus][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Ochrona kolejek i tematów z błędami magazynu do obsługi komunikatów
Niepartycjonowany kolejka lub temat przypisano tooone magazynu do obsługi komunikatów. Ten magazyn obsługi komunikatów jest niedostępny, wszystkie operacje dla tej kolejki lub temat zakończy się niepowodzeniem. A podzielona na partycje kolejki na powitania drugiej strony, składa się z wielu fragmentów. Każdy fragment są przechowywane w różnych magazynie obsługi komunikatów. Po wysłaniu wiadomości tooa partycjonowanej kolejka lub temat usługi Service Bus przypisuje tooone wiadomość hello hello fragmentów. Odpowiedni magazyn obsługi wiadomości powitania jest niedostępny, usługi Service Bus zapisuje wiadomość hello tooa fragmentu innego, jeśli to możliwe. Aby uzyskać więcej informacji na temat partycjonowane jednostki, zobacz [partycjonowane jednostki do obsługi komunikatów][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Ochrona przed przestojami centrum danych lub awarii
tooallow Failover między dwoma centrami danych, można utworzyć przestrzeni nazw usługi Service Bus w każde centrum danych. Na przykład Witaj nazw usługi Service Bus **contosoPrimary.servicebus.windows.net** może znajdować się w regionie Stanów Zjednoczonych północ/centralnego hello, i **contosoSecondary.servicebus.windows.net**może znajdować się w regionie nam Południowa/centralnego hello. Jeśli jednostki do obsługi komunikatów usługi Service Bus musi pozostać dostępna w obecności hello awarii centrum danych, możesz utworzyć jednostkę w obu tych przestrzeni nazw.

Aby uzyskać więcej informacji, zobacz sekcja "Niepowodzenie usługi Service Bus w obrębie centrum danych Azure" hello [asynchroniczne wzorce i wysokiej dostępności do obsługi komunikatów][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Ochrona punktów końcowych przekazywania względem przestojami centrum danych lub awarii
Replikacja geograficzna punktów końcowych przekazywania umożliwia to usługa, która przedstawia przekazywania toobe punktu końcowego, dostępny w obecności hello awarie usługi Service Bus. tooachieve replikacja geograficzna, usługa hello musi utworzyć dwa punkty końcowe przekazywania w różnych przestrzeniach nazw. przestrzenie nazw Hello musi znajdować się w różnych centrach danych i hello dwa punkty końcowe muszą mieć różne nazwy. Na przykład podstawowy punkt końcowy jest osiągalny w obszarze **contosoPrimary.servicebus.windows.net/myPrimaryService**, a jego odpowiednikiem dodatkowej można połączyć się w obszarze **contosoSecondary.servicebus.windows.net /mySecondaryService**.

Usługa Hello następnie nasłuchuje oba punkty końcowe, a klient może wywołać hello usługi za pośrednictwem albo punktu końcowego. Aplikacja kliencka losowo wybiera jeden z przekaźników hello jako hello podstawowy punkt końcowy i wysyła jego żądanie toohello aktywny punkt końcowy. Jeśli operacja hello kończy się niepowodzeniem z kodem błędu, ten błąd oznacza, że tego punktu końcowego przekazywania hello jest niedostępny. Aplikacja Hello otwiera toohello kopii zapasowej punktu końcowego kanału i wysyła żądanie hello. W tym momencie hello active i tworzenia kopii zapasowej punkty końcowe hello przełączyć role: powitania klienta aplikacji uwzględnia hello starego aktywny punkt końcowy toobe hello nowy punkt końcowy kopii zapasowej i hello starego zapasowego punktu końcowego toobe hello nowy aktywny punkt końcowy. Jeśli niepowodzenie operacji zarówno wysyłania, role hello Witaj dwie jednostki pozostają bez zmian i zostanie zwrócony błąd.

Witaj [— replikacja geograficzna z usługą Service Bus obsługiwanych przez przekaźnik wiadomości] [ Geo-replication with Service Bus relayed Messages] przykładzie pokazano, jak przekazuje tooreplicate.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Ochrona kolejek i tematów względem przestojami centrum danych lub awarii
tooachieve odporności na awarie centrum danych przy użyciu komunikatów obsługiwanych przez brokera, Usługa Service Bus obsługuje dwa podejścia: *active* i *pasywnym* replikacji. Dla każdego z podejść Jeśli dany kolejka lub temat musi pozostać dostępna w obecności hello awarii centrum danych, można go utworzyć w obu tych przestrzeni nazw. Obie te jednostki można mieć hello tej samej nazwy. Na przykład w obszarze osiągalna kolejki głównej **contosoPrimary.servicebus.windows.net/myQueue**, a jego odpowiednikiem dodatkowej można połączyć się w obszarze **contosoSecondary.servicebus.windows.net/myQueue**.

Jeśli aplikacja hello wymaga stałej łączności nadawcy do odbiornika, aplikacja hello można zaimplementować trwałe kolejki po stronie klienta tooprevent utratą i tooshield hello nadawcy wiadomości z przejściowych błędów usługi Service Bus.

## <a name="active-replication"></a>Aktywna replikacja
Aktywna replikacja używa jednostek w obu tych przestrzeni nazw dla każdej operacji. Każdy klient, który wysyła komunikat wysyła dwie kopie hello tego samego komunikatu. Pierwsza kopia Hello są wysyłane toohello podstawowej jednostki (na przykład **contosoPrimary.servicebus.windows.net/sales**), i drugą kopię wiadomości powitania hello są wysyłane toohello dodatkowej jednostki (na przykład  **contosoSecondary.servicebus.windows.net/sales**).

Klient odbiera komunikaty z kolejek obu. procesy odbiornika Hello hello pierwsza kopia wiadomości, a druga kopia hello jest pomijane. toosuppress zduplikowanych wiadomości powitania nadawcy musi tagu każdy komunikat z unikatowym identyfikatorem. Obydwie kopie wiadomości powitania musi być oznaczane hello tego samego identyfikatora. Można użyć hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] lub [BrokeredMessage.Label] [ BrokeredMessage.Label] właściwości lub hello tootag właściwości niestandardowej Komunikat. odbiornik Hello muszą zachować listę komunikatów, które już została odebrana.

Witaj [— replikacja geograficzna z komunikatów obsługiwanych przez brokera magistrali usługi] [ Geo-replication with Service Bus Brokered Messages] przykładzie pokazano aktywna replikacja jednostek do obsługi komunikatów.

> [!NOTE]
> podejście aktywna replikacja Hello podwaja hello liczba operacji, w związku z tym takie podejście może prowadzić toohigher kosztów.
> 
> 

## <a name="passive-replication"></a>Pasywne replikacji
W przypadku awarii bez hello pasywnym replikacji używa tylko jeden z dwóch jednostek obsługi komunikatów hello. Klient wysyła jednostki active toohello wiadomość hello. Jeśli operacja hello w jednostce active hello kończy się niepowodzeniem z kodem błędu wskazujący hello centrum danych, czy jednostki active hello hosty mogą być niedostępne, powitania klienta wysyła kopię jednostek kopii zapasowej toohello wiadomość hello. W tym momencie hello active i jednostek kopii zapasowej hello przełączyć role: powitania klienta wysyłania uwzględnia hello starego aktywnych toobe hello nowej kopii zapasowej jednostki i hello starego jednostka kopii zapasowej jest hello nowej jednostki aktywne. Jeśli niepowodzenie operacji zarówno wysyłania, role hello Witaj dwie jednostki pozostają bez zmian i zostanie zwrócony błąd.

Klient odbiera komunikaty z kolejek obu. Ponieważ jest stosowany tego odbiornika hello odbiera dwie kopie hello sam komunikatu, hello odbiornika musi pomijania zduplikowanych wiadomości. Można pominąć duplikatów hello sam sposób jak opisane dla aktywnej replikacji.

Ogólnie rzecz biorąc pasywnym replikacji jest bardziej ekonomiczne niż replikacja usługi active, ponieważ w większości przypadków jest wykonywane tylko jedna operacja. Czas oczekiwania, przepływności i koszt są identyczne toohello niezreplikowanej scenariusza.

Korzystając z pasywnym replikacji, w hello następujące scenariusze komunikaty mogą być utracone lub odbierane dwa razy:

* **Opóźnienie wiadomości lub utraty**: założono, że nadawca hello pomyślnie wysłał wiadomość kolejki głównej toohello m1 i kolejki hello staje się niedostępna przed odbiornika hello odbiera m1. nadawca Hello wysyła kolejki dodatkowej toohello m2 kolejnych komunikatów Szukaj komunikatu. Jeśli kolejka głównej hello jest tymczasowo niedostępny, odbiornika hello odbiera m1 po kolejki hello znowu dostępne. W przypadku awarii odbiornika hello nigdy nie może zostać wyświetlony m1.
* **Zduplikowana odbioru**: założono tego nadawcy hello wysyła kolejki głównej toohello komunikatów m. Usługa Service Bus pomyślnie przetwarza m, ale nie powiedzie się toosend odpowiedzi. Po hello wysłać czasu operacji wychodzących, hello Nadawca wysyła identyczne kopię kolejki dodatkowej toohello m. Jeśli odbiornik hello jest pierwsza kopia stanie tooreceive hello m przed kolejki głównej hello staje się niedostępny, odbiornika hello odbiera obydwie kopie m w przybliżeniu hello tym samym czasie. Jeśli odbiornik hello nie jest możliwe tooreceive hello pierwszego kopiowania m przed kolejki głównej hello przestanie być dostępny, odbiornika hello początkowo odbiera tylko hello drugiej kopii m, ale otrzyma kopię m po udostępnieniu hello kolejki głównej.

Witaj [— replikacja geograficzna z usługą Service Bus obsługiwanych przez brokera komunikatów] [ Geo-replication with Service Bus Brokered Messages] przykładzie pokazano pasywnym replikacji jednostki do obsługi komunikatów.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat odzyskiwania po awarii, zobacz następujące artykuły:

* [Ciągłość prowadzenia działalności biznesowej bazy danych Azure SQL][Azure SQL Database Business Continuity]
* [Projektowanie aplikacji odporne na platformie Azure][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
