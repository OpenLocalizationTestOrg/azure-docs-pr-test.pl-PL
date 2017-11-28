---
title: "Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Konfigurowanie komputerów do zarządzania w usłudze Konfiguracja DSC automatyzacji Azure"
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
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="52b10-103">Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="52b10-104">Dlaczego zarządzanie maszynami z usługi Konfiguracja DSC automatyzacji Azure?</span><span class="sxs-lookup"><span data-stu-id="52b10-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="52b10-105">Podobnie jak [konfiguracji żądanego stanu środowiska PowerShell](https://technet.microsoft.com/library/dn249912.aspx), konfiguracji żądanego stanu programu Azure automatyzacji jest proste, ale wydajne, usługi do zarządzania konfiguracją dla węzłów DSC (fizycznych i maszyn wirtualnych) w dowolnego centrum danych chmury lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="52b10-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="52b10-106">Umożliwia on skalowalność między maszyn szybko i łatwo z lokalizacji centralnej, bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="52b10-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="52b10-107">Możesz łatwo dodać maszyny, przypisz je deklaratywne konfiguracje i wyświetlanie raportów przedstawiający każdego komputera zgodności do pożądanego stanu, który można określić.</span><span class="sxs-lookup"><span data-stu-id="52b10-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="52b10-108">Warstwa zarządzania Konfiguracja DSC automatyzacji Azure jest DSC warstwa zarządzania usługi Automatyzacja Azure jest do wykonywania skryptów PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b10-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="52b10-109">Innymi słowy w taki sam sposób jak usługi Automatyzacja Azure ułatwia zarządzanie skryptów programu PowerShell, pomaga również zarządzać konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="52b10-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="52b10-110">Aby dowiedzieć się więcej o zaletach usługi Konfiguracja DSC automatyzacji Azure, zobacz [omówienie Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52b10-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="52b10-111">Konfiguracja DSC automatyzacji Azure mogą służyć do zarządzania różnych komputerach:</span><span class="sxs-lookup"><span data-stu-id="52b10-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="52b10-112">Maszyny wirtualne platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="52b10-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="52b10-113">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-113">Azure virtual machines</span></span>
* <span data-ttu-id="52b10-114">Maszyny wirtualne Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="52b10-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="52b10-115">Fizyczna/wirtualna systemu Windows maszyny lokalnej, lub w chmurze innych niż Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="52b10-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="52b10-116">W infrastrukturze lokalnej, na platformie Azure lub w chmurze innych niż Azure maszyny fizycznej/wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="52b10-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="52b10-117">Ponadto jeśli firma nie jest gotowa do zarządzania konfiguracji komputera z chmury, konfiguracja DSC automatyzacji Azure mogą służyć jako punktu końcowego tylko do raportu.</span><span class="sxs-lookup"><span data-stu-id="52b10-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="52b10-118">Dzięki temu można ustawić żądaną konfiguracją (push) za pośrednictwem usługi Konfiguracja DSC lokalnego oraz sformatowanego Szczegóły raportowania zgodności węzła z żądanego stanu w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="52b10-119">W poniższych sekcjach opisano, jak można dołączyć każdego typu maszyny do usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="52b10-120">Maszyny wirtualne platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="52b10-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="52b10-121">Z usługi Konfiguracja DSC automatyzacji Azure można łatwo dodać maszyn wirtualnych platformy Azure (klasyczne) dla zarządzania konfiguracją przy użyciu portalu Azure, lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b10-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="52b10-122">Pod maską i bez konieczności zdalnego do maszyny Wirtualnej administratora rozszerzenia konfiguracji żądanego stanu programu Azure VM rejestruje maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="52b10-123">Ponieważ rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, kroki, aby śledzić postęp lub Rozwiązywanie problemów znajdują się w [ **dołączania maszyny wirtualnej Azure Rozwiązywanie problemów z** ](#troubleshooting-azure-virtual-machine-onboarding) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="52b10-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="52b10-124">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="52b10-124">Azure portal</span></span>

