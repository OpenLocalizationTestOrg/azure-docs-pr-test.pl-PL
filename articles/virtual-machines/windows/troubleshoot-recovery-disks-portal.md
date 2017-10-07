---
title: "aaaUse a Windows Rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot problemów maszyny wirtualnej systemu Windows na platformie Azure w przypadku łączącego hello systemu operacyjnego dysku tooa odzyskiwania maszyny Wirtualnej przy użyciu hello portalu Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Rozwiązywanie problemów z maszyny Wirtualnej systemu Windows, dołączając hello systemu operacyjnego maszyny Wirtualnej odzyskiwania tooa dysku przy użyciu hello portalu Azure
Jeśli maszyny wirtualnej systemu Windows (VM) na platformie Azure napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów. Typowym przykładem jest aktualizację aplikacji, która uniemożliwia hello maszyna wirtualna stanie tooboot pomyślnie. Szczegółów tego artykułu jak toouse hello Azure tooconnect portalu wirtualnej twardego błędy tooanother toofix maszyny Wirtualnej systemu Windows na dysku, a następnie ponownie utwórz oryginalnego maszyny Wirtualnej.

## <a name="recovery-process-overview"></a>Omówienie procesu odzyskiwania
proces rozwiązywania problemów Hello jest następujący:

1. Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.
2. Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Windows na potrzeby rozwiązywania problemów.
3. Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej. Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.
4. Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.
5. Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.


## <a name="determine-boot-issues"></a>Określenie zagadnień rozruchu
toodetermine Dlaczego maszyny Wirtualnej nie jest możliwe tooboot poprawnie, sprawdź, czy diagnostyki rozruchu hello zrzut ekranu maszyny Wirtualnej. Typowym przykładem może być aktualizacji aplikacji nie powiodło się lub podstawowy wirtualny dysk twardy jest usunięty lub przeniesiony.

Wybierz maszyny Wirtualnej w portalu hello, a następnie przewiń w dół toohello **pomocy technicznej i rozwiązywania problemów** sekcji. Kliknij przycisk **diagnostyki rozruchu** zrzut ekranu hello tooview. Należy pamiętać, wszystkie określone komunikaty o błędach lub kody błędów toohelp ustalić, dlaczego hello wirtualna doświadcza problemu. Witaj poniższy przykład przedstawia Maszynę wirtualną oczekiwanie na zatrzymanie usługi:

