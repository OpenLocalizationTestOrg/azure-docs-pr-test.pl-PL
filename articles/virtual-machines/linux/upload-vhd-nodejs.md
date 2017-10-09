---
title: aaaUpload niestandardowego obrazu systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft
description: "Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego (VHD) z niestandardowego obrazu systemu Linux przy użyciu modelu wdrażania usługi Resource Manager hello i hello Azure CLI w wersji 1.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku przy użyciu hello Azure CLI w wersji 1.0
W tym artykule opisano sposób tooupload tooAzure wirtualnego dysku twardego (VHD) przy użyciu hello modelu wdrażania usługi Resource Manager i Tworzenie maszyn wirtualnych systemu Linux z tego obrazu niestandardowego. Ta funkcja pozwala tooinstall i skonfiguruj wymagania tooyour distro systemu Linux, a następnie użyj tego wirtualnego dysku twardego tooquickly Tworzenie maszyn wirtualnych platformy Azure (maszyny wirtualne).


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowych poleceń tooupload tooAzure maszyny Wirtualnej. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#requirements).

Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `myimages`.

Najpierw utwórz grupę zasobów. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUs` lokalizacji:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Tworzenie dysków wirtualnych toohold konta magazynu. Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Lista hello klucze dostępu dla konta magazynu. Zanotuj `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Utwórz kontener w ramach konta magazynu przy użyciu klucza magazynu hello, który został uzyskany. Witaj poniższy przykład tworzy kontener o nazwie `myimages` przy użyciu wartości klucza magazynu hello z `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

Na koniec przekazać kontener toohello Twojego wirtualnego dysku twardego, utworzony. Określ hello tooyour ścieżkę lokalną wirtualnego dysku twardego w obszarze `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

Teraz można utworzyć maszyny Wirtualnej z dysku wirtualnego przekazane [przy użyciu szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). Umożliwia także hello interfejsu wiersza polecenia, określając hello URI tooyour dysku (`--image-urn`). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego hello wcześniej przekazany:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

