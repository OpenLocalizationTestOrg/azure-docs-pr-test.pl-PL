---
title: aaaAttach tooa dysku maszyny Wirtualnej Azure classic | Dokumentacja firmy Microsoft
description: "Dołącz dane dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania i zainicjować go."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Dołącz dane dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

W tym artykule opisano sposób tworzenia tooattach nowych i istniejących dysków w z hello Classic wdrażania modelu tooa maszyny wirtualnej systemu Windows przy użyciu hello portalu Azure.

Możesz również [dołączyć tooa dysku danych maszyny Wirtualnej systemu Linux w portalu Azure hello](../../linux/attach-disk-portal.md).

Przed dołączeniem dysku, należy przejrzeć te wskazówki:

* Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Magazyn w warstwie Premium toouse, należy serii DS lub GS-series maszyny wirtualnej. Z tych maszyn wirtualnych służy dysków z konta magazynu zarówno Premium i standardowa. Magazyn w warstwie Premium jest dostępna w pewnych regionach. Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Dla nowego dysku nie ma potrzeby toocreate jej pierwszym ponieważ Azure tworzy go po dołączeniu go.

Możesz również [dołączenie dysku danych przy użyciu programu Powershell](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Znajdź hello maszyny wirtualnej
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz hello maszyny wirtualnej z wymienionych na pulpicie nawigacyjnym hello zasobu hello.
3. W okienku po lewej stronie powitania w obszarze **ustawienia**, kliknij przycisk **dysków**.

    ![Otwórz ustawienia dysku](./media/attach-disk/virtualmachinedisks.png)

Kontynuuj przez następujące instrukcje dotyczące dołączania albo [nowy dysk](#option-1-attach-a-new-disk) lub [istniejącego dysku](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opcja 1: Dołączać i zainicjuj nowego dysku

1. Na powitania **dysków** bloku, kliknij przycisk **Dołącz nowy**.
2. Przejrzyj ustawienia domyślne hello, zaktualizuj odpowiednio do potrzeb, a następnie kliknij **OK**.

   ![Przejrzyj ustawienia dysku](./media/attach-disk/attach-new.png)

3. Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.

### <a name="initialize-a-new-data-disk"></a>Zainicjuj nowy dysk danych

1. Połącz toohello maszyny wirtualnej. Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Po zalogowaniu się na maszynie wirtualnej toohello Otwórz **Menedżera serwera**. Wybierz w okienku po lewej stronie powitania **usług plików i magazynowania**.

    ![Otwórz Menedżera serwera](../media/attach-disk-portal/fileandstorageservices.png)

3. Wybierz **dysków**.
4. Witaj **dysków** sekcja zawiera informacje o dyskach hello. W większości przypadków maszyny wirtualnej ma dysk 0 na partycje, dysk 1 i 2 dysku. Dysk 0 na partycje jest hello dysk systemu operacyjnego, dysk 1 jest hello tymczasowego i dysk 2 jest dysk danych hello nowo dołączony toohello maszyny wirtualnej. Hello list dysku danych hello partycji jako **nieznany**.

 Kliknij prawym przyciskiem myszy dysk hello i wybierz **zainicjować**.

5. Wiesz, że wszystkie dane zostaną usunięte po zainicjowaniu hello dysku. Kliknij przycisk **tak** tooacknowledge hello ostrzeżenie i zainicjować hello dysku. Po wykonaniu tych czynności partycji hello będzie wyświetlany jako **GPT**. Ponownie kliknij prawym przyciskiem myszy dysk hello i wybierz **nowy wolumin**.

6. Ukończ Kreatora hello przy użyciu wartości domyślnych hello. Po zakończeniu pracy Kreatora hello hello **woluminów** sekcji przedstawiono hello nowego woluminu. dysk Hello jest teraz danych toostore w trybie online i gotowe.

    ![Wolumin został zainicjowany pomyślnie](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Opcja 2: Dołączanie istniejącego dysku
1. Na powitania **dysków** bloku, kliknij przycisk **Attach istniejących**.
2. W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **lokalizacji**.

   ![Dołączanie istniejącego dysku](./media/attach-disk/attachexistingdisksettings.png)
3. W obszarze **kont magazynu**, wybierz konto hello i kontener, który zawiera plik VHD hello.

   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Wybierz plik VHD hello.
5. W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik hello jest wyświetlana w obszarze **pliku VHD**. Kliknij przycisk **OK**.
6. Po Azure dołącza hello maszyny wirtualnej toohello dysku, znajduje się w ustawieniach dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.

## <a name="use-trim-with-standard-storage"></a>PRZYCINANIE za pomocą magazynu w warstwie standardowa

Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE. PRZYCINANIE odrzuca nieużywanych bloków na dysku hello tak rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz. Korzystając z operacją PRZYCINANIA zapisać kosztów, w tym nieużywanych bloków wynikających z usunięcie dużych plików.

Możesz uruchomić to polecenie toocheck hello PRZYCINANIA ustawienie. Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:

```
fsutil behavior query DisableDeleteNotify
```

Jeśli polecenie hello zwraca wartość 0, PRZYCINANIE włączono poprawnie. Jeśli zmienna zwraca 1, uruchom następujące polecenie tooenable PRZYCINANIE hello:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Następne kroki
Jeśli aplikacja wymaga toouse hello D: dysku toostore danych, możesz [zmienić hello litera dysku tymczasowego Windows hello](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Dodatkowe zasoby
[O dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../../virtual-machines-linux-about-disks-vhds.md)
