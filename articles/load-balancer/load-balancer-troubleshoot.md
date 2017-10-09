---
title: "aaaTroubleshoot modułu równoważenia obciążenia Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z znane problemy z modułem równoważenia obciążenia Azure"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Rozwiązywanie problemów z usługą równoważenia obciążenia Azure

Ta strona zawiera informacje dotyczące rozwiązywania problemów dla często zadawane pytania usługi równoważenia obciążenia Azure. Gdy hello łączności usługi równoważenia obciążenia jest niedostępny, hello objawy najczęściej są następujące: 
- Maszyny wirtualne za hello modułu równoważenia obciążenia nie odpowiadają badania toohealth 
- Maszyny wirtualne za hello modułu równoważenia obciążenia nie odpowiadają toohello ruch na porcie hello skonfigurowane

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Objaw: Maszyny wirtualne za hello modułu równoważenia obciążenia nie odpowiadają badania toohealth
Witaj tooparticipate serwerów wewnętrznej bazy danych w zestawie usługi równoważenia obciążenia hello muszą one przejść hello sondowania wyboru. Aby uzyskać więcej informacji na temat sondy kondycji, zobacz [sondy modułu równoważenia obciążenia opis](load-balancer-custom-probe-overview.md). 

może nie odpowiadać puli zaplecza modułu równoważenia obciążenia Hello maszyn wirtualnych sondy toohello termin tooany z hello z następujących powodów: 
- Puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej jest zła 
- Ładowanie puli zaplecza modułu równoważenia maszyny Wirtualnej nie nasłuchuje na porcie sondowania hello 
- Zapora lub grupy zabezpieczeń sieci blokuje port hello na powitania puli zaplecza modułu równoważenia obciążenia maszyn wirtualnych 
- Inne błędy konfiguracji usługi równoważenia obciążenia

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>Przyczyna 1: Puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej jest zła 

**Sprawdzanie poprawności i rozwiązania**

tooresolve ten problem, zaloguj się za toohello uczestniczących maszyny wirtualne i sprawdź, czy hello stan maszyny Wirtualnej jest w dobrej kondycji i mogą odpowiadać za**narzędzia PsPing** lub **TCPing** z innej maszyny Wirtualnej w puli hello. Hello maszyna wirtualna jest w złej kondycji lub sondę toohello toorespond, należy rozwiązać problem hello, Pobierz hello maszyny Wirtualnej kopii tooa dobrej kondycji, aby uczestniczyć w równoważenia obciążenia.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Przyczyny 2: Puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej nie jest nasłuchuje na porcie sondowania hello
Jeśli hello maszyna wirtualna jest w dobrej kondycji, ale nie odpowiada toohello sondowania, jedną z możliwych przyczyn może być czy port sondy hello nie jest otwarty na powitania uczestniczących maszyny Wirtualnej lub hello maszyny Wirtualnej nie nasłuchuje na tym porcie.

**Sprawdzanie poprawności i rozwiązania**

1. Zaloguj się w zapleczu toohello maszyny Wirtualnej. 
2. Otwórz wiersz polecenia i uruchom następujące polecenie toovalidate istnieje aplikacja nasłuchuje na porcie sondowania hello hello:   
            polecenie netstat -
3. Jeśli stan portu hello nie jest wymieniony jako **LISTENING**, skonfiguruj hello prawidłowego portu. 
4. Można także wybrać innego portu, który jest wymieniony jako **LISTENING**i zaktualizuj odpowiednio załadować konfiguracji usługi równoważenia.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>Przyczyny 3: Zapora lub grupy zabezpieczeń sieci blokuje port hello na powitania puli zaplecza modułu równoważenia obciążenia maszyn wirtualnych  
Jeśli Zapora hello na powitania wirtualna blokuje port sondy hello lub grup zabezpieczeń co najmniej jeden sieciowe skonfigurowane na powitania podsieci lub hello maszyny Wirtualnej, nie zezwala na powitania sondowania tooreach hello portu, hello maszyny Wirtualnej jest sondy kondycji toohello toorespond.          

**Sprawdzanie poprawności i rozwiązania**

* Jeśli włączona jest Zapora hello, sprawdź, czy skonfigurowano port sondy hello tooallow. Jeśli nie, konfigurować hello zapory tooallow ruch na porcie sondowania hello i ponownie przetestuj. 
* Z listy hello grup zabezpieczeń sieci Sprawdź, czy hello przychodzący lub wychodzący ruch na porcie sondowania hello został zakłóceń. 
* Sprawdź również, czy **Odmów wszystkich** grup zabezpieczeń sieci reguły hello hello maszyny Wirtualnej karty Sieciowej lub hello podsieci, która ma wyższy priorytet niż hello domyślna reguła, która umożliwia sond LB & ruchu (grup zabezpieczeń sieci musi zezwalać na adres IP usługi równoważenia obciążenia 168.63.129.16). 
* Jeśli żadnego z tych reguł blokują ruch sondowania hello, Usuń, a następnie zmień konfigurację hello reguły tooallow hello badania ruchu.  
* Sprawdź, czy hello maszyna wirtualna ma teraz uruchomione, odpowiada badania kondycji toohello. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>Przyczyna 4: Inne błędy konfiguracji usługi równoważenia obciążenia
Jeśli wszystkie hello poprzedniego powoduje, że prawdopodobnie toobe weryfikacji i poprawnie rozpoznać i hello wewnętrznej bazy danych maszyny Wirtualnej nadal nie odpowiada toohello sondy kondycji, a następnie ręcznie testowania połączeń i zbierać łączności hello toounderstand niektóre dane śledzenia.

