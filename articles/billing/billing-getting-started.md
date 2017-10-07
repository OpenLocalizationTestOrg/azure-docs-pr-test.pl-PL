---
title: "aaaPrevent nieoczekiwany kosztów zarządzania rozliczeń - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooavoid nieoczekiwany opłat na rachunku platformy Azure. Przy użyciu funkcji Śledzenie kosztów i zarządzania dla subskrypcji Microsoft Azure."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a>Zapobiegaj nieoczekiwany kosztów zarządzania kosztów i rozliczenia Azure

Podczas tworzenia konta platformy Azure, istnieje kilka sposobów tooget zorientować się z wydatków. W hello [portalu Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), po wybraniu hello subskrypcji, możesz wyświetlić Twojej bieżącej podziału kosztów i ocena wydajności. Możesz również [Pobierz poza faktury i szczegółów plików użycia](billing-download-azure-invoice-daily-usage-date.md). Jeśli chcesz toogroup kosztów zasobów używany do różnych projektów i zespołów przyjrzeć się [znakowanie zasobów](../azure-resource-manager/resource-group-using-tags.md). Jeśli Twoja organizacja ma system raportowania preferowane jest toouse, zapoznaj się hello [rozliczeń interfejsów API](billing-usage-rate-card-overview.md). 

Aby uzyskać więcej informacji na temat dzienne użycie zobacz [zrozumieć rachunku platformy Microsoft Azure](billing-understand-your-bill.md).

