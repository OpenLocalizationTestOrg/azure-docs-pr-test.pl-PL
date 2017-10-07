---
title: "maszyny wirtualne aaaReplicate funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Azure Site Recovery i środowiska PowerShell (Resource Manager) | Dokumentacja firmy Microsoft"
description: "Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Azure Site Recovery i programu PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu programu PowerShell i usługi Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Klasyczny portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell — model klasyczny](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Omówienie
Usługa Azure Site Recovery przyczynia się tooyour ciągłości i odzyskiwaniem po awarii (BCDR) odzyskiwania strategii biznesowej poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania. Pełną listę wdrażania scenariuszy dla hello [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).

W tym artykule opisano, jak toouse PowerShell tooautomate typowych zadań należy tooperform podczas konfigurowania maszyny wirtualne funkcji Hyper-V tooreplicate usługi Azure Site Recovery w magazynie tooAzure chmur programu System Center VMM.

Hello artykuł zawiera wymagania wstępne dla scenariusza hello i pokazuje

* Jak tooset się magazynu usług odzyskiwania
* Zainstaluj hello dostawcy usługi Azure Site Recovery na źródłowym serwerze programu VMM hello
* Zarejestruj serwer hello w magazynie hello, Dodaj konto magazynu platformy Azure
* Zainstaluj agenta usług odzyskiwania Azure hello na serwerach hostów funkcji Hyper-V
* Skonfiguruj ustawienia ochrony chmury VMM, które mają być zastosowane tooall chronione maszyny wirtualne
* Włącz ochronę tych maszyn wirtualnych.
* Przetestuj hello awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.

Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello.
>
>

## <a name="before-you-start"></a>Przed rozpoczęciem
Upewnij się, że te wymagania wstępne zostały spełnione:

