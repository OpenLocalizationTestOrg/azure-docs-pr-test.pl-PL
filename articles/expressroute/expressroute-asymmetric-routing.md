---
title: aaaAsymmetric routing | Dokumentacja firmy Microsoft
description: "W tym artykule przedstawiono hello problemów, które klient może sprostać asymetrycznego routingu w sieci z wielu docelowego tooa łącza."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Routing asymetryczny z wieloma ścieżkami sieciowymi
W tym artykule wyjaśniono, jak ruch sieciowy w obie strony może podążać różnymi trasami w przypadku dostępności wielu ścieżek między miejscem źródłowym i docelowym.

Jego ważne toounderstand dwa pojęcia toounderstand asymetrycznego routingu. Co jest efektem hello wiele ścieżek sieci. Witaj innych jest sposób urządzenia, takie jak zapory, Zachowaj stan. Tego rodzaju urządzenia są nazywane urządzeniami stanowymi. Kombinacja te dwa czynniki tworzy w sieci, do której ruch jest porzucone przez urządzenie stanowe, ponieważ hello stanowe urządzenia nie wykrył, że ruchu sieciowego pochodzi z urządzenia hello scenariuszy.

## <a name="multiple-network-paths"></a>Wiele ścieżek sieciowych
Gdy sieci przedsiębiorstwa ma tylko jedną toohello link, który przechodzi przez Internet za pośrednictwem swojego usługodawcy internetowego, wszystkie tooand ruchu z hello Internet hello tej samej ścieżce. Często firm zakupu wielu obwody jako nadmiarowe ścieżki, tooimprove sieci przestojów. W takim przypadku jego możliwe, że ruchu przechodzącego spoza sieci hello, toohello Internet, przesyłany przez jedno łącze i hello zwracać ruch przechodzi przez różne łącza. Jest to często określane mianem routingu asymetrycznego. W asymetrycznego routingu odwrotnej ruchu sieciowego ma inną ścieżkę z oryginalnego przepływu hello.

