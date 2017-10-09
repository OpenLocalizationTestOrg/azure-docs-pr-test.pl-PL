---
title: "aaaPlans i rozliczeń w harmonogramie Azure"
description: "Plany i rozliczeń w harmonogramie Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Plany i rozliczeń w harmonogramie Azure
## <a name="job-collection-plans"></a>Plany kolekcji zadań
Kolekcji zadań to płatna jednostka hello w harmonogramie Azure. Kolekcje zadań zawiera liczbę zadań i są dostępne w trzech planów — wolne, standardowa i Premium — opisane poniżej.

| **Planu kolekcji zadań** | **Maksymalna liczba zadań na kolekcji zadań** | **Maksymalna liczba cyklu** | **Kolekcje maksymalna liczba zadań dla subskrypcji** | **Limity** |
|:--- |:--- |:--- |:--- |:--- |
| **W warstwie bezpłatna** |5 zadań na kolekcji zadań |Raz na godzinę. Nie można wykonać zadania częściej niż raz na godzinę |Subskrypcji jest dozwolone w górę too1 bezpłatnej kolekcji zadań |Nie można użyć [obiekt wychodzącego autoryzacji HTTP](scheduler-outbound-authentication.md) |
| **Standardowa** |50 zadań na kolekcji zadań |Raz na minutę. Nie można wykonać zadania częściej niż raz na minutę |Subskrypcji jest dozwolone w górę too100 kolekcji standardowych zadań |Zestaw funkcji toofull dostępu harmonogramu |
| **P10 Premium** |50 zadań na kolekcji zadań |Raz na minutę. Nie można wykonać zadania częściej niż raz na minutę |Subskrypcja może się too10, 000 kolekcji zadań — wersja Premium P10. <a href="mailto:wapteams@microsoft.com">Skontaktuj się z nami</a> Aby uzyskać więcej informacji. |Zestaw funkcji toofull dostępu harmonogramu |
| **P20 Premium** |1000 zadań na kolekcji zadań |Raz na minutę. Nie można wykonać zadania częściej niż raz na minutę |Subskrypcja może się too10, 000 kolekcji zadań — wersja Premium P20. <a href="mailto:wapteams@microsoft.com">Skontaktuj się z nami</a> Aby uzyskać więcej informacji. |Zestaw funkcji toofull dostępu harmonogramu |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Aktualizacje i zmiany na starszą wersję plany kolekcji zadań
Można uaktualnić lub obniżyć planu kolekcji zadań w każdej chwili między hello planów wolne, standardowa i Premium. Jednak zmiany na starszą wersję tooa bezpłatnej kolekcji zadań, obniżenia poziomu hello może zakończyć się niepowodzeniem dla jednego z hello z następujących powodów:

