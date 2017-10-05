---
title: "Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w klasycznym wdrożenia | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w wdrożenie klasyczne"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w wdrożenie klasyczne
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Może pojawić się błędy podczas próby usunięcia konta magazynu Azure, kontenera lub dysku VHD w programie [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure](https://manage.windowsazure.com/). Te problemy mogą być spowodowane przez następujące okoliczności:

* Dysk i wirtualny dysk twardy nie zostały automatycznie usunięte wraz z maszyną wirtualną. Może to być przyczyną niepowodzenia usuwania konta magazynu. Nie możemy Usuń dysk, dzięki czemu można użyć dysku do zainstalowania inną maszynę Wirtualną.
* Nadal istnieje dzierżawa dysku lub obiektu blob skojarzonego z dyskiem.
* Nadal jest obraz maszyny Wirtualnej, który używa konta obiektów blob, kontenera lub magazynu.

Jeśli problem Azure nie jest opisany w tym artykule, odwiedź fora Azure na [MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Możesz zamieścić problemu na tych fora lub do @AzureSupport w serwisie Twitter. Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="symptoms"></a>Objawy
W poniższej sekcji przedstawiono typowe błędy, które może pojawić się podczas próby usunięcia konta magazynu platformy Azure, kontenery lub wirtualne dyski twarde.

### <a name="scenario-1-unable-to-delete-a-storage-account"></a>Scenariusz 1: Nie można usunąć konta magazynu
Po przejściu do konta magazynu classic w [portalu Azure](https://portal.azure.com/) i wybierz **usunąć**, mogą być prezentowane z listy obiektów, które uniemożliwiają usunięcie konta magazynu:

  ![Obraz błąd podczas usuwania konta magazynu](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Po przejściu do konta magazynu w [klasycznego portalu Azure](https://manage.windowsazure.com/) i wybierz **usunąć**, może pojawić się jeden z następujących błędów:

- *Konto magazynu StorageAccountName zawiera obrazów maszyn wirtualnych. Upewnij się, że te obrazy muszą zostać usunięte przed usunięciem tego konta magazynu.*

- *Nie można usunąć konta magazynu < vm magazynu account-name >. Nie można usunąć konta magazynu < vm magazynu account-name >: "konto magazyn < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski. Te obrazy i/lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu. ".*

- *Konto magazynu < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski, np. xxxxxxxxx-xxxxxxxxx-O-209490240936090599. Upewnij się, te obrazy i lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu.*

- *Konto magazynu < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Te artefakty muszą zostać usunięte z repozytorium obrazów przed usunięciem tego konta magazynu*.

- *Przedstawia się, że konto magazynu nie powiodła się < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Upewnij się, że te artefakty muszą zostać usunięte z repozytorium obrazów przed usunięciem tego konta magazynu. Podczas próby usunięcia konta magazynu i nie są skojarzone z nim dyski nadal aktywne, zostanie wyświetlony komunikat informujący o active dysków, które muszą zostać usunięte*.

### <a name="scenario-2-unable-to-delete-a-container"></a>Scenariusz 2: Nie można usunąć kontenera
Podczas próby usunięcia kontenera magazynu, może zostać wyświetlony następujący błąd:

*Nie można usunąć kontenera magazynu <container name>. Błąd: "jest obecnie dzierżawy w kontenerze i identyfikator dzierżawy nie został określony w żądaniu*.

Lub

*Następujące dyski maszyny wirtualnej korzysta obiekty BLOB w tym kontenerze, dlatego nie można usunąć kontenera: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-to-delete-a-vhd"></a>Scenariusz 3: Nie można usunąć wirtualnego dysku twardego
Po usunięciu maszyny Wirtualnej i spróbuj go usunąć obiekty BLOB i skojarzone pliki VHD, może pojawić się następujący komunikat:

*Nie można usunąć obiektu blob "path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Błąd: "jest obecnie dzierżawy w obiekcie blob i identyfikator dzierżawy nie został określony w żądaniu.*

Lub

*Obiektu blob "BlobName.vhd" jest używany jako dysk maszyny wirtualnej "VirtualMachineDiskName", dlatego nie można usunąć obiektu blob.*

## <a name="solution"></a>Rozwiązanie
Aby rozwiązać najbardziej typowe problemy, wypróbuj następujące metody:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a>Krok 1: Usuń wszystkie dyski, które uniemożliwiają usunięcie konta magazynu, kontenera lub wirtualnego dysku twardego
1. Przełącz się do [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Wybierz **maszyny WIRTUALNEJ** > **dysków**.

    ![Obraz dysków na maszynach wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Znajdź dyski skojarzone z kontem magazynu, kontenerem lub wirtualnym dyskiem twardym, które chcesz usunąć. Są one dostępne w lokalizacji dysku.

    ![Obraz, który zawiera informacje o lokalizacji dla dysków w klasycznym portalu Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Usuń dyski za pomocą jednej z następujących metod:

  - Jeśli istnieje maszyna wirtualna nie są wyświetlane na **podłączone do** pola dysku, możesz usunąć dysk bezpośrednio.

  - Jeśli dysk jest dyskiem danych, wykonaj następujące kroki:

    1. Sprawdź nazwę dołączonego dysku do maszyny wirtualnej.
    2. Przejdź do **maszyn wirtualnych** > **wystąpień**, a następnie zlokalizuj maszyny Wirtualnej.
    3. Upewnij się, że nic nie jest aktywnie przy użyciu dysku.
    4. Wybierz **odłączyć dysku** w dolnej części portalu, aby odłączyć dysk.
    5. Przejdź do **maszyn wirtualnych** > **dysków**i zaczekaj, aż **podłączone do** pola, aby włączyć puste. Oznacza to, że dysk został pomyślnie odłączona od maszyny Wirtualnej.
    6. Wybierz **usunąć** w dolnej części **maszyn wirtualnych** > **dysków** można usunąć dysku.

  - Jeśli dysk jest dyskiem systemu operacyjnego ( **zawiera system operacyjny** pole ma wartość, takich jak system Windows) i dołączony do maszyny Wirtualnej, wykonaj następujące kroki, aby usunąć maszynę Wirtualną. Nie można odłączyć dysk systemu operacyjnego, a więc musimy usunąć maszynę Wirtualną do zwolnienia dzierżawy.

    1. Sprawdź nazwę dysk danych jest dołączony do maszyny wirtualnej.  
    2. Przejdź do **maszyn wirtualnych** > **wystąpień**, a następnie wybierz dysk dołączony do maszyny Wirtualnej.
    3. Upewnij się, że nic nie jest aktywnie przy użyciu maszyny wirtualnej i nie są już potrzebne maszyny wirtualnej.
    4. Wybierz dysk maszyny Wirtualnej jest dołączony do, następnie wybierz **usunąć** > **usuwanie dołączonych dysków**.
    5. Przejdź do **maszyn wirtualnych** > **dysków**i zaczekaj na znikają dysku.  Może upłynąć kilka minut, aż to możliwe, i może być konieczne odświeżenie strony.
    6. Jeśli dysk nie zniknie, poczekaj, aż **podłączone do** pola, aby włączyć puste. Oznacza to, że dysk pełni została odłączona od maszyny Wirtualnej.  Następnie wybierz dysk i wybierz **usunąć** w dolnej części strony, aby usunąć dysk.


   > [!NOTE]
   > Jeśli dysk jest dołączony do maszyny Wirtualnej, nie można go usunąć. Dyski są odłączone asynchronicznie z usuniętych maszyny Wirtualnej. Może upłynąć kilka minut, po usunięciu maszyny Wirtualnej dla tego pola wyczyszczone.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a>Krok 2: Usuń wszelkie obrazy maszyny Wirtualnej, które uniemożliwiają usunięcie konta magazynu i kontener
1. Przełącz się do [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Wybierz **maszyny WIRTUALNEJ** > **obrazów**, a następnie usuń obrazów, które są skojarzone z kontem magazynu, kontenera lub wirtualnego dysku twardego.

    Następnie ponownie spróbuj usunąć konto magazynu, kontenera lub wirtualnego dysku twardego.

> [!WARNING]
> Zanim usuniesz konto, wykonaj kopię zapasową wszystkich danych, które chcesz zapisać. Po usunięciu wirtualnego dysku twardego, obiektów blob, tabeli, kolejki lub pliku spowoduje jego trwałe skasowanie. Upewnij się, że zasób nie jest w użyciu.
>
>

## <a name="about-the-stopped-deallocated-status"></a>Stan zatrzymane (cofnięciu przydziału)
Maszyny wirtualne, które zostały utworzone w klasycznym modelu wdrażania i zostać zatrzymane będą miały **zatrzymane (cofnięciu przydziału)** stanu w zależności [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure](https://manage.windowsazure.com/).

**Klasyczny portal Azure**:

![Zatrzymano stanu (Deallocated) dla maszyn wirtualnych z portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure portal**:

![Zatrzymana (cofnięciu przydziału) stanu dla maszyn wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

Stan "Zatrzymane (cofnięciu przydziału)" zwalnia zasoby komputera, na przykład procesora CPU, pamięci i sieci. Dyski, jednak są nadal przechowywane, dzięki czemu będzie można szybko utworzyć ponownie maszynę Wirtualną w razie potrzeby. Te dyski są tworzone na wirtualne dyski twarde, które bazują na magazynu Azure. Konto magazynu ma następujące wirtualne dyski twarde, a dyski mają dzierżawy na tych dyskach VHD.

## <a name="next-steps"></a>Następne kroki
* [Usunięcie konta magazynu](storage-create-storage-account.md#delete-a-storage-account)
