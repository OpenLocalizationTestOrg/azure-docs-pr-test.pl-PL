---
title: "ustawienia obrazu portalu Azure Marketplace aaaConfigure w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Konfigurowanie obrazów Azure Marketplace, których można użyć w przypadku tworzenia maszyny Wirtualnej w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Skonfiguruj ustawienia obrazu portalu Azure Marketplace w usłudze Azure DevTest Labs
DevTest Labs obsługuje tworzenia maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace w zależności od sposobu konfiguracji portalu Azure Marketplace toobe obrazy używane w laboratorium. W tym artykule opisano sposób toospecify, którego, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium. Dzięki temu, że zespół ma tylko dostępu toohello Marketplace obrazów, które są im potrzebne. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Wybierz obrazy portalu Azure Marketplace, które są dozwolone podczas tworzenia maszyny Wirtualnej
1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello. 
4. W bloku hello laboratorium, wybierz **konfiguracji i zasadach**.
5. W laboratorium w **konfiguracji i zasadach** bloku w obszarze **baz maszyn wirtualnych**, wybierz pozycję **obrazów Marketplace**.
6. Określ, czy się, że wszystkie hello kwalifikowaną toobe obrazów Azure Marketplace dostępne do użycia jako baza dla nowej maszyny Wirtualnej. W przypadku wybrania **tak**, następnie wszystkie obrazy portalu Azure Marketplace hello spełniające wszystkie hello następujące kryteria są dozwolone w laboratorium hello:
   
   * Obraz powitania tworzy jednej maszyny Wirtualnej, **i**
   * Obraz powitania używa usługi Azure Resource Manager tooprovision maszyn wirtualnych, **i**
   * Obraz powitania nie wymaga zakup planu licencjonowania bardzo
     
    Jeśli nie toobe obrazów dozwolone, lub ma toospecify obrazów, które mogą być używane, wybierz **nr**.
     
     ![Opcja tooallow wszystkie toobe obrazów w witrynie Marketplace używany jako obrazy podstawowe dla maszyn wirtualnych](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. W przypadku wybrania **nr** toohello poprzedniego kroku, hello **dozwolone obrazów/wybierz wszystkie** pole wyboru jest włączone. 
   Możesz użyć tej opcji wraz z wybierz tooquickly pole wyszukiwania hello lub usuń zaznaczenie wszystkich elementów hello wyświetlane na liście hello.
   * Wybierz hello Azure Marketplace obrazy tooallow dla tworzenia maszyny Wirtualnej pojedynczo, zaznaczając wyboru odpowiednich każdego obrazu.
   * Wybierz nic z listy hello, jeśli nie chcesz tooallow żadnych portalu Azure Marketplace toobe obrazy używane w laboratorium hello.
   
    ![Można określić, które obrazy portalu Azure Marketplace może służyć jako podstawowy obrazów maszyn wirtualnych](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu, jak obrazy portalu Azure Marketplace są dozwolone podczas tworzenia maszyny Wirtualnej, następnym krokiem hello jest zbyt[Dodawanie maszyny Wirtualnej laboratorium tooyour](devtest-lab-add-vm-with-artifacts.md).

