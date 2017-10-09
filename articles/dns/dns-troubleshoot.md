---
title: "Przewodnik rozwiązywania problemów DNS aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot typowe problemy związane z usługi Azure DNS"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Usługa Azure DNS przewodnik rozwiązywania problemów

Ta strona zawiera informacje dotyczące rozwiązywania problemów dla często zadawane pytania usługi Azure DNS.

Jeśli te kroki nie rozwiążą problemu, możesz również wyszukać lub post problemu na naszych [forum pomocy technicznej społeczności w witrynie MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). Alternatywnie Otwórz żądanie pomocy technicznej platformy Azure.


## <a name="i-cant-create-a-dns-zone"></a>Nie można utworzyć strefy DNS

tooresolve typowe problemy, wypróbuj co najmniej jeden z hello następujące kroki:

1.  Przejrzyj powitalne inspekcji usługi Azure DNS rejestruje Przyczyna niepowodzenia hello toodetermine.
2.  Każda nazwa strefy DNS musi być unikatowa w obrębie swojej grupy zasobów. Oznacza to, że dwie strefy DNS z hello takie same nazwy nie mogą współużytkować grupę zasobów. Spróbuj użyć innej nazwy strefy lub innej grupy zasobów.
3.  Może zostać wyświetlony błąd "Osiągnięto lub przekroczono maksymalną liczbę stref w subskrypcji {identyfikator subskrypcji} hello." Użyj innej subskrypcji platformy Azure, usuń niektóre strefy lub skontaktuj się z pomocą techniczną platformy Azure tooraise limit subskrypcji.
4.  Może zostać wyświetlony błąd "hello strefa"{Nazwa strefy}"nie jest dostępny." Ten błąd oznacza, że usługi Azure DNS tooallocate serwerów nazw dla tej strefy DNS. Spróbuj użyć innej nazwy strefy. Alternatywnie Jeśli jesteś właścicielem nazwy domeny hello, skontaktuj się z pomocy technicznej platformy Azure, który można przydzielić serwery nazw dla Ciebie.


### <a name="recommended-documents"></a>**Zalecane dokumenty**

[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)<br>
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md) (Tworzenie strefy DNS)

## <a name="i-cant-create-a-dns-record"></a>Nie można utworzyć nowego rekordu DNS

tooresolve typowe problemy, wypróbuj co najmniej jeden z hello następujące kroki:

1.  Przejrzyj powitalne inspekcji usługi Azure DNS rejestruje Przyczyna niepowodzenia hello toodetermine.
2.  Zestaw rekordów hello istnieje już?  Usługa DNS platformy Azure zarządza rekordami przy użyciu rekordu *ustawia*, hello kolekcji rekordów hello takie same nazwy i hello takie same, które są typu. Jeśli rekord z hello takie same nazwy i typ już istnieje, następnie tooadd innego takie należy edytować hello istniejącego rekordu zestawu rekordów.
3.  Czy próbujesz toocreate rekord w wierzchołku strefy DNS hello (hello "główny" hello strefy)? Jeśli tak, hello Konwencja DNS jest toouse hello "@" jako nazwa rekordu hello znak. Należy również zauważyć, że hello standardy usługi DNS nie zezwalają na rekordy CNAME w wierzchołku strefy hello.
4.  Czy występuje konflikt dotyczący rekordu CNAME?  Standardy usługi DNS Hello nie zezwalają na rekordu CNAME o hello takie same nazwy jako rekord innego typu. Jeśli masz istniejące CNAME, tworzenie rekordu z hello nie powiedzie się w tej samej nazwy innego typu.  Podobnie utworzenie rekordu CNAME kończy się niepowodzeniem, jeśli nazwa hello odpowiada istniejącego rekordu innego typu. Usuń konflikt hello przez usunięcie hello inny rekord lub wybrać nazwę innego rekordu.
5.  Czy osiągnięto limit hello hello liczby zestawów rekordów w strefie DNS? Witaj bieżąca liczba zestawów rekordów i hello maksymalną liczbę zestawów rekordów są wyświetlane w portalu Azure, w obszarze hello 'właściwości' strefy hello hello. Jeśli zostanie osiągnięty limit, następnie usuń niektóre zestawy rekordów lub skontaktuj się z pomocą techniczną platformy Azure tooraise limitu zestaw rekordów dla tej strefy, a następnie spróbuj ponownie. 


