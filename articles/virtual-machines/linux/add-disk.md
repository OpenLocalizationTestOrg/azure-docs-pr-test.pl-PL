---
title: "dysk tooLinux maszyny Wirtualnej za pomocą aaaAdd hello Azure CLI | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooadd tooyour trwałe dysku maszyny Wirtualnej systemu Linux z hello Azure CLI w wersji 1.0 oraz 2.0."
keywords: "maszyny wirtualnej systemu Linux, Dodaj zasób dysku"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a>Dodaj tooa dysku maszyny Wirtualnej systemu Linux
W tym artykule opisano, jak tooattach a trwałe dysku tooyour maszyny Wirtualnej, dzięki czemu można zachować dane — nawet wtedy, gdy maszyna wirtualna jest ponownie udostępnić toomaintenance lub zmiany rozmiaru. 

## <a name="quick-commands"></a>Szybkie polecenia
Witaj następujący przykład dołącza `50`GB toohello dysku maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

dyski zarządzane toouse:

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

dyski toouse niezarządzanych:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Dołączenie dysku zarządzanego

Używanie dysków zarządzanych pozwala toofocus maszyn wirtualnych i ich dyski bez obaw o kontach magazynu Azure. Można szybko tworzyć i dołączyć dysku zarządzanego tooa maszynę Wirtualną przy użyciu hello tej samej grupy zasobów platformy Azure, lub można utworzyć dowolną liczbę dysków, a następnie dołącz je.


### <a name="attach-a-new-disk-tooa-vm"></a>Dołącz nowe tooa dysku maszyny Wirtualnej

Jeśli jest potrzebna nowy dysk na maszynie Wirtualnej, można użyć hello `az vm disk attach` polecenia.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Dołączanie istniejącego dysku 

W wielu przypadkach możesz dołączyć dyski, które zostały już utworzone. Znajdź najpierw identyfikator dysku hello, a następnie przekazać tego toohello `az vm disk attach` polecenia. Witaj poniższy przykład używa dysku utworzone za pomocą `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Witaj dane wyjściowe podobne hello następujące (można użyć hello `-o table` opcji dane wyjściowe hello tooformat polecenia tooany w):

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a>Podłącz dysk niezarządzane

Trwa dołączanie nowego dysku jest szybkie, jeżeli nie stanowi tworzenia dysku w hello tego samego konta magazynu jako maszyny Wirtualnej. Typ `azure vm disk attach-new` toocreate i dołączyć nowego dysku GB dla maszyny Wirtualnej. Jeśli w sposób jawny nie identyfikuje konto magazynu, dyskami tworzenia jest umieszczany w hello samo konto magazynu, w którym znajduje się na dysku systemu operacyjnego. Witaj następujący przykład dołącza `50`GB toohello dysku maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Połącz toohello nowy dysk hello toomount maszyny Wirtualnej systemu Linux
> [!NOTE]
> W tym temacie łączy tooa maszyny Wirtualnej przy użyciu nazwy użytkownika i hasła. toouse toocommunicate pary kluczy publicznych i prywatnych z maszyny Wirtualnej, zobacz [jak tooUse SSH z systemem Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

Należy tooSSH do Twojej toopartition maszyny Wirtualnej platformy Azure, formatowania i instalacji nowego dysku, dlatego może być używany z maszyny Wirtualnej systemu Linux. Jeśli nie masz doświadczenia w obsłudze połączenia z serwerem **ssh**, polecenie hello ma postać hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`i wygląda hello:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Dane wyjściowe

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

Teraz, gdy nawiązano połączenie tooyour maszyny Wirtualnej, wszystko jest gotowe tooattach dysku.  Znajdź najpierw hello na dysku, przy użyciu `dmesg | grep SCSI` (metoda hello jest używany toodiscover nowego dysku może się różnić). W takim przypadku wygląda mniej więcej tak:

```bash
dmesg | grep SCSI
```

Dane wyjściowe

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

i w przypadku hello w tym temacie, hello `sdc` dysk jest hello jedną, która ma. Teraz hello partycji z `sudo fdisk /dev/sdc` — przy założeniu, że w sieci wielkość hello dysk był `sdc`, był dysk podstawowy na partycji 1 i zaakceptować hello innych wartości domyślnych.

