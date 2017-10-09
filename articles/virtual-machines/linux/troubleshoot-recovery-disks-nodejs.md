---
title: "aaaUse a Linux Rozwiązywanie problemów dotyczących maszyny Wirtualnej z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot, korzystając z połączenia hello systemu operacyjnego dysku tooa odzyskiwania maszyny Wirtualnej przez maszyny Wirtualnej systemu Linux hello Azure CLI w wersji 1.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Rozwiązywanie problemów z maszyny Wirtualnej systemu Linux, dołączając hello systemu operacyjnego maszyny Wirtualnej odzyskiwania tooa dysku przy użyciu hello Azure CLI w wersji 1.0
Jeśli maszyny wirtualnej systemu Linux (VM) napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów. Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab` który zapobiega hello maszyna wirtualna stanie tooboot pomyślnie. Szczegóły tego artykułu jak toouse hello Azure CLI 1.0 tooconnect wirtualnej twarde błędy tooanother toofix maszyny Wirtualnej systemu Linux na dysku, a następnie ponownie utworzyć oryginalnego maszyny Wirtualnej.


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#recovery-process-overview) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="recovery-process-overview"></a>Omówienie procesu odzyskiwania
proces rozwiązywania problemów Hello jest następujący:

1. Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.
2. Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Linux na potrzeby rozwiązywania problemów.
3. Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej. Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.
4. Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.
5. Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.

Upewnij się, że masz [hello najnowsze Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowany i rejestrowane w trybie Menedżera zasobów:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.


## <a name="determine-boot-issues"></a>Określenie zagadnień rozruchu
Sprawdź, czy toodetermine serial dane wyjściowe hello Dlaczego maszyny Wirtualnej nie jest możliwe tooboot poprawnie. Typowym przykładem jest nieprawidłowy wpis w `/etc/fstab`, lub hello podstawowy wirtualny dysk twardy jest usunięty lub przeniesiony.

Witaj poniższy przykład pobiera dane wyjściowe serial hello z hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Przejrzyj toodetermine serial dane wyjściowe hello Dlaczego hello maszyny Wirtualnej kończy się niepowodzeniem tooboot. Jeśli hello serial danych wyjściowych nie jest zapewnienie oznaczenie, może być konieczne tooreview pliki dziennika w `/var/log` po utworzeniu hello wirtualny dysk twardy podłączony tooa Rozwiązywanie problemów z maszyny Wirtualnej.


## <a name="view-existing-virtual-hard-disk-details"></a>Szczegóły istniejącego wirtualnego dysku twardego
Przed dołączeniem tooanother Twojego wirtualnego dysku twardego maszyny Wirtualnej, potrzebna jest nazwa hello tooidentify hello wirtualnego dysku twardego (VHD). 

Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Wyszukaj `Vhd URI` w danych wyjściowych hello z hello poprzedzających polecenia. Witaj skróconą przykładowe dane wyjściowe wyglądają następująco hello `Vhd URI` hello ostatniego wiersza:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Usuń istniejącą maszynę Wirtualną
Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure. Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje. Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC). Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej. Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta. dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.

pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie. Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu. Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.

powitania po usuwaniu przykład Witaj maszyny Wirtualnej o nazwie `myVM` z hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej. dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej
Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów. Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse maszyny Wirtualnej i edytowania zawartości hello dysku. Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np. Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.

Po dołączeniu istniejącego wirtualnego dysku twardego hello, określ dysk toohello adres URL hello uzyskanych w poprzednim hello `azure vm show` polecenia. Witaj poniższy przykład dołącza istniejących toohello wirtualnego dysku twardego, rozwiązywanie problemów z maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Zainstalować dysk dołączonych danych hello

> [!NOTE]
> Witaj następujące przykłady szczegółowo opisano czynności hello maszyny Wirtualnej systemu Ubuntu. Jeśli używasz różnych distro Linux, takich jak Red Hat Enterprise Linux i SUSE, hello lokalizacje plików dziennika i `mount` poleceń mogą być nieco inne. Zapoznaj się z dokumentacją toohello dla Twojego distro określonych dla hello odpowiednie zmiany w poleceniach.

1. Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń hello tooyour SSH. Jeśli dysk jest hello pierwszy danych dysk dołączony tooyour Rozwiązywanie problemów z maszyny Wirtualnej, dysk hello jest prawdopodobnie zbyt podłączony`/dev/sdc`. Użyj `dmseg` tooview dołączone dyski:

    ```bash
    dmesg | grep SCSI
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    W hello poprzedzających przykład, dysk systemu operacyjnego hello jest na `/dev/sda` i hello dysku tymczasowym podana dla każdej maszyny Wirtualnej jest w `/dev/sdb`. Jeśli masz wiele dysków z danymi, należy je na `/dev/sdd`, `/dev/sde`i tak dalej.

