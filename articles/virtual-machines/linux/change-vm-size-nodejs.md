---
title: "tooresize aaaHow Maszynę wirtualną systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Jak tooscale zapasowych lub Zmniejsz maszyny wirtualnej systemu Linux, zmieniając hello rozmiar maszyny Wirtualnej."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Zmień rozmiar maszyny Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure 1.0

## <a name="overview"></a>Omówienie

Po udostępnić maszynę wirtualną (VM), można skalować hello maszyny Wirtualnej w górę lub w dół, zmieniając hello [rozmiar maszyny Wirtualnej][vm-sizes]. W niektórych przypadkach należy najpierw cofnąć hello maszyny Wirtualnej. Może to nastąpić, jeśli hello nowy rozmiar jest niedostępny na hello sprzętu klastra, który jest hostem hello maszyny Wirtualnej.

W tym artykule przedstawiono sposób tooresize a maszyny Wirtualnej systemu Linux przy użyciu hello [interfejsu wiersza polecenia Azure][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#resize-a-linux-vm) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="resize-a-linux-vm"></a>Zmień rozmiar maszyny Wirtualnej systemu Linux
tooresize maszyny Wirtualnej, wykonaj hello następujące kroki.

1. Uruchom następujące polecenia interfejsu wiersza polecenia hello. To polecenie wyświetla hello rozmiarów maszyn wirtualnych, które są dostępne w klastrze sprzętu hello gdzie hello maszyny Wirtualnej jest hostowana.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. W razie potrzeby hello znajduje się rozmiar Uruchom hello następujące polecenia tooresize hello maszyny Wirtualnej.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Witaj maszyna wirtualna zostanie ponownie uruchomiona w trakcie tego procesu. Po ponownym uruchomieniu hello z istniejącego systemu operacyjnego i dysków z danymi będzie można ponownie zamapować. Elementy na dysku tymczasowym hello zostaną utracone.
   
    Użyj hello `--enable-boot-diagnostics` powoduje włączenie [diagnostyki rozruchu][boot-diagnostics], toolog żadnych toostartup powiązane błędy.
3. W przeciwnym razie w razie potrzeby hello się, że nie ma rozmiar Uruchom hello następujące polecenia toodeallocate hello maszyny Wirtualnej, jej rozmiar, a następnie ponownie uruchom hello maszyny Wirtualnej.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Cofanie przydziału hello wirtualna zwalnia również dynamiczne adresy IP przypisane toohello maszyny Wirtualnej. nie dotyczy Hello systemu operacyjnego i dysków z danymi.
   > 
   > 

## <a name="next-steps"></a>Następne kroki
Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie. Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Linux maszyny][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