![Wyświetlanie maszyny Wirtualnej diagnostyki rozruchu dzienniki konsoli](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

Możesz również kliknąć **zrzut ekranu** toodownload przechwytywania hello zrzut ekranu maszyny Wirtualnej.


## <a name="view-existing-virtual-hard-disk-details"></a>Szczegóły istniejącego wirtualnego dysku twardego
Przed dołączeniem tooanother Twojego wirtualnego dysku twardego maszyny Wirtualnej, potrzebna jest nazwa hello tooidentify hello wirtualnego dysku twardego (VHD). 

Wybierz grupę zasobów z hello portalu, a następnie wybierz konto magazynu. Kliknij przycisk **obiekty BLOB**w hello poniższy przykład:

![Wybierz magazyn obiektów blob](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

Zwykle mają kontener o nazwie **wirtualne dyski twarde** który przechowuje wirtualnych dysków twardych. Wybierz tooview kontenera hello listę wirtualnych dysków twardych. Nazwy hello notatki z wirtualnego dysku twardego (prefiks hello jest zwykle hello nazwą maszyny Wirtualnej):

![Określenie dysku VHD w programie kontenera magazynu](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Wybierz z listy hello istniejącego wirtualnego dysku twardego i skopiuj adres URL hello do użycia w hello następujące kroki:

![Skopiuj istniejący adres URL wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Usuń istniejącą maszynę Wirtualną
Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure. Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje. Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC). Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej. Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta. dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.

pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie. Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu. Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.

Wybierz maszyny Wirtualnej w portalu hello, a następnie kliknij przycisk **usunąć**:

![Maszyna wirtualna rozruchu diagnostyki zrzut ekranu przedstawiający błąd rozruchu](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej. dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej
Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów. Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse stanie toobe maszyny Wirtualnej i edytowania zawartości hello dysku. Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np. Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.

1. Wybierz grupę zasobów z hello portalu, a następnie wybierz rozwiązywania problemów z maszyny Wirtualnej. Wybierz **dysków** , a następnie kliknij przycisk **Attach istniejących**:

    ![Dołączanie istniejącego dysku w portalu hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect istniejącego wirtualnego dysku twardego, kliknij przycisk **pliku VHD**:

    ![Przeglądnie w poszukiwaniu istniejącego dysku VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Wybierz konto magazynu i kontener, a następnie kliknij istniejący dysk VHD. Kliknij przycisk hello **wybierz** przycisk tooconfirm wyboru:

    ![Wybieranie istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Teraz wybrać dysk VHD, kliknij polecenie **OK** tooattach hello istniejącego wirtualnego dysku twardego:

    ![Potwierdź dołączanie istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Po kilku sekundach hello **dysków** okienko dla maszyny Wirtualnej zawiera istniejącego wirtualnego dysku twardego połączenia jako dysk z danymi:

    ![Istniejący wirtualny dysk twardy dołączony jako dysk danych](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Zainstalować dysk dołączonych danych hello

1. Otwórz tooyour połączenia pulpitu zdalnego maszyny Wirtualnej. Wybierz maszyny Wirtualnej w portalu hello i kliknij przycisk **Connect**. Pobierz i Otwórz plik połączenia RDP hello. Wprowadź toolog Twoje poświadczenia w tooyour maszyny Wirtualnej w następujący sposób:

    ![Zaloguj się za tooyour maszyny Wirtualnej przy użyciu pulpitu zdalnego](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. Otwórz **Menedżera serwera**, a następnie wybierz pozycję **usług plików i magazynowania**. 

    ![Wybierz usługi plików i magazynowania w Menedżerze serwera](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. dysk z danymi Hello jest automatycznie wykryte i dołączony. toosee listę hello połączone dysków, wybierz **dysków**. Możesz wybrać dane danych dysku tooview zbiorczego, tym hello literę dysku. Witaj następujący przykład przedstawia hello podłączony dysk danych i przy użyciu **F:**:

    ![Dysk dołączony i informacji o woluminie w Menedżerze serwera](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Rozwiązywanie problemów na oryginalny wirtualny dysk twardy
Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami. Po ma problemu hello problemów, należy kontynuować hello następujące kroki.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy
Po rozwiązaniu błędy odłączyć hello istniejącego wirtualnego dysku twardego z rozwiązywania problemów z maszyny Wirtualnej. Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.

1. Z tooyour sesji protokołu RDP hello maszyny Wirtualnej, otwórz **Menedżera serwera**, a następnie wybierz pozycję **usług plików i magazynowania**:

    ![Wybierz usługi plików i magazynowania w Menedżerze serwera](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. Wybierz **dysków** , a następnie wybierz dysk danych. Kliknij prawym przyciskiem myszy na dysku danych, a następnie wybierz **Przełącz do trybu Offline**:

    ![Ustaw dysku danych hello jako w Menedżerze serwera w trybie offline](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. Teraz odłączyć hello wirtualnego dysku twardego z hello maszyny Wirtualnej. Wybierz maszyny Wirtualnej hello portalu Azure i kliknij przycisk **dysków**. Wybierz istniejącego wirtualnego dysku twardego, a następnie kliknij przycisk **Detach**:

    ![Odłącz istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Poczekaj, aż hello maszyna wirtualna została pomyślnie odłączono dysk danych hello przed kontynuowaniem.

## <a name="create-vm-from-original-hard-disk"></a>Tworzenie maszyny Wirtualnej z oryginalny dysk twardy
Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). Szablon Hello wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu hello adres URL dysku VHD z hello wcześniej polecenia. Kliknij przycisk hello **wdrażanie tooAzure** przycisku w następujący sposób:

![Wdrożenie maszyny Wirtualnej z szablonu z serwisu Github](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

Szablon Hello jest ładowany do hello portalu Azure do wdrożenia. Wprowadź hello nazwy dla nowej maszyny Wirtualnej i istniejących zasobów platformy Azure, a następnie wklej hello adresu URL tooyour istniejącego wirtualnego dysku twardego. toobegin hello wdrożenia, kliknij przycisk **zakupu**:

![Wdrożenie maszyny Wirtualnej z szablonu](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Włączyć ponownie diagnostykę rozruchu
Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone. toocheck hello stanu diagnostyki rozruchu i włączyć w razie potrzeby wybierz maszyny Wirtualnej w portalu hello. W obszarze **monitorowanie**, kliknij przycisk **ustawień diagnostycznych**. Upewnij się, jest w stanie hello **na**, i hello znacznik wyboru obok zbyt**diagnostyki rozruchu** jest zaznaczone. Jeśli wprowadzisz zmiany, kliknij przycisk **zapisać**:

![Aktualizowanie ustawień diagnostyki rozruchu](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [tooan połączenia RDP Rozwiązywanie problemów z maszyny Wirtualnej Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Aby uzyskać więcej informacji dotyczących korzystania z Menedżera zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).