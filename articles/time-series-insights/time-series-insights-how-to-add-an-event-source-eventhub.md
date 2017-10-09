---
title: "tooadd aaaHow środowiska Azure czas serii Insights tooyour źródła zdarzeń Centrum zdarzeń | Dokumentacja firmy Microsoft"
description: "W tym samouczku opisano, jak tooadd zdarzenie czyli źródła połączonych tooan Centrum zdarzeń tooyour Insights serii czasu środowiska"
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
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>Jak tooadd źródłem zdarzenia Centrum zdarzeń

W tym samouczku opisano, jak toouse hello Azure tooadd portalu źródło zdarzenia, które odczytuje ze środowiska czasu serii Insights tooyour Centrum zdarzeń.

## <a name="prerequisites"></a>Wymagania wstępne

Utworzono Centrum zdarzeń i pisania tooit zdarzenia. Aby uzyskać więcej informacji dotyczących usługi Event Hubs, zobacz <https://azure.microsoft.com/services/event-hubs/>

> [Grupy konsumentów] Źródło zdarzenia każdego Insights serii czasu musi toohave własnej dedykowanej grupy klientów, które nie są współużytkowane z innym klientom. Jeśli korzystać z wielu czytników zdarzeń z hello tej samej grupy konsumentów, wszystkie czytniki są prawdopodobnie toosee błędów. Należy pamiętać, że jest również maksymalnie 20 grup odbiorców, na Centrum zdarzeń. Aby uzyskać więcej informacji, zobacz hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Wybierz opcję importu

Ustawienia Hello hello źródło zdarzenia można wprowadzić ręcznie lub Centrum zdarzeń można wybierać z hello centra zdarzeń, które są dostępne tooyou.
W hello **opcję importu** selektora, wybierz jedną z hello następujące opcje:

* Podaj ustawienia Centrum zdarzeń ręcznie
* Użyj Centrum zdarzeń z dostępnych subskrypcji

### <a name="select-an-available-event-hub"></a>Wybierz dostępny Centrum zdarzeń

Hello poniższej tabeli opisano poszczególne opcje hello kartę nowe źródło zdarzeń z jego opisem podczas wybierania dostępne Centrum zdarzeń jako źródło zdarzenia:

| NAZWA WŁAŚCIWOŚCI | OPIS |
| --- | --- |
| Nazwa źródła zdarzeń | Nazwa Hello źródła zdarzenia. Ta nazwa musi być unikatowa w danym środowisku Insights serii czasu.
| Element źródłowy | Wybierz **Centrum zdarzeń** toocreate źródłem zdarzenia Centrum zdarzeń.
| Identyfikator subskrypcji | Wybierz subskrypcję hello, w której utworzono to Centrum zdarzeń.
| Przestrzeń nazw magistrali usług | Wybierz hello przestrzeni nazw usługi Service Bus, która zawiera hello Centrum zdarzeń.
| Nazwa Centrum zdarzeń | Wybierz nazwę hello hello Centrum zdarzeń.
| Nazwa zasad Centrum zdarzeń | Wybierz hello udostępnionych zasad dostępu, które mogą być tworzone na karcie Konfigurowanie Centrum zdarzeń hello. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu. Hello udostępnionych zasady dostępu dla źródła zdarzeń *musi* ma **odczytu** uprawnienia.
| Grupy konsumentów Centrum zdarzeń | Witaj grupy odbiorców zdarzeń tooread z hello Centrum zdarzeń. Jest zdecydowanie zalecane toouse dedykowanej grupy klientów dla źródła zdarzenia.

### <a name="provide-event-hub-settings-manually"></a>Podaj ustawienia Centrum zdarzeń ręcznie

Witaj poniższej tabeli opisano każdej właściwości w karcie nowe źródło zdarzeń hello z jego opisem podczas wprowadzania ustawień ręcznie:

| NAZWA WŁAŚCIWOŚCI | OPIS |
| --- | --- |
| Nazwa źródła zdarzeń | Nazwa Hello źródła zdarzenia. Ta nazwa musi być unikatowa w danym środowisku Insights serii czasu.
| Element źródłowy | Wybierz **Centrum zdarzeń** toocreate źródłem zdarzenia Centrum zdarzeń.
| Identyfikator subskrypcji | Subskrypcja Hello, w której utworzono to Centrum zdarzeń.
| Grupa zasobów | Subskrypcja Hello, w której utworzono to Centrum zdarzeń.
| Przestrzeń nazw magistrali usług | Przestrzeń nazw magistrali usług to kontener dla zestawu jednostek do obsługi komunikatów. Podczas tworzenia nowego Centrum zdarzeń utworzonego również przestrzeni nazw usługi Service Bus.
| Nazwa Centrum zdarzeń | Nazwa Hello Centrum zdarzeń. Podczas tworzenia Centrum zdarzeń należy też nadać mu nazwę
| Nazwa zasad Centrum zdarzeń | Witaj zasad dostępu współdzielonego, które mogą być tworzone na karcie Konfigurowanie Centrum zdarzeń hello. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu. Hello udostępnionych zasady dostępu dla źródła zdarzeń *musi* ma **odczytu** uprawnienia.
| Klucz zasad Centrum zdarzeń | klucz dostęp współdzielony Hello używany tooauthenticate dostępu toohello — przestrzeń nazw magistrali usług. Typ hello klucz podstawowy lub pomocniczy tutaj.
| Grupy konsumentów Centrum zdarzeń | Witaj grupy odbiorców zdarzeń tooread z hello Centrum zdarzeń. Jest zdecydowanie zalecane toouse dedykowanej grupy klientów dla źródła zdarzenia.

## <a name="next-steps"></a>Następne kroki

1. Dodaj środowisku tooyour zasad dostępu do danych [danych Definiowanie zasad dostępu](time-series-insights-data-access.md)
1. Dostęp do środowiska w hello [portalu Insights serii czasu](https://insights.timeseries.azure.com)
