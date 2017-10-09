---
title: "aaaCreate pierwszej maszyny Wirtualnej w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Twojego pierwszego maszynę wirtualną w laboratorium w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Tworzenie pierwszej maszyny Wirtualnej w laboratorium w usłudze Azure DevTest Labs

Gdy początkowo dostęp DevTest Labs i zechcesz toocreate pierwszej maszyny Wirtualnej, możesz będzie prawdopodobnie to zrobić za pomocą wstępnie załadowane [obrazu z witryny marketplace podstawowej](devtest-lab-configure-marketplace-images.md). Później również będziesz w stanie toochoose z [niestandardowego obrazu oraz formułę](devtest-lab-add-vm.md) podczas tworzenia więcej maszyn wirtualnych. 

Ten samouczek przedstawia przy użyciu hello Azure tooadd portalu pierwszy laboratorium tooa maszyny Wirtualnej w usłudze DevTest Labs.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Kroki tooadd pierwszy laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs
1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
1. Z listy hello labs wybierz laboratorium hello, w której ma zostać hello toocreate maszyny Wirtualnej.  
1. W laboratorium hello **omówienie** bloku, wybierz opcję **+ Dodaj**.  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Na powitania **wybierz podstawowej** bloku, wybierz obraz marketplace hello maszyny Wirtualnej.
1. Na powitania **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej hello w hello **nazwę maszyny wirtualnej** pola tekstowego.

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej hello.  
1. Wprowadź hasło w polu tekstowym hello etykietą **wpisz wartość**.
1. Witaj **typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla hello maszyn wirtualnych w laboratorium hello.
1. Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z hello wstępnie zdefiniowane elementy, które określić hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej.
1. Wybierz **artefakty** — z listy hello artefaktów — wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz.
    **Uwaga:** nowe Labs tooDevTest lub konfigurowanie artefaktów, zobacz toohello [Dodawanie istniejących tooa artefaktu maszyny Wirtualnej](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.
1. Wybierz **Utwórz** tooadd hello określony laboratorium toohello maszyny Wirtualnej.

   Blok laboratorium Hello Wyświetla stan hello tworzenie hello VM - najpierw jako **tworzenie**, następnie jako **systemem** po hello maszyna wirtualna została uruchomiona.

## <a name="next-steps"></a>Następne kroki
* Raz hello maszyna wirtualna została utworzona, można połączyć toohello maszyny Wirtualnej, wybierając **Connect** w bloku hello maszyny Wirtualnej.
* Zapoznaj się z [Dodawanie maszyny Wirtualnej laboratorium tooa](devtest-lab-add-vm.md) na pełniejsze informacje dotyczące dodawania kolejnych maszyn wirtualnych w laboratorium.
* Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
