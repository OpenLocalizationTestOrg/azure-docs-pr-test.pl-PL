---
title: aaaScheduled zdarzenia dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Zaplanowane zdarzenia przy użyciu usługi Azure metadanych hello pakietu na maszynach wirtualnych systemu Linux."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Usługa Azure metadanych: Zaplanowanego zdarzenia (wersja zapoznawcza) dla maszyn wirtualnych systemu Linux

> [!NOTE] 
> Podglądy odbywa się dostępne tooyou warunku hello zgadzają się toohello warunki użytkowania. Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Zaplanowane zdarzenia jest jednym z subservices hello w obszarze hello Azure metadanych usługi. Jest odpowiedzialny za udostępniając informacje dotyczące zdarzeń nadchodzących (na przykład ponowny rozruch), aplikacja może przygotować je i ograniczyć przerw w działaniu. Jest ona dostępna dla wszystkich typów maszyny wirtualnej platformy Azure, w tym PaaS i IaaS. Zaplanowane zdarzenia daje zadań zapobiegawczych tooperform czasu maszyny wirtualnej efekt hello toominimize zdarzenia. 

Zaplanowane zdarzenia jest dostępna dla systemów Windows i maszyn wirtualnych systemu Linux. Informacji o zaplanowane zdarzeń w systemie Windows, temacie [zaplanowane zdarzenia dla maszyn wirtualnych systemu Windows](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Dlaczego zaplanowane zdarzenia?

Zaplanowane zdarzenia należy wykonać czynności wpływ hello toolimit intiated platformy konserwacji lub akcje inicjowane przez użytkownika w usłudze. 

Mająca wiele wystąpień obciążeń wykorzystujących stan toomaintain techniki replikacji mogą być narażone toooutages wykonywane w wielu wystąpieniach. Takie jak awarie może spowodować kosztowne zadania (na przykład odbudowywania indeksów) lub nawet utraty repliki. 

W wielu innych przypadkach hello ogólnej dostępności usługi mogą być ulepszane, wykonując takie jak sekwencji łagodne zamykanie Kończenie (lub anulowanie) locie transakcji, ponowne przypisywanie zadań tooother maszyn wirtualnych w klastrze hello (ręcznego przełączania trybu failover) lub usunięcie hello Maszyna wirtualna z puli usługi równoważenia obciążenia sieciowego. 

Istnieją przypadki, w którym powiadamianie o tym administratora o nadchodzących zdarzenia lub rejestrowanie takie zdarzenia pomocy poprawy hello użytkowanie hostowanych w chmurze hello.

Przypadki użycia Azure usługi metadanych powierzchni zaplanowane zdarzenia w następujących hello:
-   Platforma zainicjował konserwacji (na przykład wdrożenie systemu operacyjnego hosta)
-   Wywołania zainicjowane przez użytkownika (na przykład użytkownik zostanie ponownie uruchomiony lub wdraża ponownie maszyny Wirtualnej)


## <a name="hello-basics"></a>podstawy Hello  

Usługa Azure metadanych przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST jest dostępny w obrębie hello maszyny Wirtualnej. informacje Hello są dostępne za pośrednictwem bez obsługi routingu IP, dzięki czemu nie jest uwidaczniana poza hello maszyny Wirtualnej.

### <a name="scope"></a>Zakres
Zaplanowane zdarzenia są udostępniane tooall maszyn wirtualnych w usłudze w chmurze lub tooall maszyn wirtualnych w zestawie dostępności. W związku z tym należy sprawdzić hello `Resources` w hello tooidentify zdarzenia, które maszyny wirtualne mają wpływ na toobe. 

### <a name="discovering-hello-endpoint"></a>Odnajdywanie punktu końcowego hello
W przypadku hello, w którym utworzono maszynę wirtualną w sieć wirtualną (VNet), usługa metadanych hello jest dostępna z statycznego adresu IP bez obsługi routingu, `169.254.169.254`.
Jeśli nie utworzono hello maszyny wirtualnej w ramach sieci wirtualnej, hello domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest wymagane toodiscover hello punktu końcowego toouse. Można znaleźć toolearn próbki toothis jak zbyt[odnajdywanie punktu końcowego hosta hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Przechowywanie wersji 
Witaj wystąpienia usługi metadanych jest kontrolą wersji. Wersje są obowiązkowe i hello bieżąca wersja to `2017-03-01`.

> [!NOTE] 
> Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api hello. Ten format jest już obsługiwane i zostaną wycofane w przyszłości hello.

### <a name="using-headers"></a>Korzystanie z nagłówków
Kwerenda hello metadanych usługi, należy określić nagłówek hello `Metadata: true` tooensure hello żądania nie został przypadkowo przekierowany.

### <a name="enabling-scheduled-events"></a>Włączanie zaplanowanego zdarzenia
Witaj po raz pierwszy wprowadzone żądania zaplanowanego zdarzenia Azure niejawnie włącza hello funkcji na maszynie wirtualnej. W związku z tym spodziewać opóźnione odpowiedzi w pierwszym wywołaniu się tootwo minut.

### <a name="user-initiated-maintenance"></a>Konserwacja zainicjowanej przez użytkownika
Użytkownik zainicjował konserwacji maszyny wirtualnej za pomocą hello portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell powoduje zaplanowane zdarzenie. Umożliwia tootest hello konserwacji przygotowania logikę w aplikacji i pozwala tooprepare Twojej aplikacji do obsługi inicjowanych przez użytkownika.

Ponowne uruchomienie maszyny wirtualnej planuje zdarzenia z typem `Reboot`. Ponownego wdrażania maszyny wirtualnej planuje zdarzenia z typem `Redeploy`.

> [!NOTE] 
> Obecnie maksymalnie 10 operacji konserwacji zainicjowanej przez użytkownika można jednocześnie zaplanować. Ten limit zostanie złagodzony przed zaplanowane zdarzenia ogólnej dostępności.

> [!NOTE] 
> Wynikiem zaplanowane zdarzenia konserwacji zainicjowanej przez użytkownika nie jest obecnie można konfigurować. Konfigurowalne jest planowane w przyszłości.

## <a name="using-hello-api"></a>Przy użyciu interfejsu API hello

### <a name="query-for-events"></a>Zapytania do zdarzenia
Po prostu, wprowadzając następujące hello wywołania mogą wykonywać kwerendę o zaplanowane zdarzenia:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Odpowiedź zawiera tablicę zaplanowanego zdarzenia. Pusta tablica oznacza, że obecnie nie istnieją żadne zdarzenia według harmonogramu.
W przypadku hello w przypadku zaplanowanego zdarzenia odpowiedź hello zawiera tablicę zdarzeń: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Właściwości zdarzenia
|Właściwość  |  Opis |
| - | - |
| Identyfikator zdarzenia | Globalnie unikatowy identyfikator dla tego zdarzenia. <br><br> Przykład: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| Typ zdarzenia | Wpływ powoduje, że to zdarzenie. <br><br> Wartości: <br><ul><li> `Freeze`: hello maszyny wirtualnej jest zaplanowane toopause kilka sekund. Witaj procesora CPU jest wstrzymana, ale nie ma żadnego wpływu na pamięć, otwartych plików lub połączeń sieciowych. <li>`Reboot`: hello zaplanowano ponownego uruchomienia maszyny wirtualnej (z systemem innym niż trwałej pamięci jest utracone). <li>`Redeploy`: hello maszyny wirtualnej jest zaplanowane toomove tooanother węzła (tymczasowych dyski zostaną utracone). |
| ResourceType | Typ zasobu, który ma wpływ na to zdarzenie. <br><br> Wartości: <ul><li>`VirtualMachine`|
| Zasoby| Lista zasobów, które ma wpływ na to zdarzenie. Gwarantuje toocontain maszyny z co najwyżej jeden [domeny aktualizacji](manage-availability.md), ale nie może zawierać wszystkie maszyny w hello UD. <br><br> Przykład: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Stan zdarzenia | Stan tego zdarzenia. <br><br> Wartości: <ul><li>`Scheduled`: To zdarzenie jest zaplanowane toostart po hello czas określony w hello `NotBefore` właściwości.<li>`Started`: To zdarzenie zostało rozpoczęte.</ul> Nie `Completed` lub podobne stan kiedykolwiek jest dostarczana, zdarzenia hello już zostaną zwrócone, po zakończeniu hello zdarzeń.
| Nie wcześniej niż| Czas, po którym to zdarzenie może zostać uruchomiony. <br><br> Przykład: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Planowanie zdarzeń
Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości hello na podstawie zdarzeń typu. Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości. 

|Typ zdarzenia  | Minimalna powiadomień |
| - | - |
| Blokowanie| 15 minut |
| Ponowne uruchamianie | 15 minut |
| Ponowne wdrożenie | 10 minut |

### <a name="starting-an-event"></a>Uruchamianie zdarzenia 

Po rozpoznane nadchodzących zdarzenia i ukończyć logiki dla łagodne zamykanie należy zatwierdzić hello zaległych zdarzeń dokonując `POST` wywołania toohello metadanych usługi z hello `EventId`. Wskazuje tooAzure skrócić powiadomień minimalna hello czasu (jeśli jest to możliwe). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Potwierdzeniem zdarzenia umożliwia hello tooproceed zdarzeń dla wszystkich `Resources` w zdarzeniu hello hello nie tylko maszynę wirtualną, która potwierdza hello zdarzeń. W związku z tym można tooelect wiodące toocoordinate hello potwierdzenia, które mogą być prosta jako maszynę pierwszej hello na powitania `Resources` pola.




## <a name="python-sample"></a>Przykładowe Python 

Witaj następujące przykładowe zapytania hello metadane usługi dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Następne kroki 

- Dowiedz się więcej o hello interfejsami API dostępnymi w hello [metadanych wystąpienia usługi](instance-metadata-service.md).
- Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure](planned-maintenance.md).
