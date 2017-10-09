---
title: "aaaAttach danych zarządzanych dysku tooa maszyny Wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft"
description: "Sposób tooattach nowe zarządzania tooa dysku danych maszyny Wirtualnej systemu Windows w hello przy użyciu portalu Azure hello modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Jak tooattach danych zarządzanych dysku tooa maszyny Wirtualnej systemu Windows w hello portalu Azure

W tym artykule opisano, jak tooattach nowych danych zarządzanych dysku tooWindows maszyn wirtualnych za pośrednictwem hello portalu Azure. Zanim to zrobisz, przejrzyj następujące wskazówki:

* Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).
* Dla nowego dysku nie ma potrzeby toocreate jej pierwszym ponieważ Azure tworzy go po dołączeniu go.

Możesz również [dołączenie dysku danych przy użyciu programu Powershell](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Dodaj dysk danych
1. W menu powitania po lewej stronie powitania kliknij **maszyn wirtualnych**.
2. Wybierz maszynę wirtualną hello z listy hello.
3. W bloku maszyny wirtualnej hello, kliknij polecenie **dysków**.
   4. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
5. Z listy rozwijanej dla nowego dysku hello hello, wybierz **utworzyć pusty**.
6. W hello **dysków zarządzanych w Utwórz** bloku, wpisz nazwę dla dysku hello i dostosować hello inne ustawienia w razie potrzeby. Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.
7. W hello **dysków** bloku, kliknij przycisk Zapisz toosave hello nowej konfiguracji dysku dla hello maszyny Wirtualnej.
6. Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.


## <a name="initialize-a-new-data-disk"></a>Zainicjuj nowy dysk danych

1. Połącz toohello maszyny Wirtualnej.
1. Kliknij menu start hello wewnątrz hello maszyny Wirtualnej i typ **diskmgmt.msc** i trafień **Enter**. Spowoduje to uruchomienie przystawki Zarządzanie dyskami hello.
2. Zarządzanie dyskami rozpozna, że znajduje się dysk nowy, które nie zostały zainicjowane i hello Inicjowanie dysku oknie wyskakującym zostanie.
3. Upewnij się, że wybrano hello nowy dysk i kliknij przycisk **OK** tooinitialize go.
4. nowy dysk Hello pojawi się jako **nieprzydzielonego**. Kliknij prawym przyciskiem myszy na powitania dysku i wybierz **nowy wolumin prosty**. Witaj **Kreatorze nowych woluminów prostych** zostanie uruchomiona.
5. Przejdź przez kreatora hello zapewniają, że wszystkie ustawienia domyślne hello, po zakończeniu wybierz **Zakończ**.
6. Zamknij program Zarządzanie dyskami.
7. Zostanie wyświetlony okno podręczne należy tooformat hello nowy dysk przed jego użyciem. Kliknij przycisk **Format dysku**.
8. W hello **Format nowy dysk** okna dialogowego, sprawdź hello ustawienia, a następnie kliknij przycisk **Start**.
9. Zostanie wyświetlone ostrzeżenie, że formatowanie dysków hello spowoduje usunięcie wszystkich danych powitania kliknij **OK**.
10. Po zakończeniu format powitania kliknij **OK**.

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
