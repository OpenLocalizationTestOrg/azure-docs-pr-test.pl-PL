---
title: "aaaReset lokalne hasło systemu Windows bez agenta platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak tooreset hello hasła lokalnego konta użytkownika systemu Windows, gdy agent gościa Azure hello nie jest zainstalowany i działa na maszynie Wirtualnej"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Jak tooreset lokalnego hasła systemu Windows dla maszyny Wirtualnej Azure
Można zresetować hasła lokalnego systemu Windows hello maszyny wirtualnej na platformie Azure przy użyciu hello [portalu Azure lub programu Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pod warunkiem hello Azure gościa agent jest zainstalowany. Ta metoda jest hello podstawowy sposób tooreset hasła dla maszyny Wirtualnej platformy Azure. Jeśli wystąpią problemy z hello Azure gościa agent nie odpowiada, lub niepowodzeniem tooinstall po przekazaniu niestandardowego obrazu, można ręcznie zresetować hasło systemu Windows. W tym artykule szczegółowo sposób tooreset hasła konta lokalnego, dołączając hello tooanother wirtualnego dysku systemu operacyjnego źródłowej maszyny Wirtualnej. 

> [!WARNING]
> Ten proces można używać tylko w ostateczności. Zawsze spróbuj tooreset hasło za pomocą hello [portalu Azure lub programu Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pierwszy.
> 
> 

## <a name="overview-of-hello-process"></a>Omówienie procesu hello
Witaj podstawowych kroków resetowania dla maszyny Wirtualnej systemu Windows na platformie Azure, gdy brak dostępu agenta gościa Azure toohello hasła lokalnego jest następujący:

* Usuń hello źródłowej maszyny Wirtualnej. dyski wirtualne Hello są zachowywane.
* Dołącz tooanother dysku systemu operacyjnego hello źródłowej maszyny Wirtualnej VM na powitania tej samej lokalizacji, w ramach Twojej subskrypcji platformy Azure. Ta maszyna wirtualna jest hello tooas określonego Rozwiązywanie problemów z maszyny Wirtualnej.
* Za pomocą hello Rozwiązywanie problemów z maszyny Wirtualnej, Utwórz niektóre pliki konfiguracji na dysku systemu operacyjnego hello źródłowej maszyny Wirtualnej.
* Odłączanie dysku systemu operacyjnego hello maszyny Wirtualnej z hello Rozwiązywanie problemów z maszyny Wirtualnej.
* Użyj Menedżera zasobów toocreate szablonu maszyny Wirtualnej za pomocą hello oryginalny dysk wirtualny.
* Witaj Uruchamianie nowej maszyny Wirtualnej, hello plików konfiguracji powoduje utworzenie aktualizacji hello hasła użytkownika hello wymagane.

## <a name="detailed-steps"></a>Szczegółowe procedury
Zawsze spróbuj tooreset hasło za pomocą hello [portalu Azure lub programu Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed podjęciem próby hello następujące kroki. Upewnij się, że masz kopię zapasową maszyny wirtualnej, przed rozpoczęciem. 

1. Usuń hello dotyczy maszyny Wirtualnej w portalu Azure. Hello usuwania maszyny Wirtualnej usuwa tylko metadane hello, odwołanie hello hello maszyny Wirtualnej na platformie Azure. dyski wirtualne Hello są zachowywane po usunięciu hello maszyny Wirtualnej:
   
   * Wybierz hello maszyny Wirtualnej w hello portalu Azure, kliknij przycisk *usunąć*:
     
     ![Usuń istniejącą maszynę Wirtualną](./media/reset-local-password-without-agent/delete_vm.png)
2. Dołącz toohello dysku systemu operacyjnego hello źródła wirtualna Rozwiązywanie problemów z maszyny Wirtualnej. Witaj, rozwiązywanie problemów z maszyny Wirtualnej musi być w hello tym samym regionie co dysk systemu operacyjnego hello źródłowej maszyny Wirtualnej (takie jak `West US`):
   
   * Wybierz hello Rozwiązywanie problemów z maszyny Wirtualnej w hello portalu Azure. Kliknij przycisk *dysków* | *Attach istniejących*:
     
     ![Dołączanie istniejącego dysku](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Wybierz *pliku VHD* , a następnie wybierz konto magazynu hello, która zawiera źródło maszyny Wirtualnej:
     
     ![Wybieranie konta magazynu](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Wybierz kontener źródła hello. kontener źródła Hello jest zwykle *wirtualne dyski twarde*:
     
     ![Wybierz kontener magazynu](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Wybierz hello tooattach wirtualnego dysku twardego systemu operacyjnego. Kliknij przycisk *wybierz* toocomplete hello proces:
     
     ![Wybierz wirtualny dysk źródłowy](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu pulpitu zdalnego i upewnij się, że dysk systemu operacyjnego hello źródłowej maszyny Wirtualnej jest widoczna:
   
   * Wybierz hello Rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure hello i kliknij przycisk *Connect*.
   * Otwórz plik RDP hello pliki do pobrania. Wprowadź hello użytkownika i hasło hello Rozwiązywanie problemów z maszyny Wirtualnej.
   * W Eksploratorze plików poszukaj dysku danych hello podłączony. Witaj źródło maszyny Wirtualnej wirtualny dysk twardy jest hello toohello dysku tylko dane Rozwiązywanie problemów z maszyny Wirtualnej, należy hello F: dysku:
     
     ![Wyświetlanie dysków dołączonych danych](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Utwórz `gpt.ini` w `\Windows\System32\GroupPolicy` na dysku hello źródłowej maszyny Wirtualnej (jeśli istnieje gpt.ini, Zmień nazwę toogpt.ini.bak):
   
   > [!WARNING]
   > Upewnij się, możesz przypadkowo utworzyć hello następujące pliki w C:\Windows, hello dysku systemu operacyjnego hello Rozwiązywanie problemów z maszyny Wirtualnej. Utwórz hello następujące pliki w stacji hello systemu operacyjnego dla maszyny Wirtualnej, który jest dołączony jako dysk danych źródła.
   > 
   > 
   
   * Dodaj następujące wiersze do hello hello `gpt.ini` utworzony plik:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Utwórz gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Utwórz `scripts.ini` w `\Windows\System32\GroupPolicy\Machine\Scripts`. Upewnij się, że są wyświetlane w folderach ukrytych. W razie potrzeby utwórz hello `Machine` lub `Scripts` folderów.
   
   * Dodaj następujące wiersze hello hello `scripts.ini` utworzony plik:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Utwórz scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Utwórz `FixAzureVM.cmd` w `\Windows\System32` z powitania po zawartości, zastępując `<username>` i `<newpassword>` z własne wartości:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Utwórz FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Podczas definiowania hello nowe hasło, musi spełniać wymagania dotyczące złożoności hasła hello skonfigurowane dla maszyny Wirtualnej.
7. W portalu Azure odłączyć dysku powitania od hello Rozwiązywanie problemów z maszyny Wirtualnej:
   
   * Kliknij pozycję Wybierz hello Rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure hello *dysków*.
   * Wybierz hello danych dysk dołączony w kroku 2, kliknij przycisk *Detach*:
     
     ![Odłączanie dysku](./media/reset-local-password-without-agent/detach_disk.png)
8. Przed utworzeniem maszyny Wirtualnej, należy uzyskać dysk systemu operacyjnego źródłowej tooyour URI hello:
   
   * Wybierz hello konta magazynu w hello portalu Azure, kliknij przycisk *obiekty BLOB*.
   * Wybierz kontener hello. kontener źródła Hello jest zwykle *wirtualne dyski twarde*:
     
     ![Wybierz obiekt blob z konta magazynu](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Wybierz źródło wirtualnego dysku twardego systemu operacyjnego maszyny Wirtualnej, a następnie kliknij przycisk hello *kopiowania* przycisku Dalej toohello *adres URL* nazwy:
     
     ![Skopiuj identyfikator URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Tworzenie maszyny Wirtualnej z dysku systemu operacyjnego hello źródłowej maszyny Wirtualnej:
   
   * Użyj [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate maszyny Wirtualnej z dysku VHD specjalne. Kliknij przycisk hello `Deploy tooAzure` przycisk tooopen hello portalu Azure przy użyciu szczegółów opartego na szablonie hello wypełnione.
   * Jeśli chcesz tooretain wszystkich poprzednich ustawień hello hello maszyny Wirtualnej, wybierz opcję *Edytuj szablon* tooprovide istniejącej sieci wirtualnej, podsieci, karty sieciowej lub publicznego adresu IP.
   * W hello `OSDISKVHDURI` parametru pola tekstowego, Wklej hello uzyskać identyfikator URI dysku VHD źródła w hello poprzedzających krok:
     
     ![Utwórz maszynę Wirtualną z szablonu](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Po hello nowa maszyna wirtualna jest uruchomiona, należy połączyć toohello maszyny Wirtualnej przy użyciu pulpitu zdalnego z nowego hasła hello określone w hello `FixAzureVM.cmd` skryptu.
11. Z toohello Twojego sesji zdalnej nowej maszyny Wirtualnej, hello Usuń następujące pliki tooclean hello środowiska:
    
    * Z %windir%\System32
      * Usuń FixAzureVM.cmd
    * Z %windir%\System32\GroupPolicy\Machine\
      * Usuń scripts.ini
    * Z %windir%\System32\GroupPolicy
      * Usuń gpt.ini (jeśli istniał gpt.ini wcześniej i zmieniona toogpt.ini.bak, toogpt.ini wstecz Plik bak hello zmiany nazwy)

## <a name="next-steps"></a>Następne kroki
Jeśli nadal nie możesz połączyć przy użyciu pulpitu zdalnego, zobacz hello [przewodnik rozwiązywania problemów RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Witaj [szczegółowy przewodnik rozwiązywania problemów RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) analizuje Rozwiązywanie problemów z metody zamiast wykonania określonych kroków. Możesz również [otwarcia żądania pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) praktyczne pomocy.

