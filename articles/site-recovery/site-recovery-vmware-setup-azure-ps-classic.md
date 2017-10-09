---
title: " Zarządzanie serwerem procesów uruchomionych w Azure(Classic) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset się powrotu po awarii procesu Server(Classic) w usłudze Azure."
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Zarządzanie serwerem procesów działających na platformie Azure (klasyczne)
> [!div class="op_single_selector"]
> * [Klasyczny Portal Azure](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Podczas powrotu po awarii zaleca się toodeploy serwer przetwarzania na platformie Azure, jeśli istnieje duże opóźnienie między hello Azure Virtual Network i sieci lokalnej. W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania hello procesu serwerów działających na platformie Azure.

> [!NOTE]
> W tym artykule jest używane, jeśli użyto klasycznego modelu wdrażania hello hello maszyn wirtualnych w trybie failover toobe. Menedżer zasobów użyto jako hello kroki wdrażania modelu wykonaj hello w [jak tooset w górę i konfigurowanie serwera przetwarzania powrotu po awarii (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Wdrażanie serwera przetwarzania na platformie Azure

1. W portalu Azure Marketplace, utwórz maszynę wirtualną przy użyciu hello **Microsoft Azure Site odzyskiwania procesu serwera V2** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Upewnij się, że wybierz model wdrażania hello jako **klasycznego** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. W Kreatorze maszyny wirtualnej Utwórz hello > Podstawowe ustawienia, upewnij się, wybierz toowhere subskrypcji i lokalizacji hello awaryjnie hello maszyn wirtualnych.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Podłącz maszyny wirtualnej hello hello toowhich sieci wirtualnej Azure toohello przejścia w tryb failover maszyny wirtualnej jest połączona.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Po zainicjowaniu obsługi maszyny wirtualnej serwera przetwarzania hello należy toolog w i zarejestrowanie go za pomocą powitania serwera konfiguracji.

> [!NOTE]
> toouse stanie toobe tego serwera przetwarzania powrotu po awarii, należy tooregister go z serwera konfiguracji lokalne powitania.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Rejestrowanie powitania serwera przetwarzania (działające na platformie Azure) tooa konfiguracji serwerem (lokalnego)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Uaktualnianie wersji toolatest serwera przetwarzania hello.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Wyrejestrowywanie powitania serwera przetwarzania (działające na platformie Azure) z serwera konfiguracji (uruchamiane lokalnie)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