Jeśli Twoja subskrypcja jest za pośrednictwem Enterprise Agreement (EA), Cloud Solution Provider (CSP) lub dostęp sponsorowany Azure, wiele funkcji w tym artykule nie stosuj tooyou. Zamiast tego mamy inny zestaw narzędzi używanych do zarządzania kosztów. Zobacz [dodatkowe zasoby dla przedsiębiorstw, dostawca usług Kryptograficznych i dostęp sponsorowany](#other-offers).

Jeśli Twoja subskrypcja jest bezpłatna wersja próbna [programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure Otwórz (AIO) lub BizSpark, następnie Dowiedz się więcej o [limitów wydatków](#spending-limit) tooavoid mających subskrypcję unexpectantly wyłączone. 

## <a name="day-0-before-you-add-azure-services"></a>Od dnia 0: Przed dodaniem usług platformy Azure

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Szacowanie kosztów online przy użyciu kalkulatora cen hello

Zapoznaj się z hello [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/) i [całkowity koszt posiadania kalkulatora](https://aka.ms/azure-tco-calculator) tooget szacowania hello miesięczny koszt usługi hello interesuje Cię. Na przykład A1 systemu Windows maszyny wirtualnej (VM) jest szacowany toocost $66.96 USD miesięcznie w obliczeniowe godziny, jeśli pole pozostanie uruchomione przez cały czas hello:

![Zrzut ekranu przedstawiający hello Kalkulator cen wskazująca, że maszyna wirtualna A1 systemu Windows jest szacowany toocost $66.96 USD miesięcznie](./media/billing-getting-started/pricing-calcVM.png)

Aby uzyskać więcej informacji, zobacz [cennik — często zadawane pytania](https://azure.microsoft.com/pricing/faq/). Lub jeśli chcesz, aby osoba tooa tootalk, wywołania 1-800-867-1389.

### <a name="check-your-subscription-and-access"></a>Sprawdź subskrypcję i dostępu

Koszty wyświetlania wymagają [informacji toobilling dostęp na poziomie subskrypcji](billing-manage-access.md), ale tylko Witaj, Administratorze konto ma dostęp do hello [Centrum konta](https://account.windowsazure.com/Home/Index), zmienić informacje rozliczeniowe i zarządzać subskrypcjami. Witaj, Administratorze konta jest hello osoba nawiązaniem hello procesu tworzenia konta. Aby uzyskać więcej informacji, zobacz [Dodawanie lub zmienianie role administratora platformy Azure, zarządzających hello subskrypcji lub usługi](billing-add-change-azure-subscription-administrator.md).

toosee, jeśli jest hello konta administratora, przejdź toohello [bloku subskrypcji w portalu Azure hello](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) i przyjrzyj się hello listy subskrypcji, musisz mieć dostęp do. Sprawdź w obszarze **Moje roli**. Informacja *administrator konta*, a następnie jest ok. Informacja czegoś innego, takich jak *właściciela*, a następnie masz pełne uprawnienia.

![Zrzut ekranu przedstawiający roli użytkownika w hello Widok subskrypcji w hello portalu Azure](./media/billing-getting-started/sub-blade-view.PNG)

Jeśli nie jest hello konta administratora, a następnie ktoś prawdopodobnie udostępniła Ci częściowy dostęp za pośrednictwem [kontroli dostępu opartej na roli Azure Active Directory](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage subskrypcji i rozliczeń info, zmień [znaleźć Witaj, Administratorze konta](billing-subscription-transfer.md#whoisaa) i poproś o tooperform hello zadania lub [transferu hello subskrypcji tooyou](billing-subscription-transfer.md).

Jeśli administrator konta nie jest już w swojej organizacji i należy rozliczeń toomanage [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 

### <a name="spending-limit"></a>Sprawdź, czy istnieje limit wydatków

Jeśli masz subskrypcję, która używa środków następnie hello limit wydatków jest dla Ciebie domyślnie włączona. Dzięki temu, gdy spędzają z środków karty kredytowej nie zostały naliczone opłaty. Zobacz hello [pełną listę oferty Azure i dostępność hello limit wydatków](https://azure.microsoft.com/support/legal/offer-details/).

Jednak jeśli osiągnęła limit wydatków, usługi wyłączone. Oznacza to, że maszyny wirtualne są alokację. tooavoid przestojów, należy wyłączyć funkcję hello limit wydatków. Wszelkie nadwyżkowe pobiera obciążony na Twojej karty kredytowej. 

toosee Jeśli możesz już został limit wydatków, przejdź toohello [wyświetlić subskrypcje w Centrum konta hello](https://account.windowsazure.com/Subscriptions). Transparent pojawia się, gdy limit wydatków znajduje się na:

![Zrzut ekranu pokazujący ostrzeżenie dotyczące wydatków jest limit na powitania Centrum konta](./media/billing-getting-started/spending-limit-banner.PNG)

Kliknij transparent hello i postępuj zgodnie z monitami tooremove hello limit wydatków. Jeśli po utworzeniu konta nie wprowadzono karty kredytowej, musi wprowadzić hello tooremove limit wydatków. Aby uzyskać więcej informacji, zobacz [limit wydatków Azure — jak działa i jak tooenable lub usuń go](https://azure.microsoft.com/pricing/spending-limits/).

### <a name="set-up-billing-alerts"></a>Ustawianie alertów dotyczących rozliczeń

Skonfiguruj alerty dotyczące rozliczeń wiadomości e-mail tooget koszty użycia przekracza ilość, którą określisz. Jeśli masz miesięczne Ustawianie alertów dla używania zapasowej określonej wartości. Aby uzyskać więcej informacji, zobacz [skonfigurować alerty dotyczące subskrypcji platformy Microsoft Azure billing](billing-set-up-alerts.md).

![Zrzut ekranu przedstawiający rozliczeń e-mail alertów](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Ta funkcja jest dostępny w wersji zapoznawczej, dlatego należy sprawdzić użycie regularnie.

Możesz szacowania kosztów hello toouse z hello Kalkulator cen przyjąć pierwszy alertu.

### <a name="understand-limits-and-quotas-for-your-subscription"></a>Ograniczenia i limity przydziału dla subskrypcji

Brak domyślne limity subskrypcji tooeach dla elementów, jak hello liczba rdzeni Procesora i adresów IP. Można w trosce o tych ograniczeń. Aby uzyskać więcej informacji, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md). Można zażądać zwiększenia limitu tooyour lub limitu przydziału przez [kontaktu z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="day-1-as-you-add-services"></a>Dzień 1: Jak dodać usługi

### <a name="review-hello-estimated-cost-in-hello-portal"></a>Przejrzyj hello szacowany koszt w portalu hello

Zwykle po dodaniu usługi w portalu Azure hello istnieje widok pokazujący podobne szacowany koszt miesięcznie. Na przykład po wybraniu rozmiar maszyny Wirtualnej systemu Windows hello widać hello szacowane miesięczny koszt dla godziny obliczeń dla hello:

![Przykład: maszyna wirtualna A1 systemu Windows jest szacowany toocost $66.96 USD miesięcznie](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a>Dodaj znaczniki tooyour zasobów toogroup dane rozliczeń

Można użyć danych dotyczących rozliczeń toogroup tagi obsługiwanych usług. Na przykład po uruchomieniu wielu maszyn wirtualnych dla różnych zespołów można tagi toocategorize koszty przez Centrum kosztów (HR marketingu finance) lub środowiska (środowiska produkcyjnego, produkcji wstępnej, test). 

![Zrzut ekranu pokazujący konfigurowania tagów w portalu hello](./media/billing-getting-started/tags.PNG)

tagi Hello są wyświetlane w różnych koszt raportowania widoków. Na przykład, są one widoczne w Twojej [koszt analitycznego](#costs) od razu i [szczegółów CSV użycia](#invoice-and-usage) po Twojego pierwszego okresu rozliczeniowego.

Aby uzyskać więcej informacji, zobacz [używanie tagów tooorganize zasobów platformy Azure](../azure-resource-manager/resource-group-using-tags.md).

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Rozważ włączenie funkcji wycinania kosztów, takich jak automatyczne zamykanie dla maszyn wirtualnych

W zależności od scenariusza można skonfigurować automatyczne zamykanie dla maszyn wirtualnych w hello portalu Azure. Aby uzyskać więcej informacji, zobacz [automatyczne zamykanie dla maszyn wirtualnych przy użyciu usługi Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Zrzut ekranu opcji automatycznego zamknięcia w portalu hello](./media/billing-getting-started/auto-shutdown.PNG)

Automatyczne zamykanie nie jest hello taka sama, jak podczas zamykania w hello maszyny Wirtualnej z apletu Opcje zasilania. Automatyczne zamykanie zatrzymuje i zwalnia toostop sieci maszyn wirtualnych użycie dodatkowych opłat. Aby uzyskać więcej informacji, zobacz często zadawane pytania dotyczące cen [maszyn wirtualnych systemu Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) i [maszyn wirtualnych systemu Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) o stanach maszyny Wirtualnej.

Więcej funkcji wycinania koszt dla Twojego środowiska projektowania i testowania, zapoznaj się z [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

## <a name="cost-reporting"></a>Dzień 2 +: Po zakończeniu korzystania z usługi, Wyświetl użycie

### <a name="costs"></a>Regularnie Sprawdź hello portalu do podziału kosztów i ocena

Po uzyskaniu usługi uruchomione regularnie sprawdzać, ile ich jest wyceny należy. Widać bieżącego hello wydatków i ocena wydajności w portalu Azure. 

1. Odwiedź hello [bloku subskrypcji w portalu Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

2. Wybierz subskrypcję ma toosee. Może mieć tylko jeden tooselect.

3. Powinni widzieć hello podziału kosztów i ocena wydajności w bloku podręcznego hello. Nie może być obsługiwana dla danej oferty (ostrzeżenie będzie wyświetlana u góry hello). Poczekaj 24 godziny po dodaniu usługi dla hello toopopulate danych.
    
    ![Zrzut ekranu przedstawiający ocena i podział w hello portalu Azure](./media/billing-getting-started/burn-rate.PNG)

4. Możesz toopin hello widoku tooyour w pulpicie nawigacyjnym.

    ![Zrzut ekranu przedstawiający przypinanie toohello widoku pulpitu nawigacyjnego](./media/billing-getting-started/pin.PNG)

5. Kliknij przycisk **analizy kosztów** w hello listy toohello toosee po lewej stronie powitania podziału kosztów przez zasób.

    ![Zrzut ekranu przedstawiający widok analizy kosztów hello w portalu Azure](./media/billing-getting-started/cost-analysis.PNG)

6. Można filtrować według różnych właściwości, takie jak [tagi](#tags), grupy zasobów i przedziału czasu. Kliknij przycisk **Zastosuj** tooconfirm hello filtry i **Pobierz** tooexport hello widoku tooa Comma-Separated wartości (.csv) pliku.

7. Kliknij zasób toosee spędzają na historię i ile on został wyceny możesz każdego dnia.

    ![Zrzut ekranu przedstawiający hello spędzają widoku historii w portalu Azure](./media/billing-getting-started/costhistory.PNG)

Firma Microsoft zaleca sprawdzenie koszty hello Zobacz szacunkowe hello, który został wyświetlony po wybraniu hello usług. Jeśli koszty hello bardzo różnią się od szacuje, sprawdź hello planu cenowego (vs A1 maszyna wirtualna A0, na przykład) wybranego dla zasobów. 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a>Wyświetlanie kosztów dla Twojej subskrypcji w bloku rozliczenia hello

Jeśli zarządzasz wieloma subskrypcjami jako hello administratora konta, możesz wyświetlać hello agregacji naliczona kwota i podział dla Twojej subskrypcji w hello [bloku rozliczenia](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade). 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Włącz i zapoznaj się z zalecenia usługi Advisor Azure

[Klasyfikator Azure](../advisor/advisor-overview.md) jest funkcja w wersji zapoznawczej, która ułatwia obniżenie kosztów, określając z niskim użycia zasobów. Włącz ją w hello portalu Azure:

![Przycisk Advisor zrzut ekranu Azure w portalu Azure](./media/billing-getting-started/advisor-button.PNG)

Następnie, aby pobrać praktyczne zalecenia hello **koszt** kartę na pulpicie nawigacyjnym usługi Advisor hello:

![Przykład zalecenie koszt zrzut ekranu Advisor](./media/billing-getting-started/advisor-action.PNG)

Aby uzyskać więcej informacji, zobacz [zalecenia usługi Advisor koszt](../advisor/advisor-cost-recommendations.md).

### <a name="invoice-and-usage"></a>Pobierz użycie faktury i szczegóły po Twojego pierwszego okresu rozliczeniowego

Po pierwszym okresie rozliczeniowym możesz pobrać faktury Portable Document Format (PDF), a szczegóły użycia wartości Comma-Separated (CSV). Można również włączyć toohave faktura pocztą e-mail tooyou. Te pliki pomocy toounderstand co to jest ostatecznie rachunku tooyou po podatków, rabatów i środków. Jeśli nie ma subskrypcji tooyour dołączony metody płatności, te pliki mogą być niedostępne dla Ciebie. Aby uzyskać więcej informacji, zobacz [jak tooget Azure rozliczeniowego faktury i dziennego użycia danych](billing-download-azure-invoice-daily-usage-date.md) i [zrozumieć rachunku platformy Microsoft Azure](billing-understand-your-bill.md).

![Zrzut ekranu przedstawiający faktury PDF](./media/billing-getting-started/invoice.png)

Hello tagi, które można ustawić wcześniej widoczne w plikach CSV użycia szczegółów hello:

![Zrzut ekranu pokazujący tagów w hello użycia CSV](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a>Interfejs API rozliczeń

Użyj danych użycia rozliczeń get tooprogrammatically interfejsu API. Użyj hello RateCard interfejsu API i tooget razem użycia interfejsu API hello rachunku użycie. Aby uzyskać więcej informacji, zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a>Dodatkowe zasoby dla przedsiębiorstw, dostawca usług Kryptograficznych i dostęp sponsorowany

Zwróć tooyour Menedżera kont lub partnera Azure tooget uruchomiona.

| Oferta | Zasoby |
|-------------------------------|-----------------------------------------------------------------------------------|
| Umowa Enterprise Agreement (EA) | [EA portal](https://ea.azure.com/), [pomocy docs](https://ea.azure.com/helpdocs), i [raportu usługi Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Cloud Solution Provider (CSP) | Skontaktuj się dostawcą tooyour |
| Sponsorowanie systemu Azure | [Dostęp sponsorowany portalu](https://www.microsoftazuresponsorships.com/) |

Jeśli zarządzasz IT dla dużych organizacji zalecamy odczytu [szkieletu Azure enterprise](../azure-resource-manager/resource-manager-subscription-governance.md) i hello [organizacji IT oficjalny dokument](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (do pobrania PDF, tylko w języku angielskim).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Kontakt z pomocą techniczną

Jeśli potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
