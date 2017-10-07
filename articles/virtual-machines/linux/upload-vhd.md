---
title: aaaUpload lub kopiowanie niestandardowych maszyny Wirtualnej systemu Linux 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Przekazywanie lub skopiowanie dostosowane maszyny wirtualnej przy użyciu modelu wdrażania usługi Resource Manager hello i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku z hello Azure CLI 2.0

<!-- rename toocreate-vm-specialized -->

W tym artykule opisano sposób tooupload dostosowane wirtualnego dysku twardego (VHD) lub skopiuj istniejącego dysku VHD na platformie Azure i tworzenie nowych maszyn wirtualnych systemu Linux (maszyn wirtualnych) z hello niestandardowego dysku. Można zainstalować i skonfigurować wymagania dotyczące systemu Linux distro tooyour i następnie użyć tego wirtualnego dysku twardego tooquickly tworzenia nowej maszyny wirtualnej platformy Azure.

Jeśli chcesz toocreate wiele maszyn wirtualnych z dostosowanych dysku, należy utworzyć obraz z maszyny Wirtualnej lub wirtualnego dysku twardego. Aby uzyskać więcej informacji, zobacz [utworzyć niestandardowy obraz maszyny Wirtualnej platformy Azure przy użyciu interfejsu wiersza polecenia hello](tutorial-custom-images.md).

