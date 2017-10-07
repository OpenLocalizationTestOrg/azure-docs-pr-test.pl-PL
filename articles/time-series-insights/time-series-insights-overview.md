---
title: aaaOverview Azure czas serii Insights | Dokumentacja firmy Microsoft
description: "Wprowadzenie tooAzure czasu serii wgląd, nową usługę dla analizy danych serii czasu i rozwiązania IoT"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>Co to jest usługa Azure Time Series Insights?

Azure czas serii Insights to usługa w chmurze zarządzanego z magazynu, analizy i wizualizacji składników, które go łatwo tooingest, przechowywania, eksplorowanie i analizowanie miliardów zdarzeń jednocześnie. Usługa Time Series Insights zapewnia globalny wgląd w dane i umożliwia szybkie weryfikowanie rozwiązań IoT. Ponadto zapobiega kosztownym przestojom pracy urządzeń, pomagając w wykrywaniu ukrytych trendów i anomalii oraz przeprowadzaniu analiz głównych przyczyn problemów niemal w czasie rzeczywistym. Czas serii Insights wysyła strumień danych szeregu czasowego z brokerzy zdarzeń (np. centra IoT lub Event Hubs), indeksy hello danych i wycofaniu danych na podstawie zasad przechowywania można skonfigurować. Użytkownicy wykorzystują dane hello za pomocą intuicyjnego środowiska użytkownika lub interfejsów API REST zapytania.

![Omówienie usługi Time Series Insights](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Podstawowe scenariusze

* Monitorowanie i weryfikowanie rozwiązań IoT w ciągu kilku minut.
* Wizualizowanie i analizowanie danych IoT na dużą skalę.
* Usprawnianie analiz głównych przyczyn problemów i wykrywanie anomalii.
* Tworzenie globalnego widoku obejmującego wiele urządzeń, zakładów i danych.

## <a name="capabilities-and-benefits"></a>Funkcje i korzyści

* **Łatwe tooget uruchomiona**: Azure czas serii Insights wymaga nie przygotowania początkowych danych i jest bardzo szybkie. Połącz toobillions zdarzeń w Centrum IoT Azure lub Centrum zdarzeń w minutach. Po nawiązaniu połączenia wizualizacji i interakcję z danych czujnika w sekundach tooquickly zweryfikować Twojego rozwiązania IoT. Czas serii Insights jest łatwe toouse; Możesz użyć danych bez pisania pojedynczy wiersz kodu.  Nie istnieje żadne nowe toolearn języka; Czas serii Insights udostępnia surface szczegółowego, niezależnych kwerendy dla użytkowników zaawansowanych i i kliknij opcję eksploracji dla wszystkich.

* **Wgląd w czasie rzeczywistym w pobliżu**: czas serii Insights może obsługiwać setki milionów czujnik zdarzeń na dzień, z opóźnieniem jednej minuty, możesz szybko reagować toochanges. Usługa Time Series Insights umożliwia uzyskiwanie szczegółowych informacji dotyczących danych z czujników dzięki ułatwieniu szybkiego wykrywania trendów i anomalii, przeprowadzaniu złożonych analiz głównych przyczyn problemów i unikaniu kosztownych przestojów. Przez włączenie cross korelacja w czasie rzeczywistym i historycznych danych, czas serii Insights ułatwia ukryte trendów w danych hello odblokowywania.

* **Tworzenie niestandardowych rozwiązań**: dane usługi Azure Time Series Insights można osadzić w istniejących aplikacjach. Przy użyciu interfejsów API REST usługi Time Series Insights można też tworzyć nowe, niestandardowe rozwiązania. Tworzenie i udostępnianie spersonalizowanych widoki, można udostępniać innym osobom tooexplore Twojego odnajdywania.

* **Skalowalność**: czas serii Insights jest zaprojektowana toosupport IoT na dużą skalę. W wersji zapoznawczej może transfer danych przychodzących z too100 1 milion milionów zdarzeń na dzień z przechowywaniem domyślny zakres 31 dni. Możliwe jest wizualizowanie i analizowanie strumieni bieżących danych niemal w czasie rzeczywistym na tle dużych ilości danych historycznych. Przenoszenie do przodu, ruch przychodzący i przechowywania zwiększy tooaccommodate kiedykolwiek zmieniające się skali przedsiębiorstwa.

## <a name="time-series-insights-glossary"></a>Słownik dotyczący usługi Time Series Insights

* **Środowisko**: środowisko jest zasobem platformy Azure, który umożliwia pozyskiwanie i magazynowanie danych.  Klienci obsługi administracyjnej środowiska za pośrednictwem portalu Azure z ich wymaganą pojemnością hello.
* **Źródło zdarzeń**: źródło zdarzeń pochodzi od brokera zdarzeń, takiego jak usługa Azure Event Hubs.  Czas serii Insights łączy bezpośrednio tooEvent źródeł, wprowadzania hello strumienia danych bez pisania żadnego kodu. Obecnie usługa Time Series Insights obsługuje centra zdarzeń Azure Event Hub i Azure IoT Hub.
* **Danych referencyjnych**: czas serii Insights udostępnia użytkownikom hello możliwości toojoin czasu serii danych z danych referencyjnych.  Dane referencyjne mogą obejmować metadane dotyczące urządzeń lub inne statyczne dane, które zmieniają się stosunkowo rzadko. Czas serii Insights sprzężenia danych referencyjnych hello strumieni danych, dzięki czemu użytkownicy toovisualize i analizować te dane w niemal w czasie rzeczywistym.
