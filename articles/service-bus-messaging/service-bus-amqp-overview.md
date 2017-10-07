---
title: "aaaOverview protokołu AMQP 1.0 w Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Informacje o używaniu hello zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) 1.0 na platformie Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>Obsługa protokołu AMQP 1.0 w usłudze Service Bus
Witaj zarówno usługi Azure Service Bus w chmurze i lokalnych [Usługa Service Bus dla systemu Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) Obsługa hello zaawansowane komunikatów usługi kolejkowania protokołu (protokół AMQP) 1.0. Protokół AMQP umożliwia możesz toobuild między platformami, hybrydowych aplikacji przy użyciu standardowego protokołu zapewniającego Otwórz. Można utworzyć aplikacji przy użyciu składników, które są tworzone przy użyciu różnych języków i struktur, które działają w różnych systemach operacyjnych. Wszystkie te składniki łączyć tooService magistrali i bezproblemowo wymiany wiadomości biznesowych strukturalnych wydajne i w pełnej rozdzielczości.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Wprowadzenie: Co to jest protokołu AMQP 1.0 i dlaczego ważne jest?
Tradycyjnie zorientowany pośredniczącego używanych protokołów własnościowych do komunikacji między aplikacjami klienckimi i brokerów. To oznacza, że po wybraniu brokera obsługi komunikatów dla określonego dostawcy musi używać tego dostawcy bibliotek tooconnect Twojego brokera toothat aplikacji klienta. W efekcie stopień zależność od tego dostawcy, ponieważ eksportowanie aplikacji tooa innego produktu wymaga zmian kodu we wszystkich aplikacjach hello połączony. 

Ponadto łączenie brokerzy wiadomości pochodzących od różnych dostawców jest istotne znaczenie. Zwykle wymaga poziomu aplikacji mostkowania toomove komunikaty tooanother jeden system i tootranslate między ich formaty wiadomości zastrzeżonych. Jest to wymagane wspólnej; na przykład po musi podać nowe tooolder ujednolicony interfejs różnych systemów, lub zintegrować systemów IT po połączeniu.

Hello producentów oprogramowania jest firma szybko; Czasami bewildering tempem wprowadzane są nowe języki programowania i platform aplikacji. Podobnie ewoluują wymagania hello systemów IT z upływem czasu i deweloperzy mają tootake zaletą hello najnowszych funkcji platformy. Jednak czasami hello wybranego dostawcy obsługi wiadomości nie obsługuje tych platform. Ponieważ protokoły są unikatowe, jest niedozwolona w przypadku innych bibliotek tooprovide dla tych nowych platform. W związku z tym należy użyć metod, takich jak tworzenie bramy lub mostków umożliwiających toocontinue toouse hello komunikatów produktu.

Programowanie Hello powitalne zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) 1.0 został uzasadnione tych problemów. Jego występowania w Morgan Chase JP, kto, podobnie jak najbardziej finansowych usługowe, są użytkownicy zorientowany oprogramowania pośredniczącego. Celem Hello było proste: toocreate obsługi wiadomości protokołu standardu open, zgłaszającego przy użyciu składników utworzony przy użyciu różnych języków, struktur i systemów operacyjnych, aplikacji opartych na komunikat toobuild możliwe wszystkie przy użyciu najlepszych obsługi składniki z zakres dostawców.

## <a name="amqp-10-technical-features"></a>Funkcje techniczne protokołu AMQP 1.0
Protokołu AMQP 1.0 jest wydajne, niezawodne i poziom przewodowy obsługi wiadomości protokołu używania toobuild niezawodne, między platformami, aplikacje do obsługi komunikatów. Protokół Hello ma prosty cel: toodefine mechanika hello hello bezpieczne, niezawodne i wydajne transferu wiadomości między dwiema stronami. wiadomości powitania od siebie są zakodowane przy użyciu reprezentację danych, umożliwiający heterogenicznych nadawcami a odbiornikami tooexchange strukturę firm wiadomości w pełnej rozdzielczości. Witaj poniżej znajduje się podsumowanie najważniejszych funkcji hello:

