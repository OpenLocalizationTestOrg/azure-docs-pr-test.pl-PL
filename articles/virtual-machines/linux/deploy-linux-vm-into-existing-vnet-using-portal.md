---
title: "aaaDeploy maszyn wirtualnych systemu Linux w istniejącej sieci z portalu Azure | Dokumentacja firmy Microsoft"
description: "Wdróż Maszynę wirtualną systemu Linux w istniejącej sieci wirtualnej platformy Azure przy użyciu portalu hello."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Jak toodeploy maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z hello portalu Azure

W tym artykule opisano sposób toodeploy maszynę wirtualną (VM) do istniejącej sieci wirtualnej (VNet). Azure zasoby, takie jak grupy zabezpieczeń sieci wirtualnych i sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone. Po wdrożeniu sieci wirtualnej można użyć ponownie przez stałej redeployments bez żadnych infrastruktury toohello niekorzystny wpływ. Planowanie sieci wirtualnej jako tradycyjną przełącznik sieciowy sprzętu — nie trzeba tooconfigure nowego sprzętu przełącznik z każdym wdrożeniu.  

Z poprawnie skonfigurowana sieć wirtualną możesz kontynuować toodeploy nowych serwerów do tej sieci wirtualnej samodzielnego kilka, zmian wymaganych przez czas życia hello hello sieci wirtualnej.

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Najpierw utwórz tooorganize grupy zasobów wszystko, czego możesz utworzyć w tym przewodniku. Aby uzyskać więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Utwórz hello sieci wirtualnej

Następnie kompilacji hello toolaunch sieci wirtualnej maszyn wirtualnych do. Hello sieć wirtualna zawiera jedną podsieć i jest skojarzona z sieciową grupą zabezpieczeń hello z tą podsiecią w kolejnym kroku.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Dodaj podsieć toohello VNic

Wirtualne karty sieciowe (VNics) są ważne, jak można je połączyć toodifferent maszyn wirtualnych. Takie podejście zapewnia hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe. Utwórz VNic i skojarzyć go z podsiecią hello utworzony w poprzednim kroku hello.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Utwórz grupę zabezpieczeń sieci hello

Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci. Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci platformy Azure, zobacz [co to jest grupa zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego

Witaj maszyna wirtualna musi mieć dostęp z hello internet, więc regułę zezwalającą na toobe ruch przychodzący port 22 przekazywane hello sieci tooport 22 na powitania zostanie utworzona maszyna wirtualna.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Skojarz hello grupy NSG z podsiecią hello

Z hello sieć wirtualną i podsieć hello utworzona należy skojarzyć hello sieciową grupę zabezpieczeń z podsiecią hello. Może być skojarzony z całej podsieci lub VNic poszczególnych grup zabezpieczeń sieci. Zapora hello filtrowanie ruchu na poziomie podsieci hello wszystkich VNics i hello maszyn wirtualnych w obrębie podsieci hello są chronione przez hello sieciowej grupy zabezpieczeń. Witaj innej metody jest hello jest grupa zabezpieczeń sieci skojarzonych z tylko jednym kartę VNic i chronienie tylko jednej maszyny Wirtualnej.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej i grupy NSG

Przy użyciu hello portalu Azure, hello maszyny Wirtualnej systemu Linux jest wdrożony toohello istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Za pomocą portalu toochoose hello istniejących zasobów, poinstruuj Azure toodeploy hello wirtualna wewnątrz hello istniejącej sieci. Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.  

## <a name="next-steps"></a>Następne kroki

* [Użyj toocreate szablonu usługi Azure Resource Manager określonego wdrożenia](../windows/cli-deploy-templates.md)
* [Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure](create-cli-complete.md)
* [Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów](create-ssh-secured-vm-from-template.md)
