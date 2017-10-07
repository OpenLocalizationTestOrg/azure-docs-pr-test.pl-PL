---
title: "aaaData zasady dostępu w usłudze Azure czas serii Insights | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, zasady dostępu do danych toomanage w czasie serii Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Udziel dostępu danych tooa Insights serii czasu środowiska przy użyciu portalu Azure

Środowiska usługi Time Series Insights udostępniają dwa niezależne rodzaje zasad dostępu:

* Zasady dostępu do zarządzania
* Zasady dostępu do danych

Oba rodzaje zasad umożliwiają przyznawanie podmiotom usługi Azure Active Directory (użytkownikom i aplikacjom) różnych uprawnień w określonym środowisku. Hello podmiotów zabezpieczeń (Użytkownicy i aplikacje) muszą należeć toohello active directory (lub "Dzierżawą platformy Azure") skojarzone z subskrypcją hello zawierający hello środowiska.

Zasady dostępu administracyjnego przyznać uprawnienia powiązane toohello konfiguracji środowiska hello, takich jak
*   Tworzenie i usuwanie środowiska hello źródła zdarzeń odwołania zestawów danych i
*   Zarządzanie zasadami dostępu hello danych.

Zasady dostępu do danych uprawnienia tooissue kwerend danych, manipulować danymi odwołania w środowisku hello i udostępniaj zapisane kwerendy oraz skojarzone ze środowiskiem hello perspektywy.

Witaj dwa rodzaje zasady Zezwalaj wyraźnej separacji między zarządzania dostępem toohello hello środowiska i uzyskiwanie dostępu do danych toohello w środowisku hello. Na przykład jest możliwe toosetup środowisko tak, aby hello właściciela/twórcy środowiska hello jest usuwany z hello dostępu do danych. Oraz użytkowników i usług, które mogą tooread dane ze środowiska hello udziela się żadna konfiguracja toohello dostępu hello środowiska.

## <a name="grant-data-access"></a>Przyznawanie dostępu do danych
Witaj poniższej procedurze pokazano, jak toogrant dane — dostęp do głównej nazwy użytkownika:

1.  Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2.  Kliknij przycisk "Wszystkie zasoby" hello menu po lewej stronie powitania hello portalu Azure.
3.  Wybierz środowisko usługi Time Series Insights.

  ![Zarządzanie źródło czasu serii Insights hello - środowiska](media/data-access/getstarted-grant-data-access1.png)

4.  Wybierz pozycję „Dostęp do płaszczyzny danych” i kliknij przycisk „Dodaj”.

  ![Zarządzanie źródła czasu serii Insights hello — Dodawanie](media/data-access/getstarted-grant-data-access2.png)

5.  Kliknij przycisk „Wybierz użytkownika”.
6.  Wyszukiwanie i wybrać użytkownika, powitalne wiadomości e-mail.
7.  Kliknij pozycję „Wybierz” w bloku „Wybierz użytkownika”.

  ![Zarządzanie źródła czasu serii Insights hello — wybierz użytkownika](media/data-access/getstarted-grant-data-access3.png)

8.  Kliknij pozycję „Wybierz rolę”.
9.  Wybierz "Współautora", jeśli chcesz tooallow użytkownika toochange odwołanie do danych i udostępniać innym użytkownikom środowiska hello perspektyw i zapisane kwerendy. W przeciwnym razie wybierz "Czytnika" tooallow użytkownika kwerend danych w środowisku hello i zapisać osobiste (nie udostępnione) zapytania w środowisku hello.
10. Kliknij przycisk Ok, w bloku "Wybierz rolę" hello.

  ![Zarządzanie hello czasu serii Insights źródło - wybierz rolę](media/data-access/getstarted-grant-data-access4.png)

11. Kliknij przycisk Ok, w bloku "Wybierz rolę użytkownika" hello.
12. Powinien zostać wyświetlony następujący ekran:

  ![Zarządzanie hello czasu serii Insights źródło - wyników](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Następne kroki

* [Tworzenie źródła zdarzeń](time-series-insights-add-event-source.md)
* [Wysyłanie zdarzeń](time-series-insights-send-events.md) toohello źródło zdarzenia
* Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)
