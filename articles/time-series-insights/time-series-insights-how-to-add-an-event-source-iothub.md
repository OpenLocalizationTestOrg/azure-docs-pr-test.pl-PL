---
title: "tooadd aaaHow środowiska Azure czas serii Insights tooyour źródła zdarzeń Centrum IoT | Dokumentacja firmy Microsoft"
description: "W tym samouczku opisano sposób tooadd zdarzenie źródła, to znaczy połączenia tooan środowiska czasu serii Insights tooyour Centrum IoT"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Jak tooadd źródłem zdarzenia Centrum IoT

W tym samouczku opisano, jak toouse hello Azure tooadd portalu źródło zdarzenia, które odczytuje ze środowiska czasu serii Insights tooyour Centrum IoT.

## <a name="prerequisites"></a>Wymagania wstępne

Utworzono Centrum IoT i pisania tooit zdarzenia. Aby uzyskać więcej informacji o centra IoT, zobacz <https://azure.microsoft.com/services/iot-hub/>

> [Grupy konsumentów] Źródło zdarzenia każdego Insights serii czasu musi toohave własnej dedykowanej grupy klientów, które nie są współużytkowane z innym klientom. Jeśli korzystać z wielu czytników zdarzeń z hello tej samej grupy konsumentów, wszystkie czytniki są prawdopodobnie toosee błędów. Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Wybierz opcję importu

Ustawienia Hello hello źródło zdarzenia można wprowadzić ręcznie lub Centrum IoT można wybierać z hello centra IoT, które są dostępne tooyou.
W hello **opcję importu** selektora, wybierz jedną z hello następujące opcje:

* Podaj ustawienia Centrum IoT ręcznie
* Użyj Centrum IoT z dostępnych subskrypcji

### <a name="select-an-available-iot-hub"></a>Wybierz dostępny Centrum IoT

Hello poniższej tabeli opisano poszczególne opcje hello kartę nowe źródło zdarzeń z jego opisem podczas wybierania dostępne Centrum IoT jako źródło zdarzenia:

| NAZWA WŁAŚCIWOŚCI | OPIS |
| --- | --- |
| Nazwa źródła zdarzeń | Nazwa Hello źródła zdarzenia. Ta nazwa musi być unikatowa w danym środowisku Insights serii czasu.
| Element źródłowy | Wybierz **Centrum IoT** toocreate źródłem zdarzenia Centrum IoT.
| Identyfikator subskrypcji | Wybierz subskrypcję hello, w której utworzono to Centrum IoT.
| Nazwa centrum IoT | Wybierz nazwę hello hello Centrum IoT.
| Nazwa zasad Centrum IoT | Wybierz zasad dostępu hello udostępnionych, które znajdują się na powitania kartę Ustawienia Centrum IoT. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu. Hello udostępnionych zasady dostępu dla źródła zdarzeń *musi* ma **usługa połączyć** uprawnienia.
| Grupy odbiorców Centrum IoT | Witaj grupy odbiorców zdarzeń tooread z hello Centrum IoT. Jest zdecydowanie zalecane toouse dedykowanej grupy klientów dla źródła zdarzenia.

### <a name="provide-iot-hub-settings-manually"></a>Podaj ustawienia Centrum IoT ręcznie

Witaj poniższej tabeli opisano każdej właściwości w karcie nowe źródło zdarzeń hello z jego opisem podczas wprowadzania ustawień ręcznie:

| NAZWA WŁAŚCIWOŚCI | OPIS |
| --- | --- |
| Nazwa źródła zdarzeń | Nazwa Hello źródła zdarzenia. Ta nazwa musi być unikatowa w danym środowisku Insights serii czasu.
| Element źródłowy | Wybierz **Centrum IoT** toocreate źródłem zdarzenia Centrum IoT.
| Identyfikator subskrypcji | Subskrypcja Hello, w której utworzono to Centrum IoT.
| Grupa zasobów | Subskrypcja Hello, w której utworzono to Centrum IoT.
| Nazwa centrum IoT | Nazwa Hello Centrum IoT. Podczas tworzenia Centrum IoT należy też nadać mu nazwę
| Nazwa zasad Centrum IoT | zasad dostępu Hello udostępnionych, które mogą być tworzone na powitania kartę Ustawienia Centrum IoT. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu. Hello udostępnionych zasady dostępu dla źródła zdarzeń *musi* ma **usługa połączyć** uprawnienia.
| Klucz zasad Centrum IoT | klucz dostęp współdzielony Hello używany tooauthenticate dostępu toohello — przestrzeń nazw magistrali usług. Typ hello klucz podstawowy lub pomocniczy tutaj.
| Grupy odbiorców Centrum IoT | Witaj grupy odbiorców zdarzeń tooread z hello Centrum IoT. Jest zdecydowanie zalecane toouse dedykowanej grupy klientów dla źródła zdarzenia.

## <a name="next-steps"></a>Następne kroki

1. Dodaj środowisku tooyour zasad dostępu do danych [danych Definiowanie zasad dostępu](time-series-insights-data-access.md)
1. Dostęp do środowiska w hello [portalu Insights serii czasu](https://insights.timeseries.azure.com)
