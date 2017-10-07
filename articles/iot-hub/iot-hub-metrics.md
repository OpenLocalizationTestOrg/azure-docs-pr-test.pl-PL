---
title: aaaUse metryki toomonitor Centrum IoT Azure | Dokumentacja firmy Microsoft
description: "Jak toouse Centrum IoT Azure metryki tooassess i monitor hello ogólną kondycję Twojego centra IoT."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>Zrozumienie metryki Centrum IoT
Centrum IoT metryk umożliwiają lepsze danych o stanie hello hello Azure IoT zasobów w Twojej subskrypcji platformy Azure. Włącz metryki Centrum IoT można tooassess hello ogólną kondycję hello usługi Centrum IoT i urządzeniami hello połączone tooit. Statystyki dla użytkownika są ważne, ponieważ pomagają Zobacz, co się dzieje z IoT hub i pomocy głównej przyczyny problemów związanych z bez konieczności toocontact pomocy technicznej platformy Azure.

Metryki są domyślnie włączone. Można wyświetlić metryki Centrum IoT z hello portalu Azure.

## <a name="how-tooview-iot-hub-metrics"></a>Jak tooview metryki Centrum IoT
1. Tworzenie Centrum IoT. Instrukcje można znaleźć na temat toocreate Centrum IoT w hello [wprowadzenie] [ lnk-get-started] przewodnik.
2. Otwiera blok hello Centrum IoT. Z tego miejsca, kliknij przycisk **metryki**.
   
    ![][1]
