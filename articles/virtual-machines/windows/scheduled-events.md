---
title: Zaplanowane zdarzenia dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Zaplanowane zdarzenia przy użyciu usługi Azure metadanych dla na maszynach wirtualnych systemu Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: 75e811f77bade3701cce2d9945cf35d6e14e376f
ms.sourcegitcommit: 7f1ce8be5367d492f4c8bb889ad50a99d85d9a89
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Usługa Azure metadanych: Zaplanowanego zdarzenia (wersja zapoznawcza) dla maszyn wirtualnych systemu Windows

> [!NOTE] 
> Podglądy są udostępniane użytkownikowi, pod warunkiem że wyrażasz zgodę na warunki użytkowania. Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Zaplanowane zdarzenia jest usługą metadanych Azure, która zapewnia czasu aplikacji do przygotowania do obsługi maszyny wirtualnej. Zawiera informacje na temat zdarzeń planowanych konserwacji (np. Uruchom ponownie), aplikacja może przygotować je i ograniczyć przerw w działaniu. Jest ona dostępna dla wszystkich typów maszyny wirtualnej platformy Azure, w tym PaaS i IaaS w systemach Windows i Linux. 

Informacje o zdarzeniach zaplanowane w systemie Linux, zobacz [zaplanowane zdarzenia dla maszyn wirtualnych systemu Linux](../linux/scheduled-events.md).

## <a name="why-scheduled-events"></a>Dlaczego zaplanowane zdarzenia?

Wiele aplikacji może skorzystać z czasu, aby przygotować się do obsługi maszyny wirtualnej. Czas może służyć do wykonywania określonych zadań aplikacji, które zwiększenia dostępności, niezawodności i użytkowanie w tym: 

- Punkt kontrolny i przywracania
- Opróżnianie połączenia
- Pracy awaryjnej replikę podstawową 
- Usunięcie z puli usługi równoważenia obciążenia
- Rejestrowanie zdarzeń
- Łagodne zamykanie 

W przypadku używania zaplanowane zdarzeń aplikacji może odnajdywać podczas konserwacji będą występować i wyzwolić zadań, aby ograniczyć jej wpływ.  

Zaplanowane zdarzenia zawiera zdarzenia w następujących przypadkach użycia:
- Platforma zainicjował konserwacji (np. aktualizacji systemu operacyjnego hosta)
- Użytkownik zainicjował konserwacji (np. ponownego uruchamiania lub wdraża ponownie maszyny Wirtualnej)

## <a name="the-basics"></a>Podstawy  

Usługa Azure metadanych przedstawia informacje o uruchamianiu maszyn wirtualnych przy użyciu punkt końcowy REST jest dostępny z poziomu maszyny Wirtualnej. Informacje są dostępne za pośrednictwem IP bez obsługi routingu, dzięki czemu nie jest uwidaczniana poza maszyny Wirtualnej.

### <a name="scope"></a>Zakres
Zaplanowane zdarzenia są dostarczane do:
- Wszystkie maszyny wirtualne w usłudze w chmurze
- Wszystkie maszyny wirtualne w zestawie dostępności
- Wszystkie maszyny wirtualne w grupie umieszczania zestaw skali. 

W związku z tym należy sprawdzić `Resources` w zdarzenia w celu określenia, na które będzie to mieć wpływ na maszynach wirtualnych. 

## <a name="discovering-the-endpoint"></a>Odnajdywanie punktu końcowego
Dla sieci Wirtualnej włączone maszyn wirtualnych, jest pełna punktu końcowego dla najnowszej wersji zaplanowane zdarzenia: 

 > `http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01`

