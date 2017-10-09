---
title: "zalecenia usługi Advisor koszt aaaAzure | Dokumentacja firmy Microsoft"
description: "Użyj Azure Advisor toooptimize hello koszt wdrożeń platformy Azure."
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
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Zalecenia doradcy w zakresie koszt

Advisor pomaga zoptymalizować i zmniejszyć ogólną Azure wydatków, określając bezczynności i wyczerpaniu zasobów. Zalecenia z hello mogą uzyskać kosztem **koszt** kartę na pulpicie nawigacyjnym usługi Advisor hello.

![Karta koszt usługi Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Optymalizacja spędzają na zmieniając niedostatecznie wystąpień maszyny wirtualnej 
Mimo że niektóre scenariusze aplikacji może spowodować niskiego poziomu wykorzystania zgodnie z projektem, można często zaoszczędzić, zarządzając hello rozmiaru i liczby maszyn wirtualnych. Klasyfikator monitoruje użycie maszyny wirtualnej w ciągu ostatnich 14 dni, a następnie identyfikuje niskiego wykorzystania maszyn wirtualnych. Maszyny wirtualne, których użycie procesora CPU wynosi 5 procent lub mniej i użycie sieci jest 7 MB lub mniej przez cztery lub więcej dni są traktowane jako niskiego wykorzystania maszyn wirtualnych.

Pokazuje Advisor hello szacowany koszt kontynuowanie toorun maszyny wirtualnej, dzięki czemu można wybrać tooshut w dół, lub zmienić jego rozmiar.  

![Klasyfikator koszt zalecenia dotyczące zmiany rozmiaru maszyny wirtualne](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Użyj ekonomiczne rozwiązanie toomanage cele dotyczące wydajności wielu baz danych serwera SQL
Klasyfikator identyfikuje wystąpienia programu SQL server, które mogą korzystać z tworzenie elastycznych pul baz danych. Elastyczne pule baz danych Podaj toomanage proste i ekonomiczne rozwiązanie hello cele dotyczące wydajności z wieloma bazami danych, które mają różne wzorce użycia. Aby uzyskać więcej informacji na temat Azure pule elastyczne, zobacz [co to jest pula elastyczna Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Klasyfikator koszt zalecenia dotyczące elastyczne pule baz danych](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Jak tooaccess koszt zalecenia w programie Azure Advisor

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. W okienku po lewej stronie powitania kliknij **więcej usług**.

3. W hello usługa okienku menu, w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.  
 pulpit nawigacyjny usługi Advisor Hello jest wyświetlany.

4. Na pulpicie nawigacyjnym usługi Advisor hello, kliknij przycisk hello **koszt** kartę.

5. Wybierz subskrypcję hello, dla którego chcesz tooreceive zalecenia, a następnie kliknij **Uzyskaj zalecenia**.

> [!NOTE]
> tooaccess zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor. Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* powoduje uruchomienie hello Advisor hello pulpitu nawigacyjnego i klika przycisk **Uzyskaj zalecenia** przycisku. Jest to *jednorazowa operacja*. Po zarejestrowaniu subskrypcji hello są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* subskrypcji, grupy zasobów, lub określonego zasobu.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat zalecenia doradcy w zakresie, zobacz:
* [Wprowadzenie tooAdvisor](advisor-overview.md)
* [Rozpoczęcie pracy](advisor-get-started.md)
* [Zalecenia doradcy w zakresie wydajności](advisor-cost-recommendations.md)
* [Zalecenia doradcy w zakresie wysokiej dostępności](advisor-cost-recommendations.md)
* [Zalecenia doradcy w zakresie zabezpieczeń](advisor-cost-recommendations.md)
