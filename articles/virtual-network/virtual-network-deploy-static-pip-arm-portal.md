---
title: "aaaCreate maszynę Wirtualną za pomocą statycznego publicznego adresu IP - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny Wirtualnej z statyczny publiczny adres IP przy użyciu hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Utwórz maszynę Wirtualną z statycznego publicznego adresu IP za pomocą hello portalu Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Szablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klasyczny)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Utwórz maszynę Wirtualną z statycznego publicznego adresu IP

toocreate maszynę Wirtualną za pomocą statycznego publicznego adresu IP adres w hello portalu Azure, pełną hello następujące kroki:

1. W przeglądarce Przejdź toohello [portalu Azure](https://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Polecenie hello lewego górnego rogu portalu hello, **nowy**>>**obliczeniowe**>**systemu Windows Server 2012 R2 Datacenter**.
3. W hello **wybierz model wdrożenia** wybierz **Resource Manager** i kliknij przycisk **Utwórz**.
4. W hello **podstawy** bloku, wprowadź hello wirtualna informacje, jak pokazano poniżej, a następnie kliknij przycisk **OK**.
   
    ![Portal Azure — podstawy](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. W hello **wybierz rozmiar** bloku, kliknij przycisk **A1 standardowe** w sposób przedstawiony poniżej, a następnie kliknij przycisk **wybierz**.
   
    ![Portal Azure — wybierz rozmiar](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. W hello **ustawienia** bloku, kliknij przycisk **publicznego adresu IP**, a następnie w hello **tworzenie publicznego adresu IP** bloku, w obszarze **przypisania**, kliknij przycisk **Statycznych** jak pokazano poniżej. A następnie kliknij przycisk **OK**.
   
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. W hello **ustawienia** bloku, kliknij przycisk **OK**.
8. Przejrzyj hello **Podsumowanie** bloku, jak pokazano poniżej, a następnie kliknij przycisk **OK**.
   
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Zwróć uwagę, hello nowego kafelka na pulpicie nawigacyjnym.
   
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Po utworzeniu maszyny Wirtualnej hello hello **ustawienia** w sposób przedstawiony poniżej zostanie wyświetlony blok
    
    ![Portal Azure — tworzenie publicznego adresu IP](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

