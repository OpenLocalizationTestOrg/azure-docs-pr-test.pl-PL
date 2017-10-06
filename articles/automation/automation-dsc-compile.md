---
title: aaaCompiling konfiguracji DSC automatyzacji Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób konfiguracji konfiguracji żądanego stanu (DSC) toocompile automatyzacji Azure."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Kompilowanie konfiguracji DSC automatyzacji Azure

Konfiguracje konfiguracji żądanego stanu (DSC) na dwa sposoby automatyzacji Azure można kompilować: w hello portalu Azure i przy użyciu programu Windows PowerShell. Witaj Poniższa tabela pomoże określić kiedy toouse, którego metoda oparta na powitania właściwości każdej:

### <a name="azure-portal"></a>Azure Portal

* Najprostszą metodą z interaktywnego interfejsu użytkownika
* Wartości parametru proste tooprovide formularza
* Łatwo śledzić stan zadania
* Dostęp uwierzytelniony dzięki funkcji logowania do platformy Azure

### <a name="windows-powershell"></a>Windows PowerShell

* Wywoływanie z wiersza polecenia za pomocą poleceń cmdlet środowiska Windows PowerShell
* Może być uwzględniony w zautomatyzowane rozwiązanie z wielu kroków
* Podaj wartości parametrów proste i złożone
* Śledź stan zadania
* Toosupport klienta wymaganych poleceń cmdlet programu PowerShell
* ConfigurationData — dostęp próbny
* Kompiluj konfiguracje, które używają poświadczeń

Po podjęciu decyzji dotyczącej Metoda kompilacji, można użyć odpowiednich procedur hello poniżej toostart kompilowanie.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>Kompilowanie Konfiguracja DSC o hello portalu Azure

