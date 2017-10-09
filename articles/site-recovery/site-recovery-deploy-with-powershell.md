---
title: "aaaReplicate tooAzure maszyn wirtualnych funkcji Hyper-V w portalu klasycznym hello przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Automatyzowanie replikacji hello maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Site Recovery i programu PowerShell w portalu klasycznym hello"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V tooAzure przy użyciu programu PowerShell w portalu klasycznym hello
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

Hello artykuł zawiera wymagania wstępne dotyczące hello scenariusza i przedstawia sposób instalacji tooset się w magazynie usługi Site Recovery hello dostawcy usługi Azure Site Recovery na źródłowym serwerze programu VMM hello, Zarejestruj serwer hello w magazynie hello, Dodaj konto magazynu platformy Azure, zainstaluj hello Azure Agent usług odzyskiwania na serwerach hostów funkcji Hyper-V, skonfigurować ustawienia ochrony dla chmur programu VMM, które będzie zastosowane tooall chronionych maszyn wirtualnych, a następnie włącz ochronę tych maszyn wirtualnych. Aby zakończyć, testowania hello trybu failover toomake się, że wszystko działa zgodnie z oczekiwaniami.

Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.
>
>

## <a name="before-you-start"></a>Przed rozpoczęciem
Upewnij się, że te wymagania wstępne zostały spełnione:

### <a name="azure-prerequisites"></a>Wymagania wstępne platformy Azure
* Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Będziesz potrzebować toostore replikowane dane konta magazynu platformy Azure. Konto Hello musi włączyć replikację geograficzną. Należy go w tym samym regionie co magazyn usługi Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji. [Dowiedz się więcej na temat usługi Azure storage](../storage/common/storage-introduction.md).
* Należy się upewnić, że maszyny wirtualne mają tooprotect są zgodne z toomake [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>Wymagania wstępne programu VMM
* Należy na serwerze programu VMM działa na System Center 2012 R2.
* Będziesz potrzebować co najmniej jedna chmura na powitania serwera VMM ma tooprotect. Chmura Hello powinna zawierać:
  * Co najmniej jedną grupę hostów programu VMM.
  * Serwery hosta funkcji Hyper-V lub klastry w każdej grupie hostów.
  * Co najmniej jednej maszyny wirtualnej na powitania serwera źródłowego funkcji Hyper-V.

### <a name="hyper-v-prerequisites"></a>Wymagania wstępne funkcji Hyper-V
* Witaj Serwery hosta funkcji Hyper-V musi działać co najmniej **systemu Windows Server 2012** z rolą funkcji Hyper-V lub **Microsoft Hyper-V Server 2012** i mieć hello zainstalowane najnowsze aktualizacje.
* Jeśli używasz funkcji Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie, jeśli masz klaster oparty na statycznym adresie IP. Będziesz potrzebować brokera klastra hello tooconfigure ręcznie. toodo to w Menedżerze serwera > Menedżera klastra trybu Failover, kliknij pozycję Połącz klaster toohello **Konfiguruj rolę** i wybierz **brokera funkcji Hyper-V Replica** w hello **wybierz rolę**ekranie powitania Kreatora wysokiej dostępności.
* Dowolnego serwera hosta funkcji Hyper-V lub klaster, dla którego ma zostać toomanage ochrony musi być uwzględniona w chmurze VMM.

### <a name="network-mapping-prerequisites"></a>Wymagania wstępne związane z mapowaniem sieci
Podczas ochrony maszyn wirtualnych w sieci Azure mapowania mapuje między sieciami maszyn wirtualnych na źródłowym serwerze programu VMM hello a docelowej sieci platformy Azure tooenable hello następujące:

* Wszystkie komputery, które w tryb failover na powitania sam połączyć tooeach innych, niezależnie od tego, jakiego planu odzyskiwania, które znajdują się w sieci.
* Jeśli brama sieci została skonfigurowana w hello docelową sieć platformy Azure, maszyny wirtualne można łączyć z tooother lokalnych maszyn wirtualnych.
* Jeśli nie skonfigurujesz sieci mapowania tylko maszyny wirtualne, które awaryjnie w hello sam plan odzyskiwania będą mogli tooconnect tooeach innych po tooAzure pracy awaryjnej.

Jeśli chcesz, aby mapowanie sieci toodeploy potrzebne są następujące hello:

* maszyny wirtualne Hello ma tooprotect na źródłowym serwerze programu VMM hello powinna być tooa połączonych sieci maszyny Wirtualnej. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.
* Maszyny wirtualne replikowane toowhich sieć platformy Azure mogą łączyć po pracy awaryjnej. Należy wybrać tej sieci w czasie hello pracy awaryjnej. Witaj sieć powinna znajdować się w hello tym samym regionie co subskrypcja usługi Azure Site Recovery.

### <a name="powershell-prerequisites"></a>Wymagania wstępne programu PowerShell
Upewnij się, że masz toogo gotowy programu Azure PowerShell. Jeśli korzystasz już z programu PowerShell, potrzebujesz tooupgrade tooversion 0.8.10 lub nowszym. Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs). Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet hello hello usługi [tutaj](/powershell/azure/overview).

