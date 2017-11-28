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
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="e1e61-103">Zarządzanie serwerem procesów działających na platformie Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e1e61-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1e61-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e1e61-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="e1e61-105">Classic</span><span class="sxs-lookup"><span data-stu-id="e1e61-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="e1e61-106">Podczas powrotu po awarii zaleca się toodeploy serwer przetwarzania na platformie Azure, jeśli istnieje duże opóźnienie między hello Azure Virtual Network i sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="e1e61-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="e1e61-107">W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania hello procesu serwerów działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e61-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e61-108">W tym artykule jest używane, jeśli używasz toobe **Resource Manager** jako model wdrażania hello hello maszyn wirtualnych w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="e1e61-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="e1e61-109">Jeśli używasz **klasycznego** jako model wdrażania hello, wykonaj kroki hello [jak tooset w górę i konfigurowanie serwera przetwarzania powrotu po awarii (klasyczne)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="e1e61-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1e61-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e1e61-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="e1e61-111">Wdrażanie serwera przetwarzania na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e1e61-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="e1e61-112">W magazynie hello > **infrastruktura usługi Site Recovery** (w pozycji "Manage" hello) > **serwery konfiguracji** (w pozycji "Dla VMware i maszyn fizycznych"), wybierz powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e1e61-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="e1e61-113">Na stronie Szczegóły konfiguracji serwera hello, którego kliknięcie spowoduje otwarcie kliknij pozycję "+ serwera przetwarzania"</span><span class="sxs-lookup"><span data-stu-id="e1e61-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Dodaj galerii serwera przetwarzania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="e1e61-115">Na powitania **Dodaj serwer przetwarzania** strony hello wybierz następujące wartości</span><span class="sxs-lookup"><span data-stu-id="e1e61-115">On hello **Add process server** page, select hello following values</span></span>

  ![Dodawanie elementu galerii serwera przetwarzania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="e1e61-117">**Nazwa pola**</span><span class="sxs-lookup"><span data-stu-id="e1e61-117">**Field Name**</span></span>|<span data-ttu-id="e1e61-118">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="e1e61-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="e1e61-119">Zdecydować, gdzie toodeploy serwera przetwarzania</span><span class="sxs-lookup"><span data-stu-id="e1e61-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="e1e61-120">Wybierz wartość hello **wdrażanie serwera przetwarzania powrotu po awarii na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="e1e61-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="e1e61-121">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="e1e61-121">Subscription</span></span>|<span data-ttu-id="e1e61-122">Wybierz hello subskrypcji Azure, gdzie awaryjnie hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="e1e61-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="e1e61-123">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="e1e61-123">Resource Group</span></span>|<span data-ttu-id="e1e61-124">Możesz utworzyć ten serwer przetwarzania toodeploy grupy zasobów lub wybierz serwer przetwarzania hello toodeploy w istniejącej grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="e1e61-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="e1e61-125">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="e1e61-125">Location</span></span>|<span data-ttu-id="e1e61-126">Wybierz centrum danych Azure hello do maszyn wirtualnych hello w przypadku, gdy do przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="e1e61-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="e1e61-127">Azure Network</span><span class="sxs-lookup"><span data-stu-id="e1e61-127">Azure Network</span></span>|<span data-ttu-id="e1e61-128">Wybierz hello Network(VNet) wirtualnych Azure, która hello maszyn wirtualnych w przypadku, gdy do przejścia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="e1e61-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="e1e61-129">Jeśli nie przez maszyny wirtualne do wielu sieci wirtualnych platformy Azure, następnie należy serwer przetwarzania, wdrożone na sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="e1e61-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="e1e61-130">Wypełnij hello pozostałe właściwości hello powitania serwera przetwarzania</span><span class="sxs-lookup"><span data-stu-id="e1e61-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Dodaj serwer przetwarzania podsumowania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="e1e61-132">**Nazwa pola**</span><span class="sxs-lookup"><span data-stu-id="e1e61-132">**Field Name**</span></span>|<span data-ttu-id="e1e61-133">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="e1e61-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="e1e61-134">Nazwa serwera</span><span class="sxs-lookup"><span data-stu-id="e1e61-134">Server Name</span></span>|<span data-ttu-id="e1e61-135">Nazwa wyświetlana i nazwa hosta dla maszyny wirtualnej serwera procesu</span><span class="sxs-lookup"><span data-stu-id="e1e61-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="e1e61-136">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="e1e61-136">User Name</span></span>|<span data-ttu-id="e1e61-137">Nazwa użytkownika, który staje się administratorem na tej maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e1e61-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="e1e61-138">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="e1e61-138">Storage Account</span></span>|<span data-ttu-id="e1e61-139">Nazwa konta magazynu rozmieszczenia dysku wirtualnego maszyny wirtualnej hello hello</span><span class="sxs-lookup"><span data-stu-id="e1e61-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="e1e61-140">Podsieć</span><span class="sxs-lookup"><span data-stu-id="e1e61-140">Subnet</span></span>|<span data-ttu-id="e1e61-141">Hello podsieci maszyny wirtualnej hello toowhich sieci wirtualnej Azure hello jest połączony</span><span class="sxs-lookup"><span data-stu-id="e1e61-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="e1e61-142">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e1e61-142">IP Address</span></span>|<span data-ttu-id="e1e61-143">Adres IP, które chcesz hello procesu serwera tooassume po jego rozruchu</span><span class="sxs-lookup"><span data-stu-id="e1e61-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="e1e61-144">Kliknij przycisk toostart przycisku OK hello wdrażania maszyny wirtualnej serwera procesu hello.</span><span class="sxs-lookup"><span data-stu-id="e1e61-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e61-145">toouse stanie toobe tego serwera przetwarzania powrotu po awarii, należy tooregister go z serwera konfiguracji lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="e1e61-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="e1e61-146">Rejestrowanie hello procesu serwera (działające na platformie Azure) tooa konfiguracji serwerem (lokalnego)</span><span class="sxs-lookup"><span data-stu-id="e1e61-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="e1e61-147">Uaktualnianie hello procesu serwera toolatest wersji.</span><span class="sxs-lookup"><span data-stu-id="e1e61-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="e1e61-148">Wyrejestrowywanie powitania serwera przetwarzania (działające na platformie Azure) z serwera konfiguracji (uruchamiane lokalnie)</span><span class="sxs-lookup"><span data-stu-id="e1e61-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
