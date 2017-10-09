---
title: "aaaUpload wirtualnego dysku twardego pliku tooAzure DevTest Labs za pomocą Eksploratora usługi Microsoft Azure Storage | Dokumentacja firmy Microsoft"
description: "Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu Eksploratora magazynu Microsoft Azure"
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu Eksploratora magazynu Microsoft Azure

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego mogą być używane toocreate niestandardowych obrazów, które są używane tooprovision maszyn wirtualnych. W tym artykule przedstawiono sposób toouse [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) konta magazynu laboratorium tooa pliku tooupload dysku VHD. Po przesłaniu pliku wirtualnego dysku twardego hello [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób toocreate niestandardowego obrazu z hello przekazany plik VHD. Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

Witaj, wykonując kroki przeszukiwania plików podczas przekazywania wirtualnego dysku twardego Labs tooDevTest przy użyciu [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Pobierz i zainstaluj najnowszą wersję hello Eksploratora usługi Microsoft Azure Storage hello](http://www.storageexplorer.com).

1. Pobierz hello nazwę konta magazynu laboratorium hello za pośrednictwem hello portalu Azure:

    1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
    
    1. Z listy hello labs wybierz żądany laboratorium hello.  
    
    1. W bloku hello laboratorium, wybierz **konfiguracji**. 
    
    1. W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.
    
    1. Na powitania **niestandardowych obrazów** bloku, wybierz **+ Dodaj**. 
    
    1. Na powitania **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.
    
    1. Na powitania **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.
    
        ![Przekaż plik VHD za pomocą programu PowerShell][0]
    
    1. Witaj **przekazywanie obrazu za pomocą programu PowerShell** bloku Wyświetla toohello wywołania **Add-AzureVhd** polecenia cmdlet. Witaj pierwszy parametr (*docelowego*) zawiera nazwę konta magazynu hello laboratorium hello w hello następującego formatu:
    
        https://<Storage-ACCOUNT-name>.blob.Core.Windows.NET/Uploads/... 

    1. Zwróć uwagę na nazwy konta magazynu hello, ponieważ jest używana w dalszych krokach.
    
1. Połącz tooan konta subskrypcji platformy Azure przy użyciu Eksploratora usługi Storage.

    > [!TIP] 
    > 
    > Eksplorator usługi Storage obsługuje kilka opcji połączeń. W tej części przedstawiono łączącego tooa konta magazynu skojarzone z subskrypcją platformy Azure. toosee hello inne opcje połączenia obsługiwane przez Eksploratora usługi Storage, zobacz artykuł toohello [wprowadzenie do Eksploratora usługi Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Otwórz Eksploratora usługi Storage.
    
    1. W Eksploratorze usługi Storage, wybierz **ustawienia konta Azure**. 
    
        ![Ustawienia konta platformy Azure][1]
    
    1. w okienku po lewej stronie powitania Wyświetla kont Microsoft hello, do których logujesz się do. Konto tooanother tooconnect, wybierz opcję **Dodaj konto**i wykonaj hello toosign okien dialogowych za pomocą konta Microsoft, który jest skojarzony z co najmniej jedną aktywną subskrypcją platformy Azure.
    
        ![Dodaj konto][2]
    
    1. Po pomyślnym zalogowaniu się przy użyciu konta Microsoft, w okienku po lewej stronie powitania wypełnia hello subskrypcji platformy Azure skojarzonych z tym kontem. Wybierz hello subskrypcji platformy Azure, z którymi mają toowork, a następnie wybierz **Zastosuj**. (Wybieranie **wszystkie subskrypcje** przełącza hello wybór wszystkich lub brak hello wymienionych subskrypcji platformy Azure.)
    
        ![Wybieranie subskrypcji platformy Azure][3]
    
    1. w okienku po lewej stronie powitania Wyświetla hello konta magazynu skojarzone z hello wybrane subskrypcje platformy Azure.
    
        ![Wybrane subskrypcje platformy Azure][4]

1. Zlokalizuj konto magazynu laboratorium hello:

    1. W okienku po lewej stronie Eksploratora usługi Storage hello Znajdź i rozwinąć węzeł hello hello subskrypcji platformy Azure, który jest właścicielem hello laboratorium.
    
    1. W węźle subskrypcji hello rozwiń **kont magazynu**.

    1. Rozwiń węzły konta magazynu laboratorium hello tooreveal węzła dla **kontenerów obiektów Blob**, **udziałów plików**, **kolejek**, i **tabel**.
    
    1. Rozwiń węzeł hello **kontenerów obiektów Blob** węzła.
    
    1. Zaznacz zawartością toodisplay kontenera obiektów blob przekazywania hello w okienku po prawej stronie powitania.
        
        ![Przekaż katalogu][5]

1. Przekaż plik VHD hello za pomocą Eksploratora usługi Storage:

    1. W prawym okienku Eksploratora usługi Storage hello powinna zostać wyświetlona listę obiektów blob hello w hello **przekazuje** kontenera obiektów blob z konta magazynu laboratorium hello. Na powitania paska narzędzi edytora obiektów blob, wybierz **Przekaż** 
        
        ![Przekaż przycisku][6]
    
    1. Z hello **przekazać** menu rozwijanego wybierz **przekazywania plików...** .
    
    1. Na powitania **przekazać pliki** okno dialogowe, wybierz hello wielokropka.
        
        ![Wybierz plik][8]  

    1. Na powitania **tooupload wybierz pliki** okna dialogowego, przeglądania toohello żądanego pliku VHD, zaznacz go, a następnie wybierz **Otwórz**.
    
    1. Gdy zwrócił toohello **przekazać pliki** okna dialogowego, zmień **typu obiektu Blob** za**stronicowych obiektów Blob**.
    
    1. Wybierz pozycję **Przekaż**.

        ![Wybierz plik][9]  
    
    1. Witaj Eksploratora usługi Storage **dziennik aktywności** w okienku zostaną wyświetlone stan pobierania hello (wraz z łącza toocancel hello przekazywania). proces Hello przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru hello hello pliku wirtualnego dysku twardego i szybkość połączenia. 

        ![Stan przekazywania pliku][10]  

## <a name="next-steps"></a>Następne kroki

- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą hello portalu Azure](devtest-lab-create-template.md)
- [Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
