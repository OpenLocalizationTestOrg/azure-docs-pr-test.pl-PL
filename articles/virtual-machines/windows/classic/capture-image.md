---
title: Obraz maszyny Wirtualnej systemu Windows Azure aaaCapture | Dokumentacja firmy Microsoft
description: "Przechwyć obraz maszyny wirtualnej systemu Windows Azure utworzonych za pomocą hello klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Przechwyć obraz maszyny wirtualnej systemu Windows Azure utworzonych za pomocą hello klasycznego modelu wdrażania.
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Menedżer zasobów modelu informacji, zobacz [Przechwyć obraz zarządzanych uogólniony maszyny wirtualnej na platformie Azure](../capture-image-resource.md).

W tym artykule opisano sposób toocapture Azure maszyny wirtualnej z systemem Windows, można użyć jej jako obraz toocreate innych maszyn wirtualnych. Ten obraz zawiera hello dysku systemu operacyjnego i wszystkich dysków danych, które są dołączone toohello maszyny wirtualnej. Nie ma wśród nich konfiguracje sieci, dlatego potrzebujesz tooset zapasowych konfiguracji sieci, podczas tworzenia hello innych maszyn wirtualnych, korzystających z obrazu hello.

Magazyny Azure hello obrazu w obszarze **obrazów maszyn wirtualnych (klasyczne)**, **obliczeniowe** usługi na liście, podczas wyświetlania wszystkich hello usług platformy Azure. Jest to hello tym samym miejscu, w którym są przechowywane wszystkie obrazy zostały przekazane. Aby uzyskać więcej informacji o obrazach, zobacz [o obrazów maszyn wirtualnych](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Przed rozpoczęciem
Tych krokach przyjęto założenie, że już utworzona maszyna wirtualna platformy Azure i skonfigurować hello systemu operacyjnego, dołączanie dowolnego dysku z danymi. Jeśli to nie zostało to jeszcze zrobione jeszcze, zobacz następujące artykuły, aby uzyskać informacje na temat tworzenia i przygotowywanie maszyny wirtualnej hello hello:

* [Utwórz maszynę wirtualną z obrazu](createportal.md)
* [Jak tooattach danych na dysku tooa maszyny wirtualnej](attach-disk.md)
* Upewnij się, że role serwera hello są obsługiwane przy użyciu narzędzia Sysprep. Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Ten proces powoduje usunięcie hello oryginalna maszyna wirtualna po jego przechwyceniu.
>
>

Wcześniejsze toocapturing jako obraz maszyny wirtualnej platformy Azure, zalecane jest hello docelowej maszyny wirtualnej można wykonać kopii zapasowej. Maszyny wirtualne platformy Azure można kopii zapasowej za pomocą usługi Kopia zapasowa Azure. Aby uzyskać szczegółowe informacje, zobacz [Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure](../../../backup/backup-azure-vms.md). Inne rozwiązania są dostępne u certyfikowanych partnerów. toofind, co jest obecnie dostępna, wyszukaj hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Przechwytywanie maszyny wirtualnej hello
1. W hello [portalu Azure](http://portal.azure.com), **Connect** toohello maszyny wirtualnej. Aby uzyskać instrukcje, zobacz [jak toosign w tooa maszyny wirtualnej z systemem Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Otwórz okno wiersza polecenia z uprawnieniami administratora.
3. Zmień katalog hello zbyt`%windir%\system32\sysprep`, a następnie uruchom sysprep.exe.
4. Witaj **narzędzie przygotowania systemu** zostanie wyświetlone okno dialogowe. Witaj, po:

   * W **Akcja oczyszczania systemu**, wybierz pozycję **wprowadź systemu Out-of-Box Experience (OOBE)** i upewnij się, że **Generalize** jest zaznaczony. Aby uzyskać więcej informacji o korzystaniu z programu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie][How tooUse Sysprep: An Introduction].
   * W **opcje zamykania**, wybierz pozycję **zamknięcia**.
   * Kliknij przycisk **OK**.

   ![Uruchom program Sysprep](./media/capture-image/SysprepGeneral.png)
5. Narzędzie Sysprep zamyka hello maszynę wirtualną, która zmieni hello hello maszyny wirtualnej w portalu Azure hello zbyt**zatrzymane**.
6. W portalu Azure hello, kliknij przycisk **maszyn wirtualnych (klasyczne)** i wybierz hello ma toocapture maszyny wirtualnej. Witaj **obrazów maszyn wirtualnych (klasyczne)** grupy znajduje się w obszarze **obliczeniowe** podczas wyświetlania **więcej usług**.

7. Na pasku poleceń powitania kliknij **przechwytywania**.

   ![Przechwytywanie maszyny wirtualnej](./media/capture-image/CaptureVM.png)

   Witaj **hello Przechwytywanie maszyny wirtualnej** zostanie wyświetlone okno dialogowe.

8. W **nazwa obrazu**, wpisz nazwę nowego obrazu hello. W **etykiety obrazu**, wpisz etykietę hello nowy obraz.

9. Kliknij przycisk **uruchomiono program Sysprep na maszynie wirtualnej hello**. To pole wyboru oznacza toohello akcji przy użyciu narzędzia Sysprep w krokach 3 – 5. Obraz _musi_ uogólnione, uruchamiając program Sysprep przed dodaniem serwera Windows obrazu tooyour zestaw niestandardowych obrazów.

10. Po ukończeniu przechwytywania hello nowy obraz powitania staje się dostępna hello **Marketplace**, w hello **obliczeniowe**, **obrazów maszyn wirtualnych (klasyczne)** kontenera.

    ![Pomyślne przechwytywania obrazu](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Następne kroki
Obraz powitania jest maszyn wirtualnych toocreate gotowe toobe używane. toodo, utworzysz maszynę wirtualną, wybierając hello **więcej usług** element menu u dołu menu usługi hello, następnie hello **obrazów maszyn wirtualnych (klasyczne)** w hello **obliczeniowe**grupy. Aby uzyskać instrukcje, zobacz [Utwórz maszynę wirtualną z obrazu](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