1. Twoje konto usługi Automatyzacja kliknij **konfiguracji DSC**.
2. Kliknij przycisk tooopen konfiguracji jego bloku.
3. Kliknij przycisk **skompilować**.
4. W przypadku konfiguracji hello nie ma parametrów, będzie zostanie wyświetlony monit o tooconfirm czy toocompile go. Jeśli konfiguracja hello ma parametry, hello **skompilować konfiguracji** zostanie otwarty blok, więc można podać wartości parametrów. Zobacz hello [ **podstawowe parametry** ](#basic-parameters) sekcji poniżej, aby uzyskać więcej informacji o parametrach.
5. Witaj **zadania kompilacji** bloku jest otwarty, dzięki czemu można śledzić stan zadania kompilacji hello i hello konfiguracje węzłów (MOF konfiguracji dokumenty) powodowała ona toobe umieszczane na powitania serwera ściągania usługi Konfiguracja DSC automatyzacji Azure.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Kompilowanie konfiguracji DSC, przy użyciu programu Windows PowerShell

Można użyć [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart kompilowania przy użyciu programu Windows PowerShell. powitania po przykładowy kod uruchamia kompilacji konfiguracji DSC o nazwie **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`Zwraca wartość typu kompilacji zadania obiektów, których można używać tootrack jego stan. Następnie można użyć tego obiektu zadania kompilacji [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello stan zadania kompilacji hello, i [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview jego strumieni (dane wyjściowe). powitania po przykładowy kod uruchamia kompilacji hello **SampleConfig** konfiguracji, czeka, dopóki nie zostało ukończone, a następnie wyświetla jego strumieni.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Podstawowe parametry
Deklaracji parametru w konfiguracji DSC, w tym typy parametrów i właściwości działania hello takie same jak elementy runbook automatyzacji Azure. Zobacz [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md) toolearn więcej informacji na temat parametrów elementu runbook.

Witaj poniższy przykład korzysta z dwóch parametrów o nazwie **FeatureName** i **IsPresent**, toodetermine hello wartości właściwości w hello **ParametersExample.sample** węzła Konfiguracja generowanych podczas kompilacji.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

Można skompilować konfiguracji DSC, używanego podstawowych parametrów w portalu usługi Konfiguracja DSC automatyzacji Azure hello lub przy użyciu programu Azure PowerShell:

### <a name="portal"></a>Portal

W portalu hello można wprowadzić wartości parametrów po kliknięciu przycisku **skompilować**.

![tekst alternatywny](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell wymaga parametrów w [hashtable](http://technet.microsoft.com/library/hh847780.aspx) gdzie klucz hello odpowiada nazwie parametru hello i hello jest równa wartości parametru hello.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Aby dowiedzieć się, jak przekazywanie PSCredentials jako parametrów, zobacz <a href="#credential-assets"> **zasoby poświadczeń** </a> poniżej.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** pozwala tooseparate strukturalnych konfiguracji z dowolnym środowisku określonej konfiguracji podczas korzystania z usługi Konfiguracja DSC środowiska PowerShell. Zobacz [oddzielenie "Co" od "Where" w konfiguracji DSC środowiska PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn więcej informacji na temat **ConfigurationData**.

> [!NOTE]
> Można użyć **ConfigurationData** podczas kompilowania w konfiguracji DSC automatyzacji Azure przy użyciu programu Azure PowerShell, ale nie w hello portalu Azure.

Witaj następującej konfiguracji DSC przykład używa **ConfigurationData** za pośrednictwem hello **$ConfigurationData** i **$AllNodes** słów kluczowych. Należy również hello [ **xWebAdministration** modułu](https://www.powershellgallery.com/packages/xWebAdministration/) w tym przykładzie:

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

Można skompilować konfiguracji DSC hello powyżej przy użyciu programu PowerShell. Witaj poniżej PowerShell dodaje dwie toohello konfiguracji węzła serwera ściągania usługi Konfiguracja DSC automatyzacji Azure: **ConfigurationDataSample.MyVM1** i **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Elementy zawartości

Odwołania do zasobów są hello tej samej konfiguracji DSC automatyzacji Azure i elementów runbook. Zobacz hello poniżej, aby uzyskać więcej informacji:

* [Certyfikaty](automation-certificates.md)
* [Połączenia](automation-connections.md)
* [Poświadczenia](automation-credentials.md)
* [Zmienne](automation-variables.md)

### <a name="credential-assets"></a>Zasoby poświadczeń

Podczas konfiguracji DSC automatyzacji Azure mogą odwoływać się zasoby poświadczeń przy użyciu **Get-AzureRmAutomationCredential**, zasoby poświadczeń może również zostać przekazane za za pomocą parametrów, w razie potrzeby. Jeśli konfiguracja przyjmuje parametr **PSCredential** wpisz, a następnie potrzebna nazwa ciąg hello toopass zasób poświadczenia usługi Automatyzacja Azure jako wartość tego parametru, a nie obiektu PSCredential. Tle hello zasób poświadczenia usługi Automatyzacja Azure hello o tej nazwie zostanie pobrana i przekazany toohello konfiguracji.

Przechowywanie poświadczeń zabezpieczone w konfiguracji węzłów (MOF konfiguracji dokumenty) wymaga szyfrowania poświadczeń hello w pliku MOF konfiguracji węzła hello. Automatyzacja Azure dalsze przyjmuje jednym kroku i szyfruje hello całego pliku MOF. Jednak obecnie musi wskazujemy DSC środowiska PowerShell szkodzi dla poświadczeń toobe wyjściowych w postaci zwykłego tekstu podczas generowania MOF konfiguracji węzła, ponieważ DSC programu PowerShell nie może ustalić, czy usługi Automatyzacja Azure będzie szyfrowania całego pliku MOF powitania po jego Generowanie za pomocą zadania kompilacji.

Można określić DSC środowiska PowerShell jest poprawny dla poświadczeń toobe wyjściowych w postaci zwykłego tekstu w konfiguracji węzła hello wygenerowane za pomocą [ **ConfigurationData**](#configurationdata). Należy przekazać `PSDscAllowPlainTextPassword = $true` za pośrednictwem **ConfigurationData** dla każdego węzła bloku, którego nazwa występującego w konfiguracji hello DSC i używa poświadczeń.

Witaj poniższy przykład przedstawia konfiguracji DSC, która używa zasób poświadczenia usługi Automatyzacja.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

Można skompilować konfiguracji DSC hello powyżej przy użyciu programu PowerShell. Witaj poniżej PowerShell dodaje dwie toohello konfiguracji węzła serwera ściągania usługi Konfiguracja DSC automatyzacji Azure: **CredentialSample.MyVM1** i **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Importowanie konfiguracji węzła

Możesz również zaimportować configuratons węzła (za), który ma być kompilowana poza platformą Azure. Jedną z zalet tego jest może być podpisana confiturations tego węzła.
Konfiguracja węzła podpisem jest weryfikowany lokalnie w węźle zarządzanym przez agenta hello DSC, zapewnienie, że są stosowane toohello węzła konfiguracji hello pochodzi z autoryzowanego źródła.

> [!NOTE]
> Można użyć importu podpisany konfiguracji do konta usługi Automatyzacja Azure, ale automatyzacji Azure nie obsługuje obecnie kompilowanie konfiguracje podpisem.

> [!NOTE]
> Plik konfiguracji węzła nie może być większa niż 1 MB tooallow go zaimportować do usługi Automatyzacja Azure toobe.

Aby dowiedzieć się jak konfiguracje węzłów toosign na https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Importowanie konfiguracji węzła, w portalu Azure hello

1. Twoje konto usługi Automatyzacja kliknij **konfiguracji węzłów DSC**.

    ![Konfiguracje węzłów DSC](./media/automation-dsc-compile/node-config.png)
2. W hello **konfiguracji węzłów DSC** bloku, kliknij przycisk **dodać NodeConfiguration**.
3. W hello **importu** bloku, kliknij hello folderu ikona dalej toohello **pliku konfiguracji węzła** toobrowse pole tekstowe dla pliku konfiguracji węzła (MOF) na komputerze lokalnym.

    ![Przeglądaj w poszukiwaniu pliku lokalnego](./media/automation-dsc-compile/import-browse.png)
4. Wprowadź nazwę w hello **Nazwa konfiguracji** pola tekstowego. Ta nazwa musi odpowiadać nazwie hello hello konfiguracji, z którego został skompilowany hello konfiguracji węzła.
5. Kliknij przycisk **OK**.

### <a name="importing-a-node-configuration-with-powershell"></a>Importowanie konfiguracji węzła, przy użyciu programu PowerShell

Można użyć hello [AzureRmAutomationDscNodeConfiguration importu](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport polecenia cmdlet konfiguracji węzła, na koncie automatyzacji.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



