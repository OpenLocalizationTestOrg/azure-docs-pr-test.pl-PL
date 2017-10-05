---
title: Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jakie rozszerzenia są dostępne dla maszyn wirtualnych platformy Azure, pogrupowane według co ich Podaj puli zasobów i zwiększyć."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 8a5b39351f665c51ae7d83f755329e54ff3cf786
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="77806-103">Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="77806-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="77806-104">Rozszerzenia maszyny wirtualnej platformy Azure są małe aplikacji, które mają po wdrożeniu i automatyzację zadań na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="77806-105">Na przykład jeśli maszyna wirtualna wymaga instalacji oprogramowania, ochrony oprogramowania antywirusowego lub Docker konfiguracji, rozszerzenia maszyny Wirtualnej może służyć do wykonania tych zadań.</span><span class="sxs-lookup"><span data-stu-id="77806-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="77806-106">Rozszerzenia maszyny Wirtualnej platformy Azure mogą być uruchamiane przy użyciu wiersza polecenia platformy Azure, programu PowerShell, szablonów usługi Azure Resource Manager i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="77806-107">Rozszerzenia mogą być powiązane z nowego wdrożenia maszyny wirtualnej lub uruchomienia dowolnego istniejącego systemu.</span><span class="sxs-lookup"><span data-stu-id="77806-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="77806-108">Ten dokument zawiera omówienie rozszerzeń maszyny Wirtualnej, wymagań wstępnych dotyczących używania rozszerzenia maszyny Wirtualnej platformy Azure i instrukcje dotyczące wykrywania, zarządzanie i usuwanie rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span></span> <span data-ttu-id="77806-109">Ten dokument zawiera informacje uogólniony wielu rozszerzeń maszyny Wirtualnej nie są dostępne, każde z nich potencjalnie unikatowych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="77806-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="77806-110">Szczegółów dotyczących poszczególnych rozszerzeń można znaleźć w każdy dokument specyficzne dla poszczególnych rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="77806-111">Przypadki użycia i przykłady</span><span class="sxs-lookup"><span data-stu-id="77806-111">Use cases and samples</span></span>

<span data-ttu-id="77806-112">Dostępnych jest kilka różnych rozszerzeń maszyny Wirtualnej platformy Azure, każde z nich określony przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="77806-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="77806-113">Przykłady to:</span><span class="sxs-lookup"><span data-stu-id="77806-113">Some examples are:</span></span>

