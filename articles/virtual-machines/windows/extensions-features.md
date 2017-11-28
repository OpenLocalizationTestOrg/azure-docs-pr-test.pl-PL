---
title: Rozszerzenia maszyn wirtualnych i funkcje systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="22c0d-103">Rozszerzenia maszyn wirtualnych i funkcje systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22c0d-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="22c0d-104">Rozszerzenia maszyny wirtualnej platformy Azure są małe aplikacji, które mają po wdrożeniu i automatyzację zadań na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="22c0d-105">Na przykład jeśli maszyna wirtualna wymaga instalacji oprogramowania, ochrony oprogramowania antywirusowego lub Docker konfiguracji, rozszerzenia maszyny Wirtualnej może służyć do wykonania tych zadań.</span><span class="sxs-lookup"><span data-stu-id="22c0d-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="22c0d-106">Rozszerzenia maszyny Wirtualnej platformy Azure można uruchomić przy użyciu wiersza polecenia platformy Azure, programu PowerShell, szablonów usługi Azure Resource Manager i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="22c0d-107">Rozszerzenia mogą powiązany z nowego wdrożenia maszyny wirtualnej lub uruchomienia dowolnego istniejącego systemu.</span><span class="sxs-lookup"><span data-stu-id="22c0d-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="22c0d-108">Ten dokument zawiera omówienie rozszerzeń maszyny wirtualnej, wymagań wstępnych dotyczących używania rozszerzenia maszyny wirtualnej i wskazówki dotyczące sposobu wykrywania, zarządzanie i usuwanie rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="22c0d-109">Ten dokument zawiera informacje uogólniony wielu rozszerzeń maszyny Wirtualnej nie są dostępne, każde z nich potencjalnie unikatowych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="22c0d-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="22c0d-110">Szczegółów dotyczących poszczególnych rozszerzeń można znaleźć w każdy dokument specyficzne dla poszczególnych rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="22c0d-111">Przypadki użycia i przykłady</span><span class="sxs-lookup"><span data-stu-id="22c0d-111">Use cases and samples</span></span>

<span data-ttu-id="22c0d-112">Istnieje wiele różnych rozszerzeń maszyny Wirtualnej platformy Azure, każde z nich określony przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="22c0d-113">Niektóre przykładowe przypadki użycia są:</span><span class="sxs-lookup"><span data-stu-id="22c0d-113">Some example use cases are:</span></span>

