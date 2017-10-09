---
title: "Witaj aaaDeploy usługi mobilności odzyskiwania lokacji z usługi Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Opisuje, jak tooautomatically Konfiguracja DSC automatyzacji Azure toouse wdrożyć usługę mobilności odzyskiwania lokacji Azure hello oraz agenta platformy Azure dla maszyny Wirtualnej VMware i tooAzure replikacji serwera fizycznego"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Wdrażanie usługi mobilności hello usłudze Konfiguracja DSC automatyzacji Azure replikacji maszyny wirtualnej
W programie Operations Management Suite możemy umożliwiają kompleksowe tworzenie kopii zapasowych i rozwiązanie odzyskiwania po awarii, których mogą używać jako część planu zapewnienia ciągłości działalności.

Ten przebieg razem z funkcją Hyper-V firma Microsoft uruchomiona przy użyciu funkcji Hyper-V Replica. Ale mamy rozwinięte toosupport heterogenicznych Instalatora ponieważ klienci mają wiele funkcji hypervisor i platform w ich chmury.

Jeśli używasz obciążeń VMware i/lub serwerów fizycznych dzisiaj, serwer zarządzania wszystkich hello składniki usługi Azure Site Recovery w Twoje środowisko toohandle hello komunikacji i danych replikacji z platformy Azure, jest uruchamiane przy Azure folderu docelowego.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Wdrażanie usługi mobilności odzyskiwania lokacji hello przy użyciu usługi Konfiguracja DSC automatyzacji
Zacznijmy wykonując szybki podział czego ten serwer zarządzania.

Serwer zarządzania Hello uruchamia kilka ról serwera. Jedną z tych ról jest *konfiguracji*, która koordynuje komunikacji i zarządza procesami replikacji i odzyskiwania danych.

Ponadto hello *procesu* roli działa jako brama replikacji. Ta rola odbiera dane replikacji z chronionych maszyn źródłowych, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła on tooan kontem magazynu platformy Azure. Jedna hello funkcji dla roli proces hello jest również instalacji toopush hello mobilności usługi tooprotected maszyn i automatyczne odnajdywanie maszyn wirtualnych VMware.

W przypadku powrotu po awarii z platformy Azure, hello *główny cel* roli będzie obsługiwać hello replikacji danych w ramach tej operacji.

Hello chronione maszyny, możemy polegać na powitania *usługi mobilności*. Ten składnik jest maszyną wdrożonej tooevery (maszyny Wirtualnej VMware lub serwerów fizycznych), które mają tooreplicate tooAzure. On przechwytywania zapisów danych na komputerze hello i przekazuje je toohello serwera zarządzania (rola w procesie).

W przypadku zajmujące ciągłość prowadzenia działalności biznesowej, jest ważne toounderstand obciążeń z infrastruktury i hello składniki zaangażowane. Można następnie spełniać wymagania hello w celu czasu odzyskiwania (RTO) i cel punktu odzyskiwania (RPO). W tym kontekście hello usługa mobilności jest tooensuring kluczy chronionych obciążeń zgodnie z regułami.

W jaki sposób, w sposób zoptymalizowane zapewnić że niezawodnej Instalatora chronionych za pomocą z niektórych składników usługi Operations Management Suite?

W tym artykule przedstawiono przykład używania żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), wraz z usługi Site Recovery tooensure który:

* agent maszyny Wirtualnej platformy Azure i usługi mobilności Hello są toohello wdrożonej maszyny z systemem Windows, które mają tooprotect.
* agent maszyny Wirtualnej platformy Azure i usługi mobilności Hello zawsze działają w przypadku Azure to hello lokalizacją docelową replikacji.

## <a name="prerequisites"></a>Wymagania wstępne
* Instalacja wymagana hello toostore repozytorium
* Witaj toostore repozytorium wymagane hasło tooregister z serwerem zarządzania hello

  > [!NOTE]
  > Unikatowe hasło jest generowane dla każdego serwera zarządzania. Jeśli ma toodeploy wiele serwerów zarządzania, należy tooensure tego hello prawidłowe hasło jest przechowywane w pliku passphrase.txt hello.
  >
  >
