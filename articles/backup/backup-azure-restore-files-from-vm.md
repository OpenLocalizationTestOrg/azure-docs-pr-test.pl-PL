---
title: "Kopia zapasowa Azure: Odzyskiwanie plików i folderów z kopii zapasowej maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Odzyskiwanie plików z punktu odzyskiwania maszyny wirtualnej platformy Azure"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "odzyskiwanie na poziomie elementu; odzyskiwanie plików z kopii zapasowej maszyny Wirtualnej platformy Azure. Przywróć pliki z maszyny Wirtualnej Azure"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: ae7c345c11a7db25413d60ad822f16f84ca37362
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Odzyskiwanie plików z kopii zapasowej maszyny wirtualnej platformy Azure

Kopia zapasowa Azure udostępnia możliwość przywracania [maszynach wirtualnych platformy Azure i dyski](./backup-azure-arm-restore-vms.md) z kopii zapasowych maszyny Wirtualnej platformy Azure. Teraz w tym artykule opisano, jak można odzyskać elementy, takie jak pliki i foldery z kopii zapasowej maszyny Wirtualnej platformy Azure.

> [!Note]
> Ta funkcja jest dostępna dla maszyn wirtualnych platformy Azure wdrażane za pomocą modelu usługi Resource Manager i chronione w magazynie usług odzyskiwania.
> Odzyskiwanie plików z zaszyfrowanej kopii zapasowej maszyny Wirtualnej nie jest obsługiwane.
>

## <a name="mount-the-volume-and-copy-files"></a>Zainstaluj woluminu i kopiować pliki

