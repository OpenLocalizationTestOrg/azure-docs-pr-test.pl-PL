---
title: "Replicate i pracy awaryjnej maszyn wirtualnych VMware do platformy Azure przy użyciu programu PowerShell odzyskiwania lokacji Azure | Dokumentacja firmy Microsoft"
description: "Replicate i pracy awaryjnej maszyn wirtualnych VMware do platformy Azure przy użyciu programu PowerShell odzyskiwania lokacji Azure"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: raynew
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/02/2018
ms.author: bsiva
ms.openlocfilehash: ee4847a61392a8eacde82ea62c3812d601b489f3
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/13/2018
---
# <a name="replicate-and-failover-vmware-virtual-machines-to-azure-using-azure-site-recovery-powershell"></a>Replicate i pracy awaryjnej maszyn wirtualnych VMware do platformy Azure przy użyciu programu PowerShell odzyskiwania lokacji Azure

W tym artykule zobacz sposób replikowania i pracy awaryjnej maszyn wirtualnych VMware do platformy Azure przy użyciu programu Azure PowerShell. 

Omawiane kwestie:

> [!div class="checklist"]
> - Utwórz magazyn usługi Recovery Services.
> - Ustaw kontekst magazynu.
> - Sprawdź poprawność konfiguracji serwera i skalowania w poziomie serwerów procesu zarejestrowanych w magazynie.
> - Utwórz zasady replikacji i mapowanie go do użytku z serwerem konfiguracji.
> - Dodanie serwera vCenter i odnajdywanie maszyn wirtualnych VMware.
> - Tworzenie konta magazynu do replikowania maszyn wirtualnych.
> - Replikowanie maszyn wirtualnych VMware na kontach magazynu Azure.
> - Konfiguruj ustawienia trybu failover dla replikacji maszyn wirtualnych.
> - Wykonaj test trybu failover, weryfikowanie i oczyszczania testowy tryb failover.
> - Tryb failover na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem:
- Upewnij się, że rozumiesz [architektura scenariusza i składniki](concepts-vmware-to-azure-architecture.md).
- Przegląd [spełnić wymagania dotyczące](site-recovery-support-matrix-to-azure.md) dla wszystkich składników.
- Zainstalowana wersja 5.0.1 jest większy niż moduł AzureRm PowerShell. Jeśli musisz zainstalować lub uaktualnić programu Azure PowerShell, wykonaj to [Przewodnik instalowania i konfigurowania programu Azure PowerShell](/powershell/azureps-cmdlets-docs).

## <a name="log-in-to-your-microsoft-azure-subscription"></a>Zaloguj się do subskrypcji platformy Microsoft Azure

Zaloguj się do subskrypcji platformy Azure przy użyciu polecenia cmdlet Login-AzureRmAccount

```azurepowershell
Login-AzureRmAccount
```
Wybierz subskrypcję platformy Azure, aby zreplikować maszyny wirtualnej VMware. Aby uzyskać listę subskrypcji Azure, do których masz dostęp do, należy użyć polecenia cmdlet Get-AzureRmSubscription. Wybierz subskrypcję platformy Azure, aby pracować z za pomocą polecenia cmdlet Select-AzureRmSubscription.

```azurepowershell
Select-AzureRmSubscription -SubscriptionName "ASR Test Subscription"
```
## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

* Utwórz grupę zasobów, w której chcesz utworzyć magazyn usług odzyskiwania. W poniższym przykładzie nazwa grupy zasobów o nazwie VMwareDRtoAzurePS i jest tworzona w regionie, Azja Wschodnia.

```azurepowershell
New-AzureRmResourceGroup -Name "VMwareDRtoAzurePS" -Location "East Asia"
```
```
ResourceGroupName : VMwareDRtoAzurePS
Location          : eastasia
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VMwareDRtoAzurePS
```
   
* Tworzenie magazynu usług odzyskiwania. W poniższym przykładzie magazynu usług odzyskiwania nosi nazwę VMwareDRToAzurePs i zostanie utworzony w regionu Azja Wschodnia i grupy zasobów utworzonej w poprzednim kroku.