```bash
sudo fdisk /dev/sdc
```

Dane wyjściowe

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

Tworzenie partycji hello wpisując `p` w wierszu hello:

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

I zapisać systemu plików toohello partycji przy użyciu hello **mkfs** polecenie, określając filesystem typu i hello urządzenia nazwę programu. W tym temacie firma Microsoft korzysta z `ext4` i `/dev/sdc1` z powyżej:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Dane wyjściowe

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

Teraz utworzymy katalogu toomount hello system plików za pomocą `mkdir`:

```bash
sudo mkdir /datadrive
```

I zainstalować, za pomocą katalogu hello `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

dysk z danymi Hello jest teraz gotowy toouse jako `/datadrive`.

```bash
ls
```

Dane wyjściowe

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

dysk hello tooensure jest ponownej instalacji automatycznie po ponowny rozruch komputera musi być dodany plik /etc/fstab toohello. Ponadto zdecydowanie zaleca się że hello UUID (powszechnie Unikatowy identyfikator) jest używany w etc/fstab toorefer toohello dysków zamiast hello tylko nazwa urządzenia (takich jak `/dev/sdc1`). Jeśli hello system operacyjny wykryje błąd dysku podczas rozruchu, przy użyciu identyfikatora UUID hello pozwala uniknąć dysku będzie nieprawidłowa hello jest zainstalowany tooa podanej lokalizacji. Pozostałe dyski danych może następnie można przypisać te takich samych identyfikatorów urządzenia. toofind hello UUID hello nowy dysk, użyj hello **blkid** narzędzie:

```bash
sudo -i blkid
```

Witaj dane wyjściowe wyglądają podobne toohello następujące czynności:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Nieprawidłowo edycji hello **/etc/fstab** pliku może spowodować rozruch systemu. Jeśli nie wiesz, zapoznaj się z informacji w sposób tooproperly edytować ten plik dokumentacją toohello dystrybucji. Zalecane jest również, że kopia zapasowa pliku /etc/fstab hello został utworzony przed rozpoczęciem edycji.
> 
> 

Następnie otwórz folder hello **/etc/fstab** plik w edytorze tekstu:

```bash
sudo vi /etc/fstab
```

W tym przykładzie używamy hello UUID wartość dla hello nowe **/dev/sdc1** urządzenia, który został utworzony w poprzednich krokach hello i hello punktu instalacji **/datadrive**. Dodaj wiersz toohello końca hello hello **/etc/fstab** pliku:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Później usunąć dysk z danymi bez konieczności edytowania fstab może spowodować hello wirtualna toofail tooboot. Większości dystrybucji zapewniają albo hello `nofail` i/lub `nobootwait` fstab opcje. Te opcje Zezwalaj tooboot systemu, nawet jeśli dysku hello toomount zakończy się niepowodzeniem w czasie rozruchu. Dokumentacja programu dystrybucji, aby uzyskać więcej informacji na temat tych parametrów.
> 
> Witaj **nofail** opcja zapewnia, że hello maszyna wirtualna zacznie nawet wtedy, gdy system plików hello jest uszkodzony lub hello dysku nie istnieje w czasie rozruchu. Bez tej opcji, możesz napotkać zachowanie zgodnie z opisem w [nie SSH tooLinux maszyny Wirtualnej ze względu na błędy tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>PRZYCINANIE/UNMAP obsługę systemu Linux na platformie Azure
PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello. Jest to szczególnie przydatne w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone. Można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.

Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux. W zwykły sposób poszukaj dystrybucji hello zalecane podejście:

* Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:

    ```bash
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
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Następne kroki
* Należy pamiętać, że nowy dysk nie jest dostępne toohello maszyny Wirtualnej Jeśli nastąpi ponowne uruchomienie, chyba że pisania tego tooyour informacji [fstab](http://en.wikipedia.org/wiki/Fstab) pliku.
* tooensure maszyny Wirtualnej systemu Linux jest skonfigurowane poprawnie, przejrzyj hello [maszyny Linux Optymalizowanie](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalecenia.
* Rozwiń węzeł pojemności pamięci masowej przez dodanie dodatkowych dysków i [skonfigurować RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) dla wyższą wydajność.

