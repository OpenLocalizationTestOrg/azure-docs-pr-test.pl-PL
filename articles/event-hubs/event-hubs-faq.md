---
title: "aaaAzure centra zdarzeń — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Usługa Azure Event Hubs — często zadawane pytania (FAQ)"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Usługa Event Hubs — często zadawane pytania

## <a name="general"></a>Ogólne

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Jaka jest różnica hello warstwy standardowa i podstawowa centra zdarzeń?

warstwy standardowa Hello Azure Event hubs udostępnia funkcje poza co to jest dostępne w warstwie podstawowa hello. Standard dołączonych Hello następujące funkcje:
* Dłużej przechowywania zdarzeń
* Dodatkowe połączeń obsługiwanych przez brokera dodatkowy nadwyżkowe więcej niż liczba hello włączone
* Więcej niż jednej grupy odbiorców
* [Przechwytywania](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Aby uzyskać więcej informacji na temat cen warstwy dedykowanego centra zdarzeń w tym temacie hello [szczegóły cennika usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>Co to są jednostek przepływności usługi Event Hubs?

Należy wybrać jawnie jednostek przepływności usługi Event Hubs, za pośrednictwem portalu Azure hello lub szablony Menedżera zasobów centrów zdarzeń. Jednostki przepływności Zastosuj tooall centra zdarzeń w przestrzeni nazw usługi Event Hubs i każdej jednostki przepływności uprawnia toohello przestrzeni nazw hello następujące możliwości:

* Too1 MB na sekundę zdarzenia transfer danych przychodzących (zdarzenia wysyłane do Centrum zdarzeń), ale nie więcej niż 1000 wejściowych zdarzenia, operacji zarządzania lub formantu wywołania interfejsu API na sekundę.
* Too2 MB na sekundę wyjście zdarzeń (zdarzenia używane z Centrum zdarzeń).
* Zapasowej too84 GB (umożliwiający hello domyślnego okresu przechowywania 24-godzinnym) przechowywania zdarzeń.

Jednostki przepływności centra zdarzeń są rozliczane godzinowo, na podstawie hello maksymalnej liczby jednostek wybranej podczas hello podane godziny.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>Jak wymusić ograniczenia jednostki przepływności usługi Event Hubs
Jeśli przepustowość łączny ruch przychodzący hello lub występowania zdarzeń wejściowych całkowita hello przez wszystkie centra zdarzeń w przestrzeni nazw przekracza hello łącznej przepływności jednostki dodatki, nadawców są ograniczane i błędów wskazujący, że ten hello wejściowych została przekroczona.

Jeśli hello wyjście całkowitej przepływności lub hello całkowita liczba zdarzeń wyjście szybkość przez wszystkie centra zdarzeń w przestrzeni nazw przekracza hello łącznej przepływności jednostki dodatków, odbiorcy są ograniczane i błędy wskazujące, że hello wyjście została przekroczona. Przydziały przychodzące i wychodzące są wymuszane oddzielnie, umożliwiając nadawcy może spowodować tooslow zużycie zdarzenia w dół ani odbiornika uniemożliwia zdarzenia są wysyłane do Centrum zdarzeń.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>Istnieje limit liczby hello jednostek przepływności, które można wybrać?
Brak domyślnego przydziału 20 jednostek przepływności na przestrzeni nazw. Można zażądać większego limitu przydziału jednostek przepływności, zgłaszając bilet pomocy technicznej. Poza hello 20 limit jednostki przepływności pakiety są dostępne w 20 i 100 jednostek przepływności. Należy pamiętać, że korzystanie z więcej niż 20 jednostek przepływności usuwa hello możliwości toochange hello liczbę jednostek przepływności bez zgłoszenia biletu pomocy technicznej.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>Można I użyj pojedynczego toosend połączenia protokołu AMQP i odbierać z wielu centrów zdarzeń
Tak, jak długo są wszystkie usługi event hubs hello w hello tego samego obszaru nazw.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>Co to jest hello maksymalny okres przechowywania dla zdarzeń?
Warstwy standardowa centra zdarzeń obsługuje obecnie okres maksymalny czas przechowywania danych w ciągu 7 dni. Należy pamiętać, usługa event hubs nie są przeznaczone jako magazynu danych trwałych. Okresy przechowywania jest dłuższy niż 24 godziny są przeznaczone dla scenariuszy, w których jest wygodne tooreplay strumienia zdarzeń w hello tego samego systemów. na przykład tootrain lub sprawdź nowego modelu uczenia maszynowego na istniejących danych. Jeśli konieczne komunikatu przechowywania poza 7 dni, włączanie [przechwytywania centra zdarzeń](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) na zdarzenie Centrum pobiera hello dane z Twojego konta magazynu toohello Centrum zdarzeń lub konta usługi Azure Data Lake usługi wybrane. Włączanie przechwytywania wiąże opłat oparte na sieci zakupionych jednostek przepływności.

### <a name="where-is-azure-event-hubs-available"></a>Gdzie jest usługa Azure Event Hubs?
Usługa Azure Event Hubs jest dostępna we wszystkich obsługiwanych regionach platformy Azure. Lista, odwiedź stronę hello [regiony platformy Azure](https://azure.microsoft.com/regions/) strony.  

## <a name="best-practices"></a>Najlepsze praktyki

### <a name="how-many-partitions-do-i-need"></a>Jak wiele partycji potrzebuję?
Sprawdź należy pamiętać, że hello liczba partycji w Centrum zdarzeń nie można modyfikować po zakończeniu instalacji. Ten fakt jest ważne toothink, o ile partycji, należy przed rozpoczęciem pracy. 

Centra zdarzeń jest zaprojektowana tooallow czytnik jedną partycję na grupę odbiorców. W większości przypadków użycia wystarczy hello domyślne ustawienie cztery partycje. Jeśli szukasz tooscale Twojego przetwarzania zdarzeń, może być tooconsider Dodawanie dodatkowe partycje. Nie ma żadnego limitu określonego przepływności na partycji, jednak hello łącznej przepływności w przestrzeni nazw jest ograniczona liczba hello jednostek przepływności. Zwiększania hello liczbę jednostek przepływności w przestrzeni nazw można tooachieve współbieżnych czytników tooallow dodatkowe partycje własnych maksymalną przepustowość.

Jednak jeśli modelu, w którym aplikacja ma koligacji tooa określonej partycji, zwiększenie liczby hello partycji może nie być tooyou żadnych korzyści. Aby uzyskać więcej informacji na ten temat, zobacz [dostępności i spójności](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Cennik

### <a name="where-can-i-find-more-pricing-information"></a>Gdzie można znaleźć informacje o cenach więcej?
Aby uzyskać pełne informacje na temat cen usługi Event Hubs, zobacz hello [szczegóły cennika usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>Czy istnieje opłata przechowywania zdarzeń usługi Event Hubs przez więcej niż 24 godziny?
warstwy standardowa centra zdarzeń Hello Zezwalaj przechowywania wiadomości okresów dłużej niż 24 godziny, maksymalnie 7 dni. Jeśli rozmiar hello hello całkowitej liczby zdarzeń przechowywanych przekracza dozwolony magazynu hello hello liczbę jednostek przepływności wybranego (84 GB na jednostkę przepływności), rozmiar hello przekracza dozwolony hello jest rozliczana według hello opublikowane szybkość magazynu obiektów Blob platformy Azure. Dodatek magazynu Hello w każdej jednostki przepływności obejmuje kosztów magazynowania wszystkich okresów przechowywania 24 godzin (domyślnie: hello) nawet wtedy, gdy jednostka przepływności hello jest używany się toohello wejściowych maksymalny dozwolony.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Jak jest hello rozmiar magazynu usługi Event Hubs obliczone i pobierane?
Całkowity rozmiar wszystkich przechowywanych zdarzeniami, w tym wszelkie koszty wewnętrzny dla nagłówków zdarzeń lub struktur na dysku magazynu w wszystkie usługi event hubs, Hello jest mierzony w ciągu dnia hello. Na koniec hello dnia hello maksymalny rozmiar magazynu hello jest obliczana. codzienne dodatek magazynu Hello jest obliczana na podstawie hello minimalną liczbę jednostek przepływności, które zostały wybrane w dniu hello (każdej jednostki przepływności udostępnia dodatek 84 GB). Jeśli hello łączny rozmiar przekracza hello codziennie obliczane dodatek magazynu, jest on rozliczany hello nadmiarowe magazynu przy użyciu stawek obowiązujących dla magazynu obiektów Blob platformy Azure (na powitania **magazyn lokalnie nadmiarowy** szybkość).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>Jak są obliczane zdarzeń wejściowych centra zdarzeń
Centrum zdarzeń tooan traktowana jako rozliczeniowy wiadomości wysłane każdego zdarzenia. *Zdarzeń wejściowych* jest zdefiniowany jako jednostka danych, która jest mniejsza niż lub równa too64 KB. Wszystkie zdarzenia, która jest mniejsza lub równa rozmiarze too64 KB jest uważany za toobe jedno zdarzenie rozliczeniowy. Jeśli zdarzenie hello jest większy niż 64 KB, liczba hello rozliczeniowy zdarzeń jest obliczana według rozmiaru zdarzenia toohello, wielokrotności 64 KB. Na przykład 8 KB zdarzenia wysłanego toohello Centrum zdarzeń jest on rozliczany jako jedno zdarzenie, ale 96 KB wiadomość wysłana toohello Centrum zdarzeń jest on rozliczany jako dwa zdarzenia.

Używane z Centrum zdarzeń, jak również jako operacji zarządzania i kontroli wywołań, taką jak punkty kontrolne nie są liczone jako zdarzenia rozliczeniowy wejściowych, ale naliczania zapasowej dodatku jednostki przepływności toohello zdarzenia.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>Czy obsługiwanych przez brokera połączeń opłaty koncentratory tooEvent?
Opłaty za połączenia mają zastosowanie tylko wtedy, gdy jest używany protokół AMQP hello. Nie ma żadnych opłat połączenia do wysyłania zdarzeń przy użyciu protokołu HTTP, niezależnie od liczby hello wysyłania systemów lub urządzeń. Jeśli planujesz toouse AMQP (na przykład tooachieve efektywniejsze zdarzenie przesyłania strumieniowego lub tooenable dwukierunkowej komunikacji w scenariuszach IoT polecenia i kontrola), zobacz hello [uzyskać informacje o cenach usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) strony, aby uzyskać szczegółowe informacje o tym, jak wiele połączeń są uwzględnione w poszczególnych warstwach usług.

### <a name="how-is-event-hubs-capture-billed"></a>W jaki sposób są naliczane opłaty za funkcję przechwytywanie usługi Event Hubs?
Przechwytywanie jest włączona, gdy wszystkie Centrum zdarzeń w przestrzeni nazw hello włączono opcję przechwytywania hello. Przechwyć centra zdarzeń są rozliczane godzinowo na jednostkę przepływności zakupionych. Jak hello liczby jednostek przepływności zwiększyć lub zmniejszyć, karta przechwytywania centra zdarzeń odzwierciedla te zmiany w całej godz. Aby uzyskać więcej informacji dotyczących rozliczeń przechwytywania centra zdarzeń, zobacz [uzyskać informacje o cenach usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>I naliczania dla konta magazynu hello wybrany Capture centra zdarzeń?
Przechwytywanie używa konta magazynu, podane przez użytkownika po włączeniu w Centrum zdarzeń. Jest to Twoje konto magazynu, wszystkie zmiany dla tej konfiguracji są rachunku tooyour subskrypcji platformy Azure.

## <a name="quotas"></a>Przydziały

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Czy istnieją wszystkie przydziały skojarzony z usługą Event Hubs?
Aby uzyskać listę wszystkich przydziałów centra zdarzeń, zobacz [przydziały](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>Jakie są hello wyjątków generowanych przez centra zdarzeń i ich sugerowane akcje?
Listę możliwych wyjątków usługi Event Hubs, zobacz [omówienie wyjątki](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Dzienniki diagnostyczne
Usługa Event Hubs obsługuje dwa typy [dzienników diagnostycznych](event-hubs-diagnostic-logs.md) -przechwytywania dzienniki błędów i operacyjne dzienniki — które są reprezentowane w formacie json i można włączyć za pomocą hello portalu Azure.

### <a name="support-and-sla"></a>Pomoc techniczna i umowa SLA
Pomoc techniczna dla usługi Event Hubs jest dostępna za pośrednictwem hello [Fora społeczności użytkowników](https://social.msdn.microsoft.com/forums/azure/home). Pomoc dotycząca rozliczeń i subskrypcji jest świadczona bezpłatnie.

toolearn więcej informacji na temat naszych umowy dotyczącej poziomu usług, zobacz hello [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/) strony.

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
