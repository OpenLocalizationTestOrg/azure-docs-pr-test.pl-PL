---
title: "aaaUpload wirtualnego dysku twardego pliku tooAzure DevTest Labs przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu programu PowerShell"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu programu PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego mogą być używane toocreate niestandardowych obrazów, które są używane tooprovision maszyn wirtualnych. Witaj kolejnych krokach objaśniono sposób przy użyciu programu PowerShell tooupload wirtualnego dysku twardego pliku tooa laboratorium dla konta magazynu. Po przesłaniu pliku wirtualnego dysku twardego hello [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób toocreate niestandardowego obrazu z hello przekazany plik VHD. Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

Witaj następujące kroki przeszukiwania plików podczas przekazywania wirtualnego dysku twardego tooAzure DevTest Labs przy użyciu programu PowerShell. 

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.

1. Z listy hello labs wybierz żądany laboratorium hello.  

1. W bloku hello laboratorium, wybierz **konfiguracji**. 

1. W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.

1. Na powitania **niestandardowych obrazów** bloku, wybierz **+ Dodaj**. 

1. Na powitania **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.

1. Na powitania **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.

    ![Przekaż plik VHD za pomocą programu PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. Na powitania **przekazywanie obrazu za pomocą programu PowerShell** bloku, Edytor tekstu tooa skryptu programu PowerShell hello wygenerowany kopiowania.

1. Modyfikowanie hello **LocalFilePath** parametru hello **Add-AzureVhd** polecenia cmdlet toopoint toohello lokalizacja pliku wirtualnego dysku twardego, który chcesz tooupload hello.

1. W wierszu polecenia programu PowerShell, uruchom hello **Add-AzureVhd** polecenia cmdlet (z hello zmodyfikowane **LocalFilePath** parametru).

> [!WARNING] 
> 
> proces Hello przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru hello hello pliku wirtualnego dysku twardego i szybkość połączenia.

## <a name="next-steps"></a>Następne kroki

- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą hello portalu Azure](devtest-lab-create-template.md)
- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
