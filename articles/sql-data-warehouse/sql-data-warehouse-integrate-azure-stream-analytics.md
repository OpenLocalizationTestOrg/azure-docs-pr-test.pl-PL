---
title: "aaaUse Azure Stream Analytics z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z usługi Azure Stream Analytics z usługą Magazyn danych SQL Azure związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Użyj usługi Azure Stream Analytics z usługą Magazyn danych SQL
Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzanie złożonych zdarzeń małe opóźnienia, skalowalne, wysoko dostępne za pośrednictwem przesyłania strumieniowego danych w chmurze hello. Dowiedz się podstawy hello odczytując [tooAzure wprowadzenie Stream Analytics][Introduction tooAzure Stream Analytics]. Można następnie Dowiedz się jak hello toocreate rozwiązanie end-to-end z Stream Analytics, wykonując [rozpocząć korzystanie z usługi Azure Stream Analytics] [ Get started using Azure Stream Analytics] samouczka.

W tym artykule dowiesz się, jak toouse Azure SQL Data Warehouse bazy danych dla zadań para analiza ujściem danych wyjściowych.

## <a name="prerequisites"></a>Wymagania wstępne
Najpierw uruchom za pomocą hello następujące kroki w hello [rozpocząć korzystanie z usługi Azure Stream Analytics] [ Get started using Azure Stream Analytics] samouczka.  

1. Tworzenie Centrum zdarzeń dane wejściowe
2. Skonfiguruj i uruchom aplikację generator zdarzeń
3. Zainicjuj obsługę zadania usługi analiza strumienia
4. Określ dane wejściowe zadania i zapytanie

Następnie utwórz bazę danych magazynu danych SQL Azure

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Określ dane wyjściowe zadania: baza danych Azure SQL Data Warehouse
### <a name="step-1"></a>Krok 1
W przypadku zadania Stream Analytics kliknij **dane wyjściowe** od góry hello hello strony, a następnie kliknij przycisk **dodać danych wyjściowych**.

### <a name="step-2"></a>Krok 2
Wybierz bazę danych SQL, a następnie kliknij przycisk Dalej.

![][add-output]

### <a name="step-3"></a>Krok 3
Wprowadź następujące wartości na następnej stronie powitania hello:

* *Dane wyjściowe Alias*: Wprowadź przyjazną nazwę dla danych wyjściowych tego zadania.
* *Subskrypcja*:
  * Jeśli w bazie danych magazynu danych SQL jest w hello tej samej subskrypcji co zadanie usługi Stream Analytics hello, wybierz opcję użycia bazy danych SQL z bieżącej subskrypcji.
  * Jeśli baza danych jest w innej subskrypcji, wybierz Użyj bazy danych SQL z innej subskrypcji.
* *Baza danych*: należy określić nazwę hello docelowej bazy danych.
* *Nazwa serwera*: Określ nazwę serwera hello bazy danych hello właśnie zostało określone. Możesz użyć hello toofind klasycznego portalu Azure.

![][server-name]

* *Nazwa użytkownika*: Określ nazwę użytkownika konta, które ma uprawnienia do zapisu dla bazy danych hello hello.
* *Hasło*: Podaj hasło hello hello określone konto użytkownika.
* *Tabela*: Określ nazwę tabeli docelowej hello hello w bazie danych hello.

![][add-database]

### <a name="step-4"></a>Krok 4
Kliknij przycisk tooadd przycisk wyboru hello, to dane wyjściowe zadania i tooverify, że analiza strumienia może pomyślnie połączyć toohello bazy danych.

![][test-connection]

Baza danych toohello połączenia hello zakończy się powodzeniem, zobaczysz powiadomienie u dołu hello hello portalu. W dolnej hello tootest połączenia hello toohello bazy danych można kliknij przycisk Testuj połączenie.

## <a name="next-steps"></a>Następne kroki
Omówienie integracji, zobacz [Omówienie integracji usługi SQL Data Warehouse][SQL Data Warehouse integration overview].

Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
