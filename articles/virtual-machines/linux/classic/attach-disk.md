---
title: aaaAttach tooa dysku maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooattach danych na dysku tooa maszyny Wirtualnej systemu Linux przy użyciu hello Classic deployment model i Inicjowanie dysku hello gotowego do użycia"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Jak tooAttach tooa dysku danych maszyny wirtualnej systemu Linux
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Zobacz, jak za[dołączenie dysku danych przy użyciu modelu wdrażania usługi Resource Manager hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Możesz dołączyć zarówno puste dyski i dyski, które zawierają dane tooyour maszynach wirtualnych platformy Azure. Oba typy dysków są pliki VHD, które znajdują się na koncie magazynu platformy Azure. Jako dodawania maszyn Linux tooa dysku, po dołączeniu hello dysku można muszą tooinitialize i sformatuj go gotowego do użycia. Dołączanie zarówno puste dyski i zawierającej dane tooyour maszyn wirtualnych, a także jak toothen inicjowania i formatowania dysku nowego szczegółów tego artykułu.

> [!NOTE]
> Jest to najlepsze toouse rozwiązaniem, jeden lub więcej odrębnych toostore dysków danych maszyny wirtualnej. Podczas tworzenia maszyny wirtualnej platformy Azure ma dysk systemu operacyjnego i dysku tymczasowym. **Nie należy używać hello dysku tymczasowym toostore trwałych danych.** Jak wskazuje nazwę hello, zawiera tylko magazyn tymczasowy. Oferuje nie nadmiarowość lub kopii zapasowej, ponieważ go nie znajdują się w magazynie Azure.
> dysk tymczasowego Hello jest zazwyczaj zarządza hello Azure agenta systemu Linux i automatycznie instalowane za**/mnt/zasobu** (lub **katalogu/mnt** na obrazach Ubuntu). Na hello drugiej strony, dysku danych może być o nazwie jądra systemu Linux hello wyglądać mniej więcej tak `/dev/sdc`, i wymagają toopartition, formatowania i instalacji tego zasobu. Zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure] [ Agent] szczegółowe informacje.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Zainicjuj nowy dysk danych w systemie Linux
1. Tooyour SSH maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [jak toolog na tooa maszyny wirtualnej z systemem Linux][Logon].
2. Następnie wymagany identyfikator urządzenia hello toofind dla tooinitialize dysku danych hello. Istnieją dwa sposoby toodo który:
   
    ) Grep dla urządzeń SCSI w hello dzienniki, taki jak hello następujące polecenie:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Ostatnie dystrybucji Ubuntu, może być konieczne toouse `sudo grep SCSI /var/log/syslog` ponieważ rejestrowanie zbyt`/var/log/messages` mogą domyślnie wyłączone.
   
    Można znaleźć identyfikatora hello hello ostatnich danych dysku, który został dodany w wiadomości powitania, które są wyświetlane.
   
    ![Pobierz wiadomości powitania dysku](./media/attach-disk/scsidisklog.png)
   
    LUB
   
    (b) Użyj hello `lsscsi` toofind polecenia limit hello identyfikator urządzenia. `lsscsi` mogą być instalowane przez albo `yum install lsscsi` (Red Hat podstawę dystrybucje) lub `apt-get install lsscsi` (Debian podstawę dystrybucji). Można znaleźć dysku hello szukasz przez jego *lun* lub **numeru jednostki logicznej**. Na przykład Witaj *lun* dla dysków hello dołączony łatwo wynika z `azure vm disk list <virtual-machine>` jako:

    ```azurecli
    azure vm disk list myVM
    ```

    dane wyjściowe Hello są podobne toohello następujące czynności:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Porównaj te dane przy użyciu danych wyjściowych hello `lsscsi` dla hello samo przykładowe maszyny wirtualnej:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    numer ostatniej Hello w spójnej kolekcji hello w każdym wierszu jest hello *lun*. Zobacz `man lsscsi` Aby uzyskać więcej informacji.
3. Witaj, wpisz w wierszu hello następujące polecenia toocreate urządzenia:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Po wyświetleniu monitu wpisz  **n**  toocreate partycji.

    ![Utwórz urządzenie](./media/attach-disk/fdisknewpartition.png)

5. Po wyświetleniu monitu wpisz **p** partycji podstawowej hello toomake hello partycji. Typ **1** toomake hello pierwszej partycji, a następnie wpisz wprowadź wartość domyślną hello tooaccept hello cylinder. W niektórych systemach go Pokaż wartościami domyślnymi hello hello najpierw i hello ostatniego sektorów, zamiast hello cylinder. Możesz wybrać tooaccept tych wartości domyślnych.

    ![Tworzenie partycji](./media/attach-disk/fdisknewpartdetails.png)


6. Typ **p** toosee hello szczegóły hello dysku, który jest jest podzielona na partycje.

    ![Informacje o dyskach listy](./media/attach-disk/fdiskpartitiondetails.png)


7. Typ **w** toowrite ustawieniach hello hello dysku.

    ![Zapisz zmiany dysku hello](./media/attach-disk/fdiskwritedisk.png)

