---
title: "aaaAdd claimable laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd laboratorium tooa claimable maszyny wirtualnej w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Dodaj claimable laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs
Dodaj claimable laboratorium tooa maszyny Wirtualnej w podobny sposób toohow można [dodać maszyny Wirtualnej standardowego](devtest-lab-add-vm.md) — z *podstawowej* czyli albo [niestandardowego obrazu](devtest-lab-create-template.md), [formuła](devtest-lab-manage-formulas.md), lub [obrazu z witryny Marketplace](devtest-lab-configure-marketplace-images.md). W tym samouczku przedstawiono przy użyciu hello Azure tooadd portalu claimable laboratorium tooa maszyny Wirtualnej w usłudze DevTest Labs i przedstawia proces hello użytkownik wykonuje hello tooclaim maszyny Wirtualnej.

> [!NOTE]
> W przypadku wdrożenia maszyn wirtualnych laboratorium za pośrednictwem [szablonów usługi Azure Resource Manager](devtest-lab-create-environment-from-arm.md), claimable maszyn wirtualnych można utworzyć Ustawianie hello **allowClaim** tootrue właściwości w sekcji właściwości hello.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Kroki tooadd claimable laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs
1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
1. Z listy hello labs, wybierz hello laboratorium, w której chcesz toocreate hello claimable maszyny Wirtualnej.  
1. W laboratorium hello **omówienie** bloku, wybierz opcję **+ Dodaj**.  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Na powitania **wybierz podstawowej** bloku, wybierz podstawa hello maszyny Wirtualnej.
1. Na powitania **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej hello w hello **nazwę maszyny wirtualnej** pola tekstowego.

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej hello.  
1. Jeśli chcesz, aby toouse hasła przechowywane w Twojej [tajny magazynu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), wybierz pozycję **używać hasła zapisane**i określ wartości klucza, który odpowiada tooyour hasło. W przeciwnym razie wprowadź hasło w polu tekstowym hello etykietą **wpisz wartość**.
1. Witaj **typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla hello maszyn wirtualnych w laboratorium hello.
1. Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z hello wstępnie zdefiniowane elementy, które określić hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej.
1. Wybierz **artefakty** i z listy hello artefaktów, wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz. Nowe Labs tooDevTest lub konfigurowanie artefaktów, zobacz toohello [Dodawanie istniejących tooa artefaktu maszyny Wirtualnej](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.
1. Wybierz **Zaawansowane ustawienia** opcje i wygaśnięcia opcje sieciowe tooconfigure hello maszyny Wirtualnej. W obszarze **oświadczeń opcje**, wybierz **tak** toomake hello maszyny claimable.

  ![Wybierz hello toomake claimable maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Tooview lub skopiuj hello szablonu usługi Azure Resource Manager, zobacz toohello [szablonu Zapisz Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) , a następnie wróć tutaj po zakończeniu.
1. Wybierz **Utwórz** tooadd hello określony laboratorium toohello maszyny Wirtualnej.
1. Blok laboratorium Hello Wyświetla stan hello tworzenie hello VM - najpierw jako **tworzenie**, następnie jako **systemem** po hello maszyna wirtualna została uruchomiona.


## <a name="using-a-claimable-vm"></a>Przy użyciu claimable maszyny Wirtualnej

Użytkownika można oświadczeń żadnej maszyny Wirtualnej z listy "Claimable maszyny wirtualne" hello, wykonując jedną z następujących czynności:

* Z listy hello "Claimable maszyny wirtualne" u dołu bloku omówienie laboratorium hello hello, kliknij prawym przyciskiem myszy na jednym z hello maszyn wirtualnych na liście hello i wybierz polecenie **maszyny oświadczeń**.

 ![Żądanie claimable określonej maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* U góry hello hello **omówienie** bloku, wybierz **uzyskania**. Losowe maszyny wirtualnej jest przypisane z listy hello claimable maszyn wirtualnych.

 ![Żądanie żadnej claimable maszyny Wirtualnej.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Po użytkownika oświadczeń maszyny Wirtualnej, przenieść w górę do listy "Moje maszyny wirtualne" i nie jest już claimable przez innego użytkownika.

## <a name="next-steps"></a>Następne kroki
* Raz hello maszyna wirtualna została utworzona, można połączyć toohello maszyny Wirtualnej, wybierając **Connect** w bloku hello maszyny Wirtualnej.
* Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
