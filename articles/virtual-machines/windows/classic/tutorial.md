---
title: aaaCreate maszyny Wirtualnej w portalu Azure hello | Dokumentacja firmy Microsoft
description: "Utwórz maszynę wirtualną systemu Windows w hello portalu Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Utwórz maszynę wirtualną z systemem Windows w hello portalu Azure
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](tutorial.md)
> * [Środowiska PowerShell: Wdrożenia klasycznego](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu wdrażania usługi Resource Manager hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przy użyciu hello **portalu Azure**.

W tym samouczku przedstawiono sposób toocreate Azure maszyny wirtualnej (VM) z systemem Windows w hello portalu Azure. Na przykład użyjemy obrazu systemu Windows Server, ale jest to tylko jeden z hello wiele obrazów oferty Azure. Należy pamiętać, że obrazy dostępne do wyboru zależą subskrypcji. Na przykład obrazy pulpitu systemu Windows mogą być dostępne tooMSDN subskrybentów.

W tej sekcji opisano sposób toouse hello **pulpitu nawigacyjnego** w hello tooselect portalu Azure, a następnie utwórz hello maszyny wirtualnej.

Można również tworzyć maszyny wirtualne przy użyciu [własnych obrazów](createupload-vhd.md). toolearn dotyczących tego i innych metod, zobacz [toocreate różne sposoby maszyny wirtualnej systemu Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Utworzyć hello maszyny wirtualnej
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[utworzyć Maszynę wirtualną przy użyciu modelu wdrażania usługi Resource Manager hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) w hello portalu Azure.
* Zaloguj się na toohello maszyny wirtualnej. Aby uzyskać instrukcje, zobacz [logowania tooa maszyny wirtualnej z systemem Windows Server](connect-logon.md).
* Dołącz dane toostore dysku. Możesz dołączyć zarówno puste dyski i dyski, które zawierają dane. Aby uzyskać instrukcje, zobacz hello [dołączanie danych dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania](attach-disk.md).
