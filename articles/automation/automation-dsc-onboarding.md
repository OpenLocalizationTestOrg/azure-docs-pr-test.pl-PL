---
title: "aaaOnboarding maszyny do zarządzania przez Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Jak toosetup maszyny do zarządzania w usłudze Konfiguracja DSC automatyzacji Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Dlaczego zarządzanie maszynami z usługi Konfiguracja DSC automatyzacji Azure?

Podobnie jak [konfiguracji żądanego stanu środowiska PowerShell](https://technet.microsoft.com/library/dn249912.aspx), konfiguracji żądanego stanu programu Azure automatyzacji jest proste, ale wydajne, usługi do zarządzania konfiguracją dla węzłów DSC (fizycznych i maszyn wirtualnych) w dowolnego centrum danych chmury lub lokalnie. Umożliwia on skalowalność między maszyn szybko i łatwo z lokalizacji centralnej, bezpieczne. Możesz łatwo dodać maszyny, przypisz je deklaratywne konfiguracje i wyświetlanie raportów przedstawiający każdego komputera stanu toohello potrzeby zgodności określonego... Warstwa zarządzania Konfiguracja DSC automatyzacji Azure Hello jest tooDSC warstwa zarządzania jakie hello usługi Automatyzacja Azure jest tooPowerShell skryptów. Innymi słowy w hello samo usługi Automatyzacja Azure ułatwia zarządzanie skryptów programu PowerShell, ułatwia on także zarządzać konfiguracji DSC. toolearn więcej informacji na temat zalet hello przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [omówienie Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md).

Konfiguracja DSC automatyzacji Azure mogą być używane toomanage różnych komputerach:

* Maszyny wirtualne platformy Azure (klasyczne)
* Maszyny wirtualne platformy Azure
* Maszyny wirtualne Amazon Web Services (AWS)
* Fizyczna/wirtualna systemu Windows maszyny lokalnej, lub w chmurze innych niż Azure/AWS
* W infrastrukturze lokalnej, na platformie Azure lub w chmurze innych niż Azure maszyny fizycznej/wirtualną systemu Linux

Ponadto jeśli nie jest gotowy toomanage konfiguracji komputera z chmury hello, konfiguracja DSC automatyzacji Azure mogą służyć jako punktu końcowego tylko do raportu. Dzięki temu można tooset (push) wymaganą konfiguracją za pośrednictwem usługi Konfiguracja DSC lokalnego i Wyświetl sformatowanego Szczegóły raportowania zgodności węzła z hello żądany stan automatyzacji Azure.

Witaj następujące sekcje przedstawiają sposób dołączyć każdego typu maszyny tooAzure usługi Konfiguracja DSC automatyzacji.

## <a name="azure-virtual-machines-classic"></a>Maszyny wirtualne platformy Azure (klasyczne)

Z usługi Konfiguracja DSC automatyzacji Azure można łatwo dodać maszyn wirtualnych platformy Azure (klasyczne) dla zarządzania konfiguracją przy użyciu hello portalu Azure lub programu PowerShell. Pod maską hello i bez administratora o tooremote do hello maszyny Wirtualnej hello rozszerzenia konfiguracji żądanego stanu programu Azure VM rejestruje hello maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure. Ponieważ hello rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, kroki tootrack postępu lub Rozwiązywanie problemów z są udostępniane w hello [ **dołączania maszyny wirtualnej Azure Rozwiązywanie problemów z** ](#troubleshooting-azure-virtual-machine-onboarding)poniższej sekcji.

### <a name="azure-portal"></a>Azure Portal

W hello [portalu Azure](http://portal.azure.com/), kliknij przycisk **Przeglądaj** -> **maszyn wirtualnych (klasyczne)**. Wybierz hello ma tooonboard maszyny Wirtualnej systemu Windows. W bloku maszyny wirtualnej hello pulpitu nawigacyjnego kliknij **wszystkie ustawienia** -> **rozszerzenia** -> **Dodaj**  ->   **Azure Automation DSC** -> **utworzyć**. Wprowadź hello [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) wymagane dla Twojego przypadek użycia, Twoje konto usługi Automatyzacja klucz rejestracji i adresu URL rejestracji i opcjonalnie węzła toohello tooassign konfiguracji maszyny Wirtualnej.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

adres URL rejestracji hello toofind i klucza hello automatyzacji konta tooonboard hello maszyny, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Maszyny wirtualne platformy Azure

Konfiguracja DSC usługi Automatyzacja Azure umożliwia łatwe dołączyć maszyn wirtualnych platformy Azure do zarządzania konfiguracją za pomocą hello portalu Azure, szablony usługi Azure Resource Manager lub programu PowerShell. Pod maską hello i bez administratora o tooremote do hello maszyny Wirtualnej hello rozszerzenia konfiguracji żądanego stanu programu Azure VM rejestruje hello maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure. Ponieważ hello rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, kroki tootrack postępu lub Rozwiązywanie problemów z są udostępniane w hello [ **dołączania maszyny wirtualnej Azure Rozwiązywanie problemów z** ](#troubleshooting-azure-virtual-machine-onboarding)poniższej sekcji.

### <a name="azure-portal"></a>Azure Portal

W hello [portalu Azure](https://portal.azure.com/), przejdź toohello konto usługi Automatyzacja Azure, w którym ma tooonboard maszyn wirtualnych. Na pulpicie nawigacyjnym konta automatyzacji hello, kliknij przycisk **węzłów DSC** -> **dodać maszyny Wirtualnej Azure**.

W obszarze **wybierz maszyny wirtualne tooonboard**, wybierz co najmniej tooonboard maszyny wirtualnej platformy Azure więcej.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

W obszarze **Konfigurowanie danych rejestracji**, wprowadź hello [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) wymagane dla tej sprawy użycia i opcjonalnie węzła toohello tooassign konfiguracji maszyny Wirtualnej.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager

Można wdrożyć maszyn wirtualnych platformy Azure i został załadowany tooAzure usługi Konfiguracja DSC automatyzacji za pomocą szablonów usługi Azure Resource Manager. Zobacz [skonfigurować Maszynę wirtualną za pomocą rozszerzenia usługi Konfiguracja DSC i konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) szablonu przykład tego onboards tooAzure istniejących maszyn wirtualnych usługi Konfiguracja DSC automatyzacji. toofind hello klucza i rejestracji adresu URL rejestracji podjęte jako danych wejściowych w tym szablonie, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.

### <a name="powershell"></a>PowerShell

Witaj [AzureRmAutomationDscNode rejestru](/powershell/module/azurerm.automation/register-azurermautomationdscnode) polecenia cmdlet mogą być używane tooonboard maszyn wirtualnych w hello portalu Azure za pomocą programu PowerShell.

## <a name="amazon-web-services-aws-virtual-machines"></a>Maszyny wirtualne Amazon Web Services (AWS)

Możesz łatwo dodać usług Amazon Web Services maszyn wirtualnych do zarządzania konfiguracji DSC automatyzacji Azure za pomocą hello usług AWS DSC Toolkit. Dowiedz się więcej o hello toolkit [tutaj](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Fizyczna/wirtualna systemu Windows maszyny lokalnej, lub w chmurze innych niż Azure/AWS

Lokalnymi maszynami z systemem Windows i maszyny z systemem Windows w chmurze innych niż Azure (np. Amazon Web Services) można też tooAzure został załadowany usługi Konfiguracja DSC automatyzacji, tak długo, jak długo mają toohello wychodzący dostęp do Internetu za pośrednictwem kilku prostych kroków:

1. Upewnij się, że hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) jest zainstalowany na komputerach hello ma tooAzure tooonboard usługi Konfiguracja DSC automatyzacji.
2. Postępuj zgodnie ze wskazówkami hello sekcji [ **metaconfigurations generowania DSC** ](#generating-dsc-metaconfigurations) poniżej toogenerate folder zawierający hello potrzebne DSC metaconfigurations.
3. Zdalnie zastosowanie mają tooonboard hello DSC środowiska PowerShell metakonfigurację toohello maszyny. **to polecenie jest uruchamiane maszyny Hello musi mieć hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Jeśli nie można zastosować hello metaconfigurations DSC środowiska PowerShell zdalnie, należy skopiować hello metaconfigurations folder w kroku 2 na każdym tooonboard maszyny. Następnie wywołaj **DscLocalConfigurationManager zestaw** lokalnie na każdym tooonboard maszyny.
5. Za pomocą portalu Azure hello lub poleceń cmdlet, sprawdź, czy hello maszyny tooonboard teraz wyświetlane jako węzły DSC zarejestrowana na koncie usługi Automatyzacja Azure.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>W infrastrukturze lokalnej, na platformie Azure lub w chmurze innych niż Azure maszyny fizycznej/wirtualną systemu Linux

Linux lokalnych maszyn maszyn z systemem Linux na platformie Azure i maszyny z systemem Linux w chmurze Azure z systemem innym niż mogą być tooAzure został załadowany usługi Konfiguracja DSC automatyzacji tak długo, jak długo mają toohello wychodzący dostęp do Internetu za pośrednictwem kilku prostych kroków:

1. Upewnij się, że hello najnowszą wersję [PowerShell konfiguracji żądanego stanu dla systemu Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) jest zainstalowany na komputerach hello ma tooAzure tooonboard usługi Konfiguracja DSC automatyzacji.
2. Jeśli hello [ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) liter użycia i chcesz tooonboard maszyny takie że **zarówno** ściąganie danych z i zgłoś tooAzure usługi Konfiguracja DSC automatyzacji:

   + Na każdym Linux maszyny tooonboard tooAzure usługi Konfiguracja DSC automatyzacji Użyj tooonboard Register.py przy użyciu powitalne ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello klucza i rejestracji adresu URL rejestracji dla Twojego konta automatyzacji, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.

     Jeśli hello PowerShell DSC lokalny program Configuration Manager domyślnie **czy** **nie** liter Użyj lub mają tooonboard maszyny w taki sposób, że ich tylko zgłosić tooAzure usługi Konfiguracja DSC automatyzacji, ale nie ściągnięcia Konfiguracja lub moduły programu PowerShell z niego, wykonaj kroki od 3 do 6. W przeciwnym razie przejdź bezpośrednio toostep 6.

3. Postępuj zgodnie ze wskazówkami hello hello [ **metaconfigurations generowania DSC** ](#generating-dsc-metaconfigurations) sekcji poniżej toogenerate folder zawierający metaconfigurations DSC hello potrzebne.
4. Zastosuj zdalnie hello DSC środowiska PowerShell metakonfigurację toohello maszyn, które mają tooonboard:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

to polecenie jest uruchamiane maszyny Hello musi mieć hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane.

1. Jeśli nie można zastosować hello metaconfigurations DSC środowiska PowerShell zdalnie, dla każdego tooonboard maszyny Linux, skopiuj hello metakonfigurację odpowiednią toothat maszynę z folderu hello w kroku 5 na powitania Linux maszyny. Następnie wywołaj `SetDscLocalConfigurationManager.py` lokalnie na każdym komputerze z systemem Linux ma tooAzure tooonboard usługi Konfiguracja DSC automatyzacji:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Za pomocą portalu Azure hello lub poleceń cmdlet, sprawdź, czy hello maszyny tooonboard teraz wyświetlane jako węzły DSC zarejestrowana na koncie usługi Automatyzacja Azure.

## <a name="generating-dsc-metaconfigurations"></a>Trwa generowanie metaconfigurations DSC

toogenerically dołączyć dowolnego komputera tooAzure usługi Konfiguracja DSC automatyzacji [metakonfigurację DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) może być, generowane, gdy stosowane, określa, że agent hello DSC na powitania toopull maszyny z i/lub raportu tooAzure usługi Konfiguracja DSC automatyzacji. Metaconfigurations DSC dla konfiguracji DSC automatyzacji Azure mogą być generowane przy użyciu konfiguracji DSC środowiska PowerShell, albo polecenia cmdlet programu PowerShell usługi Azure Automation hello.

> [!NOTE]
> DSC metaconfigurations zawierają hello kluczy tajnych potrzebne tooonboard tooan maszyny konta automatyzacji zarządzania. Upewnij się, że tooproperly chronić żadnych metaconfigurations DSC utworzone, lub usuń je po użyciu.

### <a name="using-a-dsc-configuration"></a>Za pomocą konfiguracji DSC

1. Otwórz hello ISE programu PowerShell jako administrator na maszynie w środowisku lokalnym. Maszyna Hello musi mieć hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane.
2. Skopiuj powitania po skrypt lokalnie. Ten skrypt zawiera konfiguracji DSC środowiska PowerShell do tworzenia metaconfigurations i tookick polecenia, wyłącz hello metakonfigurację tworzenia.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Wypełnij hello klucz rejestracji i adres URL dla konta automatyzacji, jak również nazwy hello hello tooonboard maszyny. Wszystkie inne parametry są opcjonalne. toofind hello klucza i rejestracji adresu URL rejestracji dla Twojego konta automatyzacji, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.
4. Jeśli chcesz hello maszyny tooreport DSC stan informacji tooAzure usługi Konfiguracja DSC automatyzacji, ale nie ściągania konfiguracji lub moduły programu PowerShell, należy ustawić hello **ReportOnly** tootrue parametru.
5. Uruchom skrypt hello. Teraz powinno istnieć folder o nazwie **DscMetaConfigs** w katalogu roboczym zawierający hello metaconfigurations DSC środowiska PowerShell dla hello tooonboard maszyny (jako administrator):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Za pomocą poleceń cmdlet usługi Automatyzacja Azure hello

Jeśli ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager hello zgodne z przypadek użycia i ma tooonboard maszyny w taki sposób, że ich zarówno ściąganie danych z i zgłoś tooAzure usługi Konfiguracja DSC automatyzacji, polecenia cmdlet usługi Automatyzacja Azure hello zapewniają uproszczona metoda generowania hello DSC metaconfigurations potrzebne:

1. Hello Otwórz konsolę lub środowisko ISE programu PowerShell jako administrator na maszynie w środowisku lokalnym.
2. Połącz, używając Menedżera zasobów tooAzure **Add-AzureRmAccount**
3. Hello maszyn, które mają tooonboard z hello automatyzacji konta toowhich węzłach tooonboard pobrać hello metaconfigurations DSC środowiska PowerShell:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. Teraz powinno istnieć folder o nazwie ***DscMetaConfigs***, zawierający hello metaconfigurations DSC środowiska PowerShell dla hello tooonboard maszyny (jako administrator):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Bezpieczne rejestracji

Maszyny można bezpiecznie dodać tooan konto usługi Automatyzacja Azure za pośrednictwem protokołu rejestracji platformy WMF 5 DSC hello, dzięki czemu DSC węzła tooauthenticate tooa ściągnięcia V2 DSC środowiska PowerShell raportowania serwer lub (w tym konfiguracja DSC automatyzacji Azure). węzeł Hello rejestruje serwer toohello w **adresu URL rejestracji**, uwierzytelniania przy użyciu **klucz rejestracji**. Podczas rejestracji węzeł hello DSC i serwera ściągania usługi Konfiguracja DSC/raportowania negocjowania unikatowy certyfikat dla tego węzła toouse uwierzytelniania toohello serwera po rejestracji. Dzięki temu węzłów został załadowany z personifikacja jeden inny, na przykład jeśli węzeł zostanie naruszone bezpieczeństwo i zachowuje się złośliwe. Po rejestracji hello klucz rejestracji nie jest używany do uwierzytelniania ponownie i zostaną usunięte z węzła hello.

Możesz uzyskać hello informacje wymagane do protokołu rejestracji hello DSC z hello **zarządzanie kluczami** bloku w portalu Azure w wersji zapoznawczej hello. Otwarcie bloku tego klikając ikonę klucza hello na powitania **Essentials** panel hello konta automatyzacji.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* Adres URL rejestracji jest pole adresu URL hello w bloku zarządzanie kluczami hello.
* Klucz rejestracji jest hello klucz dostępu podstawowy lub pomocniczy klucz dostępu w bloku zarządzanie kluczami hello. Można użyć albo klucza.

Aby zwiększyć bezpieczeństwo, klucze podstawowe i pomocnicze dostępu hello konta automatyzacji można ponownie wygenerować w dowolnym momencie (na powitania **zarządzanie kluczami** bloku) tooprevent węzła przyszłych rejestracji przy użyciu poprzednich kluczy.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Rozwiązywanie problemów z dołączania maszyny wirtualnej platformy Azure

Konfiguracja DSC usługi Automatyzacja Azure pozwala łatwo dołączać maszyny wirtualne systemu Windows Azure dla zarządzania konfiguracją. Pod maską hello hello rozszerzenia konfiguracji żądanego stanu programu Azure maszyny Wirtualnej jest używane tooregister hello maszyny Wirtualnej w usłudze Konfiguracja DSC automatyzacji Azure. Ponieważ hello rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, śledzenie postępu i rozwiązywanie problemów z jej wykonanie może być ważne.

> [!NOTE]
> Każda metoda dołączania, które tooAzure maszyny Wirtualnej systemu Windows Azure Automation DSC, używający rozszerzenia konfiguracji żądanego stanu programu Azure VM hello może zająć godzinę tooan tooshow węzła hello się zarejestrowanej w automatyzacji Azure. Jest to powodu toohello na instalację programu Windows Management Framework 5.0 hello maszyny Wirtualnej przez rozszerzenia DSC maszyn wirtualnych Azure hello, która jest wymagana tooonboard hello wirtualna tooAzure usługi Konfiguracja DSC automatyzacji.

tootroubleshoot lub widok stanu hello hello rozszerzenie konfiguracji żądanego stanu programu Azure VM hello portalu Azure Przejdź toohello maszyny Wirtualnej trwa został załadowany, następnie kliknij pozycję -> **wszystkie ustawienia** -> **rozszerzeń**   ->  **DSC**. Aby uzyskać więcej informacji, kliknij **wyświetlić szczegółowy stan**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Wygaśnięcie certyfikatu i ponowna rejestracja

Po zarejestrowaniu komputera jako węzła DSC w konfiguracji DSC automatyzacji Azure istnieje wiele powodów dlaczego może być konieczne tooreregister tego węzła w hello przyszłych:

* Po zarejestrowaniu każdego węzła automatycznie negocjuje unikatowy certyfikat do uwierzytelniania, która wygasa po roku. Obecnie hello protokołu rejestrację DSC programu PowerShell nie automatycznego odnawiania certyfikatów, po ich wkrótce wygasną, więc należy węzłów hello tooreregister po roku. Przed ponownie zarejestrować, upewnij się, że każdy węzeł działa system Windows Management Framework 5.0 RTM. Jeśli certyfikat uwierzytelniania węzła wygasa, a węzeł hello nie jest zarejestrowane, węzeł hello będzie toocommunicate w usłudze Automatyzacja Azure i zostaną oznaczone jako "Unresponsive." Ponowna rejestracja wykonać 90 dni lub mniejsza od czasu wygaśnięcia certyfikatu hello lub w dowolnym momencie po upływie czasu wygaśnięcia certyfikatu hello spowoduje nowego certyfikatu Trwa generowanie i używanie.
* toochange żadnych [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) które zostały określone podczas początkowej rejestracji węzła hello, takich jak ConfigurationMode. Obecnie te wartości agenta DSC można zmienić tylko za pośrednictwem ponowna rejestracja. Jedynym wyjątkiem Hello jest hello konfiguracji węzła przypisanej toohello węzła — można to zmienić w konfiguracji DSC automatyzacji Azure bezpośrednio.

Ponowna rejestracja mogą być wykonywane w hello zarejestrowana węzła hello początkowo przy użyciu dowolnej z metod dołączania hello tak samo opisanych w tym dokumencie. Nie trzeba toounregister węzeł z usługi Konfiguracja DSC automatyzacji Azure przed ponownie go zarejestrować.

## <a name="related-articles"></a>Pokrewne artykuły

* [Omówienie usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md)
* [Polecenia cmdlet systemu Azure Automation DSC](/powershell/module/azurerm.automation/#automation)
* [Cennik usługi Konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/pricing/details/automation/)
