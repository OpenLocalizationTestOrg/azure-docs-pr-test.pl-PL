---
title: "aaaAzure Mobile Engagement Troubleshooting Guide — analiza"
description: "Rozwiązywanie problemów analizy, monitorowanie segmentacji i pulpit nawigacyjny w usłudze Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Przewodnik rozwiązywania problemów analizy, monitorowanie segmentacji i pulpitu nawigacyjnego
Witaj poniżej przedstawiono możliwe problemy mogą się pojawić w jaki sposób usługi Azure Mobile Engagement zbiera informacje o aplikacji, urządzeń i użytkowników.

## <a name="missingdelayed-information"></a>Brak opóźnione informacji
### <a name="issue"></a>Problem
* Informacje o jest opóźnione w znajdujących się w Analytics, segmentacji lub pulpitu nawigacyjnego.
* Monitorowanie brakuje informacji.
* Brakuje informacji Analytics, segmentacji lub pulpitu nawigacyjnego.
* Naciśnięcie limity segmentacji.

### <a name="causes"></a>Powoduje, że
* Można użyć hello Analytics API monitora interfejsu API, i toosee segmentów interfejsu API w przypadku wszystkich danych brakuje hello interfejsu użytkownika jest widoczny za pośrednictwem interfejsów API hello.
* Hello Azure Mobile Engagement SDK nie jest poprawnie zintegrowana w aplikacji nie będzie możliwe toosee informacji w hello Analytics segmentacji, monitorowanie i pulpity nawigacyjne.
* Segmenty nie można zmienić po ich utworzeniu, segmentów może być tylko "sklonowane" (skopiowany) lub "zniszczone" (usunięty). Segmenty może zawierać tylko 10 kryteriów.
* Hello najlepsze sposób tootest Brak informacji z monitorowania jest toosetup urządzenie testowe, odinstaluj i/lub ponowne zainstalowanie aplikacji hello na powitania urządzenie testowe.
* Informacje są odświeżane co 24 godziny dla analityka, segmentacji lub pulpitów nawigacyjnych.
* Informacje zawarte w nowych segmentów mogą być niewidoczne do 24 godzin po ich utworzeniu, nawet jeśli hello segment jest oparta na poprzednich informacji.
* Filtrowanie danych analityka w hello interfejsu użytkownika zostaną wyświetlone wszystkie przykłady tego typu, niezależnie od wersji aplikacji hello (np. "Awarii" przefiltrowane według nazwy zostaną wyświetlone w wersji 1 i aplikacji w wersji 2).
* Hello okresu Analytics jest oparty na hello dat z ustawień urządzenia użytkownika hello, więc użytkownika, którego telefon ma niepoprawnie ustawione Data hello mogą pojawiać się w hello niewłaściwy przedziale czasu.
* Wypchnięcia nie po stronie serwera, którego dane są rejestrowane, korzystając z przycisku hello zbyt "test", tylko rejestrowane są dane dla kampanie wypychania prawdziwe.

## <a name="cant-locate-items-in-ui"></a>Nie można zlokalizować elementów w interfejsie użytkownika
### <a name="issue"></a>Problem
* Nie można utworzyć segmenty oparte na niektóre wbudowane lub informacje o aplikacji niestandardowych tagów kryteriów.
* Nie można znaleźć niektórych wbudowanych lub informacje o aplikacji niestandardowych tagów kryteria analizy, monitorowanie lub pulpitów nawigacyjnych.
* Nie można zinterpretować hello danych analizy, monitorowanie, segmentacji lub pulpitów nawigacyjnych.

### <a name="causes"></a>Powoduje, że
* Niektóre wbudowane elementy i informacje o aplikacji są dostępne tylko jako kryteriów wypychania tagi, ale może nie być dodane segmentu tooa lub widoczne z analizy, monitorowanie lub pulpitu nawigacyjnego. 
* Utworzony w elementy i informacje o aplikacji tagi, których nie można dodać tooa segment, konieczne będzie listy toosetup docelowych kryteriów w każdym hello tooperform kampanii funkcji takie same jak oparte na segment.
* Wyświetlić menu kontekstowe hello w sekcjach analizy, monitorowanie segmentacji i pulpity nawigacyjne hello hello Azure Mobile Engagement w interfejsie użytkownika, aby uzyskać dalszą pomoc i w jaki sposób tooinformation.

## <a name="crash-troubleshooting"></a>Awarii, rozwiązywanie problemów
### <a name="issue"></a>Problem
* Wystąpiła awaria aplikacji znajdujących się w analizy, monitorowanie lub pulpitu nawigacyjnego.

### <a name="causes"></a>Powoduje, że
* tootroubleshoot aplikacja przestaje działać w analizy, monitorowanie lub pulpit nawigacyjny upewnij się, że informacje o wersji hello toocheck pod kątem znanych problemów z poprzednimi wersjami hello zestawu SDK.
* toofurther Rozwiązywanie problemów z aplikacji awarii wykonaj zdarzenia z urządzeniem testu z zainstalowania aplikacji i wyszukać identyfikator urządzenia w sekcji hello "Monitor — zdarzenia" hello Azure Mobile Engagement w interfejsie użytkownika. Następnie wykonaj hello zdarzenie, które powoduje toocrash Twojej aplikacji i wyszukiwania dodatkowych informacji w hello sekcji "Monitor awarii —" hello Azure Mobile Engagement w interfejsie użytkownika. 

