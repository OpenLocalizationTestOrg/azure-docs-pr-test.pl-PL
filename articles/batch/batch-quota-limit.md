---
title: "aaaService przydziały i limity partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przydziałów domyślnych partii zadań Azure, limity i ograniczenia i jak zwiększenie przydziału toorequest"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Limity przydziału i limity usługi Batch

Jako z innymi usługami Azure, limity na istnieją pewne zasoby skojarzone z hello usługa partia zadań. Wiele z tych limitów jest przydziałów domyślnych zastosowane przez platformę Azure w subskrypcji hello lub na poziomie konta. W tym artykule omówiono te ustawienia domyślne, i jak mogą żądać przydziału zwiększa.

Pamiętaj o tych limitach przydziału podczas projektowania i skalowania obciążeń usługi Batch. Na przykład jeśli pulę nie jest osiągnięciu hello docelowej liczby węzłów obliczeniowych, określonych przez Ciebie, może osiągnięto limit przydziału rdzeni hello konta partii zadań lub regionalnych przydziału rdzeni maszyn wirtualnych dla Twojej subskrypcji.

Można uruchomić wiele obciążeń partii w jednym konta usługi partia zadań lub dystrybucji obciążeń między kontami partii zadań, które znajdują się w hello tej samej subskrypcji, ale w różnych regionach platformy Azure.

