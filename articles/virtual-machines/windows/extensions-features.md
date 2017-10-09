---
title: "aaaVirtual komputera rozszerzeń i funkcji systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie rozszerzenia są dostępne dla maszyn wirtualnych platformy Azure, pogrupowane według co ich Podaj puli zasobów i zwiększyć."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="35bd4-103">Rozszerzenia maszyn wirtualnych i funkcje systemu Windows</span><span class="sxs-lookup"><span data-stu-id="35bd4-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="35bd4-104">Rozszerzenia maszyny wirtualnej platformy Azure są małe aplikacji, które mają po wdrożeniu i automatyzację zadań na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="35bd4-105">Na przykład, jeśli maszyna wirtualna wymaga instalacji oprogramowania, ochrony oprogramowania antywirusowego lub Docker konfiguracji, rozszerzenia maszyny Wirtualnej mogą być używane toocomplete tych zadań.</span><span class="sxs-lookup"><span data-stu-id="35bd4-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="35bd4-106">Azure rozszerzeń maszyny Wirtualnej może być uruchamiany przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, szablony usługi Azure Resource Manager i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="35bd4-107">Rozszerzenia mogą powiązany z nowego wdrożenia maszyny wirtualnej lub uruchomienia dowolnego istniejącego systemu.</span><span class="sxs-lookup"><span data-stu-id="35bd4-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="35bd4-108">Ten dokument zawiera omówienie rozszerzeń maszyny wirtualnej, wymagań wstępnych dotyczących używania rozszerzenia maszyny wirtualnej i wskazówki na sposób toodetect, zarządzania i usunąć rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="35bd4-109">Ten dokument zawiera informacje uogólniony wielu rozszerzeń maszyny Wirtualnej nie są dostępne, każde z nich potencjalnie unikatowych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="35bd4-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="35bd4-110">Rozszerzenie szczegółowe znajdują się w poszczególnych rozszerzeń poszczególnych toohello określonego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="35bd4-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="35bd4-111">Przypadki użycia i przykłady</span><span class="sxs-lookup"><span data-stu-id="35bd4-111">Use cases and samples</span></span>

<span data-ttu-id="35bd4-112">Istnieje wiele różnych rozszerzeń maszyny Wirtualnej platformy Azure, każde z nich określony przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="35bd4-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="35bd4-113">Niektóre przykładowe przypadki użycia są:</span><span class="sxs-lookup"><span data-stu-id="35bd4-113">Some example use cases are:</span></span>

