---
title: "aaaOverview pojemności dedykowanego centra zdarzeń platformy Azure | Dokumentacja firmy Microsoft"
description: "Przegląd pojemności dedykowanego centra zdarzeń Microsoft Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Omówienie usługi Event hubs w wersji dedykowanej

*Dedykowane centra zdarzeń* pojemności oferuje wdrożeń pojedynczej dzierżawy dla klientów z hello najbardziej wygórowanych wymaganiach. W pełnej skali usługi Azure Event Hubs można wejściowych ponad 2 miliony zdarzeń na sekundę lub w górę too2 GB na sekundę dane telemetryczne z pełni trwałe opóźnienia magazynu i sekundę podrzędne. To również umożliwia zintegrowanego rozwiązania przez przetwarzanie w czasie rzeczywistym i partii hello sam system. Dzięki uwzględniona w ofercie hello archiwum centra zdarzeń można ograniczyć złożoność hello rozwiązania przez jednego strumienia obsługuje potoki w czasie rzeczywistym oraz na podstawie partii.

Witaj poniższej tabeli porównano hello warstw dostępna usługa Event hubs. Oferta dedykowanego centra zdarzeń Hello jest stały cenie miesięcznej porównaniu toousage ceny dla większości jej funkcji standardowa i podstawowa. Warstwa dedykowanych Hello oferuje funkcje hello hello planie Standard, ale o pojemności skali przedsiębiorstwa, w przypadku klientów z wymagających obciążeń. 

| Funkcja | Podstawowa | Standardowa | Dedykowany |
| --- |:---:|:---:|:---:|
| Zdarzenia związane z transferem danych przychodzących | Należy zwrócić na miliona zdarzeń | Należy zwrócić na miliona zdarzeń | Dołączono |
| Jednostki przepustowości (ruch przychodzący 1 MB/s, wyjście 2 MB/s) | Należy zwrócić na godzinę | Należy zwrócić na godzinę | Dołączono |
| Rozmiar komunikatu | 256 KB | 256 KB | 1 MB |
| Zasady dotyczące wydawców | Nie dotyczy | Tak | Tak |     
| Grupy odbiorców | 1 - domyślne | 20 | 20 |
| Powtarzanie komunikatu | Tak | Tak | Tak |
| Maksymalna liczba jednostek przepływności | 20 | 20 (elastyczne too100)  | 1 jednostka wydajności≈200 |
| Połączenia obsługiwane przez brokera | 100 włączone | 1000 włączone | 100 KB włączone |
| Dodatkowe połączenia obsługiwane przez brokera | Nie dotyczy | Tak | Tak |
| Przechowywanie komunikatów | 1 dzień w cenie | 1 dzień w cenie | Konfigurowanie dni too7 włączone |
| Archiwum (wersja zapoznawcza) | Nie dotyczy   | Należy zwrócić na godzinę | Dołączono |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Korzyści wynikające z dedykowanych centra zdarzeń wydajności

Korzystając z dedykowanych centra zdarzeń, dostępne są Hello następujące korzyści:

* Obsługa za pomocą nie szumu od pozostałych dzierżawców pojedynczej dzierżawy.
* Komunikat rozmiarze too1 MB w porównaniu KB too256 dla standardowa i podstawowa.
* Zawsze powtarzalne wydajności.
* Gwarantowane toomeet pojemności, których potrzebuje Twojego serii.
* Skalowalna od 1 do 8 pojemność jednostki (CU) — zapewnianie too2 miliona zdarzeń transfer danych przychodzących na sekundę.
  * CUs Zarządzanie hello skalowania dla dedykowanego centra zdarzeń, którym każdej aktualizacji zbiorczej można podać około hello równoważne 200 jednostek przepływności (TU).
* Zero konserwacji: Firma Microsoft zarządzania równoważenia obciążenia, systemu operacyjnego aktualizacje, poprawki zabezpieczeń i partycjonowania.
* Stałe, co miesiąc cennik.

Dedykowane centra zdarzeń spowoduje również usunięcie niektóre ograniczenia przepływności hello hello standardowe oferty. Jednostki przepływności w warstwach Basic i Standard uprawniają too1000 zdarzeń na sekundę lub 1 MB na sekundę na TU i double ilość ruch wychodzący ruch przychodzący. liczby zdarzeń dotyczących komunikacji wyjściowej i oferty dedykowanych skali Hello nie ma żadnych ograniczeń na transfer danych przychodzących. Te limity reguluje tylko hello przetwarzania pojemności hello zakupu usługi event hubs.

Ta usługa jest celem hello największy telemetrii użytkowników i jest dostępne toocustomers z umową enterprise.

## <a name="how-tooonboard"></a>Jak tooonboard

za pośrednictwem umową enterprise o różnych rozmiarach CUs jest oferowana Hello dedykowanego centra zdarzeń platformy. Każdy CU zapewnia około hello równoważne 200 jednostek przepływności. Można skalować wydajność w górę lub w dół w całym toomeet miesiąca hello potrzeb przez dodanie lub usunięcie CUs. plan dedykowanych Hello jest unikatowa, w tym wystąpią bardziej praktyczne dołączania z hello usługi Event Hubs produktu team tooget hello elastyczne wdrożenia, które jest odpowiednie dla Ciebie. 

## <a name="next-steps"></a>Następne kroki
Skontaktuj się z przedstawicielem handlowym firmy Microsoft lub Microsoft Support tooget dodatkowe szczegóły dotyczące pojemności dedykowanego centra zdarzeń. Można też uzyskać więcej informacji na temat usługi Event Hubs, przechodząc na stronę hello następującego łącza:

Aby uzyskać szczegółowe informacje na temat cen odwiedź hello następującego łącza:

- [Cennik dedykowanego centra zdarzeń](https://azure.microsoft.com/pricing/details/event-hubs/). Można również skontaktować się z przedstawicielem handlowym firmy Microsoft lub Microsoft Support tooget dodatkowe szczegóły dotyczące pojemności dedykowanego centrów zdarzeń.
- Witaj [centra zdarzeń często zadawane pytania dotyczące](event-hubs-faq.md) zawiera informacje o cenach i odpowiedzi na niektóre często zadawane pytania dotyczące usługi Event Hubs. 
