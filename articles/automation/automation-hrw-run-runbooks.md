---
title: elementy runbook aaaRun na Azure procesu roboczego Runbook automatyzacji hybrydowe | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera informacje dotyczące wykonywania elementów runbook na komputerach w lokalnym centrum danych lub dostawcy chmury z rolą hybrydowy proces roboczy elementu Runbook hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Uruchomione elementy runbook na hybrydowy proces roboczy elementu Runbook 
Nie ma różnic w strukturze hello elementów runbook, które są uruchamiane w automatyzacji Azure oraz te, które uruchamiane na hybrydowy proces roboczy elementu Runbook. Elementy Runbook korzystające z każdym najprawdopodobniej różnią się znacznie jednak ponieważ elementy runbook, zwykle przeznaczonych dla hybrydowego procesu roboczego elementu Runbook zarządzanie zasobami na komputerze lokalnym hello sam lub względem zasobów w środowisku lokalnym hello, których jest wdrożona, podczas elementów runbook w automatyzacji Azure zazwyczaj zarządzać zasobami w hello chmury Azure.

Można edytować element runbook dla hybrydowego procesu roboczego Runbook automatyzacji Azure, ale mogą mieć trudności, Jeśli spróbujesz tootest hello runbook w edytorze hello.  Moduły PowerShell Hello, które uzyskują dostęp do zasobów lokalnych hello może nie być zainstalowana w Twoim środowisku usługi Automatyzacja Azure w takim przypadku, hello testu nie powiedzie się.  Po zainstalowaniu hello wymagane moduły, a następnie hello element runbook zostanie uruchomiony, ale nie będą mogli tooaccess zasoby lokalne do ukończenia testu.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Uruchamianie elementu runbook na hybrydowy proces roboczy elementu Runbook
[Uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) opisano różne metody uruchamiania elementu runbook.  Dodaje hybrydowy proces roboczy elementu Runbook **RunOn** opcja, w którym można określić nazwę hello grupy hybrydowego procesu roboczego elementu Runbook.  Jeśli określono grupę hello runbook jest pobierane i wykonywane przez pracowników hello w tej grupie.  Jeśli ta opcja nie jest określona, następnie jest uruchamiany w automatyzacji Azure normalnie.

Po uruchomieniu elementu runbook w portalu Azure hello prezentowany **Uruchom na** opcja, w którym można wybrać **Azure** lub **hybrydowy proces roboczy**.  W przypadku wybrania **hybrydowy proces roboczy**, hello grupy można wybrać z listy rozwijanej.