* **Efektywne**: protokół AMQP 1.0 stanowi nawiązaniem połączenia protokołu, że używa pliku binarnego kodowanie hello protokołu instrukcje i hello firm wiadomości przesyłane nad nim. Zawiera zaawansowane sterowanie przepływem schematy toomaximize hello wykorzystania sieci hello i składniki hello połączony. Inaczej mówiąc, protokół hello został zaprojektowany toostrike równowagi między wydajność, elastyczność i współdziałanie.
* **Niezawodne**: hello protokołu AMQP 1.0 umożliwia toobe wiadomości wymieniane zakres gwarancje niezawodności, fire i zapomnij tooreliable dokładnie — raz potwierdzenie dostarczenia.
* **Elastyczne**: protokołu AMQP 1.0 jest protokołem elastycznym, które mogą być używane toosupport topologii. Witaj tego samego protokołu może służyć do komunikacji klienta do klienta, klient brokera i broker brokera.
* **Niezależne od modelu brokera**: hello Specyfikacja protokołu AMQP 1.0 nie powoduje żadnych wymagań dotyczących modelu obsługi wiadomości powitania używany przez brokera. Oznacza to, że możliwe jest tooeasily dodać brokery tooexisting obsługi protokołu AMQP 1.0.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>Protokół AMQP 1.0 stanowi standardowe (z kapitału ")
Protokół AMQP 1.0 stanowi międzynarodowe wersje standard, zatwierdzone przez ISO i IEC jako 19464:2014 ISO/IEC.

Protokołu AMQP 1.0 został rozwijany od 2008 przez grupę core więcej niż 20 firm, zarówno dostawców technologii, jak i firm użytkownika końcowego. W tym czasie firmy użytkownika przyczyniły ich wymagania biznesowe rzeczywistych i dostawców technologii hello usprawnionych hello protokołu toomeet tych wymagań. W trakcie procesu hello dostawców uczestniczyli w zakładów, w których one współpracę toovalidate hello współdziałanie ich implementacji.

W października 2011 hello projektach przeszła tooa techniczne Komitet hello organizacji dla hello przejścia z Structured Information Standards (OASIS) i hello OASIS protokołu AMQP 1.0 standardowe został wydany w października 2012. Witaj poniższych firmy brał udział w Komisji techniczne hello podczas tworzenia hello hello standardowe:

* **Technologia dostawców**: Axway oprogramowania, Huawei technologii, IIT oprogramowania, INETCO systemów, Kaazing, Microsoft, Mitre Corporation, Primeton technologii, postęp oprogramowania, Red Hat, SITA, oprogramowania AG, Solace systemów, VMware, WSO2, Zenika.
* **Firmy użytkownika**: Bank Ameryka Suisse środki, Boerse marki, Goldman Sachs, JPMorgan Chase.

Niektóre hello często odnosiło się, że zalety otwartych standardów:

* Mniejsze ryzyko blokady w dostawcy
* Współdziałanie
* Szerokie dostępności biblioteki i narzędzia
* Ochrona przed utraty przydatności
* Dostępność personelu wiedzą
* Niższe i łatwą w obsłudze ryzyka

## <a name="amqp-10-and-service-bus"></a>Protokołu AMQP 1.0 i Service Bus
Obsługa protokołu AMQP 1.0 w Azure Service Bus oznacza, że można teraz korzystać z usługi Service Bus hello usługi kolejkowania wiadomości i publikowania/subskrypcji obsługiwanych przez brokera obsługi komunikatów funkcje z zakresu od platformy przy użyciu protokołu binarnego wydajne. Ponadto można tworzyć aplikacje obejmuje składniki utworzony przy użyciu różnych języków, struktur i systemów operacyjnych.

Witaj rysunku przedstawiono przykład wdrożenia, w których klienci Java uruchomiony w systemie Linux, napisane przy użyciu interfejsu API hello standardowe usługi komunikat Java (JMS) i .NET uruchomiony w systemie Windows, wymiana wiadomości za pośrednictwem usługi Service Bus przy użyciu protokołu AMQP 1.0.

![][0]

**Rysunek 1: Przykładowy wdrożenia scenariusz przedstawiający wieloplatformowych wiadomości przy użyciu usługi Service Bus i protokołu AMQP 1.0**

W tym hello czasu toowork z usługą Service Bus znane są następujące biblioteki klienta:

| Język | Biblioteka |
| --- | --- |
| Java |Klient usługi komunikat Java Apache Qpid (JMS)<br/>Klient IIT oprogramowania SwiftMQ Java |
| C |Apache Qpid protonów C |
| PHP |Apache Qpid protonów PHP |
| Python |Apache Qpid protonów Python |
| C# |Protokół AMQP .net Lite |

**Rysunek 2: Tabela bibliotek klienta protokołu AMQP 1.0**

## <a name="summary"></a>Podsumowanie
* Protokołu AMQP 1.0 jest otwarty, niezawodnej obsługi komunikatów protokołu służy aplikacji hybrydowych dla wielu platform, toobuild. Protokołu AMQP 1.0 jest standardem OASIS.
* Obsługa protokołu AMQP 1.0 jest teraz dostępna w Azure Service Bus, a także Usługa Service Bus dla systemu Windows Server (Service Bus 1.1). Cennik jest powitalne hello takie same jak w przypadku istniejących protokołów.

## <a name="next-steps"></a>Następne kroki
Gotowe toolearn więcej? Odwiedź hello następującego łącza:

* [Przy użyciu usługi Service Bus z .NET z protokołu AMQP]
* [Przy użyciu usługi Service Bus za pomocą języka Java w usłudze AMQP]
* [Instalowanie na maszynie Wirtualnej platformy Azure Linux Apache Qpid protonów C]
* [Protokół AMQP w usłudze Service Bus dla systemu Windows Server]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[Przy użyciu usługi Service Bus z .NET z protokołu AMQP]: service-bus-amqp-dotnet.md
[Przy użyciu usługi Service Bus za pomocą języka Java w usłudze AMQP]: service-bus-amqp-java.md
[Instalowanie na maszynie Wirtualnej platformy Azure Linux Apache Qpid protonów C]: service-bus-amqp-apache.md
[Protokół AMQP w usłudze Service Bus dla systemu Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
