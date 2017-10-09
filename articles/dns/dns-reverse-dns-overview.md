---
title: aaaOverview wstecznego DNS na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak wstecznego DNS działa i jak może służyć na platformie Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Omówienie wstecznego DNS i pomocy technicznej na platformie Azure

Ten artykuł zawiera omówienie sposobu wstecznego DNS działa i hello obsługiwane przez platformę Azure odwrotna scenariuszy DNS.

## <a name="what-is-reverse-dns"></a>Co to jest wstecznego DNS?

Konwencjonalne rekordy DNS Włącz mapowanie z adresu IP tooan nazwę (np. www.contoso.com) DNS (na przykład 64.4.6.100).  Wstecznego DNS umożliwia tłumaczenie hello nazwy tooa Wstecz (64.4.6.100) adres IP (www.contoso.com).

Odwrotnej rekordy DNS są używane w różnych sytuacjach. Na przykład odwrotnej rekordy DNS są powszechnie używane w zapobieganiu spamu e-mail weryfikując hello nadawcy wiadomości e-mail.  Hello odbierania poczty serwera pobiera hello wstecznego rekord hello wysyłania adres IP serwera DNS i sprawdza, czy że host jest toosend autoryzowanych wiadomości powitania pochodzących domeny. 

## <a name="how-reverse-dns-works"></a>Działa jak wstecznego DNS

Odwrotnej rekordy DNS są obsługiwane w specjalne stref DNS, znany jako strefy "ARPA".  Te strefy tworzą oddzielne hierarchii DNS równolegle z hierarchii normalne hello hosting domeny, takie jak "contoso.com".

Na przykład hello rekord DNS "www.contoso.com" jest implementowane za pomocą rekordu DNS "A" o nazwie hello "www" w strefie hello "contoso.com".  Ten rekord A punktów toohello odpowiedni adres IP, w tym przypadku 64.4.6.100.  wyszukiwanie wsteczne Hello jest implementowane oddzielnie, za pomocą rekordu "PTR" o nazwie "100" w strefie hello "6.4.64.in-addr.arpa" (Zauważ, że adresy IP są wycofywane w strefy ARPA.)  Ten rekord PTR, jeśli została skonfigurowana poprawnie, punktów toohello nazwy "www.contoso.com".

Jeśli organizacja jest przypisany blok adresów IP, również uzyskać hello prawo toomanage hello odpowiadającą ARPA strefę. Witaj strefy ARPA odpowiadającego toohello adres IP, bloki używane przez usługę Azure są obsługiwane i zarządzany przez firmę Microsoft. Usługodawca Internetowy może obsługiwać strefy ARPA hello adresy IP dla Ciebie lub mogą zezwolić hosta tooyou strefy ARPA hello w usłudze DNS w wybranych przez użytkownika, takie jak usługi Azure DNS.

> [!NOTE]
> Wyszukiwania DNS do przodu i wyszukiwania wstecznego DNS są implementowane w oddzielnych, równoległe hierarchii DNS. Witaj wyszukiwania wstecznego dla "www.contoso.com" jest **nie** hostowana w strefie "contoso.com" hello, zamiast jest obsługiwany w strefy ARPA hello hello odpowiedni blok adresów IP. Bloki adresów IPv4 i IPv6 używane są osobne strefy.

### <a name="ipv4"></a>IPv4

