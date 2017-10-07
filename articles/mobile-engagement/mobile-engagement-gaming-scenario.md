---
title: "aaaAzure implementacji usługi Mobile Engagement dla aplikacji do grania"
description: "Gry tooimplement scenariusza aplikacji usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Wdrożenie usługi Mobile Engagement z aplikacji do grania
## <a name="overview"></a>Omówienie
Uruchamiania gier uruchomiła nową aplikację gier role play/strategii połowy na podstawie. gry Hello została uruchomiona przez 6 miesięcy. Gry jest ogromny sukces i ma miliony pliki do pobrania i przechowywania hello jest bardzo duże tooother porównaniu uruchamiania gier aplikacji. Na powitania spotkaniu przeglądu co kwartał, uczestników zgodę potrzebnych tooincrease Średni przychód na użytkownika. Premium w grze pakiety są dostępne jako ofertach specjalnych. Te pakiety gier Zezwalaj użytkowników tooupgrade hello wygląd i wydajność swoich połowy wierszy i przynętą lub tackles w grze hello. Jednak sprzedaży pakietu są bardzo niskie. Dzięki zdecydują pierwszego tooanalyze powitania klienta doświadczenia z narzędziem analytics i następnie toodevelop zaangażowania program tooincrease sprzedaży, używając zaawansowane segmentacji.

Oparte na powitania [usługi Azure Mobile Engagement - Getting Started Guide z najlepszymi rozwiązaniami](mobile-engagement-getting-started-best-practices.md) tworzenia strategia zaangażowania.

## <a name="objectives-and-kpis"></a>Celów i wskaźników KPI
Spełnia wymagania najważniejszych uczestników hello gier. Wszystkie zgodzić się na jednym głównym celem - tooincrease premium pakietu sprzedaży przez 15%. Tworzenie one toomeasure firm kluczowych wskaźników wydajności (KPI) i dysk ten cel

* Na poziom gry hello te pakiety zakupionych?
* Co to jest hello przychód na użytkownika, na sesję na tydzień i miesięcznie?
* Co to są typy ulubionych zakupu hello?

Część 1 hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) wyjaśniono, jak toodefine hello celów i wskaźników KPI. 

Z powitalne biznesowe wskaźniki KPI dotyczące teraz zdefiniowany hello Mobile produktu Manager tworzy wskaźników KPI zaangażowania toodetermine nowego użytkownika trendów i przechowywania.

* Monitorowanie przechowywania i użyj na powitania po interwałów: codziennie, co 2 dni, co tydzień, co miesiąc i co 3 miesiące
* Liczby aktywnych użytkowników
* Klasyfikacja aplikacji Hello w hello przechowywania

Na podstawie zaleceń z hello zespół IT, powitania po techniczne kluczowych wskaźników wydajności zostały dodane hello tooanswer następujące pytania:

* Co to jest ścieżka do użytkownika (odwiedzenia strony, ile czasu użytkownicy poświęcają na nim)
* Liczba awarii (Crash) i zgłaszanie usterek napotkał na sesję
* Które wersje systemu operacyjnego działają moich użytkowników?
* Co to jest hello średni rozmiar ekranu dla moich użytkowników?
* Jakiego rodzaju łączności z Internetem masz moich użytkowników?

Dla poszczególnych wskaźników hello Mobile produktu Manager określa dane hello potrzebuje i gdzie znajduje się w jej podręcznikowym.

## <a name="engagement-program-and-integration"></a>Program zaangażowania i integracja
Przed zbudowaniem program zaangażowania zaawansowane, hello Dyrektor projektu Mobile odpowiedzialnym za hello projektu powinien wiedzę głębokie jak i kiedy produkty są używane przez użytkowników na powitania.

Po 3 miesiące hello Dyrektor projektu Mobile zebrał tooenhance wystarczającej ilości danych sprzedaży powiadomień wypychanych w aplikacji. ADAM uzyskuje informacje o który:

* Witaj pierwszego zakupu zwykle odbywa się na poziomie hello 14. 90% tych przypadkach zakupu hello jest bronie legendarnych $3.
* W takich przypadkach 80% użytkowników, które dokonały zakupu, kontynuuj hello produktu i wprowadź więcej zakupów.
* Użytkownicy, którzy przekazanego poziom hello 20, uruchom toospend więcej niż 10/ tydzień.
* Użytkownicy często toobuy pakietów premium na poziomie 16, 24 i 32.

Dziękujemy analizy toothis hello Dyrektor projektu Mobile decyduje toocreate konkretnych powiadomienia sekwencji tooincrease sprzedaży aplikacji. Tworzy trzy sekwencji powiadomień wypychanych, które wywołuje on: powitalny programu, Program sprzedaży i Program nieaktywne. Aby uzyskać więcej informacji można znaleźć toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