Użyj hello **RunOn** parametru.  Możesz użyć hello następujące polecenia toostart elementu runbook o nazwie Test-Runbook na hybrydowego grupy procesów roboczych elementu Runbook o nazwie MyHybridGroup przy użyciu programu Windows PowerShell.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Witaj **RunOn** parametru dodano toohello **Start AzureAutomationRunbook** polecenia cmdlet w wersji od 0.9.1 Microsoft Azure PowerShell.  Należy [pobrać najnowszą wersję hello](https://azure.microsoft.com/downloads/) Jeśli masz wcześniejszą zainstalowane.  Wystarczy tooinstall tej wersji stacji roboczej, na którym jest uruchamiany hello elementu runbook z programu Windows PowerShell.  Nie trzeba tooinstall go na komputerze pracownika hello o ile nie mają elementów runbook toostart z tego komputera.  Obecnie nie można uruchomić elementu runbook na hybrydowy proces roboczy elementu Runbook z innego elementu runbook, ponieważ wymagałoby to hello najnowszą wersję programu Azure Powershell toobe zainstalowane na Twoim koncie automatyzacji.  najnowszą wersję Hello jest automatycznie aktualizowana w automatyzacji Azure i automatycznie wkrótce przesuwana toohello pracowników.
>
>

## <a name="runbook-permissions"></a>Uprawnienia elementów Runbook
Elementów Runbook uruchomionych na hybrydowy proces roboczy elementu Runbook nie można Użyj hello sama metoda, która jest zazwyczaj używana w przypadku elementów runbook uwierzytelniania tooAzure zasobów, ponieważ uzyskują dostęp do zasobów poza platformą Azure.  Hello runbook albo zapewniają własnym uwierzytelnianiem toolocal zasobów lub można określić tooprovide konta RunAs kontekstu użytkownika dla wszystkich elementów runbook.

### <a name="runbook-authentication"></a>Uwierzytelnianie elementu Runbook
Domyślnie elementów runbook zostanie uruchomiony w kontekście hello hello lokalnego konta systemowego na powitania na komputerze lokalnym, więc użytkownik musi podać własne tooresources uwierzytelniania, który będzie miał dostęp.  

Można użyć [poświadczeń](http://msdn.microsoft.com/library/dn940015.aspx) i [certyfikatu](http://msdn.microsoft.com/library/dn940013.aspx) zasoby w elemencie runbook za pomocą poleceń cmdlet, które pozwalają toospecify poświadczeń, można uwierzytelniać toodifferent zasobów.  Witaj poniższy przykład przedstawia części elementu runbook, który powoduje ponowne uruchomienie komputera.  Pobiera poświadczenia na podstawie nazwy zasobów i hello poświadczeń komputera hello z zasób zmiennej, a następnie używa tych wartości w poleceniu cmdlet Restart-Computer hello.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

Można też skorzystać [InlineScript](automation-powershell-workflow.md#inlinescript), co pozwala toorun bloków kodu na innym komputerze z poświadczeń określonych przez hello [typowy parametr PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Konto Uruchom jako
Zamiast zapewnienia uwierzytelniania ich własnych zasobów toolocal elementów runbook, można określić **RunAs** konto do grupy hybrydowych procesów roboczych.  Należy określić [zasób poświadczeń](automation-credentials.md) mający dostęp do zasobów toolocal i wszystkich elementów runbook działać w ramach tych poświadczeń, podczas uruchamiania na hybrydowy proces roboczy elementu Runbook w grupie hello.  

Nazwa użytkownika Hello poświadczenia hello musi być w jednym z następujących formatów hello:

* domena azwa_użytkownika
* username@domain
* Nazwa użytkownika (dla kont lokalnych toohello na komputerze lokalnym)

Użyj hello następujące procedury toospecify konto Uruchom jako dla grupy hybrydowych procesów roboczych:

1. Utwórz [zasób poświadczeń](automation-credentials.md) z zasobami toolocal dostępu.
2. Otwórz konto automatyzacji hello w hello portalu Azure.
3. Wybierz hello **hybrydowego procesu roboczego grupy** Kafelek, a następnie wybierz grupę hello.
4. Wybierz **wszystkie ustawienia** , a następnie **ustawienia grupy hybrydowego procesu roboczego**.
5. Zmień **Uruchom jako** z **domyślne** za**niestandardowy**.
6. Wybierz poświadczenie hello i kliknij przycisk **zapisać**.

### <a name="automation-run-as-account"></a>Konto Uruchom jako automatyzacji
Jako część procesu kompilacji automatycznego wdrażania zasobów na platformie Azure może wymagać dostępu tooon lokalnych systemów toosupport zadań lub zestaw kroków w sekwencji wdrożenia.  toosupport uwierzytelnianie na platformie Azure przy użyciu konta Uruchom jako hello, należy tooinstall hello Uruchom jako certyfikat konta.  

Witaj, po runbook programu PowerShell *RunAsCertificateToHybridWorker eksportu*, eksportuje hello Uruchom jako certyfikat z konta usługi Automatyzacja Azure i pliki do pobrania i importuje go do magazynu certyfikatów komputera lokalnego hello na Hybrydowy proces roboczy podłączony toohello tego samego konta.  Po ukończeniu tego kroku sprawdza to, czy Proces roboczy hello można pomyślnie uwierzytelnić tooAzure hello konta Uruchom jako.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Zapisz hello *RunAsCertificateToHybridWorker eksportu* runbook tooyour komputera z `.ps1` rozszerzenia.  Zaimportuj go do Twojego konta automatyzacji i edytować runbook hello, zmiana hello wartość zmiennej hello `$Password` z własnego hasła.  Publikowanie, a następnie uruchom element runbook hello przeznaczonych dla grupy hybrydowego procesu roboczego hello Uruchom i uwierzytelniania przy użyciu konta Uruchom jako hello elementów runbook.  Hello zadania strumienia raporty hello próba tooimport hello certyfikat do magazynu komputer lokalny hello i jest zgodny z wielu wierszy w zależności od liczby kont automatyzacji są zdefiniowane w ramach subskrypcji i jeśli uwierzytelnianie zakończy się pomyślnie.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Rozwiązywanie problemów z elementów runbook na hybrydowy proces roboczy elementu Runbook
Dzienniki są przechowywane lokalnie na każdym hybrydowy proces roboczy na C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Hybrydowy proces roboczy rejestruje także błędów i zdarzeń w dzienniku zdarzeń systemu Windows hello w obszarze **aplikacji i usług Logs\Microsoft-SMA\Operational**.  Zdarzenia związane z toorunbooks wykonana w wątku roboczym hello są zapisywane zbyt**aplikacji i usług Logs\Microsoft-Automation\Operational**.  Witaj **Microsoft SMA** dziennika zawiera wiele więcej zdarzeń powiązanych toohello runbook zadania wciśnięcia toohello procesu roboczego hello przetwarzanie i elementu hello runbook.  Podczas hello **automatyzacji Microsoft** dziennika zdarzeń nie ma wiele zdarzeń przy użyciu szczegółów z hello rozwiązywania problemów z wykonanie elementu runbook, znajduje się co najmniej wyniki hello hello zadanie elementu runbook.  

[Element Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md) są wysyłane tooAzure automatyzacji z hybrydowych procesów roboczych tylko, takich jak zadania elementu runbook są uruchamiane w chmurze hello.  Można również włączyć hello pełne i strumieni postępu hello sam sposób jak dla innych elementów runbook.  

Jeśli elementy runbook nie są pomyślnie wykonywane i hello zadanie podsumowania przedstawia stan **zawieszone**, zapoznaj się z tematem hello Rozwiązywanie problemów z artykułu [hybrydowy proces roboczy elementu Runbook: kończy zadanie elementu runbook ze stanem Zawieszone](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat różnych metod hello, które mogą być używane toostart elementu runbook [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md).  
* Zobacz toounderstand hello różne procedury do pracy z programu PowerShell i przepływ pracy programu PowerShell elementów runbook w automatyzacji Azure za pomocą hello edytor tekstowy, [edytowanie elementu Runbook automatyzacji Azure](automation-edit-textual-runbook.md)
