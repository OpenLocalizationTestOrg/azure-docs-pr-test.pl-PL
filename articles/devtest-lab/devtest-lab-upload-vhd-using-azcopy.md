---
title: "Przekaż plik VHD na przy użyciu narzędzia AzCopy usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Przekaż plik VHD na konto magazynu w laboratorium, przy użyciu narzędzia AzCopy"
services: devtest-lab,virtual-machines
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: v-craic
ms.openlocfilehash: 11a9d03e62c674c4311c74f78e4cb2e709940941
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2018
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a>Przekaż plik VHD na konto magazynu w laboratorium, przy użyciu narzędzia AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego może służyć do tworzenia niestandardowych obrazów, które są używane do obsługi administracyjnej maszyn wirtualnych. W poniższych krokach objaśniono przy użyciu wiersza polecenia azcopy do przekazania pliku wirtualnego dysku twardego do konta magazynu laboratorium. Po przesłaniu pliku wirtualnego dysku twardego [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób tworzenia niestandardowego obrazu z przekazanego pliku wirtualnego dysku twardego. Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> Narzędzie AzCopy to narzędzie wiersza polecenia systemu Windows.

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

W poniższych krokach objaśniono za pośrednictwem przekazywania pliku wirtualnego dysku twardego za pomocą usługi Azure DevTest Labs [AzCopy](http://aka.ms/downloadazcopy). 

1. Pobierz nazwę konta magazynu laboratorium należy utworzyć przy użyciu portalu Azure:

1. Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz pozycję **Więcej usług**, a następnie z listy wybierz pozycję **DevTest Labs**.

1. Z listy labs wybierz żądany laboratorium.  

1. W bloku laboratorium, wybierz **konfiguracji**. 

1. W środowisku laboratoryjnym **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.

1. Na **niestandardowych obrazów** bloku, wybierz **+ Dodaj**. 

1. Na **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.

1. Na **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.

    ![Przekaż plik VHD za pomocą programu PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. **Przekazywanie obrazu za pomocą programu PowerShell** bloku Wyświetla wywołanie **Add-AzureVhd** polecenia cmdlet. Pierwszy parametr (*docelowego*) zawiera identyfikator URI dla kontenera obiektów blob (*przekazuje*) w następującym formacie:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Zwróć uwagę na pełny identyfikator URI, ponieważ jest używana w dalszych krokach.

1. Przekaż plik VHD za pomocą narzędzia AzCopy:
 
1. [Pobierz i zainstaluj najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy).

1. Otwórz okno polecenia i przejdź do katalogu instalacyjnego programu AzCopy. Opcjonalnie można dodać lokalizacji instalacji programu AzCopy do ścieżki systemowej. Domyślnie program AzCopy jest instalowany do następującego katalogu:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Przy użyciu konta obiektów blob i kluczy kontenera magazynu identyfikatora URI, uruchom następujące polecenie w wierszu polecenia. *VhdFileName* wartość musi być w cudzysłowie. Proces przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru pliku wirtualnego dysku twardego i szybkość połączenia.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Kolejne kroki

- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą portalu Azure](devtest-lab-create-template.md)
- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)