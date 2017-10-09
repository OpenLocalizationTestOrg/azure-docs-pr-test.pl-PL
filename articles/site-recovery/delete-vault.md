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
# <a name="delete-a-site-recovery-vault"></a>Usuń magazyn usługi Site Recovery
Zależności można uniemożliwić usunięcie magazynie usługi Azure Site Recovery. Witaj akcji, które należy tootake różnić w zależności od scenariusza odzyskiwania lokacji hello: VMware tooAzure tooAzure funkcji Hyper-V (z lub bez programu System Center Virtual Machine Manager), a kopia zapasowa Azure. Zobacz toodelete magazynu używane w usłudze Kopia zapasowa Azure [usuwanie magazynu kopii zapasowych w usłudze Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Jeśli testowany hello produktu i nie są zainteresowane o utracie danych, użyj hello życie delete — metoda toorapidly Usuń hello magazyn i jego zależności.

> Hello polecenia programu PowerShell Usuwa całą zawartość hello hello magazynu i nie jest odwracalne.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Użyj programu PowerShell tooforce usunąć hello magazynu 

hello toodelete magazynu usługi Site Recovery, nawet jeśli istnieją chronione elementy, użyj polecenia:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Usuń magazyn usługi Site Recovery 
Magazyn hello toodelete, hello wykonaj zalecane kroki dla danego scenariusza.

### <a name="vmware-vms-tooazure"></a>Maszyny wirtualne VMware tooAzure

1. Usuń wszystkie chronione maszyny wirtualne, wykonując kroki hello w [Wyłącz ochronę VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Usunąć wszystkie zasady replikacji, wykonując kroki hello w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Usuwanie odwołań toovCenter przez hello następujące kroki w [usunąć vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Usuń serwer konfiguracji hello wykonując kroki hello w [zlikwidować serwer konfiguracji](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Usuń magazyn hello.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>TooAzure maszyn wirtualnych funkcji Hyper-V (z programu Virtual Machine Manager)
1. Usuń wszystkie chronione maszyny wirtualne, wykonując kroki hello w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Usunąć wszystkie zasady replikacji, wykonując kroki hello w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Usuń odwołuje się do serwerów Machine Manager tooVirtual wykonując kroki hello w [wyrejestrować podłączony serwer VMM](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Usuń magazyn hello.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>TooAzure maszyn wirtualnych funkcji Hyper-V (bez programu Virtual Machine Manager)
1. Usuń wszystkie chronione maszyny wirtualne, wykonując kroki hello w [Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Usunąć wszystkie zasady replikacji, wykonując kroki hello w [Usuń zasady replikacji](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Usuń odwołuje się do serwerów tooHyper V wykonując kroki hello w [wyrejestrować z hosta funkcji Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Usuń lokację hello funkcji Hyper-V.

5. Usuń magazyn hello.
