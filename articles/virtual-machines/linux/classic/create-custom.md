---
title: "aaaCreate klasyczne maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 hello klasycznego modelu wdrożenia"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Jak tooCreate a klasyczne maszyny Wirtualnej systemu Linux z hello Azure CLI w wersji 1.0
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Wersja hello Menedżera zasobów dla [tutaj](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

W tym temacie opisano, jak toocreate maszyny wirtualnej systemu Linux (VM) z hello Azure CLI 1.0 za pomocą hello klasycznego modelu wdrożenia. Używamy obrazu systemu Linux, z hello dostępne **obrazów** na platformie Azure. polecenia Hello Azure CLI 1.0 podać hello następujące opcje konfiguracji, między innymi:

* Łączenie sieci wirtualnej tooa hello maszyny Wirtualnej
* Dodawanie hello wirtualna tooan istniejącą usługę w chmurze
* Dodawanie hello wirtualna tooan istniejącego konta magazynu
* Dodawanie zestawu dostępności tooan wirtualna hello lub lokalizacji

> [!IMPORTANT]
> Jeśli chcesz toouse Twojego wirtualna sieć wirtualną do połączenia się tooit bezpośrednio przez hosta lub konfigurowanie połączeń między różnymi lokalizacjami, upewnij się, że hello sieci wirtualnej można określić podczas tworzenia hello maszyny Wirtualnej. Maszyny Wirtualnej może być skonfigurowany toojoin sieci wirtualnej wyłącznie w przypadku utworzenia hello maszyny Wirtualnej. Aby uzyskać szczegółowe informacje w sieciach wirtualnych, zobacz [omówienie sieci wirtualnych Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Jak toocreate a maszyny Wirtualnej systemu Linux przy użyciu hello klasycznego modelu wdrożenia
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

