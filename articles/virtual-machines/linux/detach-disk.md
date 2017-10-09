---
title: aaaDetach dysku danych maszyny wirtualnej systemu Linux - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się toodetach dysku danych od maszyny wirtualnej na platformie Azure przy użyciu interfejsu wiersza polecenia w wersji 2.0 lub hello portalu Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Jak toodetach danych na dysku od maszyny wirtualnej systemu Linux

Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej, możesz ją łatwo odłączyć. Usuwa dysk hello z hello maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu. 

> [!WARNING]
> Jeśli możesz odłączyć dysk, który nie jest automatycznie usuwana. Jeśli masz subskrypcję magazynu tooPremium, będzie nadal opłaty za magazyn tooincur hello dysku. Aby uzyskać więcej informacji można znaleźć zbyt[cennik i rozliczenia w przypadku korzystania z magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny wirtualnej lub innej.  

## <a name="detach-a-data-disk-using-cli-20"></a>Odłączyć dysku danych przy użyciu interfejsu wiersza polecenia 2.0

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.


## <a name="detach-a-data-disk-using-hello-portal"></a>Odłączyć dysku danych przy użyciu portalu hello
1. W portalu Centrum hello, wybierz **maszyn wirtualnych**.
2. Wybierz maszynę wirtualną hello, która ma dysk danych hello toodetach i kliknij **zatrzymać** hello toodeallocate maszyny Wirtualnej.
3. W bloku maszyny wirtualnej hello, wybierz **dysków**.
4. U góry hello hello **dysków** bloku, wybierz opcję **Edytuj**.
5. W hello **dysków** bloku toohello prawej krawędzi hello dysku danych chcesz toodetach, kliknij przycisk hello ![obraz przycisku Detach](./media/detach-disk/detach.png) odłączyć przycisku.
5. Po usunięciu hello dysku, kliknij przycisk Zapisz u góry hello hello bloku.
6. W bloku maszyny wirtualnej powitania kliknij **omówienie** , a następnie kliknij przycisk hello **Start** u góry hello hello bloku toorestart hello maszyny Wirtualnej.

dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.








## <a name="next-steps"></a>Następne kroki
Jeśli chcesz dysku danych hello tooreuse został właśnie [dołączenie go tooanother wirtualna](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

