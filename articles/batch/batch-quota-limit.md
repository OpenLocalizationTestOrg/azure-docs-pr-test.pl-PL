---
title: "Usługa przydziały i limity dla partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przydziałów domyślnych partii zadań Azure, ograniczenia i ograniczenia i zwiększa jak utworzyć żądanie przydziału"
services: batch
documentationcenter: 
author: v-dotren
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 210ba4a90f24ce9b0b55c4565028232c2b7fd7cc
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2017
---
# <a name="batch-service-quotas-and-limits"></a>Limity przydziału i limity usługi Batch

Zgodnie z innymi usługami Azure, istnieją ograniczenia na niektóre zasoby skojarzone z usługi partia zadań. Wiele tych limitów jest przydziałów domyślnych zastosowane przez platformę Azure na poziomie konta lub subskrypcji. W tym artykule omówiono te ustawienia domyślne, i jak mogą żądać przydziału zwiększa.

Pamiętać przydziałów podczas projektowania i skalowania w górę obciążeń partii. Na przykład jeśli pulę będzie niższa niż docelowy liczba węzłów obliczeniowych, określony, może osiągnięto limit przydziału rdzeni dla Twojego konta usługi partia zadań.

Można uruchomić wiele obciążeń usługi Batch na jednym koncie usługi Batch lub rozdzielić obciążenia pomiędzy konta tej usługi znajdujące się w jednej subskrypcji, ale różnych regionach świadczenia usługi Azure.

Jeśli planujesz uruchamianie obciążeń produkcyjnych w partii, może być konieczne zwiększyć co najmniej jeden przydziały powyżej domyślny. Jeśli użytkownik chce podnieść limit przydziału, możesz otworzyć online [żądania obsługi klienta](#increase-a-quota) bez dodatkowych opłat.

> [!NOTE]
> Limit przydziału jest limit kredytu nie gwarancji pojemności. Jeśli wymagana pojemność na dużą skalę, skontaktuj się z pomocą techniczną platformy Azure.
> 
> 

## <a name="resource-quotas"></a>Limity przydziałów zasobów
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

### <a name="quotas-in-user-subscription-mode"></a>Przydziały w trybie użytkownika subskrypcji

Jeśli starszej wersji interfejsu API partii jest używany do tworzenia konta usługi partia zadań z trybem przydziału puli ustawioną **subskrypcji użytkownika**, przydziały są stosowane w inny sposób. W tym trybie nie jest zalecane, maszyny wirtualne wsadowe i inne zasoby są tworzone bezpośrednio w Twojej subskrypcji po utworzeniu puli. Limit przydziału rdzeni partii zadań Azure nie ma zastosowania do konto utworzone w tym trybie. Zamiast tego przydziały w subskrypcji dla regionalne obliczeniowe rdzeni i inne zasoby są stosowane. Dowiedz się więcej o te przydziały w [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).

## <a name="other-limits"></a>Inne ograniczenia.
| **Zasób** | **Limit maksymalny** |
| --- | --- |
| [Równoczesnych zadań](batch-parallel-node-tasks.md) na węzeł obliczeń |4 x liczba rdzeni węzła |
| [Aplikacje](batch-application-packages.md) na konto usługi partia zadań |20 |
| Pakiety aplikacji na aplikację |40 |
| Rozmiar pakietu aplikacji (wszystkie) |Około 195GB<sup>1</sup> |
| Maksymalna początkowy rozmiar zadań | znaki 32768<sup>2</sup> |
| Zadanie maksymalny okres istnienia | 7 dni<sup>3</sup> |

<sup>1</sup> limit bloku maksymalny rozmiar obiektu blob magazynu azure<br />
<sup>2</sup> obejmuje plików zasobów i zmienne środowiskowe<br />
<sup>3</sup> maksymalny okres istnienia zadania, gdy jest ona dodawana do zadania, po jego ukończeniu, wynosi 7 dni. Zadania ukończone utrwalić nieskończoność; dane zadanie nie zostało ukończone w ciągu maksymalny okres istnienia nie jest dostępny.


## <a name="view-batch-quotas"></a>Przydziały partii widoku
Wyświetl przydziałami konta wsadowego w [portalu Azure][portal].

1. Wybierz **partii kont** w portalu, a następnie wybierz konto usługi partia zadań interesuje Cię.
2. Wybierz **przydziały** menu konta usługi partia zadań.
3. Wyświetl przydziały zastosowanym do konta usługi partia zadań
   
    ![Przydziały konta usługi partia zadań][account_quotas]



## <a name="increase-a-quota"></a>Zwiększ limit przydziału
Wykonaj następujące kroki, aby zażądać przydział zwiększyć dla swojego konta usługi partia zadań lub subskrypcją za pomocą [portalu Azure][portal]. Typ zwiększenia limitu przydziału zależy od trybu alokacji puli konta partii zadań.

### <a name="increase-a-batch-cores-quota"></a>Zwiększ limit przydziału rdzeni partii 

1. Wybierz **Pomoc i obsługa techniczna** kafelka na pulpicie nawigacyjnym portalu lub znak zapytania (**?**) w prawym górnym rogu portalu.
2. Wybierz **nowy obsługuje żądania** > **podstawy**.
3. W **podstawy**:
   
    a. **Wystawianie typu** > **przydziału**
   
    b. Wybierz subskrypcję.
   
    c. **Typ limitu przydziału** > **partii**
   
    d. **Plan pomocy technicznej** > **Obsługa przydziałów — włączone**
   
    Kliknij przycisk **Dalej**.
4. W **Problem**:
   
    a. Wybierz **ważność** zgodnie z [wpływ na prowadzoną działalność][support_sev].
   
    b. W **szczegóły**, określ każdego przydziału, aby zmienić nazwę konta wsadowego i nowego limitu.
   
    Kliknij przycisk **Dalej**.
5. W **informacje kontaktowe**:
   
    a. Wybierz **preferowana metoda kontaktu**.
   
    b. Sprawdź i wprowadź wymagane szczegóły dotyczące kontaktu.
   
    Kliknij przycisk **Utwórz**, aby przesłać żądanie pomocy technicznej.

Po przesłaniu żądania obsługi pomocy technicznej platformy Azure skontaktuje się z Tobą. Należy pamiętać, że wykonywania żądania może potrwać maksymalnie 2 dni roboczych.


## <a name="related-topics"></a>Powiązane tematy
* [Tworzenie konta usługi partia zadań Azure za pomocą portalu Azure](batch-account-create-portal.md)
* [Omówienie funkcji usługi partia zadań Azure](batch-api-basics.md)
* [Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.png
