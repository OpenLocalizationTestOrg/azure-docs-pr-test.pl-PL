---
title: "niestandardowe sond równoważenia aaaLoad i stan kondycji monitorowania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak sondy toouse niestandardowych dla usługi równoważenia obciążenia Azure toomonitor wystąpień za usługą równoważenia obciążenia"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Opis sond modułu równoważenia obciążenia

Moduł równoważenia obciążenia Azure oferuje hello możliwości toomonitor hello kondycji wystąpień serwera przy użyciu sondy. W przypadku awarii toorespond sondę modułu równoważenia obciążenia zatrzymuje wysyłanie nowe wystąpienie zła toohello połączenia. nie dotyczy Hello istniejących połączeń i nowych połączeń są wysyłane toohealthy wystąpień.

Role usługi w chmurze (role procesów roboczych oraz role sieci web) skorzystać agenta gościa w celu monitorowania sondowania. TCP lub HTTP niestandardowego sondy musi być skonfigurowany, korzystając z maszyn wirtualnych za usługą równoważenia obciążenia.

## <a name="understand-probe-count-and-timeout"></a>Licznik sondy i limit czasu

Zachowanie sondowania zależy od:

* Hello liczba pomyślnych sond, umożliwiających toobe wystąpienia oznaczone jako czas.
* Liczba Hello sond nie powiodło się, powodujących toobe wystąpienia etykietą w dół.

wartość limitu czasu i częstotliwość Hello w SuccessFailCount ustalić, czy wystąpienie jest potwierdzone toobe uruchomiona lub nie działa. W portalu Azure hello limit czasu hello jest wartość tootwo razy hello hello częstotliwości.

Witaj badania konfiguracji wszystkich wystąpień usługi równoważenia obciążenia dla punktu końcowego (czyli zestaw z równoważeniem obciążenia) musi być hello takie same. Oznacza to, nie może mieć konfiguracji różnych sondowania dla każdego wystąpienia roli lub maszyny wirtualnej w hello sam hostowanej usługi dla kombinacji danego punktu końcowego. Na przykład każde wystąpienie musi mieć identyczne porty lokalne i przekroczeń limitu czasu.

> [!IMPORTANT]
> Sonda modułu równoważenia obciążenia używa adresu IP hello 168.63.129.16. Ten publiczny adres IP umożliwia komunikację toointernal zasoby platformy hello Przełącz your właścicielem IP scenariusz sieci wirtualnej platformy Azure. Witaj wirtualnej publiczny adres IP 168.63.129.16 jest używany we wszystkich regionach i nie zmieni się. Firma Microsoft zaleca Zezwalaj ten adres IP w żadnych zasad zapory lokalnej. Go nie należy traktować jako zagrożenie bezpieczeństwa, ponieważ tylko hello wewnętrzny platformy Azure może pobierać wiadomości z tego adresu. Jeśli nie zrobisz, będzie nieoczekiwanego zachowania w różnych scenariuszy, takich jak konfigurowanie hello tego samego zakresu adresów IP 168.63.129.16 i mających zduplikowane adresy IP.

## <a name="learn-about-hello-types-of-probes"></a>Informacje o typach hello sondy

### <a name="guest-agent-probe"></a>Sondowanie agenta gościa

To sondowanie jest tylko dostępne dla usługi w chmurze Azure. Moduł równoważenia obciążenia, korzysta z agenta gościa hello wewnątrz hello maszyny wirtualnej i nasłuchuje i wysyła odpowiedź HTTP 200 OK tylko wtedy, gdy hello wystąpienie jest w stanie gotowe hello (to znaczy nie w innym stanu takich jak zajęty, odtwarzanie lub zatrzymywanie).