### <a name="recommended-documents"></a>**Zalecane dokumenty**

[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)<br>
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md) (Tworzenie strefy DNS)



## <a name="i-cant-resolve-my-dns-record"></a>Nie mogę rozpoznać mojego rekordu DNS

Rozpoznawanie nazw DNS to wieloetapowy proces, który może się nie powieść z wielu powodów. Witaj Poniższe etapy ułatwiają zbadać, dlaczego niepowodzenie rozpoznawania nazw DNS dla rekordu DNS w strefie hostowanych w usłudze Azure DNS.

1.  Upewnij się, że rekordy DNS hello ma poprawnie skonfigurowany w usłudze Azure DNS. Przejrzyj hello rekordów DNS w hello portalu Azure, sprawdzanie, czy hello nazwę strefy, nazwę rekordu i typ rekordu są poprawne.
2.  Upewnij się, rekordy DNS hello rozpoznawane poprawnie na serwery hello Azure DNS.
    - Jeśli wprowadzisz zapytania DNS z komputera lokalnego, mogą pojawić się buforowane wyniki, które nie odzwierciedlają hello bieżący stan serwerów nazw hello.  Ponadto sieciach firmowych często używają serwerów proxy DNS, które uniemożliwiają zapytania DNS skierowane toospecific serwery nazw.  tooavoid usługa rozpoznawania nazw oparte na sieci web takich jak używać tych problemów [digwebinterface](http://digwebinterface.com).
    - Hello serwerami poprawną nazwę dla swojej strefy DNS, jak pokazano w portalu Azure hello być toospecify się, że.
    - Sprawdź, czy nazwa DNS hello jest poprawna, (masz toospecify hello w pełni kwalifikowana nazwa, łącznie z nazwą strefy hello) i typ rekordu hello jest prawidłowa
3.  Potwierdź tej nazwy domeny DNS hello została prawidłowo [delegowane serwerów nazw usługi Azure DNS toohello](dns-domain-delegation.md). Istnieje [wiele witryn innych firm umożliwiających weryfikowanie delegowania DNS](https://www.bing.com/search?q=dns+check+tool). Ten test jest *strefy* delegowania testu, dlatego należy wprowadzić tylko nazwę strefy DNS hello i nie hello pełni kwalifikowaną nazwę rekordu.
4.  Po zakończeniu hello powyżej, Twoje rekord DNS powinien teraz prowadzić poprawnie. tooverify, można ponownie użyć [digwebinterface](http://digwebinterface.com), przy użyciu hello domyślne nazwy ustawienia serwera.


### <a name="recommended-documents"></a>**Zalecane dokumenty**

[Delegat tooAzure domeny DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Jak określić hello "Usługa" i "Protokół" dla rekordu SRV?

Usługa DNS platformy Azure zarządza rekordami DNS jako zestawów rekordów — Witaj kolekcji rekordów z hello takie same nazwy i hello sam typu. Dla zestawu rekordów SRV toobe określony jako część nazwy zestawu rekordów hello należy hello "Usługa" i "Protokół". Witaj inne parametry SRV ("priority", "weight", "port" i "target") są określane oddzielnie dla każdego rekordu w zestawie rekordów hello.

Przykładowe nazwy rekordów SRV (nazwa usługi „sip”, protokół „tcp”):

- \_SIP. \_tcp (tworzy rekord w wierzchołku strefy hello)
- \_sip.\_tcp.sipservice (tworzy zestaw rekordów o nazwie „sipservice”)

### <a name="recommended-documents"></a>**Zalecane dokumenty**

[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)<br>
[Tworzenie zestawów rekordów DNS i rekordów przy użyciu hello portalu Azure](dns-getstarted-create-recordset-portal.md)
<br>
[Typ rekordu SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [strefy DNS platformy Azure i rekordów](dns-zones-records.md)
* toostart przy użyciu usługi Azure DNS, Dowiedz się, jak za[utworzyć strefę DNS](dns-getstarted-create-dnszone-portal.md) i [utworzyć rekordy DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate istniejącej strefy DNS, Dowiedz się, jak za[importowanie i eksportowanie pliku strefy DNS](dns-import-export.md).

