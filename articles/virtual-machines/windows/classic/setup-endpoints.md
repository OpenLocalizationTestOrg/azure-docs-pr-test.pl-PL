---
title: "aaaSet się punkty końcowe w klasycznym maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooset się punktów końcowych dla maszyny Wirtualnej systemu Windows w hello Azure classic portal tooallow komunikację z maszyną wirtualną systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Jak tooset się punkty końcowe w klasycznym maszyny wirtualnej systemu Windows na platformie Azure
Wszystkich maszyn wirtualnych tworzonych na platformie Azure przy użyciu hello klasycznego modelu wdrażania można automatycznie komunikują się za pośrednictwem kanału między maszynami wirtualnymi w sieci prywatnej systemu Windows hello tej samej usługi w chmurze lub sieci wirtualnej. Jednak komputery na powitania Internet lub innych sieci wirtualnych wymagają punkty końcowe toodirect hello ruchu przychodzącego ruchu tooa maszyny wirtualnej. W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

W hello **Resource Manager** model wdrażania, punkty końcowe są skonfigurowane przy użyciu **grup zabezpieczeń sieci (NSG)**. Aby uzyskać więcej informacji, zobacz [Zezwalaj dostępu zewnętrznego tooyour maszynę Wirtualną przy użyciu hello portalu Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Po utworzeniu maszyny wirtualnej systemu Windows w portalu Azure hello typowych punktów końcowych, takich jak te dotyczące usług pulpitu zdalnego i komunikacji zdalnej programu Windows PowerShell są zazwyczaj tworzone automatycznie. Podczas tworzenia maszyny wirtualnej hello lub później w razie potrzeby można skonfigurować dodatkowe punkty końcowe.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Następne kroki
* toouse tooset polecenia cmdlet programu Azure PowerShell się punkt końcowy maszyny Wirtualnej, zobacz [AzureEndpoint Dodaj](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse toomanage polecenia cmdlet programu Azure PowerShell listy ACL punktu końcowego, zobacz [Zarządzanie listy kontroli dostępu (ACL) dla punktów końcowych przy użyciu programu PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Jeśli utworzono maszynę wirtualną w modelu wdrażania usługi Resource Manager hello, możesz użyć programu Azure PowerShell zbyt[Utwórz grupy zabezpieczeń sieci](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol toohello ruch maszyny Wirtualnej.
