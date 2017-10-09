---
title: "aaaAttach niezarządzanych danych dysku tooa maszyny Wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft"
description: "Jak tooattach niezarządzanych danych nowego lub istniejącego dysku tooa maszyny Wirtualnej systemu Windows w hello przy użyciu portalu Azure hello modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Jak tooattach niezarządzanych danych na dysku tooa maszyny Wirtualnej systemu Windows w hello portalu Azure

W tym artykule opisano sposób niezarządzanych tooattach istniejących i nowych dysków tooWindows maszyn wirtualnych za pośrednictwem hello portalu Azure. Możesz również [dołączenie dysku danych przy użyciu programu PowerShell](./attach-disk-ps.md). Zanim to zrobisz, przejrzyj następujące wskazówki:

* Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).
* Magazyn w warstwie Premium toouse, należy serii DS lub GS-series maszyny wirtualnej. Z tych maszyn wirtualnych służy dysków z konta magazynu zarówno Premium i standardowa. Magazyn w warstwie Premium jest dostępna w pewnych regionach. Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Dla nowego dysku nie ma potrzeby toocreate jej pierwszym ponieważ Azure tworzy go po dołączeniu go.


Możesz również [dołączenie dysku danych przy użyciu programu Powershell](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Znajdź hello maszyny wirtualnej
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu powitania po lewej stronie powitania kliknij **maszyn wirtualnych**.
3. Wybierz maszynę wirtualną hello z listy hello.
4. W bloku maszyny wirtualnej powitania kliknij **dysków**.
   
Kontynuuj przez następujące instrukcje dotyczące dołączania albo [nowy dysk](#option-1-attach-a-new-disk) lub [istniejącego dysku](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opcja 1: Dołączać i zainicjuj nowego dysku
1. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. W hello **dysków zarządzanych w Attach** bloku, wpisz nazwę dysku hello w **nazwa** , a następnie wybierz **New (pusty dysk)** w **typ źródła**.
3. W obszarze **kontenera magazynu**, kliknij przycisk hello **Przeglądaj** przycisk i Przeglądaj toohello konta magazynu i kontener, w którym chcesz hello nowego wirtualnego dysku twardego toobe przechowywane i następnie kliknij przycisk **wybierz**. 
  
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Po wykonaniu hello ustawienia hello dysku danych, kliknij przycisk **OK**.
4. Po powrocie do hello **dysków** bloku, kliknij przycisk **zapisać** konfiguracji maszyny Wirtualnej toohello tooadd hello dysku.


### <a name="initialize-a-new-data-disk"></a>Zainicjuj nowy dysk danych

1. Połącz toohello maszyny wirtualnej. Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Kliknij przycisk hello **Start** menu wewnątrz hello maszyny Wirtualnej i typ **diskmgmt.msc** i trafień **Enter**. Spowoduje to uruchomienie przystawki Zarządzanie dyskami hello.
2. Zarządzanie dyskami uznaje, że znajduje się dysk nowy, niezainicjowanej hello Inicjowanie dysku oknie wyskakującym zostanie.
3. Upewnij się, że wybrano hello nowy dysk i kliknij przycisk **OK** tooinitialize go.
4. Witaj nowy dysk jest teraz wyświetlany jako **nieprzydzielonego**. Kliknij prawym przyciskiem myszy na powitania dysku i wybierz **nowy wolumin prosty**. Witaj **Kreatorze nowych woluminów prostych** uruchamia.
5. Przejdź przez kreatora hello zapewniają, że wszystkie ustawienia domyślne hello, po zakończeniu wybierz **Zakończ**.
6. Zamknij program Zarządzanie dyskami.
7. Pobierz okno podręczne, które należy tooformat hello nowy dysk przed jego użyciem. Kliknij przycisk **Format dysku**.
8. W hello **Format nowy dysk** okna dialogowego, sprawdź hello ustawienia, a następnie kliknij przycisk **Start**.
9. Kliknij pozycję wyświetlone ostrzeżenie, że formatowanie hello dysków na partycje powoduje usunięcie wszystkich danych hello **OK**.
10. Po zakończeniu format powitania kliknij **OK**.


## <a name="option-2-attach-an-existing-disk"></a>Opcja 2: Dołączanie istniejącego dysku
1. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Na powitania **dysku niezarządzane Attach** bloku, w **typ źródła** wybierz **blob istniejące**.

    ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Kliknij przycisk **Przeglądaj** toonavigate toohello konto magazynu i kontener, w którym hello istniejącego dysku VHD znajduje się. Kliknij i hello wirtualnego dysku twardego, a następnie kliknij **wybierz**.
4. Kliknij przycisk **OK** w hello **dysku niezarządzane Attach** bloku.
5. W hello **dysków** bloku, kliknij przycisk **zapisać** tooadd hello dysku toohello Konfiguracja hello maszyny Wirtualnej.
   


## <a name="use-trim-with-standard-storage"></a>PRZYCINANIE za pomocą magazynu w warstwie standardowa

Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE. PRZYCINANIE odrzuca nieużywanych bloków na dysku hello tak rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz. Można to zapisanie kosztów, jeśli Tworzenie dużych plików, a następnie usuń je. 

Możesz uruchomić to polecenie toocheck hello PRZYCINANIA ustawienie. Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:

```
fsutil behavior query DisableDeleteNotify
```

Jeśli polecenie hello zwraca wartość 0, PRZYCINANIE włączono poprawnie. Jeśli zmienna zwraca 1, uruchom następujące polecenie tooenable PRZYCINANIE hello:
```
fsutil behavior set DisableDeleteNotify 0
```

Po usunięciu danych z dysku, upewnij się, że hello PRZYCINANIA operacji opróżniania poprawnie, uruchamiając defragmentowania z operacją PRZYCINANIA:

```
defrag.exe <volume:> -l
```

Ponadto upewnij się, że cały wolumin hello jest ograniczona przez formatowania woluminu hello.


## <a name="next-steps"></a>Następne kroki
Jeśli użytkownik aplikacji musi toouse hello D: dysku toostore danych, możesz [zmienić hello litera dysku tymczasowego Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