* Windows Management Framework (WMF) zainstalowany na komputerach hello mają tooenable ochrony (wymagania dotyczące usługi Konfiguracja DSC automatyzacji) w wersji 5.0

  > [!NOTE]
  > Jeśli chcesz toouse maszyny DSC dla systemu Windows, które mają zainstalowaną WMF 4.0, zobacz sekcję hello [DSC użytku w środowiskach rozłączonych](## Use DSC in disconnected environments).
  

usługi mobilności Hello można zainstalować za pomocą wiersza polecenia hello i przyjmuje wiele argumentów. Dlatego należy plików binarnych hello toohave (po wyodrębnianie je z ustawień) i przechowywać je w miejscu, gdzie można je odzyskać za pomocą konfiguracji DSC.

## <a name="step-1-extract-binaries"></a>Krok 1: Pliki binarne wyodrębniania
1. potrzebne dla tej instalacji, pliki hello tooextract Przeglądaj toohello następującego katalogu na serwerze zarządzania:

    **\Microsoft azure lokacji Recovery\home\svsystems\pushinstallsvc\repository**

    W tym folderze powinien zostać wyświetlony plik MSI o nazwie:

    **ASR_UA_version_Windows_GA_date_Release.exe firmy Microsoft**

    Witaj Użyj następującego polecenia tooextract hello Instalatora:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Zaznacz wszystkie pliki i wysyłać je tooa skompresowanego folderu (zip).

Masz teraz hello plików binarnych muszą tooautomate ustawienia hello hello usługi mobilności przy użyciu usługi Konfiguracja DSC automatyzacji.

### <a name="passphrase"></a>Hasło
Następnie należy toodetermine miejscu tooplace tego folderu zip. Konto magazynu platformy Azure, można użyć jako pokazano później, toostore hello hasło, które należy hello instalacji. następnie zarejestruje Hello agenta z serwerem zarządzania hello jako część procesu hello.

Witaj hasło, które uzyskano podczas wdrażania serwera zarządzania hello mogą zostać zapisane jako passphrase.txt tooa pliku tekstowego.

Umieść zarówno hello folderu zip, jak i hasło hello w dedykowanych kontenera w hello kontem magazynu platformy Azure.

![Lokalizacja folderu](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Jeśli wolisz tookeep tych plików w udziale w sieci, możesz to zrobić. Wystarczy tooensure że hello DSC zasobu, która będzie używana później ma dostęp i można uzyskać Instalator hello i hasło.

## <a name="step-2-create-hello-dsc-configuration"></a>Krok 2: Tworzenie konfiguracji hello DSC
Instalator Hello zależy od WMF 5.0. Witaj maszyny toosuccessfully zastosować hello konfiguracji za pomocą usługi Konfiguracja DSC automatyzacji, WMF 5.0 musi toobe obecny.

środowisko Hello używa powitania po Przykładowa konfiguracja DSC:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
Konfiguracja Hello będzie wykonywać następujące hello:

* zmienne Hello poinformuje hello konfiguracji, gdzie tooget hello pliki binarne usługi mobilności hello i hello agenta maszyny Wirtualnej Azure, gdzie tooget hello hasło, a dane wyjściowe toostore hello.
* Hello konfiguracji zaimportuje hello xPSDesiredStateConfiguration DSC zasobów, dzięki czemu można używać `xRemoteFile` toodownload hello pliki z repozytorium hello.
* Konfiguracja Hello utworzy katalog, w którym ma pliki binarne hello toostore.
* Witaj archiwum zasobów zostanie Wyodrębnij pliki hello z folderu zip hello.
* zasób instalacji pakietu Hello zainstaluje usługi mobilności hello z hello UNIFIEDAGENT. Wywołanie pliku EXE Instalatora hello określonych argumentów. (hello zmiennych, które skonstruować argumenty hello konieczne tooreflect toobe zmienić środowiska).
* Hello pakietu zasobów AzureAgent spowoduje zainstalowanie agenta maszyny Wirtualnej Azure hello, co jest zalecane na każdej maszynie Wirtualnej, która działa na platformie Azure. agent maszyny Wirtualnej Azure Hello ułatwia też możliwe tooadd toohello rozszerzenia maszyny Wirtualnej po pracy awaryjnej.
* Witaj usługi lub zasobów zapewnia, że hello powiązane usługi mobilności i hello usług platformy Azure są zawsze uruchomiona.

Zapisz konfigurację hello **ASRMobilityService**.

> [!NOTE]
> Należy pamiętać hello tooreplace CSIP na serwerze konfiguracji tooreflect hello rzeczywiste Zarządzanie tak, aby hello agent zostanie poprawnie podłączone i użyje hello poprawne hasło.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Krok 3: Przekaż tooAutomation DSC
Ponieważ konfiguracji hello DSC wprowadzone zaimportuje wymagane moduł zasobów DSC (xPSDesiredStateConfiguration), należy tooimport ten moduł w automatyzacji przed przekazaniem konfiguracji hello DSC.

Logowanie tooyour konta automatyzacji Przeglądaj zbyt**zasoby** > **modułów**i kliknij przycisk **galerii przeglądania**.

W tym miejscu można znaleźć modułu hello i zaimportuj go tooyour konta.

![Importowanie modułu](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Po zakończeniu, przejdź tooyour maszyny, gdzie masz hello Azure Resource Manager modułów zainstalowanych i kontynuować konfiguracji DSC tooimport hello nowo utworzony.

### <a name="import-cmdlets"></a>Poleceń cmdlet importu
W programie PowerShell Zaloguj tooyour subskrypcji platformy Azure. Modyfikowanie hello tooreflect poleceń cmdlet środowiska i przechwycić informacje o koncie automatyzacji w zmiennej:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Przekaż hello konfiguracji tooAutomation DSC za pomocą następującego polecenia cmdlet hello:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Kompiluj hello konfiguracji DSC automatyzacji
Następnie należy toocompile hello konfiguracji DSC automatyzacji tak, aby uruchomić tooregister tooit węzłów. Możesz osiągnąć, uruchamiając następujące polecenie cmdlet hello:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Może to zająć kilka minut, ponieważ jest wdrażany zasadniczo hello konfiguracji toohello hostowanej DSC ściągania usługi.

Po skompilowaniu hello konfiguracji mogą pobierać informacje zadania hello przy użyciu programu PowerShell (Get-AzureRmAutomationDscCompilationJob) lub za pomocą hello [portalu Azure](https://portal.azure.com/).

![Pobieranie zadania](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Teraz pomyślnie opublikowany i przekazać Twojej tooAutomation konfiguracji DSC usługi Konfiguracja DSC.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Krok 4: Dołączenia maszyny tooAutomation DSC
> [!NOTE]
> Jednym z wymagań wstępnych hello wykonywania czynności opisanych w tym scenariuszu jest czy maszynach z systemem Windows są aktualizowane przy użyciu najnowszej wersji platformy WMF hello. Można pobrać i zainstalować poprawną wersję powitania dla danej platformy z hello [Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Teraz utworzysz metaconfig zastosuje tooyour węzłów DSC. toosucceed z tym, należy tooretrieve hello punktu końcowego adresu URL i hello klucz podstawowy dla wybranego konta automatyzacji na platformie Azure. Te wartości można znaleźć **klucze** na powitania **wszystkie ustawienia** bloku hello konta automatyzacji.

![Wartości klucza](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

W tym przykładzie masz serwera fizycznego systemu Windows Server 2012 R2, które mają tooprotect przy użyciu usługi Site Recovery.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Sprawdź, czy wszystkie oczekujące operacje zmiany nazwy pliku w rejestrze hello
Przed rozpoczęciem tooassociate powitania serwera z punktem końcowym usługi Konfiguracja DSC automatyzacji hello zaleca się sprawdzanie wszelkie oczekujące operacje zmiany nazwy pliku w rejestrze hello. One może zabrania hello Instalator zakończył powodu tooa oczekujące na ponowny rozruch.

Uruchom następujące polecenia cmdlet tooverify nie oczekuje na ponowne uruchomienie na powitania serwera istnieje hello:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Jeśli ten pokazuje puste, to OK tooproceed. Jeśli nie, należy spełnić to przez ponowny rozruch serwera hello w oknie obsługi.

tooapply hello konfiguracji na serwerze hello rozpoczęciem hello PowerShell Integrated Scripting Environment (ISE) i uruchom hello następującego skryptu. Jest to zasadniczo lokalnej konfiguracji DSC poinstruować hello lokalny program Configuration Manager aparat tooregister z hello usługi Konfiguracja DSC automatyzacji i pobrać hello określonej konfiguracji (ASRMobilityService.localhost).

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Ta konfiguracja spowoduje tooregister aparatu, sama hello lokalny program Configuration Manager z usługi Konfiguracja DSC automatyzacji. Również określi, jak powinien działać aparat hello, co jego zrobić, jeśli istnieje kilka konfiguracji (ApplyAndAutoCorrect) i jak go należy kontynuować konfiguracji hello Jeśli ponowne uruchomienie jest wymagane.

Po uruchomieniu tego skryptu węzła hello powinien się rozpoczynać tooregister usługi Konfiguracja DSC automatyzacji.

![Trwa rejestrowanie węzła](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Wróć toohello portalu Azure widać tego węzła do nowo zarejestrowanych hello okazało się teraz w portalu hello.

![Zarejestrowany węzła w portalu hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Na serwerze hello można uruchomić następującego środowiska PowerShell zostały poprawnie zarejestrowane tooverify polecenia cmdlet, które hello węzła hello:

```powershell
Get-DscLocalConfigurationManager
```

Po konfiguracji hello został pobrany i stosowane toohello serwera, można to sprawdzić, uruchamiając następujące polecenie cmdlet hello:

```powershell
Get-DscConfigurationStatus
```

dane wyjściowe Hello pokazuje powitania serwera został pomyślnie pobierane jego konfiguracji:

![Dane wyjściowe](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Ponadto instalacji usługi mobilności hello ma własny dziennik, który znajduje się w temacie *SystemDrive*\ProgramData\ASRSetupLogs.

To wszystko. Teraz pomyślnie wdrożone i zarejestrowane hello usługi mobilności na maszynie hello mają tooprotect przy użyciu usługi Site Recovery. DSC będzie upewnij się, czy zawsze są uruchomione usługi hello wymagane.

![Pomyślne wdrożenie](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Po serwera zarządzania hello wykryje hello pomyślne wdrożenie, można skonfigurować ochrony i włączyć replikację na maszynie hello przy użyciu usługi Site Recovery.

## <a name="use-dsc-in-disconnected-environments"></a>Użyj usługi Konfiguracja DSC w środowiskach rozłączonych
Jeśli komputery nie są toohello połączenia internetowego, można nadal zależą od DSC toodeploy i skonfigurować usługi mobilności hello na powitania obciążeń, które mają tooprotect.

Możliwe jest utworzenie własnych serwera ściągania usługi Konfiguracja DSC w danym środowisku tooessentially Podaj hello takie same możliwości, które można uzyskać z usługi Konfiguracja DSC automatyzacji. Oznacza to klientom Witaj będzie pobierać hello konfiguracji (po jej zarejestrowaniu) toohello DSC punktu końcowego. Innym rozwiązaniem jest jednak toomanually wypychania hello DSC konfiguracji tooyour maszyny lokalnie lub zdalnie.

Należy pamiętać, że w tym przykładzie dodano parametr dla nazwy komputera hello. pliki zdalne Hello teraz znajdują się w udziale zdalnym, który powinien być dostępny przez hello maszyny, które mają tooprotect. Witaj na końcu skryptu hello enacts hello konfiguracji, a następnie uruchamia komputer docelowy toohello konfiguracji DSC tooapply hello.

### <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że zainstalowano ten moduł programu PowerShell xPSDesiredStateConfiguration hello. Dla komputerów z systemem Windows zainstalowaną WMF 5.0 można zainstalować moduł xPSDesiredStateConfiguration hello, uruchamiając następujące polecenia cmdlet na komputerach docelowych hello hello:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

Można również pobrać i zapisać hello modułu, w razie potrzeby toodistribute on tooWindows maszyny, które mają WMF 4.0. Uruchom to polecenie cmdlet na komputerze, w którym występuje PowerShellGet (WMF 5.0):

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Dla WMF 4.0, upewnij się również, że hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) jest zainstalowane na maszynie hello.

Witaj następującej konfiguracji może zostać umieszczony tooWindows maszyny, które mają WMF 5.0 i programu WMF 4.0:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Tooinstantiate własne serwera ściągania usługi Konfiguracja DSC na możliwości hello toomimic sieci firmowej, które można pobrać z usługi Konfiguracja DSC automatyzacji, zobacz [ustawienie serwera ściągania usługi Konfiguracja DSC sieci web](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Opcjonalnie: Wdrażanie konfiguracji DSC przy użyciu szablonu usługi Azure Resource Manager
Ten artykuł ma fokus w sposób tworzenia własnych tooautomatically konfiguracji DSC wdrażania usługi mobilności hello i hello Agent maszyny Wirtualnej — oraz upewnij się, że działają na maszynach hello, które mają tooprotect. Mamy także szablonu usługi Azure Resource Manager, który zostanie wdrożona tego DSC konfiguracji tooa nowe lub istniejące konto usługi Automatyzacja Azure. Szablon Hello będzie używać parametrów wejściowych toocreate automatyzacji zasoby zawierające hello zmienne dla danego środowiska.

Po wdrożeniu hello szablonu można po prostu odwołać toostep 4 w tym tooonboard przewodnik maszynach.

Szablon Hello wykona następujące hello:

1. Użyj istniejącego konta automatyzacji lub Utwórz nową
2. Przeprowadzanie parametrów wejściowych:
   * ASRRemoteFile--hello lokalizacji, gdzie są przechowywane instalacji usługi mobilności hello
   * ASRPassphrase--hello lokalizacji, gdzie są przechowywane hello passphrase.txt pliku
   * ASRCSEndpoint — Witaj adres IP serwera zarządzania
3. Zaimportuj moduł programu PowerShell xPSDesiredStateConfiguration hello
4. Tworzenie i kompilacja hello konfiguracji DSC

Witaj wszystkich poprzednich krokach nastąpi w odpowiedniej kolejności hello, tak aby można było uruchomić dołączania maszynach do ochrony.

Szablon Hello, instrukcje dotyczące wdrażania, znajduje się na [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Wdrażanie szablonu hello przy użyciu programu PowerShell:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Następne kroki
Po wdrożeniu agentów usługa mobilności hello można [włączyć replikację](site-recovery-vmware-to-azure.md) hello maszyn wirtualnych.
