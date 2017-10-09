---
title: "węzły klastra HPC Pack aaaAutoscale | Dokumentacja firmy Microsoft"
description: "Automatycznie zwiększyć lub zmniejszyć hello liczba węzłów obliczeniowych klastra HPC Pack na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Automatycznie zwiększyć lub zmniejszyć zasobów klastra HPC Pack hello na platformie Azure, zgodnie z toohello obciążenie klastra
Jeśli wdrażania platformy Azure "serii" węzłów w klastrze HPC Pack lub utworzyć klaster HPC Pack w maszynach wirtualnych platformy Azure, możesz sposób, aby automatycznie zwiększać i zmniejszać zasoby klastra hello, takie jak węzłów lub rdzeni zgodnie z hello obciążenie klastra hello. Skalowanie hello zasoby klastra w ten sposób umożliwia toouse zasobów platformy Azure wydajniej i kontrolę kosztów ich.

W tym artykule przedstawiono HPC Pack udostępnia zasoby obliczeniowe tooautoscale na dwa sposoby:

* Witaj właściwości klastra HPC Pack **AutoGrowShrink**

* Witaj **AzureAutoGrowShrink.ps1** skryptu środowiska PowerShell klastra HPC

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Obecnie tylko automatycznie można zwiększyć lub zmniejszyć węzły obliczeniowe HPC Pack uruchomionych w systemie operacyjnym Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Ustaw właściwość klastra AutoGrowShrink hello
### <a name="prerequisites"></a>Wymagania wstępne

