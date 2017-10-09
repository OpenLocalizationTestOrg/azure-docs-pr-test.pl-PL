---
title: "aaaCreate i przekazać tooAzure dysku VHD systemu Linux | Dokumentacja firmy Microsoft"
description: "Tworzenie i przekazywanie Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Linux hello przy użyciu klasycznego modelu wdrożenia hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Tworzenie i przekazywanie wirtualnego dysku twardego zawierający hello System operacyjny Linux
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Możesz również [Przekaż obraz niestandardowy dysku przy użyciu usługi Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

W tym artykule opisano, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD), dzięki czemu można używać jako własnego obrazu toocreate maszynach wirtualnych platformy Azure. Dowiedz się, jak tooprepare hello systemu operacyjnego, można użyć toocreate wiele maszyn wirtualnych na podstawie obrazu. 


## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że hello następujące elementy:

* **Linux zainstalowanego systemu operacyjnego w pliku VHD** — zainstalowano [dystrybucji Linux zatwierdzone na platformie Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w formacie VHD hello. Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:
  * Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu. W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.
  * Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure. Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello. W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell. Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem. Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.

* **Interfejs wiersza polecenia platformy Azure** — najnowsza wersja hello instalacji [interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello wirtualnego dysku twardego.

<a id="prepimage"> </a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Krok 1: Przygotowanie toobe obraz powitania przekazany
Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello następujące artykuły przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure. Po wykonaniu kroków hello powitania po przewodnikach potem wróć tutaj po utworzeniu pliku wirtualnego dysku twardego, który jest gotowy tooupload tooAzure:

* **[Na podstawie centOS dystrybucji](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian systemu Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Inne — niezatwierdzonych dystrybucji](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Witaj umowy SLA platformy Azure stosuje toovirtual maszynami hello używany w hello szczegóły konfiguracji określone w obsługiwanych wersjach systemu operacyjnego Linux tylko wtedy, gdy jeden z hello dystrybucje zatwierdzone [systemu Linux na Azure-Endorsed dystrybucji ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Wszystkie dystrybucje systemu Linux w galerii Azure obrazu hello są potwierdzony dystrybucje z hello wymaganej konfiguracji.
> 
> 

Zobacz też hello  **[informacje o instalacji systemu Linux](../create-upload-generic.md#general-linux-installation-notes)**  bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.

<a id="connect"> </a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Krok 2: Przygotowanie hello tooAzure połączenia
Upewnij się, że używasz hello Azure CLI w hello klasycznego modelu wdrażania (`azure config mode asm`), następnie zalogowanie się na koncie tooyour:

```azurecli
azure login
```


<a id="upload"> </a>

## <a name="step-3-upload-hello-image-tooazure"></a>Krok 3: Przekaż hello tooAzure obrazu
Należy tooupload konta magazynu w pliku wirtualnego dysku twardego. Albo można wybrać istniejące konto magazynu lub [Utwórz nową](../../../storage/common/storage-create-storage-account.md).

Użyj hello Azure CLI tooupload hello obrazu przy użyciu hello następujące polecenie:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

W poprzednim przykładzie hello:

* **BlobStorageURL** jest adres URL hello hello konta magazynu, Zaplanuj toouse
* **YourImagesFolder** jest hello kontenera w magazynie obiektów blob w miejscu toostore obrazów
* **VHDName** jest hello etykietą, która jest wyświetlana w portalu tooidentify hello wirtualnego dysku twardego.
* **PathToVHDFile** jest hello Pełna ścieżka i nazwa pliku VHD hello na tym komputerze.

następujące polecenie Hello przedstawia pełny przykład:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Krok 4: Tworzenie maszyny Wirtualnej z obrazu hello
Możesz utworzyć maszynę Wirtualną przy użyciu `azure vm create` w hello sam sposób jak regularne maszyny Wirtualnej. Określ nazwę hello obrazu należy nadać hello poprzedniego kroku. W hello poniższy przykład, używamy hello **myImage** podany w poprzednim kroku hello nazwa obrazu:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate własnych maszyn wirtualnych, podać własne nazwy użytkownika + hasła, lokalizację, nazwy DNS i nazwa obrazu.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz [odwołania wiersza polecenia platformy Azure dla hello Azure klasycznego modelu wdrażania](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