Dostępne są dwie opcje:
* [Przekazywanie wirtualnego dysku twardego](#option-1-upload-a-specialized-vhd)
* [Skopiuj istniejącej maszyny Wirtualnej Azure](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Szybkie polecenia

Podczas tworzenia nowej maszyny Wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) z dysku dostosowane lub specjalne możesz **dołączyć** hello dysku (— attach-os-disk) zamiast określania obraz niestandardowy lub witryny marketplace (— obrazu). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* za pomocą hello managed dysku o nazwie *myManagedDisk* utworzone na podstawie niestandardowych dysk VHD:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Wymagania
Witaj toocomplete następujące kroki, należy:

* Maszyny wirtualnej systemu Linux, który został przygotowany do użycia na platformie Azure. Witaj [hello przygotowanie wirtualna](#prepare-the-vm) sekcji tego artykułu opisano, jak toofind distro określone informacje na temat instalowania hello agenta systemu Linux platformy Azure (agenta waagent), który jest wymagany dla hello wirtualna toowork poprawnie na platformie Azure i musisz toobe stanie tooconnect tooit przy użyciu protokołu SSH.
* plik VHD Hello z istniejącego [dystrybucji Linux zatwierdzone na platformie Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w formacie VHD hello. Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:
  * Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu. W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu **przekonwertować qemu img**.
  * Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure. Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello. W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [przekonwertować qemu img](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell. Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem. Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.
> 
> 


* Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione *myResourceGroup*, *mojekontomagazynu*, i *mydisks*.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Przygotowanie hello maszyny Wirtualnej

Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). następujące artykuły Hello przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure:

* [Na podstawie centOS dystrybucji](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian systemu Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Inne — niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Zobacz też hello [informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.

> [!NOTE]
> Witaj [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) stosuje tooVMs systemem Linux, tylko gdy jeden z hello dystrybucje zatwierdzone na jest używany z hello szczegóły konfiguracji określone w obsługiwanych wersjach w [systemu Linux na zatwierdzone na platformie Azure Dystrybucje](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Opcja 1: Przekazywanie wirtualnego dysku twardego

Możesz przekazać dostosowane wirtualnego dysku twardego uruchomione na komputerze lokalnym lub wyeksportowany z innej chmury. toouse hello wirtualnego dysku twardego toocreate nowej maszyny Wirtualnej Azure, należy tooupload hello wirtualnego dysku twardego tooa magazynu kont i Utwórz dysków zarządzanych z hello wirtualnego dysku twardego. 

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Przed przekazaniem dysku niestandardowych i Tworzenie maszyn wirtualnych, należy najpierw toocreate grupą zasobów o [Tworzenie grupy az](/cli/azure/group#create).

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji: [dysków zarządzanych Azure — omówienie](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Utwórz konto magazynu dla niestandardowego dysku i maszyn wirtualnych o [Tworzenie konta magazynu az](/cli/azure/storage/account#create). 

Witaj poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu* w utworzoną wcześniej grupę zasobów hello:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Wyświetl klucze konta magazynu
Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu. Klawisze dostępu są używane podczas uwierzytelniania toohello konta magazynu, takich jak przeprowadzanie operacji zapisu. Przeczytaj więcej na temat [Zarządzanie dostępu tutaj toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Wyświetl klucze dostępu hello z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list).

Wyświetl klucze dostępu hello utworzone konto magazynu hello:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

Witaj wynik jest podobny do:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Zanotuj **klucz1** jako zostanie użyty toointeract z konta magazynu w następnych krokach hello.

### <a name="create-a-storage-container"></a>Tworzenie kontenera magazynu
W hello sam sposób, że toologically różnych katalogach organizowanie lokalnego systemu plików, tworzyć dyski kontenery tooorganize konta magazynu. Konto magazynu może zawierać dowolną liczbę kontenerów. Tworzenie kontenera z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create).

Witaj poniższy przykład tworzy kontener o nazwie *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Przekaż hello wirtualnego dysku twardego
Teraz Przekaż dysku niestandardowych z [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload). Przekazywanie i przechowywać dysku niestandardowych jako stronicowy obiekt blob.

Określ użytkownika klucza dostępu, kontener hello, utworzony w poprzednim kroku hello, a następnie hello ścieżki toohello niestandardowego dysku na komputerze lokalnym:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Witaj przekazywanie wirtualnego dysku twardego może chwilę potrwać.

### <a name="create-a-managed-disk"></a>Tworzenie dysku zarządzanego


Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego za pomocą [Tworzenie dysku az](/cli/azure/disk#create). Witaj poniższy przykład tworzy zarządzanych dysk o nazwie *myManagedDisk* z wirtualnego dysku twardego hello przekazać tooyour o nazwie konto magazynu i kontener:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Opcja 2: Kopiowanie istniejącej maszyny Wirtualnej

Można również utworzyć hello dostosowane maszyny Wirtualnej w ramach platformy Azure, a następnie dysku systemu operacyjnego hello kopii i dołącz je tooa nowej maszyny Wirtualnej toocreate kolejną kopię. Jest to testowania poprawnie, ale jeśli chcesz toouse istniejącej maszyny Wirtualnej platformy Azure jako hello model wiele nowych maszyn wirtualnych, naprawdę należy utworzyć **obrazu** zamiast tego. Aby uzyskać więcej informacji o tworzeniu obrazu z istniejącej maszyny Wirtualnej Azure, zobacz [utworzyć niestandardowy obraz maszyny Wirtualnej platformy Azure przy użyciu hello interfejsu wiersza polecenia](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Utwórz migawkę

W tym przykładzie tworzy migawkę maszyny wirtualnej o nazwie *myVM* w grupie zasobów *myResourceGroup* i tworzy migawkę o nazwie *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Tworzenie dysków zarządzanych w hello

Utwórz nowy dysk zarządzanego z hello migawki.

Pobierz identyfikator hello hello migawki. W tym przykładzie hello migawki o nazwie *osDiskSnapshot* i hello *myResourceGroup* grupy zasobów.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Utwórz hello dysków zarządzanych. W tym przykładzie utworzysz zarządzanych dysk o nazwie *myManagedDisk* z naszych migawki to 128 GB w rozmiarze w magazynu w warstwie standardowa.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Utwórz hello maszyny Wirtualnej

Teraz utworzyć maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i Dołącz (--attach-os-disk) hello zarządzane dysku jako dysku hello systemu operacyjnego. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myNewVM* za pomocą hello managed utworzone na podstawie przekazanego dysk VHD dysku:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Powinno być możliwe tooSSH do hello maszyny Wirtualnej przy użyciu poświadczeń hello z hello źródłowej maszyny Wirtualnej. 

## <a name="next-steps"></a>Następne kroki
Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md). Można również zbyt[Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nowych maszyn wirtualnych. Upewnij się, jeśli masz aplikacje działające na maszyn wirtualnych konieczność tooaccess zbyt[Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