### <a name="azure-prerequisites"></a>Wymagania wstępne platformy Azure
* Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/). Jeśli nie masz, Rozpocznij od [bezpłatne konto](https://azure.microsoft.com/free). Ponadto możesz przeczytać temat hello [cennik usługi Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Będziesz potrzebować subskrypcji dostawcy usług Kryptograficznych, jeśli próbujesz się hello replikacji tooa dostawcy usług Kryptograficznych subskrypcji scenariusza. Dowiedz się więcej o programie dostawcy usług Kryptograficznych hello w [jak tooenroll w programie dostawcy usług Kryptograficznych hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Będziesz potrzebować tooAzure danych replikowanych toostore konta platformy Azure w wersji 2 magazynu (Resource Manager). Konto Hello musi włączyć replikację geograficzną. Należy go w hello na tym samym regionie co hello usługi Azure Site Recovery i musi być skojarzone z hello tej samej subskrypcji lub hello dostawcy usług Kryptograficznych subskrypcji. toolearn więcej informacji na temat konfigurowania magazynu Azure, zobacz hello [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md) odwołania.
* Należy się upewnić, że maszyny wirtualne mają tooprotect spełniają hello toomake [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Obecnie tylko operacje poziomu maszyny Wirtualnej jest możliwe za pośrednictwem programu Powershell. Obsługa operacji poziomu planu odzyskiwania zostaną wprowadzone wkrótce.  Obecnie masz ograniczone tooperforming przełączanie w trybie Failover tylko na poziom szczegółowości "chronione maszyny Wirtualnej", a nie na poziomie planu odzyskiwania.
>
>

### <a name="vmm-prerequisites"></a>Wymagania wstępne programu VMM
* Należy na serwerze programu VMM działa na System Center 2012 R2.
* Żadnym serwerze VMM obejmującego maszyny wirtualne mają tooprotect musi być uruchomiona hello dostawcy usługi Azure Site Recovery. To jest instalowany podczas wdrażania usługi Azure Site Recovery hello.
* Będziesz potrzebować co najmniej jedna chmura na powitania serwera VMM ma tooprotect. Chmura Hello powinna zawierać:
  * Co najmniej jedną grupę hostów programu VMM.
  * Co najmniej jeden serwer hosta lub klaster funkcji Hyper-V w każdej grupie hostów.
  * Co najmniej jednej maszyny wirtualnej na powitania serwera źródłowego funkcji Hyper-V.
* Dowiedz się więcej o konfigurowaniu chmur VMM:
  * Dowiedz się więcej o prywatnych chmur programu VMM [What's New in chmury prywatnej z programu System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) i [chmur VMM 2012 i hello](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Dowiedz się więcej o [sieci szkieletowej chmury hello Konfigurowanie programu VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Po elementów sieci szkieletowej chmury w miejscu więcej informacji o tworzeniu chmur prywatnych w [tworzenia chmury prywatnej w programie VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) i [wskazówki: tworzenie chmur prywatnych z programu System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Wymagania wstępne funkcji Hyper-V
* Witaj Serwery hosta funkcji Hyper-V musi działać co najmniej **systemu Windows Server 2012** z rolą funkcji Hyper-V lub **Microsoft Hyper-V Server 2012** i mieć hello zainstalowane najnowsze aktualizacje.
* Jeśli używasz funkcji Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie, jeśli masz klaster oparty na statycznym adresie IP. Będziesz potrzebować brokera klastra hello tooconfigure ręcznie. dla
* Instrukcje można znaleźć [jak tooConfigure brokera funkcji Hyper-V Replica](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Dowolnego serwera hosta funkcji Hyper-V lub klaster, dla którego ma zostać toomanage ochrony musi być uwzględniona w chmurze VMM.

### <a name="network-mapping-prerequisites"></a>Wymagania wstępne związane z mapowaniem sieci
W przypadku ochrony maszyn wirtualnych na platformie Azure, mapowanie sieci hello mapuje hello sieci maszyn wirtualnych na źródłowym serwerze programu VMM hello i docelowej sieci platformy Azure tooenable hello poniżej:

* Wszystkie komputery, które w tryb failover na powitania sam połączyć tooeach innych, niezależnie od tego, jakiego planu odzyskiwania, które znajdują się w sieci.
* Jeśli brama sieci została skonfigurowana w hello docelową sieć platformy Azure, maszyny wirtualne można łączyć z tooother lokalnych maszyn wirtualnych.
* Jeśli nie skonfigurujesz mapowania sieci tylko hello maszyn wirtualnych, które w tryb failover w hello sam plan odzyskiwania będą mogli tooconnect tooeach innych po tooAzure awaryjnej.

Jeśli chcesz, aby mapowanie sieci toodeploy potrzebne są następujące hello:

* maszyny wirtualne Hello ma tooprotect na źródłowym serwerze programu VMM hello powinna być tooa połączonych sieci maszyny Wirtualnej. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.
* Maszyny wirtualne replikowane toowhich sieć platformy Azure mogą łączyć po awaryjnym. Należy wybrać tej sieci w czasie hello awaryjnym. Witaj sieć powinna znajdować się w hello tym samym regionie co subskrypcja usługi Azure Site Recovery.

Dowiedz się więcej o mapowanie sieci w

* [Jak tooconfigure sieci logicznych w programie VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Jak tooconfigure maszyny Wirtualnej sieci i bram w programie VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Jak tooconfigure i monitor sieci wirtualne na platformie Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

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
1. Utwórz grupę zasobów usługi Azure Resource Manager, jeśli nie masz już

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Utwórz nowy magazyn usług odzyskiwania i zapisać hello utworzony obiekt magazynu ASR w zmiennej (zostanie później użyty). Można również pobierać hello ASR magazynu obiektu post tworzenia przy użyciu polecenia cmdlet Get-AzureRMRecoveryServicesVault hello:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Krok 3: Ustaw hello kontekst magazynu usług odzyskiwania

Ustaw kontekst magazynu hello uruchamiając hello poniżej polecenia.

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

## <a name="step-5-create-an-azure-storage-account"></a>Krok 5: Tworzenie konta magazynu platformy Azure

Jeśli nie masz konta magazynu platformy Azure, Utwórz konto włączono replikację geograficzną w hello tej samej lokalizacji geograficznej co hello magazynu, uruchamiając następujące polecenie hello:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Należy pamiętać, że konto magazynu hello musi być w tym samym regionie co usługa Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Krok 6: Hello instalacji agenta usług odzyskiwania Azure
1. Pobierz agenta usług odzyskiwania Azure hello na [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) i zainstaluj go na każdym serwerze hosta funkcji Hyper-V znajdujące się w hello VMM możesz chmur mają tooprotect.
2. Uruchom następujące polecenie na wszystkich hostach VMM hello:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Krok 7: Konfigurowanie chmury ustawienia ochrony
1. Utwórz tooAzure zasady replikacji, uruchamiając następujące polecenie hello:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Pobierz kontenera ochrony, uruchamiając następujące polecenia hello:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Pobierz hello zasad szczegóły tooa zmienną przy użyciu zadania hello, który został utworzony i podając hello zasad przyjazną nazwę:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Uruchom skojarzenie hello kontenera ochrony hello z zasadami replikacji hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Po zakończeniu zadania hello, uruchom następujące polecenie hello:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Po zakończeniu przetwarzania zadania hello, uruchom następujące polecenie hello:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).

## <a name="step-8-configure-network-mapping"></a>Krok 8: Konfigurowanie mapowania sieci
Przed rozpoczęciem mapowania sieci Sprawdź, czy maszyny wirtualne na źródłowym serwerze programu VMM hello są połączone tooa sieci maszyny Wirtualnej. Ponadto należy utworzyć jeden lub więcej sieci wirtualnych platformy Azure.

Dowiedz się więcej na temat sposobu toocreate a wirtualnych sieci, za pomocą usługi Azure Resource Manager i programu PowerShell, w [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą usługi Azure Resource Manager i programu PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Należy zauważyć, że wiele sieci maszyn wirtualnych mogą być mapowane tooa pojedynczej sieci platformy Azure. Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po awaryjnym. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.

1. Witaj pierwsze polecenie pobiera serwerów hello bieżący magazyn Azure Site Recovery. polecenie Hello przechowuje hello serwerów Microsoft Azure Site Recovery w hello $Servers tablicy zmiennej.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hello drugie polecenie pobiera hello sieci odzyskiwania lokacji dla pierwszego serwera hello hello $Servers tablicy. polecenie Hello przechowuje hello sieci w zmiennej hello $Networks.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. trzecie polecenie Hello pobiera sieci wirtualnych platformy Azure, a następnie tę wartość w zmiennej hello $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. polecenie cmdlet końcowego Hello tworzy mapowanie między hello sieci podstawowej i hello sieci maszyny wirtualnej platformy Azure. polecenia cmdlet Hello określa hello sieci podstawowej jako pierwszy element $Networks hello. polecenia cmdlet Hello określa sieć maszyny wirtualnej jako pierwszy element $AzureVmNetworks hello.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Krok 9: Włączanie ochrony dla maszyn wirtualnych
Po hello serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello.

 Należy uwzględnić następujące hello:

* Maszyny wirtualne muszą spełniać wymagania dotyczące usługi Azure. Sprawdź je w [warunki wstępne i pomocy technicznej](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) w przewodniku planowania hello.
* dla maszyny wirtualnej hello musi być ustawiona ochrona tooenable, hello systemu operacyjnego i właściwości dysku systemu operacyjnego. Podczas tworzenia maszyny wirtualnej w programie VMM przy użyciu szablonu maszyny wirtualnej można ustawić właściwości hello. Można również ustawić te właściwości dla istniejących maszyn wirtualnych na powitania **ogólne** i **konfiguracja sprzętu** karty hello właściwości maszyny wirtualnej. Jeśli nie ustawisz tych właściwości w programie VMM będziesz w stanie tooconfigure je w portalu usługi Azure Site Recovery hello.

1. Ochrona tooenable hello uruchom następujące polecenia kontenera ochrony hello tooget:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Pobierz jednostki ochrony hello (VM), uruchamiając następujące polecenie hello:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Włącz hello DR dla maszyny Wirtualnej hello, uruchamiając następujące polecenie hello:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Testowanie wdrożenia
tootest wdrożenia można uruchomić testu Failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania uwzględniający wiele maszyn wirtualnych i uruchom test awaryjnej hello planu. Awaryjnej testu symuluje z mechanizmu awaryjnej i odzyskiwania w sieci izolowanej. Należy pamiętać, że:

* Tooconnect toohello maszyny wirtualnej platformy Azure przy użyciu pulpitu zdalnego po awaryjnym hello, należy włączyć połączenia pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover.
* Po miała użyjesz publicznego adresu IP address tooconnect toohello maszynę wirtualną na platformie Azure przy użyciu pulpitu zdalnego. Jeśli chcesz toodo to, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają łączącego tooa maszyny wirtualnej przy użyciu adresu publicznego.

toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
- Uruchom hello testowy tryb failover, uruchamiając następujące polecenie hello:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Realizacja planowanego trybu failover
- Uruchom hello planowanego trybu failover, uruchamiając następujące polecenie hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Uruchom nieplanowanego trybu failover
- Uruchom hello nieplanowanego trybu failover, uruchamiając następujące polecenie hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
