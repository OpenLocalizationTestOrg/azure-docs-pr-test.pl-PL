---
title: "aaaSet się punkty końcowe w klasycznym maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooset się punktów końcowych dla maszyny Wirtualnej systemu Linux w hello Azure classic portal tooallow komunikacji z maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Jak tooset się punkty końcowe w klasycznym maszyny wirtualnej systemu Linux na platformie Azure
Wszystkie maszyny wirtualne systemu Linux utworzone na platformie Azure przy użyciu hello klasycznego modelu wdrażania może komunikować się automatycznie kanałem sieci prywatnej innym maszynom wirtualnym w hello się, że takie same w chmurze, usługi lub wirtualnych sieci. Jednak komputery na powitania Internet lub innych sieci wirtualnych wymagają punkty końcowe toodirect hello ruchu przychodzącego ruchu tooa maszyny wirtualnej. W tym artykule jest również dostępny do [maszyn wirtualnych Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

W hello **Resource Manager** model wdrażania, punkty końcowe są skonfigurowane przy użyciu **grup zabezpieczeń sieci (NSG)**. Aby uzyskać więcej informacji, zobacz [Otwieranie portów i punkty końcowe](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Po utworzeniu maszyny wirtualnej systemu Linux w portalu Azure hello punkt końcowy dla protokołu Secure Shell (SSH) jest zwykle tworzony automatycznie. Podczas tworzenia maszyny wirtualnej hello lub później w razie potrzeby można skonfigurować dodatkowe punkty końcowe.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Następne kroki
* Punkt końcowy maszyny Wirtualnej można również utworzyć za pomocą hello [interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Uruchom hello **utworzyć punktu końcowego maszyny wirtualnej azure** polecenia.
* Jeśli utworzono maszynę wirtualną w modelu wdrażania usługi Resource Manager hello hello wiersza polecenia platformy Azure w trybie Menedżera zasobów można użyć zbyt[Utwórz grupy zabezpieczeń sieci](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol toohello ruch maszyny Wirtualnej.
