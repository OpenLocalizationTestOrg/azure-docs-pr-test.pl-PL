---
title: "aaaDelete magazynu usługi Site Recovery"
description: "Dowiedz się, jak toodelete magazynie usługi Azure Site Recovery na podstawie hello scenariuszu odzyskiwania lokacji."
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
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="39bd0-103">Usuń magazyn usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="39bd0-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="39bd0-104">Zależności można uniemożliwić usunięcie magazynie usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="39bd0-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="39bd0-105">Witaj akcji, które należy tootake różnić w zależności od scenariusza odzyskiwania lokacji hello: VMware tooAzure tooAzure funkcji Hyper-V (z lub bez programu System Center Virtual Machine Manager), a kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="39bd0-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="39bd0-106">Zobacz toodelete magazynu używane w usłudze Kopia zapasowa Azure [usuwanie magazynu kopii zapasowych w usłudze Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="39bd0-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="39bd0-107">Jeśli testowany hello produktu i nie są zainteresowane o utracie danych, użyj hello życie delete — metoda toorapidly Usuń hello magazyn i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="39bd0-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="39bd0-108">Hello polecenia programu PowerShell Usuwa całą zawartość hello hello magazynu i nie jest odwracalne.</span><span class="sxs-lookup"><span data-stu-id="39bd0-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="39bd0-109">Użyj programu PowerShell tooforce usunąć hello magazynu</span><span class="sxs-lookup"><span data-stu-id="39bd0-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="39bd0-110">hello toodelete magazynu usługi Site Recovery, nawet jeśli istnieją chronione elementy, użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="39bd0-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="39bd0-111">Usuń magazyn usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="39bd0-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="39bd0-112">Magazyn hello toodelete, hello wykonaj zalecane kroki dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="39bd0-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="39bd0-113">Maszyny wirtualne VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="39bd0-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="39bd0-114">Usuń wszystkie chronione maszyny wirtualne, wykonując kroki hello w [Wyłącz ochronę VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="39bd0-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="39bd0-115">Usunąć wszystkie zasady replikacji, wykonując kroki hello w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="39bd0-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="39bd0-116">Usuwanie odwołań toovCenter przez hello następujące kroki w [usunąć vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="39bd0-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="39bd0-117">Usuń serwer konfiguracji hello wykonując kroki hello w [zlikwidować serwer konfiguracji](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="39bd0-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="39bd0-118">Usuń magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="39bd0-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="39bd0-119">TooAzure maszyn wirtualnych funkcji Hyper-V (z programu Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="39bd0-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="39bd0-120">Usuń wszystkie chronione maszyny wirtualne, wykonując kroki hello w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="39bd0-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="39bd0-121">Usunąć wszystkie zasady replikacji, wykonując kroki hello w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="39bd0-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="39bd0-122">Usuń odwołuje się do serwerów Machine Manager tooVirtual wykonując kroki hello w [wyrejestrować podłączony serwer VMM](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="39bd0-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="39bd0-123">Usuń magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="39bd0-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="39bd0-124">TooAzure maszyn wirtualnych funkcji Hyper-V (bez programu Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="39bd0-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="39bd0-125">Usuń wszystkie chronione maszyny wirtualne, wykonując kroki hello w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="39bd0-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="39bd0-126">Usunąć wszystkie zasady replikacji, wykonując kroki hello w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="39bd0-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="39bd0-127">Usuń odwołuje się do serwerów tooHyper V wykonując kroki hello w [wyrejestrować z hosta funkcji Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="39bd0-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="39bd0-128">Usuń lokację hello funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="39bd0-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="39bd0-129">Usuń magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="39bd0-129">Delete hello vault.</span></span>
