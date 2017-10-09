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
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="f2168-103">Zarządzanie serwerem procesów działających na platformie Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="f2168-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2168-104">Klasyczny Portal Azure</span><span class="sxs-lookup"><span data-stu-id="f2168-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="f2168-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2168-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="f2168-106">Podczas powrotu po awarii zaleca się toodeploy serwer przetwarzania na platformie Azure, jeśli istnieje duże opóźnienie między hello Azure Virtual Network i sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="f2168-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="f2168-107">W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania hello procesu serwerów działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f2168-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f2168-108">W tym artykule jest używane, jeśli użyto klasycznego modelu wdrażania hello hello maszyn wirtualnych w trybie failover toobe.</span><span class="sxs-lookup"><span data-stu-id="f2168-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="f2168-109">Menedżer zasobów użyto jako hello kroki wdrażania modelu wykonaj hello w [jak tooset w górę i konfigurowanie serwera przetwarzania powrotu po awarii (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="f2168-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2168-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f2168-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="f2168-111">Wdrażanie serwera przetwarzania na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f2168-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="f2168-112">W portalu Azure Marketplace, utwórz maszynę wirtualną przy użyciu hello **Microsoft Azure Site odzyskiwania procesu serwera V2**</span><span class="sxs-lookup"><span data-stu-id="f2168-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="f2168-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="f2168-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="f2168-114">Upewnij się, że wybierz model wdrażania hello jako **klasycznego**</span><span class="sxs-lookup"><span data-stu-id="f2168-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="f2168-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="f2168-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="f2168-116">W Kreatorze maszyny wirtualnej Utwórz hello > Podstawowe ustawienia, upewnij się, wybierz toowhere subskrypcji i lokalizacji hello awaryjnie hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f2168-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="f2168-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="f2168-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="f2168-118">Podłącz maszyny wirtualnej hello hello toowhich sieci wirtualnej Azure toohello przejścia w tryb failover maszyny wirtualnej jest połączona.</span><span class="sxs-lookup"><span data-stu-id="f2168-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="f2168-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="f2168-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="f2168-120">Po zainicjowaniu obsługi maszyny wirtualnej serwera przetwarzania hello należy toolog w i zarejestrowanie go za pomocą powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f2168-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="f2168-121">toouse stanie toobe tego serwera przetwarzania powrotu po awarii, należy tooregister go z serwera konfiguracji lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="f2168-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="f2168-122">Rejestrowanie powitania serwera przetwarzania (działające na platformie Azure) tooa konfiguracji serwerem (lokalnego)</span><span class="sxs-lookup"><span data-stu-id="f2168-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="f2168-123">Uaktualnianie wersji toolatest serwera przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="f2168-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="f2168-124">Wyrejestrowywanie powitania serwera przetwarzania (działające na platformie Azure) z serwera konfiguracji (uruchamiane lokalnie)</span><span class="sxs-lookup"><span data-stu-id="f2168-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