1. Zaloguj się do [Azure Portal](http://portal.Azure.com). Znajdź odpowiedniego magazynu usług odzyskiwania i wymagany element kopii zapasowej.

2. W bloku elementu kopii zapasowej, kliknij **odzyskiwanie plików**

    ![Otwórz element kopii zapasowej magazynu usług odzyskiwania](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    **Odzyskiwanie plików** zostanie otwarty blok.

    ![Blok odzyskiwania plików](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Z **wybierz punkt odzyskiwania** menu rozwijanego wybierz punkt odzyskiwania, który zawiera pliki. Domyślnie już jest wybrany najnowszy punkt odzyskiwania.

4. Kliknij przycisk **Pobierz plik wykonywalny** (dla systemu Windows Azure maszyny Wirtualnej) lub **Pobierz skrypt** (dla systemu Linux Azure VM) w celu pobrania oprogramowania, które będzie używane do kopiowania plików z punktu odzyskiwania.

  Skryptu lub pliku wykonywalnego tworzy połączenie między komputerem lokalnym a określony punkt odzyskiwania.

5. Wymagane jest hasło, aby uruchomić skrypt pobrany/plik wykonywalny. Hasło można skopiować z portalu, za pomocą przycisku Kopiuj obok wygenerowane hasło

    ![Wygenerowane hasło](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Na komputerze, na którym chcesz odzyskać pliki uruchamianie skryptu lub pliku wykonywalnego. Należy uruchomić je przy użyciu poświadczeń administratora. Jeśli skrypt zostanie uruchomiony na komputerze z ograniczonym dostępem, upewnij się, Brak dostępu do:

    - witrynie Download.microsoft.com
    - Punkty końcowe systemu Azure, używany do tworzenia kopii zapasowych maszyny Wirtualnej Azure
    - wychodzące port 3260

   Dla systemu Linux skrypt wymaga składników "open-iscsi" i "lshw" połączyć się z punktem odzyskiwania. Jeśli te nie istnieją na komputerze, na którym jest uruchomiony, poprosi o podanie uprawnień zainstalować odpowiednie składniki i instaluje je na zgody.
   
   Wprowadź hasło skopiowane z portalu po wyświetleniu monitu. Po wprowadzeniu prawidłowego hasła skrypty nawiązuje połączenie z punktem odzyskiwania.
      
    ![Blok odzyskiwania plików](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Skrypt można uruchomić na dowolnym komputerze, systemu operacyjnego tego samego (lub zgodne) jako kopii zapasowej maszyny Wirtualnej. Zobacz [tabeli zgodny system operacyjny](backup-azure-restore-files-from-vm.md#compatible-os) dla zgodnych systemów operacyjnych. Jeśli chronionej maszyny wirtualnej Azure korzysta z miejsca do magazynowania systemu Windows (w przypadku maszyn wirtualnych systemu Windows Azure) lub Arrays(for Linux VMs) LVM/RAID, nie można uruchomić skryptu lub pliku wykonywalnego w tej samej maszyny wirtualnej. Zamiast tego należy uruchomić ją na innym komputerze z zgodny system operacyjny.

### <a name="compatible-os"></a>Zgodny system operacyjny

#### <a name="for-windows"></a>Dla systemu Windows

W poniższej tabeli przedstawiono zgodność między systemami operacyjnymi serwera i komputera. Podczas odzyskiwania plików, nie można przywrócić plików między systemy operacyjne niezgodne.

|System operacyjny serwera | Zgodny system operacyjny klienta  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Dla systemu Linux

W systemie Linux podstawowe wymagane jest, że system operacyjny na komputerze, na którym skrypt jest uruchamiany powinna obsługiwać systemu plików występuje w maszyny Wirtualnej systemu Linux kopii zapasowej plików. Podczas wybierania maszyny, aby uruchomić skrypt, upewnij się, że ma zgodny system operacyjny i wersje wymienione w poniższej tabeli.

|System operacyjny Linux | Wersje  |
| --------------- | ---- |
| Ubuntu | 12.04 i powyżej. |
| CentOS | 6.5 i powyżej.  |
| RHEL | 6.7 i powyżej. |
| Debian | 7 i nowsze |
| Oracle Linux | 6.4 i powyżej. |

Skrypt wymaga również python i bash składników do wykonywania i bezpieczne łączenie z punktu odzyskiwania.

|Składnik | Wersja  |
| --------------- | ---- |
| Bash | 4 i nowsze |
| python | 2.6.6 i powyżej.  |


### <a name="identifying-volumes"></a>Identyfikowanie woluminów

#### <a name="for-windows"></a>Dla systemu Windows

Po uruchomieniu exectuable systemu operacyjnego instaluje nowe woluminy i przypisuje litery dysku. Eksplorator Windows lub w Eksploratorze plików można użyć do przeglądania tych dysków. Przypisane do woluminów litery dysków może nie być tych samych liter, co oryginalna maszyna wirtualna, jednak jest zachowywana nazwa woluminu. Na przykład, jeśli został woluminu na maszynie wirtualnej oryginalnego "dysk danych (E:\)", można dołączyć jako woluminu "dysk danych ("Wszystkie litery dysków dostępne":\) na komputerze lokalnym. Przeglądaj wszystkie woluminy wymienionych w danych wyjściowych skryptu do momentu znalezienia plików/folderów.  
       
   ![Blok odzyskiwania plików](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Dla systemu Linux

W systemie Linux woluminy punktu odzyskiwania są instalowane w folderze, w którym skrypt jest uruchamiany. W związku z tym są wyświetlane dołączonych dysków, woluminów i odpowiadające im ścieżki instalacji. Zainstaluj tych ścieżek są widoczne dla użytkowników mających dostęp na poziomie głównym. Przeglądaj woluminów wymienionych w danych wyjściowych skryptu.

  ![Blok odzyskiwania plików systemu Linux](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-the-connection"></a>Zamykanie połączenia

Po zidentyfikowaniu pliki i skopiować je do lokalizacji magazynu lokalnego, usunąć lub odinstalować dodatkowych dysków. Aby odinstalować dyski, na **odzyskiwanie plików** bloku w portalu Azure, kliknij przycisk **odinstalować dyski**.

![Odinstaluj dysków](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Gdy dyski zostały odinstalowane, pojawi się komunikat informujący o pomyślnym zakończeniu go. Może upłynąć kilka minut, aż połączenie w celu odświeżenia, aby usunąć dyski.

W systemie Linux, po jest Przerwano połączenie z punktem odzyskiwania, system operacyjny nie powoduje usunięcia odpowiednich ścieżkach instalacji automatycznie. Istnieją one jako woluminy "oddzielony" i są widoczne, ale zgłosić błąd, gdy użytkownik dostępu do zapisu plików. Można je ręcznie usunąć. Skrypt uruchamiania, identyfikuje wszelkie istniejące z poprzednich punktów odzyskiwania woluminy i czyści po zgody.

## <a name="special-configurations"></a>Konfiguracje specjalne

### <a name="dynamic-disks"></a>Dyski dynamiczne

Jeśli maszyny Wirtualnej platformy Azure, która została utworzona kopia zapasowa ma woluminy, które obejmują wiele dysków (łączone i woluminów rozłożonych) i/lub odpornej na uszkodzenia (woluminy dublowane i RAID-5) na dyskach dynamicznych, nie można uruchomić pliku wykonywalnego skryptu na tej samej maszyny Wirtualnej. Zamiast tego należy uruchomić pliku wykonywalnego skryptu na innym komputerze z zgodny system operacyjny.

### <a name="windows-storage-spaces"></a>Miejsca do magazynowania systemu Windows

Miejsca do magazynowania systemu Windows jest to technologia magazynu systemu Windows, który pozwala na wirtualizację magazynu. Z miejscami do magazynowania systemu Windows można grupowanie standardowych dysków w pule magazynu, a następnie tworzyć dyski wirtualne miejsca do magazynowania, z dostępnego miejsca w tych pul magazynów.

Jeśli maszyny Wirtualnej platformy Azure, która została utworzona kopia zapasowa korzysta z funkcji miejsca do magazynowania systemu Windows, nie można uruchomić pliku wykonywalnego skryptu na tej samej maszyny Wirtualnej. Zamiast tego należy uruchomić pliku wykonywalnego skryptu na innym komputerze z zgodny system operacyjny.

### <a name="lvmraid-arrays"></a>Tablice LVM/RAID

W systemie Linux Menedżer woluminów logicznych (LVM) i/lub oprogramowania macierze RAID są używane do zarządzania przez wiele dysków logicznych woluminów. Jeśli kopie zapasowe maszyny Wirtualnej systemu Linux używa LVM i/lub macierzy RAID, nie można uruchomić skrypt na tej samej maszyny Wirtualnej. Zamiast tego uruchomić skrypt na żadną inną maszynę z systemem operacyjnym zgodny i który obsługuje system plików kopii zapasowej maszyny wirtualnej.

Dane wyjściowe skryptu wyświetla dyski LVM i/lub macierzy RAID i woluminów o typie partycji, jak pokazano poniżej

   ![Blok danych wyjściowych LVM systemu Linux](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Następujące polecenia muszą być uruchamiane przez użytkownika, aby wyświetlić te partycje w trybie online. 

**W przypadku partycji LVM**

```
$ pvs <volume name as shown above in the script output> 
```
Ta lista zawiera nazwy grup woluminu w obszarze woluminu fizycznych.

```
$ lvdisplay <volume-group-name from the pvs command’s results> 
```
Ta lista zawiera wszystkie woluminy logiczne, nazwy i ich ścieżki w grupie woluminu.

```
$ mount <LV path> </mountpath>
```
Aby zainstalować logicznej woluminów na ścieżkę wybranych przez użytkownika.


**Dla macierzy RAID**

```
$ mdadm –detail –scan
```
Zostaną wyświetlone szczegółowe informacje o wszystkich dysków raid. Odpowiedni dysk RAID, które będą wyświetlane jako`/dev/mdm/<RAID array name in the backed up VM>`

Jeśli na dysku RAID woluminy fizyczne za pomocą polecenia instalacji.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Jeśli ten dysk RAID inny LVM skonfigurowane w nim postępuj zgodnie z procedurą w sposób opisany powyżej dla partycji LVM o nazwie woluminu RAID dysku nazwy

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli masz problemy podczas przywracania plików z maszyn wirtualnych Sprawdź poniższej tabeli, aby uzyskać dodatkowe informacje.

| Komunikat o błędzie / scenariusza | Prawdopodobna przyczyna | Zalecane działanie |
| ------------------------ | -------------- | ------------------ |
| Dane wyjściowe exe: *wyjątek łączenie się z obiektem docelowym* |Skrypt nie będzie mógł uzyskać dostępu do punktu odzyskiwania | Sprawdź, czy komputer spełnia wymagania dotyczące dostępu wymienionym powyżej|  
|   Dane wyjściowe exe: *element docelowy ma już zalogowany za pośrednictwem sesji ISCSI.* | Skrypt zostało już wykonane na tym samym komputerze, a dyski zostały dołączone | Już zostały dołączone woluminy punktu odzyskiwania. Mogą one nie można zainstalować z tych samych liter dysków oryginalnego maszyny wirtualnej. Przeglądaj wszystkie dostępne woluminy w Eksploratorze plików dla pliku |
| Dane wyjściowe exe: *tego skryptu jest nieprawidłowa, ponieważ dyski mają został odinstalowany przez 12 hr portal/przekroczył limit. Pobierz nowy skrypt z portalu.* |  Dyski mają został odinstalowany z portalu lub przekroczono limit 12 hr |    Tego konkretnego pliku exe teraz jest nieprawidłowy i nie można uruchomić. Jeśli chcesz uzyskać dostęp do plików tego odzyskiwania w momencie, odwiedź portal dla nowego pliku exe|
| Na komputerze, na którym uruchomiono pliku exe: nowe woluminy nie są odinstalowany po kliknięciu przycisku dezinstalacji |    Inicjator ISCSI na tym komputerze nie jest odpowiada/odświeżyć połączenie z docelowym i obsługi pamięci podręcznej |    Poczekaj kilka minut po naciśnięciu przycisku dezinstalacji. Jeśli nowe woluminy nadal są nie odinstalowana, przejdź do wszystkich woluminów. To zmusza inicjatora, aby odświeżyć połączenie i ten wolumin został odinstalowany z komunikatem o błędzie, że dysk nie jest dostępna|
| Dane wyjściowe exe: skrypt jest uruchamiany pomyślnie, ale "Nowe woluminy dołączony" nie jest wyświetlany w danych wyjściowych skryptu | Jest to przejściowy błąd   | Woluminy czy zostały już dołączone. Otwórz Eksploratora do przeglądania. Jeśli używasz tej samej maszyny do uruchamiania skryptów zawsze, rozważ ponowne uruchomienie komputera i listy powinien być wyświetlany w kolejnych exe uruchamia. |
| Właściwe dla systemu Linux: nie można wyświetlić żądanego woluminów | System operacyjny na komputerze, na którym skrypt jest uruchamiany nie może rozpoznać źródłowy system plików kopii zapasowej maszyny wirtualnej | Sprawdź, czy punkt odzyskiwania awaryjnego zgodne lub zgodne z plikami. Jeśli plik spójne, uruchom skrypt na innym komputerze których system operacyjny rozpoznaje kopię zapasową plików maszyny Wirtualnej |
| Właściwe dla systemu Windows: nie można wyświetlić żądanego woluminów | Dyski zostały dołączone, ale nie skonfigurowano woluminów | Na ekranie zarządzania dysku określenie dodatkowych dysków, powiązane z punktem odzyskiwania. Jeśli którykolwiek z tych dysków znajduje się w trybie offline stan spróbuj je w trybie online klikając prawym przyciskiem myszy na dysku i kliknij przycisk "Online"|