- <span data-ttu-id="35bd4-114">Stosowanie programu PowerShell żądany stan konfiguracji tooa maszyny wirtualnej za pomocą rozszerzenia hello DSC dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="35bd4-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="35bd4-115">Aby uzyskać więcej informacji, zobacz [Azure żądany stan konfiguracji rozszerzenia](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="35bd4-116">Skonfiguruj monitorowanie za pomocą rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="35bd4-117">Aby uzyskać więcej informacji, zobacz [tooLog maszyny wirtualne Azure połączyć Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="35bd4-118">Skonfiguruj Monitorowanie infrastruktury platformy Azure z hello Datadog rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="35bd4-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="35bd4-119">Aby uzyskać więcej informacji, zobacz hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="35bd4-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="35bd4-120">Skonfiguruj maszynę wirtualną platformy Azure przy użyciu Chef.</span><span class="sxs-lookup"><span data-stu-id="35bd4-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="35bd4-121">Aby uzyskać więcej informacji, zobacz [automatyzacji Azure wdrożenia maszyny wirtualnej z Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="35bd4-122">Ponadto rozszerzenia tooprocess rozszerzenia niestandardowego skryptu dostępnej dla maszyn wirtualnych w systemach Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="35bd4-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="35bd4-123">Witaj rozszerzenia niestandardowego skryptu dla systemu Windows umożliwia żadnych toobe skrypt programu PowerShell uruchomić na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="35bd4-124">Jest to przydatne podczas projektowania wdrożeń platformy Azure, które wymagają konfiguracji oprócz zapewniają jakie natywnego narzędzia Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="35bd4-125">Aby uzyskać więcej informacji, zobacz [rozszerzenie skryptu niestandardowego maszyny Wirtualnej systemu Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="35bd4-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35bd4-126">Prerequisites</span></span>

<span data-ttu-id="35bd4-127">Każde rozszerzenie maszyny wirtualnej może mieć własny zestaw wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="35bd4-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="35bd4-128">Na przykład hello rozszerzenia maszyny Wirtualnej platformy Docker ma wymagań wstępnych obsługiwanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="35bd4-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="35bd4-129">Wymagania dotyczące poszczególnych rozszerzeń są szczegółowo opisane w dokumentacji konkretnego rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="35bd4-130">Agent maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35bd4-130">Azure VM agent</span></span>
<span data-ttu-id="35bd4-131">agent maszyny Wirtualnej Azure Hello zarządza interakcji między maszyny wirtualnej platformy Azure i hello kontrolera sieci szkieletowej Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="35bd4-132">agent maszyny Wirtualnej Hello jest odpowiedzialny za dużo aspekty funkcjonalne, wdrażania i zarządzania maszynami wirtualnymi platformy Azure, łącznie z rozszerzeniami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="35bd4-133">agent maszyny Wirtualnej Azure Hello jest preinstalowany na portalu Azure Marketplace obrazów i można zainstalować w obsługiwanych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="35bd4-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="35bd4-134">Aby uzyskać informacje dotyczące obsługiwanych systemów operacyjnych i instrukcje dotyczące instalacji, zobacz [agenta maszyny wirtualnej platformy Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="35bd4-135">Odnajdywanie rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bd4-135">Discover VM extensions</span></span>
<span data-ttu-id="35bd4-136">Wiele różnych rozszerzeń maszyny Wirtualnej są dostępne do użycia z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="35bd4-137">toosee pełną listę, uruchom następujące polecenie z modułu programu PowerShell usługi Azure Resource Manager hello hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="35bd4-138">Upewnij się, że lokalizacja hello potrzeby toospecify po uruchomieniu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="35bd4-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="35bd4-139">Uruchom rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bd4-139">Run VM extensions</span></span>

<span data-ttu-id="35bd4-140">Rozszerzenia maszyny wirtualnej platformy Azure może działać w istniejących maszyn wirtualnych, które jest przydatne, gdy potrzebne zmiany w konfiguracji toomake lub Przywróć łączność w przypadku wdrożonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="35bd4-141">Rozszerzenia maszyny Wirtualnej dołączany także wdrażanie szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35bd4-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="35bd4-142">Za pomocą rozszerzeń z szablonami usługi Resource Manager, można włączyć toobe maszyn wirtualnych platformy Azure, wdrożyć i skonfigurować bez potrzeby interwencji po wdrożeniu hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="35bd4-143">Hello następujące metody mogą być używane toorun rozszerzenie dla istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="35bd4-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35bd4-144">PowerShell</span></span>

<span data-ttu-id="35bd4-145">Istnieje kilka poleceń programu PowerShell do uruchamiania poszczególnych rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="35bd4-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="35bd4-146">toosee listy, uruchom następujące polecenia programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="35bd4-147">Zapewnia to dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="35bd4-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="35bd4-148">Witaj poniższy przykład używa toodownload rozszerzenia niestandardowego skryptu hello skryptu z repozytorium GitHub na powitania docelowej maszyny wirtualnej, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="35bd4-149">Aby uzyskać więcej informacji na powitania rozszerzenia niestandardowego skryptu, zobacz [Omówienie rozszerzenia niestandardowego skryptu](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="35bd4-150">W tym przykładzie hello rozszerzenia dostępu do maszyny Wirtualnej jest używane tooreset hello hasło administratora maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="35bd4-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="35bd4-151">Aby uzyskać więcej informacji na powitania rozszerzenia dostępu do maszyny Wirtualnej, zobacz [usługi pulpitu zdalnego resetowania na maszynie wirtualnej Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="35bd4-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="35bd4-152">Witaj `Set-AzureRmVMExtension` polecenie może być używane toostart wszystkie rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="35bd4-153">Aby uzyskać więcej informacji, zobacz hello [odwołania zestawu AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="35bd4-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="35bd4-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="35bd4-154">Azure portal</span></span>

<span data-ttu-id="35bd4-155">Rozszerzenia maszyny Wirtualnej może być zastosowane tooan istniejącej maszyny wirtualnej za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="35bd4-156">toodo tak, wybierz maszynę wirtualną hello mają toouse, wybierz **rozszerzenia**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="35bd4-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="35bd4-157">Zapewnia to listę dostępnych rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="35bd4-157">This provides a list of available extensions.</span></span> <span data-ttu-id="35bd4-158">Wybierz hello mają i wykonaj kroki powitania w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="35bd4-159">Witaj poniższy obraz przedstawia hello instalacji hello rozszerzenia Microsoft Antimalware hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Zainstaluj rozszerzenie ochrony przed złośliwym oprogramowaniem](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="35bd4-161">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35bd4-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="35bd4-162">Rozszerzeń maszyny Wirtualnej może być dodany tooan szablonu usługi Azure Resource Manager i wykonany przy użyciu wdrożenia hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="35bd4-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="35bd4-163">Wdrażanie rozszerzeń przy użyciu szablonu jest przydatne w przypadku tworzenia wdrożeń platformy Azure w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="35bd4-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="35bd4-164">Na przykład powitalne następujące JSON jest pobierana z szablonem usługi Resource Manager, który wdraża zestaw maszyn wirtualnych z równoważeniem obciążenia i bazy danych Azure SQL, a następnie instaluje aplikację .NET Core na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="35bd4-165">Instalacja oprogramowania hello odpowiada on za Hello rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="35bd4-166">Aby uzyskać więcej informacji, zobacz hello [pełne szablonu usługi Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="35bd4-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="35bd4-167">Aby uzyskać więcej informacji, zobacz [szablony Authoring Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="35bd4-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="35bd4-168">Zabezpieczanie danych rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bd4-168">Secure VM extension data</span></span>

<span data-ttu-id="35bd4-169">Jeśli korzystasz z rozszerzenia maszyny Wirtualnej, może być konieczne tooinclude poufne informacje, takie jak poświadczeń, nazwy konta magazynu i klucze dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="35bd4-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="35bd4-170">Wiele rozszerzeń maszyny Wirtualnej obejmują konfiguracji chronionych danych i tylko odszyfrowującego wewnątrz hello docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="35bd4-171">Każde rozszerzenie ma używającym w dokumentacji konkretnego rozszerzenia schematu określonej konfiguracji chronionych.</span><span class="sxs-lookup"><span data-stu-id="35bd4-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="35bd4-172">Witaj poniższy przykład przedstawia wystąpienie hello rozszerzenia niestandardowego skryptu dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="35bd4-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="35bd4-173">Należy zauważyć, że tego tooexecute polecenia hello zawiera zestaw poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="35bd4-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="35bd4-174">W tym przykładzie hello tooexecute polecenia nie będą szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="35bd4-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="35bd4-175">Bezpieczny ciąg wykonywania hello przenosząc hello **tooexecute polecenia** toohello właściwości **chronione** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="35bd4-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="35bd4-176">Rozwiązywanie problemów z rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bd4-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="35bd4-177">Każde rozszerzenie maszyny Wirtualnej może być określone kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="35bd4-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="35bd4-178">Na przykład podczas korzystania z rozszerzenia niestandardowego skryptu hello, skryptu wykonywania szczegóły można znaleźć lokalnie na maszynie wirtualnej hello, na którym uruchomiono hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="35bd4-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="35bd4-179">Wszystkie kroki rozwiązywania problemów specyficzne dla rozszerzenia są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="35bd4-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="35bd4-180">następujące kroki rozwiązywania problemów Hello mają zastosowanie tooall rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bd4-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="35bd4-181">Wyświetl stan rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="35bd4-181">View extension status</span></span>

<span data-ttu-id="35bd4-182">Po uruchomieniu rozszerzenie maszyny wirtualnej na maszynie wirtualnej, użyj powitania po stan rozszerzenia tooreturn polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35bd4-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="35bd4-183">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="35bd4-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="35bd4-184">Witaj `Name` Parametr przyjmuje nazwę hello danego rozszerzenia toohello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="35bd4-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="35bd4-185">dane wyjściowe Hello wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="35bd4-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="35bd4-186">Stan wykonania rozszerzenia można znaleźć w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="35bd4-187">Wybierz stan hello tooview rozszerzenia maszyny wirtualnej wybierz hello, **rozszerzenia**, i wybierz hello żądanego rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="35bd4-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="35bd4-188">Uruchom ponownie rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bd4-188">Rerun VM extensions</span></span>

<span data-ttu-id="35bd4-189">Może się zdarzyć, w których toobe, musi mieć rozszerzenie maszyny wirtualnej ponownie.</span><span class="sxs-lookup"><span data-stu-id="35bd4-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="35bd4-190">Można to zrobić, usuwając hello rozszerzenia, a następnie ponowne uruchomienie rozszerzenia hello metodą wykonywania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35bd4-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="35bd4-191">tooremove rozszerzenia, uruchom następujące polecenie z modułu Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="35bd4-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="35bd4-192">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="35bd4-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="35bd4-193">Rozszerzenie może zostać także usunięty przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35bd4-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="35bd4-194">toodo tak:</span><span class="sxs-lookup"><span data-stu-id="35bd4-194">toodo so:</span></span>

1. <span data-ttu-id="35bd4-195">Wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="35bd4-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="35bd4-196">Wybierz **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="35bd4-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="35bd4-197">Wybierz żądaną hello rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="35bd4-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="35bd4-198">Wybierz **odinstalować**.</span><span class="sxs-lookup"><span data-stu-id="35bd4-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="35bd4-199">Typowe odwołanie do rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bd4-199">Common VM extensions reference</span></span>
| <span data-ttu-id="35bd4-200">Nazwa rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="35bd4-200">Extension name</span></span> | <span data-ttu-id="35bd4-201">Opis</span><span class="sxs-lookup"><span data-stu-id="35bd4-201">Description</span></span> | <span data-ttu-id="35bd4-202">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="35bd4-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35bd4-203">Niestandardowe rozszerzenie skryptu dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="35bd4-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="35bd4-204">Uruchom skrypty przed maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35bd4-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="35bd4-205">Niestandardowe rozszerzenie skryptu dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="35bd4-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="35bd4-206">Rozszerzenia konfiguracji DSC dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="35bd4-206">DSC Extension for Windows</span></span> |<span data-ttu-id="35bd4-207">Rozszerzenia DSC (konfiguracji żądanego stanu) programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="35bd4-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="35bd4-208">Rozszerzenia konfiguracji DSC dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="35bd4-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="35bd4-209">Rozszerzenie Diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="35bd4-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="35bd4-210">Zarządzanie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="35bd4-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="35bd4-211">Rozszerzenie diagnostyki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35bd4-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="35bd4-212">Rozszerzenia dostępu do maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35bd4-212">Azure VM Access Extension</span></span> |<span data-ttu-id="35bd4-213">Zarządzaj użytkownikami i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="35bd4-213">Manage users and credentials</span></span> |[<span data-ttu-id="35bd4-214">Rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="35bd4-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
