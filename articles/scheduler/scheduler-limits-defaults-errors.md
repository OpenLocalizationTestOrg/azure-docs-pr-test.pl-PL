---
title: "Limity aaaScheduler oraz wartości domyślnych"
description: "Limity harmonogramu oraz wartości domyślnych"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Limity harmonogramu oraz wartości domyślnych
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Przydziały harmonogramu, limity ustawień domyślnych i limity
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>Witaj x-ms-request-id nagłówka
Każde żądanie dotyczące hello usługa Harmonogram zwraca nagłówka odpowiedzi o nazwie**x-ms-request-id**. Ten nagłówek zawiera wartości nieprzezroczystej, który unikatowo identyfikuje hello żądania.

Jeśli żądanie jest stale się niepowodzeniem, a ma zweryfikowaniu, że Żądanie hello jest poprawnie sformułowany, możesz użyć tej wartości tooreport hello błąd tooMicrosoft. W raporcie, uwzględniania hello wartości x-ms-request-id hello przybliżony czas tego hello żądanie, hello identyfikator subskrypcji hello, kolekcji zadań i/lub zadania i hello typ operacji, która hello próby żądania.

## <a name="see-also"></a>Zobacz też
 [Co to jest Scheduler?](scheduler-intro.md)

 [Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Azure Scheduler](scheduler-high-availability-reliability.md)

 [Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler](scheduler-outbound-authentication.md)

