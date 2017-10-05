---
title: "Omówienie pojemności dedykowanego centra zdarzeń platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b3af61ec0923a0d9d207cee790d59aa9254a578b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Omówienie usługi Event hubs w wersji dedykowanej

*Dedykowane centra zdarzeń* pojemności oferuje wdrożeń pojedynczej dzierżawy dla klientów z najbardziej wygórowanych wymaganiach. W pełnej skali usługi Azure Event Hubs można wejściowych ponad 2 miliony zdarzeń na sekundę, czyli do 2 GB na sekundę telemetrii pełni trwałe opóźnienia magazynu i sekundę podrzędnych. Umożliwia to również zintegrowane rozwiązania przez przetwarzanie w czasie rzeczywistym i partii w tym samym systemie. Z archiwum centra zdarzeń uwzględniona w ofercie można zmniejszyć złożoność rozwiązania przez jednego strumienia obsługuje potoki w czasie rzeczywistym oraz na podstawie partii.

W poniższej tabeli porównano warstw dostępna usługa Event hubs. Oferta dedykowanego centra zdarzeń jest stały miesięcznej cenie, w porównaniu do użycia ceny większość funkcji standardowa i podstawowa. Dedykowany warstwy oferuje funkcje planie Standard, ale o pojemności skali przedsiębiorstwa, w przypadku klientów z wymagających obciążeń. 

| Funkcja | Podstawowa | Standardowa | Dedykowany |
| --- |:---:|:---:|:---:|
| Zdarzenia związane z transferem danych przychodzących | Należy zwrócić na miliona zdarzeń | Należy zwrócić na miliona zdarzeń | Dołączono |
| Jednostki przepustowości (ruch przychodzący 1 MB/s, wyjście 2 MB/s) | Należy zwrócić na godzinę | Należy zwrócić na godzinę | Dołączono |
| Rozmiar komunikatu | 256 KB | 256 KB | 1 MB |
| Zasady dotyczące wydawców | Nie dotyczy | Tak | Tak |     
| Grupy odbiorców | 1 - domyślne | 20 | 20 |
| Powtarzanie komunikatu | Tak | Tak | Tak |
| Maksymalna liczba jednostek przepływności | 20 | 20 (elastyczne do 100)  | 1 jednostka wydajności≈200 |
| Połączenia obsługiwane przez brokera | 100 włączone | 1000 włączone | 100 KB włączone |
| Dodatkowe połączenia obsługiwane przez brokera | Nie dotyczy | Tak | Tak |
| Przechowywanie komunikatów | 1 dzień w cenie | 1 dzień w cenie | Liczba uwzględnianych dni: do 7 |
| Archiwum (wersja zapoznawcza) | Nie dotyczy   | Należy zwrócić na godzinę | Dołączono |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Korzyści wynikające z dedykowanych centra zdarzeń wydajności

Korzystając z dedykowanych centra zdarzeń, dostępne są następujące korzyści:

* Obsługa za pomocą nie szumu od pozostałych dzierżawców pojedynczej dzierżawy.
* Rozmiar komunikatu zwiększa 1 MB w porównaniu do 256 KB dla standardowa i podstawowa.
* Zawsze powtarzalne wydajności.
* Gwarancji wydajności, aby spełnić potrzeby serii.
* Skalowalna od 1 do 8 pojemność jednostki (CU) — dostarczający zdarzenia służąca do milionów 2 na sekundę.
  * CUs Zarządzanie skali dla dedykowanego centra zdarzeń, którym każdej aktualizacji zbiorczej można podać odpowiednikiem około 200 jednostek przepływności (TU).
* Zero konserwacji: Firma Microsoft zarządzania równoważenia obciążenia, systemu operacyjnego aktualizacje, poprawki zabezpieczeń i partycjonowania.
* Stałe, co miesiąc cennik.

Dedykowane centra zdarzeń spowoduje również usunięcie niektóre ograniczenia przepustowości Standard oferty. Jednostki przepływności w warstwach Basic i Standard uprawnia do 1000 zdarzeń na sekundę lub 1 MB na sekundę na TU i double ilość ruch wychodzący ruch przychodzący. Liczby zdarzeń dotyczących komunikacji wyjściowej i oferty dedykowanych skalowania nie ma żadnych ograniczeń na transfer danych przychodzących. Te limity reguluje tylko wydajności przetwarzania zakupionych event hubs.

Ta usługa jest przeznaczona dla użytkowników dane telemetryczne największą i jest dostępny dla klientów z umową enterprise.

## <a name="how-to-onboard"></a>Jak dołączyć

Dedykowane centra zdarzeń platformy jest oferowany przez umową enterprise o różnych rozmiarach CUs. Każdy CU udostępnia odpowiednik około 200 jednostek przepływności. Wydajność można skalować w górę lub w dół w ciągu miesiąca do własnych potrzeb, dodając lub usuwając CUs. Dedykowany plan jest unikatowa, w tym wystąpią bardziej praktyczne dołączania od zespołu produktu usługi Event Hubs można pobrać elastyczne wdrożenia, które jest odpowiednie dla Ciebie. 

## <a name="next-steps"></a>Następne kroki
Skontaktuj się z przedstawicielem handlowym firmy Microsoft lub Microsoft Support, aby uzyskać więcej informacji na temat pojemności dedykowanego centra zdarzeń. Można też uzyskać więcej informacji na temat usługi Event Hubs, przechodząc na stronę następujących łączy:

Aby uzyskać szczegółowe informacje na temat cen odwiedź następujących łączy:

- [Cennik dedykowanego centra zdarzeń](https://azure.microsoft.com/pricing/details/event-hubs/). Można również skontaktować się sprzedaży przedstawicielem firmy Microsoft lub Support firmy Microsoft, aby uzyskać więcej informacji na temat pojemności dedykowanego centra zdarzeń.
- [Centra zdarzeń często zadawane pytania dotyczące](event-hubs-faq.md) zawiera informacje o cenach i odpowiedzi na niektóre często zadawane pytania dotyczące usługi Event Hubs. 
