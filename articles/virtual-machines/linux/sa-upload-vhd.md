---
title: aaaUpload niestandardowego dysku Linux Azure CLI 2.0 | Dokumentacja firmy Microsoft
description: "Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego (VHD), przy użyciu modelu wdrażania usługi Resource Manager hello i hello Azure CLI 2.0"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku z hello Azure CLI 2.0
W tym artykule pokazano, jak tooupload tooan wirtualnego dysku twardego (VHD) magazynu Azure konta hello Azure CLI 2.0 i Tworzenie maszyn wirtualnych systemu Linux z tego dysku niestandardowych. Można również wykonać te kroki hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ta funkcja pozwala tooinstall i skonfiguruj wymagania tooyour distro systemu Linux, a następnie użyj tego wirtualnego dysku twardego tooquickly Tworzenie maszyn wirtualnych platformy Azure (maszyny wirtualne).

W tym temacie używa konta magazynu dla hello końcowego wirtualne dyski twarde, ale można też wykonać te czynności przy użyciu [dyskach zarządzanych](upload-vhd.md). 

## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowych poleceń tooupload tooAzure wirtualnego dysku twardego. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#requirements).

Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `mydisks`.

Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUs` lokalizacji:

```azurecli
az group create --name myResourceGroup --location westus
```

Tworzenie dysków wirtualnych z toohold konta magazynu [Tworzenie konta magazynu az](/cli/azure/storage/account#create). Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Listę hello klawiszy dostępu dla konta magazynu z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list). Zanotuj `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Utwórz kontener w ramach konta magazynu przy użyciu klucza magazynu hello uzyskany z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create). Witaj poniższy przykład tworzy kontener o nazwie `mydisks` przy użyciu wartości klucza magazynu hello z `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Na koniec, przekaż z kontenera toohello VHD zostały utworzone z [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload). Określ hello tooyour ścieżkę lokalną wirtualnego dysku twardego w obszarze `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Określ dysk tooyour URI hello (`--image`) z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego hello wcześniej przekazany:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

