---
title: "aaaUse a Rozwiązywanie problemów dotyczących maszyny Wirtualnej z hello Azure CLI 2.0 w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot, korzystając z połączenia hello systemu operacyjnego dysku tooa odzyskiwania maszyny Wirtualnej przez maszyny Wirtualnej systemu Linux hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Rozwiązywanie problemów z maszyny Wirtualnej systemu Linux, dołączając odzyskiwanie tooa dysku hello systemu operacyjnego maszyny Wirtualnej z hello Azure CLI 2.0
Jeśli maszyny wirtualnej systemu Linux (VM) napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów. Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab` który zapobiega hello maszyna wirtualna stanie tooboot pomyślnie. Szczegóły tego artykułu jak toouse hello Azure CLI 2.0 tooconnect wirtualnej twarde błędy tooanother toofix maszyny Wirtualnej systemu Linux na dysku, a następnie ponownie utworzyć oryginalnego maszyny Wirtualnej. Można również wykonać te kroki hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Omówienie procesu odzyskiwania
proces rozwiązywania problemów Hello jest następujący:

1. Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.
2. Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Linux na potrzeby rozwiązywania problemów.
3. Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej. Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.
4. Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.
5. Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.

tooperform następujące czynności, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.


## <a name="determine-boot-issues"></a>Określenie zagadnień rozruchu
Sprawdź, czy toodetermine serial dane wyjściowe hello Dlaczego maszyny Wirtualnej nie jest możliwe tooboot poprawnie. Typowym przykładem jest nieprawidłowy wpis w `/etc/fstab`, lub hello podstawowy wirtualny dysk twardy jest usunięty lub przeniesiony.

Pobierz dzienniki rozruchu hello z [az maszyny wirtualnej diagnostyki rozruchu get rozruchu dziennika](/cli/azure/vm/boot-diagnostics#get-boot-log). Witaj poniższy przykład pobiera dane wyjściowe serial hello z hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Przejrzyj toodetermine serial dane wyjściowe hello Dlaczego hello maszyny Wirtualnej kończy się niepowodzeniem tooboot. Jeśli hello serial danych wyjściowych nie jest zapewnienie oznaczenie, może być konieczne tooreview pliki dziennika w `/var/log` po utworzeniu hello wirtualny dysk twardy podłączony tooa Rozwiązywanie problemów z maszyny Wirtualnej.


## <a name="view-existing-virtual-hard-disk-details"></a>Szczegóły istniejącego wirtualnego dysku twardego
Przed dołączeniem tooanother Twojego wirtualnego dysku twardego (VHD) maszyny Wirtualnej, należy tooidentify hello URI hello dysku systemu operacyjnego. 

Wyświetl informacje o sieci maszyny Wirtualnej z [az maszyny wirtualnej pokazu](/cli/azure/vm#show). Użyj hello `--query` flagi tooextract hello URI toohello OS dysku. Witaj poniższy przykład pobiera informacje o dysku dla maszyny Wirtualnej o nazwie hello `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Witaj identyfikatora URI jest zbyt podobne**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Usuń istniejącą maszynę Wirtualną
Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure. Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje. Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC). Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej. Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta. dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.

pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie. Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu. Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.

Usuń hello maszyny Wirtualnej z [usunąć maszyny wirtualnej az](/cli/azure/vm#delete). powitania po usuwaniu przykład Witaj maszyny Wirtualnej o nazwie `myVM` z hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej. dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej
Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów. Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse maszyny Wirtualnej i edytowania zawartości hello dysku. Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np. Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.

Dołącz hello istniejącego wirtualnego dysku twardego z [dołączyć az wirtualna niezarządzanych dysku](/cli/azure/vm/unmanaged-disk#attach). Po dołączeniu istniejącego wirtualnego dysku twardego hello, określ dysk toohello URI hello uzyskanych w poprzednim hello `az vm show` polecenia. Witaj poniższy przykład dołącza istniejących toohello wirtualnego dysku twardego, rozwiązywanie problemów z maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
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

2. Teraz odłączyć hello wirtualnego dysku twardego z hello maszyny Wirtualnej. Zamknij tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej. Witaj listy dołączonych tooyour dysków danych Rozwiązywanie problemów z maszyny Wirtualnej z [lista niezarządzanych dysków maszyny wirtualnej az](/cli/azure/vm/unmanaged-disk#list). Witaj poniższy przykład list hello dysków z danymi dołączony toohello maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Zanotuj nazwę powitania dla istniejącego wirtualnego dysku twardego. Na przykład nazwa dysku z hello hello identyfikator URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** jest **myVHD**. 

    Odłączyć dysku danych powitania od maszyny Wirtualnej [odłączyć az wirtualna niezarządzanych dysku](/cli/azure/vm/unmanaged-disk#detach). Witaj poniższy przykład odłącza dysk hello o nazwie `myVHD` z hello maszyny Wirtualnej o nazwie `myVMRecovery` w hello `myResourceGroup` grupy zasobów:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Tworzenie maszyny Wirtualnej z oryginalny dysk twardy
Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). Witaj rzeczywiste JSON szablonu jest w hello następujące łącze:

- https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD/azuredeploy.JSON

Witaj szablonu wdraża maszynę Wirtualną przy użyciu hello identyfikator URI dysku VHD z hello wcześniej polecenia. Wdrażanie szablonu hello z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create). Podaj hello URI tooyour oryginalny dysk VHD i określ typ hello systemu operacyjnego, rozmiar maszyny Wirtualnej i Nazwa maszyny Wirtualnej w następujący sposób:

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Włączyć ponownie diagnostykę rozruchu
Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone. Włącz diagnostykę rozruchu z [włączyć diagnostyki rozruchu az wirtualna](/cli/azure/vm/boot-diagnostics#enable). Witaj poniższy przykład umożliwia włączenie rozszerzenia diagnostycznych hello na powitania maszyny Wirtualnej o nazwie `myDeployedVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [Rozwiązywanie problemów z SSH połączeń tooan maszyny Wirtualnej Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej systemu Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
