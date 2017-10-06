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
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Odzyskiwanie plików z kopii zapasowej maszyny wirtualnej platformy Azure

Kopia zapasowa Azure stanowi hello możliwości toorestore [maszynach wirtualnych platformy Azure i dyski](./backup-azure-arm-restore-vms.md) z kopii zapasowych maszyny Wirtualnej platformy Azure. Teraz w tym artykule opisano, jak można odzyskać elementy, takie jak pliki i foldery z kopii zapasowej maszyny Wirtualnej platformy Azure.

> [!Note]
> Ta funkcja jest dostępna dla maszyn wirtualnych Azure wdrażane za pomocą modelu usługi Resource Manager hello i chronionych tooa magazynu usług odzyskiwania.
> Odzyskiwanie plików z zaszyfrowanej kopii zapasowej maszyny Wirtualnej nie jest obsługiwane.
>

## <a name="mount-hello-volume-and-copy-files"></a>Zainstaluj hello woluminu i kopiować pliki

1. Zaloguj się na powitania [portalu Azure](http://portal.Azure.com). Znajdowanie hello odpowiedniego magazynu usług odzyskiwania i hello wymagany element kopii zapasowej.

2. W bloku kopia zapasowa elementu hello, kliknij **odzyskiwanie plików**

    ![Otwórz element kopii zapasowej magazynu usług odzyskiwania](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Witaj **odzyskiwanie plików** zostanie otwarty blok.

    ![Blok odzyskiwania plików](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Z hello **wybierz punkt odzyskiwania** menu rozwijanego, hello wybierz punkt odzyskiwania, który zawiera pliki hello ma. Domyślnie program hello najnowszy punkt odzyskiwania została już wybrana.

4. Kliknij przycisk **Pobierz plik wykonywalny** (dla systemu Windows Azure maszyny Wirtualnej) lub **Pobierz skrypt** (dla systemu Linux maszyny Wirtualnej platformy Azure) oprogramowania hello toodownload użyjesz toocopy pliki z punktu odzyskiwania hello.

  Witaj skryptu lub pliku wykonywalnego tworzy połączenie między hello komputera lokalnego i hello określony punkt odzyskiwania.

5. Należy hasła toorun hello pobrane skryptu/pliku wykonywalnego. Możesz skopiować hello hasła z portalu hello za pomocą przycisku Kopiuj hello obok hello wygenerowane hasło

    ![Wygenerowane hasło](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Na komputerze hello miejscu toorecover hello plików Uruchom hello skryptu lub pliku wykonywalnego. Należy uruchomić je przy użyciu poświadczeń administratora. Po uruchomieniu skryptu hello na komputerze z ograniczonym dostępem, upewnij się, Brak dostępu do:

    - witrynie Download.microsoft.com
    - Punkty końcowe systemu Azure, używany do tworzenia kopii zapasowych maszyny Wirtualnej Azure
    - wychodzące port 3260

   Dla systemu Linux, skrypt hello wymaga składników "open-iscsi" i "lshw" punkt odzyskiwania toohello tooconnect. Jeśli te nie istnieją na komputerze hello, w którym jest uruchomiony, prosi o uprawnienie tooinstall hello odpowiednie składniki i instaluje je na zgody.
   
   Wprowadź hasło hello skopiowany z portalu powitania po wyświetleniu monitu. Po wprowadzeniu prawidłowego hasła hello skrypty hello łączy toohello punktu odzyskiwania.
      
    ![Blok odzyskiwania plików](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Witaj skrypt można uruchomić na dowolnym komputerze, który zawiera system operacyjny hello tego samego (lub zgodne) w hello kopii zapasowej maszyny Wirtualnej. Zobacz hello [tabeli zgodny system operacyjny](backup-azure-restore-files-from-vm.md#compatible-os) dla zgodnych systemów operacyjnych. Jeśli hello chroniony wirtualnej platformy Azure jest używana maszyny miejsca do magazynowania systemu Windows (w przypadku maszyn wirtualnych systemu Windows Azure) lub Arrays(for Linux VMs) LVM/RAID, to nie można uruchomić skryptu lub pliku wykonywalnego hello na hello tej samej maszyny wirtualnej. Zamiast tego należy uruchomić ją na innym komputerze z zgodny system operacyjny.

### <a name="compatible-os"></a>Zgodny system operacyjny

#### <a name="for-windows"></a>Dla systemu Windows

Witaj, w następującej tabeli przedstawiono hello zgodności między systemami operacyjnymi serwera i komputera. Podczas odzyskiwania plików, nie można przywrócić plików między systemy operacyjne niezgodne.

|System operacyjny serwera | Zgodny system operacyjny klienta  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Dla systemu Linux

W systemie Linux, podstawowy wymóg hello jest hello tego systemu operacyjnego maszyny hello gdzie hello skrypt jest uruchamiany powinna obsługiwać hello filesystem z hello w hello pliki kopii zapasowej maszyny Wirtualnej systemu Linux. Podczas wybierania skryptu hello toorun maszyny, upewnij się, że ma niezgodne wersje systemu operacyjnego i hello hello wymienionych w poniższej tabeli hello.

|System operacyjny Linux | Wersje  |
| --------------- | ---- |
| Ubuntu | 12.04 i powyżej. |
| CentOS | 6.5 i powyżej.  |
| RHEL | 6.7 i powyżej. |
| Debian | 7 i nowsze |
| Oracle Linux | 6.4 i powyżej. |

skrypt Hello również wymaga python i bash tooexecute składników i bezpieczne łączenie toohello punktu odzyskiwania.

|Składnik | Wersja  |
| --------------- | ---- |
| Bash | 4 i nowsze |
| python | 2.6.6 i powyżej.  |


### <a name="identifying-volumes"></a>Identyfikowanie woluminów

#### <a name="for-windows"></a>Dla systemu Windows

Po uruchomieniu hello exectuable systemu operacyjnego hello instaluje hello nowe woluminy i przypisuje litery dysku. Eksplorator Windows lub w Eksploratorze plików toobrowse można używać tych dysków. Hello przypisane woluminów toohello litery dysków mogą nie być powitalne tych samych liter jak hello oryginalna maszyna wirtualna, jednak hello nazwa woluminu jest zachowywana. Na przykład, jeśli hello woluminu na powitania oryginalna maszyna wirtualna została "dysk danych (E:\)", można dołączyć jako woluminu "dysk danych ("Wszystkie litery dysków dostępne":\) hello komputera lokalnego. Przeglądaj wszystkie woluminy wymienionych w danych wyjściowych skryptu hello do momentu znalezienia plików/folderów.  
       
   ![Blok odzyskiwania plików](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Dla systemu Linux

W systemie Linux powitania woluminy punktu odzyskiwania hello są toohello zainstalowanego folderu, gdzie hello skrypt jest uruchamiany. Witaj dołączonych dysków, woluminów i instalowania odpowiedniej hello ścieżki są wyświetlane odpowiednio. Zainstaluj tych ścieżek są widoczne toousers mające dostęp na poziomie głównym. Przeglądaj woluminów hello wymienionych w danych wyjściowych skryptu hello.

  ![Blok odzyskiwania plików systemu Linux](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Zamykanie połączenia hello

Po zidentyfikowaniu hello plików i ich kopiowanie tooa lokalizacji magazynu lokalnego, usunąć lub odinstalować hello dodatkowych dysków. toounmount hello dysków, na powitania **odzyskiwanie plików** bloku w hello portalu Azure, kliknij przycisk **odinstalować dyski**.

![Odinstaluj dysków](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Po hello dyski zostały odinstalowane, pojawi się komunikat informujący o pomyślnym zakończeniu go. Tak, aby usunąć dyski hello może potrwać kilka minut, aż hello toorefresh połączenia.

W systemie Linux, po punkt odzyskiwania toohello połączenia hello jest Przerwano, hello systemu operacyjnego nie powoduje usunięcia hello odpowiadające im ścieżki instalacji automatycznie. Istnieją one jako woluminy "oddzielony" i są widoczne, ale zgłoszenie błędu, gdy użytkownik dostępu i zapisu plików hello. Można je ręcznie usunąć. skrypt Hello, uruchamiania, identyfikuje wszelkie istniejące z poprzednich punktów odzyskiwania woluminy i czyści po zgody.

## <a name="special-configurations"></a>Konfiguracje specjalne

### <a name="dynamic-disks"></a>Dyski dynamiczne

Jeśli hello maszyny Wirtualnej platformy Azure, która została utworzona kopia zapasowa ma woluminów obejmujących wiele dysków (woluminy łączone i rozłożone) i/lub odpornej na uszkodzenia (woluminy dublowane i RAID-5) w przypadku dysków dynamicznych nie można uruchomić pliku wykonywalnego skryptu hello na hello tej samej maszyny Wirtualnej. Zamiast tego należy uruchomić skrypt wykonywalnego hello na innym komputerze z zgodny system operacyjny.

### <a name="windows-storage-spaces"></a>Miejsca do magazynowania systemu Windows

Miejsca do magazynowania systemu Windows jest to technologia magazynu systemu Windows, który pozwala toovirtualize magazynu. Z miejscami do magazynowania systemu Windows można grupowanie standardowych dysków w pule magazynu, a następnie tworzyć dyski wirtualne miejsca do magazynowania, z hello dostępnego miejsca w tych pul magazynów.

Jeśli hello maszyny Wirtualnej platformy Azure, która została utworzona kopia zapasowa używa funkcji miejsca do magazynowania systemu Windows, a następnie hello wykonywalnego skryptu nie można uruchomić na hello tej samej maszyny Wirtualnej. Zamiast tego należy uruchomić skrypt wykonywalnego hello na innym komputerze z zgodny system operacyjny.

### <a name="lvmraid-arrays"></a>Tablice LVM/RAID

W systemie Linux, Menedżer woluminów logicznych (LVM) i/lub oprogramowania macierzy RAID są woluminy logiczne toomanage używane przez wiele dysków. Jeśli hello kopii zapasowej maszyny Wirtualnej systemu Linux używa LVM i/lub macierzy RAID, nie można uruchomić skryptu hello na powitania tej samej maszyny Wirtualnej. Zamiast tego uruchomić skrypt hello na żadną inną maszynę z systemem operacyjnym zgodny i który obsługuje filesystem hello kopii zapasowej maszyny Wirtualnej.

Wyświetla dane wyjściowe skryptu Hello hello LVM i/lub macierzy RAID dyski i woluminy hello hello typu partycji, jak pokazano poniżej

   ![Blok danych wyjściowych LVM systemu Linux](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Witaj następujące polecenia, toobe uruchomić przez toobring użytkownika hello tych partycji w trybie online. 

**W przypadku partycji LVM**

```
$ pvs <volume name as shown above in hello script output> 
```
Ta lista zawiera nazwy grupy woluminów hello w woluminie fizycznym.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Ta lista zawiera wszystkie woluminy logiczne, nazwy i ich ścieżki w grupie woluminu.

```
$ mount <LV path> </mountpath>
```
toomount hello woluminy logiczne toohello ścieżka wybranych przez użytkownika.


**Dla macierzy RAID**

```
$ mdadm –detail –scan
```
Zostaną wyświetlone szczegółowe informacje o wszystkich dysków raid. odpowiedni dysk RAID Hello będą wyświetlane jako`/dev/mdm/<RAID array name in hello backed up VM>`

Jeśli na dysku RAID hello woluminy fizyczne, należy użyć polecenia instalacji hello.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Jeśli ten dysk RAID inny LVM skonfigurowane w nim postępuj hello tej samej procedury, zgodnie z powyższym LVM partycji o nazwie woluminu hello hello nazwy dysku RAID

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli masz problemy podczas przywracania plików z maszyn wirtualnych hello Sprawdź hello w poniższej tabeli, aby uzyskać dodatkowe informacje.

| Komunikat o błędzie / scenariusza | Prawdopodobna przyczyna | Zalecane działanie |
| ------------------------ | -------------- | ------------------ |
| Dane wyjściowe exe: *wyjątek łączenie toohello docelowego* |Skrypt nie jest punkt odzyskiwania może tooaccess hello | Sprawdź, czy maszyna hello spełnia wymagania dotyczące dostępu hello wymienione powyżej|  
|   Dane wyjściowe exe: *hello docelowy ma już zalogowany za pośrednictwem sesji ISCSI.* |   skrypt Hello już zostało wykonane na powitalne tego samego komputera i hello dyski zostały dołączone |   już zostały dołączone woluminy Hello hello punktu odzyskiwania. NIE mogą one zainstalowane z hello sam dysk liter hello oryginalna maszyna wirtualna. Przeglądanie wszystkich dostępnych woluminów hello w Eksploratorze plików hello pliku |
| Dane wyjściowe exe: *tego skryptu jest nieprawidłowa, ponieważ dyski hello ma został odinstalowany przez hello portal/przekroczyła limit 12 hr. Pobierz nowy skrypt z hello portalu.* |    dyski Hello ma został odinstalowany z portalu hello lub przekroczono limit 12 hr hello |  Tego konkretnego pliku exe teraz jest nieprawidłowy i nie można uruchomić. Jeśli chcesz się, że tooaccess hello pliki tego odzyskiwania w momencie, odwiedź portal powitania dla nowego pliku exe|
| Na komputerze hello, w którym uruchomiono hello exe: hello nowe woluminy nie są odinstalowany po kliknięciu przycisku dismount hello |    Hello inicjatora ISCSI na maszynie hello nie jest elementem docelowym toohello połączenia odpowiada/odświeżanie i obsługi pamięci podręcznej hello |    Poczekaj kilka minut po naciśnięciu przycisku dismount hello. Jeśli hello nowe woluminy nadal są nie odinstalowana, przejdź do wszystkich woluminów hello. Ten wymusza, który hello inicjatora toorefresh hello połączenia i hello wolumin został odinstalowany z komunikatem o błędzie które hello dysku nie jest dostępna|
| Dane wyjściowe exe: skrypt jest uruchamiany pomyślnie, ale "Nowe woluminy dołączony" nie jest wyświetlany w danych wyjściowych skryptu hello |   Jest to przejściowy błąd   | woluminy Hello czy zostały już dołączone. Otwórz Eksploratora toobrowse. Jeśli używasz hello sam maszyny do uruchamiania skryptów zawsze, rozważ ponowne uruchomienie komputera hello i ma być wyświetlana lista hello w hello kolejnych exe uruchamia. |
| Właściwe dla systemu Linux: hello nie jest w stanie tooview żądanego woluminów | Witaj systemu operacyjnego maszyny hello gdzie hello skrypt jest uruchamiany nie może rozpoznać hello źródłowy system plików z hello kopii zapasowej maszyny Wirtualnej | Sprawdź, czy punkt odzyskiwania hello jest awarii zgodne lub zgodne z plikami. Jeśli skrypt hello spójne, uruchom plik na innym komputerze, w których system operacyjny rozpoznaje hello kopię zapasową plików maszyny Wirtualnej |
| Właściwe dla systemu Windows: hello nie jest w stanie tooview żądanego woluminów | może dołączone dyski Hello, ale woluminów hello nie zostały skonfigurowane. | Z ekranu zarządzania dysku hello Zidentyfikuj punktu odzyskiwania powiązanego toohello dodatkowych dysków hello. Jeśli którykolwiek z tych dysków znajduje się w trybie offline stan spróbuj je w trybie online klikając prawym przyciskiem myszy na powitania dysku, a następnie kliknij przycisk "Online"|
