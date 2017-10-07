---
title: "zalecenia usługi Advisor wydajności aaaAzure | Dokumentacja firmy Microsoft"
description: "Użyj doradcy toooptimize hello wydajności Azure wdrożeń."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Zalecenia doradcy w zakresie wydajności

Azure zalecenia wydajności doradcy w zakresie zwiększyć szybkość hello i czas odpowiedzi aplikacji biznesowych o znaczeniu krytycznym. Zalecenia dotyczące wydajności z usługi Advisor można uzyskać na powitania **wydajności** karta pulpitu nawigacyjnego usługi Advisor hello.

![Karta wydajność usługi Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Poprawić wydajność bazy danych w usłudze Advisor bazy danych SQL

Advisor zapewnia spójne, skonsolidowanego widoku zaleceń dla wszystkich zasobów na platformie Azure. Umożliwia integrację z toobring doradcy bazy danych SQL można zalecenia dotyczące poprawy wydajności hello bazy danych SQL Azure. Doradca bazy danych programu SQL ocenia hello wydajności baz danych SQL Azure, analizując Twojej historii użycia. Oferuje zaleceń, które są najbardziej odpowiednie do uruchamiania typowych zadań hello bazy danych. 

> [!NOTE]
> zalecenia tooget bazy danych musi mieć o tydzień użycia, a w ciągu tygodnia musi być pewne spójnej działania. Doradca bazy danych SQL można zoptymalizować łatwiej wzorców zapytania spójna niż dla losowych seria działań.

Aby uzyskać więcej informacji o usłudze Advisor bazy danych SQL, zobacz [doradcy bazy danych SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Zalecenia dotyczące bazy danych SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Zwiększyć wydajność pamięci podręcznej Redis i niezawodności

Klasyfikator identyfikuje wystąpienia pamięci podręcznej Redis, gdzie mogą być niekorzystny wpływ na wydajność wysokie użycie pamięci, obciążenie serwera, przepustowości sieci lub dużej liczby połączeń klientów. Usługa Advisor udostępnia także najlepszych rozwiązań toohelp zalecenia uniknąć potencjalnych problemów. Aby uzyskać więcej informacji o pamięci podręcznej Redis, zobacz [Advisor pamięci podręcznej Redis](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Zwiększyć wydajność aplikacji usługi i niezawodności

Klasyfikator Azure integruje się poniżej rekomendowane najlepsze rozwiązania dla poprawy środowiska usługi aplikacji i wykrywania możliwości odpowiednie platformy. Przykłady zalecenia usługi aplikacji:
* Wykrywanie wystąpień, w którym na wyczerpaniu pamięci lub zasobów procesora CPU przez środowisk uruchomieniowych aplikacji z opcjami środki zaradcze.
* Wykrywanie wystąpień, w którym collocating zasoby, takie jak aplikacje sieci web i baz danych można zwiększyć wydajność i tańsze. 

Aby uzyskać więcej informacji na temat zalecenia usługi aplikacji, zobacz [najlepsze rozwiązania dotyczące usługi Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Zalecenia dotyczące usług aplikacji](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>Jak tooaccess zalecenia dotyczące wydajności w usługi Advisor

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. W okienku po lewej stronie powitania kliknij **więcej usług**.

3. W hello usługa okienku menu, w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.  
 pulpit nawigacyjny usługi Advisor Hello jest wyświetlany.

4. Na pulpicie nawigacyjnym usługi Advisor hello, kliknij przycisk hello **wydajności** kartę.

5. Wybierz subskrypcję hello, dla którego chcesz tooreceive zalecenia, a następnie kliknij **Uzyskaj zalecenia**.

> [!NOTE]
> tooaccess zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor. Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* powoduje uruchomienie hello Advisor hello pulpitu nawigacyjnego i klika przycisk **Uzyskaj zalecenia** przycisku. Jest to *jednorazowa operacja*. Po zarejestrowaniu subskrypcji hello są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* subskrypcji, grupy zasobów, lub określonego zasobu.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat zalecenia doradcy w zakresie, zobacz:

* [Wprowadzenie tooAdvisor](advisor-overview.md)
* [Wprowadzenie do usługi Advisor](advisor-get-started.md)
* [Zalecenia doradcy w zakresie koszt](advisor-performance-recommendations.md)
* [Zalecenia doradcy w zakresie wysokiej dostępności](advisor-high-availability-recommendations.md)
* [Zalecenia doradcy w zakresie zabezpieczeń](advisor-security-recommendations.md)

