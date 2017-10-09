---
title: "Statystyka aaaReal czasu w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Statystyki w czasie rzeczywistym udostępnia w czasie rzeczywistym danych dotyczących wydajności hello Azure CDN podczas dostarczania zawartości tooyour klientów."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Omówienie
W tym dokumencie opisano statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN.  Ta funkcja udostępnia w czasie rzeczywistym danych, takie jak przepustowości, pamięci podręcznej stanów i tooyour równoczesnych połączeń CDN profilu podczas dostarczania zawartości tooyour klientów. Dzięki temu ciągłego monitorowania kondycji hello usługi w dowolnym momencie, w tym zdarzenia dotyczące przejdź na żywo.

dostępne są następujące wykresy Hello:

* [Przepustowość](#bandwidth)
* [Kody stanu](#status-codes)
* [Stany pamięci podręcznej](#cache-statuses)
* [Połączenia](#connections)

## <a name="accessing-real-time-stats"></a>Uzyskiwanie dostępu do statystyki w czasie rzeczywistym
1. W hello [Azure Portal](https://portal.azure.com), Przeglądaj tooyour profilu CDN.
   
    ![Blok profilu CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
3. Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **statystyki w czasie rzeczywistym** wysuwane okno.  Polecenie **HTTP dużego obiektu**.
   
    ![Portal zarządzania usługi CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    Wykresy statystyki w czasie rzeczywistym Hello są wyświetlane.

Każda z wykresy hello Wyświetla statystyki w czasie rzeczywistym dla hello wybrany przedział czasu, uruchamianie podczas ładowania strony hello.  Wykresy Hello automatycznie aktualizowane co kilka sekund.  Witaj **Odśwież wykres** przycisku, jeśli jest obecny, spowoduje wyczyszczenie hello wykresu, po czym zostanie wyświetlona tylko wybrane hello danych.

## <a name="bandwidth"></a>Przepustowość
![Wykres przepustowości](./media/cdn-real-time-stats/cdn-bandwidth.png)

Witaj **przepustowości** wykres przedstawia hello ilość przepustowości używanej w ramach bieżącej platformie hello za pośrednictwem hello wybrany okres. Witaj przyciemnione część hello wykres wskazuje użycia przepustowości. Hello dokładną ilość przepustowości aktualnie używane jest wyświetlana bezpośrednio pod hello wykres liniowy.

## <a name="status-codes"></a>Kody stanu
![Wykres kod stanu](./media/cdn-real-time-stats/cdn-status-codes.png)

Witaj **kodów stanu** wykres wskazuje, jak często niektórych kody odpowiedzi HTTP dochodzi za pośrednictwem hello wybrany okres.

> [!TIP]
> Opis każdej opcji Kod stanu HTTP, zobacz [kody stanu HTTP CDN Azure](https://msdn.microsoft.com/library/mt759238.aspx).
> 
> 

Bezpośrednio nad hello wykres zostanie wyświetlona lista kodów stanu HTTP. Ta lista wskazuje poszczególnych kodów stanu, który można umieścić w hello wykres liniowy i hello bieżąca liczba zdarzeń na sekundę dla tego kodu stanu. Domyślnie wiersz jest wyświetlany dla każdej z tych kodów stanu hello wykresie. Jednak można wybrać tooonly kodów stanu hello monitor, które mają specjalne znaczenie dla danej konfiguracji sieci CDN. toodo, sprawdź hello potrzeby kodów stanu i wyczyść wszystkie inne opcje, a następnie kliknij **Odśwież wykres**. 

Można ukryć danych zarejestrowanych dla kodu określonego stanu.  Z legendy hello bezpośrednio pod hello wykresu kliknij przycisk Kod stanu hello ma toohide. Kod stanu Hello będą natychmiast ukryte hello wykresu. Ponowne kliknięcie tego kodu stanu spowoduje toobe tej opcji, ponownie wyświetlone.

## <a name="cache-statuses"></a>Stany pamięci podręcznej
![Wykres stanów pamięci podręcznej](./media/cdn-real-time-stats/cdn-cache-status.png)

Witaj **pamięci podręcznej stanów** wykres wskazuje, jak często niektóre rodzaje pamięci podręcznej stanów dochodzi za pośrednictwem hello wybrany okres. 

> [!TIP]
> Opis opcji Kod stanu każdego pamięci podręcznej, zobacz [kodów stanu systemu Azure CDN pamięci podręcznej](https://msdn.microsoft.com/library/mt759237.aspx).
> 
> 

Zostanie wyświetlona lista kodów stanu pamięci podręcznej bezpośrednio nad hello wykresu. Ta lista wskazuje poszczególnych kodów stanu, który można umieścić w hello wykres liniowy i hello bieżąca liczba zdarzeń na sekundę dla tego kodu stanu. Domyślnie wiersz jest wyświetlany dla każdej z tych kodów stanu hello wykresie. Jednak można wybrać tooonly kodów stanu hello monitor, które mają specjalne znaczenie dla danej konfiguracji sieci CDN. toodo, sprawdź hello potrzeby kodów stanu i wyczyść wszystkie inne opcje, a następnie kliknij **Odśwież wykres**. 

Można ukryć danych zarejestrowanych dla kodu określonego stanu.  Z legendy hello bezpośrednio pod hello wykresu kliknij przycisk Kod stanu hello ma toohide. Kod stanu Hello będą natychmiast ukryte hello wykresu. Ponowne kliknięcie tego kodu stanu spowoduje toobe tej opcji, ponownie wyświetlone.

## <a name="connections"></a>Połączenia
![Wykres połączeń](./media/cdn-real-time-stats/cdn-connections.png)

Ten wykres wskazuje liczbę połączeń zostały ustalonych tooyour serwery krawędzi. Każde żądanie dla zasobu, który przechodzi przez naszych wyników sieci CDN w połączeniu.

## <a name="next-steps"></a>Następne kroki
* Bądź na bieżąco z [alertów w czasie rzeczywistym w usłudze Azure CDN](cdn-real-time-alerts.md)
* Dig głębiej z [zaawansowane raporty HTTP](cdn-advanced-http-reports.md)
* Analizowanie [wzorców użycia](cdn-analyze-usage-patterns.md)

