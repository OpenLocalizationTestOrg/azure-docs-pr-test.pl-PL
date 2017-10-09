---
title: "aaaCreate i przekazywanie maszyny Wirtualnej obrazu przy użyciu programu Powershell | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate i przekaż uogólniony obraz systemu Windows Server (VHD) przy użyciu hello klasycznego modelu wdrażania i programu Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego z systemem Windows Server
W tym artykule opisano, jak tooupload własne uogólniony maszyny Wirtualnej obrazu jako wirtualny dysk twardy (VHD), można użyć toocreate maszyn wirtualnych. Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde w systemie Microsoft Azure, zobacz [o dyski i wirtualne dyski twarde dla maszyn wirtualnych](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Możesz również [przekazać](../upload-generalized-managed.md) maszyny wirtualnej z wykorzystaniem hello modelu Resource Manager.

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że masz:

* **Subskrypcja platformy Azure** — Jeśli nie masz, możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -masz hello Microsoft Azure PowerShell modułu zainstalowany i skonfigurowany toouse subskrypcji.
* **A. Plik VHD** — obsługiwane systemu operacyjnego przechowywanego w pliku VHD i maszyny wirtualnej podłączone tooa Windows. Określ, czy toosee hello ról serwera uruchomionych na powitania wirtualnego dysku twardego są obsługiwane przez program Sysprep. Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > Hello VHDX format nie jest obsługiwany w systemie Microsoft Azure. Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello [polecenia cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Aby uzyskać więcej informacji, zobacz [wpis w blogu](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>Krok 1: Przygotowywanie hello wirtualnego dysku twardego
Przed przekazaniem hello tooAzure wirtualnego dysku twardego, musi on toobe uogólniony przy użyciu narzędzia Sysprep hello. — Przygotowanie toobe wirtualnego dysku twardego hello użyty jako obraz. Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx). Utwórz kopię zapasową hello maszyny Wirtualnej przed uruchomieniem programu Sysprep.

Aby ukończyć powitalnych procedury został zainstalowany z hello maszyny wirtualnej, która hello systemu operacyjnego:

1. Zaloguj się toohello systemu operacyjnego.
2. Otwórz okno wiersza polecenia z uprawnieniami administratora. Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.

    ![Otwórz okno wiersza polecenia](./media/createupload-vhd/sysprep_commandprompt.png)
3. Witaj **narzędzie przygotowania systemu** zostanie wyświetlone okno dialogowe.

   ![Uruchom program Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. W hello **narzędzie przygotowania systemu**, wybierz pozycję **wprowadź systemu poza środowisko pola (OOBE)** i upewnij się, że **Generalize** jest zaznaczony.
5. W **opcje zamykania**, wybierz pozycję **zamknięcia**.
6. Kliknij przycisk **OK**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Krok 2: Tworzenie konta magazynu i kontener
Należy konto magazynu na platformie Azure, więc plik VHD hello tooupload miejsce. W tym kroku przedstawiono sposób toocreate konta lub get hello informacje z istniejącego konta. Zastąp zmienne hello w &lsaquo; nawiasy &rsaquo; odpowiednimi informacjami.

1. Login

    ```powershell
    Add-AzureAccount
    ```

2. Ustaw subskrypcji platformy Azure.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Utwórz nowe konto magazynu. Nazwa Hello hello konta magazynu powinna być unikatowa, 3 do 24 znaków. Nazwa Hello może być dowolną kombinacją liter i cyfr. Należy również toospecify lokalizacji, takiej jak "Wschód nam"

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Ustaw nowe konto magazynu hello jako domyślne hello.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Utwórz nowy kontener.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Krok 3: Przekaż plik VHD hello
Użyj hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello wirtualnego dysku twardego.

Z okna programu Azure PowerShell hello używany w poprzednim kroku hello, typ hello następujące polecenie i Zastąp zmienne hello w &lsaquo; nawiasy &rsaquo; odpowiednimi informacjami.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Krok 4: Dodawanie listy tooyour obrazów hello niestandardowych obrazów
Użyj hello [AzureVMImage Dodaj](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) polecenia cmdlet tooadd hello obrazu toohello listy obrazów niestandardowych.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Następne kroki
Możesz teraz [Tworzenie niestandardowych maszyny Wirtualnej](createportal.md) przy użyciu hello można przekazać obrazu.