Aby uzyskać więcej informacji, zobacz [Konfigurowanie hello pliku definicji usługi (csdef) dla sondy kondycji](https://msdn.microsoft.com/library/azure/ee758710.aspx) lub [rozpocząć tworzenie internetowy równoważenia obciążenia dla usług w chmurze](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>Dzięki czemu sondowanie agenta gościa, Oznacz wystąpienia swój stan jako niezdrowy?

W przypadku niepowodzenia toorespond HTTP 200 OK agenta gościa hello znaczniki usługi równoważenia obciążenia hello hello wystąpienia jako odpowiadać i kończy działanie wysyłania ruchu toothat wystąpienia. Moduł równoważenia obciążenia Hello nadal tooping hello wystąpienia. Agent gościa hello odpowie 200 protokołu HTTP, usługi równoważenia obciążenia hello wysyła wystąpienia toothat ruchu ponownie.

Korzystając z roli sieci web, hello kodu witryny sieci Web jest zwykle działa w w3wp.exe, który nie jest monitorowane przez hello Azure sieci szkieletowej lub agenta gościa. To oznacza, że błędy w w3wp.exe (na przykład odpowiedzi HTTP 500) nie będzie toohello zgłoszone agenta gościa, a hello modułu równoważenia obciążenia nie będą brane danego wystąpienia poza obrotu.

### <a name="http-custom-probe"></a>Niestandardowe badanie HTTP

niestandardowe sondy modułu równoważenia obciążenia HTTP Hello przesłania sondowanie agenta gościa domyślne hello, co oznacza, możesz utworzyć własne niestandardowej logiki toodetermine hello kondycji hello wystąpienia roli. Moduł równoważenia obciążenia Hello sondy punktu końcowego co 15 s domyślnie. wystąpienie Hello jest uznawany za toobe rotacji usługi równoważenia obciążenia hello, jeśli odpowiada z 200 protokołu HTTP w hello limicie czasu (w sekundach 31 domyślnie).

Może to być przydatne w przypadku tooimplement własnego wystąpienia tooremove logiki z obrotu usługi równoważenia obciążenia. Można na przykład określić tooremove wystąpienia, jeśli jest ponad 90% zasobów Procesora i zwraca stan – 200. Jeśli masz role sieci web, które używają w3wp.exe, oznacza to też, możesz uzyskać automatyczne monitorowania witryny sieci Web, ponieważ błędów w kodzie witryny sieci Web, którą będzie zwracać sondę modułu równoważenia obciążenia toohello stan – 200.

> [!NOTE]
> Badanie niestandardowych Hello HTTP obsługuje ścieżek względnych i tylko protokołu HTTP. Protokół HTTPS nie jest obsługiwane.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>Co sprawia, że badanie niestandardowych HTTP oznaczyć swój stan jako niezdrowy wystąpienia?

* Witaj aplikacji HTTP zwraca kod odpowiedzi HTTP innych niż 200 (na przykład 403, 404 lub 500). To jest dodatnią potwierdzenia, że aplikacja hello wystąpienie powinno się znaleźć poza usługi od razu.
* Hello HTTP serwer nie odpowiada na wszystkich po hello limitu czasu. W zależności od wartość limitu czasu hello jest ustawiona, może to oznaczać tej sondy wielu żądań bez odpowiedzi przed hello sondowanie pobiera oznaczona jako nie działa z rzeczywistym użyciem (czyli przed SuccessFailCount sond są wysyłane).
* Serwer Hello zamyka hello połączenia za pośrednictwem resetowania TCP.

### <a name="tcp-custom-probe"></a>Niestandardowe sondowaniem TCP

Sondy protokołu TCP nawiązania połączenia, wykonując trójstopniowego z portem hello zdefiniowane.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>Dzięki czemu niestandardowy sondowaniem TCP oznaczyć swój stan jako niezdrowy wystąpienia?

* Witaj TCP serwer nie odpowiada na wszystkich po hello limit czasu. Gdy hello sondowania jest oznaczony jako nieuruchomiona zależy od hello liczba nieudanych sondowania żądania, które były skonfigurowane toogo bez odpowiedzi, zanim oznaczysz sondowania hello jako nie działa.
* Sonda Hello odbiera TCP zresetować z hello wystąpienia roli.

Aby uzyskać więcej informacji o konfigurowaniu sondy kondycji protokołu HTTP lub sondowaniem TCP, zobacz [rozpocząć tworzenie internetowy równoważenia obciążenia w Menedżerze zasobów przy użyciu programu PowerShell](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>Dodaj dobrej kondycji wystąpień do obrotu usługi równoważenia obciążenia

TCP i HTTP są traktowane jako dobrej kondycji i oznacz hello wystąpienia roli co w przypadku dobrej kondycji:

* Moduł równoważenia obciążenia Hello pobiera dodatnią sondowania hello pierwszego czasu powitalne rozruchu maszyny Wirtualnej.
* Liczba Hello SuccessFailCount (opisanym wcześniej) określa wartość hello pomyślne sond, które są wymagane toomark wystąpienia roli hello w dobrej kondycji. Jeśli usunięto wystąpienia roli, hello liczbę sond pomyślne, kolejne musi równa lub przekracza wartość hello wystąpienia roli hello toomark SuccessFailCount jako uruchomione.

> [!NOTE]
> Jeśli kondycji hello wystąpienia roli jest zmienne, usługi równoważenia obciążenia hello oczekuje już przed wprowadzeniem wystąpienia roli hello w dobrej kondycji hello. Jest to realizowane za pośrednictwem zasad tooprotect hello użytkownika i infrastruktura hello.

## <a name="use-log-analytics-for-load-balancer"></a>Użyj analizy dzienników dla usługi równoważenia obciążenia

Można użyć [logowania dla usługi równoważenia obciążenia analytics](load-balancer-monitor-log.md) toocheck na powitania sondy kondycji stanu i badania count. Rejestrowanie można łączyć z usługi Power BI lub usługi Azure Operational Insights tooprovide Statystyka stanu kondycji modułu równoważenia obciążenia.
