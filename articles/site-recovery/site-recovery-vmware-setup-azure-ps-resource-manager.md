---
title: " Zarządzanie serwerem procesów działających na platformie Azure (Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposobu tooset się powrotu po awarii procesu serwera (Resource Manager) w systemie Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Zarządzanie serwerem procesów działających na platformie Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Classic](./site-recovery-vmware-setup-azure-ps-classic.md)

Podczas powrotu po awarii zaleca się toodeploy serwer przetwarzania na platformie Azure, jeśli istnieje duże opóźnienie między hello Azure Virtual Network i sieci lokalnej. W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania hello procesu serwerów działających na platformie Azure.

> [!NOTE]
> W tym artykule jest używane, jeśli używasz toobe **Resource Manager** jako model wdrażania hello hello maszyn wirtualnych w trybie failover. Jeśli używasz **klasycznego** jako model wdrażania hello, wykonaj kroki hello [jak tooset w górę i konfigurowanie serwera przetwarzania powrotu po awarii (klasyczne)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Wdrażanie serwera przetwarzania na platformie Azure
1. W magazynie hello > **infrastruktura usługi Site Recovery** (w pozycji "Manage" hello) > **serwery konfiguracji** (w pozycji "Dla VMware i maszyn fizycznych"), wybierz powitania serwera konfiguracji.
2. Na stronie Szczegóły konfiguracji serwera hello, którego kliknięcie spowoduje otwarcie kliknij pozycję "+ serwera przetwarzania"

  ![Dodaj galerii serwera przetwarzania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  Na powitania **Dodaj serwer przetwarzania** strony hello wybierz następujące wartości

  ![Dodawanie elementu galerii serwera przetwarzania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Nazwa pola**|**Wartość**|
|-|-|
|Zdecydować, gdzie toodeploy serwera przetwarzania|Wybierz wartość hello **wdrażanie serwera przetwarzania powrotu po awarii na platformie Azure** |
|Subskrypcja|Wybierz hello subskrypcji Azure, gdzie awaryjnie hello maszyny wirtualne|
|Grupa zasobów|Możesz utworzyć ten serwer przetwarzania toodeploy grupy zasobów lub wybierz serwer przetwarzania hello toodeploy w istniejącej grupie zasobów|
|Lokalizacja|Wybierz centrum danych Azure hello do maszyn wirtualnych hello w przypadku, gdy do przejścia w tryb failover|
|Azure Network|Wybierz hello Network(VNet) wirtualnych Azure, która hello maszyn wirtualnych w przypadku, gdy do przejścia w tryb failover. Jeśli nie przez maszyny wirtualne do wielu sieci wirtualnych platformy Azure, następnie należy serwer przetwarzania, wdrożone na sieć wirtualną|

4. Wypełnij hello pozostałe właściwości hello powitania serwera przetwarzania

  ![Dodaj serwer przetwarzania podsumowania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Nazwa pola**|**Wartość**|
|-|-|
|Nazwa serwera|Nazwa wyświetlana i nazwa hosta dla maszyny wirtualnej serwera procesu|
| Nazwa użytkownika|Nazwa użytkownika, który staje się administratorem na tej maszynie wirtualnej|
|Konto magazynu|Nazwa konta magazynu rozmieszczenia dysku wirtualnego maszyny wirtualnej hello hello|
|Podsieć|Hello podsieci maszyny wirtualnej hello toowhich sieci wirtualnej Azure hello jest połączony|
| Adres IP|Adres IP, które chcesz hello procesu serwera tooassume po jego rozruchu|
5. Kliknij przycisk toostart przycisku OK hello wdrażania maszyny wirtualnej serwera procesu hello.

> [!NOTE]
> toouse stanie toobe tego serwera przetwarzania powrotu po awarii, należy tooregister go z serwera konfiguracji lokalne powitania.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Rejestrowanie hello procesu serwera (działające na platformie Azure) tooa konfiguracji serwerem (lokalnego)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Uaktualnianie hello procesu serwera toolatest wersji.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Wyrejestrowywanie powitania serwera przetwarzania (działające na platformie Azure) z serwera konfiguracji (uruchamiane lokalnie)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