<span data-ttu-id="52b10-125">W [portalu Azure](http://portal.azure.com/), kliknij przycisk **Przeglądaj** -> **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="52b10-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="52b10-126">Wybierz maszynę Wirtualną systemu Windows, które chcesz dołączyć.</span><span class="sxs-lookup"><span data-stu-id="52b10-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="52b10-127">W bloku pulpitu nawigacyjnego maszyny wirtualnej, kliknij **wszystkie ustawienia** -> **rozszerzenia** -> **Dodaj** -> **Konfiguracja DSC automatyzacji Azure** -> **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="52b10-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="52b10-128">Wprowadź [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) wymagane dla Twojego przypadek użycia, Twoje konto usługi Automatyzacja klucz rejestracji i adresu URL rejestracji i opcjonalnie konfiguracji węzła można przypisać do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b10-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="52b10-129">Aby znaleźć adres URL rejestracji i klucza dla konta usługi Automatyzacja, aby dołączyć maszynę, aby zobaczyć [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="52b10-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="52b10-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52b10-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="52b10-131">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-131">Azure virtual machines</span></span>

<span data-ttu-id="52b10-132">Konfiguracja DSC usługi Automatyzacja Azure pozwala łatwo dodać maszyn wirtualnych platformy Azure do zarządzania konfiguracją przy użyciu portalu Azure, szablonów usługi Azure Resource Manager lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b10-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="52b10-133">Pod maską i bez konieczności zdalnego do maszyny Wirtualnej administratora rozszerzenia konfiguracji żądanego stanu programu Azure VM rejestruje maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="52b10-134">Ponieważ rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, kroki, aby śledzić postęp lub Rozwiązywanie problemów znajdują się w [ **dołączania maszyny wirtualnej Azure Rozwiązywanie problemów z** ](#troubleshooting-azure-virtual-machine-onboarding) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="52b10-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="52b10-135">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="52b10-135">Azure portal</span></span>

<span data-ttu-id="52b10-136">W [portalu Azure](https://portal.azure.com/), przejdź do konta usługi Automatyzacja Azure, które chcesz dołączyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b10-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="52b10-137">Na pulpicie nawigacyjnym konta automatyzacji, kliknij przycisk **węzłów DSC** -> **dodać maszyny Wirtualnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="52b10-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="52b10-138">W obszarze **wybierz maszyny wirtualne do dołączenia**, wybierz jeden lub więcej wirtualnej platformy Azure, maszyny dołączyć.</span><span class="sxs-lookup"><span data-stu-id="52b10-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="52b10-139">W obszarze **Konfigurowanie danych rejestracji**, wprowadź [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) wymagany dla tej sprawy używany oraz opcjonalnie konfiguracji węzła można przypisać do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b10-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="52b10-140">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="52b10-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="52b10-141">Można wdrożyć maszyn wirtualnych platformy Azure i dołączać do konfiguracji DSC automatyzacji Azure za pomocą szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52b10-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="52b10-142">Zobacz [skonfigurować Maszynę wirtualną za pomocą rozszerzenia usługi Konfiguracja DSC i konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) szablonu przykład tego onboards istniejącej maszyny Wirtualnej do usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="52b10-143">Aby znaleźć klucz rejestracji i adresu URL rejestracji podjęte jako danych wejściowych w tym szablonie, zobacz [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="52b10-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="52b10-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52b10-144">PowerShell</span></span>

<span data-ttu-id="52b10-145">[AzureRmAutomationDscNode rejestru](/powershell/module/azurerm.automation/register-azurermautomationdscnode) polecenia cmdlet można używać do dodawania maszyn wirtualnych w portalu Azure za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b10-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="52b10-146">Maszyny wirtualne Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="52b10-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="52b10-147">Możesz łatwo dodać usług Amazon Web Services maszyn wirtualnych do zarządzania konfiguracji DSC automatyzacji Azure przy użyciu zestawu narzędzi usług AWS DSC.</span><span class="sxs-lookup"><span data-stu-id="52b10-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="52b10-148">Dowiedz się więcej o zestawie narzędzi programu [tutaj](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="52b10-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="52b10-149">Fizyczna/wirtualna systemu Windows maszyny lokalnej, lub w chmurze innych niż Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="52b10-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="52b10-150">Lokalnymi maszynami z systemem Windows i maszyny z systemem Windows w chmurze innych niż Azure (np. Amazon Web Services) także można dołączać do usługi Konfiguracja DSC automatyzacji Azure, jak długo mają połączenia wychodzące z Internetem za pośrednictwem kilku prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="52b10-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="52b10-151">Upewnij się, najnowsza wersja [platformy WMF 5](http://aka.ms/wmf5latest) jest zainstalowany na komputerach, do których chcesz dołączyć do usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="52b10-152">Postępuj zgodnie z instrukcjami w sekcji [ **metaconfigurations generowania DSC** ](#generating-dsc-metaconfigurations) poniżej, aby wygenerować folderu zawierającego potrzebne metaconfigurations DSC.</span><span class="sxs-lookup"><span data-stu-id="52b10-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="52b10-153">Zdalnie Zastosuj metakonfigurację DSC programu PowerShell na maszynach, które chcesz dołączyć.</span><span class="sxs-lookup"><span data-stu-id="52b10-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="52b10-154">**To polecenie jest uruchamiane maszyny musi mieć najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane**:</span><span class="sxs-lookup"><span data-stu-id="52b10-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="52b10-155">Jeśli nie można zastosować metaconfigurations DSC środowiska PowerShell zdalnie, należy skopiować metaconfigurations folder w kroku 2 na każdej maszynie do dołączenia.</span><span class="sxs-lookup"><span data-stu-id="52b10-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="52b10-156">Następnie wywołaj **DscLocalConfigurationManager zestaw** lokalnie na każdym komputerze do dołączenia.</span><span class="sxs-lookup"><span data-stu-id="52b10-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="52b10-157">Za pomocą portalu Azure lub poleceń cmdlet, sprawdź, czy maszyny do dołączenia teraz wyświetlane jako węzły DSC zarejestrowana na koncie usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="52b10-158">W infrastrukturze lokalnej, na platformie Azure lub w chmurze innych niż Azure maszyny fizycznej/wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="52b10-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="52b10-159">Maszyny z systemem Linux lokalnymi, maszyny z systemem Linux na platformie Azure i maszyny z systemem Linux w chmurze Azure z systemem innym niż także można dołączać do usługi Konfiguracja DSC automatyzacji Azure, jak długo mają połączenia wychodzące z Internetem za pośrednictwem kilku prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="52b10-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="52b10-160">Upewnij się, najnowsza wersja [PowerShell konfiguracji żądanego stanu dla systemu Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) jest zainstalowany na komputerach, do których chcesz dołączyć do usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="52b10-161">Jeśli [ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) liter użycia i chcesz dołączyć maszyn takie że **zarówno** ściąganie danych z i raporty do usługi Konfiguracja DSC automatyzacji Azure:</span><span class="sxs-lookup"><span data-stu-id="52b10-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="52b10-162">Na każdej maszynie systemu Linux, aby rozpocząć korzystanie z usługi Konfiguracja DSC automatyzacji Azure Aby dołączyć przy użyciu ustawień domyślnych programu PowerShell DSC lokalny program Configuration Manager, użyj Register.py:</span><span class="sxs-lookup"><span data-stu-id="52b10-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="52b10-163">Aby znaleźć klucz rejestracji i adresu URL rejestracji dla Twojego konta automatyzacji, zobacz [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="52b10-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="52b10-164">Jeśli ustawienia domyślne programu Configuration Manager lokalnego DSC środowiska PowerShell **czy** **nie** dopasowania sieci przypadek użycia, lub chcesz dołączyć maszyn, tak aby tylko raport, aby konfiguracja DSC automatyzacji Azure, ale zrobić nie ściągania konfiguracji lub moduły programu PowerShell z niego, należy wykonać kroki od 3 do 6.</span><span class="sxs-lookup"><span data-stu-id="52b10-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="52b10-165">W przeciwnym razie bezpośrednio przejść do kroku 6.</span><span class="sxs-lookup"><span data-stu-id="52b10-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="52b10-166">Postępuj zgodnie z instrukcjami w [ **metaconfigurations generowania DSC** ](#generating-dsc-metaconfigurations) sekcji poniżej, aby wygenerować folderu zawierającego potrzebne metaconfigurations DSC.</span><span class="sxs-lookup"><span data-stu-id="52b10-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="52b10-167">Na maszynach, które chcesz dołączyć zdalnie Zastosuj metakonfigurację DSC programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="52b10-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="52b10-168">To polecenie jest uruchamiane maszyny musi mieć najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52b10-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="52b10-169">Jeśli nie można zastosować metaconfigurations DSC środowiska PowerShell zdalnie, dla każdej maszyny Linux do dołączenia, skopiuj metakonfigurację odpowiadającego danej maszynie z folderu w kroku 5 na komputerze systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="52b10-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="52b10-170">Następnie wywołaj `SetDscLocalConfigurationManager.py` lokalnie na każdym komputerze z systemem Linux których chcesz dołączyć do usługi Konfiguracja DSC automatyzacji Azure:</span><span class="sxs-lookup"><span data-stu-id="52b10-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="52b10-171">Za pomocą portalu Azure lub poleceń cmdlet, sprawdź, czy maszyny do dołączenia teraz wyświetlane jako węzły DSC zarejestrowana na koncie usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="52b10-172">Trwa generowanie metaconfigurations DSC</span><span class="sxs-lookup"><span data-stu-id="52b10-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="52b10-173">Można tu dodać dowolnego komputera do usługi Konfiguracja DSC automatyzacji Azure, [metakonfigurację DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) mogą być generowane, gdy stosowane, informuje DSC agenta na komputerze ściąganie danych z i/lub raportować do usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="52b10-174">Metaconfigurations DSC dla konfiguracji DSC automatyzacji Azure mogą być generowane przy użyciu konfiguracji DSC środowiska PowerShell lub polecenia cmdlet programu PowerShell automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="52b10-175">DSC metaconfigurations zawierają kluczy tajnych potrzebne do dołączenia komputera do automatyzacji konto do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="52b10-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="52b10-176">Upewnij się, że odpowiednio chronić żadnych metaconfigurations DSC utworzone, lub usuń je po użyciu.</span><span class="sxs-lookup"><span data-stu-id="52b10-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="52b10-177">Za pomocą konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="52b10-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="52b10-178">Otwórz program PowerShell ISE z uprawnieniami administratora na maszynie w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="52b10-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="52b10-179">Komputer musi mieć najnowszą wersję [platformy WMF 5](http://aka.ms/wmf5latest) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52b10-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="52b10-180">Skopiuj poniższy skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="52b10-180">Copy the following script locally.</span></span> <span data-ttu-id="52b10-181">Ten skrypt zawiera konfiguracji DSC środowiska PowerShell do tworzenia metaconfigurations i polecenie, aby rozpocząć poza tworzenia metakonfigurację.</span><span class="sxs-lookup"><span data-stu-id="52b10-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
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

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="52b10-182">Wprowadź klucz rejestracji i adres URL dla konta automatyzacji, jak również nazwy maszyny do dołączenia.</span><span class="sxs-lookup"><span data-stu-id="52b10-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="52b10-183">Wszystkie inne parametry są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="52b10-183">All other parameters are optional.</span></span> <span data-ttu-id="52b10-184">Aby znaleźć klucz rejestracji i adresu URL rejestracji dla Twojego konta automatyzacji, zobacz [ **Secure rejestracji** ](#secure-registration) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="52b10-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="52b10-185">Maszyny zgłoszenia DSC informacje o stanie do usługi Konfiguracja DSC automatyzacji Azure, ale nie ściągania konfiguracji lub moduły programu PowerShell, ustawić **ReportOnly** parametru na wartość true.</span><span class="sxs-lookup"><span data-stu-id="52b10-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="52b10-186">Uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="52b10-186">Run the script.</span></span> <span data-ttu-id="52b10-187">Teraz powinno istnieć folder o nazwie **DscMetaConfigs** w katalogu roboczym zawierający metaconfigurations DSC środowiska PowerShell dla maszyn dołączyć (jako administrator):</span><span class="sxs-lookup"><span data-stu-id="52b10-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="52b10-188">Za pomocą poleceń cmdlet usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="52b10-189">Jeśli ustawienia domyślne programu PowerShell DSC lokalny program Configuration Manager są zgodne z przypadek użycia, i chcesz dołączyć maszyn tak, aby mogli zarówno ściąganie danych z i raporty do usługi Konfiguracja DSC automatyzacji Azure, poleceń cmdlet usługi Automatyzacja Azure umożliwiają uproszczony generowania metaconfigurations DSC potrzebne:</span><span class="sxs-lookup"><span data-stu-id="52b10-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="52b10-190">Otwórz konsolę lub środowisko ISE programu PowerShell jako administrator na maszynie w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="52b10-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="52b10-191">Połącz przy użyciu usługi Azure Resource Manager **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="52b10-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="52b10-192">Pobierz metaconfigurations DSC środowiska PowerShell dla maszyn, które mają do dołączenia z konta automatyzacji, do której chcesz dodać węzły:</span><span class="sxs-lookup"><span data-stu-id="52b10-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="52b10-193">Teraz powinno istnieć folder o nazwie ***DscMetaConfigs***, zawierający metaconfigurations DSC środowiska PowerShell dla maszyn dołączyć (jako administrator):</span><span class="sxs-lookup"><span data-stu-id="52b10-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="52b10-194">Bezpieczne rejestracji</span><span class="sxs-lookup"><span data-stu-id="52b10-194">Secure registration</span></span>

<span data-ttu-id="52b10-195">Maszyny można bezpiecznie dołączyć do konta usługi Automatyzacja Azure za pośrednictwem protokołu rejestracji platformy WMF 5 DSC, dzięki czemu węzła DSC do uwierzytelniania na serwerze ściągania V2 DSC programu PowerShell lub serwer raportowania (w tym konfiguracja DSC automatyzacji Azure).</span><span class="sxs-lookup"><span data-stu-id="52b10-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="52b10-196">Rejestruje węzła do serwera w **adresu URL rejestracji**, uwierzytelniania przy użyciu **klucz rejestracji**.</span><span class="sxs-lookup"><span data-stu-id="52b10-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="52b10-197">Podczas rejestracji, węzła DSC i serwera ściągania usługi Konfiguracja DSC/raportowania negocjowania unikatowy certyfikat dla tego węzła na potrzeby uwierzytelniania serwera po rejestracji.</span><span class="sxs-lookup"><span data-stu-id="52b10-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="52b10-198">Dzięki temu węzłów został załadowany z personifikacja jeden inny, na przykład jeśli węzeł zostanie naruszone bezpieczeństwo i zachowuje się złośliwe.</span><span class="sxs-lookup"><span data-stu-id="52b10-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="52b10-199">Po rejestracji klucz rejestracji nie jest używany do uwierzytelniania ponownie i są usuwane z węzła.</span><span class="sxs-lookup"><span data-stu-id="52b10-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="52b10-200">Można uzyskać informacji wymaganych dla protokołu rejestrację DSC z **zarządzanie kluczami** bloku w portalu Azure w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="52b10-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="52b10-201">Otwórz ten blok, klikając ikonę klucza **Essentials** panelu dla konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="52b10-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="52b10-202">Adres URL rejestracji jest pole adresu URL w bloku zarządzanie kluczami.</span><span class="sxs-lookup"><span data-stu-id="52b10-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="52b10-203">Klucz rejestracji jest klucz dostępu podstawowy lub pomocniczy klucz dostępu w bloku zarządzanie kluczami.</span><span class="sxs-lookup"><span data-stu-id="52b10-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="52b10-204">Można użyć albo klucza.</span><span class="sxs-lookup"><span data-stu-id="52b10-204">Either key can be used.</span></span>

<span data-ttu-id="52b10-205">Aby zwiększyć bezpieczeństwo, klucze podstawowe i pomocnicze dostępu konta automatyzacji można ponownie wygenerować w dowolnym momencie (na **zarządzanie kluczami** bloku) aby zapobiec węzła przyszłych rejestracji przy użyciu poprzednich kluczy.</span><span class="sxs-lookup"><span data-stu-id="52b10-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="52b10-206">Rozwiązywanie problemów z dołączania maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="52b10-207">Konfiguracja DSC usługi Automatyzacja Azure pozwala łatwo dołączać maszyny wirtualne systemu Windows Azure dla zarządzania konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="52b10-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="52b10-208">Pod maską rozszerzenia konfiguracji żądanego stanu programu Azure VM służy do rejestrowania maszyny Wirtualnej z usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="52b10-209">Ponieważ rozszerzenia konfiguracji żądanego stanu programu Azure VM uruchamia asynchronicznie, śledzenie postępu i rozwiązywanie problemów z jej wykonanie może być ważne.</span><span class="sxs-lookup"><span data-stu-id="52b10-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="52b10-210">Każda metoda dołączania maszyny Wirtualnej systemu Windows Azure do konfiguracji DSC automatyzacji Azure używający rozszerzenia konfiguracji żądanego stanu programu Azure maszyny Wirtualnej może potrwać do godziny na węzeł, aby wyświetlić się zarejestrować w usłudze Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="52b10-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="52b10-211">Jest to spowodowane instalacji systemu Windows Management Framework 5.0 na maszynie Wirtualnej przez rozszerzenia DSC maszyny Wirtualnej Azure, który jest wymagany do dołączenia do usługi Konfiguracja DSC automatyzacji Azure maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b10-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="52b10-212">Rozwiązywanie problemów i wyświetlanie stanu rozszerzenia konfiguracji żądanego stanu programu Azure maszyny Wirtualnej, w portalu Azure przejdź do maszyny Wirtualnej trwa został załadowany, a następnie kliknij pozycję -> **wszystkie ustawienia** -> **rozszerzenia** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="52b10-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="52b10-213">Aby uzyskać więcej informacji, kliknij **wyświetlić szczegółowy stan**.</span><span class="sxs-lookup"><span data-stu-id="52b10-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="52b10-214">Wygaśnięcie certyfikatu i ponowna rejestracja</span><span class="sxs-lookup"><span data-stu-id="52b10-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="52b10-215">Po zarejestrowaniu komputera jako węzła DSC w konfiguracji DSC automatyzacji Azure istnieją istnieje wiele możliwych przyczyn, dlaczego należy zarejestrować ten węzeł w przyszłości:</span><span class="sxs-lookup"><span data-stu-id="52b10-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="52b10-216">Po zarejestrowaniu każdego węzła automatycznie negocjuje unikatowy certyfikat do uwierzytelniania, która wygasa po roku.</span><span class="sxs-lookup"><span data-stu-id="52b10-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="52b10-217">Obecnie protokołu rejestrację DSC programu PowerShell nie automatycznego odnawiania certyfikatów, po ich wkrótce wygasną, więc należy ponownie zarejestrować węzły po roku.</span><span class="sxs-lookup"><span data-stu-id="52b10-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="52b10-218">Przed ponownie zarejestrować, upewnij się, że każdy węzeł działa system Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="52b10-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="52b10-219">Jeśli certyfikat uwierzytelniania węzła wygaśnie, a węzeł nie jest zarejestrowane, węzeł będzie mogła komunikować się z usługi Automatyzacja Azure i zostaną oznaczone jako "Unresponsive."</span><span class="sxs-lookup"><span data-stu-id="52b10-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="52b10-220">Ponowna rejestracja wykonać 90 dni lub mniejsza od czasu wygaśnięcia certyfikatu lub w dowolnym momencie po czas wygaśnięcia certyfikatu spowoduje powstanie nowego certyfikatu Trwa generowanie i używanie.</span><span class="sxs-lookup"><span data-stu-id="52b10-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="52b10-221">Aby zmienić dowolne [wartości środowiska PowerShell DSC lokalny program Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) które zostały określone podczas początkowej rejestracji węzła, takich jak ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="52b10-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="52b10-222">Obecnie te wartości agenta DSC można zmienić tylko za pośrednictwem ponowna rejestracja.</span><span class="sxs-lookup"><span data-stu-id="52b10-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="52b10-223">Jedynym wyjątkiem jest konfiguracji węzła przypisanej do węzła — można to zmienić w konfiguracji DSC automatyzacji Azure bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="52b10-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="52b10-224">Ponowna rejestracja można wykonać w taki sam sposób, w zarejestrowany węzeł początkowo przy użyciu dowolnej z metod dołączania opisanych w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="52b10-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="52b10-225">Nie trzeba wyrejestrować węzła z usługi Konfiguracja DSC automatyzacji Azure przed ponownie go zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="52b10-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="52b10-226">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="52b10-226">Related Articles</span></span>

* [<span data-ttu-id="52b10-227">Omówienie usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="52b10-228">Polecenia cmdlet systemu Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="52b10-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="52b10-229">Cennik usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="52b10-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
