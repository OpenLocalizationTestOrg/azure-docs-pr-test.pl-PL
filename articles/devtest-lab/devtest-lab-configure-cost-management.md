---
title: "aaaView hello miesięczne laboratorium szacowany koszt trendu w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello Azure DevTest Labs miesięczne wykresu trendu szacowany koszt."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Widok hello miesięczne laboratorium szacowany koszt trendu w usłudze Azure DevTest Labs
Funkcja zarządzania koszt Hello DevTest Labs pomaga śledzić hello koszt laboratorium. W tym artykule przedstawiono sposób toouse hello **miesięczny Trend szacowany koszt** tooview wykresu hello bieżącego miesiąca kalendarzowego szacowany koszt do daty i hello szacowany koszt koniec miesiąca hello bieżącego miesiąca kalendarzowego. W tym artykule dowiesz się, jak tooview hello miesięczne wykresu trendu szacowany koszt w hello portalu Azure.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Wyświetlanie hello miesięczny Trend szacowany koszt wykresu
Witaj tooview miesięczny Trend szacowany koszt wykresu, wykonaj następujące kroki: 

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello.   
4. W bloku hello laboratorium, wybierz **koszt ustawienia**.
5. W laboratorium hello **koszt ustawienia** bloku, wybierz opcję **trend koszt laboratorium**.
6. Witaj Poniższy zrzut ekranu przedstawia przykład wykresu kosztów. 
   
    ![Wykres kosztu](./media/devtest-lab-configure-cost-management/graph.png)

Witaj **szacowany koszt** wartość jest hello bieżącego miesiąca kalendarzowego szacowany koszt do daty. Witaj **koszt planowany** hello szacowany koszt hello całego bieżącego miesiąca kalendarzowego oblicza się przy użyciu hello koszt laboratorium dla hello poprzedniej pięć dni.

koszty Hello jest zaokrąglana toohello najbliższej liczby całkowitej. Na przykład: 

* 5.01 Zaokrągla liczbę w górę too6 
* 5.50 Zaokrągla liczbę w górę too6
* 5.99 Zaokrągla liczbę w górę too6

W trakcie jego stany powyżej wykresu hello, hello koszty Zobacz na wykresie hello są *szacowany* koszty przy użyciu [płatność za rzeczywiste użycie](https://azure.microsoft.com/offers/ms-azr-0003p/) oferuje.
Ponadto następujące hello są *nie* objęte hello obliczania kosztów:

* Dostawca usług Kryptograficznych i Dreamspark subskrypcje obecnie nie są obsługiwane jako Azure DevTest Labs używa hello [Azure API rozliczeń](../billing/billing-usage-rate-card-overview.md) laboratorium hello toocalculate koszt, który nie obsługuje dostawcy usług Kryptograficznych lub Dreamspark subskrypcji.
* Twoje stawek oferty. Obecnie nie jesteśmy w stanie toouse Twojego stawek oferty (wyświetlany w obszarze subskrypcji) czy musisz mieć negocjowane z Microsoft lub partnerów. Użyto płatność za rzeczywiste użycie stawki.
* Twoje podatki
* Twoje zniżki
* Waluta. Obecnie koszt laboratorium hello jest wyświetlana tylko w walucie USD.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne
* [Dwa więcej tookeep rzeczy koszt zgodnie z planem w usłudze DevTest Labs](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Dlaczego koszt progi?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Następne kroki
Oto obok niektórych tootry rzeczy:

* [Definiowanie zasad laboratorium](devtest-lab-set-lab-policy.md) — Dowiedz się, jak tooset hello różnych zasad używane toogovern korzystania laboratorium i jego maszyn wirtualnych. 
* [Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) — podczas tworzenia maszyny Wirtualnej, należy określić podstawowy, który może być niestandardowy obraz lub obrazu z witryny Marketplace. W tym artykule przedstawiono sposób toocreate niestandardowego obrazu z pliku VHD.
* [Konfigurowanie portalu Marketplace obrazów](devtest-lab-configure-marketplace-images.md) — DevTest Labs obsługuje tworzenie maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace. W tym artykule przedstawiono sposób toospecify, którego, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium.
* [Utwórz maszynę Wirtualną w laboratorium](devtest-lab-add-vm-with-artifacts.md) -ilustruje sposób toocreate maszyny Wirtualnej z obrazu podstawowego (albo niestandardowe lub Marketplace) i w jaki sposób toowork z artefaktami w maszynie Wirtualnej.