8. Teraz można tworzyć hello system plików na powitania nowej partycji. Dołącz identyfikator urządzenia toohello numer partycji hello (w hello poniższy przykład `/dev/sdc1`). Witaj poniższy przykład tworzy partycji ext4 /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Utworzyć systemu plików](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > SuSE Linux Enterprise 11 systemów obsługują tylko dostęp tylko do odczytu ext4 systemów plików. Dla tych systemów zaleca się tooformat hello nowy system plików jako ext3 zamiast ext4.

9. Wprowadź katalog toomount hello nowy system plików, w następujący sposób:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Na koniec hello dysk, można zainstalować w następujący sposób:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    dysk z danymi Hello jest teraz gotowy toouse jako **/datadrive**.
   
    ![Tworzenie dysku hello hello katalogu i instalacji](./media/attach-disk/mkdirandmount.png)

11. Dodaj hello nowego dysku zbyt/etc/fstab:
   
    dysk hello tooensure jest ponownej instalacji automatycznie po ponowny rozruch komputera musi być dodany plik /etc/fstab toohello. Ponadto zdecydowanie zaleca się, że ten hello UUID (powszechnie Unikatowy identyfikator) jest używany w /etc/fstab toorefer toohello dysku, a nie tylko hello nazwę urządzenia (tj. /dev/sdc1). Identyfikator UUID przy użyciu hello pozwala uniknąć dysku będzie nieprawidłowa hello jest zainstalowany tooa podanej lokalizacji, jeśli hello system operacyjny wykryje błąd dysku podczas rozruchu, a wszelkie pozostałe dyski danych są następnie przypisywane te identyfikatory urządzeń. toofind hello UUID hello nowego dysku, możesz użyć hello **blkid** narzędzie:
   
    ```bash
    sudo -i blkid
    ```
   
    Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Nieprawidłowo edycji hello **/etc/fstab** pliku może spowodować rozruch systemu. Jeśli nie wiesz, zapoznaj się z informacji w sposób tooproperly edytować ten plik dokumentacją toohello dystrybucji. Zalecane jest również, że kopia zapasowa pliku /etc/fstab hello został utworzony przed rozpoczęciem edycji.

    Następnie otwórz folder hello **/etc/fstab** plik w edytorze tekstu:

    ```bash
    sudo vi /etc/fstab
    ```

    W tym przykładzie używamy hello UUID wartość dla hello nowe **/dev/sdc1** urządzenia, który został utworzony w poprzednich krokach hello i hello punktu instalacji **/datadrive**. Dodaj wiersz toohello końca hello hello **/etc/fstab** pliku:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Lub na systemy oparte na systemie SuSE Linux może być konieczne toouse nieco inny format:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Witaj `nofail` opcja zapewnia, że hello maszyna wirtualna zacznie nawet wtedy, gdy system plików hello jest uszkodzony lub hello dysku nie istnieje w czasie rozruchu. Bez tej opcji, możesz napotkać zachowanie zgodnie z opisem w [nie SSH tooLinux maszyny Wirtualnej ze względu na błędy tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Teraz można sprawdzić, czy jest zainstalowany system plików hello prawidłowo odinstalowywania, a następnie woluminom hello systemu plików, np. przy użyciu punktu instalacji przykład hello `/datadrive` utworzone w hello wcześniej kroki:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Jeśli hello `mount` polecenie powoduje błąd, sprawdź plik hello/etc/fstab poprawną składnię. Jeśli dodatkowe dane dysków lub partycji są tworzone, wprowadź je w/etc/fstab także oddzielnie.

    Należy zapisu dysku hello za pomocą tego polecenia:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Następnie usunięcie dysku danych bez konieczności edytowania fstab może spowodować hello wirtualna toofail tooboot. Jeśli jest to często dochodzi, większości dystrybucji zapewniają albo hello `nofail` i/lub `nobootwait` fstab opcje, które umożliwiają tooboot systemu, nawet wtedy, gdy dysk hello toomount zakończy się niepowodzeniem w czasie rozruchu. Dokumentacja programu dystrybucji, aby uzyskać więcej informacji na temat tych parametrów.

### <a name="trimunmap-support-for-linux-in-azure"></a>PRZYCINANIE/UNMAP obsługę systemu Linux na platformie Azure
PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello. Operacje te są szczególnie przydatna w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone. Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.

Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux. W zwykły sposób poszukaj dystrybucji hello zalecane podejście:

* Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* W niektórych przypadkach hello `discard` opcji może mieć wpływ na wydajność. Alternatywnie można uruchomić hello `fstrim` ręcznie polecenie z wiersza polecenia hello, lub dodaj je tooyour crontab toorun regularnie:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Następne kroki
Więcej o korzystaniu z maszyny Wirtualnej systemu Linux w hello następujące artykuły:

* [Jak toolog na tooa maszyny wirtualnej z systemem Linux][Logon]
* [Jak toodetach dysku od maszyny wirtualnej systemu Linux](detach-disk.md)
* [Przy użyciu interfejsu wiersza polecenia Azure hello z hello klasycznego modelu wdrożenia](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Skonfiguruj RAID na maszynie Wirtualnej systemu Linux na platformie Azure](../configure-raid.md)
* [Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