- <span data-ttu-id="22c0d-114">Dotyczą konfiguracji środowiska PowerShell żądany stan maszyny wirtualnej za pomocą rozszerzenia usługi Konfiguracja DSC dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="22c0d-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="22c0d-115">Aby uzyskać więcej informacji, zobacz [Azure żądany stan konfiguracji rozszerzenia](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="22c0d-116">Skonfiguruj monitorowanie maszyny wirtualnej przy użyciu rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22c0d-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="22c0d-117">Aby uzyskać więcej informacji, zobacz [łączenie maszyn wirtualnych platformy Azure do analizy dzienników](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="22c0d-118">Skonfiguruj Monitorowanie infrastruktury platformy Azure z rozszerzeniem Datadog.</span><span class="sxs-lookup"><span data-stu-id="22c0d-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="22c0d-119">Aby uzyskać więcej informacji, zobacz [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="22c0d-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="22c0d-120">Skonfiguruj maszynę wirtualną platformy Azure przy użyciu Chef.</span><span class="sxs-lookup"><span data-stu-id="22c0d-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="22c0d-121">Aby uzyskać więcej informacji, zobacz [automatyzacji Azure wdrożenia maszyny wirtualnej z Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="22c0d-122">Oprócz rozszerzenia procesu rozszerzenia niestandardowego skryptu jest dostępna dla maszyn wirtualnych w systemach Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="22c0d-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="22c0d-123">Rozszerzenia niestandardowego skryptu dla systemu Windows umożliwia dowolny skrypt programu PowerShell do uruchamiania na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="22c0d-124">Jest to przydatne podczas projektowania wdrożeń platformy Azure, które wymagają konfiguracji oprócz zapewniają jakie natywnego narzędzia Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="22c0d-125">Aby uzyskać więcej informacji, zobacz [rozszerzenie skryptu niestandardowego maszyny Wirtualnej systemu Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="22c0d-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22c0d-126">Prerequisites</span></span>

<span data-ttu-id="22c0d-127">Każde rozszerzenie maszyny wirtualnej może mieć własny zestaw wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="22c0d-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="22c0d-128">Dla wystąpienia rozszerzenia maszyny Wirtualnej platformy Docker jest wymaganiem wstępnym obsługiwanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="22c0d-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="22c0d-129">Wymagania dotyczące poszczególnych rozszerzeń są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="22c0d-130">Agent maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22c0d-130">Azure VM agent</span></span>
<span data-ttu-id="22c0d-131">Agent maszyny Wirtualnej platformy Azure zarządza interakcji między maszyny wirtualnej platformy Azure i kontroler sieci szkieletowej Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="22c0d-132">Agent maszyny Wirtualnej jest odpowiedzialny za dużo aspekty funkcjonalne, wdrażania i zarządzania maszynami wirtualnymi platformy Azure, łącznie z rozszerzeniami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="22c0d-133">Agent maszyny Wirtualnej platformy Azure jest preinstalowany na portalu Azure Marketplace obrazów i można zainstalować w obsługiwanych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="22c0d-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="22c0d-134">Aby uzyskać informacje dotyczące obsługiwanych systemów operacyjnych i instrukcje dotyczące instalacji, zobacz [agenta maszyny wirtualnej platformy Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="22c0d-135">Odnajdywanie rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22c0d-135">Discover VM extensions</span></span>
<span data-ttu-id="22c0d-136">Wiele różnych rozszerzeń maszyny Wirtualnej są dostępne do użycia z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="22c0d-137">Aby wyświetlić pełną listę, uruchom następujące polecenie z modułu programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22c0d-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="22c0d-138">Upewnij się, że określ żądaną lokalizację po uruchomieniu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="22c0d-139">Uruchom rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22c0d-139">Run VM extensions</span></span>

<span data-ttu-id="22c0d-140">Rozszerzenia maszyny wirtualnej platformy Azure może działać w istniejących maszyn wirtualnych, co jest przydatne, gdy trzeba wprowadzić zmiany w konfiguracji lub Przywróć łączność w przypadku wdrożonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="22c0d-141">Rozszerzenia maszyny Wirtualnej dołączany także wdrażanie szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22c0d-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="22c0d-142">Za pomocą rozszerzeń z szablonami usługi Resource Manager, można włączyć maszyn wirtualnych platformy Azure wdrożyć i skonfigurować bez konieczności interwencji po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="22c0d-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="22c0d-143">Następujących metod można uruchomić rozszerzenia dla istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="22c0d-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22c0d-144">PowerShell</span></span>

<span data-ttu-id="22c0d-145">Istnieje kilka poleceń programu PowerShell do uruchamiania poszczególnych rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="22c0d-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="22c0d-146">Umożliwia wyświetlenie listy, uruchom następujące polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22c0d-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="22c0d-147">Zapewnia to dane wyjściowe podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="22c0d-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="22c0d-148">W poniższym przykładzie użyto rozszerzenia niestandardowego skryptu do pobrania skryptu z repozytorium GitHub na docelowej maszynie wirtualnej, a następnie uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="22c0d-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="22c0d-149">Aby uzyskać więcej informacji dotyczących rozszerzenia niestandardowego skryptu, zobacz [Omówienie rozszerzenia niestandardowego skryptu](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="22c0d-150">W tym przykładzie rozszerzenia dostępu do maszyny Wirtualnej służy do resetowania hasła administracyjnego maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="22c0d-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="22c0d-151">Aby uzyskać więcej informacji dotyczących rozszerzenia dostępu do maszyny Wirtualnej, zobacz [usługi pulpitu zdalnego resetowania na maszynie wirtualnej Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="22c0d-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="22c0d-152">`Set-AzureRmVMExtension` Polecenia można uruchomić wszystkie rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="22c0d-153">Aby uzyskać więcej informacji, zobacz [odwołania zestawu AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="22c0d-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="22c0d-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="22c0d-154">Azure portal</span></span>

<span data-ttu-id="22c0d-155">Rozszerzenia maszyny Wirtualnej może odnosić się do istniejącej maszyny wirtualnej za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="22c0d-156">Aby to zrobić, wybierz maszynę wirtualną, aby użyć, wybierz **rozszerzenia**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="22c0d-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="22c0d-157">Zapewnia to listę dostępnych rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="22c0d-157">This provides a list of available extensions.</span></span> <span data-ttu-id="22c0d-158">Wybierz jedną, mają i postępuj zgodnie z instrukcjami kreatora.</span><span class="sxs-lookup"><span data-stu-id="22c0d-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="22c0d-159">Na poniższej ilustracji przedstawiono instalacja rozszerzenia Microsoft Antimalware z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Zainstaluj rozszerzenie ochrony przed złośliwym oprogramowaniem](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="22c0d-161">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22c0d-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="22c0d-162">Rozszerzenia maszyny Wirtualnej można dodać do szablonu usługi Azure Resource Manager i wykonywane przy użyciu wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="22c0d-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="22c0d-163">Wdrażanie rozszerzeń przy użyciu szablonu jest przydatne w przypadku tworzenia wdrożeń platformy Azure w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="22c0d-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="22c0d-164">Na przykład następujący kod JSON jest pobierana z szablonem usługi Resource Manager, który wdraża zestaw maszyn wirtualnych z równoważeniem obciążenia i bazy danych Azure SQL, a następnie instaluje aplikację .NET Core na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="22c0d-165">Rozszerzenia maszyny Wirtualnej zapewnia obsługę instalacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="22c0d-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="22c0d-166">Aby uzyskać więcej informacji, zobacz [pełne szablonu usługi Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="22c0d-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="22c0d-167">Aby uzyskać więcej informacji, zobacz [szablony Authoring Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="22c0d-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="22c0d-168">Zabezpieczanie danych rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22c0d-168">Secure VM extension data</span></span>

<span data-ttu-id="22c0d-169">Jeśli korzystasz z rozszerzenia maszyny Wirtualnej, może być konieczne jest stosowanie poufne informacje, takie jak poświadczeń, nazwy konta magazynu i klucze dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="22c0d-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="22c0d-170">Wiele rozszerzeń maszyny Wirtualnej obejmują konfiguracji chronionych danych i tylko odszyfrowującego wewnątrz docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="22c0d-171">Każde rozszerzenie ma używającym w dokumentacji konkretnego rozszerzenia schematu określonej konfiguracji chronionych.</span><span class="sxs-lookup"><span data-stu-id="22c0d-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="22c0d-172">W poniższym przykładzie przedstawiono wystąpienia rozszerzenia niestandardowego skryptu dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="22c0d-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="22c0d-173">Zwróć uwagę, że polecenie do wykonania zawiera zestaw poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="22c0d-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="22c0d-174">W tym przykładzie wykonanie polecenia nie będą szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="22c0d-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="22c0d-175">Bezpieczny ciąg wykonywania przez przeniesienie **polecenie do wykonania** właściwości **chronione** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="22c0d-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="22c0d-176">Rozwiązywanie problemów z rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22c0d-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="22c0d-177">Każde rozszerzenie maszyny Wirtualnej może być określone kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="22c0d-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="22c0d-178">Na przykład podczas korzystania z rozszerzenia niestandardowego skryptu, szczegóły wykonywania skryptu można znaleźć lokalnie na maszynie wirtualnej, na którym uruchomiono rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="22c0d-179">Wszystkie kroki rozwiązywania problemów specyficzne dla rozszerzenia są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="22c0d-180">Następujące kroki dotyczą wszystkich rozszerzeń maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="22c0d-181">Wyświetl stan rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="22c0d-181">View extension status</span></span>

<span data-ttu-id="22c0d-182">Po uruchomieniu rozszerzenie maszyny wirtualnej na maszynie wirtualnej, użyj następującego polecenia programu PowerShell, aby zwrócić stan rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="22c0d-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="22c0d-183">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="22c0d-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="22c0d-184">`Name` Parametr przyjmuje Nazwa rozszerzenia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="22c0d-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="22c0d-185">Dane wyjściowe wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="22c0d-185">The output looks like the following:</span></span>

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

<span data-ttu-id="22c0d-186">Stan wykonania rozszerzenia można znaleźć w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="22c0d-187">Aby wyświetlić stan rozszerzenia, wybierz maszynę wirtualną, wybierz polecenie **rozszerzenia**i wybierz żądane rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="22c0d-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="22c0d-188">Uruchom ponownie rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22c0d-188">Rerun VM extensions</span></span>

<span data-ttu-id="22c0d-189">Może to być przypadkach, w których można ponownie uruchomić wymaga rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22c0d-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="22c0d-190">Można to zrobić, usuwając rozszerzenie, a następnie ponowne uruchomienie rozszerzenia metodą wykonywania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22c0d-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="22c0d-191">Aby usunąć rozszerzenie, uruchom następujące polecenie z modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22c0d-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="22c0d-192">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="22c0d-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="22c0d-193">Rozszerzenie może zostać także usunięty przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22c0d-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="22c0d-194">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="22c0d-194">To do so:</span></span>

1. <span data-ttu-id="22c0d-195">Wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="22c0d-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="22c0d-196">Wybierz **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="22c0d-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="22c0d-197">Wybierz żądane rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="22c0d-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="22c0d-198">Wybierz **odinstalować**.</span><span class="sxs-lookup"><span data-stu-id="22c0d-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="22c0d-199">Typowe odwołanie do rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="22c0d-199">Common VM extensions reference</span></span>
| <span data-ttu-id="22c0d-200">Nazwa rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="22c0d-200">Extension name</span></span> | <span data-ttu-id="22c0d-201">Opis</span><span class="sxs-lookup"><span data-stu-id="22c0d-201">Description</span></span> | <span data-ttu-id="22c0d-202">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="22c0d-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22c0d-203">Niestandardowe rozszerzenie skryptu dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22c0d-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="22c0d-204">Uruchom skrypty przed maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22c0d-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="22c0d-205">Niestandardowe rozszerzenie skryptu dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22c0d-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="22c0d-206">Rozszerzenia konfiguracji DSC dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22c0d-206">DSC Extension for Windows</span></span> |<span data-ttu-id="22c0d-207">Rozszerzenia DSC (konfiguracji żądanego stanu) programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="22c0d-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="22c0d-208">Rozszerzenia konfiguracji DSC dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22c0d-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="22c0d-209">Rozszerzenie Diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="22c0d-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="22c0d-210">Zarządzanie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="22c0d-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="22c0d-211">Rozszerzenie diagnostyki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22c0d-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="22c0d-212">Rozszerzenia dostępu do maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22c0d-212">Azure VM Access Extension</span></span> |<span data-ttu-id="22c0d-213">Zarządzaj użytkownikami i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="22c0d-213">Manage users and credentials</span></span> |[<span data-ttu-id="22c0d-214">Rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="22c0d-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
