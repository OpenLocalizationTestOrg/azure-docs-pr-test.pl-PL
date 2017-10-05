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
# <a name="delete-a-site-recovery-vault"></a>Usuń magazyn usługi Site Recovery
Zależności można uniemożliwić usunięcie magazynie usługi Azure Site Recovery. Akcje, które należy wykonać różnić w zależności od scenariusza usługi Site Recovery: VMware do platformy Azure, funkcji Hyper-V (z lub bez programu System Center Virtual Machine Manager) na platformie Azure oraz Azure Backup. Aby usunąć magazyn używany w usłudze Kopia zapasowa Azure, zobacz [usuwanie magazynu kopii zapasowych w usłudze Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Jeśli testowania produktu i nie są zainteresowane o utracie danych, należy użyć metody delete force szybko usunąć magazyn i jego zależności.

> Polecenia programu PowerShell Usuwa całą zawartość magazynu i nie jest odwracalne.

## <a name="use-powershell-to-force-delete-the-vault"></a>Użyj programu PowerShell, aby wymusić usunięcie magazynu 

Aby usunąć magazyn usługi Site Recovery, nawet jeśli istnieją elementy chronione, wykonaj następujące polecenia:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Usuń magazyn usługi Site Recovery 
Aby usunąć magazyn, wykonaj kroki zalecane dla danego scenariusza.

### <a name="vmware-vms-to-azure"></a>Maszyny wirtualne VMware do platformy Azure

1. Usuń wszystkie chronione maszyny wirtualne, wykonując kroki opisane w [Wyłącz ochronę VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Usuń wszystkie zasady replikacji, wykonując kroki opisane w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Usuń odwołania do vCenter, wykonując kroki opisane w [usunąć vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Usuń serwer konfiguracji, wykonując kroki opisane w [zlikwidować serwer konfiguracji](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Usuń magazyn.


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a>Maszyny wirtualne funkcji Hyper-V (z programu Virtual Machine Manager) w systemie Azure
1. Usuń wszystkie chronione maszyny wirtualne, wykonując kroki opisane w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Usuń wszystkie zasady replikacji, wykonując kroki opisane w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Usuń odwołania do serwerów programu Virtual Machine Manager, wykonując kroki opisane w [wyrejestrować podłączony serwer VMM](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Usuń magazyn.

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a>Maszyny wirtualne funkcji Hyper-V (bez programu Virtual Machine Manager) w systemie Azure
1. Usuń wszystkie chronione maszyny wirtualne, wykonując kroki opisane w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Usuń wszystkie zasady replikacji, wykonując kroki opisane w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Usuń odwołania do serwerów funkcji Hyper-V, wykonując kroki opisane w [wyrejestrować z hosta funkcji Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Usunąć lokacji funkcji Hyper-V.

5. Usuń magazyn.
