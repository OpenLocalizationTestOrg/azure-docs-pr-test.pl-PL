---
title: aaaDownload dysku VHD systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Pobierz dysku VHD systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello i hello portalu Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Pobierz dysku VHD systemu Linux na platformie Azure

W tym artykule dowiesz się, jak toodownload [Linux wirtualnego dysku twardego (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello pliku z platformy Azure przy użyciu wiersza polecenia platformy Azure i portalu Azure. 

Maszynach wirtualnych (VM) platformy Azure używana [dysków](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) jako toostore miejscu systemu operacyjnego, aplikacje i dane. Wszystkie maszyny wirtualne Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym. dysk systemu operacyjnego Hello został początkowo utworzony z obrazu, a zarówno hello dysku systemu operacyjnego i obraz powitania są przechowywane na koncie magazynu Azure wirtualne dyski twarde. Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde.

Jeśli jeszcze tego nie zrobiono, zainstaluj [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Zatrzymaj hello maszyny Wirtualnej

Nie można pobrać wirtualnego dysku twardego z platformy Azure, jeśli jest dołączona tooa uruchamiania maszyny Wirtualnej. Należy toostop hello wirtualna toodownload dysku VHD. Jeśli chcesz toouse wirtualnego dysku twardego [obrazu](tutorial-custom-images.md) toocreate innych maszyn wirtualnych o nowe dyski, należy toodeprovision i uogólnienia systemu operacyjnego hello zawarte w hello plików i Zatrzymaj hello maszyny Wirtualnej. Witaj toouse wirtualnego dysku twardego jako dysk nowe wystąpienie klasy istniejącej maszyny Wirtualnej lub dysku danych, należy tylko toostop i deallocate hello maszyny Wirtualnej.

toouse hello jako toocreate obrazu wirtualnego dysku twardego innych maszyn wirtualnych, wykonaj następujące kroki:

1. Użyj SSH, nazwa konta hello i hello publicznego adresu IP hello wirtualna tooconnect tooit i anulowanie zastrzeżenia go. Witaj + użytkownika parametru spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie. Jeśli poświadczenia konta w toohello maszyny Wirtualnej są pieczenia, Opuść to + parametr użytkownika. Witaj poniższy przykład umożliwia usunięcie ostatnie konto użytkownika elastycznie hello:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Zaloguj się tooyour konto platformy Azure z [logowania az](https://docs.microsoft.com/cli/azure/#login).
3. Zatrzymaj i cofnięcia przydzielenia hello maszyny Wirtualnej.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Generalize hello maszyny Wirtualnej. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

toouse hello wirtualny dysk twardy jako dysk dla nowego wystąpienia istniejącej maszyny Wirtualnej lub dysku danych, wykonaj następujące kroki:

1.  Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2.  W menu Centrum powitania kliknij **maszyn wirtualnych**.
3.  Wybierz hello maszyny Wirtualnej z listy hello.
4.  W bloku hello hello maszyny Wirtualnej, kliknij **zatrzymać**.

    ![Zatrzymanie maszyny Wirtualnej](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Generowania adresu URL SAS

toodownload hello pliku VHD, należy toogenerate [sygnatury dostępu współdzielonego (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) adresu URL. Podczas generowania adresu URL hello czas wygaśnięcia jest przypisany toohello adresu URL.

1.  W menu hello hello bloku hello maszyny Wirtualnej, kliknij polecenie **dysków**.
2.  Wybierz dysk systemu operacyjnego hello hello maszyny Wirtualnej, a następnie kliknij przycisk **wyeksportować**.
3.  Kliknij przycisk **generowania adresu URL**.

    ![Generowania adresu URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Pobierz wirtualnego dysku twardego

1.  W obszarze hello adres URL, który został wygenerowany kliknij plik VHD hello pobierania.

    ![Pobierz wirtualnego dysku twardego](./media/download-vhd/export-download.png)

2.  Może być konieczne tooclick **zapisać** w hello przeglądarki toostart hello pobierania. Domyślna nazwa pliku VHD hello Hello jest *abcd*.

    ![Kliknij przycisk Zapisz w przeglądarce hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak za[przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku z hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Zarządzanie hello Azure dysków Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

