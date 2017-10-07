---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V z programu PowerShell i usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Zautomatyzować hello replikacji maszyn wirtualnych funkcji Hyper-V tooAzure z usługą Azure Site Recovery przy użyciu programu PowerShell i Menedżera zasobów Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Replikowanie między maszynami wirtualnymi funkcji Hyper-V lokalnymi i Azure przy użyciu programu PowerShell i usługi Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Klasyczny portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Omówienie
Usługa Azure Site Recovery przyczynia się tooyour ciągłości i awaryjnego odzyskiwania strategii biznesowej poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania. Aby uzyskać pełną listę scenariuszy wdrażania, zobacz hello [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).

Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą programu Windows PowerShell. Może współpracować z dwóch typów modułów: hello modułu Azure profilu lub hello moduł usługi Azure Resource Manager.

Lokacji odzyskiwania poleceń cmdlet programu PowerShell, dostępna przy użyciu programu Azure PowerShell dla usługi Azure Resource Manager pomóc chronić i odzyskiwać serwerów na platformie Azure.

W tym artykule opisano sposób toouse środowiska Windows PowerShell razem z usługą Azure Resource Manager, toodeploy tooconfigure usługi Site Recovery i organizowania tooAzure ochrony serwera. przykład Witaj używane w tym artykule przedstawiono sposób tooprotect, tryb failover i odzyskiwanie maszyn wirtualnych na tooAzure hosta funkcji Hyper-V za pomocą programu Azure PowerShell z usługą Azure Resource Manager.

> [!NOTE]
> Witaj poleceń cmdlet programu PowerShell odzyskiwania lokacji obecnie pozwalają hello tooconfigure następujące: jeden tooanother witryny programu Virtual Machine Manager, tooAzure witryny programu Virtual Machine Manager i tooAzure lokacji funkcji Hyper-V.
>
>

Nie ma potrzeby toobe toouse ekspertów programu PowerShell w tym artykule, ale trzeba toounderstand hello podstawowe pojęcia, takie jak moduły, polecenia cmdlet i sesje. Aby uzyskać więcej informacji na temat programu Windows PowerShell, zobacz [Wprowadzenie do programu Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).

