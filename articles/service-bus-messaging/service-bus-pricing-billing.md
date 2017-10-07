---
title: aaaService magistrali cennik i rozliczenia | Dokumentacja firmy Microsoft
description: "Omówienie struktury cennik usługi Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Usługa Service Bus cennik i rozliczenia
Usługa Service Bus jest oferowany Basic, Standard i [Premium](service-bus-premium-messaging.md) warstw. Można wybrać dla każdej przestrzeni nazw usługi Service Bus, który utworzono warstwy usług, i stosuje ten wybór warstwy dla wszystkich obiektów utworzonych w tej przestrzeni nazw.

> [!NOTE]
> Aby uzyskać szczegółowe informacje o cenach bieżącej usługi Service Bus, zobacz hello [cennik usługi Azure Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)i hello [— często zadawane pytania dla magistrali usługi](service-bus-faq.md#pricing).
>
>

Usługa Service Bus używa hello następujące dwa liczników do kolejek i tematów/subskrypcji:

1. **Operacje do obsługi komunikatów**: zdefiniowany jako wywołania interfejsu API z kolejki i tematu/subskrypcji usługi punktów końcowych. Ten licznik spowoduje zastąpienie wiadomości wysyłane lub odbierane jako podstawową jednostkę hello rozliczeniowy użycie kolejek i tematów/subskrypcji.
2. **Obsługiwane przez brokera połączeń**: zdefiniowany jako hello maksymalna liczba połączeń trwałych Otwórz przed kolejki, tematy i subskrypcje w danego próbkowania jednogodzinnym przedziale czasu. Ten licznik ma zastosowanie tylko w warstwie standardowa hello, w którym można otwierać dodatkowych połączeń (wcześniej połączenia zostały ograniczone too100 dla kolejki/tematu/subskrypcji) do opłaty za połączenia nominalnego.

Witaj **standardowe** warstwy wprowadza pomiarowej ceny operacji z kolejki i tematy/subskrypcji, co rabaty oparte na woluminie z % too80 na powitania najwyższy poziom użycia. Brak opłat podstawowej warstwy standardowa $ 10 na miesiąc, co umożliwia tooperform się too12.5 mln operacji miesięcznie bez ponoszenia dodatkowych kosztów.

Witaj **Premium** warstwy zapewniają izolację zasobów w warstwie Procesora i pamięci hello, dzięki czemu obciążenia poszczególnych klientów uruchamia się w izolacji. Ten kontener zasobów jest nazywany *jednostką obsługi komunikatów*. Każda przestrzeń nazw w warstwie Premium ma przydzieloną co najmniej jedną jednostkę obsługi komunikatów. Możesz kupić 1, 2 lub 4 jednostki obsługi komunikatów dla każdej przestrzeni nazw usługi Service Bus w warstwie Premium. Pojedyncze obciążenie lub jednostka może obejmować wiele jednostek obsługi komunikatów, a hello liczbę jednostek obsługi komunikatów można dowolnie zmieniać, chociaż są w 24-godzinnym lub codziennie opłaty. wynik Hello jest przewidywalną i powtarzalną wydajność dla rozwiązania na podstawie usługi Service Bus. Poprawa dotyczy nie tylko przewidywalności i dostępności, ale również szybkości działania.

Pamiętaj tylko raz rozliczany opłata podstawowa warstwy standardowa hello na miesiąc na subskrypcję platformy Azure. Oznacza to, że po utworzeniu przestrzeni nazw usługi Service Bus warstwy jeden Standard będzie toocreate można dowolną liczbę dodatkowych standardowych przestrzeni nazw można dowolnie w tej samej subskrypcji platformy Azure, bez ponoszenia dodatkowych podstawowa opłat.

Witaj [cennik usługi Service Bus](https://azure.microsoft.com/pricing/details/service-bus/) tabela zawiera podsumowanie hello różnice funkcjonalne między warstwami hello podstawowa, standardowa i Premium.

## <a name="messaging-operations"></a>Operacje obsługi komunikatów
W ramach hello nowy model cenowy zmienia rozliczeń dla kolejek i tematów/subskrypcji. Te jednostki są przejścia z rozliczeń na toobilling komunikatów dla operacji. "Operacji" oznacza wywołania interfejsu API tooany przed punkt końcowy usługi kolejki i tematu/subskrypcji. Obejmuje to operacje stanu zarządzania, wysyłania i odbierania i sesji.

| Typ operacji | Opis |
| --- | --- |
| Zarządzanie |Tworzenia, odczytu, aktualizacji, usuwania (CRUD) z kolejki i tematy/subskrypcji. |
| Obsługa komunikatów |Wysyłanie i odbieranie wiadomości z kolejki i tematy/subskrypcji. |
| Stan sesji |Pobierania lub ustawiania stanu sesji na kolejki i tematu/subskrypcji. |

Ceny hello wymienione na powitania dla szczegółów kosztów [cennik usługi Service Bus](https://azure.microsoft.com/pricing/details/service-bus/) strony.

## <a name="brokered-connections"></a>Połączenia obsługiwane przez brokera
*Obsługiwane przez brokera połączeń* pomieścić wzorców użycia klienta, obejmujących wiele "stale połączonych" nadawców/odbiorcy przed kolejki, tematy i subskrypcje. Stale połączonych nadawców/odbiorcy są te, które łączą się przy użyciu protokołu AMQP lub HTTP z inną niż zero uzyskują limitu czasu (na przykład HTTP długi sondowania). HTTP nadawcami a odbiornikami natychmiastowego limitu czasu nie generują obsługiwanych przez brokera połączeń.

Dla połączenia przydziały i limity inne usługi, zobacz hello [przydziały usługi Service Bus](service-bus-quotas.md) artykułu.

liczby użycie agregacji obsługiwanych przez brokera połączeń między hello subskrypcji platformy Azure i usuwa limit połączeń obsługiwanych przez brokera na przestrzeń nazw hello Hello warstwy standardowa. Aby uzyskać więcej informacji, zobacz hello [obsługiwanych przez brokera połączeń](https://azure.microsoft.com/pricing/details/service-bus/) tabeli.

> [!NOTE]
> 1000 obsługiwanych przez brokera połączeń są dołączone standardowe warstwy obsługi wiadomości powitania (przy użyciu opłata podstawowa hello) i może być współużytkowana przez wszystkie kolejki, tematy i subskrypcje w ramach subskrypcji platformy Azure hello skojarzone.
>
>

<br />

> [!NOTE]
> Rozliczenia jest oparta na powitania maksymalna liczba jednoczesnych połączeń i jest obliczone proporcjonalnie co godzinę oparte na 744 godzin w miesiącu.
>
>

| Warstwa Premium |
| --- |
| Obsługiwane przez brokera połączeń nie są naliczane w warstwie Premium hello. |

Aby uzyskać więcej informacji na temat obsługiwanych przez brokera połączeń, zobacz hello [— często zadawane pytania](#faq) później w tym temacie.

## <a name="faq"></a>Często zadawane pytania

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>Co to są obsługiwane przez brokera połączeń i jak pobrać daną opłatę dla nich?
Obsługiwanego przez brokera połączenia jest zdefiniowana jako jedną z następujących hello:

1. Połączenia protokołu AMQP z kolejki usługi Service Bus tooa klienta lub tematu/subskrypcji.
2. HTTP wywołania tooreceive wiadomości z kolejki, która ma wartość limitu czasu odbierania większa od zera lub tematu usługi Service Bus.

Usługi Service Bus opłat za hello maksymalna liczba jednoczesnych połączeń obsługiwanych przez brokera, które przekraczają hello uwzględniona ilość (1000 w warstwie standardowa hello). Pików są mierzone na godzinę, obliczone proporcjonalnie dzieląc przez 744 godzin w miesiącu i dodaje się za pośrednictwem hello co miesiąc rozliczeń okresu. Hello uwzględniona ilość (1000 połączeń obsługiwanych przez brokera na miesiąc) jest stosowana na końcu hello hello okresie rozliczeniowym przed hello sumę hello obliczone proporcjonalnie pików co godzinę.

Na przykład:

1. Każda 10 000 urządzeń łączy się za pomocą pojedynczego połączenia protokołu AMQP i odbiera poleceń z tematu usługi Service Bus. Witaj urządzenia wysyłają dane telemetryczne zdarzenia tooan Centrum zdarzeń. Jeśli wszystkie urządzenia podłączone 12 godzin każdego dnia, zastosuj powitania po opłaty za połączenia (w tooany dodanie innych opłat tematu usługi Service Bus): połączenia o szybkości 10 000 * 12 godzin * 31 dni / 744 = 5000 obsługiwanych przez brokera połączeń. Po dodatku miesięczne hello 1000 połączeń obsługiwanych przez brokera będzie obciążana 4000 połączeń obsługiwanych przez brokera, szybkością hello 0,03 USD na połączenie obsługiwanych przez brokera, łącznie z $120.
2. 10 000 urządzeń odbierać komunikaty z kolejki usługi Service Bus za pośrednictwem protokołu HTTP, określając limit czasu równy zero. Wszystkie urządzenia połączyć 12 godzin codziennie, będzie mógł przeglądać powitania po opłaty za połączenia (w tooany dodanie opłat za inne usługi Service Bus): 10 000 HTTP odbierania połączeń * 12 godzin dziennie * 31 dni / godziny 744 = 5000 obsługiwanych przez brokera połączeń.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Czy obsługiwanych przez brokera połączeń opłaty tooqueues i tematy/subskrypcji?
Tak. Nie ma żadnych opłat połączenia do wysyłania zdarzeń przy użyciu protokołu HTTP, niezależnie od liczby hello wysyłania systemów lub urządzeń. Odbieranie zdarzeń z protokołem HTTP przy użyciu przekroczenie limitu czasu większą niż zero, nazywane czasem "long sondowania," generuje opłaty za połączenia obsługiwanych przez brokera. Połączenia protokołu AMQP Generowanie opłaty za połączenia obsługiwanych przez brokera, niezależnie od tego, czy połączenia hello są używane toosend lub odbierania. Należy pamiętać, że połączenia o szybkości 100 obsługiwanych przez brokera są dozwolone bez żadnych opłat w podstawowej przestrzeni nazw. Jest to również hello maksymalną liczbę obsługiwanych przez brokera połączeń dozwolonych dla hello subskrypcji platformy Azure. Witaj pierwszych 1000 obsługiwanych przez brokera połączeń we wszystkich standardowych przestrzeni nazw w subskrypcji platformy Azure są uwzględniane bez dodatkowych opłat (poza opłata podstawowa hello). Ponieważ te dodatki są wystarczająco dużo toocover wiele usług — scenariusze obsługi komunikatów, zazwyczaj opłaty za połączenia obsługiwanych przez brokera tylko stają się odpowiednie, jeśli planujesz toouse AMQP i HTTP long sondowania z dużej liczby klientów. na przykład tooachieve efektywniejsze zdarzenie przesyłania strumieniowego lub Włącz komunikację dwukierunkową z wieloma urządzeniami lub wystąpień aplikacji.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe informacje o cenach usługi Service Bus, zobacz hello [cennikiem usługi Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).
* Zobacz hello [— często zadawane pytania dla magistrali usługi](service-bus-faq.md#pricing) dla niektórych typowych — często zadawane pytania dotyczące usługi Service bus cennika i rozliczeń.

[Azure portal]: https://portal.azure.com
