---
title: aaaWhat jest Harmonogram systemu Azure? | Microsoft Docs
description: "Harmonogram systemu Azure pozwala toodeclaratively opisano akcje toorun w chmurze hello. Usługa następnie planuje i uruchamia te akcje automatycznie."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Co to jest usługa Azure Scheduler?
Harmonogram systemu Azure pozwala toodeclaratively opisano akcje toorun w chmurze hello. Usługa następnie planuje i uruchamia te akcje automatycznie.  Harmonogram dokonuje tego przy użyciu [hello portalu Azure](scheduler-get-started-portal.md), kod, [interfejsu API REST](https://msdn.microsoft.com/library/mt629143.aspx), lub Azure PowerShell.

Usługa Scheduler tworzy, obsługuje i wywołuje zaplanowane prace.  Usługa Scheduler nie hostuje żadnych obciążeń ani nie uruchamia żadnego kodu. *Wywołuje* ona jedynie kod hostowany gdzie indziej — na platformie Azure, lokalnie lub przez innego dostawcę. Wywoływanie następuje z użyciem protokołu HTTP, HTTPS, kolejki magazynu, kolejki magistrali usług lub tematu magistrali usług.

Harmonogramy harmonogramu [zadania](scheduler-concepts-terms.md), przechowuje historię wyników wykonania zadania jedną można sprawdzić, czy sposób niejednoznaczny i niezawodne toobe obciążeń harmonogramy uruchamiania. Zadań Webjob Azure (część hello funkcja Web Apps w usłudze Azure App Service) i innych funkcji planowania platformy Azure za pomocą harmonogramu w tle hello. Witaj [interfejsu API REST harmonogramu](https://msdn.microsoft.com/library/mt629143.aspx) umożliwia zarządzanie hello komunikacji dla tych akcji. W tym kontekście usługa Scheduler umożliwia prostą obsługę [złożonych harmonogramów i zaawansowanych cykli](scheduler-advanced-complexity.md).

Istnieje kilka scenariuszy, które nadają się użycie toohello harmonogramu. Na przykład:

* *Cykliczne akcje aplikacji:* okresowe gromadzenie danych z serwisu Twitter w ramach źródła danych.
* *Codzienna konserwacja:* codzienne oczyszczanie dzienników, tworzenie kopii zapasowych i wykonywanie innych zadań konserwacji. Na przykład administrator może wybrać tooback bazę danych hello godzinie 1:00 codziennie hello dalej 9 miesięcy.

Harmonogram umożliwia toocreate, zaktualizować, usuwanie, wyświetlanie, zadania i zarządzać nimi i [zadania kolekcje](scheduler-concepts-terms.md) programowo, za pomocą skryptów i w portalu hello.

## <a name="see-also"></a>Zobacz też
 [Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure](scheduler-advanced-complexity.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Azure Scheduler](scheduler-high-availability-reliability.md)

 [Limity, wartości domyślne i kody błędów usługi Azure Scheduler](scheduler-limits-defaults-errors.md)

 [Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler](scheduler-outbound-authentication.md)