3. W bloku metryki hello można wyświetlić metryki hello Centrum IoT i tworzenie niestandardowych widoków Twoje metryki. Możesz wybrać toosend punktu końcowego usługi Event Hubs tooan danych metryk lub konta usługi Azure Storage, klikając **ustawień diagnostycznych**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>Centrum IoT metryki i w jaki sposób toouse ich
Centrum IoT zawiera kilka miar toogive Przegląd kondycji hello koncentratora i hello całkowitej liczby urządzeń podłączonych. Możesz łączyć informacji z wielu toopaint metryki pełny obraz powitania stanu hello Centrum IoT. Witaj w poniższej tabeli opisano metryki hello, który śledzi każdego centrum IoT i jak wszystkie metryki odnosi się toohello ogólny stan hello Centrum IoT.

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Próby wysłania wiadomości telemetrii|Licznik|Łącznie|Liczba toobe próba telemetrii urządzenia do chmury wiadomości wysłanych tooyour Centrum IoT|
|d2c.telemetry.ingress.SUCCESS|Wysłane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury wysłana pomyślnie tooyour Centrum IoT|
|c2d.Commands.egress.COMPLETE.SUCCESS|Polecenia zakończona|Licznik|Łącznie|Liczba poleceń chmury do urządzenia zakończyło się powodzeniem, hello urządzenia|
|c2d.Commands.egress.Abandon.SUCCESS|Porzucone poleceń|Licznik|Łącznie|Porzucone przez urządzenie hello polecenia chmury do urządzenia|
|c2d.Commands.egress.Reject.SUCCESS|Polecenia odrzucone|Licznik|Łącznie|Liczba odrzuconych przez urządzenie hello poleceń chmury do urządzenia|
|devices.totalDevices|Łączna liczba urządzeń|Licznik|Łącznie|Liczba urządzeń zarejestrowanych w Centrum IoT tooyour|
|devices.connectedDevices.allProtocol|Połączonych urządzeń|Licznik|Łącznie|Liczba urządzeń podłączonych tooyour Centrum IoT|
|d2c.telemetry.egress.SUCCESS|Dostarczane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów pomyślnie zostały napisane tooendpoints (łącznie)|
|d2c.telemetry.egress.dropped|Porzucone komunikaty|Licznik|Łącznie|Liczba komunikatów porzuconych, ponieważ nie odpowiadało żadnych tras i trasy rezerwowy hello został wyłączony|
|d2c.telemetry.egress.orphaned|Oddzielone wiadomości|Licznik|Łącznie|Hello liczba wiadomości nie zgodnych tras, wszelkie tym hello rezerwowy trasy|
|d2c.telemetry.egress.invalid|Nieprawidłowy wiadomości|Licznik|Łącznie|Witaj liczba wiadomości nie dostarczyć powodu tooincompatibility z punktem końcowym hello|
|d2c.telemetry.egress.Fallback|Wiadomości pasujące rezerwowy warunku|Licznik|Łącznie|Liczba komunikatów zapisanych toohello rezerwowego punktu końcowego|
|d2c.endpoints.egress.eventHubs|Komunikaty dostarczone tooEvent punkty końcowe Centrum|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie napisane tooEvent punkty końcowe Centrum|
|d2c.endpoints.latency.eventHubs|Opóźnienie komunikat dla punktów końcowych Centrum zdarzeń|w milisekundach|Średnia|Witaj średnie opóźnienie między centrum IoT toohello ruch przychodzący komunikat i komunikat przychodzący do punktu końcowego Centrum zdarzeń, w milisekundach|
|d2c.endpoints.egress.serviceBusQueues|Komunikaty dostarczone tooService kolejki magistrali punkty końcowe|Licznik|Łącznie|Liczba punktów końcowych kolejki magistrali tooService zapisany pomyślnie zostały wiadomości|
|d2c.endpoints.latency.serviceBusQueues|Czas oczekiwania na wiadomość dla punktów końcowych z kolejką usługi Service Bus|w milisekundach|Średnia|Witaj średnie opóźnienie między centrum IoT toohello ruch przychodzący komunikat i komunikat przychodzący do punktu końcowego kolejką usługi Service Bus, w milisekundach|
|d2c.endpoints.egress.serviceBusTopics|Komunikaty dostarczone tooService tematu Bus punkty końcowe|Licznik|Łącznie|Liczba wiadomości były punkty końcowe tematu Bus tooService pomyślnie zapisany|
|d2c.endpoints.latency.serviceBusTopics|Opóźnienie komunikat dla punktów końcowych temat magistrali usług|w milisekundach|Średnia|Witaj średnie opóźnienie między centrum IoT toohello ruch przychodzący komunikat i komunikat przychodzący do punktu końcowego Service Bus tematu w milisekundach|
|d2c.endpoints.egress.builtIn.events|Komunikaty dostarczone toohello wbudowanym punktem końcowym (wiadomości/zdarzeń)|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie napisane toohello wbudowanym punktem końcowym (wiadomości/zdarzeń)|
|d2c.endpoints.latency.builtIn.events|Opóźnienie wiadomość hello wbudowanym punktem końcowym (wiadomości/zdarzeń)|w milisekundach|Średnia|Witaj średnie opóźnienie między centrum IoT toohello ruch przychodzący komunikat i transfer danych przychodzących wiadomości do hello wbudowanym punktem końcowym (wiadomości/zdarzeń), w milisekundach |
|d2c.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z urządzeń|Licznik|Łącznie|odczytuje Hello liczba wszystkie udane dwie inicjowanych przez urządzenie.|
|d2c.Twin.Read.failure|Nie powiodło się dwie odczyty z urządzeń|Licznik|Łącznie|Witaj liczbę wszystkich nie odczyty dwie inicjowanych przez urządzenie.|
|d2c.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z urządzeń|Bajty|Średnia|Hello średnia, minimum i maksimum dla wszystkich pomyślnych inicjowanych przez urządzenie dwie odczytów.|
|d2c.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba Hello wszystkie udane aktualizacji dwie inicjowanych przez urządzenie.|
|d2c.Twin.Update.failure|Nie powiodło się dwie aktualizacje z urządzeń|Licznik|Łącznie|Hello liczbę wszystkich nieudanych aktualizacji dwie inicjowanych przez urządzenie.|
|d2c.Twin.Update.size|Rozmiar aktualizacji dwie z urządzeń|Bajty|Średnia|Hello średnia, minimum i maksymalny rozmiar wszystkich pomyślnych inicjowanych przez urządzenie dwie aktualizacji.|
|c2d.Methods.SUCCESS|Pomyślne bezpośrednie wywołania metod|Licznik|Łącznie|Liczba Hello wszystkich pomyślnych wywołań metody bezpośredniego.|
|c2d.Methods.failure|Nie powiodło się bezpośrednie wywołania metod|Licznik|Łącznie|Witaj liczbę wszystkich nie wywołania metody bezpośredniego.|
|c2d.Methods.requestSize|Rozmiar żądania bezpośrednie wywołania metod|Bajty|Średnia|Średnia Hello, min i max wszystkich pomyślnych żądań metoda bezpośrednia.|
|c2d.Methods.responseSize|Rozmiar odpowiedzi bezpośrednie wywołania metod|Bajty|Średnia|Średnia Hello, min i max wszystkich odpowiedzi metoda bezpośrednia powiodło się.|
|c2d.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z zaplecza|Licznik|Łącznie|odczytuje Hello liczba wszystkie udane dwie inicjowane zakończenia Wstecz.|
|c2d.Twin.Read.failure|Nie powiodło się dwie odczytuje z zaplecza|Licznik|Łącznie|Odczyty wstecz zakończenia inicjowane przez dwie Hello liczbę wszystkich, nie powiodło się.|
|c2d.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z wewnętrznego|Bajty|Średnia|Hello średnia, minimum i maksimum o wszystkie udane wstecz zakończenia inicjowane przez dwie odczytów.|
|c2d.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba Hello wszystkie udane aktualizacji inicjowane zakończenia wstecz dwie.|
|c2d.Twin.Update.failure|Nie powiodło się dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Hello liczbę wszystkich nie powiodło się wstecz zakończenia inicjowane przez dwie aktualizacji.|
|c2d.Twin.Update.size|Rozmiar aktualizacji dwie z wewnętrznego|Bajty|Średnia|Hello średnia, minimum i maksymalny rozmiar wszystkich pomyślnych wstecz zakończenia inicjowane przez dwie aktualizacji.|
|twinQueries.success|Dwie pomyślne zapytania|Licznik|Łącznie|Liczba Hello wszystkie zapytania dwie powiodło się.|
|twinQueries.failure|Nie powiodło się dwie zapytań|Licznik|Łącznie|Liczba Hello wszystkie zapytania dwie nie powiodło się.|
|twinQueries.resultSize|Rozmiar wyników zapytania dwie|Bajty|Średnia|Średnia Hello, min i max hello wynik rozmiaru wszystkich zapytań dwie powiodło się.|
|jobs.createTwinUpdateJob.success|Pomyślne utworzenie kont dwie aktualizacji zadań|Licznik|Łącznie|Liczba Hello wszystkich pomyślnym utworzeniu zadania aktualizacji dwie.|
|jobs.createTwinUpdateJob.failure|Nie powiodło się tworzenie dwie aktualizacji zadań|Licznik|Łącznie|Liczba Hello wszystkie nie powiodło się tworzenie zadań aktualizacji dwie.|
|jobs.createDirectMethodJob.success|Pomyślne tworzenia zadań wywołania — metoda|Licznik|Łącznie|Liczba Hello wszystkich pomyślnym utworzeniu zadania wywołania metody bezpośredniego.|
|jobs.createDirectMethodJob.failure|Nie powiodło się tworzenie zadań wywołania — metoda|Licznik|Łącznie|Liczba Hello wszystkie nie powiodło się tworzenie zadań wywołania metody bezpośredniego.|
|jobs.listJobs.success|Zadania toolist pomyślnych wywołań|Licznik|Łącznie|Liczba Hello wszystkie zadania toolist pomyślnych wywołań.|
|jobs.listJobs.failure|Wywołania zakończone błędem toolist zadania|Licznik|Łącznie|Liczba Hello wszystkie zadania toolist wywołania nie powiodło się.|
|jobs.cancelJob.success|Anulowane zadania powiodło się|Licznik|Łącznie|Hello liczba wszystkich pomyślnych wywołań toocancel zadania.|
|jobs.cancelJob.failure|Anulowanie zadania nie powiodło się|Licznik|Łącznie|Liczba Hello wszystkie wywołania zakończone błędem toocancel zadania.|
|jobs.queryJobs.success|Pomyślnie wykonane zadanie zapytań|Licznik|Łącznie|Liczba Hello wszystkie zadania tooquery pomyślnych wywołań.|
|jobs.queryJobs.failure|Nie powiodło się zadanie odpytuje|Licznik|Łącznie|Liczba Hello wszystkie zadania tooquery wywołania nie powiodło się.|
|Jobs.Completed|Zadania ukończone|Licznik|Łącznie|Liczba Hello wszystkie zadania zakończone.|
|Jobs.failed|Zadania zakończone niepowodzeniem|Licznik|Łącznie|Liczba Hello wszystkie zadania zakończone niepowodzeniem.|

## <a name="next-steps"></a>Następne kroki
Teraz, przedstawiono omówienie Centrum IoT metryki, skorzystaj z tego łącza toolearn więcej o zarządzaniu Centrum IoT Azure:

* [Operacje monitorowania][lnk-monitor]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
