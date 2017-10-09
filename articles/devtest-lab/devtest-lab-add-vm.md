---
title: "aaaAdd laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd laboratorium tooa maszyny wirtualnej w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Dodawanie laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs
Jeśli masz już [pierwszej maszyny Wirtualnej utworzone](devtest-lab-create-first-vm.md), prawdopodobnie zostało to z wstępnie załadowane [obrazu z witryny marketplace](devtest-lab-configure-marketplace-images.md). Teraz, jeśli chcesz tooadd kolejnych maszyn wirtualnych tooyour laboratorium można także *podstawowej* czyli albo [niestandardowego obrazu](devtest-lab-create-template.md) lub [formuła](devtest-lab-manage-formulas.md). Ten samouczek przedstawia przy użyciu hello Azure tooadd portalu laboratorium tooa maszyny Wirtualnej w usłudze DevTest Labs.

Ten artykuł zawiera także sposób toomanage hello artefaktów dla maszyn wirtualnych w laboratorium.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Kroki tooadd laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs
1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
1. Z listy hello labs wybierz laboratorium hello, w której ma zostać hello toocreate maszyny Wirtualnej.  
1. W laboratorium hello **omówienie** bloku, wybierz opcję **+ Dodaj**.  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Na powitania **wybierz podstawowej** bloku, wybierz podstawa hello maszyny Wirtualnej.
1. Na powitania **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej hello w hello **nazwę maszyny wirtualnej** pola tekstowego.

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej hello.  
1. Jeśli chcesz, aby toouse hasła przechowywane w Twojej [tajny magazynu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), wybierz pozycję **używać hasła zapisane**i określ wartości klucza, który odpowiada tooyour hasło. W przeciwnym razie wprowadź hasło w polu tekstowym hello etykietą **wpisz wartość**.
1. Witaj **typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla hello maszyn wirtualnych w laboratorium hello.
1. Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z hello wstępnie zdefiniowane elementy, które określić hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej.
1. Wybierz **artefakty** — z listy hello artefaktów — wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz.
    **Uwaga:** nowe Labs tooDevTest lub konfigurowanie artefaktów, zobacz toohello [Dodawanie istniejących tooa artefaktu maszyny Wirtualnej](#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.
1. Wybierz **Zaawansowane ustawienia** opcje i wygaśnięcia opcje sieciowe tooconfigure hello maszyny Wirtualnej. 

   tooset opcję wygaśnięcia, wybierz hello kalendarza ikona toospecify daty, na którym hello maszyny Wirtualnej zostaną automatycznie usunięte.  Domyślnie program hello wirtualna nigdy nie wygasa. 
1. Tooview lub skopiuj hello szablonu usługi Azure Resource Manager, zobacz toohello [szablonu Zapisz Azure Resource Manager](#save-azure-resource-manager-template) , a następnie wróć tutaj po zakończeniu.
1. Wybierz **Utwórz** tooadd hello określony laboratorium toohello maszyny Wirtualnej.
1. Blok laboratorium Hello Wyświetla stan hello tworzenie hello VM - najpierw jako **tworzenie**, następnie jako **systemem** po hello maszyna wirtualna została uruchomiona.

> [!NOTE]
> [Dodaj Maszynę wirtualną claimable](devtest-lab-add-claimable-vm.md) pokazuje, jak toomake hello claimable maszyny Wirtualnej, aby była ona dostępna do użycia przez dowolnego użytkownika hello laboratorium.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Dodaj istniejące tooa artefaktu maszyny Wirtualnej
Podczas tworzenia maszyny Wirtualnej, można dodać istniejącego artefaktów. Każdy laboratorium obejmuje artefaktów z hello publicznego DevTest Labs artefaktu repozytorium, a także artefaktów, że po utworzeniu i tooyour dodano własne repozytorium artefaktów.

* Azure DevTest Labs *artefakty* umożliwiają określenie *akcje* który są wykonywane, gdy zostanie zainicjowana hello maszyny Wirtualnej, takie jak uruchamianie skryptów programu Windows PowerShell, uruchamianie poleceń Bash i instalowania oprogramowania.
* Artefaktu *parametry* umożliwiają dostosowanie hello artefaktu dla konkretnego scenariusza

toodiscover toocreate artefaktów, zobacz temat hello artykułu, [Dowiedz się, jak tooauthor własne artefaktów dla za pomocą DevTest Labs](devtest-lab-artifact-author.md).

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
1. Z listy hello labs wybierz hello laboratorium zawierającego hello maszynę Wirtualną, z którym ma zostać toowork.  
1. Wybierz **Moje maszyny wirtualne**.
1. Wybierz hello żądana maszyny Wirtualnej.
1. Wybierz **artefakty**. 
1. Wybierz **zastosować artefakty**.
1. Na powitania **zastosować artefakty** bloku, wybierz hello artefaktu ma toohello tooadd maszyny Wirtualnej.
1. Na powitania **artefaktu Dodaj** bloku, wprowadź wartości parametrów hello wymaganych i opcjonalnych parametrów, które są potrzebne.  
1. Wybierz **Dodaj** toohello artefaktów i przywracać hello tooadd **zastosować artefakty** bloku.
1. Czy kontynuować dodawanie artefakty zgodnie z potrzebami dla maszyny Wirtualnej.
1. Po dodaniu użytkownika artefakty możesz [zmienić kolejność hello, w których hello artefakty są uruchamiane](#change-the-order-in-which-artifacts-are-run). Możesz również wrócić zbyt[wyświetlać lub modyfikować artefaktu](#view-or-modify-an-artifact).
1. Po zakończeniu dodawania artefakty wybierz **Zastosuj**

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Zmień kolejność hello, w którym są uruchamiane artefaktów
Domyślnie akcje hello artefaktów hello są wykonywane w kolejności hello, w której są dodawane toohello maszyny Wirtualnej. Hello poniższe kroki przedstawiają sposób toochange hello kolejności, w których hello artefakty są uruchamiane.

1. U góry hello hello **zastosować artefakty** bloku, link hello wybierz opcję określającą liczbę hello artefaktów, które zostały dodane toohello maszyny Wirtualnej.
   
    ![Dodawany numer artefaktów tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Na powitania **wybrane artefakty** bloku, przeciągnij i upuść artefakty hello na powitania potrzeby kolejności. **Uwaga:** Jeśli masz problemy z przeciąganiem artefaktu hello, upewnij się, czy przeciąga z powitania po lewej stronie powitania artefaktu. 
1. Po zakończeniu wybierz przycisk **OK**.  

## <a name="view-or-modify-an-artifact"></a>Wyświetlanie i modyfikowanie artefaktów
Witaj poniższe kroki przedstawiają sposób tooview lub modyfikowanie parametrów hello artefaktu:

1. U góry hello hello **zastosować artefakty** bloku, link hello wybierz opcję określającą liczbę hello artefaktów, które zostały dodane toohello maszyny Wirtualnej.
   
    ![Dodawany numer artefaktów tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Na powitania **wybrane artefakty** bloku, wybierz hello artefaktu ma tooview, lub edytować.  
1. Na powitania **artefaktu Dodaj** bloku, utwórz wszelkie wymagane zmiany i wybierz **OK** tooclose hello **artefaktu Dodaj** bloku.
1. Wybierz **OK** tooclose hello **wybrane artefakty** bloku.

## <a name="save-azure-resource-manager-template"></a>Zapisz szablon usługi Azure Resource Manager
Szablon usługi Azure Resource Manager udostępnia toodefine deklaratywne powtarzalne wdrożenia. Hello następujące kroki opisano, jak toosave hello szablonu usługi Azure Resource Manager dla hello Trwa tworzenie maszyny Wirtualnej.
Po zapisaniu szablonu usługi Azure Resource Manager hello można użyć zbyt[wdrażania nowych maszyn wirtualnych przy użyciu programu Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. Na powitania **maszyny wirtualnej** bloku, wybierz opcję **szablon ARM widoku**.
2. Na powitania **szablonu widoku Azure Resource Manager** bloku, wybierz hello szablonu tekstu.
3. Kopiuj hello Schowka toohello zaznaczonego tekstu.
4. Wybierz **OK** tooclose hello **bloku Wyświetl szablon Menedżera zasobów Azure**.
5. Otwórz Edytor tekstu.
6. Wklej tekst szablonu hello ze Schowka hello.
7. Zapisz plik hello do późniejszego użycia.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Następne kroki
* Raz hello maszyna wirtualna została utworzona, można połączyć toohello maszyny Wirtualnej, wybierając **Connect** w bloku hello maszyny Wirtualnej.
* Dowiedz się, jak za[Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs](devtest-lab-artifact-author.md).
* Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
