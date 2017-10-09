---
title: "aaaConfigure źródeł danych w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Źródła danych do definiowania danych hello czy zbiera analizy dzienników z agentów i inne połączenie źródeł.  W tym artykule opisano pojęcia hello jak analizy dzienników korzysta ze źródeł danych, wyjaśnia hello szczegóły dotyczące tooconfigure i zawiera podsumowanie hello różnych źródeł danych dostępne."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Źródła danych w analizy dzienników
Analiza dzienników zbiera dane z hello połączonych źródeł w obszarze roboczym pakietu OMS i zapisuje go w repozytorium OMS.  Witaj dane zbierane z każdej jest zdefiniowana przez hello źródeł danych, które można skonfigurować.  Dane w repozytorium OMS hello są przechowywane jako zestaw rekordów.  Dla każdego źródła danych tworzy rekordy określonego typu z każdym typem o własny zestaw właściwości.

![Zbierania danych analizy dzienników](./media/log-analytics-data-sources/overview.png)

Źródła danych są inne niż OMS rozwiązania, które również zbieranie danych z połączonych źródeł i tworzenie rekordów w repozytorium OMS hello.  Rozwiązania można dodać obszaru roboczego tooyour z hello galerii rozwiązań i zwykle zapewnia dodatkowe analizy narzędzi w portalu OMS hello.  

## <a name="summary-of-data-sources"></a>Podsumowanie źródeł danych
w hello w poniższej tabeli wymieniono Hello źródeł danych, które są aktualnie dostępne w analizy dzienników.  Każdy ma łącze tooa oddzielnym artykule podanie szczegółów dla tego źródła danych.

| Źródło danych | Typ zdarzenia | Opis |
|:--- |:--- |:--- |
| [Niestandardowe dzienniki](log-analytics-data-sources-custom-logs.md) |\<Nazwa_dziennika\>_CL |Pliki tekstowe agentów systemu Windows lub Linux, zawierające informacje w dzienniku. |
| [Dzienniki zdarzeń systemu Windows](log-analytics-data-sources-windows-events.md) |Wydarzenie |Zbierane zdarzenia z dziennika zdarzeń hello na komputerach z systemem Windows. |
| [Liczniki wydajności systemu Windows](log-analytics-data-sources-performance-counters.md) |Wydajności |Liczniki wydajności są zbierane z komputerów z systemem Windows. |
| [Liczniki wydajności systemu Linux](log-analytics-data-sources-performance-counters.md) |Wydajności |Liczniki wydajności zebrane z komputerów z systemem Linux. |
| [Dzienniki usług IIS](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Internetowe usługi informacyjne dzienniki w formacie W3C. |
| [Dziennik systemu](log-analytics-data-sources-syslog.md) |Dziennik systemu |Zdarzenia dziennika systemowego na komputerach z systemem Windows lub Linux. |

## <a name="configuring-data-sources"></a>Konfigurowanie źródeł danych
Konfigurowanie źródeł danych z hello **danych** menu analizy dzienników **ustawienia**.  Dowolna konfiguracja jest dostarczana źródeł tooall połączone w obszarze roboczym pakietu OMS.  Nie można obecnie wykluczyć wszystkich agentów z tej konfiguracji.

![Skonfiguruj zdarzenia systemu Windows](./media/log-analytics-data-sources/configure-events.png)

1. W konsoli OMS powitania kliknij hello **ustawienia** kafelka lub hello **ustawienia** przycisk u góry hello hello ekranu.
2. Wybierz **danych**.
3. Polecenie tooconfigure źródła danych hello.
4. Wykonaj hello łącze toohello dokumentacji dla każdego źródła danych w hello powyżej tabela zawiera szczegółowe informacje na ich konfiguracji.

> [!NOTE]
> Obecnie nie można skonfigurować źródła danych analizy dzienników w hello portalu Azure.

## <a name="data-collection"></a>Zbieranie danych
Konfiguracje źródła danych są dostępne w ramach tooagents, które są bezpośrednio połączone tooLog analityka w ciągu kilku minut.  Witaj określone dane są zbierane z agenta hello i dostarczane bezpośrednio tooLog analityka w źródle danych tooeach w określonych odstępach czasu.  Zapoznaj się dokumentacją powitania dla każdego źródła danych dla tych szczegółowych informacji.

Agenci programu System Center Operations Manager (SCOM) w dołączonej grupy zarządzania konfiguracji źródła danych są przetłumaczyć pakietów administracyjnych i dostarczyć co 5 minut domyślnie toohello grupy zarządzania.  Hello agent pobiera hello pakiet administracyjny jak każdy inny i zbiera hello określone dane. W zależności od Witaj Witaj źródła danych dane zostaną wysłane albo tooa serwera zarządzania, który przesyła dalej hello toohello danych analizy dzienników lub hello agent wyśle hello danych tooLog Analytics bez pośrednictwa powitania serwera zarządzania. Odwołuje się zbyt[szczegóły zbierania danych w celu OMS funkcji i rozwiązań](log-analytics-add-solutions.md#data-collection-details) szczegółowe informacje.  Możesz przeczytać o szczegółach łączenia SCOM i OMS i modyfikowanie częstotliwości hello tej konfiguracji jest dostarczany w [skonfigurować integrację z programem System Center Operations Manager](log-analytics-om-agents.md).

Jeśli hello agent tooLog tooconnect analityka lub Operations Manager, będzie toocollect dane, które będzie dostarczać, podczas nawiązywania połączenia.  Dane mogą zostać utracone, jeśli hello ilość danych osiągnie hello maksymalny rozmiar pamięci podręcznej klienta na powitania lub hello agent nie jest możliwe tooestablish połączenia w ciągu 24 godzin.

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Wszystkie dane zebrane przez analizy dzienników jest przechowywane w repozytorium OMS hello jako rekordów.  Rejestruje zebrane przez różnych źródeł danych będą mieć własny zestaw właściwości i zostać zidentyfikowane na podstawie ich **typu** właściwości.  Zawiera dokumentacja powitania dla każdego źródła danych i rozwiązania, aby uzyskać szczegółowe informacje o poszczególnych typów rekordów.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [rozwiązań](log-analytics-add-solutions.md) czy dodać funkcje tooLog Analytics i zbierać dane do repozytorium OMS hello.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.  
* Skonfiguruj [alerty](log-analytics-alerts.md) tooproactively powiadamia użytkownika o krytyczne dane zebrane ze źródeł danych i rozwiązań.