**Sprawdzanie poprawności i rozwiązania**

* Użyj **narzędzia Psping** z jednego z hello innych maszyn wirtualnych w ramach hello sieci wirtualnej tootest hello sondowania portu odpowiedzi (przykład:.\psping.exe 10.0.0.4:3389 -t) i zanotować wyniki. 
* Użyj **TCPing** z jednego z hello innych maszyn wirtualnych w ramach hello sieci wirtualnej tootest hello sondowania portu odpowiedzi (przykład:.\tcping.exe 10.0.0.4 3389) i zanotować wyniki. 
* Jeśli odpowiedź nie zostanie odebrana w tych testów ping następnie
    - Uruchom jednoczesnych Netsh śledzenia w puli zaplecza hello docelowej maszyny Wirtualnej i innego testu maszyny Wirtualnej z hello sam sieci wirtualnej. Teraz uruchom test narzędzia PsPing przez pewien czas, zbierać dane śledzenia niektórych sieci, a następnie zatrzymać hello testu. 
    - Analizowanie hello przechwytywania ruchu sieciowego i czy istnieją zarówno zapytania przychodzące i wychodzące pakiety toohello pokrewne polecenia ping. 
        - Jeśli nie pakiety przychodzące są przestrzegane w puli zaplecza hello maszyny Wirtualnej, jest potencjalnie sieciowych grup zabezpieczeń lub blokowania ruchu hello przez niewłaściwa konfiguracja. 
        - Jeśli w puli zaplecza hello maszyny Wirtualnej nie pakietów wychodzących, hello maszyny Wirtualnej musi toobe sprawdzane pod kątem niepowiązanych problemy (eample, port sondy hello blokowania aplikacji). 
    - Sprawdź, jeśli pakietów sondowania hello są wymuszone tooanother docelowego (prawdopodobnie przez ustawienia przez) przed osiągnięciem hello modułu równoważenia obciążenia. Może to spowodować hello ruchu toonever reach hello wewnętrznej bazy danych maszyny Wirtualnej. 
