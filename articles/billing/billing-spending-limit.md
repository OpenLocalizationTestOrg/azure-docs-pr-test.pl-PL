---
title: "limit wydatków Azure aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Opisuje, jak limit wydatków Azure działa i jak tooremove go"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>Zrozumienie Azure limit wydatków i w jaki sposób tooremove go

Limit wydatków na platformie Azure jest ograniczeniem ile może przeznaczyć subskrypcji platformy Azure. Wszystkich nowych klientów, którzy Załóż hello wersja próbna lub oferty, które obejmuje środki na korzystanie z wielu miesiącach ma hello włączona domyślnie limit wydatków. limit wydatków Hello jest $0. Nie można zmienić. limit wydatków Hello nie jest dostępna dla typów subskrypcji, takich jak płatność za rzeczywiste użycie subskrypcji i planów zobowiązań. Zobacz hello [pełną listę oferty Azure i dostępność hello hello limit wydatków](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>Co się stanie, gdy I osiągną hello limit wydatków?

Użycie powoduje opłat, które wyczerpanie zasobów miesięczne hello uwzględnione w ramach Twojej oferty, hello usług, które można wdrożyć są wyłączone dla hello reszty dany miesiąc rozliczeniowy. Na przykład wdrożone usługi Cloud Services zostaną usunięte ze środowiska produkcyjnego, a maszyny wirtualne platformy Azure zostaną zatrzymane i ponownie alokowane. tooprevent usług z wyłączone, możesz wybrać tooremove limitu wydatków. Wyłączenie usług danych hello kont magazynu i bazy danych są dostępne w sposób tylko do odczytu dla administratorów. Początku hello hello następnego miesiąca rozliczeniowego, jeśli ofertę zawiera środków przez wiele miesięcy, subskrypcja będzie ponownie włączyć. Następnie można ponownie wdrożyć usługi w chmurze i kont magazynu tooyour pełny dostęp i baz danych.

Po bezpłatnej subskrypcji próbnej hello osiągnie limit wydatków hello, możesz ponownie włączyć hello subskrypcji i automatycznego [standardowe oferty płatności obejmujące uaktualnienia tooour](billing-upgrade-azure-subscription.md) w ciągu 90 dni.

Chcesz otrzymywać powiadomienia, gdy naciśniesz hello limit wydatków dla danej oferty. Zaloguj się na toohello [Centrum konta platformy Azure](https://account.windowsazure.com), wybierz pozycję **konta**, a następnie wybierz **subskrypcje**. Zobaczysz powiadomienia o subskrypcjach, które osiągnęły hello limit wydatków.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Czynności, które są pobierane dla nawet wtedy, gdy limit wydatków włączone

Niektóre usługi platformy Azure i [zakupy w witrynie Marketplace](https://azure.microsoft.com/marketplace/) może spowodować naliczenie opłat zgodnie z metodą płatności hello (DW), nawet wtedy, gdy ustawiono limit wydatków. Przykłady są licencji programu Visual studio, Azure Active Directory premium plany pomocy technicznej i większości firm marki usług sprzedawane za pośrednictwem hello Marketplace.


## <a name="when-not-toouse-hello-spending-limit"></a>Jeśli nie toouse hello limitu wydatków

limit wydatków Hello może uniemożliwiać wdrażania lub przy użyciu określonych marketplace i usług firmy Microsoft. Poniżej przedstawiono scenariusze hello, gdzie należy usunąć hello limit wydatków w ramach subskrypcji.

- Planujesz toodeploy pierwsze obrazy firmy Oracle i usług, takich jak Visual Studio Team Services. W tym scenariuszu powoduje tooexceed wydatki ograniczyć niemal natychmiast i powoduje, że Twoje toobe subskrypcji wyłączone.

- Masz usługi, których działania nie można przerwać.

- Usługi i zasoby z ustawienia, takie jak adresy IP wirtualnych, które nie mają toolose. Te ustawienia zostaną utracone po cofnięciu przydziału hello usług i zasobów.


## <a name="remove-hello-spending-limit"></a>Usuń limit wydatków hello

Możesz usunąć hello limit w dowolnym momencie wydatków, dopóki jest prawidłową formę płatności skojarzonych z Twoją subskrypcją. W przypadku ofert mających środki przez wiele miesięcy można także ponownie włączyć hello limit wydatków na początku hello następnym cyklu rozliczeniowym.

limit wydatków tooremove, wykonaj następujące kroki:

1. Zaloguj się na toohello [Centrum konta platformy Azure](https://account.windowsazure.com).

2. Wybierz subskrypcję.

3. Jeśli subskrypcja hello jest wyłączona z powodu toohello osiągnięcia limitu wydatków, kliknij to powiadomienie: "Subskrypcja osiągnęła Limit wydatków hello i został wyłączony tooprevent opłat". W przeciwnym razie kliknij przycisk **Usuń limit wydatków** w hello **stan SUBSKRYPCJI** obszaru.

4. Wybierz odpowiednią opcję.

|Opcja|Efekt|
|-------|-----|
|Usuń trwale limit wydatków|Usuwa hello limit wydatków bez włączania go automatycznie na początku hello hello następnym okresie rozliczeniowym.|
|Usuń limit wydatków dla bieżącego okresu rozliczeniowego hello|Usuwa hello limit wydatków, tak aby go włącza ponownie automatycznie na początku hello hello następnym okresie rozliczeniowym.|

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