- <span data-ttu-id="77806-114">Zastosuj PowerShell żądany stan konfiguracje dla maszyny wirtualnej dla systemu Linux przy użyciu rozszerzenia usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="77806-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span></span> <span data-ttu-id="77806-115">Aby uzyskać więcej informacji, zobacz [Azure żądany stan konfiguracji rozszerzenia](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="77806-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="77806-116">Konfigurowanie monitorowania maszyny wirtualnej z rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77806-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="77806-117">Aby uzyskać więcej informacji, zobacz [jak monitorować Maszynę wirtualną systemu Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="77806-117">For more information, see [How to monitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="77806-118">Skonfiguruj Monitorowanie infrastruktury platformy Azure z rozszerzeniem Datadog.</span><span class="sxs-lookup"><span data-stu-id="77806-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="77806-119">Aby uzyskać więcej informacji, zobacz [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="77806-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="77806-120">Konfigurowanie hosta Docker na maszynie wirtualnej platformy Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="77806-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span></span> <span data-ttu-id="77806-121">Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyny Wirtualnej platformy Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="77806-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="77806-122">Oprócz rozszerzenia procesu rozszerzenia niestandardowego skryptu jest dostępna dla maszyn wirtualnych w systemach Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="77806-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="77806-123">Rozszerzenia niestandardowego skryptu dla systemu Linux umożliwia dowolny skrypt Bash do uruchamiania na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span></span> <span data-ttu-id="77806-124">Niestandardowe skrypty są przydatne w przypadku projektowania wdrożeń platformy Azure, które wymagają konfiguracji oprócz zapewniają jakie natywnego narzędzia Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="77806-125">Aby uzyskać więcej informacji, zobacz [rozszerzenie skryptu niestandardowego maszyny Wirtualnej systemu Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="77806-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="77806-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77806-126">Prerequisites</span></span>

<span data-ttu-id="77806-127">Każde rozszerzenie maszyny wirtualnej może mieć własny zestaw wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="77806-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="77806-128">Dla wystąpienia rozszerzenia maszyny Wirtualnej platformy Docker jest wymaganiem wstępnym obsługiwanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="77806-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="77806-129">Wymagania dotyczące poszczególnych rozszerzeń są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="77806-130">Agent maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77806-130">Azure VM agent</span></span>

<span data-ttu-id="77806-131">Agent maszyny Wirtualnej platformy Azure zarządza interakcje między maszyny wirtualnej platformy Azure i kontroler sieci szkieletowej Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-131">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="77806-132">Agent maszyny Wirtualnej jest odpowiedzialny za dużo aspekty funkcjonalne, wdrażania i zarządzania maszynami wirtualnymi platformy Azure, łącznie z rozszerzeniami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="77806-133">Agent maszyny Wirtualnej platformy Azure jest preinstalowany na portalu Azure Marketplace obrazów i można zainstalować ręcznie w obsługiwanych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="77806-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="77806-134">Aby uzyskać informacje dotyczące obsługiwanych systemów operacyjnych i instrukcje dotyczące instalacji, zobacz [agenta maszyny wirtualnej platformy Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="77806-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="77806-135">Odnajdywanie rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-135">Discover VM extensions</span></span>

<span data-ttu-id="77806-136">Wiele różnych rozszerzeń maszyny Wirtualnej są dostępne do użycia z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="77806-137">Aby wyświetlić pełną listę, uruchom następujące polecenie z wiersza polecenia platformy Azure, zastępując lokalizacji przykład wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="77806-137">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="77806-138">Uruchom rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-138">Run VM extensions</span></span>

<span data-ttu-id="77806-139">Rozszerzenia maszyny wirtualnej platformy Azure może działać w istniejących maszyn wirtualnych, które są przydatne, gdy trzeba wprowadzić zmiany w konfiguracji lub Przywróć łączność w przypadku wdrożonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="77806-140">Rozszerzenia maszyny Wirtualnej dołączany także wdrażanie szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77806-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="77806-141">Za pomocą rozszerzeń z szablonami usługi Resource Manager, można wdrożyć i konfigurować bez interwencji po wdrożeniu maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="77806-142">Następujących metod można uruchomić rozszerzenia dla istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-142">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="77806-143">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77806-143">Azure CLI</span></span>

<span data-ttu-id="77806-144">Rozszerzenia maszyny wirtualnej platformy Azure mogą być uruchamiane na istniejącej maszyny wirtualnej za pomocą `az vm extension set` polecenia.</span><span class="sxs-lookup"><span data-stu-id="77806-144">Azure virtual machine extensions can be run against an existing virtual machine by using the `az vm extension set` command.</span></span> <span data-ttu-id="77806-145">W tym przykładzie jest uruchamiana rozszerzenie skryptu niestandardowego dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-145">This example runs the custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="77806-146">Skrypt generuje dane wyjściowe podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="77806-146">The script produces output similar to the following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up the VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="77806-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="77806-147">Azure portal</span></span>

<span data-ttu-id="77806-148">Rozszerzenia maszyny Wirtualnej może odnosić się do istniejącej maszyny wirtualnej za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-148">VM extensions can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="77806-149">Aby to zrobić, wybierz maszynę wirtualną, wybierz **rozszerzenia**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="77806-149">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="77806-150">Wybierz rozszerzenia, z listy dostępnych rozszerzeń i postępuj zgodnie z instrukcjami w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="77806-150">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span></span>

<span data-ttu-id="77806-151">Na poniższej ilustracji przedstawiono instalacja rozszerzenia Linux niestandardowego skryptu z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-151">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span></span>

![Zainstaluj rozszerzenie skryptu niestandardowego](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="77806-153">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="77806-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="77806-154">Rozszerzenia maszyny Wirtualnej można dodać do szablonu usługi Azure Resource Manager i wykonywane przy użyciu wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="77806-154">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="77806-155">Podczas wdrażania rozszerzenia za pomocą szablonu można tworzyć wdrożeń platformy Azure w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="77806-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="77806-156">Na przykład następujący kod JSON jest pobierana z szablonem usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77806-156">For example, the following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="77806-157">Szablon wdraża zestaw maszyn wirtualnych z równoważeniem obciążenia i bazy danych Azure SQL, a następnie instaluje aplikację .NET Core na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-157">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="77806-158">Rozszerzenia maszyny Wirtualnej zapewnia obsługę instalacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="77806-158">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="77806-159">Aby uzyskać więcej informacji, zobacz pełny [szablonu usługi Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="77806-159">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="77806-160">Aby uzyskać więcej informacji, zobacz [szablonów Authoring Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="77806-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="77806-161">Zabezpieczanie danych rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-161">Secure VM extension data</span></span>

<span data-ttu-id="77806-162">Jeśli korzystasz z rozszerzenia maszyny Wirtualnej, może być konieczne jest stosowanie poufne informacje, takie jak poświadczeń, nazwy konta magazynu i klucze dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="77806-162">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="77806-163">Wiele rozszerzeń maszyny Wirtualnej obejmują konfiguracji chronionych danych i tylko odszyfrowującego wewnątrz docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="77806-164">Każde rozszerzenie ma schematu określonej konfiguracji chronionych, a każdy szczegółowo opisano w dokumentacji konkretnego rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="77806-165">W poniższym przykładzie przedstawiono wystąpienia rozszerzenia niestandardowego skryptu dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="77806-165">The following example shows an instance of the Custom Script extension for Linux.</span></span> <span data-ttu-id="77806-166">Zwróć uwagę, że polecenie do wykonania zawiera zestaw poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="77806-166">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="77806-167">W tym przykładzie wykonanie polecenia nie będą szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="77806-167">In this example, the command to execute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="77806-168">Przenoszenie **polecenie do wykonania** właściwości **chronione** konfiguracja zabezpiecza ciąg wykonywania.</span><span class="sxs-lookup"><span data-stu-id="77806-168">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="77806-169">Rozwiązywanie problemów z rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="77806-170">Każde rozszerzenie maszyny Wirtualnej może być rozwiązywania problemów z określonego rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-170">Each VM extension may have troubleshooting steps specific to the extension.</span></span> <span data-ttu-id="77806-171">Na przykład jeśli używasz rozszerzenia niestandardowego skryptu, szczegóły wykonywania skryptu można znaleźć lokalnie na maszynie wirtualnej, na którym uruchomiono rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-171">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="77806-172">Wszystkie kroki rozwiązywania problemów specyficzne dla rozszerzenia są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="77806-173">Następujące kroki dotyczą wszystkich rozszerzeń maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-173">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="77806-174">Wyświetl stan rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="77806-174">View extension status</span></span>

<span data-ttu-id="77806-175">Po maszyny wirtualnej była uruchamiana rozszerzenia maszyny wirtualnej, użyj następującego polecenia wiersza polecenia platformy Azure ma zostać zwrócony stan rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77806-175">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span></span> <span data-ttu-id="77806-176">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="77806-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="77806-177">Dane wyjściowe wyglądają następująco następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="77806-177">The output looks like the following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="77806-178">Stan wykonania rozszerzenia można znaleźć w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-178">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="77806-179">Aby wyświetlić stan rozszerzenia, wybierz maszynę wirtualną, wybierz polecenie **rozszerzenia**i wybierz żądane rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="77806-179">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="77806-180">Uruchom ponownie rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-180">Rerun a VM extension</span></span>

<span data-ttu-id="77806-181">Może to być przypadkach, w których można ponownie uruchomić wymaga rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77806-181">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="77806-182">Możesz ponownie uruchomić rozszerzenia, usuwając go i następnie ponowne uruchomienie rozszerzenia metodą wykonywania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77806-182">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="77806-183">Aby usunąć rozszerzenie, uruchom następujące polecenie z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77806-183">To remove an extension, run the following command with the Azure CLI.</span></span> <span data-ttu-id="77806-184">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="77806-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="77806-185">Aby usunąć rozszerzenie, należy w następujących krokach w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="77806-185">You can remove an extension by using the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="77806-186">Wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="77806-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="77806-187">Wybierz **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="77806-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="77806-188">Wybierz żądane rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="77806-188">Select the desired extension.</span></span>
4. <span data-ttu-id="77806-189">Wybierz **odinstalować**.</span><span class="sxs-lookup"><span data-stu-id="77806-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="77806-190">Typowe odwołania do rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-190">Common VM extension reference</span></span>
| <span data-ttu-id="77806-191">Nazwa rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="77806-191">Extension name</span></span> | <span data-ttu-id="77806-192">Opis</span><span class="sxs-lookup"><span data-stu-id="77806-192">Description</span></span> | <span data-ttu-id="77806-193">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="77806-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77806-194">Niestandardowe rozszerzenie skryptu dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="77806-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="77806-195">Uruchom skrypty przed maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77806-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="77806-196">Niestandardowe rozszerzenie skryptu dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="77806-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="77806-197">Rozszerzenie docker</span><span class="sxs-lookup"><span data-stu-id="77806-197">Docker extension</span></span> |<span data-ttu-id="77806-198">Instalowanie demona Docker do obsługi poleceń zdalnych Docker.</span><span class="sxs-lookup"><span data-stu-id="77806-198">Install the Docker daemon to support remote Docker commands.</span></span> |[<span data-ttu-id="77806-199">Rozszerzenie maszyny wirtualnej Docker</span><span class="sxs-lookup"><span data-stu-id="77806-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="77806-200">Rozszerzenie dostępu do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-200">VM Access extension</span></span> |<span data-ttu-id="77806-201">Odzyskać dostęp do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77806-201">Regain access to an Azure virtual machine</span></span> |[<span data-ttu-id="77806-202">Rozszerzenie dostępu do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="77806-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="77806-203">Rozszerzenie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="77806-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="77806-204">Zarządzanie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="77806-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="77806-205">Rozszerzenie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="77806-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="77806-206">Rozszerzenia dostępu do maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77806-206">Azure VM Access extension</span></span> |<span data-ttu-id="77806-207">Zarządzaj użytkownikami i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="77806-207">Manage users and credentials</span></span> |[<span data-ttu-id="77806-208">Rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="77806-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