W przypadku, gdy utworzono maszynę wirtualną w sieć wirtualną (VNet), usługa metadanych jest dostępne ze statycznego adresu IP bez obsługi routingu, `169.254.169.254`.
Jeśli maszyna wirtualna nie została utworzona w ramach sieci wirtualnej, a domyślnym czcionkom dla usługi w chmurze i klasycznych maszyn wirtualnych, dodatkową logikę jest wymagany, aby odnaleźć adres IP do użycia. Odwołuje się do poniższego przykładu, aby dowiedzieć się, jak [odnajdywanie punktu końcowego hosta](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Obsługa wersji 
Usługa zdarzeń zaplanowane jest kontrolą wersji. Wersje są obowiązkowe i bieżąca wersja to `2017-08-01`.

| Wersja | Informacje o wersji | 
| - | - | 
| 2017-08-01 | <li> Usunięte dołączany początku podkreślenia z nazwy zasobów dla maszyn wirtualnych Iaas<br><li>Wymaganie nagłówek metadanych wymuszone dla wszystkich żądań | 
| 2017-03-01 | <li>W wersji zapoznawczej

> [!NOTE] 
> Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api. Ten format jest już obsługiwane i zostaną wycofane w przyszłości.

### <a name="using-headers"></a>Korzystanie z nagłówków
Kwerenda usługi metadanych, należy określić nagłówek `Metadata:true` aby upewnić się, żądanie nie zostało przekierowane przypadkowo. `Metadata:true` Nagłówek jest wymagany dla wszystkich żądań zaplanowanego zdarzenia. Nie można dołączyć nagłówka w żądaniu spowoduje nieprawidłowe żądanie odpowiedzi z metadanych usługi.

### <a name="enabling-scheduled-events"></a>Włączanie zaplanowanego zdarzenia
Utwórz żądanie zaplanowanego zdarzenia po raz pierwszy Azure niejawnie włączy tę funkcję na maszynie wirtualnej. W związku z tym spodziewać opóźnione odpowiedzi w Twoje pierwsze wywołanie do dwóch minut.

> [!NOTE]
> Zaplanowane zdarzenia jest automatycznie wyłączana dla usługi, jeśli usługi nie wymagają punkt końcowy 1 dzień. Po wyłączeniu zaplanowane zdarzeń dla usługi nie będą istnieć żadne zdarzenia utworzone dla obsługi inicjowanych przez użytkownika.

### <a name="user-initiated-maintenance"></a>Konserwacja zainicjowanej przez użytkownika
Użytkownik zainicjował konserwacji maszyny wirtualnej za pośrednictwem portalu Azure, interfejsu API, interfejsu wiersza polecenia lub środowiska PowerShell powoduje zaplanowane zdarzenie. To umożliwia przetestowanie logiki przygotowania konserwacji w aplikacji oraz umożliwia aplikacji w taki sposób przygotować się do obsługi inicjowanych przez użytkownika.

Ponowne uruchomienie maszyny wirtualnej planuje zdarzenia z typem `Reboot`. Ponownego wdrażania maszyny wirtualnej planuje zdarzenia z typem `Redeploy`.

> [!NOTE] 
> Obecnie maksymalnie 100 operacji konserwacji zainicjowanej przez użytkownika można jednocześnie zaplanować.

> [!NOTE] 
> Wynikiem zaplanowane zdarzenia konserwacji zainicjowanej przez użytkownika nie jest obecnie można konfigurować. Konfigurowalne jest planowane w przyszłości.

## <a name="using-the-api"></a>Korzystanie z interfejsu API

### <a name="query-for-events"></a>Zapytania do zdarzenia
Mogą wykonywać kwerendę o zaplanowane zdarzenia po prostu, wprowadzając następujące wywołanie:

#### <a name="powershell"></a>PowerShell
```
curl http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01 -H @{"Metadata"="true"}
```

Odpowiedź zawiera tablicę zaplanowanego zdarzenia. Pusta tablica oznacza, że obecnie nie istnieją żadne zdarzenia według harmonogramu.
W przypadku w przypadku zaplanowanego zdarzenia odpowiedzi zawiera tablicę zdarzeń: 
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
| Typ zdarzenia | Wpływ powoduje, że to zdarzenie. <br><br> Wartości: <br><ul><li> `Freeze`: Planowane maszyny wirtualnej jest wstrzymywać w kilka sekund. Procesor jest wstrzymana, ale nie ma żadnego wpływu na pamięć, otwartych plików lub połączeń sieciowych. <li>`Reboot`: Ponowne uruchomienie zaplanowano maszyny wirtualnej (z systemem innym niż trwałej pamięci jest utracone). <li>`Redeploy`: Zaplanowano maszynę wirtualną można przenieść do innego węzła (tymczasowych dyski zostaną utracone). |
| ResourceType | Typ zasobu, który ma wpływ na to zdarzenie. <br><br> Wartości: <ul><li>`VirtualMachine`|
| Zasoby| Lista zasobów, które ma wpływ na to zdarzenie. Gwarantuje zawiera maszyny z co najwyżej jeden [domeny aktualizacji](manage-availability.md), ale nie może zawierać wszystkie maszyny w UD. <br><br> Przykład: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Stan zdarzenia | Stan tego zdarzenia. <br><br> Wartości: <ul><li>`Scheduled`: To zdarzenie jest zaplanowane do uruchomienia po upływie czasu określonego w `NotBefore` właściwości.<li>`Started`: To zdarzenie zostało rozpoczęte.</ul> Nie `Completed` lub podobne stan kiedykolwiek jest dostarczana, zdarzenie nie zostanie zwrócony po zakończeniu zdarzenia.
| Nie wcześniej niż| Czas, po którym to zdarzenie może zostać uruchomiony. <br><br> Przykład: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Planowanie zdarzeń
Zaplanowano każdego zdarzenia minimalna ilość czasu w przyszłości oparty na typie zdarzenia. Ten czas jest odzwierciedlone w zdarzeniu `NotBefore` właściwości. 

|Typ zdarzenia  | Minimalna powiadomień |
| - | - |
| Blokowanie| 15 minut |
| Ponowne uruchamianie | 15 minut |
| Ponowne wdrożenie | 10 minut |

### <a name="starting-an-event"></a>Uruchamianie zdarzenia 

Po rozpoznane nadchodzących zdarzenia i ukończyć logiki dla łagodne zamykanie należy zatwierdzić zaległych zdarzeń dokonując `POST` wywołanie usługi metadanych z `EventId`. To wskazuje na platformie Azure skrócić minimalna powiadomień czasu (jeśli jest to możliwe). 

Poniżej znajduje się w formacie json `POST` treść żądania. Żądanie powinno zawierać listę `StartRequests`. Każdy `StartRequest` zawiera `EventId` dla zdarzeń, aby przyspieszyć:
```
{
    "StartRequests" : [
        {
            "EventId": {EventId}
        }
    ]
}
```

#### <a name="powershell"></a>PowerShell
```
curl -H @{"Metadata"="true"} -Method POST -Body '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' -Uri http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01
```

> [!NOTE] 
> Potwierdzeniem zdarzenia umożliwia zdarzeń w przypadku wszystkich `Resources` w przypadku, nie tylko w maszynie wirtualnej, który potwierdza zdarzenia. W związku z tym można wybrać opcję wybiera wiodące do koordynowania potwierdzenia, które mogą być prosta jako maszynę pierwszej w `Resources` pola.


## <a name="powershell-sample"></a>Przykładowe programu PowerShell 

Poniższy przykład korzysta z usługi metadanych dla zaplanowanych zdarzeń i zatwierdza każdego zdarzenia oczekujące.

```PowerShell
# How to get scheduled events 
function Get-ScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function Approve-ScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function Handle-ScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = Get-ScheduledEvents $scheduledEventURI

# Handle events however is best for your service
Handle-ScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        Approve-ScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 

## <a name="next-steps"></a>Następne kroki 

- Przejrzyj przykłady kodu zaplanowane zdarzenia w [repozytorium Github Azure wystąpienie metadanych zaplanowane zdarzenia](https://github.com/Azure-Samples/virtual-machines-scheduled-events-discover-endpoint-for-non-vnet-vm)
- Dowiedz się więcej o interfejsami API dostępnymi w [metadanych wystąpienia usługi](instance-metadata-service.md).
- Dowiedz się więcej o [zaplanowanej konserwacji dla maszyn wirtualnych systemu Windows Azure](planned-maintenance.md).
