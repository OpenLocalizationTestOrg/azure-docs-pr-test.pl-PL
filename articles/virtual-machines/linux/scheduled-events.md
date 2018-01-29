---
title: Zaplanowane zdarzenia dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Planowanie zdarzeń za pomocą usługi metadanych platformy Azure dla maszyn wirtualnych systemu Linux."
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
ms.openlocfilehash: ae9955253647f3277729e7905baf7bb07645de42
ms.sourcegitcommit: 0e1c4b925c778de4924c4985504a1791b8330c71
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/06/2018
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Usługa Azure metadanych: Zaplanowanego zdarzenia (wersja zapoznawcza) dla maszyn wirtualnych systemu Linux

> [!NOTE] 
> Podglądy są udostępniane użytkownikowi, pod warunkiem że wyrażasz zgodę na warunki użytkowania. Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Zaplanowane zdarzenia jest subservice w ramach usługi metadanych platformy Azure, określające czas aplikacji do przygotowania do obsługi maszyny wirtualnej (VM). Zawiera informacje na temat zdarzeń planowanych konserwacji (na przykład ponowny rozruch), aby przygotować je i ograniczyć aplikacji przerw w działaniu. Jest ona dostępna dla wszystkich typów maszyn wirtualnych platformy Azure, w tym PaaS i IaaS w systemach Windows i Linux. 

Informacji o zaplanowane zdarzeń w systemie Windows, temacie [zaplanowane zdarzenia dla maszyn wirtualnych systemu Windows](../windows/scheduled-events.md).

## <a name="why-use-scheduled-events"></a>Dlaczego warto używać zaplanowane zdarzenia?

Wiele aplikacji może skorzystać z czasu na przygotowanie wirtualna konserwacji. Czas może służyć do wykonywania zadań specyficznych dla aplikacji, które zwiększenia dostępności, niezawodności i użytkowanie, w tym: 

- Punkt kontrolny i przywracania.
- Opróżnianie połączenia.
- Tryb pracy awaryjnej replikę podstawową.
- Usuwanie z puli usługi równoważenia obciążenia.
- Rejestrowanie zdarzeń.
- Łagodne zamykanie.

Zaplanowane zdarzenia aplikacja może odnajdywać podczas konserwacji będą występować i wyzwolić zadań, aby ograniczyć jej wpływ.  

Zaplanowane zdarzenia zawiera zdarzenia w następujących przypadkach użycia:

- Zainicjowano platformy obsługi (na przykład aktualizacji systemu operacyjnego hosta)
- Użytkownik zainicjował konserwacji (na przykład, ponownego uruchamiania lub wdraża ponownie maszyny Wirtualnej)

## <a name="the-basics"></a>Podstawy  

  Metadane usługi przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST, który jest dostępny z poziomu maszyny Wirtualnej. Informacje są dostępne za pośrednictwem nonroutable IP, dzięki czemu nie jest uwidaczniana poza maszyny Wirtualnej.

### <a name="scope"></a>Zakres
Zaplanowane zdarzenia są dostarczane do:

- Wszystkie maszyny wirtualne w usłudze w chmurze.
- Wszystkich maszyn wirtualnych w zestawie dostępności.
- Wszystkie maszyny wirtualne w grupie umieszczania zestaw skali. 

Sprawdź, w związku z tym `Resources` pola w zdarzeniu do identyfikowania dotyczy które maszyn wirtualnych.

### <a name="discover-the-endpoint"></a>Odnajdywanie punktu końcowego
Dla maszyn wirtualnych, które są włączone dla sieci wirtualnych jest pełna punktu końcowego dla najnowszej wersji zaplanowane zdarzenia: 

 > `http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01`

W przypadku których maszyny Wirtualnej jest tworzona w ramach sieci wirtualnej, jest dostępna z nonroutable statycznego adresu IP, usługi metadanych `169.254.169.254`.
Jeśli maszyna wirtualna nie jest tworzony w ramach sieci wirtualnej, a domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest wymagany, aby odnaleźć adres IP do użycia. Aby dowiedzieć się, jak [odnajdywanie punktu końcowego hosta](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm), zobacz ten przykład.

### <a name="versioning"></a>Obsługa wersji 
Usługa zaplanowane zdarzenia jest kontrolą wersji. Wersje są obowiązkowe, a bieżąca wersja to `2017-08-01`.

| Wersja | Informacje o wersji | 
| - | - | 
| 2017-08-01 | <li> Usunięte dołączany początku podkreślenia z nazwy zasobów dla maszyn wirtualnych Iaas<br><li>Wymaganie nagłówka metadanych wymuszone dla wszystkich żądań | 
| 2017-03-01 | <li>W wersji zapoznawczej


> [!NOTE] 
> Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api. Ten format jest już obsługiwane i zostaną wycofane w przyszłości.

### <a name="use-headers"></a>Użyj nagłówków
Kwerenda usługi metadanych, należy określić nagłówek `Metadata:true` zapewnienie żądania przypadkowo nie został przekierowany. `Metadata:true` Nagłówek jest wymagany dla wszystkich żądań zaplanowanego zdarzenia. Nie można dołączyć nagłówka w żądaniu wynikiem "Złe żądanie" odpowiedź z usługi metadanych.

### <a name="enable-scheduled-events"></a>Włącz zaplanowane zdarzenia
Utwórz żądanie zaplanowanego zdarzenia po raz pierwszy Azure niejawnie włączy tę funkcję na maszynie Wirtualnej. W związku z tym mogą pojawić się odpowiedzi opóźnione w Twoje pierwsze wywołanie do dwóch minut.

