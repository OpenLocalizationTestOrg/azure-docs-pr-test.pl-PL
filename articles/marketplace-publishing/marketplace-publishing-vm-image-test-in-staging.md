---
title: "aaaTest oferują maszyny Wirtualnej na powitania Marketplace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest, obraz maszyny Wirtualnej, dla hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Testowanie ofertę maszyny Wirtualnej dla hello Azure Marketplace tymczasowych
Sposób wdrażania programu jednostki SKU w prywatnej "piaskownicy", gdzie testowania i zweryfikować jego działanie przed jego wdrożeniem toohello Marketplace przemieszczania. Witaj SKU pojawia się w przemieszczania analogiczny, jak tooa klienta, który został wdrożony go. Obraz maszyny Wirtualnej musi być toostaging certyfikowanych toobe naciśnięty.

## <a name="step-1-push-your-offer-toostaging"></a>Krok 1: Push toostaging Twojej oferty
1. Na powitania **publikowania** , kliknij pozycję **Push tooStaging**.
   
    ![Rysowanie](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Jeśli Portal publikowania hello powiadamia o błędy, należy je poprawić.
3. W hello **kto ma dostęp do Twojej oferty przemieszczanego?** okna dialogowego wprowadź hello Lista subskrypcji platformy Azure, który będzie używany toopreview ofertę w hello [portalu Azure w wersji zapoznawczej](https://portal.azure.com).
   
   > [!NOTE]
   > W przypadku maszyn wirtualnych i szablonów rozwiązania należy **nie** dozwolonych subskrypcje typu Dostawca usług Kryptograficznych, DreamSpark lub Azure otwartym.
   > 
   > 

    > W przypadku maszyn wirtualnych, po kliknięciu przycisku hello **tooSTAGING WYPYCHANIA**, hello następujące kroki są wykonywane za hello sceny. Będziesz w stanie tooview postęp hello każdego kroku karcie publikowania hello w hello publikowania portalu. Należy sprawdzić tej strony w regularnych odstępach czasu (do czasu hello stan pokazuje przejściowa) Aby uzyskać informacje o błędzie, który konieczne korekty użytkownika końcowego.

    > - Na początku przemieszczania żądanie przejdzie do zespołu certyfikacji toohello, który zweryfikować hello wirtualnego dysku twardego. Jednak jeśli — Otrzymano żądanie tylko marketingu zmiany, następnie hello certyfikacji krok zostanie pominięty.
    > - Po zakończeniu certyfikacji hello replikacji rozpoczęcia oferty hello we wszystkich hello centrach danych platformy Azure. Zazwyczaj zajmuje 24-48hours dla toocomplete replikacji hello ale może potrwać tooa tygodnia, w zależności od rozmiaru hello hello wirtualnego dysku twardego. Jeśli jednak — Otrzymano żądanie tylko marketingu zmiany, następnie replikacji hello jest szybsze.
    > - Po ukończeniu replikacji hello jest to oferta hello będą dostępne w hello [portalu Azure](http:/portal.azure.com). W tym hello czas stanu stają się UMIESZCZONE w hello publikowania portalu. Przemieszczanego oferta nie jest widoczna hello [portalu Azure](http:/portal.azure.com) wyłącznie przy użyciu nazwy e-mail hello skojarzone z subskrypcją hello, z których hello są przygotowywane oferty.

1. Zaloguj się toohello [portalu Azure w wersji zapoznawczej](https://portal.azure.com) przy użyciu jednej z hello subskrypcji platformy Azure na liście hello w poprzednim kroku.
2. Znajdź Twoją ofertę i zweryfikować punkty obrazu maszyny Wirtualnej:
   
   * Upewnij się, że marketingu zawartości jest wyświetlane poprawnie w hello Marketplace.
   * Wdrażanie na trasie hello obrazu maszyny Wirtualnej.
     
      ![img mapy portalu](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Ofertę pozostanie w przejściowym dopóki bezzwłocznego powiadamiania firmy Microsoft za pośrednictwem hello Portal publikowania [**publikowania** kartę > kliknij przycisk hello **"TooProduction tooPush zatwierdzenie żądania"**] czy toopush gotowe tooproduction. Jest to toohave idealne czas, sprawdź wszyscy członkowie zespołu nad wszystko w ramach przygotowania do Twojej oferty, przechodząc do listy.
> 
> Hello przemieszczania platformy jest przeznaczony do testowania oferta hello w trybie podglądu przez wydawcę hello. Zdecydowanie zniechęcić się przy użyciu tego platofrm do celów dostępnych w handlu.
> 
> 

## <a name="next-steps"></a>Następne kroki
Ofertę jest "przemieszczony", a zostały przetestowane jego funkcjonalność i marketingu zawartości, możesz przejść publikowanie końcowego toohello fazy **krok 4**: [wdrażanie toohello Twojego oferta portalu Marketplace](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md)

