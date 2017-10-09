---
title: "aaaUpload wirtualnego dysku twardego pliku tooAzure DevTest Labs przy użyciu narzędzia AzCopy | Dokumentacja firmy Microsoft"
description: "Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu narzędzia AzCopy"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu narzędzia AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego mogą być używane toocreate niestandardowych obrazów, które są używane tooprovision maszyn wirtualnych. Hello następujące kroki opisano przy użyciu tooupload narzędzia wiersza polecenia AzCopy hello wirtualnego dysku twardego pliku tooa laboratorium dla konta magazynu. Po przesłaniu pliku wirtualnego dysku twardego hello [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób toocreate niestandardowego obrazu z hello przekazany plik VHD. Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> Narzędzie AzCopy to narzędzie wiersza polecenia systemu Windows.

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

Witaj, wykonując kroki przeszukiwania plików podczas przekazywania wirtualnego dysku twardego tooAzure DevTest Labs przy użyciu [AzCopy](http://aka.ms/downloadazcopy). 

1. Pobierz hello nazwę konta magazynu laboratorium hello za pośrednictwem hello portalu Azure:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.

1. Z listy hello labs wybierz żądany laboratorium hello.  

1. W bloku hello laboratorium, wybierz **konfiguracji**. 

1. W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.

1. Na powitania **niestandardowych obrazów** bloku, wybierz **+ Dodaj**. 

1. Na powitania **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.

1. Na powitania **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.

    ![Przekaż plik VHD za pomocą programu PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Witaj **przekazywanie obrazu za pomocą programu PowerShell** bloku Wyświetla toohello wywołania **Add-AzureVhd** polecenia cmdlet. Witaj pierwszy parametr (*docelowego*) zawiera hello identyfikatora URI dla kontenera obiektów blob (*przekazuje*) w hello następującego formatu:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Zwróć uwagę na powitania pełny identyfikator URI, ponieważ jest używana w dalszych krokach.

1. Przekaż plik VHD hello przy użyciu narzędzia AzCopy:
 
1. [Pobierz i zainstaluj najnowszą wersję programu AzCopy, hello](http://aka.ms/downloadazcopy).

1. Otwórz okno polecenia i przejdź do katalogu instalacyjnego toohello AzCopy. Opcjonalnie można dodać ścieżki systemu tooyour lokalizacji instalacji hello AzCopy. Narzędzie AzCopy jest domyślnie zainstalowany toohello następującego katalogu:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Przy użyciu hello konta obiektów blob i kluczy kontenera magazynu identyfikatora URI, uruchom następujące polecenie w wierszu polecenia hello hello. Witaj *vhdFileName* . wartość musi toobe w cudzysłowy. proces Hello przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru hello hello pliku wirtualnego dysku twardego i szybkość połączenia.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Następne kroki

- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą hello portalu Azure](devtest-lab-create-template.md)
- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)