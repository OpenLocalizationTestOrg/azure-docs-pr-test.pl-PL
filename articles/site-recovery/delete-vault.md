---
title: "Usuń magazyn usługi Site Recovery"
description: "Dowiedz się, jak usunąć magazynie usługi Azure Site Recovery, oparta na scenariuszu odzyskiwania lokacji."
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="d4b98-103">Usuń magazyn usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d4b98-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="d4b98-104">Zależności można uniemożliwić usunięcie magazynie usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d4b98-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="d4b98-105">Akcje, które należy wykonać różnić w zależności od scenariusza usługi Site Recovery: VMware do platformy Azure, funkcji Hyper-V (z lub bez programu System Center Virtual Machine Manager) na platformie Azure oraz Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="d4b98-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="d4b98-106">Aby usunąć magazyn używany w usłudze Kopia zapasowa Azure, zobacz [usuwanie magazynu kopii zapasowych w usłudze Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d4b98-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="d4b98-107">Jeśli testowania produktu i nie są zainteresowane o utracie danych, należy użyć metody delete force szybko usunąć magazyn i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="d4b98-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="d4b98-108">Polecenia programu PowerShell Usuwa całą zawartość magazynu i nie jest odwracalne.</span><span class="sxs-lookup"><span data-stu-id="d4b98-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="d4b98-109">Użyj programu PowerShell, aby wymusić usunięcie magazynu</span><span class="sxs-lookup"><span data-stu-id="d4b98-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="d4b98-110">Aby usunąć magazyn usługi Site Recovery, nawet jeśli istnieją elementy chronione, wykonaj następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d4b98-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="d4b98-111">Usuń magazyn usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d4b98-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="d4b98-112">Aby usunąć magazyn, wykonaj kroki zalecane dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="d4b98-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="d4b98-113">Maszyny wirtualne VMware do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4b98-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="d4b98-114">Usuń wszystkie chronione maszyny wirtualne, wykonując kroki opisane w [Wyłącz ochronę VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="d4b98-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="d4b98-115">Usuń wszystkie zasady replikacji, wykonując kroki opisane w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="d4b98-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="d4b98-116">Usuń odwołania do vCenter, wykonując kroki opisane w [usunąć vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="d4b98-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="d4b98-117">Usuń serwer konfiguracji, wykonując kroki opisane w [zlikwidować serwer konfiguracji](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="d4b98-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="d4b98-118">Usuń magazyn.</span><span class="sxs-lookup"><span data-stu-id="d4b98-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="d4b98-119">Maszyny wirtualne funkcji Hyper-V (z programu Virtual Machine Manager) w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="d4b98-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="d4b98-120">Usuń wszystkie chronione maszyny wirtualne, wykonując kroki opisane w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="d4b98-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="d4b98-121">Usuń wszystkie zasady replikacji, wykonując kroki opisane w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="d4b98-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="d4b98-122">Usuń odwołania do serwerów programu Virtual Machine Manager, wykonując kroki opisane w [wyrejestrować podłączony serwer VMM](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="d4b98-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="d4b98-123">Usuń magazyn.</span><span class="sxs-lookup"><span data-stu-id="d4b98-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="d4b98-124">Maszyny wirtualne funkcji Hyper-V (bez programu Virtual Machine Manager) w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="d4b98-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="d4b98-125">Usuń wszystkie chronione maszyny wirtualne, wykonując kroki opisane w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="d4b98-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="d4b98-126">Usuń wszystkie zasady replikacji, wykonując kroki opisane w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="d4b98-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="d4b98-127">Usuń odwołania do serwerów funkcji Hyper-V, wykonując kroki opisane w [wyrejestrować z hosta funkcji Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="d4b98-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="d4b98-128">Usunąć lokacji funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d4b98-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="d4b98-129">Usuń magazyn.</span><span class="sxs-lookup"><span data-stu-id="d4b98-129">Delete the vault.</span></span>
