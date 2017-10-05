---
title: "Dołączenie dysku danych do maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak można dołączyć danych do nowego lub istniejącego dysku do maszyny Wirtualnej systemu Linux, w portalu Azure przy użyciu modelu wdrażania Menedżera zasobów."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a>Jak można dołączyć dysku danych do maszyny Wirtualnej systemu Linux, w portalu Azure
W tym artykule przedstawiono sposób dołączyć istniejących i nowych dysków do maszyny wirtualnej systemu Linux za pośrednictwem portalu Azure. Możesz również [dołączenie dysku danych do maszyny Wirtualnej systemu Windows w portalu Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Można użyć Azure dysków zarządzane lub niezarządzane dysków. Dyski zarządzane są obsługiwane przez platformę Azure i nie wymagają wszystkie lub lokalizację do przechowywania ich. Niezarządzane dyski wymagają konta magazynu i mają pewne [przydziały i ograniczenia, które są stosowane](../../azure-subscription-service-limits.md#storage-limits). Aby uzyskać więcej informacji o dyskach Azure Managed Disks, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md).

Przed dołączeniem dysków do maszyny Wirtualnej, przejrzyj następujące wskazówki:

* Rozmiar maszyny wirtualnej Określa, ile można dołączać dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Aby użyć magazyn w warstwie Premium, należy serii DS lub GS-series maszyny wirtualnej. Można użyć zarówno Premium i standardowa dysków z tych maszyn wirtualnych. Magazyn w warstwie Premium jest dostępna w pewnych regionach. Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Dysków dołączonych do maszyn wirtualnych są faktycznie pliki VHD przechowywane na platformie Azure. Aby uzyskać więcej informacji, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-the-virtual-machine"></a>Znaleźć maszyny wirtualnej
1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
2. W menu Centrum kliknij pozycję **Virtual Machines**.
3. Wybierz maszynę wirtualną z listy.
4. Do wirtualnej maszyny bloku, w **Essentials**, kliknij przycisk **dysków**.
   
    ![Otwórz ustawienia dysku](./media/attach-disk-portal/find-disk-settings.png)

Kontynuuj przez następujące instrukcje dotyczące dołączania albo [dysków zarządzanych w](#use-azure-managed-disks) lub [niezarządzane dysku](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Użyj zarządzanego dysku systemu Azure

### <a name="attach-a-new-disk"></a>Dołączanie nowego dysku

1. Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Kliknij menu rozwijane dla **nazwa** i wybierz **Tworzenie dysku**:

    ![Utwórz Azure dysków zarządzanych](./media/attach-disk-portal/create-new-md.png)

3. Wprowadź nazwę dysku zarządzanego. Przejrzyj ustawienia domyślne, należy zaktualizować odpowiednio do potrzeb, a następnie kliknij **Utwórz**.
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/create-new-md-settings.png)

4. Kliknij przycisk **zapisać** do tworzenia dysków zarządzanych i aktualizowania konfiguracji maszyny Wirtualnej:

   ![Zapisz nowy dysk zarządzane Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. Po Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**. Dyski zarządzane są zasobem najwyższego poziomu dysku pojawia się w katalogu głównym grupy zasobów:

   ![Dysku platformy Azure zarządzanych w grupie zasobów](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Dołączanie istniejącego dysku
1. Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Kliknij menu rozwijane dla **nazwa** Aby wyświetlić listę istniejących dysków zarządzanych dostępny dla Twojej subskrypcji platformy Azure. Wybierz zarządzane dysku, aby dołączyć:

   ![Dołączanie istniejącego dysku zarządzanego Azure](./media/attach-disk-portal/select-existing-md.png)

3. Kliknij przycisk **zapisać** dołączyć istniejącego dysku zarządzanego i zaktualizować konfiguracji maszyny Wirtualnej:
   
   ![Zapisanie aktualizacji dysku zarządzanego Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Po Azure dołącza dysk do maszyny wirtualnej, jest wymienione w ustawieniach dysku maszyny wirtualnej w obszarze **dysków z danymi**.

## <a name="use-unmanaged-disks"></a>Niezarządzane dysków

### <a name="attach-a-new-disk"></a>Dołączanie nowego dysku

1. Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Przejrzyj ustawienia domyślne, należy zaktualizować odpowiednio do potrzeb, a następnie kliknij **OK**.
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-new.png)
3. Po Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.

### <a name="attach-an-existing-disk"></a>Dołączanie istniejącego dysku
1. Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **pliku VHD**.
   
   ![Dołączanie istniejącego dysku](./media/attach-disk-portal/attach-existing.png)
3. W obszarze **kont magazynu**, wybierz konto i kontener, który zawiera plik VHD.
   
   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk-portal/find-storage-container.png)
4. Wybierz plik VHD.
5. W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik jest wyświetlana w obszarze **pliku VHD**. Kliknij przycisk **OK**.
6. Po Azure dołącza dysk do maszyny wirtualnej, jest wymienione w ustawieniach dysku maszyny wirtualnej w obszarze **dysków z danymi**.


## <a name="next-steps"></a>Następne kroki
Po dodaniu dysku, należy przygotować go do użycia. Aby uzyskać więcej informacji, zobacz [porady: inicjowanie nowy dysk danych w systemie Linux](add-disk.md).