* Zmień typ sondy hello (na przykład HTTP tooTCP) i skonfigurować odpowiedni port hello grup zabezpieczeń sieci listy kontroli dostępu i toovalidate zapory, jeśli jest hello problem z konfiguracją hello odpowiedzi na sondę. Aby uzyskać więcej informacji na temat konfiguracji sondy kondycji, zobacz [równoważenia obciążenia punktu końcowego konfiguracji sondy kondycji](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Objaw: Maszyny wirtualne za usługą równoważenia obciążenia nie odpowiadają tootraffic na powitania skonfigurowany port danych

Jeśli w puli zaplecza maszyny Wirtualnej znajduje się w dobrej kondycji i odpowiada toohello sondy kondycji, ale nadal nie uczestniczy w hello równoważenia obciążenia lub nie odpowiada toohello ruch danych, może być spowodowane tooany hello z następujących powodów: 
* Maszyna wirtualna nie nasłuchuje na porcie danych hello puli zaplecza modułu równoważenia obciążenia 
* Grupy zabezpieczeń sieci blokuje port hello na powitania puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej  
* Uzyskiwanie dostępu do hello modułu równoważenia obciążenia z hello tej samej maszyny Wirtualnej i karty Sieciowej 
* Uzyskiwanie dostępu do hello VIP usługi równoważenia obciążenia Internet z hello uczestniczących puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>Przyczyna 1: Puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej nie jest nasłuchuje na porcie danych hello 
Jeśli maszyna wirtualna nie odpowiada toohello ruch w sieci, może to być spowodowane albo hello port docelowy nie jest otwarty na powitania uczestniczących maszyny Wirtualnej lub hello maszyny Wirtualnej nie nasłuchuje na tym porcie. 

**Sprawdzanie poprawności i rozwiązania**

1. Zaloguj się w zapleczu toohello maszyny Wirtualnej. 
2. Otwórz wiersz polecenia i uruchom następujące polecenie toovalidate istnieje aplikacja nasłuchuje na porcie danych hello hello:  
            polecenie netstat - 
3. Jeśli hello port nie ma na liście ze stanem "NASŁUCHIWANIA" Konfigurowanie portu odbiornika prawidłowego hello 
4. Jeżeli hello port jest oznaczona jako Listening, sprawdź aplikacji docelowej hello na tym porcie w poszukiwaniu możliwych problemów. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>Przyczyny 2: Grupy zabezpieczeń sieci blokuje port hello na powitania puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej  

Jeśli co najmniej jeden sieciowej grupy zabezpieczeń skonfigurowane na powitania podsieci lub hello maszyny Wirtualnej, blokuje hello źródłowy adres IP lub port, następnie hello maszyna wirtualna jest toorespond.

* Lista hello grup zabezpieczeń sieci skonfigurowane na powitania wewnętrznej bazy danych maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz:
    -  [Zarządzanie grupami zabezpieczeń sieci przy użyciu hello portalu](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [Zarządzanie grupami zabezpieczeń sieci przy użyciu programu PowerShell](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* Z listy hello grup zabezpieczeń sieci Sprawdź, czy:
    - Witaj przychodzący lub wychodzący ruch na porcie danych hello ma zakłóceń. 
    - **Odmów wszystkich** reguły grupy zabezpieczeń sieci na powitania karty Sieciowej z podsieci maszyny Wirtualnej lub hello hello, która ma wyższy priorytet tej reguły domyślnej hello umożliwiający sondy modułu równoważenia obciążenia i ruchu (grup zabezpieczeń sieci musi zezwalać na adres IP usługi równoważenia obciążenia 168.63.129.16, który jest port sondy) 
* Jeśli dowolne zasady hello blokują ruch hello, Usuń i ponownie skonfigurować te reguły tooallow hello ruchu w sieci.  
* Należy sprawdzić, czy hello maszyna wirtualna ma teraz uruchomione sondy kondycji toohello toorespond.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>Przyczyny 3: Uzyskiwanie dostępu do hello modułu równoważenia obciążenia z hello tej samej maszyny Wirtualnej i interfejsu sieciowego 

Jeśli aplikacji hostowanej w zapleczu hello wirtualna modułu równoważenia obciążenia jest w trakcie tooaccess innej aplikacji hostowanej w hello zaplecza tej samej maszyny Wirtualnej za pośrednictwem hello tego samego interfejsu sieciowego, jest to nieobsługiwany scenariusz i zakończy się niepowodzeniem. 

**Rozdzielczość** może rozwiązać ten problem, korzystając z jednej z następujących metod hello:
* Skonfiguruj pulę zaplecza oddzielne maszyn wirtualnych na aplikację. 
* Konfigurowanie aplikacji hello w dwóch kart interfejsu Sieciowego maszyn wirtualnych każda aplikacja korzystał z własnego interfejsu sieciowego i adresu IP. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>Przyczyna 4: Uzyskiwanie dostępu do hello wewnętrznego adresu VIP usługi równoważenia obciążenia z hello uczestniczących puli zaplecza modułu równoważenia obciążenia maszyny Wirtualnej

Jeśli skonfigurowano ILB wirtualne adresy IP w sieci wirtualnej i próbuje jednego uczestnika zaplecza hello maszyn wirtualnych tooaccess hello wewnętrzny VIP usługi równoważenia obciążenia, który powoduje błąd. Jest to nieobsługiwany scenariusz.
**Rozdzielczość** oceny bramą aplikacji lub innych toosupport proxy (na przykład nginx lub haproxy) to rodzaju scenariusza. Aby uzyskać więcej informacji na temat bramy aplikacji, zobacz [omówienie bramy aplikacji](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>Przechwytywanie dodatkowe sieci
Jeśli zdecydujesz się tooopen sprawy pomocy technicznej, zbieranie hello następujących informacji szybsze rozwiązanie problemu. Wybierz pojedynczy zaplecza hello tooperform wirtualna następujące testy:
- Przy użyciu narzędzia Psping z jednego z zaplecza hello maszyn wirtualnych w ramach hello sieci wirtualnej tootest hello sondowania portu odpowiedzi (przykład: 10.0.0.4:3389 narzędzia psping) i zanotować wyniki. 
- Użyj TCPing z jednego z zaplecza hello maszyn wirtualnych w ramach hello sieci wirtualnej tootest hello sondowania portu odpowiedzi (przykład: 10.0.0.4:3389 narzędzia psping) i zanotować wyniki.
- Jeśli odpowiedź nie zostanie odebrana w tych testów ping, uruchom jednoczesnych Netsh trace hello wewnętrznej bazy danych maszyny Wirtualnej, i hello testowej sieci wirtualnej maszyny Wirtualnej podczas uruchamiania narzędzia PsPing następnie zatrzymać hello Netsh trace. 
  
## <a name="next-steps"></a>Następne kroki

Jeśli hello powyższych kroków nie rozwiąże problemu hello, otwórz [obsługuje biletu](https://azure.microsoft.com/support/options/).