Konto magazynu docelowego Hello ma toobe hello sam jako gdzie przekazany wirtualny dysk. Możesz również muszą toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello **tworzenia maszyny wirtualnej az** polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH. Więcej o hello [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Wymagania
Witaj toocomplete następujące kroki, należy:

* **Linux zainstalowanego systemu operacyjnego w pliku VHD** -Zainstaluj [dystrybucji zatwierdzone na platformie Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w hello wirtualnego dysku twardego Format. Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:
  * Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu. W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.
  * Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure. Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello. W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell. Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem. Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.
> 
> 

* Maszyny wirtualne utworzone na podstawie niestandardowych dysku musi znajdować się w hello samo konto magazynu jako hello samego dysku
  * Tworzenie toohold konto i kontener magazynu zarówno niestandardowego dysku i utworzone maszyny wirtualne
  * Po utworzeniu wszystkich maszyn wirtualnych, można bezpiecznie usunąć dysku

Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `mydisks`.

<a id="prepimage"> </a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Przygotowanie toobe dysku hello przekazany
Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). następujące artykuły Hello przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure:

* **[Na podstawie centOS dystrybucji](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian systemu Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Inne — niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Zobacz też hello  **[informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes)**  bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.

> [!NOTE]
> Witaj [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) stosuje tooVMs systemem Linux, tylko gdy jeden z hello dystrybucje zatwierdzone na jest używany z hello szczegóły konfiguracji określone w obsługiwanych wersjach w [systemu Linux na zatwierdzone na platformie Azure Dystrybucje](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Grupy zasobów logicznie zebranie wszystkich toosupport zasobów Azure hello maszyn wirtualnych, takie jak hello sieci wirtualnych i magazynu. Dla grup zasobów więcej informacji, zobacz [omówienie grupy zasobów](../../azure-resource-manager/resource-group-overview.md). Przed przekazaniem dysku niestandardowych i Tworzenie maszyn wirtualnych, należy najpierw toocreate grupą zasobów o [Tworzenie grupy az](/cli/azure/group#create).

Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Utwórz konto magazynu dla niestandardowego dysku i maszyn wirtualnych o [Tworzenie konta magazynu az](/cli/azure/storage/account#create). Wszystkie maszyny wirtualne z dyskami niezarządzane, tworzonych z Twojej toobe potrzeby niestandardowego dysku w hello tego samego konta magazynu jako tego dysku. 

Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount` w utworzoną wcześniej grupę zasobów hello:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Wyświetl klucze konta magazynu
Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu. Klawisze dostępu są używane podczas uwierzytelniania toohello konta magazynu, takich jak toocarry operacje zapisu. Przeczytaj więcej na temat [Zarządzanie dostępu tutaj toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Wyświetl klucze dostępu hello z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list).

Wyświetl klucze dostępu hello utworzone konto magazynu hello:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Zanotuj `key1` jak zostanie użyty toointeract z konta magazynu w następnych krokach hello.

## <a name="create-a-storage-container"></a>Tworzenie kontenera magazynu
W hello sam sposób, że toologically różnych katalogach organizowanie lokalnego systemu plików, tworzyć dyski kontenery tooorganize konta magazynu. Konto magazynu może zawierać dowolną liczbę kontenerów. Tworzenie kontenera z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create).

Witaj poniższy przykład tworzy kontener o nazwie `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Przekazywanie wirtualnego dysku twardego
Teraz Przekaż dysku niestandardowych z [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload). Przekazywanie i przechowywać dysku niestandardowych jako stronicowy obiekt blob.

Określ użytkownika klucza dostępu, kontener hello, utworzony w poprzednim kroku hello, a następnie hello ścieżki toohello niestandardowego dysku na komputerze lokalnym:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Utwórz hello maszyny Wirtualnej
toocreate maszyny Wirtualnej z dyskami niezarządzane, określ dysk tooyour URI hello (`--image`) z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego hello wcześniej przekazany:

Określ hello `--image` parametr o [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) toopoint tooyour niestandardowego dysku. Upewnij się, że `--storage-account` dopasowań hello konto magazynu, w którym przechowywane niestandardowe dysku. Nie masz toouse hello tego samego kontenera jako hello toostore niestandardowego dysku maszyn wirtualnych. Upewnij się, że toocreate żadnych dodatkowych kontenerów w hello sam sposób jak hello wcześniejszych krokach przed przekazaniem dysku niestandardowych.

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dysku niestandardowych:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Możesz nadal konieczne toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello **tworzenia maszyny wirtualnej az** polecenia takie jak nazwa użytkownika i kluczy SSH.


## <a name="resource-manager-template"></a>Szablon usługi Resource Manager
Szablony usługi Azure Resource Manager są plików JavaScript Object Notation (JSON), które definiują środowiska hello mają toobuild. Szablony Hello dzieli się toodifferent dostawców zasobów, takich jak obliczeń lub sieci. Możesz użyć istniejących szablonów lub napisać własny. Przeczytaj więcej na temat [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).

W ramach hello `Microsoft.Compute/virtualMachines` dostawcy szablonu, masz `storageProfile` węzła, który zawiera szczegóły konfiguracji powitania dla maszyny Wirtualnej. Witaj dwie główne parametry tooedit są hello `image` i `vhd` identyfikatorów URI punktu tooyour niestandardowego dysku i dysk wirtualny nowej maszyny Wirtualnej. Hello poniżej przedstawiono przykład hello JSON dla przy użyciu niestandardowego dysku:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Można użyć [toocreate tego istniejącego szablonu maszyny Wirtualnej z obrazu niestandardowego](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) lub przeczytaj o [Tworzenie szablonów usługi Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Po utworzeniu szablonu skonfigurowanego użyj [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) toocreate maszyn wirtualnych. Określ identyfikator URI szablonu JSON hello z hello `--template-uri` parametru:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Jeśli masz plik JSON przechowywane lokalnie na komputerze, możesz użyć hello `--template-file` parametru zamiast tego:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Następne kroki
Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md). Można również zbyt[Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nowych maszyn wirtualnych. Upewnij się, jeśli masz aplikacje działające na maszyn wirtualnych konieczność tooaccess zbyt[Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

