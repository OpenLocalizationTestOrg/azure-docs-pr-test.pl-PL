---
title: "aaaVirtual komputera rozszerzeń i funkcji w systemie Linux | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="55d24-103">Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="55d24-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="55d24-104">Rozszerzenia maszyny wirtualnej platformy Azure są małe aplikacji, które mają po wdrożeniu i automatyzację zadań na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="55d24-105">Na przykład, jeśli maszyna wirtualna wymaga instalacji oprogramowania, ochrony oprogramowania antywirusowego lub Docker konfiguracji, rozszerzenia maszyny Wirtualnej mogą być używane toocomplete tych zadań.</span><span class="sxs-lookup"><span data-stu-id="55d24-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="55d24-106">Rozszerzenia maszyny Wirtualnej platformy Azure mogą być uruchamiane przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, szablony usługi Azure Resource Manager i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="55d24-107">Rozszerzenia mogą być powiązane z nowego wdrożenia maszyny wirtualnej lub uruchomienia dowolnego istniejącego systemu.</span><span class="sxs-lookup"><span data-stu-id="55d24-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="55d24-108">Ten dokument zawiera omówienie rozszerzeń maszyny Wirtualnej, wymagań wstępnych dotyczących używania rozszerzenia maszyny Wirtualnej platformy Azure i wskazówki na sposób toodetect, zarządzania i usunąć rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="55d24-109">Ten dokument zawiera informacje uogólniony wielu rozszerzeń maszyny Wirtualnej nie są dostępne, każde z nich potencjalnie unikatowych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="55d24-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="55d24-110">Rozszerzenie szczegółowe znajdują się w poszczególnych rozszerzeń poszczególnych toohello określonego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="55d24-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="55d24-111">Przypadki użycia i przykłady</span><span class="sxs-lookup"><span data-stu-id="55d24-111">Use cases and samples</span></span>

<span data-ttu-id="55d24-112">Dostępnych jest kilka różnych rozszerzeń maszyny Wirtualnej platformy Azure, każde z nich określony przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="55d24-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="55d24-113">Przykłady to:</span><span class="sxs-lookup"><span data-stu-id="55d24-113">Some examples are:</span></span>

- <span data-ttu-id="55d24-114">Zastosowanie programu PowerShell żądany stan konfiguracji tooa maszyny wirtualnej za pomocą hello rozszerzenia konfiguracji DSC dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="55d24-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="55d24-115">Aby uzyskać więcej informacji, zobacz [Azure żądany stan konfiguracji rozszerzenia](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="55d24-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="55d24-116">Konfigurowanie monitorowania maszyny wirtualnej z hello rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="55d24-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="55d24-117">Aby uzyskać więcej informacji, zobacz [jak toomonitor Maszynę wirtualną systemu Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="55d24-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="55d24-118">Skonfiguruj Monitorowanie infrastruktury platformy Azure z hello Datadog rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="55d24-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="55d24-119">Aby uzyskać więcej informacji, zobacz hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="55d24-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="55d24-120">Konfigurowanie hosta Docker na maszynie wirtualnej platformy Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello.</span><span class="sxs-lookup"><span data-stu-id="55d24-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="55d24-121">Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyny Wirtualnej platformy Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="55d24-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="55d24-122">Ponadto rozszerzenia tooprocess rozszerzenia niestandardowego skryptu dostępnej dla maszyn wirtualnych w systemach Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="55d24-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="55d24-123">Witaj rozszerzenia niestandardowego skryptu dla systemu Linux umożliwia żadnych Bash toobe skrypt uruchamiany na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="55d24-124">Niestandardowe skrypty są przydatne w przypadku projektowania wdrożeń platformy Azure, które wymagają konfiguracji oprócz zapewniają jakie natywnego narzędzia Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="55d24-125">Aby uzyskać więcej informacji, zobacz [rozszerzenie skryptu niestandardowego maszyny Wirtualnej systemu Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="55d24-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="55d24-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55d24-126">Prerequisites</span></span>

<span data-ttu-id="55d24-127">Każde rozszerzenie maszyny wirtualnej może mieć własny zestaw wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="55d24-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="55d24-128">Na przykład hello rozszerzenia maszyny Wirtualnej platformy Docker ma wymagań wstępnych obsługiwanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="55d24-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="55d24-129">Wymagania dotyczące poszczególnych rozszerzeń są szczegółowo opisane w dokumentacji konkretnego rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="55d24-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="55d24-130">Agent maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-130">Azure VM agent</span></span>