2. Utwórz toomount katalogu istniejącego wirtualnego dysku twardego. Witaj poniższy przykład tworzy katalog o nazwie `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Jeśli masz wiele partycji na istniejącego wirtualnego dysku twardego, zainstaluj hello wymagane partycji. Witaj poniższy przykład instaluje hello pierwszej partycji podstawowej na `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Najlepszym rozwiązaniem jest toomount dysków danych na maszynach wirtualnych platformy Azure przy użyciu hello unikatowym identyfikatorem (UUID) hello wirtualnego dysku twardego. W przypadku tego scenariusza rozwiązywania problemów z krótkim instalowanie hello wirtualny dysk twardy za pomocą hello UUID nie jest konieczne. Jednak w ramach normalnego użytkowania edycji `/etc/fstab` toomount wirtualnych dysków twardych za pomocą nazwy urządzenia, a nie może spowodować UUID hello tooboot toofail maszyny Wirtualnej.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Rozwiązywanie problemów na oryginalny wirtualny dysk twardy
Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami. Po ma problemu hello problemów, należy kontynuować hello następujące kroki.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy
Po rozwiązaniu błędy, odinstaluj i odłączyć istniejącego wirtualnego dysku twardego hello rozwiązywania problemów z maszyny Wirtualnej. Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.

1. Z tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej należy odinstalować istniejącego wirtualnego dysku twardego hello. Najpierw zmienić poza hello katalogu nadrzędnego punktu instalacji:

    ```bash
    cd /
    ```

    Teraz należy odinstalować istniejącego wirtualnego dysku twardego hello. Witaj poniższy przykład odinstalowuje hello urządzenie pod adresem `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Teraz odłączyć hello wirtualnego dysku twardego z hello maszyny Wirtualnej. Zamknij tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej. W hello Azure CLI pierwszy hello listy dołączony tooyour dysków danych Rozwiązywanie problemów z maszyny Wirtualnej. Witaj poniższy przykład list hello dysków z danymi dołączony toohello maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Uwaga hello `Lun` wartość dla istniejącego wirtualnego dysku twardego. Witaj następujące przykładowe dane wyjściowe polecenia przedstawia hello istniejącego wirtualnego dysku znajduje się w jednostce LUN 0:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Odłączyć dysku danych powitania od maszyny Wirtualnej przy użyciu odpowiednich hello `Lun` wartość:

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Tworzenie maszyny Wirtualnej z oryginalny dysk twardy
Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). Witaj rzeczywiste JSON szablonu jest w hello następujące łącze:

- https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD/azuredeploy.JSON

Szablon Hello wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu hello adres URL dysku VHD z hello wcześniej polecenia. Witaj poniższy przykład wdraża hello szablonu toohello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Hello odpowiedzi wyświetla monit dotyczący hello szablonu, takie jak nazwa maszyny Wirtualnej (`myDeployedVM` hello następujący przykład), typ systemu operacyjnego (`Linux`), a rozmiar maszyny Wirtualnej (`Standard_DS1_v2`). Witaj `osDiskVhdUri` jest hello takie same jak wcześniej używane podczas podłączania hello istniejącego wirtualnego dysku twardego toohello Rozwiązywanie problemów z maszyny Wirtualnej. Przykład danych wyjściowych polecenia hello i wyświetla monit jest następujący:

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Włączyć ponownie diagnostykę rozruchu

Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone. Witaj poniższy przykład umożliwia włączenie rozszerzenia diagnostycznych hello na powitania maszyny Wirtualnej o nazwie `myDeployedVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [Rozwiązywanie problemów z SSH połączeń tooan maszyny Wirtualnej Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej systemu Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
