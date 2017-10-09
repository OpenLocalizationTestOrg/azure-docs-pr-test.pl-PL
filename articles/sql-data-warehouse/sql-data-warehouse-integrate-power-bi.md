---
title: "aaaUse usługi Power BI z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z usługi Power BI z usługą Magazyn danych SQL Azure związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Użyj usługi Power BI z usługą Magazyn danych SQL
Podobnie jak w przypadku bazy danych SQL Azure SQL danych magazynu bezpośrednie połączenie umożliwia tooleverage użytkownika zaawansowanych przekazywanie logicznej obok hello możliwości analityczne usługi Power BI.  Za pomocą bezpośrednich Connect zapytania są wysyłane wstecz tooyour Azure SQL Data Warehouse w czasie rzeczywistym Ci poznać platformę hello danych.  To, połączone z hello skali usługi SQL Data Warehouse umożliwia użytkownikom toocreate dynamicznych raportów w minutach przed terabajtów danych.  Ponadto wprowadzenie hello hello Otwórz w przycisk usługi Power BI umożliwia użytkownikom toodirectly Połącz usługi Power BI tootheir SQL Data Warehouse bez zbierania informacji z innych części Azure.

Podczas używania połączenia bezpośredniego należy Uwaga:

* Określ nazwę FQDN serwera hello podczas łączenia z (Aby uzyskać więcej informacji zobacz poniżej)
* Upewnij się, reguły zapory dla bazy danych hello są skonfigurowane za "Zezwalaj na dostęp tooAzure usługi".
* Wszystkie akcje, takich jak wybierając kolumnę lub Dodawanie filtru bezpośrednio zwrócą hello magazynu danych
* Kafelki są odświeżane co około 15 minut (w przypadku odświeżania toobe zaplanowane nie są konieczne)
* Funkcja pytania i odpowiedzi nie jest dostępna dla bezpośrednie łączenie zestawów danych
* Zmiany schematu nie są odczytywane automatycznie
* Wszystkie zapytania bezpośredniego połączenia limit czasu będzie 2 minuty

Te ograniczenia i uwagi może zmienić w dalszym ciągu tooimprove hello środowiska. tooconnect kroki Hello są szczegółowo opisane poniżej.  

## <a name="using-hello-open-in-power-bi-button"></a>Przy użyciu przycisku "Otwórz w usłudze Power BI" hello
Witaj najprostszy sposób toomove między magazyn danych SQL i usługi Power BI jest hello Otwórz w usłudze Power BI przycisku. Ten przycisk pozwala tooseamlessly rozpocząć tworzenie nowych pulpitów nawigacyjnych w usłudze Power BI.  

1. Rozpoczęto tooget Przejdź tooyour wystąpienie usługi SQL Data Warehouse w hello klasycznego portalu Azure.
2. Kliknij przycisk "Otwórz w usłudze Power BI" hello.
3. Jeśli nie jesteśmy w stanie toosign w bezpośrednio, lub jeśli nie masz konta usługi Power BI, konieczne będzie toosign w.  
4. Pojawi się, że wstępne wypełnianie toohello strona połączenia SQL Data Warehouse, hello informacje z usługą SQL Data Warehouse.
5. Po wprowadzeniu poświadczeń będzie tooyour pełni podłączonej usługi SQL Data Warehouse.

## <a name="connecting-through-hello-power-bi-portal"></a>Łączenie za pośrednictwem portalu usługi Power BI hello
W dodatku toousing hello Otwórz w usłudze Power BI przycisku użytkownicy mogą łączyć tootheir SQL Data Warehouse za pośrednictwem hello Power BI portalu.

1. Kliknij przycisk "Pobierz dane" u dołu okienka nawigacji hello hello.
2. Wybierz "Bazy danych".
3. Raz na stronie powitania, baz danych, wybierz "Azure SQL Data Warehouse", a następnie kliknij przycisk "Połącz".
4. Wprowadź informacje niezbędne połączenia hello.  Nazwa serwera, a nazwa bazy danych znajdują się w hello portalu Azure.
5. Nastąpi przekierowanie ponownie się, że nazwa hello wystąpienia zostanie wyświetlona strona głównego toohello usługi Power Bi i po nawiązaniu połączenia z nowego wpisu w obszarze "Zestaw danych".  
6. Możesz kliknąć hello nowy zestaw danych tooexplore wszystkie hello tabele i widoki w bazie danych. Wybierając kolumnę wyśle źródła wstecz toohello kwerendy, dynamicznego tworzenia wizualny. Te elementy wizualne mogą być zapisywane w nowy raport i ponownie przypięty tooyour pulpitu nawigacyjnego.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
