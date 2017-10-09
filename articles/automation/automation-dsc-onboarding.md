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
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="54f0f-103">Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="54f0f-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="54f0f-104">Dlaczego zarządzanie maszynami z usługi Konfiguracja DSC automatyzacji Azure?</span><span class="sxs-lookup"><span data-stu-id="54f0f-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="54f0f-105">Podobnie jak [konfiguracji żądanego stanu środowiska PowerShell](https://technet.microsoft.com/library/dn249912.aspx), konfiguracji żądanego stanu programu Azure automatyzacji jest proste, ale wydajne, usługi do zarządzania konfiguracją dla węzłów DSC (fizycznych i maszyn wirtualnych) w dowolnego centrum danych chmury lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="54f0f-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="54f0f-106">Umożliwia on skalowalność między maszyn szybko i łatwo z lokalizacji centralnej, bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="54f0f-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="54f0f-107">Możesz łatwo dodać maszyny, przypisz je deklaratywne konfiguracje i wyświetlanie raportów przedstawiający każdego komputera stanu toohello potrzeby zgodności określonego...</span><span class="sxs-lookup"><span data-stu-id="54f0f-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="54f0f-108">Warstwa zarządzania Konfiguracja DSC automatyzacji Azure Hello jest tooDSC warstwa zarządzania jakie hello usługi Automatyzacja Azure jest tooPowerShell skryptów.</span><span class="sxs-lookup"><span data-stu-id="54f0f-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="54f0f-109">Innymi słowy w hello samo usługi Automatyzacja Azure ułatwia zarządzanie skryptów programu PowerShell, ułatwia on także zarządzać konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="54f0f-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="54f0f-110">toolearn więcej informacji na temat zalet hello przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [omówienie Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54f0f-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="54f0f-111">Konfiguracja DSC automatyzacji Azure mogą być używane toomanage różnych komputerach:</span><span class="sxs-lookup"><span data-stu-id="54f0f-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="54f0f-112">Maszyny wirtualne platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="54f0f-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="54f0f-113">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54f0f-113">Azure virtual machines</span></span>
* <span data-ttu-id="54f0f-114">Maszyny wirtualne Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="54f0f-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="54f0f-115">Fizyczna/wirtualna systemu Windows maszyny lokalnej, lub w chmurze innych niż Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="54f0f-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="54f0f-116">W infrastrukturze lokalnej, na platformie Azure lub w chmurze innych niż Azure maszyny fizycznej/wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="54f0f-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="54f0f-117">Ponadto jeśli nie jest gotowy toomanage konfiguracji komputera z chmury hello, konfiguracja DSC automatyzacji Azure mogą służyć jako punktu końcowego tylko do raportu.</span><span class="sxs-lookup"><span data-stu-id="54f0f-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="54f0f-118">Dzięki temu można tooset (push) wymaganą konfiguracją za pośrednictwem usługi Konfiguracja DSC lokalnego i Wyświetl sformatowanego Szczegóły raportowania zgodności węzła z hello żądany stan automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="54f0f-119">Witaj następujące sekcje przedstawiają sposób dołączyć każdego typu maszyny tooAzure usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="54f0f-120">Maszyny wirtualne platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="54f0f-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="54f0f-121">Z usługi Konfiguracja DSC automatyzacji Azure można łatwo dodać maszyn wirtualnych platformy Azure (klasyczne) dla zarządzania konfiguracją przy użyciu hello portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f0f-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="54f0f-122">Pod maską hello i bez administratora o tooremote do hello maszyny Wirtualnej hello rozszerzenia konfiguracji żądanego stanu programu Azure VM rejestruje hello maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="54f0f-123">Ponieważ hello rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, kroki tootrack postępu lub Rozwiązywanie problemów z są udostępniane w hello [ **dołączania maszyny wirtualnej Azure Rozwiązywanie problemów z** ](#troubleshooting-azure-virtual-machine-onboarding)poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="54f0f-124">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="54f0f-124">Azure portal</span></span>

<span data-ttu-id="54f0f-125">W hello [portalu Azure](http://portal.azure.com/), kliknij przycisk **Przeglądaj** -> **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="54f0f-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="54f0f-126">Wybierz hello ma tooonboard maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="54f0f-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="54f0f-127">W bloku maszyny wirtualnej hello pulpitu nawigacyjnego kliknij **wszystkie ustawienia** -> **rozszerzenia** -> **Dodaj**  ->   **Azure Automation DSC** -> **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="54f0f-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="54f0f-128">Wprowadź hello [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) wymagane dla Twojego przypadek użycia, Twoje konto usługi Automatyzacja klucz rejestracji i adresu URL rejestracji i opcjonalnie węzła toohello tooassign konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54f0f-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="54f0f-129">adres URL rejestracji hello toofind i klucza hello automatyzacji konta tooonboard hello maszyny, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="54f0f-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54f0f-130">PowerShell</span></span>

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

## <a name="azure-virtual-machines"></a><span data-ttu-id="54f0f-131">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54f0f-131">Azure virtual machines</span></span>

<span data-ttu-id="54f0f-132">Konfiguracja DSC usługi Automatyzacja Azure umożliwia łatwe dołączyć maszyn wirtualnych platformy Azure do zarządzania konfiguracją za pomocą hello portalu Azure, szablony usługi Azure Resource Manager lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f0f-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="54f0f-133">Pod maską hello i bez administratora o tooremote do hello maszyny Wirtualnej hello rozszerzenia konfiguracji żądanego stanu programu Azure VM rejestruje hello maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="54f0f-134">Ponieważ hello rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, kroki tootrack postępu lub Rozwiązywanie problemów z są udostępniane w hello [ **dołączania maszyny wirtualnej Azure Rozwiązywanie problemów z** ](#troubleshooting-azure-virtual-machine-onboarding)poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="54f0f-135">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="54f0f-135">Azure portal</span></span>

<span data-ttu-id="54f0f-136">W hello [portalu Azure](https://portal.azure.com/), przejdź toohello konto usługi Automatyzacja Azure, w którym ma tooonboard maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="54f0f-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="54f0f-137">Na pulpicie nawigacyjnym konta automatyzacji hello, kliknij przycisk **węzłów DSC** -> **dodać maszyny Wirtualnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="54f0f-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="54f0f-138">W obszarze **wybierz maszyny wirtualne tooonboard**, wybierz co najmniej tooonboard maszyny wirtualnej platformy Azure więcej.</span><span class="sxs-lookup"><span data-stu-id="54f0f-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="54f0f-139">W obszarze **Konfigurowanie danych rejestracji**, wprowadź hello [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) wymagane dla tej sprawy użycia i opcjonalnie węzła toohello tooassign konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54f0f-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="54f0f-140">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54f0f-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="54f0f-141">Można wdrożyć maszyn wirtualnych platformy Azure i został załadowany tooAzure usługi Konfiguracja DSC automatyzacji za pomocą szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54f0f-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="54f0f-142">Zobacz [skonfigurować Maszynę wirtualną za pomocą rozszerzenia usługi Konfiguracja DSC i konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) szablonu przykład tego onboards tooAzure istniejących maszyn wirtualnych usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="54f0f-143">toofind hello klucza i rejestracji adresu URL rejestracji podjęte jako danych wejściowych w tym szablonie, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="54f0f-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54f0f-144">PowerShell</span></span>

<span data-ttu-id="54f0f-145">Witaj [AzureRmAutomationDscNode rejestru](/powershell/module/azurerm.automation/register-azurermautomationdscnode) polecenia cmdlet mogą być używane tooonboard maszyn wirtualnych w hello portalu Azure za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f0f-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="54f0f-146">Maszyny wirtualne Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="54f0f-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="54f0f-147">Możesz łatwo dodać usług Amazon Web Services maszyn wirtualnych do zarządzania konfiguracji DSC automatyzacji Azure za pomocą hello usług AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="54f0f-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="54f0f-148">Dowiedz się więcej o hello toolkit [tutaj](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="54f0f-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="54f0f-149">Fizyczna/wirtualna systemu Windows maszyny lokalnej, lub w chmurze innych niż Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="54f0f-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="54f0f-150">Lokalnymi maszynami z systemem Windows i maszyny z systemem Windows w chmurze innych niż Azure (np. Amazon Web Services) można też tooAzure został załadowany usługi Konfiguracja DSC automatyzacji, tak długo, jak długo mają toohello wychodzący dostęp do Internetu za pośrednictwem kilku prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="54f0f-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="54f0f-151">Upewnij się, że hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) jest zainstalowany na komputerach hello ma tooAzure tooonboard usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="54f0f-152">Postępuj zgodnie ze wskazówkami hello sekcji [ **metaconfigurations generowania DSC** ](#generating-dsc-metaconfigurations) poniżej toogenerate folder zawierający hello potrzebne DSC metaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="54f0f-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="54f0f-153">Zdalnie zastosowanie mają tooonboard hello DSC środowiska PowerShell metakonfigurację toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="54f0f-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="54f0f-154">**to polecenie jest uruchamiane maszyny Hello musi mieć hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane**:</span><span class="sxs-lookup"><span data-stu-id="54f0f-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="54f0f-155">Jeśli nie można zastosować hello metaconfigurations DSC środowiska PowerShell zdalnie, należy skopiować hello metaconfigurations folder w kroku 2 na każdym tooonboard maszyny.</span><span class="sxs-lookup"><span data-stu-id="54f0f-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="54f0f-156">Następnie wywołaj **DscLocalConfigurationManager zestaw** lokalnie na każdym tooonboard maszyny.</span><span class="sxs-lookup"><span data-stu-id="54f0f-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="54f0f-157">Za pomocą portalu Azure hello lub poleceń cmdlet, sprawdź, czy hello maszyny tooonboard teraz wyświetlane jako węzły DSC zarejestrowana na koncie usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="54f0f-158">W infrastrukturze lokalnej, na platformie Azure lub w chmurze innych niż Azure maszyny fizycznej/wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="54f0f-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="54f0f-159">Linux lokalnych maszyn maszyn z systemem Linux na platformie Azure i maszyny z systemem Linux w chmurze Azure z systemem innym niż mogą być tooAzure został załadowany usługi Konfiguracja DSC automatyzacji tak długo, jak długo mają toohello wychodzący dostęp do Internetu za pośrednictwem kilku prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="54f0f-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="54f0f-160">Upewnij się, że hello najnowszą wersję [PowerShell konfiguracji żądanego stanu dla systemu Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) jest zainstalowany na komputerach hello ma tooAzure tooonboard usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="54f0f-161">Jeśli hello [ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) liter użycia i chcesz tooonboard maszyny takie że **zarówno** ściąganie danych z i zgłoś tooAzure usługi Konfiguracja DSC automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="54f0f-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="54f0f-162">Na każdym Linux maszyny tooonboard tooAzure usługi Konfiguracja DSC automatyzacji Użyj tooonboard Register.py przy użyciu powitalne ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager:</span><span class="sxs-lookup"><span data-stu-id="54f0f-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="54f0f-163">toofind hello klucza i rejestracji adresu URL rejestracji dla Twojego konta automatyzacji, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="54f0f-164">Jeśli hello PowerShell DSC lokalny program Configuration Manager domyślnie **czy** **nie** liter Użyj lub mają tooonboard maszyny w taki sposób, że ich tylko zgłosić tooAzure usługi Konfiguracja DSC automatyzacji, ale nie ściągnięcia Konfiguracja lub moduły programu PowerShell z niego, wykonaj kroki od 3 do 6.</span><span class="sxs-lookup"><span data-stu-id="54f0f-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="54f0f-165">W przeciwnym razie przejdź bezpośrednio toostep 6.</span><span class="sxs-lookup"><span data-stu-id="54f0f-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="54f0f-166">Postępuj zgodnie ze wskazówkami hello hello [ **metaconfigurations generowania DSC** ](#generating-dsc-metaconfigurations) sekcji poniżej toogenerate folder zawierający metaconfigurations DSC hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="54f0f-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="54f0f-167">Zastosuj zdalnie hello DSC środowiska PowerShell metakonfigurację toohello maszyn, które mają tooonboard:</span><span class="sxs-lookup"><span data-stu-id="54f0f-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="54f0f-168">to polecenie jest uruchamiane maszyny Hello musi mieć hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="54f0f-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="54f0f-169">Jeśli nie można zastosować hello metaconfigurations DSC środowiska PowerShell zdalnie, dla każdego tooonboard maszyny Linux, skopiuj hello metakonfigurację odpowiednią toothat maszynę z folderu hello w kroku 5 na powitania Linux maszyny.</span><span class="sxs-lookup"><span data-stu-id="54f0f-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="54f0f-170">Następnie wywołaj `SetDscLocalConfigurationManager.py` lokalnie na każdym komputerze z systemem Linux ma tooAzure tooonboard usługi Konfiguracja DSC automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="54f0f-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="54f0f-171">Za pomocą portalu Azure hello lub poleceń cmdlet, sprawdź, czy hello maszyny tooonboard teraz wyświetlane jako węzły DSC zarejestrowana na koncie usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="54f0f-172">Trwa generowanie metaconfigurations DSC</span><span class="sxs-lookup"><span data-stu-id="54f0f-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="54f0f-173">toogenerically dołączyć dowolnego komputera tooAzure usługi Konfiguracja DSC automatyzacji [metakonfigurację DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) może być, generowane, gdy stosowane, określa, że agent hello DSC na powitania toopull maszyny z i/lub raportu tooAzure usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="54f0f-174">Metaconfigurations DSC dla konfiguracji DSC automatyzacji Azure mogą być generowane przy użyciu konfiguracji DSC środowiska PowerShell, albo polecenia cmdlet programu PowerShell usługi Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="54f0f-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="54f0f-175">DSC metaconfigurations zawierają hello kluczy tajnych potrzebne tooonboard tooan maszyny konta automatyzacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="54f0f-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="54f0f-176">Upewnij się, że tooproperly chronić żadnych metaconfigurations DSC utworzone, lub usuń je po użyciu.</span><span class="sxs-lookup"><span data-stu-id="54f0f-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="54f0f-177">Za pomocą konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="54f0f-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="54f0f-178">Otwórz hello ISE programu PowerShell jako administrator na maszynie w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="54f0f-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="54f0f-179">Maszyna Hello musi mieć hello najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="54f0f-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="54f0f-180">Skopiuj powitania po skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="54f0f-180">Copy hello following script locally.</span></span> <span data-ttu-id="54f0f-181">Ten skrypt zawiera konfiguracji DSC środowiska PowerShell do tworzenia metaconfigurations i tookick polecenia, wyłącz hello metakonfigurację tworzenia.</span><span class="sxs-lookup"><span data-stu-id="54f0f-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

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

3. <span data-ttu-id="54f0f-182">Wypełnij hello klucz rejestracji i adres URL dla konta automatyzacji, jak również nazwy hello hello tooonboard maszyny.</span><span class="sxs-lookup"><span data-stu-id="54f0f-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="54f0f-183">Wszystkie inne parametry są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="54f0f-183">All other parameters are optional.</span></span> <span data-ttu-id="54f0f-184">toofind hello klucza i rejestracji adresu URL rejestracji dla Twojego konta automatyzacji, zobacz hello [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="54f0f-185">Jeśli chcesz hello maszyny tooreport DSC stan informacji tooAzure usługi Konfiguracja DSC automatyzacji, ale nie ściągania konfiguracji lub moduły programu PowerShell, należy ustawić hello **ReportOnly** tootrue parametru.</span><span class="sxs-lookup"><span data-stu-id="54f0f-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="54f0f-186">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="54f0f-186">Run hello script.</span></span> <span data-ttu-id="54f0f-187">Teraz powinno istnieć folder o nazwie **DscMetaConfigs** w katalogu roboczym zawierający hello metaconfigurations DSC środowiska PowerShell dla hello tooonboard maszyny (jako administrator):</span><span class="sxs-lookup"><span data-stu-id="54f0f-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="54f0f-188">Za pomocą poleceń cmdlet usługi Automatyzacja Azure hello</span><span class="sxs-lookup"><span data-stu-id="54f0f-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="54f0f-189">Jeśli ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager hello zgodne z przypadek użycia i ma tooonboard maszyny w taki sposób, że ich zarówno ściąganie danych z i zgłoś tooAzure usługi Konfiguracja DSC automatyzacji, polecenia cmdlet usługi Automatyzacja Azure hello zapewniają uproszczona metoda generowania hello DSC metaconfigurations potrzebne:</span><span class="sxs-lookup"><span data-stu-id="54f0f-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="54f0f-190">Hello Otwórz konsolę lub środowisko ISE programu PowerShell jako administrator na maszynie w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="54f0f-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="54f0f-191">Połącz, używając Menedżera zasobów tooAzure **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="54f0f-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="54f0f-192">Hello maszyn, które mają tooonboard z hello automatyzacji konta toowhich węzłach tooonboard pobrać hello metaconfigurations DSC środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="54f0f-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

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
    
4. <span data-ttu-id="54f0f-193">Teraz powinno istnieć folder o nazwie ***DscMetaConfigs***, zawierający hello metaconfigurations DSC środowiska PowerShell dla hello tooonboard maszyny (jako administrator):</span><span class="sxs-lookup"><span data-stu-id="54f0f-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="54f0f-194">Bezpieczne rejestracji</span><span class="sxs-lookup"><span data-stu-id="54f0f-194">Secure registration</span></span>

<span data-ttu-id="54f0f-195">Maszyny można bezpiecznie dodać tooan konto usługi Automatyzacja Azure za pośrednictwem protokołu rejestracji platformy WMF 5 DSC hello, dzięki czemu DSC węzła tooauthenticate tooa ściągnięcia V2 DSC środowiska PowerShell raportowania serwer lub (w tym konfiguracja DSC automatyzacji Azure).</span><span class="sxs-lookup"><span data-stu-id="54f0f-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="54f0f-196">węzeł Hello rejestruje serwer toohello w **adresu URL rejestracji**, uwierzytelniania przy użyciu **klucz rejestracji**.</span><span class="sxs-lookup"><span data-stu-id="54f0f-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="54f0f-197">Podczas rejestracji węzeł hello DSC i serwera ściągania usługi Konfiguracja DSC/raportowania negocjowania unikatowy certyfikat dla tego węzła toouse uwierzytelniania toohello serwera po rejestracji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="54f0f-198">Dzięki temu węzłów został załadowany z personifikacja jeden inny, na przykład jeśli węzeł zostanie naruszone bezpieczeństwo i zachowuje się złośliwe.</span><span class="sxs-lookup"><span data-stu-id="54f0f-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="54f0f-199">Po rejestracji hello klucz rejestracji nie jest używany do uwierzytelniania ponownie i zostaną usunięte z węzła hello.</span><span class="sxs-lookup"><span data-stu-id="54f0f-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="54f0f-200">Możesz uzyskać hello informacje wymagane do protokołu rejestracji hello DSC z hello **zarządzanie kluczami** bloku w portalu Azure w wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="54f0f-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="54f0f-201">Otwarcie bloku tego klikając ikonę klucza hello na powitania **Essentials** panel hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="54f0f-202">Adres URL rejestracji jest pole adresu URL hello w bloku zarządzanie kluczami hello.</span><span class="sxs-lookup"><span data-stu-id="54f0f-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="54f0f-203">Klucz rejestracji jest hello klucz dostępu podstawowy lub pomocniczy klucz dostępu w bloku zarządzanie kluczami hello.</span><span class="sxs-lookup"><span data-stu-id="54f0f-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="54f0f-204">Można użyć albo klucza.</span><span class="sxs-lookup"><span data-stu-id="54f0f-204">Either key can be used.</span></span>

<span data-ttu-id="54f0f-205">Aby zwiększyć bezpieczeństwo, klucze podstawowe i pomocnicze dostępu hello konta automatyzacji można ponownie wygenerować w dowolnym momencie (na powitania **zarządzanie kluczami** bloku) tooprevent węzła przyszłych rejestracji przy użyciu poprzednich kluczy.</span><span class="sxs-lookup"><span data-stu-id="54f0f-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="54f0f-206">Rozwiązywanie problemów z dołączania maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54f0f-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="54f0f-207">Konfiguracja DSC usługi Automatyzacja Azure pozwala łatwo dołączać maszyny wirtualne systemu Windows Azure dla zarządzania konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="54f0f-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="54f0f-208">Pod maską hello hello rozszerzenia konfiguracji żądanego stanu programu Azure maszyny Wirtualnej jest używane tooregister hello maszyny Wirtualnej w usłudze Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="54f0f-209">Ponieważ hello rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, śledzenie postępu i rozwiązywanie problemów z jej wykonanie może być ważne.</span><span class="sxs-lookup"><span data-stu-id="54f0f-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="54f0f-210">Każda metoda dołączania, które tooAzure maszyny Wirtualnej systemu Windows Azure Automation DSC, używający rozszerzenia konfiguracji żądanego stanu programu Azure VM hello może zająć godzinę tooan tooshow węzła hello się zarejestrowanej w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0f-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="54f0f-211">Jest to powodu toohello na instalację programu Windows Management Framework 5.0 hello maszyny Wirtualnej przez rozszerzenia DSC maszyn wirtualnych Azure hello, która jest wymagana tooonboard hello wirtualna tooAzure usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="54f0f-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="54f0f-212">tootroubleshoot lub widok stanu hello hello rozszerzenie konfiguracji żądanego stanu programu Azure VM hello portalu Azure Przejdź toohello maszyny Wirtualnej trwa został załadowany, następnie kliknij pozycję -> **wszystkie ustawienia** -> **rozszerzeń**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="54f0f-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="54f0f-213">Aby uzyskać więcej informacji, kliknij **wyświetlić szczegółowy stan**.</span><span class="sxs-lookup"><span data-stu-id="54f0f-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="54f0f-214">Wygaśnięcie certyfikatu i ponowna rejestracja</span><span class="sxs-lookup"><span data-stu-id="54f0f-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="54f0f-215">Po zarejestrowaniu komputera jako węzła DSC w konfiguracji DSC automatyzacji Azure istnieje wiele powodów dlaczego może być konieczne tooreregister tego węzła w hello przyszłych:</span><span class="sxs-lookup"><span data-stu-id="54f0f-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="54f0f-216">Po zarejestrowaniu każdego węzła automatycznie negocjuje unikatowy certyfikat do uwierzytelniania, która wygasa po roku.</span><span class="sxs-lookup"><span data-stu-id="54f0f-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="54f0f-217">Obecnie hello protokołu rejestrację DSC programu PowerShell nie automatycznego odnawiania certyfikatów, po ich wkrótce wygasną, więc należy węzłów hello tooreregister po roku.</span><span class="sxs-lookup"><span data-stu-id="54f0f-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="54f0f-218">Przed ponownie zarejestrować, upewnij się, że każdy węzeł działa system Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="54f0f-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="54f0f-219">Jeśli certyfikat uwierzytelniania węzła wygasa, a węzeł hello nie jest zarejestrowane, węzeł hello będzie toocommunicate w usłudze Automatyzacja Azure i zostaną oznaczone jako "Unresponsive."</span><span class="sxs-lookup"><span data-stu-id="54f0f-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="54f0f-220">Ponowna rejestracja wykonać 90 dni lub mniejsza od czasu wygaśnięcia certyfikatu hello lub w dowolnym momencie po upływie czasu wygaśnięcia certyfikatu hello spowoduje nowego certyfikatu Trwa generowanie i używanie.</span><span class="sxs-lookup"><span data-stu-id="54f0f-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="54f0f-221">toochange żadnych [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) które zostały określone podczas początkowej rejestracji węzła hello, takich jak ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="54f0f-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="54f0f-222">Obecnie te wartości agenta DSC można zmienić tylko za pośrednictwem ponowna rejestracja.</span><span class="sxs-lookup"><span data-stu-id="54f0f-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="54f0f-223">Jedynym wyjątkiem Hello jest hello konfiguracji węzła przypisanej toohello węzła — można to zmienić w konfiguracji DSC automatyzacji Azure bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="54f0f-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="54f0f-224">Ponowna rejestracja mogą być wykonywane w hello zarejestrowana węzła hello początkowo przy użyciu dowolnej z metod dołączania hello tak samo opisanych w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="54f0f-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="54f0f-225">Nie trzeba toounregister węzeł z usługi Konfiguracja DSC automatyzacji Azure przed ponownie go zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="54f0f-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="54f0f-226">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="54f0f-226">Related Articles</span></span>

* [<span data-ttu-id="54f0f-227">Omówienie usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="54f0f-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="54f0f-228">Polecenia cmdlet systemu Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="54f0f-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="54f0f-229">Cennik usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="54f0f-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