![Sieć z wieloma ścieżkami](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Mimo że nastąpi to przede wszystkim na powitania Internet, asymetrycznego routingu również ma zastosowanie kombinacji tooother wiele ścieżek. Dotyczy, na przykład zarówno ścieżka Internet tooan i ścieżki prywatnej, która go toohello tego samego miejsca docelowego, a toomultiple ścieżek prywatne, które go toohello tego samego miejsca docelowego.

Każdy router na sposób hello, z toodestination źródła oblicza hello najlepsze ścieżki tooreach miejsca docelowego. Witaj routera najlepsze możliwe ścieżki opiera się na dwie główne czynniki:

* Routing między sieciami zewnętrznymi opiera się na protokole routingu o nazwie Border Gateway Protocol (BGP). Protokół BGP pobiera anonsów sąsiadów i uruchamia je na kolejnych kroków toodetermine hello najlepsze ścieżki toohello przeznaczone docelowego. Ścieżka najlepsze hello są przechowywane w tabeli routingu.
* Długość Hello maskę podsieci skojarzoną z trasy wpływ ścieżki routingu. Router odbiera kilka anonsów dla hello tego samego adresu IP, ale o różnych masek podsieci, hello router preferuje hello anonsu z maską podsieci dłużej ponieważ uwzględniono więcej określoną trasę.

## <a name="stateful-devices"></a>Urządzenia stanowe
Routery przyjrzeć się nagłówek IP hello pakietu do celów routingu. Niektóre urządzenia Szukaj trudniejsze wewnątrz hello pakietu. Zazwyczaj te urządzenia sprawdzają nagłówki warstwy 4 (protokół TCP lub UDP), a nawet warstwy 7 (warstwa aplikacji). Urządzenia te to urządzenia zabezpieczające lub urządzenia optymalizujące przepustowość. 

Zapora jest typowym przykładem urządzenia stanowego. Zapora zezwala lub nie zezwala toopass pakietów, za pomocą ich interfejsów na podstawie różnych pól, takie jak protokół, port TCP/UDP i nagłówków adresu URL. Ten poziom inspekcję pakietów umieszcza przy dużym obciążenia na urządzeniu hello przetwarzania. wydajność tooimprove hello Zapora sprawdza hello pierwszego pakietu przepływu. Jeśli umożliwia tooproceed pakietów hello zachowuje hello przepływ informacji w tabeli stanu. Wszystkie kolejne pakiety powiązane toothis przepływu dozwolone są oparte na powitania wstępnego określenia. Pakiet jest częścią istniejącego przepływu może przyjeździe hello zapory. Jeśli Zapora hello nie ma poprzedniego stanu informacji o jego, zapory hello porzuca pakietów hello.

## <a name="asymmetric-routing-with-expressroute"></a>Routing asymetryczny przy użyciu usługi ExpressRoute
Po podłączeniu tooMicrosoft za pośrednictwem usługi Azure ExpressRoute, takie jak zmiany sieci to:

* Masz wiele tooMicrosoft łącza. Jedno łącze jest istniejące połączenie internetowe, a hello innych odbywa się za pośrednictwem usługi ExpressRoute. Niektóre tooMicrosoft ruchu może przejść przez hello internetowych, ale Wróć za pośrednictwem usługi ExpressRoute, albo na odwrót.
* Usługa ExpressRoute zapewnia bardziej szczegółowe adresy IP. Tak dla ruchu z Twojej sieci tooMicrosoft dla usług oferowanych przez usługi ExpressRoute, routery zawsze wybierasz ExpressRoute.

toounderstand hello wpływ mają te dwie zmiany w sieci, teraz należy wziąć pod uwagę kilka scenariuszy. Na przykład masz tylko jedną toohello obwodu Internet i korzystać z wszystkich usług firmy Microsoft za pośrednictwem hello Internet. Witaj ruch z sieci traverses tooMicrosoft i z powrotem hello tego samego łącza internetowego i przechodzi przez zaporę Windows hello. rejestruje zapory Hello hello przepływu widzi hello pierwszego pakietu i zwracać pakiety są dozwolone, ponieważ przepływ hello istnieje w tabeli stanu hello.

![Routing asymetryczny przy użyciu usługi ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

Załóżmy teraz, że usługa ExpressRoute została włączona i korzystasz z usług oferowanych przez firmę Microsoft za jej pośrednictwem. Innych usług firmy Microsoft są używane przez hello Internet. Możesz wdrożyć oddzielny zapory na Twojej krawędzi, który jest połączony tooExpressRoute. Microsoft anonsuje dokładniej prefiksy tooyour sieci za pośrednictwem usługi do określonych usług. Infrastrukturę routingu wybiera ExpressRoute jako hello preferowaną ścieżką dla tych prefiksów. Jeśli Twoje publicznego tooMicrosoft adresy IP są nie prowadzi anonsowania za pośrednictwem usługi ExpressRoute, Microsoft komunikuje się z publicznych adresów IP, za pośrednictwem hello Internet. Ruch do przodu z Twojej sieci tooMicrosoft używa usługi ExpressRoute i odwrotnej ruch od firmy Microsoft używa hello Internet. Gdy hello zapory na krawędzi hello widzi pakiet odpowiedzi dla przepływu, który nie zostanie znaleziona w tabeli stanu hello, porzuca hello zwracany ruchu.

Jeśli wybierzesz hello toouse puli tego samego translatora adresów sieciowych (NAT) dla usługi ExpressRoute i hello Internet, zobaczysz podobne problemy klientom Witaj w sieci, w prywatnych adresów IP. Żądania dla usług takich jak Windows Update przejść za pomocą hello Internet, ponieważ adresy IP dla tych usług nie są rozgłaszane za pośrednictwem usługi ExpressRoute. Jednak ruch zwracany hello wróci za pośrednictwem usługi ExpressRoute. Jeśli Microsoft otrzymuje adres IP z hello tej samej maski podsieci z hello Internet i ExpressRoute, ExpressRoute go preferuje hello Internet. Jeśli zapora lub innego urządzenia stanowych, które znajduje się na krawędzi Twojej sieci i ukierunkowane ExpressRoute nie ma wcześniejszych informacji o hello przepływu, porzuca pakietów hello, które należą toothat przepływu.

## <a name="asymmetric-routing-solutions"></a>Rozwiązania w zakresie routingu asymetrycznego
Masz dwie główne opcje toosolve hello problem asymetrycznego routingu. Jest za pośrednictwem routingu i hello innych jest za pomocą opartego na źródle translatora adresów Sieciowych (SNAT).

### <a name="routing"></a>Routing
Upewnij się, czy łącza sieci (rozległej WAN) rozległej anonsowany tooappropriate publiczne adresy IP. Na przykład jeśli chcesz toouse hello Internet ruchu uwierzytelniania i ExpressRoute dla ruchu poczty nie powinien anonsują publiczne adresy IP usługi Active Directory Federation Services (AD FS) za pośrednictwem usługi ExpressRoute. Podobnie, upewnij się, nie tooexpose usługi lokalnej adresy tooIP serwera usług AD FS, które hello router odebrał za pośrednictwem usługi ExpressRoute. Trasy odebranych za pośrednictwem usługi ExpressRoute są bardziej szczegółowe, więc finalizowania ExpressRoute hello preferowaną ścieżką dla tooMicrosoft ruchu uwierzytelniania. Wywołuje to asymetryczny routing.

Jeśli chcesz toouse ExpressRoute do uwierzytelniania, upewnij się, że są anonsowanie publiczne adresy IP usług AD FS, za pośrednictwem usługi ExpressRoute bez translatora adresów sieciowych. Dzięki temu ruch, który pochodzi od firmy Microsoft i przechodzi tooan w lokalnym serwera usług AD FS przechodzi przez usługi ExpressRoute. Zwracany ruch od klienta tooMicrosoft wykorzystuje ExpressRoute, ponieważ jego trasy preferowane hello za pośrednictwem Internetu hello.

### <a name="source-based-nat"></a>Translator adresów sieciowych oparty na źródle
Innym sposobem rozwiązania problemów z routingiem asymetrycznym jest translator adresów sieciowych oparty na źródle (SNAT). Na przykład można mieć nie anonsowanych hello publiczny adres IP serwera Simple Mail Transfer Protocol (SMTP) lokalnymi ExpressRoute ponieważ planujesz hello toouse Internet dla tego typu komunikacji. Żądanie, które pochodzą z firmą Microsoft, a następnie przechodzi tooyour w lokalnym hello Internet przechodzi przez serwer SMTP. Możesz SNAT hello przychodzącego żądania tooan wewnętrznego adresu IP. Ruch odwrotnej z serwera SMTP hello przechodzi toohello zaporą brzegową (który jest używany dla translatora adresów Sieciowych) zamiast za pośrednictwem usługi ExpressRoute. ruch zwracany Hello powraca za pośrednictwem hello Internet.

![Konfiguracja translatora adresów sieciowych opartych na źródle](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Wykrywanie routingu asymetrycznego
Traceroute jest hello najlepsze sposób toomake się upewnić, że ruchu sieciowego przechodzi przez hello oczekiwano ścieżki. Jeśli ruch z sieci lokalnej SMTP server tooMicrosoft tootake hello Internet ścieżki, hello oczekiwanych traceroute pochodzi z tooOffice serwera SMTP hello 365. wynik Hello weryfikuje ruchu w rzeczywistości opuszcza sieci kierunku hello Internet, a nie do usługi ExpressRoute.

