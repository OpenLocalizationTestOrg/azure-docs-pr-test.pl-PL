---
title: aaaDetach dysku danych maszyny wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się toodetach dysku danych od maszyny wirtualnej na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Jak toodetach danych na dysku z maszyny wirtualnej systemu Windows
Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej, możesz ją łatwo odłączyć. Usuwa dysk hello z hello maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu.

> [!WARNING]
> Jeśli możesz odłączyć dysk, który nie jest automatycznie usuwana. Jeśli masz subskrypcję magazynu tooPremium, będzie nadal opłaty za magazyn tooincur hello dysku. Aby uzyskać więcej informacji można znaleźć zbyt[cennik i rozliczenia w przypadku korzystania z magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny wirtualnej lub innej.

## <a name="detach-a-data-disk-using-hello-portal"></a>Odłączyć dysku danych przy użyciu portalu hello
1. W portalu Centrum hello, wybierz **maszyn wirtualnych**.
2. Wybierz maszynę wirtualną hello, która ma dysk danych hello toodetach i kliknij **zatrzymać** hello toodeallocate maszyny Wirtualnej.
3. W bloku maszyny wirtualnej hello, wybierz **dysków**.
4. U góry hello hello **dysków** bloku, wybierz opcję **Edytuj**.
5. W hello **dysków** bloku toohello prawej krawędzi hello dysku danych chcesz toodetach, kliknij przycisk hello ![obraz przycisku Detach](./media/detach-disk/detach.png) odłączyć przycisku.
5. Po usunięciu hello dysku, kliknij przycisk Zapisz u góry hello hello bloku.
6. W bloku maszyny wirtualnej powitania kliknij **omówienie** , a następnie kliknij przycisk hello **Start** u góry hello hello bloku toorestart hello maszyny Wirtualnej.



dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.

## <a name="detach-a-data-disk-using-powershell"></a>Odłączyć dysku danych przy użyciu programu PowerShell
W tym przykładzie hello pierwsze polecenie pobiera hello maszyny wirtualnej o nazwie **MyVM07** w hello **RG11** za pomocą polecenia cmdlet Get-AzureRmVM hello grupy zasobów. Witaj polecenie sklepach hello maszyny wirtualnej w hello **$VirtualMachine** zmiennej.

drugie polecenie Hello usuwa hello dysku danych o nazwie DataDisk3 z hello maszyny wirtualnej.

polecenie końcowego Hello aktualizuje stan hello hello maszyny wirtualnej toocomplete hello proces usuwania dysku z danymi hello.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Aby uzyskać więcej informacji, zobacz [AzureRmVMDataDisk Usuń](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz dysku danych hello tooreuse został właśnie [dołączenie go tooanother maszyny Wirtualnej](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