* Bezpłatna kolekcja zadań już istnieje w subskrypcji hello
* Zadanie w kolekcji zadań hello ma wartość cyklu wyższe niż dozwolona liczba zadań w kolekcji zadań wolne. Witaj maksymalna wartość cyklu dozwolone w bezpłatna kolekcja zadań jest raz na godzinę
* Ma więcej niż 5 zadań w kolekcji zadań hello
* Zadanie w kolekcji zadań hello ma akcji HTTP lub HTTPS, która używa [obiekt wychodzącego autoryzacji HTTP](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Plany rozliczeń i Azure
Subskrypcje nie pobiera bezpłatnej kolekcji zadań. Jeśli masz więcej niż 100 kolekcji zadań standardowe (10 rozliczeń jednostek standard), wówczas jest lepsze toohave transakcji wszystkich zadań w planie premium hello kolekcji.

Jeśli masz jednej kolekcji zadań standardowa i premium jednej kolekcji zadań są rachunku standardowe rozliczeniowym jednostki *i* premium rozliczeniowym jednostki. opłaty usługi harmonogramu Hello na podstawie liczby hello kolekcje aktywnego zadania, które są ustawione tooeither standardowa lub premium; to jest dokładniej hello w dwóch następnych sekcjach.

## <a name="standard-billable-units"></a>Standardowe jednostki rozliczeń
Standardowe jednostki rozliczeniowy mogą obejmować się too10 kolekcji standardowych zadań. Ponieważ kolekcja standardowych zadań może zawierać maksymalnie too50 zadań na kolekcji zadań, standardowe jednostki rozliczeń umożliwia toohave subskrypcji, się zadania too500 — się tooalmost milionów 22 zadania wykonaniami miesięcznie.

Jeśli masz zakresu od 1 do 10 kolekcji standardowych zadań, zostaną naliczone 1 standardowe jednostki rozliczeń. Jeśli masz między kolekcji standardowych zadań 11 i 20 zostaną naliczone 2 standard jednostek rozliczeń. Jeśli między 21 i kolekcje 30 zadań standardowy, zostaną naliczone 3 standard jednostek rozliczeń i tak dalej.

## <a name="p10-premium-billable-units"></a>P10 Jednostki rozliczeniowy — wersja Premium
Jednostka rozliczeniowy premium P10 mogą obejmować się too10, 000 kolekcji zadań — wersja premium P10. Ponieważ kolekcja zadań — wersja premium P10 może zawierać maksymalnie too50 zadań na kolekcji zadań, jedną jednostkę rozliczeń premium umożliwia toohave subskrypcji, w górę too500, 000 zadania — się tooalmost MLD 22 zadania wykonaniami miesięcznie.

Jeśli masz zakresu od 1 do 10 000 kolekcji zadań — wersja premium, zostaną naliczone 1 jednostki rozliczeń — wersja premium P10. Jeśli masz zakresu od od 10 001 do 20 000 premium kolekcji zadań, zostaną naliczone 2 jednostek rozliczeń — wersja premium P10 i tak dalej.

W związku z tym zadania — wersja premium P10 kolekcje mają hello tę samą funkcjonalność kolekcji standardowych zadań hello ale udostępniono podział cen w przypadku, gdy aplikacja wymaga dużo kolekcji zadań.

## <a name="p20-premium-billable-units"></a>P20 Jednostki rozliczeniowy — wersja Premium
Jednostka rozliczeniowy premium P20 mogą obejmować się too5, 000 kolekcji zadań — wersja premium P20. Ponieważ kolekcja zadań — wersja premium P20 może zawierać maksymalnie too1, 000 zadań na kolekcji zadań jedną jednostkę rozliczeń premium umożliwia toohave subskrypcji, zapasowej too5 000, 000 zadania — w górę tooalmost MLD 220 zadania wykonaniami miesięcznie.

Kolekcje zadań — wersja premium p20 zapewnia hello takie same możliwości jak kolekcji zadań — wersja premium P10, ale obsługuje również większa numer zadań na kolekcji zadań i większą łączną liczbę zadań ogólny niż P10 premium dzięki czemu możesz toohave większą skalowalność.

## <a name="billing-and-active-status"></a>Stan rozliczeń i aktywne
Kolekcje zadań są zawsze aktywne, chyba że całej subskrypcji stała się do niektórych tymczasowego stan wyłączenia powodu toobilling problemów. Witaj tylko tooensure sposób, że kolekcja zadań nie jest on rozliczany jest tooeither ustawić toohello *wolne* planu lub toodelete kolekcji zadań hello.

Mimo że można wyłączyć wszystkich zadań w ramach kolekcji zadań, w ramach jednej operacji, nie zmienia się stan rozliczeń hello kolekcji zadań hello — będzie kolekcji zadań hello *nadal* opłaty będą naliczane. Podobnie zadanie puste kolekcje są traktowane jako aktywne i będą naliczane.

## <a name="pricing"></a>Cennik
Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik harmonogramu](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Zobacz też
 [Co to jest Scheduler?](scheduler-intro.md)

 [Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Azure Scheduler](scheduler-high-availability-reliability.md)

 [Limity, wartości domyślne i kody błędów usługi Azure Scheduler](scheduler-limits-defaults-errors.md)

 [Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler](scheduler-outbound-authentication.md)

