---
title: aaaDownload dysku VHD systemu Windows z platformy Azure | Dokumentacja firmy Microsoft
description: "Pobierz dysku VHD systemu Windows przy użyciu hello portalu Azure."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Pobierz zestaw Windows wirtualnego dysku twardego z platformy Azure

W tym artykule dowiesz się, jak toodownload [Windows wirtualnego dysku twardego (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pliku z platformy Azure przy użyciu hello portalu Azure. 

Maszynach wirtualnych (VM) platformy Azure używana [dysków](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) jako toostore miejscu systemu operacyjnego, aplikacje i dane. Wszystkie maszyny wirtualne Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym. dysk systemu operacyjnego Hello został początkowo utworzony z obrazu, a zarówno hello dysku systemu operacyjnego i obraz powitania są przechowywane na koncie magazynu Azure wirtualne dyski twarde. Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde.

## <a name="stop-hello-vm"></a>Zatrzymaj hello maszyny Wirtualnej

Nie można pobrać wirtualnego dysku twardego z platformy Azure, jeśli jest dołączona tooa uruchamiania maszyny Wirtualnej. Należy toostop hello wirtualna toodownload dysku VHD. Jeśli chcesz toouse wirtualnego dysku twardego [obrazu](tutorial-custom-images.md) toocreate innych maszyn wirtualnych o nowe dyski, użyj [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello systemu operacyjnego znajdującego się w pliku hello, a następnie zatrzymać hello maszyny Wirtualnej. Witaj toouse wirtualnego dysku twardego jako dysk nowe wystąpienie klasy istniejącej maszyny Wirtualnej lub dysku danych, należy tylko toostop i deallocate hello maszyny Wirtualnej.

toouse hello jako toocreate obrazu wirtualnego dysku twardego innych maszyn wirtualnych, wykonaj następujące kroki:

1.  Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com/).
2.  [Połącz toohello wirtualna](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  Na powitania maszyny Wirtualnej Otwórz okno wiersza polecenia hello jako administrator.
4.  Zmień katalog hello zbyt*%windir%\system32\sysprep* i uruchom sysprep.exe.
5.  Okno dialogowe narzędzia przygotowywania systemu hello, wybierz **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że **Generalize** jest zaznaczone.
6.  Wybierz opcje zamykania **zamknięcia**, a następnie kliknij przycisk **OK**. 

toouse hello wirtualny dysk twardy jako dysk dla nowego wystąpienia istniejącej maszyny Wirtualnej lub dysku danych, wykonaj następujące kroki:

1.  W menu Centrum hello w hello portalu Azure kliknij **maszyn wirtualnych**.
2.  Wybierz hello maszyny Wirtualnej z listy hello.
3.  W bloku hello hello maszyny Wirtualnej, kliknij **zatrzymać**.

    ![Zatrzymanie maszyny Wirtualnej](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Generowania adresu URL SAS

toodownload hello pliku VHD, należy toogenerate [sygnatury dostępu współdzielonego (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) adresu URL. Podczas generowania adresu URL hello czas wygaśnięcia jest przypisany toohello adresu URL.

1.  W menu hello hello bloku hello maszyny Wirtualnej, kliknij polecenie **dysków**.
2.  Wybierz dysk systemu operacyjnego hello hello maszyny Wirtualnej, a następnie kliknij przycisk **wyeksportować**.
3.  Ustawianie czasu wygaśnięcia hello hello adresu URL za*36000*.
4.  Kliknij przycisk **generowania adresu URL**.

    ![Generowania adresu URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> czas wygaśnięcia Hello jest zwiększona z tooprovide domyślne hello wystarczająco dużo czasu toodownload hello dużego pliku wirtualnego dysku twardego systemu operacyjnego Windows Server. Można oczekiwać, że plik wirtualnego dysku twardego, który zawiera tootake systemu operacyjnego Windows Server hello kilka toodownload godzin w zależności od połączenia. Jeśli pobierasz dysku VHD dla dysku danych hello domyślny czas jest wystarczająca. 
> 
> 

## <a name="download-vhd"></a>Pobierz wirtualnego dysku twardego

1.  W obszarze hello adres URL, który został wygenerowany kliknij plik VHD hello pobierania.

    ![Pobierz wirtualnego dysku twardego](./media/download-vhd/export-download.png)

2.  Może być konieczne tooclick **zapisać** w hello przeglądarki toostart hello pobierania. Domyślna nazwa pliku VHD hello Hello jest *abcd*.

    ![Kliknij przycisk Zapisz w przeglądarce hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak za[przekazać tooAzure pliku wirtualnego dysku twardego](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Tworzenie dysków zarządzanych z niezarządzanego dysków na koncie magazynu](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Zarządzanie dyskami Azure przy użyciu programu PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