```azurepowershell
New-AzureRmRecoveryServicesVault -Name "VMwareDRToAzurePs" -Location "East Asia" -ResourceGroupName "VMwareDRToAzurePs"
```
```
Name              : VMwareDRToAzurePs
ID                : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VMwareDRToAzurePs/providers/Microsoft.RecoveryServices/vaults/VMwareDRToAzurePs
Type              : Microsoft.RecoveryServices/vaults
Location          : eastasia
ResourceGroupName : VMwareDRToAzurePs
SubscriptionId    : xxxxxxxx-xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
``` 

* Pobierz klucz rejestracji magazynu dla magazynu. Klucz rejestracji magazynu jest stosowana do rejestrowania lokalnego serwera konfiguracji w tym magazynie. Rejestracja jest częścią procesu instalacji oprogramowania serwera konfiguracji.

```azurepowershell
#Get the vault object by name and resource group and save it to the $vault PowerShell variable 
$vault = Get-AzureRmRecoveryServicesVault -Name "VMwareDRToAzurePS" -ResourceGroupName "VMwareDRToAzurePS"

#Download vault registration key to the path C:\Work
Get-AzureRmRecoveryServicesVaultSettingsFile -SiteRecovery -Vault $Vault -Path "C:\Work\"
```
```
FilePath
--------
C:\Work\VMwareDRToAzurePs_2017-11-23T19-52-34.VaultCredentials
```

