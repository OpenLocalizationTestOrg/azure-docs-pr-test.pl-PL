---
title: aaaAttach tooa dysku danych maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Jak tooattach danych nowego lub istniejącego dysku tooa maszyny Wirtualnej systemu Linux w hello przy użyciu portalu Azure hello modelu wdrażania usługi Resource Manager."
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
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Jak tooattach danych na dysku tooa maszyny Wirtualnej systemu Linux w hello portalu Azure
W tym artykule opisano, jak tooattach istniejących i nowych dysków maszyny wirtualnej systemu Linux tooa za pośrednictwem hello portalu Azure. Możesz również [dołączyć tooa dysku danych maszyny Wirtualnej systemu Windows w portalu Azure hello](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Możesz wybrać toouse albo Azure dysków zarządzanych lub niezarządzanych dysków. Zarządzane dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je. Niezarządzane dyski wymagają konta magazynu i mają pewne [przydziały i ograniczenia, które są stosowane](../../azure-subscription-service-limits.md#storage-limits). Aby uzyskać więcej informacji o dyskach Azure Managed Disks, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md).

Przed dołączeniem tooyour dysków maszyny Wirtualnej, przejrzyj te wskazówki:

* Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Magazyn w warstwie Premium toouse, należy serii DS lub GS-series maszyny wirtualnej. Można użyć zarówno Premium i standardowa dysków z tych maszyn wirtualnych. Magazyn w warstwie Premium jest dostępna w pewnych regionach. Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Maszyny toovirtual dołączone dyski są faktycznie pliki VHD przechowywane na platformie Azure. Aby uzyskać więcej informacji, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Znajdź hello maszyny wirtualnej
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **maszyn wirtualnych**.
3. Wybierz maszynę wirtualną hello z listy hello.
4. toohello wirtualnej maszyny bloku, w **Essentials**, kliknij przycisk **dysków**.
   
    ![Otwórz ustawienia dysku](./media/attach-disk-portal/find-disk-settings.png)

Kontynuuj przez następujące instrukcje dotyczące dołączania albo [dysków zarządzanych w](#use-azure-managed-disks) lub [niezarządzane dysku](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Użyj zarządzanego dysku systemu Azure

### <a name="attach-a-new-disk"></a>Dołączanie nowego dysku

1. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Kliknij menu rozwijanego hello **nazwa** i wybierz **Tworzenie dysku**:

    ![Utwórz Azure dysków zarządzanych](./media/attach-disk-portal/create-new-md.png)

3. Wprowadź nazwę dysku zarządzanego. Przejrzyj ustawienia domyślne hello, zaktualizuj odpowiednio do potrzeb, a następnie kliknij **Utwórz**.
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/create-new-md-settings.png)

4. Kliknij przycisk **zapisać** toocreate hello zarządzane dysku i aktualizacji konfiguracji maszyny Wirtualnej hello:

   ![Zapisz nowy dysk zarządzane Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**. Dyski zarządzane są zasobem najwyższego poziomu, hello dysk zostanie wyświetlony w głównym hello hello grupy zasobów:

   ![Dysku platformy Azure zarządzanych w grupie zasobów](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Dołączanie istniejącego dysku
1. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Kliknij menu rozwijanego hello **nazwa** tooview listę istniejących zarządzane tooyour dostępne dyski subskrypcji platformy Azure. Wybierz hello zarządzane tooattach dysku:

   ![Dołączanie istniejącego dysku zarządzanego Azure](./media/attach-disk-portal/select-existing-md.png)

3. Kliknij przycisk **zapisać** istniejących hello tooattach zarządzane dysku i aktualizacji konfiguracji maszyny Wirtualnej hello:
   
   ![Zapisanie aktualizacji dysku zarządzanego Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Po Azure dołącza hello maszyny wirtualnej toohello dysku, znajduje się w ustawieniach dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.

## <a name="use-unmanaged-disks"></a>Niezarządzane dysków

### <a name="attach-a-new-disk"></a>Dołączanie nowego dysku

1. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. Przejrzyj ustawienia domyślne hello, zaktualizuj odpowiednio do potrzeb, a następnie kliknij **OK**.
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-new.png)
3. Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.

### <a name="attach-an-existing-disk"></a>Dołączanie istniejącego dysku
1. Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.
2. W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **pliku VHD**.
   
   ![Dołączanie istniejącego dysku](./media/attach-disk-portal/attach-existing.png)
3. W obszarze **kont magazynu**, wybierz konto hello i kontener, który zawiera plik VHD hello.
   
   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk-portal/find-storage-container.png)
4. Wybierz plik VHD hello.
5. W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik hello jest wyświetlana w obszarze **pliku VHD**. Kliknij przycisk **OK**.
6. Po Azure dołącza hello maszyny wirtualnej toohello dysku, znajduje się w ustawieniach dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.


## <a name="next-steps"></a>Następne kroki
Po dodaniu dysku hello należy tooprepare go do użycia. Aby uzyskać więcej informacji, zobacz [porady: inicjowanie nowy dysk danych w systemie Linux](add-disk.md).
