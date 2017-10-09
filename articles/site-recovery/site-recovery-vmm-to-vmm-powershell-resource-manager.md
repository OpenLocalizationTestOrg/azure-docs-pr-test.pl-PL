---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V w lokacji dodatkowej tooa VMM przy użyciu programu PowerShell (usługi Azure Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toodeploy usługi Azure Site Recovery tooorchestrate replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooa lokacja dodatkowa programu VMM przy użyciu programu PowerShell (Resource Manager)"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooa lokacja dodatkowa programu VMM przy użyciu programu PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Klasyczny portal](site-recovery-vmm-to-vmm-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Usługa Site Recovery tooAzure Zapraszamy! W tym artykule należy użyć, jeśli tooreplicate lokalnych maszyn wirtualnych funkcji Hyper-V zarządzanych w lokacji dodatkowej tooa chmur programu System Center Virtual Machine Manager (VMM).

W tym artykule opisano, jak toouse PowerShell tooautomate typowych zadań należy tooperform podczas konfigurowania maszyny wirtualnej funkcji Hyper-V tooreplicate usługi Azure Site Recovery w chmurach VMM tooSystem Center chmur programu System Center VMM w lokacji dodatkowej.

Hello artykuł zawiera wymagania wstępne dla scenariusza hello i pokazuje

* Jak tooset się magazynu usług odzyskiwania
* Zainstaluj hello dostawcy usługi Azure Site Recovery na źródłowym serwerze programu VMM hello i hello docelowym serwerze VMM
* Zarejestruj hello serwery VMM w magazynie hello
* Skonfiguruj zasady replikacji dla hello chmury VMM. ustawienia replikacji Hello hello zasady zostaną zastosowane tooall chronione maszyny wirtualne
* Włącz ochronę maszyn wirtualnych hello.
* Testowanie trybu failover hello maszyn wirtualnych, pojedynczo lub w ramach planu odzyskiwania toomake się, że wszystko działa zgodnie z oczekiwaniami.
* Wykonaj planowane lub nieplanowane przełączenie awaryjne maszyn wirtualnych, pojedynczo lub w ramach planu odzyskiwania toomake się, że wszystko działa zgodnie z oczekiwaniami.

Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Platforma Azure ma dwa różne [modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md) związane z tworzeniem zasobów i pracą z nimi: Azure Resource Manager i model klasyczny. Azure ma dwa portale — klasyczny portal Azure obsługującym hello klasycznego modelu wdrażania hello i hello portalu Azure z obsługą oba modele wdrażania. W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.
>
>

## <a name="on-premises-prerequisites"></a>Lokalne wymagania wstępne
Oto, co jest potrzebne w hello głównej i dodatkowej lokalnymi lokacji toodeploy tego scenariusza:

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **VMM** |Zaleca się wdrożyć serwer VMM w lokacji głównej hello a serwerem programu VMM w lokacji dodatkowej hello.<br/><br/> Możesz również [replikacji między chmurami na jednym serwerze VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo to będziesz potrzebować co najmniej dwóch chmur skonfigurowane na serwerze VMM hello.<br/><br/> Serwery VMM powinna być uruchomiona co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami hello.<br/><br/> Każdy serwer VMM musi mieć jedną lub więcej chmur skonfigurowane i wszystkich chmur musi mieć zestawu profilu pojemności funkcji Hyper-V hello. <br/><br/>Chmury muszą zawierać co najmniej jedną grupę hostów programu VMM.<br/><br/>Dowiedz się więcej o konfigurowaniu chmur VMM w [sieci szkieletowej chmury hello Konfigurowanie VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), i [wskazówki: tworzenie chmur prywatnych z programu System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> Program VMM serwery powinny mieć dostęp do Internetu. |
| **Funkcja Hyper-V** |Serwery funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą funkcji Hyper-V hello i mieć hello zainstalowane najnowsze aktualizacje.<br/><br/> Serwer funkcji Hyper-V powinien zawierać co najmniej jedną maszynę wirtualną.<br/><br/>  Serwery hosta funkcji Hyper-V powinien znajdować się w grupach hostów w hello głównych i dodatkowych chmurach VMM.<br/><br/> Jeśli używasz funkcji Hyper-V w klastrze systemu Windows Server 2012 R2 należy zainstalować [zaktualizować 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Jeśli korzystasz z funkcji Hyper-V w klastrze na Uwaga systemu Windows Server 2012 broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP. Będziesz potrzebować brokera klastra hello tooconfigure ręcznie. [Dowiedz się więcej](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Dostawca** |Podczas wdrażania usługi Site Recovery należy zainstalować na serwerach VMM hello dostawcy usługi Azure Site Recovery. Hello dostawca komunikuje się z usługą Site Recovery za pośrednictwem protokołu HTTPS 443 tooorchestrate replikacji. Jest wykonywana replikacja danych między hello podstawowe i pomocnicze serwery funkcji Hyper-V za pośrednictwem hello sieci LAN lub połączenie sieci VPN.<br/><br/> Hello dostawca uruchomiony na serwerze VMM hello musi uzyskać dostępu do adresów URL toothese: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.<br/><br/> Ponadto Zezwalaj na komunikację zapory z toohello serwery VMM hello [zakresy IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i umożliwić hello protokołu HTTPS (port 443). |

### <a name="network-mapping-prerequisites"></a>Wymagania wstępne związane z mapowaniem sieci
Mapowanie sieci działa między sieciami maszyn wirtualnych VMM na powitania podstawowym i pomocniczym serwerze programu VMM do:

* Optymalnie umieścić po pracy awaryjnej maszyn wirtualnych repliki dodatkowej hosty funkcji Hyper-V.
* Połączenia sieci VM tooappropriate maszyn wirtualnych repliki.
* Jeśli nie zostanie skonfigurowana sieć mapowania repliki maszyn wirtualnych nie będą tooany połączonych sieci po pracy awaryjnej.
* Jeśli chcesz, aby tooset sieć mapowania podczas odzyskiwania lokacji wdrożenia w tym miejscu to co jest potrzebne:

  * Upewnij się, że maszyny wirtualne w źródle powitania serwera hosta funkcji Hyper-V są tooa połączonych sieci maszyny Wirtualnej VMM. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.
  * Sprawdź, czy hello dodatkowej chmury, które będzie używane do odzyskiwania ma skonfigurowane odpowiednie sieci maszyny Wirtualnej. Ta sieć maszyn wirtualnych powinny być tooa połączone sieci logicznej, która ma powiązanego z chmurą dodatkowej hello.

Dowiedz się więcej o konfigurowaniu sieci w programie VMM w hello poniżej artykułów

* [Jak tooconfigure sieci logicznych w programie VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Jak tooconfigure maszyny Wirtualnej sieci i bram w programie VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Dowiedz się więcej](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) o tym, jak działa mapowanie sieci.

### <a name="powershell-prerequisites"></a>Wymagania wstępne programu PowerShell
Upewnij się, że masz toogo gotowy programu Azure PowerShell. Jeśli korzystasz już z programu PowerShell, potrzebujesz tooupgrade tooversion 0.8.10 lub nowszym. Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz hello [prowadzą tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs). Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet hello hello usługi [tutaj](/powershell/azure/overview).

toolearn o porad ułatwiających przy użyciu poleceń cmdlet hello, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz hello [przewodnik tooget uruchomiona za pomocą poleceń cmdlet Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Krok 1: Ustaw hello subskrypcji
1. Z programu Azure powershell tooyour logowania konta platformy Azure: za pomocą następującego polecenia cmdlet hello

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Pobierz listę subskrypcji. To wyświetla również hello subscriptionIDs dla każdego hello subskrypcji. Zanotuj identyfikator subskrypcji hello hello subskrypcji, w którym chcesz magazynu usług odzyskiwania hello toocreate    

        Get-AzureRmSubscription
3. Ustaw hello subskrypcji, w których hello magazynu usług odzyskiwania jest utworzony, podając identyfikator subskrypcji hello toobe

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Krok 2. Tworzenie magazynu Usług odzyskiwania
1. Tworzenie grupy zasobów platformy Azure Resource Manager, jeśli nie masz już

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Utwórz nowy magazyn usług odzyskiwania i zapisać hello utworzony obiekt magazynu ASR w zmiennej (zostanie później użyty). Można również pobierać hello ASR magazynu obiektu post tworzenia przy użyciu polecenia cmdlet Get-AzureRMRecoveryServicesVault hello:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Krok 3: Ustaw hello kontekst magazynu usług odzyskiwania
1. Jeśli masz już utworzony magazyn, należy uruchomić hello poniżej polecenia tooget hello magazynu.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Ustaw kontekst magazynu hello uruchamiając hello poniżej polecenia.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Krok 4: Instalowanie hello dostawcy usługi Azure Site Recovery
1. Na maszynie VMM hello należy utworzyć katalog, uruchamiając następujące polecenie hello:

       New-Item c:\ASR -type directory
2. Wyodrębnij pliki hello przy użyciu dostawcy hello pobrane, uruchamiając następujące polecenie hello

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Zainstaluj dostawcę hello przy użyciu hello następującego polecenia:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Poczekaj na powitania toofinish instalacji.
4. Zarejestruj serwer hello w magazynie hello przy użyciu hello następujące polecenie:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>Krok 5: Utwórz i Skojarz zasady replikacji
1. Utwórz zasady replikacji funkcji Hyper-V 2012 R2, uruchamiając następujące polecenie hello:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Witaj chmury VMM może zawierać hosty funkcji Hyper-V z różnymi wersjami systemu Windows Server (jak wspomniano w wymagania wstępne funkcji Hyper-V hello), ale zasady replikacji hello jest właściwego dla wersji systemu operacyjnego. Jeśli masz różnych hostach z systemem w wersji systemów operacyjnych, następnie utwórz zasady replikacji osobne dla każdego typu wersji systemu operacyjnego. Aby uzyskać np: Jeśli masz pięć hostów z uruchomionym systemem Windows 2012 serwerów i trzech w systemie Windows Server 2012 R2, należy utworzyć dwa zasady replikacji — po jednej dla każdego typu wersji systemu operacyjnego.

1. Pobierz kontener ochronę podstawową hello (podstawowy chmury VMM) i odzyskiwania kontenera ochrony (odzyskiwania chmury VMM), uruchamiając następujące polecenia hello:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Pobierania zasad hello utworzonego w kroku 1 przy użyciu przyjaznej nazwy zasady hello hello

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Uruchom skojarzenie hello hello kontenera ochrony (w chmurze VMM) z zasadami replikacji hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Poczekaj, aż toocomplete zadania skojarzenia zasad hello. Możesz sprawdzić, jeśli zadania hello zakończone przy użyciu powitania po fragment programu PowerShell.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Po zakończeniu przetwarzania zadania hello, uruchom następujące polecenie hello:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).

## <a name="step-6-configure-network-mapping"></a>Krok 6: Skonfigurowanie mapowania sieci
1. Witaj pierwsze polecenie pobiera serwerów hello bieżący magazyn Azure Site Recovery. polecenie Hello przechowuje hello serwerów Microsoft Azure Site Recovery w hello $Servers tablicy zmiennej.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Witaj poniżej polecenia Pobierz sieć odzyskiwania lokacji hello hello źródłowym serwerze programu VMM i hello docelowym serwerze VMM.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > Witaj źródłowym serwerze programu VMM można Witaj, pierwszy lub hello drugi hello w jednym serwerów tablicy. Sprawdź nazwy hello hello serwerów programu VMM i odpowiednio uzyskać hello sieci


1. polecenie cmdlet końcowego Hello tworzy mapowanie między hello sieci podstawowej i hello odzyskiwania sieci. polecenia cmdlet Hello określa hello sieci podstawowej jako pierwszy element hello $PrimaryNetworks i hello sieci odzyskiwania jako pierwszy element $RecoveryNetworks hello.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Krok 7: Konfigurowanie mapowania magazynu
1. Witaj poniżej polecenie pobiera hello Lista klasyfikacji magazynu do zmiennej $storageclassifications.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Hello poniżej polecenia pobrania hello źródła klasyfikacji w zmiennej $SourceClassificaion i klasyfikacji docelowego w zmiennej $TargetClassification.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > klasyfikacje Hello źródłowym i docelowym może być dowolny element w tablicy hello. Zobacz dane wyjściowe toohello hello poniżej indeks hello toofigure polecenia źródłowa i docelowa klasyfikacji $storageclassifications tablicy.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object - FriendlyName właściwości, identyfikator | Formatowanie tabeli


1. Hello poniżej polecenie cmdlet tworzy mapowanie między hello źródła klasyfikacji i hello docelowy klasyfikacji.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Krok 8. Włączanie ochrony dla maszyn wirtualnych
Po hello serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello.

1. Ochrona tooenable hello uruchom następujące polecenia kontenera ochrony hello tooget:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Pobierz jednostki ochrony hello (VM), uruchamiając następujące polecenie hello:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Włącz replikację hello maszyny Wirtualnej, uruchamiając następujące polecenie hello:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Testowanie wdrożenia
Planowanie wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania składające się z wielu maszyn wirtualnych i uruchomić test trybu failover dla hello tootest. Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.

> [!NOTE]
> Plan odzyskiwania można utworzyć aplikacji w portalu Azure.
>
>

toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
1. Uruchom hello poniżej poleceń cmdlet tooget hello maszyny Wirtualnej sieci toowhich ma tootest trybu failover do maszyn wirtualnych.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Wykonaj test trybu failover maszyny wirtualnej, wykonując następujące hello:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Wykonaj test trybu failover planu odzyskiwania, wykonując następujące hello:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Realizacja planowanego trybu failover
1. Wykonaj planowany tryb failover maszyny wirtualnej, wykonując następujące hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Planowany tryb failover planu odzyskiwania należy wykonać następujący hello:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Uruchom nieplanowanego trybu failover
1. Wykonaj nieplanowany tryb failover maszyny wirtualnej, wykonując następujące hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. Wykonaj nieplanowany tryb failover planu odzyskiwania, wykonując następujące hello:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <a name=monitor></a>Monitorowanie aktywności
Witaj Użyj następującego polecenia toomonitor hello działania. Należy pamiętać, że masz toowait Between zadania hello toofinish przetwarzania.

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej](/powershell/module/azurerm.recoveryservices.backup/#recovery) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.
