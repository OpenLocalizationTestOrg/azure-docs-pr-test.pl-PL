---
title: " Zarządzanie serwerem procesów działających na platformie Azure (Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania serwera przetwarzania powrotu po awarii (Resource Manager) na platformie Azure."
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="dbafe-103">Zarządzanie serwerem procesów działających na platformie Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="dbafe-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbafe-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dbafe-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="dbafe-105">Classic</span><span class="sxs-lookup"><span data-stu-id="dbafe-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="dbafe-106">Podczas powrotu po awarii zaleca się wdrożyć serwer przetwarzania na platformie Azure, jeśli istnieje duże opóźnienie między sieci wirtualnej platformy Azure i siecią lokalną.</span><span class="sxs-lookup"><span data-stu-id="dbafe-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="dbafe-107">W tym artykule opisano, jak można skonfigurować, konfigurowanie i zarządzanie serwerami procesów działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbafe-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="dbafe-108">Ten artykuł ma być używany, jeśli używasz **Resource Manager** jako model wdrażania dla maszyny wirtualnej podczas pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbafe-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="dbafe-109">Jeśli używasz **klasycznego** jako model wdrażania, postępuj zgodnie z instrukcjami [jak skonfigurować i konfigurowanie serwera przetwarzania powrotu po awarii (klasyczne)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="dbafe-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbafe-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dbafe-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="dbafe-111">Wdrażanie serwera przetwarzania na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="dbafe-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="dbafe-112">W magazynie > **infrastruktura usługi Site Recovery** (w pozycji "Manage") > **serwery konfiguracji** (w pozycji "Dla VMware i maszyn fizycznych"), wybierz serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dbafe-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="dbafe-113">Na stronie szczegółów konfiguracji serwera, który zostanie otwarty, kliknij przycisk "+ serwera przetwarzania"</span><span class="sxs-lookup"><span data-stu-id="dbafe-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![Dodaj galerii serwera przetwarzania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="dbafe-115">Na **Dodaj serwer przetwarzania** wybierz następujące wartości</span><span class="sxs-lookup"><span data-stu-id="dbafe-115">On the **Add process server** page, select the following values</span></span>

  ![Dodawanie elementu galerii serwera przetwarzania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="dbafe-117">**Nazwa pola**</span><span class="sxs-lookup"><span data-stu-id="dbafe-117">**Field Name**</span></span>|<span data-ttu-id="dbafe-118">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="dbafe-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="dbafe-119">Wybierz miejsce wdrożenia serwera przetwarzania</span><span class="sxs-lookup"><span data-stu-id="dbafe-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="dbafe-120">Wybierz wartość **wdrażanie serwera przetwarzania powrotu po awarii na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="dbafe-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="dbafe-121">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="dbafe-121">Subscription</span></span>|<span data-ttu-id="dbafe-122">Wybierz subskrypcję Azure, w którym przełączyć maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="dbafe-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="dbafe-123">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="dbafe-123">Resource Group</span></span>|<span data-ttu-id="dbafe-124">Można utworzyć grupy zasobów, aby wdrożyć ten serwer przetwarzania lub wybrać wdrożenie serwera przetwarzania w istniejącej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="dbafe-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="dbafe-125">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="dbafe-125">Location</span></span>|<span data-ttu-id="dbafe-126">Wybierz centrum danych Azure, w której maszyny wirtualne w przypadku, gdy do przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="dbafe-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="dbafe-127">Azure Network</span><span class="sxs-lookup"><span data-stu-id="dbafe-127">Azure Network</span></span>|<span data-ttu-id="dbafe-128">Wybierz Network(VNet) wirtualnych Azure który maszyn wirtualnych w przypadku, gdy do przejścia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="dbafe-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="dbafe-129">Jeśli nie przez maszyny wirtualne do wielu sieci wirtualnych platformy Azure, następnie należy serwer przetwarzania, wdrożone na sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="dbafe-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="dbafe-130">Wypełnij pozostałe właściwości serwera przetwarzania</span><span class="sxs-lookup"><span data-stu-id="dbafe-130">Fill in the rest of the properties for the process server</span></span>

  ![Dodaj serwer przetwarzania podsumowania](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="dbafe-132">**Nazwa pola**</span><span class="sxs-lookup"><span data-stu-id="dbafe-132">**Field Name**</span></span>|<span data-ttu-id="dbafe-133">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="dbafe-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="dbafe-134">Nazwa serwera</span><span class="sxs-lookup"><span data-stu-id="dbafe-134">Server Name</span></span>|<span data-ttu-id="dbafe-135">Nazwa wyświetlana i nazwa hosta dla maszyny wirtualnej serwera procesu</span><span class="sxs-lookup"><span data-stu-id="dbafe-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="dbafe-136">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="dbafe-136">User Name</span></span>|<span data-ttu-id="dbafe-137">Nazwa użytkownika, który staje się administratorem na tej maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dbafe-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="dbafe-138">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="dbafe-138">Storage Account</span></span>|<span data-ttu-id="dbafe-139">Nazwa konta magazynu rozmieszczenia dysku wirtualnego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dbafe-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="dbafe-140">Podsieć</span><span class="sxs-lookup"><span data-stu-id="dbafe-140">Subnet</span></span>|<span data-ttu-id="dbafe-141">Podsieć sieci wirtualnej Azure, do którego jest podłączony maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dbafe-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="dbafe-142">Adres IP</span><span class="sxs-lookup"><span data-stu-id="dbafe-142">IP Address</span></span>|<span data-ttu-id="dbafe-143">Adres IP, które chcesz serwera przetwarzania do wniosku po jego rozruchu</span><span class="sxs-lookup"><span data-stu-id="dbafe-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="dbafe-144">Kliknij przycisk OK, aby rozpocząć wdrażanie maszyny wirtualnej serwera procesu.</span><span class="sxs-lookup"><span data-stu-id="dbafe-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="dbafe-145">Aby można było użyć tego serwera przetwarzania powrotu po awarii, musisz zarejestrowanie go za pomocą lokalnego serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dbafe-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="dbafe-146">Rejestrowanie serwera przetwarzania (działające na platformie Azure) do konfiguracji serwera (uruchamiane lokalnie)</span><span class="sxs-lookup"><span data-stu-id="dbafe-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="dbafe-147">Uaktualnianie serwera przetwarzania do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="dbafe-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="dbafe-148">Wyrejestrowywanie serwera przetwarzania (działające na platformie Azure) z serwera konfiguracji (uruchamiane lokalnie)</span><span class="sxs-lookup"><span data-stu-id="dbafe-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
