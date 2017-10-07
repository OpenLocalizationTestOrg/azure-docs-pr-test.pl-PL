---
title: "aaaMigrate sieci wirtualnej platformy Azure (klasyczną) z grupą koligacji regionu tooa | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate sieci wirtualnej (wdrożenia klasyczne) z koligacji grupy tooa regionu."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Migracja sieci wirtualnej (klasyczne) z regionu tooa grupy koligacji

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać modelu wdrażania usługi Resource Manager hello.

Grupy koligacji upewnij się, że zasoby są tworzone w ramach tej samej grupie koligacji fizycznie są obsługiwane przez serwery, które są blisko siebie włączenie tych zasobów toocommunicate szybsze hello. W ciągu ostatnich hello grupy koligacji były wymagane do tworzenia sieci wirtualnych (klasyczny). W tym czasie hello usługi Menedżera sieci, zarządzaną sieciami wirtualnymi (klasyczne) może pracować tylko w ramach zestawu serwerów fizycznych lub jednostki skalowania. Ulepszenia architektury nastąpiło nasilenie zakresu hello sieci zarządzania tooa regionu.

W wyniku tych usprawnień architektury grup koligacji nie jest już zalecane lub wymagane dla sieci wirtualnych (klasyczny). Użyj Hello grup koligacji dla sieci wirtualnych (klasyczne) zastępuje regionów. Sieci wirtualne (klasyczne) skojarzonych z regiony są nazywane regionalnych sieci wirtualnych.

Zaleca się, że grupy koligacji nie używaj ogólnie. Oprócz wymagań sieci wirtualnej hello grupy koligacji były również ważne toouse tooensure zasoby, takie jak zasobów obliczeniowych (klasyczne) i magazynu (klasyczne), zostały umieszczone obok siebie. Jednak z hello bieżącej architektury sieci platformy Azure, tych wymagań umieszczania nie są już wymagane.

> [!IMPORTANT]
> Chociaż jest technicznie możliwe, toocreate sieci wirtualnej, która jest skojarzona z grupą koligacji, nie istnieje żadne atrakcyjnych toodo Przyczyna tak. Wiele funkcji sieci wirtualnej, takich jak grupy zabezpieczeń sieciowych, są dostępne tylko po użyciu regionalną sieć wirtualną, a nie są dostępne dla sieci wirtualnych, które są skojarzone z grup koligacji.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Edytowanie pliku konfiguracji sieci hello

1. Eksportowanie pliku konfiguracji sieci hello. toolearn jak tooexport konfiguracji sieci przy użyciu programu PowerShell lub plik hello Azure interfejsu wiersza polecenia (CLI) 1.0, zobacz [skonfigurować sieć wirtualną przy użyciu pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md#export).
2. Edytowanie pliku konfiguracji sieci hello, zastępując **AffinityGroup** z **lokalizacji**. Określ Azure [region](https://azure.microsoft.com/regions) dla **lokalizacji**.
   
   > [!NOTE]
   > Witaj **lokalizacji** to region hello, określony dla hello grupie koligacji, która jest skojarzona z sieci wirtualnej (klasyczny). Na przykład, jeśli w Twojej sieci wirtualnej (klasyczne) jest skojarzona z grupą koligacji znajdującego się w zachodnie stany USA, podczas migracji Twoje **lokalizacji** musi wskazywać tooWest Stanów Zjednoczonych. 
   > 
   > 
   
    Edytuj hello następujące wiersze w pliku konfiguracji sieci, zastępując wartości hello własnych: 
   
    **Stara wartość:** \<VirtualNetworkSitename = AffinityGroup "VNetUSWest" = "VNetDemoAG"\> 
   
    **Nowa wartość:** \<VirtualNetworkSitename = "VNetUSWest" Lokalizacja = "Zachodnie stany USA"\>
3. Zapisz zmiany i [zaimportować](virtual-networks-using-network-configuration-file.md#import) hello tooAzure konfiguracji sieci.

> [!NOTE]
> Ta migracja nie powoduje żadnych przestojów tooyour usług.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Jakie toodo, jeśli masz maszyny Wirtualnej (klasyczne) w grupie koligacji
Maszyny wirtualne (klasyczne) są obecnie w grupie koligacji nie ma potrzeby toobe usunięte z grupy koligacji hello. Po wdrożeniu maszyny Wirtualnej jest jednostką skalowania pojedynczego tooa wdrożone. Grupy koligacji, można ograniczyć zestaw hello dostępnych rozmiarów maszyn wirtualnych do nowego wdrożenia maszyny Wirtualnej, ale istniejącej maszyny Wirtualnej, które zostało wdrożone już jest ograniczony zestaw toohello maszyny wirtualnej rozmiarów dostępnych w jednostce skalowania hello, w których hello maszyna wirtualna jest wdrożona. Ponieważ powitalne maszyna wirtualna jest już wdrożony tooa jednostki skalowania, usuwanie maszyny Wirtualnej z grupy koligacji nie ma wpływu na powitania maszyny Wirtualnej.
