---
title: "Testowanie ofertę szablon rozwiązania dla witryny Marketplace | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak przetestować ofertę szablon rozwiązania dla portalu Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a>Testowanie ofertę szablon rozwiązania tymczasowych
Przemieszczania oznacza wdrażanie ofertę w prywatnej "piaskownicy", gdzie należy przetestować i sprawdzić jego działanie przed wypchnięciem go do produkcji. Oferta jest wyświetlany w przemieszczania analogiczny, jak na rzecz klienta, który został wdrożony go. Aby zostać przeniesiony do przemieszczania muszą być certyfikowane ofertę.

Po przemieszczeniu oferty można wyświetlać i przetestować oferty w [Azure Portal](https://portal.azure.com/).

Wykonaj poniższe kroki, aby push Twojej oferty przemieszczania i przetestować go w [Azure Portal](https://portal.azure.com/):

1. Przejdź do [Portal publikowania](https://publish.windowsazure.com) > **szablony rozwiązań** kartę > ofertę > **publikowania** > **wypychania do przemieszczania**.
2. Podaj listę subskrypcji platformy Azure, które będą używane do przetestowania ofertę.
3. Zaloguj się do portalu Azure w wersji zapoznawczej przy użyciu Identyfikatora subskrypcji, który został użyty w poprzednim kroku.
4. Wykonuje round co najmniej jedną testowania w portalu Azure w wersji zapoznawczej w punktach wymienionych poniżej:
   * Upewnij się, że marketingu zawartość zostaną wyświetlone poprawnie w portalu Azure Marketplace.
   * Wdrażanie na trasie topologii.
   * Wykonaj test wydajności, a testy obciążenia.
   * Upewnij się, że topologii opiera się na najlepsze rozwiązania.

## <a name="next-steps"></a>Następne kroki
Jeśli są zadowalające wyniki, a następnie można przejść do fazy publikowania końcowego oferta **krok 4**: [wdrażanie Twojej oferty w portalu Marketplace](marketplace-publishing-push-to-production.md). W przeciwnym razie zmiany w ramach Twojej oferty, a żądanie certyfikacji ponownie.

> [!NOTE]
> Marketing zmian zawartości certyfikacji nie jest wymagane.
> 
> 

Zobacz [wprowadzenie: jak publikowanie oferty w portalu Azure Marketplace](marketplace-publishing-getting-started.md) przewodnik dotyczący wszystkie zadania wydawcy.