Hello Nazwa strefy wyszukiwania wstecznego IPv4 powinny mieć hello następującego formatu: `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Na przykład podczas tworzenia strefy wyszukiwania wstecznego toohost rekordów dla hostów z adresów IP, które są w hello 192.0.2.0/24 prefiks, nazwę strefy hello zostałyby utworzone w przez izolowanie hello sieci prefiks adresu hello (192.0.2), a następnie odwracanie kolejności hello (2.0.192) i dodawanie hello sufiks `.in-addr.arpa`.

|Klasa podsieci|Prefiks sieci  |Prefiks odwróconej sieci  |Standardowa sufiks  |Nazwa strefy wyszukiwania wstecznego |
|-------|----------------|------------|-----------------|---------------------------|
|Klasa A|203.0.0.0/8     | 203        | .w addr.arpa   | `203.in-addr.arpa`        |
|Klasa B|198.51.0.0/16   | 51.198     | .w addr.arpa   | `51.198.in-addr.arpa`     |
|Klasa C|192.0.2.0/24    | 2.0.192    | .w addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Classless delegowania IPv4

W niektórych przypadkach zakres adresów IP hello przydzielone tooan organizacji jest mniejszy niż klasa C (/ 24) zakresu. W takim przypadku zakres adresów IP hello nie mieści się w granicach strefy w ramach hello `.in-addr.arpa` strefy hierarchię i dlatego nie może być delegowane jako strefy podrzędnej.

Zamiast tego jest używany inny mechanizm kontroli tootransfer poszczególnych wyszukiwania wstecznego (PTR) rejestruje tooa dedykowanego strefy DNS. Ten mechanizm deleguje strefy podrzędnej dla każdego zakres adresów IP, a następnie każdego adresu IP w hello map zakres indywidualnie toothat strefy podrzędnej przy użyciu rekordów CNAME.

Na przykład załóżmy, że organizacja otrzymuje 192.0.2.128/26 zakres IP hello przez jego usługodawcy internetowego. Stanowi to 64 adresy IP z 192.0.2.128 too192.0.2.191. Wstecznego DNS dla tego zakresu jest zaimplementowana w następujący sposób:
- organizacja Hello tworzy strefę wyszukiwania wstecznego o nazwie 128-26.2.0.192.in-addr.arpa. Prefiks Hello "128-26' reprezentuje hello organizacji toohello segment przypisany sieci w ramach hello klasy C (/ 24) zakresu.
- Hello usługodawcy internetowego tworzy tooset rekordy NS zapasowej hello delegowania hello powyżej strefy DNS w strefie nadrzędnej klasy C hello. Tworzy również rekordy CNAME w hello nadrzędnego (Klasa C) strefy wyszukiwania wstecznego, mapowania poszczególnych adresów IP hello IP zakresu toohello nowej strefy utworzonej przez organizację hello:

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- Witaj organizacji, a następnie zarządza hello poszczególnych rekordów PTR w ich strefy podrzędnej.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Wyszukiwanie wsteczne hello IP address "192.0.2.129" zapytania dotyczące rekordu PTR o nazwie "129.2.0.192.in-addr.arpa". To zapytanie rozpoznaje za pośrednictwem hello CNAME w hello rekordu PTR toohello strefy nadrzędnej w hello strefy podrzędnej.

### <a name="ipv6"></a>Protokół IPv6

Nazwa strefy wyszukiwania wstecznego IPv6 Hello musi należeć do hello następującej postaci:`<IPv6 network prefix in reverse order>.ip6.arpa`

Na przykład. Podczas tworzenia strefy wyszukiwania wstecznego toohost rekordy dotyczące hostów z adresów IP, które znajdują się w hello 2001:db8:1000:abdc:: / 64 prefiks, nazwę strefy hello zostałyby utworzone przez izolowanie hello sieci prefiks adresu hello (2001:db8:abdc::). Następnie rozwiń węzeł hello IPv6 sieci prefiks tooremove [zero kompresji](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), jeśli był prefiks adresu hello IPv6 tooshorten używanych (2001:0db8:abdc:0000::). Od ostatniej hello odwrócenie kropką jako hello ogranicznik między każdą liczbę szesnastkową hello prefiksu, toobuild hello prefiks sieci (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) i Dodaj sufiks hello `.ip6.arpa`.


|Prefiks sieci  |Prefiks rozwinięte i odwróconej sieci |Standardowa sufiks |Nazwa strefy wyszukiwania wstecznego  |
|---------|---------|---------|---------|
|2001:db8:abdc:: / 64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | . ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102:: / 64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | . ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Obsługa platformy Azure wstecznego DNS

Azure obsługuje dwa oddzielne scenariusze dotyczące tooreverse DNS:

**Hosting hello wyszukiwania wstecznego strefy odpowiedniego tooyour blok adresów IP.**
Usługa DNS platformy Azure może służyć za[przechowywania stref wyszukiwania wstecznego i zarządzanie nimi hello rekordów PTR dla każdego wyszukiwania wstecznego DNS](dns-reverse-dns-hosting.md)dla protokołów IPv4 i IPv6.  proces tworzenia strefy wyszukiwania wstecznego (ARPA) hello, konfigurowanie delegowania hello Hello i konfigurowanie PTR rekordów jest hello takie same jak w przypadku regularnego strefy DNS.  Witaj tylko różnice są delegowania hello musi być skonfigurowany za pomocą usługodawca Internetowy, a nie rejestratora DNS, czy powinien być używany tylko hello typu rekordu PTR.

**Skonfiguruj hello odwrotnej rekordu DNS dla adresu IP hello przypisanego tooyour usługi Azure.** Azure umożliwia utworzenie zbyt[Konfigurowanie wyszukiwania wstecznego hello hello adresy IP przydzielone tooyour usługi Azure](dns-reverse-dns-for-azure-services.md).  To wyszukiwanie wsteczne jest skonfigurowana przez platformę Azure jako rekord PTR w odpowiedniej strefy ARPA hello.  Te strefy ARPA, odpowiadającego zakresów IP hello tooall używanych przez platformę Azure, są obsługiwane przez firmę Microsoft

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących wstecznego DNS, zobacz [istnienia wstecznego wyszukiwania DNS dla Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Dowiedz się, jak za[strefy wyszukiwania wstecznego hello hosta zakres IP przypisany usługodawcy internetowego w usłudze Azure DNS](dns-reverse-dns-for-azure-services.md).
<br>
Dowiedz się, jak za[Zarządzanie odwrotnej rekordy DNS dla usług Azure](dns-reverse-dns-for-azure-services.md).

