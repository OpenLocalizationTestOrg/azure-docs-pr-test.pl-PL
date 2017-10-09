---
title: "aaaConnect maszyn wirtualnych systemu Linux w usłudze w chmurze | Dokumentacja firmy Microsoft"
description: "Połączenie maszyn wirtualnych systemu Linux utworzone za pomocą hello wdrażania klasycznego modelu tooan usługi w chmurze Azure lub sieci wirtualnej."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Połączenie maszyn wirtualnych systemu Linux utworzone za pomocą hello klasycznego modelu wdrażania z wirtualnych sieci lub usługę w chmurze
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Maszyny wirtualne systemu Linux utworzone za pomocą hello klasycznego modelu wdrażania są zawsze umieszczane w usłudze w chmurze. Usługa w chmurze Hello działa jako kontener i udostępnia unikatowy publicznej nazwy DNS, publiczny adres IP i zestaw maszyny wirtualnej hello tooaccess punktów końcowych w porównaniu z hello Internet. usługi w chmurze Hello może znajdować się w sieci wirtualnej, ale nie jest wymagane. Możesz również [połączenie maszyn wirtualnych systemu Windows za pomocą wirtualnej sieci lub w chmurze usługi](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Jeśli usługa w chmurze nie jest w sieci wirtualnej, jest nazywany *autonomiczny* usługi w chmurze. maszyny wirtualne Hello autonomicznej usługi w chmurze komunikują się z innych maszyn wirtualnych przy użyciu hello publicznej nazwy DNS innych maszyn wirtualnych i hello ruch przesyłany hello Internet. Jeśli usługa w chmurze jest w sieci wirtualnej maszyn wirtualnych hello, że usługa w chmurze może komunikować się z innych maszyn wirtualnych w sieci wirtualnej hello bez wysyłania cały ruch przez hello Internet.

Jeśli umieścisz maszyn wirtualnych w hello tej samej usługi chmury autonomiczny, można nadal używać równoważenia obciążenia i zestawy dostępności. Aby uzyskać więcej informacji, zobacz [maszyn wirtualnych równoważenia obciążenia](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) i [Zarządzanie hello dostępność maszyn wirtualnych](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nie można jednak zorganizować hello maszyn wirtualnych w podsieciach lub połączyć sieć lokalną tooyour usługi chmury autonomicznych. Oto przykład:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Następne kroki
Po utworzeniu maszyny wirtualnej jest dobrym rozwiązaniem zbyt[Dodaj dysk danych](attach-disk.md) więc obciążeń i usług danych toostore lokalizacji.