Użyj klucza rejestracji pobranego magazynu i wykonaj kroki opisane w artykułach podane poniżej do ukończenia instalacji i rejestracji serwera konfiguracji.
* [Wybranie celów ochrony](site-recovery-set-up-vmware-to-azure.md#choose-your-protection-goals)
* [Konfigurowanie środowiska źródłowego](site-recovery-set-up-vmware-to-azure.md#set-up-the-source-environment) 

## <a name="set-the-vault-context"></a>Ustaw kontekst magazynu

> [!TIP]
> Moduł Azure PowerShell odzyskiwania lokacji (moduł AzureRm.RecoveryServices.SiteRecovery) zawiera łatwy w użyciu aliasów dla większości poleceń cmdlet. Polecenia cmdlet w module formę  *\<operacji >-**AzureRmRecoveryServicesAsr**\<obiektu >* i mieć równoważne aliasy, które będzie mieć postać  *\<Operacji >-**ASR**\<obiektu >*. W tym artykule wykorzystano aliasy polecenia cmdlet w celu ułatwienia odczytu.

Ustaw kontekst magazynu przy użyciu polecenia cmdlet Set-ASRVaultContext. Po ustawieniu kolejnych operacji usługi Azure Site Recovery w sesji programu PowerShell są wykonywane w kontekście wybranego magazynu. W poniższym przykładzie szczegółów magazynu z $vault zmienna służy do określania kontekst magazynu dla sesji programu PowerShell.
 ```azurepowershell
Set-ASRVaultContext -Vault $vault
```
```
ResourceName      ResourceGroupName ResourceNamespace          ResouceType
------------      ----------------- -----------------          -----------
VMwareDRToAzurePs VMwareDRToAzurePs Microsoft.RecoveryServices vaults
```

Kolejne sekcje w tym artykule przyjęto założenie, czy kontekst magazynu dla operacji usługi Azure Site Recovery został ustawiony.

## <a name="validate-that-your-configuration-server-and-scale-out-process-servers-are-registered-to-the-vault"></a>Sprawdź poprawność konfiguracji serwera i skalowania w poziomie serwerów procesu zarejestrowanych w magazynie

 Przykładowa:
- Serwer konfiguracji o nazwie *ConfigurationServer* został zarejestrowany w tym magazynie
- Dodatkowy serwer przetwarzania, o nazwie *ProcessServer skalowania* został zarejestrowany do *ConfigurationServer*
- Konta o nazwie *vCenter_account*, *WindowsAccount*, i *LinuxAccount* są skonfigurowane na serwerze konfiguracji. Te konta są używane, aby dodać serwer vCenter do wykrycia maszyn wirtualnych oraz do instalacji wypychanej usługi mobilności oprogramowania na serwerach z systemem Windows i Linux, które powinny być replikowane.

Zarejestrowanych serwerów konfiguracji są reprezentowane przez obiekt sieci szkieletowej w programie Azure Site Recovery. W tym kroku Pobierz listę sieci szkieletowej obiektów w magazynie i zidentyfikować serwer konfiguracji.

```azurepowershell
# Verify that the Configuration server is successfully registered to the vault
$ASRFabrics = Get-ASRFabric
$ASRFabrics.count
```
```
1
```
```azurepowershell
#Print details of the Configuration Server
$ASRFabrics[0]
```
```
Name                  : 2c33d710a5ee6af753413e97f01e314fc75938ea4e9ac7bafbf4a31f6804460d
FriendlyName          : ConfigurationServer
ID                    : /Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VMwareDRToAzurePs/providers/Microsoft.RecoveryServices/vaults/VMwareDRToAzurePs/replicationFabrics
                        /2c33d710a5ee6af753413e97f01e314fc75938ea4e9ac7bafbf4a31f6804460d
Type                  : Microsoft.RecoveryServices/vaults/replicationFabrics
FabricType            : VMware
SiteIdentifier        : ef7a1580-f356-4a00-aa30-7bf80f952510
FabricSpecificDetails : Microsoft.Azure.Commands.RecoveryServices.SiteRecovery.ASRVMWareSpecificDetails
```

* Określenie serwerów procesu, który może służyć do replikowania maszyn.

```azurepowershell
$ProcessServers = $ASRFabrics[0].FabricSpecificDetails.ProcessServers
for($i=0; $i -lt $ProcessServers.count; $i++) {
 "{0,-5} {1}" -f $i, $ProcessServers[$i].FriendlyName
}
```
```
0     ScaleOut-ProcessServer
1     ConfigurationServer
```

Z powyższych danych wyjściowych ***$ProcessServers [0]*** odpowiada *ProcessServer skalowania* i ***$ProcessServers [1]*** odpowiada roli Serwer przetwarzania na *ConfigurationServer*

* Określenie konta, które są skonfigurowane na serwerze konfiguracji.

```azurepowershell
$AccountHandles = $ASRFabrics[0].FabricSpecificDetails.RunAsAccounts
#Print the account details
$AccountHandles
```
```
AccountId AccountName
--------- -----------
1         vCenter_account
2         WindowsAccount
3         LinuxAccount
```

Z powyższych danych wyjściowych ***$AccountHandles [0]*** odnosi się do konta *vCenter_account*, ***$AccountHandles [1]*** kontu *WindowsAccount*, i ***$AccountHandles [2]*** kontu *LinuxAccount*

## <a name="create-a-replication-policy-and-map-it-for-use-with-the-configuration-server"></a>Utwórz zasady replikacji i mapowanie go do użytku z serwera konfiguracji

W tym kroku tworzone są dwie zasady replikacji. Jedna zasada do replikowania maszyn wirtualnych VMware do platformy Azure, a drugi do replikowania przejścia w tryb failover maszyn wirtualnych działających na platformie Azure z powrotem do lokalnej lokacji oprogramowania VMware.

> [!NOTE]
> Większość operacji usługi Azure Site Recovery są wykonywane asynchronicznie. Po zainicjowaniu operacji przesyłania zadania usługi Azure Site Recovery i zadania śledzenia obiekt jest zwracany. To zadanie śledzenia obiekt może służyć do monitorowania stanu operacji.

* Utwórz zasady replikacji o nazwie *ReplicationPolicy* replikacja maszyn wirtualnych VMware do platformy Azure z określonej właściwości.

```azurepowershell
$Job_PolicyCreate = New-ASRPolicy -VMwareToAzure -Name "ReplicationPolicy" -RecoveryPointRetentionInHours 24 -ApplicationConsistentSnapshotFrequencyInHours 4 -RPOWarningThresholdInMinutes 60

# Track Job status to check for completion
while (($Job_PolicyCreate.State -eq "InProgress") -or ($Job_PolicyCreate.State -eq "NotStarted")){ 
        sleep 10; 
        $Job_PolicyCreate = Get-ASRJob -Job $Job_PolicyCreate
}

#Display job status
$Job_PolicyCreate
```
```
Name             : 8d18e2d9-479f-430d-b76b-6bc7eb2d0b3e
ID               : /Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VMwareDRToAzurePs/providers/Microsoft.RecoveryServices/vaults/VMwareDRToAzurePs/replicationJobs/8d18e2d
                   9-479f-430d-b76b-6bc7eb2d0b3e
Type             :
JobType          : AddProtectionProfile
DisplayName      : Create replication policy
ClientRequestId  : a162b233-55d7-4852-abac-3d595a1faac2 ActivityId: 9895234a-90ea-4c1a-83b5-1f2c6586252a
State            : Succeeded
StateDescription : Completed
StartTime        : 11/24/2017 2:49:24 AM
EndTime          : 11/24/2017 2:49:23 AM
TargetObjectId   : ab31026e-4866-5440-969a-8ebcb13a372f
TargetObjectType : ProtectionProfile
TargetObjectName : ReplicationPolicy
AllowedActions   :
Tasks            : {Prerequisites check for creating the replication policy, Creating the replication policy}
Errors           : {}
```

* Utwórz zasady replikacji do użycia na potrzeby powrotu po awarii z platformy Azure do lokacji lokalnej VMware.

```azurepowershell
$Job_FailbackPolicyCreate = New-ASRPolicy -AzureToVMware -Name "ReplicationPolicy-Failback" -RecoveryPointRetentionInHours 24 -ApplicationConsistentSnapshotFrequencyInHours 4 -RPOWarningThresholdInMinutes 60
```

Szczegóły zadania w *$Job_FailbackPolicyCreate* do śledzenia do ukończenia operacji.

* Utwórz mapowanie kontenera ochrony, aby zamapować zasady replikacji z serwera konfiguracji.

```azurepowershell
#Get the protection container corresponding to the Configuration Server
$ProtectionContainer = Get-ASRProtectionContainer -Fabric $ASRFabrics[0]

#Get the replication policies to map by name.
$ReplicationPolicy = Get-ASRPolicy -Name "ReplicationPolicy"
$FailbackReplicationPolicy = Get-ASRPolicy -Name "ReplicationPolicy-Failback"

# Associate the replication policies to the protection container corresponding to the Configuration Server. 

$Job_AssociatePolicy = New-ASRProtectionContainerMapping -Name "PolicyAssociation1" -PrimaryProtectionContainer $ProtectionContainer -Policy $Policy[0]

# Check the job status
while (($Job_AssociatePolicy.State -eq "InProgress") -or ($Job_AssociatePolicy.State -eq "NotStarted")){ 
        sleep 10; 
        $Job_AssociatePolicy = Get-ASRJob -Job $Job_AssociatePolicy
}
$Job_AssociatePolicy.State

$Job_AssociateFailbackPolicy = New-ASRProtectionContainerMapping -Name "FailbackPolicyAssociation" -PrimaryProtectionContainer $ProtectionContainer -Policy $Policy[0]

# Check the job status
while (($Job_AssociateFailbackPolicy.State -eq "InProgress") -or ($Job_AssociateFailbackPolicy.State -eq "NotStarted")){ 
        sleep 10; 
        $Job_AssociateFailbackPolicy = Get-ASRJob -Job $Job_AssociateFailbackPolicy
}
$Job_AssociateFailbackPolicy.State

```

## <a name="add-a-vcenter-server-and-discover-vmware-virtual-machines"></a>Dodanie serwera vCenter i odnajdywanie maszyn wirtualnych VMware

Dodanie serwera vCenter według adresu IP lub nazwy hosta. **— Port** parametr określa port vCenter Server, aby nawiązać połączenie, **— nazwa** parametr określa przyjazną nazwę dla serwera vCenter i **-konta** parametr określa dojście konta na serwerze konfiguracji można użyć w celu odnalezienia maszyn wirtualnych zarządzanych przez serwer vCenter.

```azurepowershell
# The $AccountHandles[0] variable holds details of vCenter_account

$Job_AddvCenterServer = New-ASRvCenter -Fabric $ASRFabrics[0] -Name "MyvCenterServer" -IpOrHostName "10.150.24.63" -Account $AccountHandles[0] -Port 443

#Wait for the job to complete and ensure it completed successfully

while (($Job_AddvCenterServer.State -eq "InProgress") -or ($Job_AddvCenterServer.State -eq "NotStarted")) { 
        sleep 30; 
        $Job_AddvCenterServer = Get-ASRJob -Job $Job_AddvCenterServer
}
$Job_AddvCenterServer
```
```
Name             : 0f76f937-f9cf-4e0e-bf27-10c9d1c252a4
ID               : /Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VMwareDRToAzurePs/providers/Microsoft.RecoveryServices/vaults/VMwareDRToAzurePs/replicationJobs/0f76f93
                   7-f9cf-4e0e-bf27-10c9d1c252a4
Type             :
JobType          : DiscoverVCenter
DisplayName      : Add vCenter server
ClientRequestId  : a2af8892-5686-4d64-a528-10445bc2f698 ActivityId: 7ec05aad-002e-4da0-991f-95d0de7a9f3a
State            : Succeeded
StateDescription : Completed
StartTime        : 11/24/2017 2:41:47 AM
EndTime          : 11/24/2017 2:44:37 AM
TargetObjectId   : 10.150.24.63
TargetObjectType : VCenter
TargetObjectName : MyvCenterServer
AllowedActions   :
Tasks            : {Adding vCenter server}
Errors           : {}
```

## <a name="create-storage-accounts"></a>Tworzenie kont magazynu

W tym kroku są tworzone konta magazynu, które będą używane do replikacji. Te konta magazynu są używane później do replikowania maszyn wirtualnych. Upewnij się, że konta magazynu są tworzone w tym samym regionie Azure jako magazynu. Ten krok można pominąć, jeśli planujesz użyć istniejącego konta magazynu na potrzeby replikacji.

> [!NOTE]
> Podczas replikowania lokalnych maszyn wirtualnych na konto magazynu premium, należy określić dodatkowe konto magazynu (dziennika konta magazynu). Konto magazynu dziennika przechowuje dzienników replikacji jako magazynu pośredniego, dopóki Dzienniki mogą być stosowane w celu magazynu premium.
>

```azurepowershell

$PremiumStorageAccount = New-AzureRmStorageAccount -ResourceGroupName "VMwareDRToAzurePs" -Name "premiumstorageaccount1" -Location "East Asia" -SkuName Premium_LRS

$LogStorageAccount = New-AzureRmStorageAccount -ResourceGroupName "VMwareDRToAzurePs" -Name "logstorageaccount1" -Location "East Asia" -SkuName Standard_LRS

$ReplicationStdStorageAccount= New-AzureRmStorageAccount -ResourceGroupName "VMwareDRToAzurePs" -Name "replicationstdstorageaccount1" -Location "East Asia" -SkuName Standard_LRS
```

## <a name="replicate-vmware-virtual-machines"></a>Replikowanie maszyn wirtualnych VMware

Trwa około 15-20 minut dla maszyn wirtualnych, które mają zostać wykryte z serwera vCenter. Po odnaleziony, chronione elementu tworzony jest obiekt w usłudze Azure Site Recovery dla każdej odnalezionych maszyny wirtualnej. W tym kroku trzech spośród odnalezionych maszyny wirtualnej są replikowane do konta usługi Azure Storage, utworzony w poprzednim kroku.

Potrzebne są następujące szczegóły, aby chronić odnalezionych maszyny wirtualnej:
* Element chronione powinny być replikowane.
* Konta magazynu, aby replikować maszyny wirtualnej. Ponadto magazynu dziennika jest potrzebne do ochrony maszyn wirtualnych na konto magazynu premium.
* Proces serwera, który ma być używany do replikacji. Na liście serwerów dostępnych procesu zostało pobrane i zapisywane w ***$ProcessServers [0]****(skalowania ProcessServer)* i ***$ProcessServers [1]*** *(ConfigurationServer)* zmiennych.
* Konto używane do instalacji wypychanej usługi mobilności oprogramowania na komputerach. Lista dostępnych kont zostało pobrane i przechowywane w ***$AccountHandles*** zmiennej.
* Mapowanie kontenera ochrony dla grupy replikacji do zastosowania w przypadku replikacji.
* Grupy zasobów, w którym należy utworzyć maszyny wirtualnej w tryb failover.
* Opcjonalnie sieci wirtualnej platformy Azure i podsieć, z którą nie powiodło się na maszynie wirtualnej powinny być połączone.

Teraz replikacji przy użyciu ustawień określonych w tej tabeli następujące maszyny wirtualne


|Maszyna wirtualna  |Serwer przetwarzania        |Konto magazynu              |Konto magazynu dziennika  |Zasady           |Konto instalacji usługi mobilności|Docelowa grupa zasobów  | Docelowy sieci wirtualnej  |Docelowej podsieci  |
|-----------------|----------------------|-----------------------------|---------------------|-----------------|-----------------------------------------|-----------------------|-------------------------|---------------|
|Win2K12VM1       |ProcessServer skalowania w poziomie|premiumstorageaccount1       |logstorageaccount1   |ReplicationPolicy|WindowsAccount                           |VMwareDRToAzurePs      |Sieć wirtualna ASR                 |Podsieć 1       |
|CentOSVM1       |ConfigurationServer   |replicationstdstorageaccount1| ND                 |ReplicationPolicy|LinuxAccount                             |VMwareDRToAzurePs      |Sieć wirtualna ASR                 |Podsieć 1       |   
|CentOSVM2       |ConfigurationServer   |replicationstdstorageaccount1| ND                 |ReplicationPolicy|LinuxAccount                             |VMwareDRToAzurePs      |Sieć wirtualna ASR                 |Podsieć 1       |   

 
```azurepowershell

#Get the target resource group to be used
$ResourceGroup = Get-AzureRmResourceGroup -Name "VMwareToAzureDrPs"

#Get the target virtual network to be used
$RecoveryVnet = Get-AzureRmVirtualNetwork -Name "ASR-vnet" -ResourceGroupName "asrrg" 

#Get the protection container mapping for replication policy named ReplicationPolicy
$PolicyMap  = Get-ASRProtectionContainerMapping -ProtectionContainer $ProtectionContainer | where PolicyFriendlyName -eq "ReplicationPolicy"

#Get the protectable item corresponding to the virtual machine Win2K12VM1
$VM1 = Get-ASRProtectableItem -ProtectionContainer $ProtectionContainer -FriendlyName "Win2K12VM1"

# Enable replication for virtual machine Win2K12VM1
# The name specified for the replicated item needs to be unique within the protection container. Using a random GUID to ensure uniqueness
$Job_EnableRepication1 = New-ASRReplicationProtectedItem -VMwareToAzure -ProtectableItem $VM1 -Name (New-Guid).Guid -ProtectionContainerMapping $PolicyMap -RecoveryAzureStorageAccountId $PremiumStorageAccount.Id -LogStorageAccountId $LogStorageAccount.Id -ProcessServer $ProcessServers[0] -Account $AccountHandles[1] -RecoveryResourceGroupId $ResourceGroup.ResourceId -RecoveryAzureNetworkId $RecoveryVnet.Id -RecoveryAzureSubnetName "Subnet-1" 

#Get the protectable item corresponding to the virtual machine CentOSVM1
$VM2 = Get-ASRProtectableItem -ProtectionContainer $ProtectionContainer -FriendlyName "CentOSVM1"

# Enable replication for virtual machine CentOSVM1
$Job_EnableRepication2 = New-ASRReplicationProtectedItem -VMwareToAzure -ProtectableItem $VM2 -Name (New-Guid).Guid -ProtectionContainerMapping $PolicyMap -RecoveryAzureStorageAccountId $ReplicationStdStorageAccount.Id  -ProcessServer $ProcessServers[1] -Account $AccountHandles[2] -RecoveryResourceGroupId $ResourceGroup.ResourceId -RecoveryAzureNetworkId $RecoveryVnet.Id -RecoveryAzureSubnetName "Subnet-1"

#Get the protectable item corresponding to the virtual machine CentOSVM2
$VM3 = Get-ASRProtectableItem -ProtectionContainer $ProtectionContainer -FriendlyName "CentOSVM2"

# Enable replication for virtual machine CentOSVM2
$Job_EnableRepication3 = New-ASRReplicationProtectedItem -VMwareToAzure -ProtectableItem $VM3 -Name (New-Guid).Guid -ProtectionContainerMapping $PolicyMap -RecoveryAzureStorageAccountId $ReplicationStdStorageAccount.Id  -ProcessServer $ProcessServers[1] -Account $AccountHandles[2] -RecoveryResourceGroupId $ResourceGroup.ResourceId -RecoveryAzureNetworkId $RecoveryVnet.Id -RecoveryAzureSubnetName "Subnet-1" 

```

Po replikacji Włącz zadanie zostało ukończone pomyślnie, Replikacja początkowa została uruchomiona dla maszyn wirtualnych. Replikacja początkowa może trochę potrwać w zależności od ilości danych do replikacji oraz przepustowość dostępną dla replikacji. Po ukończeniu replikacji początkowej, maszyna wirtualna zostanie przeniesiona do stanu chronionych. Gdy maszyna wirtualna osiągnie stan chronionych, które można wykonać test trybu failover dla maszyny wirtualnej, należy go dodać do planów odzyskiwania itp.

Możesz sprawdzić stan replikacji i kondycję replikacji maszyny wirtualnej za pomocą polecenia cmdlet Get-ASRReplicationProtectedItem.

```azurepowershell
Get-ASRReplicationProtectedItem -ProtectionContainer $ProtectionContainer | Select FriendlyName, ProtectionState, ReplicationHealth
```
```
FriendlyName ProtectionState                 ReplicationHealth
------------ ---------------                 -----------------
CentOSVM1    Protected                       Normal
CentOSVM2    InitialReplicationInProgress    Normal
Win2K12VM1   Protected                       Normal
```

## <a name="configure-failover-settings-for-replicating-virtual-machines"></a>Konfiguruj ustawienia trybu failover dla replikacji maszyn wirtualnych

Ustawienia trybu failover dla chronionych maszyn może zostać zaktualizowana przy użyciu polecenia cmdlet Set-ASRReplicationProtectedItem. Niektóre ustawienia, które mogą zostać zaktualizowane za pomocą tego polecenia cmdlet są:
* Nazwa maszyny wirtualnej, która ma zostać utworzony w tryb failover
* Rozmiar maszyny wirtualnej, która ma zostać utworzony w tryb failover maszyny Wirtualnej
* Sieć wirtualna platformy Azure i podsieć, która kart sieciowych maszyny wirtualnej powinny być podłączone do na trybu failover
* Tryb failover do zarządzanych dysków
* Zastosuj korzyści Użyj hybrydowe platformy Azure
* Przypisz statyczny adres IP z sieci wirtualnej docelowy ma być przypisany do maszyny wirtualnej w tryb failover.

W tym przykładzie modyfikacjom rozmiar maszyny Wirtualnej maszyny wirtualnej, która ma zostać utworzony w tryb failover maszyny wirtualnej *Win2K12VM1* i określ, czy użyć maszyny wirtualnej zarządzanych dyski w tryb failover.

```azurepowershell
$ReplicatedVM1 = Get-ASRReplicationProtectedItem -FriendlyName "Win2K12VM1" -ProtectionContainer $ProtectionContainer

Set-ASRReplicationProtectedItem -InputObject $ReplicatedVM1 -Size "Standard_DS11" -UseManagedDisk True
```
```
Name             : cafa459c-44a7-45b0-9de9-3d925b0e7db9
ID               : /Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/VMwareDRToAzurePs/providers/Microsoft.RecoveryServices/vaults/VMwareDRToAzurePs/replicationJobs/cafa459
                   c-44a7-45b0-9de9-3d925b0e7db9
Type             :
JobType          : UpdateVmProperties
DisplayName      : Update the virtual machine
ClientRequestId  : b0b51b2a-f151-4e9a-a98e-064a5b5131f3 ActivityId: ac2ba316-be7b-4c94-a053-5363f683d38f
State            : InProgress
StateDescription : InProgress
StartTime        : 11/24/2017 2:04:26 PM
EndTime          :
TargetObjectId   : 88bc391e-d091-11e7-9484-000c2955bb50
TargetObjectType : ProtectionEntity
TargetObjectName : Win2K12VM1
AllowedActions   :
Tasks            : {Update the virtual machine properties}
Errors           : {}
```

## <a name="perform-a-test-failover-validate-and-cleanup-test-failover"></a>Wykonaj test trybu failover, weryfikowanie i oczyszczania testowy tryb failover

```azurepowershell
#Test failover of Win2K12VM1 to the test virtual network "V2TestNetwork"

#Get details of the test failover virtual network to be used
TestFailovervnet = Get-AzureRmVirtualNetwork -Name "V2TestNetwork" -ResourceGroupName "asrrg" 

#Start the test failover operation
$TFOJob = Start-ASRTestFailoverJob -ReplicationProtectedItem $ReplicatedVM1 -AzureVMNetworkId $TestFailovervnet.Id -Direction PrimaryToRecovery
```
Po zadania testowego trybu failover zakończy się pomyślnie, można zauważyć, że maszynę wirtualną z sufiksem *"-Test"* (w tym przypadku Win2K12VM1-Test) do jego nazwa jest tworzona na platformie Azure. 

Można teraz nawiązać połączenia testowego przejścia w tryb failover maszyny wirtualnej i sprawdź poprawność testowania trybu failover.

Oczyszczanie test trybu failover przy użyciu polecenia cmdlet Start-ASRTestFailoverCleanupJob. Ta operacja usuwa z maszyną wirtualną utworzoną w ramach operacji trybu failover testu.

```azurepowershell
$Job_TFOCleanup = Start-ASRTestFailoverCleanupJob -ReplicationProtectedItem $ReplicatedVM1
```

## <a name="failover-to-azure"></a>Tryb failover na platformie Azure

W tym kroku będziemy trybu failover maszyny wirtualnej Win2K12VM1 określony punkt odzyskiwania.

```azurepowershell
# Get the list of available recovery points for Win2K12VM1
$RecoveryPoints = Get-ASRRecoveryPoint -ReplicationProtectedItem $ReplicatedVM1
"{0} {1}" -f $RecoveryPoints[0].RecoveryPointType, $RecoveryPoints[0].RecoveryPointTime
```
```
CrashConsistent 11/24/2017 5:28:25 PM
```
```azurepowershell

#Start the failover job
$Job_Failover = Start-ASRUnplannedFailoverJob -ReplicationProtectedItem $ReplicatedVM1 -Direction PrimaryToRecovery -RecoveryPoint $RecoveryPoints[0]
do {
        $Job_Failover = Get-ASRJob -Job $Job_Failover;
        sleep 60;
} while (($Job_Failover.State -eq "InProgress") -or ($JobFailover.State -eq "NotStarted"))
$Job_Failover.State
```
```
Succeeded
```

Po pomyślnym przejścia w tryb failover, można zatwierdzić pracy awaryjnej operacji i Instalator replikacja odwrotna z platformy Azure z powrotem do lokalnej lokacji oprogramowania VMware.

## <a name="next-steps"></a>Kolejne kroki
Widok [Azure PowerShell odzyskiwania lokacji odniesienia ](https://docs.microsoft.com/powershell/module/AzureRM.RecoveryServices.SiteRecovery) Aby dowiedzieć się, jak można wykonywać inne zadania, takie jak tworzenie planów odzyskiwania i testowania trybu failover planu odzyskiwania za pomocą programu PowerShell.