<span data-ttu-id="55d24-131">agent maszyny Wirtualnej Azure Hello zarządza interakcje między maszyny wirtualnej platformy Azure i hello kontrolera sieci szkieletowej Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="55d24-132">agent maszyny Wirtualnej Hello jest odpowiedzialny za dużo aspekty funkcjonalne, wdrażania i zarządzania maszynami wirtualnymi platformy Azure, łącznie z rozszerzeniami maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="55d24-133">agent maszyny Wirtualnej Azure Hello jest preinstalowany na portalu Azure Marketplace obrazów i można zainstalować ręcznie w obsługiwanych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="55d24-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="55d24-134">Aby uzyskać informacje dotyczące obsługiwanych systemów operacyjnych i instrukcje dotyczące instalacji, zobacz [agenta maszyny wirtualnej platformy Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="55d24-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="55d24-135">Odnajdywanie rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-135">Discover VM extensions</span></span>

<span data-ttu-id="55d24-136">Wiele różnych rozszerzeń maszyny Wirtualnej są dostępne do użycia z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="55d24-137">toosee pełną listę, uruchom hello następujące polecenie z wiersza polecenia platformy Azure hello, zastępując lokalizacji przykład hello hello wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="55d24-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="55d24-138">Uruchom rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-138">Run VM extensions</span></span>

<span data-ttu-id="55d24-139">Rozszerzenia maszyny wirtualnej platformy Azure może działać w istniejących maszyn wirtualnych, które są przydatne, gdy potrzebne zmiany w konfiguracji toomake lub Przywróć łączność w przypadku wdrożonej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="55d24-140">Rozszerzenia maszyny Wirtualnej dołączany także wdrażanie szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55d24-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="55d24-141">Za pomocą rozszerzeń z szablonami usługi Resource Manager, można wdrożyć i konfigurować bez interwencji po wdrożeniu maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="55d24-142">Hello następujące metody mogą być używane toorun rozszerzenie dla istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="55d24-143">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-143">Azure CLI</span></span>

<span data-ttu-id="55d24-144">Rozszerzenia maszyny wirtualnej platformy Azure mogą być uruchamiane na istniejącej maszyny wirtualnej za pomocą hello `az vm extension set` polecenia.</span><span class="sxs-lookup"><span data-stu-id="55d24-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="55d24-145">W tym przykładzie jest uruchamiana hello niestandardowe rozszerzenie skryptu dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="55d24-146">Witaj skrypt generuje dane wyjściowe podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="55d24-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="55d24-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="55d24-147">Azure portal</span></span>