* **HPC Pack 2012 R2 Update 2 lub nowszym klastra** -hello węzła głównego klastra może być wdrożona lokalnie lub w maszynie Wirtualnej platformy Azure. Zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget pracę z węzłem głównym lokalnymi i węzły platformy Azure "serii". Zobacz hello [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly wdrożenie klastra HPC Pack w maszynach wirtualnych platformy Azure.

* **W przypadku klastra z węzła głównego na platformie Azure (modelu wdrażania usługi Resource Manager)** — począwszy od HPC Pack 2016 certyfikatów uwierzytelniania w aplikacji usługi Azure Active Directory służy do automatycznie powiększania i zmniejszanie rozmiaru klastra maszyny wirtualne wdrażane za pomocą Usługa Azure Resource Manager. Konfigurowanie certyfikatu w następujący sposób:

  1. Po wdrożeniu klastra łączyć węzła głównego tooone pulpitu zdalnego.

  2. Przekaż hello węzła głównego tooeach certyfikatu (format PFX z kluczem prywatnym) i zainstaluj tooCert:\LocalMachine\My i Cert: \LocalMachine\Root.

  3. Uruchom program Azure PowerShell jako administrator i uruchom następujące polecenia w jednym węźle głównym hello:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Jeśli konto użytkownika należy do więcej niż jednej dzierżawy usługi Azure Active Directory lub subskrypcji platformy Azure, można uruchomić następujące hello polecenia tooselect hello poprawne dzierżawy i subskrypcji:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Uruchom następujące polecenie tooview hello hello aktualnie wybrane dzierżawy i subskrypcji:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Uruchom hello następującego skryptu

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    gdzie

    **Nazwa wyświetlana** — Nazwa wyświetlana Azure aktywnej aplikacji. Jeśli aplikacja hello nie istnieje, jest tworzony w usłudze Azure Active Directory.

    **Strona główna** — strona główna hello aplikacji hello. Można skonfigurować zastępczego adresu URL, tak jak hello poprzedzających przykład.

    **IdentifierUri** — identyfikator aplikacji hello. Można skonfigurować zastępczego adresu URL, tak jak hello poprzedzających przykład.

    **CertificateThumbprint** — odcisk palca certyfikatu hello zainstalowany na powitania węzła głównego w kroku 1.

    **TenantId** -Identyfikatorem usługi Azure Active Directory dzierżawy. Hello identyfikator dzierżawcy można pobrać z portalu usługi Azure Active Directory hello **właściwości** strony.

    Aby uzyskać więcej informacji o **ConfigARMAutoGrowShrinkCert.ps1**Uruchom `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **W przypadku klastra z węzła głównego na platformie Azure (klasycznego modelu wdrażania)** — Jeśli używasz hello HPC Pack IaaS wdrożenia skryptu toocreate hello klastra hello klasycznego modelu wdrażania, Włącz hello **AutoGrowShrink** klastra Właściwość przez ustawienie opcji AutoGrowShrink hello w pliku konfiguracyjnym hello klastra. Aby uzyskać więcej informacji, zobacz dokumentację hello, towarzyszące hello [pobieranie skryptu](https://www.microsoft.com/download/details.aspx?id=44949).

    Można również włączyć hello **AutoGrowShrink** właściwości klastra po wdrożeniu klastra hello przy użyciu środowiska PowerShell klastra HPC polecenia opisane w następujących sekcji hello. tooprepare tego, pierwszy hello pełną następujące kroki:

  1. Skonfiguruj certyfikat zarządzania platformy Azure na powitania węzła głównego i w hello subskrypcji platformy Azure. W przypadku testowego wdrożenia można użyć hello domyślne Microsoft HPC Azure certyfikatu z podpisem własnym instalujący na powitania węzłem głównym HPC Pack a następnie przekaż tooyour tego certyfikatu subskrypcji platformy Azure. Dla opcji i procedury, zobacz hello [wskazówki w bibliotece TechNet](https://technet.microsoft.com/library/gg481759.aspx).

  2. Uruchom **regedit** na powitania węzła głównego, przejdź tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo i Dodaj wartość ciągu. Ustaw nazwę wartości hello zbyt "Odcisk palca" i wartości danych toohello odcisk palca certyfikatu hello w kroku 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Właściwość AutoGrowShrink hello tooset polecenia środowiska PowerShell klastra HPC
Poniżej przedstawiono tooset polecenia środowiska PowerShell klastra HPC próbki **AutoGrowShrink** i tootune jego zachowanie w przypadku dodatkowych parametrów. Zobacz [parametry AutoGrowShrink](#AutoGrowShrink-parameters) dalszej części tego artykułu hello pełną listę ustawień.

toorun tych poleceń, uruchom program HPC PowerShell na powitania węzła głównego klastra jako administrator.

**Witaj tooenable AutoGrowShrink właściwości**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**Witaj toodisable AutoGrowShrink właściwości**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**Witaj toochange Zwiększ interwał w minutach**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**Witaj toochange Zmniejszanie interwału w minutach**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**tooview hello bieżącej konfiguracji AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**tooexclude węzeł grupy z AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Ten parametr jest obsługiwane począwszy od HPC Pack 2016
>

### <a name="autogrowshrink-parameters"></a>Parametry AutoGrowShrink
Witaj poniżej przedstawiono AutoGrowShrink parametry, które można modyfikować za pomocą hello **HpcClusterProperty zestaw** polecenia.

* **EnableGrowShrink** — przełącznik tooenable lub wyłącz hello **AutoGrowShrink** właściwości.
* **ParamSweepTasksPerCore** — liczba parametrów zadania toogrow jednego rdzenia. Domyślnie Hello jest toogrow jednego rdzenia poszczególnych zadań.

  > [!NOTE]
  > Zmiany HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** za**TasksPerResourceUnit**. Jest oparty na typie zasobów zadania hello, a węzeł, gniazda lub core.
  >
  >
* **GrowThreshold** — próg umieszczonych w kolejce zadań tootrigger automatycznego przyrostu. Witaj domyślna to 1, co oznacza, że jeśli istnieją 1 lub więcej zadań w hello stanu umieszczonych w kolejce, automatycznie rozszerzaj węzłów.
* **GrowInterval** — interwał w minutach tootrigger automatycznego przyrostu. Witaj domyślny interwał wynosi 5 minut.
* **ShrinkInterval** — interwał w minutach tootrigger automatyczne zmniejszanie. Witaj domyślny interwał wynosi 5 minut. |
* **ShrinkIdleTimes** — liczba węzłów hello tooindicate tooshrink ciągłego kontroli są w stanie bezczynności. Witaj domyślna to 3 razy. Na przykład, jeśli hello **ShrinkInterval** wynosi 5 minut, HPC Pack sprawdza, czy węzeł hello jest w stanie bezczynności co 5 minut. Jeśli węzły hello są w stanie bezczynności hello po 3 ciągłego sprawdza (15 minut), HPC Pack zmniejsza tego węzła.
* **ExtraNodesGrowRatio** -procent dodatkowe węzły toogrow zadań komunikat interfejsu (Passing Interface). Witaj, wartość domyślna to 1, co oznacza, że HPC Pack rozwoju węzłów % 1 dla zadań MPI.
* **GrowByMin** -przełącznika tooindicate, czy zasady automatycznego przyrostu hello opiera się na powitania zasobów minimalne wymagane hello zadania. Domyślna Hello to false, co oznacza, że HPC Pack rozwoju węzłów zadań na podstawie zasobów maksymalną hello wymagane hello zadań.
* **SoaJobGrowThreshold** — próg przychodzące SOA żądań tootrigger hello automatycznego wzrostu procesu. Wartość domyślna Hello jest 50000.

  > [!NOTE]
  > Ten parametr jest obsługiwana, począwszy od HPC Pack 2012 R2 Update 3.
  >
  >
* **SoaRequestsPerCore** — liczba SOA przychodzących żądań toogrow jednego rdzenia. Wartość domyślna Hello jest 20000.

  > [!NOTE]
  > Ten parametr jest obsługiwana, począwszy od HPC Pack 2012 R2 Update 3.
  >
* **ExcludeNodeGroups** — węzły w hello określone grupy węzła automatycznie zwiększyć lub zmniejszyć.
  
  > [!NOTE]
  > Ten parametr jest obsługiwana, począwszy od HPC Pack 2016.
  >

### <a name="mpi-example"></a>Przykład MPI
Domyślnie HPC Pack rozwoju 1% dodatkowe węzły zadań MPI (**ExtraNodesGrowRatio** ustawiono too1). Przyczyna Hello jest MPI może wymagać wielu węzłów, czy hello zadanie można uruchomić tylko po zakończeniu wszystkich węzłów. Po uruchomieniu węzłów Azure czasami jeden węzeł może być konieczne więcej czasu toostart niż inne, powodując inne węzły toobe bezczynności podczas oczekiwania na tym tooget węzła gotowe. Powiększając dodatkowe węzły, HPC Pack skraca czas oczekiwania tego zasobu i potencjalnie zapisuje kosztów. Procent hello tooincrease dodatkowe węzły zadań MPI (na przykład too10%), uruchom polecenie podobne do

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Przykład SOA
Domyślnie **SoaJobGrowThreshold** ustawiono too50000 i **SoaRequestsPerCore** ustawiono too200000. Jeśli prześlesz jedno zadanie SOA z żądaniami 70000 istnieje jedno zadanie w kolejce i żądania przychodzące są 70000. W takim przypadku HPC Pack rozwoju 1 rdzeń hello w kolejce zadań i żądań przychodzących, rozwoju (70000 50000) / podstawowe 20000 = 1, dlatego w łącznie rozwoju 2 rdzeni dla tego zadania SOA.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Uruchom skrypt AzureAutoGrowShrink.ps1 hello
### <a name="prerequisites"></a>Wymagania wstępne

* **HPC Pack 2012 R2 Update 1 lub nowszym klastra** — Witaj **AzureAutoGrowShrink.ps1** skryptów jest zainstalowany w hello % CCP_HOME % bin folder. Witaj węzła głównego klastra może być wdrożona lokalnie lub w maszynie Wirtualnej platformy Azure. Zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget pracę z węzłem głównym lokalnymi i węzły platformy Azure "serii". Zobacz hello [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly wdrożenie klastra HPC Pack w maszynach wirtualnych platformy Azure lub użyj [szablonie Szybki Start Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Program Azure PowerShell 1.4.0** -skryptu hello zależy od obecnie tę konkretną wersję programu Azure PowerShell.
* **Dla klastra przy użyciu platformy Azure serii węzłów** — Uruchom skrypt hello na komputerze klienckim, na których zainstalowano pakiet HPC lub na powitania węzła głównego. Jeśli uruchomiona na komputerze klienckim, upewnij się, ustaw hello zmiennej $env: węzła głównego toohello toopoint CCP_SCHEDULER. musi zostać dodany Hello Azure "serii" węzłów klastra toohello, ale hello stan wdrożonych nie mogą być.
* **Dla klastra wdrożone w maszynach wirtualnych platformy Azure (modelu wdrażania usługi Resource Manager)** -klastra z maszyn wirtualnych Azure wdrożone w modelu wdrażania usługi Resource Manager hello skrypt hello obsługuje dwie metody uwierzytelniania systemu Azure: Zaloguj tooyour konto platformy Azure skrypt hello toorun zawsze (uruchamiając `Login-AzureRmAccount`, lub skonfigurować tooauthenticate główna usługi przy użyciu certyfikatu. HPC Pack zawiera skrypt hello **ConfigARMAutoGrowShrinkCert.ps** toocreate nazwy głównej usługi o certyfikat. Witaj skrypt tworzy aplikację usługi Azure Active Directory (Azure AD) i nazwy głównej usługi i przypisuje nazwy głównej usługi toohello roli współautora hello. skrypt hello toorun, uruchom program Azure PowerShell jako administrator i uruchom następujące polecenia hello:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Aby uzyskać więcej informacji o **ConfigARMAutoGrowShrinkCert.ps1**Uruchom `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,

* **Dla klastra wdrożone w maszynach wirtualnych platformy Azure (klasycznego modelu wdrażania)** — Uruchom skrypt hello na powitania węzła głównego maszyny Wirtualnej, ponieważ zależy on od hello **Start HpcIaaSNode.ps1** i **Stop-HpcIaaSNode.ps1**skrypty, które są zainstalowane na. Ponadto te skrypty wymagają certyfikatu zarządzania platformy Azure lub plik ustawień publikowania (zobacz [Zarządzaj węzłów obliczeniowych w HPC Pack klastra w systemie Azure](hpcpack-cluster-node-manage.md)). Upewnij się, wszystkie hello obliczeniowe węzła maszyny wirtualne, konieczne są już dodane toohello klastra. Mogą być hello zatrzymana.



### <a name="syntax"></a>Składnia
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>Parametry
* **NodeTemplates** -nazwy hello węzeł Szablony toodefine hello zakres hello toogrow węzłów i zmniejszyć. Jeśli nie zostanie określony (hello wartość domyślna to @()), wszystkie węzły w hello **AzureNodes** węzła grupy są w zakres podczas **NodeType** ma wartość AzureNodes, a wszystkie węzły w hello **ComputeNodes** węzła grupy są w przypadku zakres **NodeType** ma wartość ComputeNodes.
* **JobTemplates** -nazwy hello zadania szablonów toodefine hello zakres hello toogrow węzłów.
* **Typ NodeType** — Witaj typu węzła toogrow i zmniejszyć. Obsługiwane są następujące wartości:

  * **AzureNodes** — w przypadku Azure PaaS (serii) węzły w lokalnej lub w klastrze IaaS platformy Azure.
  * **ComputeNodes** — dla węzła obliczeniowego maszyn wirtualnych tylko w klastrze IaaS platformy Azure.

* **NumOfQueuedJobsPerNodeToGrow** -liczbę zadań umieszczonych w kolejce wymagane toogrow jeden węzeł.
* **NumOfQueuedJobsToGrowThreshold** -hello próg liczbę zadań umieszczonych w kolejce toostart hello wzrostu procesu.
* **NumOfActiveQueuedTasksPerNodeToGrow** -hello liczba aktywnych zadań w kolejce wymagane toogrow jeden węzeł. Jeśli **NumOfQueuedJobsPerNodeToGrow** zostanie podana wartość większą niż 0, ten parametr jest ignorowany.
* **NumOfActiveQueuedTasksToGrowThreshold** -hello Próg liczby aktywnych zadań w kolejce toostart hello wzrostu procesu.
* **NumOfInitialNodesToGrow** — Witaj początkowa minimalna liczba węzłów toogrow, jeśli wszystkie węzły hello w zakresie są **wdrożone nie** lub **zatrzymane (Deallocated)**.
* **GrowCheckIntervalMins** -hello interwał w minutach od sprawdza toogrow.
* **ShrinkCheckIntervalMins** -hello interwał w minutach od sprawdza tooshrink.
* **ShrinkCheckIdleTimes** — Witaj liczby sprawdzeń ciągłego zmniejszania (rozdzielone **ShrinkCheckIntervalMins**) tooindicate hello węzły są w stanie bezczynności.
* **UseLastConfigurations** — Witaj poprzedniej konfiguracji zapisane w pliku argumentu hello.
* **ArgFile**— Witaj nazwa toosave plik używany argument hello i hello konfiguracje toorun hello skrypt aktualizacji.
* **LogFilePrefix** -hello prefiks nazwy pliku dziennika hello. Można określić ścieżkę. Domyślnie dziennik hello jest zapisywane toohello bieżący katalog roboczy.

### <a name="example-1"></a>Przykład 1
Witaj poniższy przykład umożliwia skonfigurowanie hello Azure serii węzłów z toogrow domyślny szablon AzureNode i zmniejsza się automatycznie. Jeśli wszystkie węzły są początkowo w hello **wdrożone nie** stanu, są uruchamiane co najmniej 3 węzłach. Jeśli hello liczbę zadań umieszczonych w kolejce przekroczy 8, skrypt hello rozpoczyna węzłów aż do ich liczba przekracza stosunek hello umieszczonych w kolejce zadań do **NumOfQueuedJobsPerNodeToGrow**. Jeśli węzeł zostanie znaleziony toobe bezczynności 3 kolejne czas bezczynności, zostanie zatrzymana.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Przykład 2
Witaj poniższy przykład umożliwia skonfigurowanie hello Azure obliczeniowe węzła maszyny wirtualne wdrażane z hello domyślny szablon ComputeNode toogrow i zmniejsza się automatycznie.
zadania Hello konfigurowane za pomocą szablonu zadania domyślne hello zdefiniować zakres hello obciążenia w klastrze hello. Jeśli wszystkie węzły hello są początkowo zatrzymana, są uruchamiane co najmniej 5 węzłów. Jeśli hello liczba aktywnych zadań w kolejce przekroczy 15, skrypt hello rozpoczyna węzłów aż do ich liczba przekracza hello stosunek aktywne zadania w kolejce za**NumOfActiveQueuedTasksPerNodeToGrow**. Jeśli węzeł zostanie znaleziony toobe bezczynności 10 kolejnych czas bezczynności, zostanie zatrzymana.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
