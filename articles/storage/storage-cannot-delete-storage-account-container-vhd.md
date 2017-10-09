---
title: "aaaTroubleshoot usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w klasycznym wdrożenia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w wdrożenie klasyczne
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Może pojawić się błędy podczas próby toodelete hello konta magazynu Azure, kontenera lub wirtualnego dysku twardego w hello [portalu Azure](https://portal.azure.com/) lub hello [klasycznego portalu Azure](https://manage.windowsazure.com/). Witaj problemów może być spowodowane hello w następujących okolicznościach:

* Po usunięciu maszyny Wirtualnej hello dysku i wirtualnego dysku twardego nie są automatycznie usuwane. Może to być hello Przyczyna niepowodzenia usuwania konta magazynu. Firma Microsoft nie należy usuwać hello dysku, aby mogli używać toomount dysku hello inną maszynę Wirtualną.
* Na dysku lub hello obiektu blob skojarzoną z dyskiem hello nadal jest dzierżawy.
* Nadal jest obraz maszyny Wirtualnej, który używa konta obiektów blob, kontenera lub magazynu.

Jeśli problem Azure nie jest opisany w tym artykule, odwiedź hello na forach platformy Azure [MSDN i hello przepełnienie stosu](https://azure.microsoft.com/support/forums/). Problem można umieścić na tych fora lub too@AzureSupport w serwisie Twitter. Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na powitania [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="symptoms"></a>Objawy
powitania po sekcja zawiera listę typowych błędów, które może pojawić się podczas próby kontami magazynu Azure hello toodelete, kontenery lub wirtualne dyski twarde.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Scenariusz 1: Nie można toodelete konta magazynu
Po przejściu konta magazynu classic toohello w hello [portalu Azure](https://portal.azure.com/) i wybierz **usunąć**, mogą być prezentowane z listy obiektów, które uniemożliwiają usunięcie konta magazynu hello:

  ![Obraz błąd podczas usuwania konta magazynu hello](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Po przejściu toohello konta magazynu w hello [klasycznego portalu Azure](https://manage.windowsazure.com/) i wybierz **usunąć**, może pojawić się jeden hello następujące błędy:

- *Konto magazynu StorageAccountName zawiera obrazów maszyn wirtualnych. Upewnij się, że te obrazy muszą zostać usunięte przed usunięciem tego konta magazynu.*

- *Konto magazynu toodelete < vm magazynu account-name > nie powiodło się. Konto magazynu toodelete < vm magazynu account-name >: "konto magazyn < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski. Te obrazy i/lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu. ".*

- *Konto magazynu < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski, np. xxxxxxxxx-xxxxxxxxx-O-209490240936090599. Upewnij się, te obrazy i lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu.*

- *Konto magazynu < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Te artefakty muszą zostać usunięte z repozytorium obrazów hello przed usunięciem tego konta magazynu*.

- *Przedstawia się, że konto magazynu nie powiodła się < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Upewnij się, że te artefakty muszą zostać usunięte z repozytorium obrazów hello przed usunięciem tego konta magazynu. Podczas próby toodelete konta magazynu i nie są skojarzone z nim dyski nadal aktywne, zostanie wyświetlony komunikat informujący o tym, istnieją aktywne dysków, które należy usunąć toobe*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Scenariusz 2: Nie można toodelete kontenera
Podczas próby kontenera magazynu hello toodelete można napotkać hello następujący błąd:

*Kontenera magazynu nie powiodło się toodelete <container name>. Błąd: "jest obecnie dzierżawy w kontenerze hello i identyfikator dzierżawy nie został określony w żądaniu hello*.

Lub

*powitania po dysków maszyny wirtualnej korzysta obiekty BLOB w tym kontenerze, dlatego nie można usunąć kontenera hello: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Scenariusz 3: Nie można toodelete wirtualnego dysku twardego
Po usunięciu maszyny Wirtualnej i następnie obiekty BLOB hello toodelete spróbuj dla hello odpowiednich wirtualne dyski twarde, może pojawić się następujące wiadomość hello:

*Obiekt blob toodelete nie powiodło się "path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Błąd: "jest obecnie dzierżawy na powitania obiektów blob i identyfikator dzierżawy nie został określony w żądaniu hello.*

Lub

*Obiektu blob "BlobName.vhd" jest używany jako dysk maszyny wirtualnej "VirtualMachineDiskName", dlatego nie można usunąć obiektu blob hello.*

## <a name="solution"></a>Rozwiązanie
tooresolve hello najbardziej typowe problemy, spróbuj hello następujące metody:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>Krok 1: Usuń wszystkie dyski, które uniemożliwiają usunięcie konta magazynu hello, kontenera lub wirtualnego dysku twardego
1. Przełącz toohello [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Wybierz **maszyny WIRTUALNEJ** > **dysków**.

    ![Obraz dysków na maszynach wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Zlokalizuj hello dysków, które są skojarzone z konta magazynu hello, kontenera lub dysku VHD, które mają toodelete. Po zaznaczeniu hello lokalizację dysku hello znajdziesz hello skojarzonego konta magazynu, kontenera lub wirtualnego dysku twardego.

    ![Obraz, który zawiera informacje o lokalizacji dla dysków w klasycznym portalu Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Usuń dyski hello przy użyciu jednej z następujących metod hello:

  - Jeśli istnieje maszyna wirtualna nie są wyświetlane na hello **podłączone do** pola hello dysku, możesz usunąć dysk hello bezpośrednio.

  - Jeśli dysk hello jest dysk danych, wykonaj następujące kroki:

    1. Sprawdź nazwę hello hello, w której jest dołączona maszyna wirtualna, która hello dysku.
    2. Przejdź za**maszyn wirtualnych** > **wystąpień**, a następnie zlokalizuj hello maszyny Wirtualnej.
    3. Upewnij się, że nic nie jest aktywnie używających hello dysku.
    4. Wybierz **odłączyć dysku** u dołu hello hello portalu toodetach hello dysku.
    5. Przejdź za**maszyn wirtualnych** > **dysków**i zaczekaj, aż hello **podłączone do** tooturn pole puste. Oznacza to, że dysk hello pomyślnie została odłączona od hello maszyny Wirtualnej.
    6. Wybierz **usunąć** u dołu hello **maszyn wirtualnych** > **dysków** toodelete hello dysku.

  - Jeśli hello dysk jest dyskiem systemu operacyjnego (hello **zawiera system operacyjny** pole ma wartość, takich jak system Windows) i dołączone tooa maszyny Wirtualnej, wykonaj następujące kroki hello toodelete maszyny Wirtualnej. Nie można odłączyć dysku systemu operacyjnego Hello, dzięki czemu będziemy mogli toodelete hello wirtualna toorelease hello dzierżawy.

    1. Sprawdź nazwę hello powitalne maszyny wirtualnej hello dysk danych jest dołączony do.  
    2. Przejdź za**maszyn wirtualnych** > **wystąpień**, a następnie wybierz hello maszynę Wirtualną, która hello dysku jest dołączony do.
    3. Upewnij się, że nic nie jest aktywnie używających hello maszyny wirtualnej i czy użytkownik nie jest już konieczne hello maszyny wirtualnej.
    4. Wybierz hello wirtualna hello dysk jest dołączony do, następnie wybierz **usunąć** > **Delete hello dołączone dyski**.
    5. Przejdź za**maszyn wirtualnych** > **dysków**i zaczekaj, aż hello toodisappear dysku.  Może potrwać kilka minut, aż ten toooccur i może być konieczne toorefresh hello strony.
    6. Jeśli dysk hello nie zniknie, poczekaj, aż hello **podłączone do** tooturn pole puste. Oznacza to, że dysk hello pełni została odłączona od hello maszyny Wirtualnej.  Następnie wybierz dysk hello i wybierz **usunąć** u dołu hello hello strony toodelete hello dysku.


   > [!NOTE]
   > Jeśli dysk jest tooa dołączona maszyna wirtualna, nie będzie możliwe toodelete go. Dyski są odłączone asynchronicznie z usuniętych maszyny Wirtualnej. Może upłynąć kilka minut, po usunięciu hello maszyny Wirtualnej dla tego tooclear pole w górę.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>Krok 2: Usuń wszelkie obrazów maszyn wirtualnych, które uniemożliwiają usunięcie konta magazynu hello lub kontenera
1. Przełącz toohello [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Wybierz **maszyny WIRTUALNEJ** > **obrazów**, a następnie usuń hello obrazów, które są skojarzone z kontem magazynu hello, kontenera lub wirtualnego dysku twardego.

    Po tym spróbuj ponownie konto magazynu hello toodelete, kontenera lub wirtualnego dysku twardego.

> [!WARNING]
> Należy się tooback zapasową wszystkich danych, które mają toosave przed usunięciem konta hello. Po usunięciu wirtualnego dysku twardego, obiektów blob, tabeli, kolejki lub pliku spowoduje jego trwałe skasowanie. Upewnij się, że hello zasób nie jest w użyciu.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>O hello stan zatrzymane (cofnięciu przydziału)
Maszyny wirtualne, które zostały utworzone w hello klasycznego modelu wdrażania i zostać zatrzymane będą miały hello **zatrzymane (cofnięciu przydziału)** stan albo hello [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure ](https://manage.windowsazure.com/).

**Klasyczny portal Azure**:

![Zatrzymano stanu (Deallocated) dla maszyn wirtualnych z portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure portal**:

![Zatrzymana (cofnięciu przydziału) stanu dla maszyn wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

Stan "Zatrzymane (cofnięciu przydziału)" zwalnia zasoby komputera hello, takie jak hello procesora CPU, pamięci i sieci. dyski Hello, jednak są nadal przechowywane, dzięki czemu będzie można szybko utworzyć ponownie hello maszyny Wirtualnej w razie potrzeby. Te dyski są tworzone na wirtualne dyski twarde, które bazują na magazynu Azure. Konto magazynu Hello ma te wirtualne dyski twarde i dyski hello jest dzierżawy na tych dyskach VHD.

## <a name="next-steps"></a>Następne kroki
* [Usunięcie konta magazynu](storage-create-storage-account.md#delete-a-storage-account)
