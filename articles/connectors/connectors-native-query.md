---
title: Akcja kwerendy hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft
description: "Przegląd hello zapytania akcji do wykonania akcji, takich jak tablicy filtrów."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Rozpoczynanie pracy z akcją zapytań hello
Za pomocą akcji zapytania hello, możesz pracować z partii tablice tooaccomplish przepływy pracy i do:

* Utwórz zadania dla wszystkich rekordów o wysokim priorytecie z bazy danych.
* Zapisz wszystkie załączniki plików PDF do wiadomości e-mail do obiektów blob platformy Azure.

tooget uruchomiony przy użyciu akcji zapytania hello w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Za pomocą akcji zapytania hello
Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki. [Dowiedz się więcej o akcjach](connectors-overview.md).  

Akcja kwerendy Hello aktualnie ma jedną operację o nazwie tablicy filtrów hello, która jest widoczna w Projektancie hello. To pozwala tooquery tablicy i zwraca zestawu wyników filtrowane.

Oto, jak można dodać go w aplikacji logiki:

1. Wybierz hello **nowy krok** przycisku.
2. Wybierz **Dodaj akcję**.
3. W polu wyszukiwania akcji hello wpisz **filtru** toolist hello **tablicy filtrów** akcji.
   
    ![Wybierz akcję zapytania hello](./media/connectors-native-query/using-action-1.png)
4. Wybierz toofilter tablicy. (hello Poniższy zrzut ekranu przedstawia hello tablicę wyniki wyszukiwania usługi Twitter.)
5. Utwórz tooevaluate warunku w każdym elemencie. (hello następującego zrzutu ekranu filtry tweetów od użytkowników, którzy mają więcej niż 100 adherentami).
   
    ![Akcja kwerendy hello ukończone](./media/connectors-native-query/using-action-2.png)
   
    Akcja Hello dane wyjściowe obejmują nowe tablica, która zawiera tylko wyniki, które spełniają wymagań filtru hello.
6. Kliknij przycisk hello lewego górnego rogu hello toosave narzędzi i Twoje logiki aplikacji zapisze zarówno i publikowanie (Aktywuj).

## <a name="query-action"></a>Akcja kwerendy
Poniżej przedstawiono szczegóły hello hello akcję, która obsługuje ten łącznik. Łącznik Hello ma jedną akcję możliwe.

| Akcja | Opis |
| --- | --- |
| Macierz filtru |Sprawdza warunek dla każdego elementu w tablicy i zwraca wyniki hello |

## <a name="action-details"></a>Szczegóły akcji
Akcja kwerendy Hello jest dostarczany z jedną akcję możliwe. Witaj poniższych tabelach opisano hello wymagane i opcjonalne pola wejściowego dla akcji hello i hello odpowiednie dane wyjściowe szczegóły, które są skojarzone z przy użyciu akcji hello.

### <a name="filter-array"></a>Macierz filtru
Oto Hello pól wejściowych dla akcji hello, dzięki czemu żądania wychodzącego HTTP.
A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Z * |Z |Witaj toofilter tablicy |
| Warunek * |gdzie |Witaj tooevaluate warunek dla każdego elementu |

<br>

### <a name="output-details"></a>Szczegóły danych wyjściowych
Witaj poniżej przedstawiono szczegóły danych wyjściowych dla hello odpowiedzi HTTP.

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Filtrowane tablicy |Tablica |Tablica, która zawiera obiekt dla każdego wyniku filtrowane |

## <a name="next-steps"></a>Następne kroki
Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).