Można również uzyskać więcej informacji [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Partnerzy firmy Microsoft, które są częścią programu Cloud Solution Provider (CSP) hello można konfigurować i zarządzać ochrony serwerów ich klientom odpowiednich klientów tootheir subskrypcje dostawcy usług Kryptograficznych (subskrypcje dzierżawy).
>
>

## <a name="before-you-start"></a>Przed rozpoczęciem
Upewnij się, że te wymagania wstępne zostały spełnione:

* A [Microsoft Azure](https://azure.microsoft.com/) konta. Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). Ponadto możesz przeczytać temat [cennik usługi Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Aby uzyskać informacje na temat tej wersji i w jaki sposób tooinstall, zobacz [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Witaj [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) i [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modułów. Możesz pobrać najnowsze wersje tych modułów hello ze hello [galerii programu PowerShell](https://www.powershellgallery.com/)

W tym artykule przedstawiono sposób toouse programu Azure Powershell z tooconfigure usługi Azure Resource Manager i zarządzania ochroną serwerów. przykład Witaj używane w tym artykule przedstawiono sposób tooprotect maszynę wirtualną na hoście funkcji Hyper-V, tooAzure uruchomiony. Witaj następujące wymagania wstępne są określone toothis przykładów. Wyczerpujący zestaw wymagań dotyczących hello różne scenariusze odzyskiwania lokacji, zapoznaj się z dokumentacją toohello dotyczące toothat scenariusza.

* Hosta funkcji Hyper-V z systemem Windows Server 2012 R2 lub Microsoft Hyper-V Server 2012 R2 zawierającego co najmniej jednej maszyny wirtualnej.
* Serwery funkcji Hyper-V połączony toohello Internetu, bezpośrednio lub za pośrednictwem serwera proxy.
* Witaj maszyn wirtualnych, które mają tooprotect powinna być zgodna z [wymagania wstępne dotyczące maszyny wirtualnej](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Krok 1: Zaloguj się tooyour konto platformy Azure
1. Otwórz konsolę programu PowerShell i uruchom to polecenie toosign w tooyour konto platformy Azure. polecenia cmdlet Hello powoduje wyświetlenie strony sieci web, która spowoduje wyświetlenie monitu o podanie poświadczeń konta.

        Login-AzureRmAccount

    Alternatywnie możesz także dołączyć poświadczeń konta jako toohello parametru `Login-AzureRmAccount` polecenia cmdlet, za pomocą hello `-Credential` parametru.

    W przypadku dostawcy usług Kryptograficznych partnera pracy imieniu dzierżawcy Określ powitania klienta dzierżawcy, przy użyciu nazwy domeny głównej dla identyfikatora dzierżawcy lub dzierżawcy.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Konta może mieć kilka subskrypcji, więc należy skojarzyć hello subskrypcję toouse hello konta.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Sprawdź, czy subskrypcja jest zarejestrowanych toouse hello Azure dostawców dla usług odzyskiwania i Site Recovery przy użyciu następującego polecenia hello:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   W hello dane wyjściowe tych poleceń, jeśli hello **RegistrationState** ustawiono zbyt**zarejestrowanej**, możesz przejść tooStep 2. Jeśli nie, należy zarejestrować dostawcę Brak hello w ramach subskrypcji.

   Witaj tooregister dostawca usługi Azure Site Recovery i usług odzyskiwania, uruchom następujące polecenia hello:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Sprawdź, czy dostawców hello pomyślnie zarejestrowane za pomocą następującego polecenia hello: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` i `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Krok 2: Konfigurowanie powitalne magazyn usług odzyskiwania
1. Utwórz grupę zasobów usługi Azure Resource Manager, w którym można będzie utworzyć magazyn hello, lub użyj istniejącej grupy zasobów. Można utworzyć nową grupę zasobów, przy użyciu hello następujące polecenie:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    w przypadku, gdy zmienna hello $ResourceGroupName zawiera hello nazwę grupy zasobów hello ma toocreate, a zmienna hello $Geo zawiera hello Azure regionu, w których grupa zasobów hello toocreate (na przykład "Brazylia Południowa").

    Można uzyskać listy grup zasobów w ramach subskrypcji, za pomocą hello `Get-AzureRmResourceGroup` polecenia cmdlet.
2. Utwórz nowy magazyn usług odzyskiwania Azure w następujący sposób:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Można pobrać listy istniejących magazynów za pomocą hello `Get-AzureRmRecoveryServicesVault` polecenia cmdlet.

> [!NOTE]
> Jeśli chcesz, aby operacje tooperform magazynów usługi Site Recovery utworzony przy użyciu klasycznego portalu hello lub hello modułu programu PowerShell do zarządzania usługi Azure, można pobrać listę takich magazynów za pomocą hello `Get-AzureRmSiteRecoveryVault` polecenia cmdlet. Należy utworzyć nowy magazyn usług odzyskiwania dla wszystkich nowych operacji. Witaj magazynów usługi Site Recovery, utworzony wcześniej są obsługiwane, ale nie ma hello najnowszych funkcji.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Krok 3: Ustawianie hello kontekst magazynu usług odzyskiwania
1. Ustaw kontekst magazynu hello, uruchamiając następujące polecenie hello:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Krok 4: Tworzenie lokacji funkcji Hyper-V i wygenerowanie nowego klucza rejestracji magazynu hello witryny.
1. Utwórz nową witrynę funkcji Hyper-V w następujący sposób:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    To polecenie cmdlet uruchamia lokacji hello toocreate zadania usługi Site Recovery i zwraca obiekt zadania usługi Site Recovery. Poczekaj, aż hello toocomplete zadania i Sprawdź zadania hello zakończyła się pomyślnie.

    Można pobrać obiektu zadania hello i tym samym sprawdź bieżący stan zadania hello hello za pomocą polecenia cmdlet Get-AzureRmSiteRecoveryJob hello.
2. Generowanie i Pobierz klucz rejestracji dla lokacji hello w następujący sposób:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Kopia hello pobrane hosta klucza toohello funkcji Hyper-V. Należy hello klucza tooregister hello funkcji Hyper-V host toohello lokacji.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Krok 5: Instalowanie dostawcy usługi Azure Site Recovery hello i Agent usług odzyskiwania Azure na hoście funkcji Hyper-V
1. Pobierz Instalator hello hello najnowsza wersja dostawcy hello z [Microsoft](https://aka.ms/downloaddra).
2. Hello uruchom Instalator na hoście funkcji Hyper-V, a na końcu instalacji hello hello nadal toohello kroku rejestracji.
3. Po wyświetleniu monitu podaj hello pobranych klucz rejestracji lokacji i zakończyć rejestrację witryny toohello hosta funkcji Hyper-V hello.
4. Sprawdź, czy hostujących hello funkcji Hyper-V jest zarejestrowany toohello lokacji za pomocą następującego polecenia hello:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Krok 6: Tworzenie zasad replikacji i powiązać ją z kontenera ochrony hello
1. Utwórz zasady replikacji w następujący sposób:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Witaj wyboru zwrócił tooensure zadania, które tworzenia zasad replikacji hello zakończyło się pomyślnie.

   > [!IMPORTANT]
   > Witaj określone konto magazynu powinna być w hello tego samego regionu Azure co magazyn usług odzyskiwania i ma włączoną replikację geograficzną.
   >
   > * Jeśli hello określony odzyskiwania konta magazynu jest typu usługi Azure Storage (klasyczny), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (klasyczny).
   > * Jeśli hello określono konto magazynu odzyskiwania jest typu magazynu Azure (Azure Resource Manager), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (usługi Azure Resource Manager).
   >
   >
2. Pobierz hello ochrony kontenera odpowiedniej toohello lokacji, w następujący sposób:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Uruchom skojarzenia hello kontenera ochrony hello hello zasady replikacji, w następujący sposób:

     $Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-$Policy zasad - PrimaryProtectionContainer $protectionContainer

   Poczekaj, aż hello skojarzenia zadania toocomplete i upewnij się, czy zakończyła się pomyślnie.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Krok 7: Włączanie ochrony dla maszyn wirtualnych
1. Pobierz odpowiedni toohello jednostki ochrony hello maszyna wirtualna ma tooprotect, w następujący sposób:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Start ochrona powitalnych maszyny wirtualnej, w następujący sposób:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Witaj określone konto magazynu powinna być w hello tego samego regionu Azure co magazyn usług odzyskiwania i ma włączoną replikację geograficzną.
   >
   > * Jeśli hello określony odzyskiwania konta magazynu jest typu usługi Azure Storage (klasyczny), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (klasyczny).
   > * Jeśli hello określono konto magazynu odzyskiwania jest typu magazynu Azure (Azure Resource Manager), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (usługi Azure Resource Manager).
   >
   > Jeśli hello chronisz maszyny Wirtualnej ma więcej niż jedną tooit dołączony na dysku, określ dysk systemu operacyjnego hello przy użyciu hello *OSDiskName* parametru.
   >
   >
3. Poczekaj na powitania tooreach maszyn wirtualnych chronionych stanu po replikacji początkowej hello. Może to potrwać kilka minut w zależności od czynników, takich jak hello ilość danych toobe replikowane. i hello tooAzure dostępną przepustowość nadrzędnego. Stan zadania Hello i StateDescription zaktualizowano następujące na powitania osiągnięcia chronionych stan maszyny Wirtualnej.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Właściwości odzyskiwania, takich jak hello rozmiaru roli maszyny Wirtualnej i pracy awaryjnej hello sieć platformy Azure tooattach hello maszyny wirtualnej sieci interfejsu karty tooupon aktualizacji.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Krok 8: Uruchom test trybu failover
1. Uruchom zadania testowego trybu failover, w następujący sposób:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Sprawdź test hello utworzenia maszyny Wirtualnej na platformie Azure. (hello test pracy awaryjnej zadanie zostanie zawieszone, po utworzeniu hello testowej maszyny Wirtualnej na platformie Azure. Witaj zadanie zostało ukończone przez czyszczenie artefaktów hello utworzona po wznowieniu zadania hello, jak pokazano w następnym kroku hello.)
3. Hello pełny test trybu failover, w następujący sposób:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej](https://msdn.microsoft.com/library/azure/mt637930.aspx) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.
