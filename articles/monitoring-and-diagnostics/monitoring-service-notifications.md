---
title: "aaaWhat są powiadomienia o kondycji usługi | Dokumentacja firmy Microsoft"
description: "Powiadomienia o kondycji usługi zezwala na komunikaty kondycji usługi tooview publikowania przez Microsoft Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Powiadomienia o kondycji usługi
## <a name="overview"></a>Omówienie

W tym artykule opisano, jak tooview powiadomień o kondycji usługi przy użyciu hello portalu Azure.

Powiadomienia o kondycji usługi Zezwalaj możesz tooview usługi kondycji wiadomości opublikowanych przez hello Azure zespół, który może mieć wpływ na zasoby hello w ramach Twojej subskrypcji. Te powiadomienia są podklasą klasy działania dziennika zdarzeń i można także znaleźć w bloku dziennika aktywności hello. Powiadomienia o kondycji usługi może być informacyjne lub można wykonać w zależności od klasy hello.

Istnieje pięć klas powiadomień o kondycji usługi:  

- **Wymagana akcja:** z tootime czasu firma Microsoft zauważyć coś nietypowego się tak zdarzyć na Twoim koncie. Firma Microsoft może być konieczne toowork z tooremedy należy to. Wyślemy powiadomienie albo wyszczególnieniem akcje hello należy tootake lub z szczegółowe informacje na temat inżynierii toocontact Azure lub obsługuje.  
- **Odzyskiwanie asystowaną:** wystąpiło zdarzenie i inżynierów potwierdzeniu, że nadal występują wpływu. Inżynieria należy toowork z Tobą bezpośrednio toobring toorestoration Twojej usługi.  
- **Zdarzenie:** wpływające na zdarzenia usługi aktualnie ma wpływ na co najmniej jeden hello zasobów w ramach subskrypcji.  
- **Konserwacja:** jest powiadomienie informujące o działanie zaplanowanej konserwacji, które mogą mieć wpływ na co najmniej jeden hello zasobów w ramach Twojej subskrypcji.  
- **Informacje o:** od czasu tootime użytkownik może otrzymywać powiadomienia, że komunikacja tooyou o potencjalnych funkcje optymalizacji, które mogą pomóc zwiększenie wykorzystanie zasobów.  
- **Zabezpieczenia:** pilnych zabezpieczeń powiązane informacje dotyczące Twojego solution(s) działających na platformie Azure.

Każde powiadomienie o kondycji usługi prowadzi szczegóły hello zakres i znaczenie tooyour zasobów. Zawiera szczegółowe informacje:

Nazwa właściwości | Opis
-------- | -----------
Kanały | Jest jednym z hello następujące wartości: "Administrator", "Operacji"
correlationId | Jest zazwyczaj identyfikator GUID w formacie ciągu hello. Zdarzenia z tym należy toohello zwykle udostępnić tę samą akcję pełny hello correlationId tego samego.
eventDataId | Jest hello Unikatowy identyfikator zdarzenia
EventName | Tytuł hello hello zdarzenia
poziom | Poziom hello zdarzeń. Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"
resourceProviderName | Nazwa dostawcy zasobów hello hello wpływ na zasób
Typ zasobu| Typ zasobu hello Hello wpływ na zasób
Podstan | Zazwyczaj hello kod stanu HTTP hello odpowiadającego wywołania REST, ale można również uwzględnić inne parametry opisujące podstanu, takich jak te wartości typowych: OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (HTTP Kod stanu: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503), limit czasu bramy (kod stanu HTTP: 504).
eventTimestamp | Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello.
submissionTimestamp |   Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań.
subscriptionId | Witaj w trakcie którego zarejestrowano to zdarzenie subskrypcji platformy Azure
status | Ciąg opisujący stan hello hello operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane.
operationName | Nazwa operacji hello.
category | "ServiceHealth"
resourceId | Identyfikator zasobu hello wpływ na zasobów.
Properties.Title | Tytuł Hello zlokalizowane dla tej komunikacji. Język domyślny hello jest angielski.
Properties.Communication | Szczegóły Hello zlokalizowane hello komunikacji z kodu znaczników HTML. Domyślne hello jest angielski.
Properties.incidentType | Możliwe wartości: AssistedRecovery, ActionRequired, informacje, zdarzenie, obsługi, zabezpieczeń
Properties.trackingId | Identyfikuje hello incydent, który jest skojarzony to zdarzenie. Użyj tego zdarzenia pokrewne tooan toocorrelate hello zdarzenia.
Properties.impactedServices | Zmienionym obiektu blob JSON opisującą hello usług i regionów, które mają wpływ zdarzenia hello. Lista usług, z których każda ma elementy ServiceName i listę ImpactedRegions, z których każda ma RegionName.
Properties.defaultLanguageTitle | Komunikacja Hello w języku angielskim
Properties.defaultLanguageContent | Komunikacja Hello w języku angielskim jako kod znaczników html i zwykły tekst
Properties.Stage | Możliwe wartości AssistedRecovery, ActionRequired, informacje, zdarzenie, zabezpieczeń: są aktywne, rozwiązane. W konserwacji są: aktywny, planowane, w toku, anulowane, Rescheduled, rozwiązane, Zakończ
Properties.communicationId | Komunikacja Hello to zdarzenie jest skojarzony.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Wyświetlanie powiadomienia usługi kondycji w hello portalu Azure
1.  W hello [portal](https://portal.azure.com), przejdź toohello **Monitor** usługi

    ![Monitorowanie](./media/monitoring-service-notifications/home-monitor.png)
2.  Kliknij przycisk hello **Monitor** tooopen opcji zapasowej hello Monitor bloku. Ten blok gromadzi wszystkie ustawienia monitorowania i dane użytkownika w jednym skonsolidowanym widoku. Pierwszym otwarciu toohello **dziennik aktywności** sekcji.

3.  Teraz kliknij **powiadomień usługi** sekcji

    ![Monitorowanie](./media/monitoring-service-notifications/service-health-summary.png)
4.  Kliknij dowolną tooview pozycje hello więcej szczegółów

5. Polecenie hello **+ Dodaj alertu dziennika aktywności** tooensure powiadomienia tooreceive operacji są powiadamiani powiadomień usługi przyszłości tego typu. więcej informacji na temat konfigurowania alertów na powiadomienia usługi toolearn [kliknij tutaj](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Następne kroki:
Odbieranie [alertów powiadomienia, gdy powiadomienie o kondycji usługi](monitoring-activity-log-alerts-on-service-notifications.md) jest przesyłana  
Dowiedz się więcej o [alertów dotyczących działań w Dzienniku](monitoring-activity-log-alerts.md)