Jeśli planujesz toorun obciążeń produkcyjnych w partii, konieczne może tooincrease co najmniej jednego przydziały hello powyżej hello domyślne. Jeśli chcesz tooraise limit przydziału, możesz otworzyć online [żądania obsługi klienta](#increase-a-quota) bez dodatkowych opłat.

> [!NOTE]
> Limit przydziału jest limit kredytu nie gwarancji pojemności. Jeśli wymagana pojemność na dużą skalę, skontaktuj się z pomocą techniczną platformy Azure.
> 
> 

## <a name="resource-quotas"></a>Limity przydziałów zasobów
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Przydziały w trybie użytkownika subskrypcji

Dla konta wsadowego z trybem przydziału puli ustawić także**subskrypcji użytkownika**, partii maszyny wirtualne i inne zasoby, takie jak kont magazynu, są tworzone bezpośrednio w ramach Twojej subskrypcji po utworzeniu puli. limit przydziału rdzeni partii zadań Azure Hello tooan konto utworzone w tym trybie nie ma zastosowania. Zamiast tego są stosowane przydziały hello w subskrypcji dla rdzeni regionalnych obliczeniowych i innych zasobów. Dowiedz się więcej o te przydziały w [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).

Podczas planowania użycia zasobów dla konto utworzone w trybie użytkownika subskrypcji, hello Uwaga po partii zasobów (Dodawanie toocompute rdzenie) są wymagane dla każdego 40 maszyn wirtualnych systemu Linux lub 20 maszyn wirtualnych systemu Windows:

| Zasób | Przydział | Dostawca |
| --- | ---| --- |
| Jedno konto magazynu | Konta magazynu | Microsoft.Storage |
| Jeden publiczny adres IP | Publiczne adresy IP | Microsoft.Network | 
| Jedną sieć wirtualną | Sieci wirtualne | Microsoft.Network | 
| Grupy zabezpieczeń sieci | Grupy zabezpieczeń sieci | Microsoft.Network | 
| Jeden zestaw skali maszyny wirtualnej | Zestawy skali maszyn wirtualnych | Microsoft.Compute | 
| Jedna usługa równoważenia obciążenia | Moduły równoważenia obciążenia | Microsoft.Network | 

Hello rdzeni przydziału na poziomie regionalnym lub na rodzinę maszyny Wirtualnej powinny być zestaw zgodnie z toohello rozmiar maszyny Wirtualnej wymagana dla puli partii lub pul:

| Przydział | Dostawca |
| --- | ---- |
| Całkowita liczba rdzeni regionalne | Microsoft.Compute |
| … Rodziny rdzeni | Microsoft.Compute |



## <a name="other-limits"></a>Inne ograniczenia.
| **Zasób** | **Limit maksymalny** |
| --- | --- |
| [Równoczesnych zadań](batch-parallel-node-tasks.md) na węzeł obliczeń |4 x liczba rdzeni węzła |
| [Aplikacje](batch-application-packages.md) na konto usługi partia zadań |20 |
| Pakiety aplikacji na aplikację |40 |
| Rozmiar pakietu aplikacji (wszystkie) |Około 195GB<sup>1</sup> |
| Maksymalna początkowy rozmiar zadań | znaki 32768<sup>2</sup> |

<sup>1</sup> limit bloku maksymalny rozmiar obiektu blob magazynu azure<br />
<sup>2</sup> obejmuje plików zasobów i zmienne środowiskowe

## <a name="view-batch-quotas"></a>Przydziały partii widoku
Wyświetl przydziałami konta wsadowego w hello [portalu Azure][portal].

1. Wybierz **partii kont** w portalu hello, a następnie wybierz konto usługi partia zadań hello interesuje Cię.
2. Wybierz **właściwości** na konto usługi partia zadań hello menu bloku.
3. bloku właściwości Hello Wyświetla hello **przydziały** obecnie stosowane toohello konta usługi partia zadań
   
    ![Przydziały konta usługi partia zadań][account_quotas]

Dla konta wsadowego, utworzony w trybie użytkownika subskrypcji hello widoku powiązanych przydziały subskrypcji w hello portalu Azure.

1. Wybierz **subskrypcje**i wybierz subskrypcję hello używasz hello konta usługi partia zadań.

2. Na powitania **subskrypcji** bloku, wybierz opcję **użycia + przydziały**.



## <a name="increase-a-quota"></a>Zwiększ limit przydziału
Wykonaj te kroki toorequest, zwiększ limit przydziału dla konta partii zadań lub subskrypcję za pomocą hello [portalu Azure][portal]. Typ Hello zwiększenia limitu przydziału zależy od trybu alokacji puli hello konta partii zadań.

### <a name="increase-a-batch-cores-quota"></a>Zwiększ limit przydziału rdzeni partii 

Jeśli Twoje konto usługi partia zadań została utworzona w **partii usługi** tryb, wykonaj te kroki toorequest zwiększenia limitu przydziału rdzeni partii:

1. Wybierz hello **Pomoc i obsługa techniczna** kafelka na pulpicie nawigacyjnym portalu lub hello znak zapytania (**?**) w hello prawym górnym rogu portalu hello.
2. Wybierz **nowy obsługuje żądania** > **podstawy**.
3. Na powitania **podstawy** bloku:
   
    a. **Wystawianie typu** > **przydziału**
   
    b. Wybierz subskrypcję.
   
    c. **Typ limitu przydziału** > **partii**
   
    d. **Plan pomocy technicznej** > **Obsługa przydziałów — włączone**
   
    Kliknij przycisk **Dalej**.
4. Na powitania **Problem** bloku:
   
    a. Wybierz **ważność** zgodnie z tooyour [wpływ na prowadzoną działalność][support_sev].
   
    b. W **szczegóły**, określ każdy przydział ma toochange, nazwa konta wsadowego hello i hello nowego limitu.
   
    Kliknij przycisk **Dalej**.
5. Na powitania **informacje kontaktowe** bloku:
   
    a. Wybierz **preferowana metoda kontaktu**.
   
    b. Sprawdź, a następnie wprowadź szczegóły dotyczące kontaktu hello wymagane.
   
    Kliknij przycisk **Utwórz** toosubmit hello obsługi żądania.

Po przesłaniu żądania obsługi pomocy technicznej platformy Azure skontaktuje się z Tobą. Pamiętaj, że Kończenie żądania hello może potrwać too2 dni roboczych.

### <a name="increase-a-subscription-cores-quota"></a>Zwiększ limit przydziału rdzeni subskrypcji

Jeśli Twoje konto usługi partia zadań została utworzona w **subskrypcji użytkownika** tryb i potrzebujesz dodatkowych regionalnych lub wirtualna rodziny rdzeni żądania, a limit przydziału Zwiększ w ramach subskrypcji. Aby uzyskać instrukcje, zobacz [żądań Zwiększ limit przydziału rdzeni Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>Powiązane tematy
* [Tworzenie konta usługi partia zadań Azure za pomocą portalu Azure hello](batch-account-create-portal.md)
* [Omówienie funkcji usługi partia zadań Azure](batch-api-basics.md)
* [Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