toolearn o porad ułatwiających przy użyciu poleceń cmdlet hello, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz [wprowadzenie do poleceń cmdlet Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Krok 1: Ustaw hello subskrypcji
W programie PowerShell Uruchom te polecenia cmdlet:

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Zastąp hello elementów w obrębie hello "< >" konkretnych informacji.

## <a name="step-2-create-a-site-recovery-vault"></a>Krok 2: Tworzenie magazynu usługi Site Recovery
W programie PowerShell Zamień hello elementów w obrębie hello "< >" konkretnych informacji i uruchom następujące polecenia:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Krok 3: Generowanie klucza rejestracji magazynu
Wygeneruj klucz rejestracji w magazynie hello. Po pobraniu hello dostawcy usługi Azure Site Recovery i zainstaluj go na serwerze VMM hello, użyjesz tego serwera VMM hello tooregister kluczy w magazynie hello.

1. Pobierz plik ustawienia magazynu hello i Ustaw kontekst hello:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Ustaw kontekst magazynu hello, uruchamiając następujące polecenia hello:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Krok 4: Instalowanie hello dostawcy usługi Azure Site Recovery
1. Na maszynie VMM hello należy utworzyć katalog, uruchamiając następujące polecenie hello:

   ```

   pushd C:\ASR\

   ```
2. Wyodrębnij pliki hello przy użyciu dostawcy hello pobrane, uruchamiając następujące polecenie hello

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Zainstaluj dostawcę hello przy użyciu hello następującego polecenia:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Poczekaj na powitania toofinish instalacji.
4. Zarejestruj serwer hello w magazynie hello przy użyciu hello następujące polecenie:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Krok 5: Tworzenie konta magazynu platformy Azure
Jeśli nie masz konta magazynu platformy Azure, Utwórz konto z włączoną replikacją geograficzną, uruchamiając następujące polecenie hello:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Należy pamiętać, że konto magazynu hello musi być w tym samym regionie co usługa Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Krok 6: Hello instalacji agenta usług odzyskiwania Azure
Z hello portalu Azure, zainstaluj agenta usług odzyskiwania Azure hello na każdym serwerze hosta funkcji Hyper-V znajdujących się w chmurach VMM hello mają tooprotect.

Uruchom następujące polecenie na wszystkich hostach VMM hello:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Krok 7: Konfigurowanie chmury ustawienia ochrony
1. Utwórz tooAzure profilu ochrony chmury, uruchamiając następujące polecenie hello:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Pobierz kontenera ochrony, uruchamiając następujące polecenia hello:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Uruchom skojarzenie hello hello kontenera ochrony z chmurą hello:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Po zakończeniu zadania hello, uruchom następujące polecenie hello:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Po zakończeniu przetwarzania zadania hello, uruchom następujące polecenie hello:

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



toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).

## <a name="step-8-configure-network-mapping"></a>Krok 8: Konfigurowanie mapowania sieci
Przed rozpoczęciem mapowania sieci Sprawdź, czy maszyny wirtualne na źródłowym serwerze programu VMM hello są połączone tooa sieci maszyny Wirtualnej. Ponadto należy utworzyć jeden lub więcej sieci wirtualnych platformy Azure. Należy zauważyć, że wiele sieci maszyn wirtualnych mogą być mapowane tooa pojedynczej sieci platformy Azure.

Należy pamiętać, że jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie istnieje docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.

