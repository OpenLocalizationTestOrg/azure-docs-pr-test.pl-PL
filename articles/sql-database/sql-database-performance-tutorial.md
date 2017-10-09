---
title: "wydajność aaaTroubleshoot problemy i zoptymalizować bazę danych | Dokumentacja firmy Microsoft"
description: "Zastosuj tooyour zalecenia dotyczące wydajności bazy danych SQL, a także czyść jak wgląd w toogain hello wydajność kwerend hello uruchamiania bazy danych"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Rozwiązywanie problemów z wydajnością i zoptymalizować bazę danych

Częstymi przyczynami słabej wydajności bazy danych są brakujące indeksy i nieprawidłowo zoptymalizowane zapytania. W tym samouczku dowiesz się:
> [!div class="checklist"]
> * Przejrzyj i Zastosuj przywrócić zalecenia dotyczące poprawy wydajności
> * Znajdź zapytania z wykorzystania zasobów wysoka
> * Znajdź zapytania długo działające

> Należy ciągłe obciążenie bazy danych z problemów z wydajnością — Brak indeksu na przykład tooreceive zalecenia.
>

## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Przejrzyj i Zastosuj zalecenia

Wykonaj te kroki tooapply zalecenie z systemu hello bazy danych:

1. Kliknij przycisk hello **zaleceń** w bloku bazy danych hello menu.

    ![zalecenie dotyczące wydajności](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Z listy hello zalecenia wybierz active zalecenia. W tym przykładzie Create Index.

    ![Wybierz zalecenia](./media/sql-database-performance-tutorial/create_index.png)

3. Zastosuj hello zalecenie, klikając hello **Zastosuj** przycisku. Opcjonalnie, przejrzyj szczegóły zalecenia hello i zawiera skrypt hello T-SQL zbyt można wykonać, klikając **Wyświetl skrypt** przycisku.

    ![Zastosuj zalecenia](./media/sql-database-performance-tutorial/apply.png)

4. [Opcjonalnie] Włączanie automatycznego dostrajania dla toobe zalecenia stosowane automatycznie.

    ![automatycznego dostrajania](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Przywróć zalecenia

Witaj doradcy bazy danych monitoruje każdy zalecenie zaimplementowana. Jeśli zalecenia nie poprawi obciążenia hello zostanie automatycznie przywrócony. Ręczne przywracanie zalecenie jest możliwe, ale nie jest konieczna w większości przypadków. toorevert zalecenia:

1. Przejdź do menu zalecenia dotyczące wydajności toohello i wybierz jedną z hello stosowane zalecenia.

    ![Wybierz zalecenia](./media/sql-database-performance-tutorial/select.png)

2. W widoku szczegółów powitania kliknij **Przywróć**.

    ![Przywróć zalecenia](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Znajdź zapytania hello, który wykorzystuje hello najwięcej zasobów

Wykonaj te kroki toofind hello zapytania zużywające hello najwięcej zasobów:

1. Polecenie hello **szczegółowe informacje o wydajności zapytań** w bloku bazy danych hello menu.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Wybierz typ zasobu.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Wybierz hello pierwszego zapytania w tabeli hello.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/select_query.png)

4. Przejrzyj szczegóły zapytania hello.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Znajdź hello najdłuższym uruchomione zapytania

1. Przejdź tooQuery szczegółowe informacje o wydajności i wybierz hello **długo działające kwerendy** kartę.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/long_running.png)

3. Wybierz hello pierwszego zapytania w tabeli hello.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/select_first_query.png)

4. Przejrzyj szczegóły zapytania hello.

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Następne kroki 
Częstymi przyczynami słabej wydajności bazy danych są brakujące indeksy i nieprawidłowo zoptymalizowane zapytania. W tym samouczku przedstawiono do:
> [!div class="checklist"]
> * Przejrzyj i Zastosuj przywrócić zalecenia dotyczące poprawy wydajności
> * Znajdź zapytania z wykorzystania zasobów wysoka
> * Znajdź zapytania długo działające

[Wskazówki dotyczące dostrajania wydajności bazy danych SQL](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