> [!NOTE]
> Zaplanowane zdarzenia jest automatycznie wyłączana dla usługi, jeśli usługi nie wymagają punktu końcowego jeden dzień. Po wyłączeniu zaplanowane zdarzeń dla usługi zdarzenia nie są tworzone dla obsługi inicjowanych przez użytkownika.

### <a name="user-initiated-maintenance"></a>Użytkownik zainicjował konserwacji
Użytkownik zainicjował konserwacji maszyny Wirtualnej za pomocą portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell powoduje zaplanowane zdarzenie. Następnie można przetestować logiki przygotowania konserwacji w aplikacji, a aplikacja można przygotować do obsługi inicjowanych przez użytkownika.

Jeśli ponowne uruchomienie maszyny Wirtualnej, z typem zdarzenia `Reboot` zostało zaplanowane. Jeśli ponownego wdrażania maszyny Wirtualnej, z typem zdarzenia `Redeploy` zostało zaplanowane.

> [!NOTE] 
> Obecnie maksymalnie 100 operacji konserwacji zainicjowane przez użytkownika można jednocześnie zaplanować.

> [!NOTE] 
> Zainicjowane przez użytkownika konserwacji, który daje w zaplanowanych zdarzeń nie jest obecnie można konfigurować. Konfigurowalne jest planowane w przyszłości.

## <a name="use-the-api"></a>Za pomocą interfejsu API

### <a name="query-for-events"></a>Zapytania do zdarzenia
Za pomocą następujących wywołania mogą wykonywać kwerendę o zaplanowane zdarzenia:

#### <a name="bash"></a>Bash
```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01
```

Odpowiedź zawiera tablicę zaplanowanego zdarzenia. Pusta tablica oznacza to, czy obecnie żadne zdarzenia nie zostały zaplanowane.
W przypadku w przypadku zaplanowanego zdarzenia odpowiedzi zawiera tablicę zdarzeń. 
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
| Typ zdarzenia | Wpływ powoduje, że to zdarzenie. <br><br> Wartości: <br><ul><li> `Freeze`: Planowane maszyna wirtualna jest wstrzymywać w kilka sekund. Procesor jest wstrzymana, ale nie nie wpływa na pamięć, otwartych plików lub połączeń sieciowych. <li>`Reboot`: Maszyna wirtualna jest zaplanowane na ponowne uruchomienie komputera. (Nietrwałych pamięci jest utracone). <li>`Redeploy`: Planowane maszyna wirtualna jest przeniesienie do innego węzła. (Tymczasowych dyski zostaną utracone.) |
| ResourceType | Typ zasobu, którego dotyczy to zdarzenie. <br><br> Wartości: <ul><li>`VirtualMachine`|
| Zasoby| Lista zasobów, których dotyczy to zdarzenie. Listy jest gwarantowana zawiera maszyny z co najwyżej jeden [domeny aktualizacji](manage-availability.md), ale mogą nie zawierać wszystkich maszyn w UD. <br><br> Przykład: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Obiektu EventStatus | Stan tego zdarzenia. <br><br> Wartości: <ul><li>`Scheduled`: To zdarzenie jest zaplanowane do uruchomienia po upływie czasu określonego w `NotBefore` właściwości.<li>`Started`: To zdarzenie zostało rozpoczęte.</ul> Nie `Completed` lub podobne stan kiedykolwiek jest dostępne. Zdarzenie nie jest zwracana po zakończeniu zdarzenia.
| Nie wcześniej niż| Czas, po którym można uruchomić tego zdarzenia. <br><br> Przykład: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Planowanie zdarzeń
Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości zależy od typu zdarzenia. Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości. 

|Typ zdarzenia  | Minimalna powiadomień |
| - | - |
| Blokowanie| 15 minut |
| Ponowne uruchamianie | 15 minut |
| Ponowne wdrożenie | 10 minut |

### <a name="start-an-event"></a>Uruchomić zdarzenie 

Po Dowiedz się o nadchodzących zdarzenia i Zakończ logiki dla łagodne zamykanie należy zatwierdzić zaległych zdarzeń dokonując `POST` wywołanie usługi metadanych z `EventId`. To wywołanie wskazuje na platformie Azure, skrócić minimalna powiadomień czasu (jeśli jest to możliwe). 

W poniższym przykładzie JSON jest oczekiwany w `POST` treść żądania. Żądanie powinno zawierać listę `StartRequests`. Każdy `StartRequest` zawiera `EventId` dla zdarzeń, aby przyspieszyć:
```
{
    "StartRequests" : [
        {
            "EventId": {EventId}
        }
    ]
}
```

#### <a name="bash-sample"></a>Przykładowe bash
```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01
```

> [!NOTE] 
> Potwierdzeniem zdarzenia umożliwia zdarzeń w przypadku wszystkich `Resources` w przypadku, nie tylko maszynę Wirtualną, która potwierdza zdarzenia. W związku z tym można wybrać wiodące do koordynowania potwierdzenia, która może być tak proste, jak pierwszy komputer w `Resources` pola.

## <a name="python-sample"></a>Przykładowe Python 

Poniższy przykład wysyła zapytanie metadanych usługi zaplanowanego zdarzenia i zatwierdza każdego zaległe zdarzenia:

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01"
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
            print "+ Scheduled Event. This host " + this_host + " is scheduled for " + eventtype + " not before " + notbefore
            # Add logic for handling events here


def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)

if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Kolejne kroki 
- Przejrzyj przykłady kodu zaplanowane zdarzenia w [repozytorium Github narzędzia Azure wystąpienie metadanych zaplanowane zdarzenia](https://github.com/Azure-Samples/virtual-machines-scheduled-events-discover-endpoint-for-non-vnet-vm).
- Przeczytaj więcej na temat interfejsów API, które są dostępne w [wystąpienia usługi metadanych](instance-metadata-service.md).
- Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure](planned-maintenance.md).