Konto magazynu docelowego Hello ma toobe hello sam jako gdzie przekazany wirtualny dysk. Możesz również muszą toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello `azure vm create` polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH. Więcej o hello [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Wymagania
Witaj toocomplete następujące kroki, należy:

* **Linux zainstalowanego systemu operacyjnego w pliku VHD** -Zainstaluj [dystrybucji zatwierdzone na platformie Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w hello wirtualnego dysku twardego Format. Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:
  * Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu. W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.
  * Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure. Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello. W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell. Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem. Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.
> 
> 

* Maszyny wirtualne utworzone na podstawie niestandardowego obrazu musi znajdować się w hello samo konto magazynu jako hello samego obrazu
  * Tworzenie toohold konto i kontener magazynu zarówno niestandardowego obrazu i utworzone maszyny wirtualne
  * Po utworzeniu wszystkich maszyn wirtualnych, można bezpiecznie usunąć obrazu

Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `myimages`.

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Przygotowanie toobe obraz powitania przekazany
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


## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Grupy zasobów logicznie zebranie wszystkich toosupport zasobów Azure hello maszyn wirtualnych, takie jak hello sieci wirtualnych i magazynu. Przeczytaj więcej na temat [grupy zasobów platformy Azure, w tym miejscu](../../azure-resource-manager/resource-group-overview.md). Przed przekazaniem obrazu niestandardowego dysku i Tworzenie maszyn wirtualnych, najpierw toocreate grupę zasobów. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUS` lokalizacji:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
Maszyny wirtualne są przechowywane jako stronicowe obiekty BLOB w ramach konta magazynu. Przeczytaj więcej na temat [magazynu obiektów blob platformy Azure w tym miejscu](../../storage/common/storage-introduction.md#blob-storage). Możesz utworzyć konto magazynu obrazu niestandardowego dysku i maszyn wirtualnych. Wszystkie maszyny wirtualne utworzone z dysku niestandardowego obrazu muszą toobe w hello tego samego konta magazynu jako obrazu.

Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount` w utworzoną wcześniej grupę zasobów hello:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Wyświetl klucze konta magazynu
Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu. Klawisze dostępu są używane podczas uwierzytelniania toohello konta magazynu, takich jak toocarry operacje zapisu. Przeczytaj więcej na temat [Zarządzanie dostępu tutaj toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Możesz wyświetlić klawisze dostępu z hello `azure storage account keys list` polecenia.

Wyświetl klucze dostępu hello utworzone konto magazynu hello:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
W hello sam sposób, że toologically różnych katalogach organizowanie lokalnego systemu plików, tworzenie kontenery w ramach tooorganize konta magazynu dysków wirtualnych i obrazów. Konto magazynu może zawierać dowolną liczbę kontenerów. 

Witaj poniższy przykład tworzy kontener o nazwie `myimages`, określania klucza dostępu hello uzyskanych w poprzednim kroku hello (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>Przekazywanie wirtualnego dysku twardego
Teraz można faktycznie przekazywanie obrazu niestandardowego dysku. Jako wszystkich wirtualnych dysków używanych przez maszyny wirtualne, należy przekazać i przechowywania obrazu niestandardowego dysku jako stronicowy obiekt blob.

Określ użytkownika klucza dostępu, kontener hello, utworzony w poprzednim kroku hello, a następnie hello ścieżki toohello dysku niestandardowego obrazu na komputerze lokalnym:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Tworzenie maszyny Wirtualnej z obrazu niestandardowego
Podczas tworzenia maszyn wirtualnych z obrazu niestandardowego dysku, należy określić obraz dysku toohello URI hello. Upewnij się, że hello zgodne konto magazynu docelowego przechowywania obrazu niestandardowego dysku. Można utworzyć maszyny Wirtualnej przy użyciu szablonu hello Azure CLI lub JSON Menedżera zasobów.

### <a name="create-a-vm-using-hello-azure-cli"></a>Utwórz maszynę Wirtualną przy użyciu hello wiersza polecenia platformy Azure
Określ hello `--image-urn` parametr hello `azure vm create` polecenia toopoint tooyour dysku niestandardowego obrazu. Upewnij się, że `--storage-account-name` dopasowań hello przechowywania obrazu niestandardowego dysku konta magazynu. Nie masz toouse hello tego samego kontenera jako hello toostore obrazu niestandardowego dysku maszyn wirtualnych. Upewnij się, że toocreate żadnych dodatkowych kontenerów w hello sam sposób jak hello wcześniejszych krokach przed przekazaniem dysku niestandardowych obrazów.

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z obrazu niestandardowego dysku:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

Możesz nadal konieczne toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello `azure vm create` polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH. Dowiedz się więcej o hello [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Utwórz maszynę Wirtualną przy użyciu szablonu JSON
Szablony usługi Azure Resource Manager są plików JavaScript Object Notation (JSON), które definiują środowiska hello mają toobuild. Szablony Hello dzieli się toodifferent dostawców zasobów, takich jak obliczeń lub sieci. Możesz użyć istniejących szablonów lub napisać własny. Przeczytaj więcej na temat [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).

W ramach hello `Microsoft.Compute/virtualMachines` dostawcy szablonu, masz `storageProfile` węzła, który zawiera szczegóły konfiguracji powitania dla maszyny Wirtualnej. Witaj dwie główne parametry tooedit są hello `image` i `vhd` identyfikatorów URI punktu tooyour obrazu niestandardowego dysku i dysk wirtualny nowej maszyny Wirtualnej. Witaj poniżej przedstawiono przykład hello JSON dla przy użyciu obrazu niestandardowego dysku:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Można użyć [toocreate tego istniejącego szablonu maszyny Wirtualnej z obrazu niestandardowego](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) lub przeczytaj o [Tworzenie szablonów usługi Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Po utworzeniu szablonu skonfigurowanego tworzenia maszyn wirtualnych przy użyciu hello `azure group deployment create` polecenia. Określ identyfikator URI szablonu JSON hello z hello `--template-uri` parametru:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Jeśli masz plik JSON przechowywane lokalnie na komputerze, możesz użyć hello `--template-file` parametru zamiast tego:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Następne kroki
Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md). Można również zbyt[Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nowych maszyn wirtualnych. Upewnij się, jeśli masz aplikacje działające na maszyn wirtualnych konieczność tooaccess zbyt[Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