<span data-ttu-id="55d24-148">Rozszerzenia maszyny Wirtualnej może być zastosowane tooan istniejącej maszyny wirtualnej za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="55d24-149">toodo tak, wybierz maszynę wirtualną hello, wybierz **rozszerzenia**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="55d24-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="55d24-150">Wybierz rozszerzenie hello z hello listę dostępnych rozszerzeń i postępuj zgodnie z instrukcjami powitania w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="55d24-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="55d24-151">Witaj poniższy obraz przedstawia hello instalacji hello rozszerzenie skryptu niestandardowego Linux z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Zainstaluj rozszerzenie skryptu niestandardowego](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="55d24-153">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55d24-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="55d24-154">Rozszerzeń maszyny Wirtualnej może być dodany tooan szablonu usługi Azure Resource Manager i wykonany przy użyciu wdrożenia hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="55d24-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="55d24-155">Podczas wdrażania rozszerzenia za pomocą szablonu można tworzyć wdrożeń platformy Azure w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="55d24-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="55d24-156">Na przykład po JSON hello jest pobierana z szablonem usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55d24-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="55d24-157">Szablon Hello wdraża zestaw maszyn wirtualnych z równoważeniem obciążenia i bazy danych Azure SQL, a następnie instaluje aplikację .NET Core na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="55d24-158">Instalacja oprogramowania hello odpowiada on za Hello rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="55d24-159">Aby uzyskać więcej informacji, zobacz pełną hello [szablonu usługi Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="55d24-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="55d24-160">Aby uzyskać więcej informacji, zobacz [szablonów Authoring Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="55d24-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="55d24-161">Zabezpieczanie danych rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-161">Secure VM extension data</span></span>

<span data-ttu-id="55d24-162">Jeśli korzystasz z rozszerzenia maszyny Wirtualnej, może być konieczne tooinclude poufne informacje, takie jak poświadczeń, nazwy konta magazynu i klucze dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="55d24-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="55d24-163">Wiele rozszerzeń maszyny Wirtualnej obejmują konfiguracji chronionych danych i tylko odszyfrowującego wewnątrz hello docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="55d24-164">Każde rozszerzenie ma schematu określonej konfiguracji chronionych, a każdy szczegółowo opisano w dokumentacji konkretnego rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="55d24-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="55d24-165">Witaj poniższy przykład przedstawia wystąpienie hello rozszerzenia niestandardowego skryptu dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="55d24-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="55d24-166">Należy zauważyć, że tego tooexecute polecenia hello zawiera zestaw poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="55d24-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="55d24-167">W tym przykładzie hello tooexecute polecenia nie będą szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="55d24-167">In this example, hello command tooexecute will not be encrypted.</span></span>


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

<span data-ttu-id="55d24-168">Przenoszenie hello **tooexecute polecenia** toohello właściwości **chronione** konfiguracja zabezpiecza hello wykonywania ciągu.</span><span class="sxs-lookup"><span data-stu-id="55d24-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="55d24-169">Rozwiązywanie problemów z rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="55d24-170">Każde rozszerzenie maszyny Wirtualnej może być Rozwiązywanie problemów z rozszerzenia toohello określonych czynności.</span><span class="sxs-lookup"><span data-stu-id="55d24-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="55d24-171">Na przykład podczas korzystania z rozszerzenia niestandardowego skryptu hello, szczegóły wykonywania skryptu można znaleźć lokalnie na maszynie wirtualnej hello, na którym uruchomiono hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="55d24-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="55d24-172">Wszystkie kroki rozwiązywania problemów specyficzne dla rozszerzenia są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="55d24-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="55d24-173">następujące kroki rozwiązywania problemów Hello mają zastosowanie tooall rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55d24-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="55d24-174">Wyświetl stan rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="55d24-174">View extension status</span></span>

<span data-ttu-id="55d24-175">Po uruchomieniu rozszerzenie maszyny wirtualnej na maszynie wirtualnej, użyj powitania po stan rozszerzenia tooreturn polecenia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="55d24-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="55d24-176">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="55d24-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="55d24-177">dane wyjściowe Hello wygląda hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="55d24-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="55d24-178">Stan wykonania rozszerzenia można znaleźć w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="55d24-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="55d24-179">Wybierz stan hello tooview rozszerzenia maszyny wirtualnej wybierz hello, **rozszerzenia**, i wybierz hello żądanego rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="55d24-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="55d24-180">Uruchom ponownie rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-180">Rerun a VM extension</span></span>

<span data-ttu-id="55d24-181">Może się zdarzyć, w których toobe, musi mieć rozszerzenie maszyny wirtualnej ponownie.</span><span class="sxs-lookup"><span data-stu-id="55d24-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="55d24-182">Możesz ponownie uruchomić rozszerzenia, usuwając go i następnie ponowne uruchomienie rozszerzenia hello metodą wykonywania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="55d24-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="55d24-183">tooremove rozszerzenia, uruchom następujące polecenie z wiersza polecenia platformy Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="55d24-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="55d24-184">Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="55d24-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="55d24-185">Rozszerzenie można usunąć przy użyciu hello następujące kroki w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="55d24-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="55d24-186">Wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="55d24-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="55d24-187">Wybierz **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="55d24-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="55d24-188">Wybierz żądaną hello rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="55d24-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="55d24-189">Wybierz **odinstalować**.</span><span class="sxs-lookup"><span data-stu-id="55d24-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="55d24-190">Typowe odwołania do rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-190">Common VM extension reference</span></span>
| <span data-ttu-id="55d24-191">Nazwa rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="55d24-191">Extension name</span></span> | <span data-ttu-id="55d24-192">Opis</span><span class="sxs-lookup"><span data-stu-id="55d24-192">Description</span></span> | <span data-ttu-id="55d24-193">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="55d24-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55d24-194">Niestandardowe rozszerzenie skryptu dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="55d24-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="55d24-195">Uruchom skrypty przed maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="55d24-196">Niestandardowe rozszerzenie skryptu dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="55d24-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="55d24-197">Rozszerzenie docker</span><span class="sxs-lookup"><span data-stu-id="55d24-197">Docker extension</span></span> |<span data-ttu-id="55d24-198">Zainstaluj hello Docker demon toosupport Docker poleceń zdalnych.</span><span class="sxs-lookup"><span data-stu-id="55d24-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="55d24-199">Rozszerzenie maszyny wirtualnej Docker</span><span class="sxs-lookup"><span data-stu-id="55d24-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="55d24-200">Rozszerzenie dostępu do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-200">VM Access extension</span></span> |<span data-ttu-id="55d24-201">Odzyskanie dostępu tooan maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="55d24-202">Rozszerzenie dostępu do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55d24-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="55d24-203">Rozszerzenie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="55d24-204">Zarządzanie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="55d24-205">Rozszerzenie Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="55d24-206">Rozszerzenia dostępu do maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="55d24-206">Azure VM Access extension</span></span> |<span data-ttu-id="55d24-207">Zarządzaj użytkownikami i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="55d24-207">Manage users and credentials</span></span> |[<span data-ttu-id="55d24-208">Rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="55d24-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
