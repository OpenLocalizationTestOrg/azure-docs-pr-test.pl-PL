---
title: Diagnostyka aaaBoot dla maszyn wirtualnych systemu Linux na platformie Azure | Doc firmy Microsoft
description: "Omówienie Witaj dwie funkcje debugowania dla maszyn wirtualnych systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Jak toouse rozruchu maszyn wirtualnych systemu Linux tootroubleshoot Diagnostyka Azure

Na platformie Azure jest teraz dostępna obsługa dwóch funkcji debugowania: obsługa danych wyjściowych konsoli i zrzutu ekranu dla modelu wdrażania przy użyciu usługi Azure Virtual Machines Resource Manager. 

Podczas przełączania tooAzure własny obraz lub nawet rozruch jeden z obrazów platformy hello, może istnieć wiele przyczyn, dlaczego pobiera maszynę wirtualną do stanu rozruchowego. Te funkcje włączenia należy tooeasily diagnozowanie i odzyskiwanie po błędach rozruchu maszyn wirtualnych.

Dla maszyn wirtualnych systemu Linux można łatwo przeglądać dane wyjściowe hello dziennika konsoli z hello portalu:

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
Jednak dla systemów Windows i maszyn wirtualnych systemu Linux Azure umożliwia również toosee hello maszyny Wirtualnej z funkcji hypervisor hello zrzut ekranu:

![Błąd](./media/boot-diagnostics/screenshot2.png)

Obie te funkcje są obsługiwane dla maszyn wirtualnych platformy Azure we wszystkich regionach. Uwaga, zrzuty ekranu i danych wyjściowych może potrwać too10 tooappear minut na koncie magazynu.

## <a name="common-boot-errors"></a>Typowe błędy rozruchu

- [Zagadnienia dotyczące systemu plików](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Problemy z jądra](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [Błędy FSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Włączanie diagnostyki na nowej maszynie wirtualnej
1. Podczas tworzenia nowej maszyny wirtualnej z hello portalu w wersji zapoznawczej, wybierz hello **usługi Azure Resource Manager** z listy rozwijanej modelu wdrażania hello:
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. Skonfiguruj te pliki diagnostyczne hello miejsce chcesz tooplace monitorowanie opcja tooselect hello magazynu konta.
 
    ![Tworzenie maszyny wirtualnej](./media/boot-diagnostics/screenshot4.jpg)

3. Jeśli wdrażasz za pomocą szablonu usługi Azure Resource Manager, przejdź tooyour zasobu maszyny wirtualnej i Dołącz sekcji profilu diagnostyki hello. Należy pamiętać, nagłówek wersji interfejsu API toouse hello "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. profilu diagnostyki Hello umożliwia konta magazynu hello tooselect miejscu tooput tych dzienników.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Aktualizowanie istniejącej maszyny wirtualnej

diagnostyki rozruchu tooenable za pośrednictwem portalu hello, można także zaktualizować istniejącej maszyny wirtualnej za pośrednictwem portalu hello. Wybierz hello diagnostyki rozruchu opcji i Zapisz. Uruchom ponownie hello wirtualna tootake efekt.

![Aktualizowanie istniejącej maszyny wirtualnej](./media/boot-diagnostics/screenshot5.png)