Witaj pierwsze polecenie pobiera serwerów hello bieżący magazyn Azure Site Recovery. polecenie Hello przechowuje hello serwerów Microsoft Azure Site Recovery w hello $Servers tablicy zmiennej.

    $Servers = Get-AzureSiteRecoveryServer


Hello drugie polecenie pobiera hello sieci odzyskiwania lokacji dla pierwszego serwera hello hello $Servers tablicy. polecenie Hello przechowuje hello sieci w zmiennej hello $Networks.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

trzecie polecenie Hello pobiera subskrypcji platformy Azure za pomocą polecenia cmdlet Get-AzureSubscription hello, a następnie zapisanie tej wartości w zmiennej hello $Subscriptions.

    $Subscriptions = Get-AzureSubscription



polecenie czwarty Hello pobiera sieci wirtualnych platformy Azure przy użyciu polecenia cmdlet Get-AzureVNetSite hello, a następnie tę wartość w zmiennej hello $AzureVmNetworks.

    $AzureVmNetworks = Get-AzureVNetSite



polecenie cmdlet końcowego Hello tworzy mapowanie między hello sieci podstawowej i hello sieci maszyny wirtualnej platformy Azure. polecenia cmdlet Hello określa hello sieci podstawowej jako pierwszy element $Networks hello. polecenia cmdlet Hello określa sieć maszyny wirtualnej jako pierwszy element $AzureVmNetworks hello za pomocą jego identyfikatora. polecenie Hello zawiera swój identyfikator subskrypcji platformy Azure.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Krok 9: Włączanie ochrony dla maszyn wirtualnych
Po serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello. Należy uwzględnić następujące hello:

Maszyny wirtualne muszą spełniać [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

dla maszyny wirtualnej hello musi być ustawiona systemu operacyjnego hello ochrony tooenable i właściwości dysku systemu operacyjnego. Podczas tworzenia maszyny wirtualnej w programie VMM przy użyciu szablonu maszyny wirtualnej można ustawić właściwości hello. Można również ustawić te właściwości dla istniejących maszyn wirtualnych na powitania **ogólne** i **konfiguracja sprzętu** karty hello właściwości maszyny wirtualnej. Jeśli nie ustawisz tych właściwości w programie VMM będziesz w stanie tooconfigure je w portalu usługi Azure Site Recovery hello.

1. Ochrona tooenable hello uruchom następujące polecenia kontenera ochrony hello tooget:

     $ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-Name $CloudName
2. Pobierz jednostki ochrony hello (VM), uruchamiając następujące polecenie hello:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Włącz hello DR dla maszyny Wirtualnej hello, uruchamiając następujące polecenie hello:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Testowanie wdrożenia
Planowanie wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania składające się z wielu maszyn wirtualnych i uruchomić test trybu failover dla hello tootest. Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej. Należy pamiętać, że:

* Maszyna wirtualna toohello tooconnect na platformie Azure przy użyciu pulpitu zdalnego po hello w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover.
* Po przejściu w tryb failover użyjesz publicznego adresu IP address tooconnect toohello maszynę wirtualną na platformie Azure przy użyciu pulpitu zdalnego. Jeśli chcesz toodo to, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają łączącego tooa maszyny wirtualnej przy użyciu adresu publicznego.

toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).

### <a name="create-a-recovery-plan"></a>Tworzenie planu odzyskiwania
1. Utwórz plik .xml jako szablon dla planu odzyskiwania przy użyciu danych hello poniżej, a następnie zapisz go jako "C:\RPTemplatePath.xml".
2. Zmień węzeł RecoveryPlan hello identyfikator, nazwę PrimaryServerId i SecondaryServerId.
3. Zmień węzeł ProtectionEntity hello PrimaryProtectionEntityId (vmid z programu VMM).
4. Możesz dodać więcej maszyn wirtualnych, dodając więcej węzłów ProtectionEntity.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Wypełnij hello danych w szablonie hello:

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Utwórz hello RecoveryPlan:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
1. Pobierz obiekt RecoveryPlan hello, uruchamiając następujące polecenie hello:

     $RPObject = get-AzureSiteRecoveryRecoveryPlan-Name $RPName;
2. Uruchom hello testowy tryb failover, uruchamiając następujące polecenie hello:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


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
[Dowiedz się więcej](/powershell/azure/overview) o poleceniach cmdlet programu PowerShell systemu Azure lokacji odzyskiwania. </a>.
