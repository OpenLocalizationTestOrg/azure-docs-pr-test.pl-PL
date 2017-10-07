---
title: "aaaAzure rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Wdróż hello Agent monitora sieci na maszynie wirtualnej z systemem Windows przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="92732-103">Rozszerzenie maszyny wirtualnej obserwatorów agenta sieciowe dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="92732-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="92732-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="92732-104">Overview</span></span>

<span data-ttu-id="92732-105">[Azure obserwatora sieciowego](https://review.docs.microsoft.com/en-us/azure/network-watcher/) jest sieci performance monitoring, Diagnostyka i analiza usługa, która umożliwia monitorowanie sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92732-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="92732-106">Hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta jest wymagane dla niektórych funkcji obserwatora sieciowego hello na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="92732-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="92732-107">Dotyczy to również Przechwytywanie ruchu sieciowego na żądanie i inne zaawansowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="92732-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="92732-108">Hello szczegóły tego dokumentu obsługiwane platformy i opcje wdrażania dla hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="92732-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92732-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92732-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="92732-110">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="92732-110">Operating system</span></span>

<span data-ttu-id="92732-111">Witaj rozszerzenia sieci obserwatorów agenta dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.</span><span class="sxs-lookup"><span data-stu-id="92732-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="92732-112">Należy pamiętać, że hello Nano Server nie jest obsługiwana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="92732-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="92732-113">Łączność z Internetem</span><span class="sxs-lookup"><span data-stu-id="92732-113">Internet connectivity</span></span>

<span data-ttu-id="92732-114">Niektóre hello funkcji Agent monitora sieci wymaga tego hello docelowej maszyny wirtualnej toohello połączenia internetowego.</span><span class="sxs-lookup"><span data-stu-id="92732-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="92732-115">Bez połączeń wychodzących hello możliwości tooestablish niektóre funkcje sieciowe obserwatorów agenta hello nieprawidłowe działanie lub stała się niedostępna.</span><span class="sxs-lookup"><span data-stu-id="92732-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="92732-116">Aby uzyskać więcej informacji, zobacz hello [dokumentacji obserwatora sieciowego](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92732-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="92732-117">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="92732-117">Extension schema</span></span>

<span data-ttu-id="92732-118">Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent monitora sieci.</span><span class="sxs-lookup"><span data-stu-id="92732-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="92732-119">rozszerzenie Hello ani wymaga nie obsługuje ustawienia dostarczone przez użytkownika w tej chwili i zależy od konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="92732-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="92732-120">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="92732-120">Property values</span></span>

| <span data-ttu-id="92732-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92732-121">Name</span></span> | <span data-ttu-id="92732-122">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="92732-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="92732-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="92732-123">apiVersion</span></span> | <span data-ttu-id="92732-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="92732-124">2015-06-15</span></span> |
| <span data-ttu-id="92732-125">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="92732-125">publisher</span></span> | <span data-ttu-id="92732-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="92732-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="92732-127">type</span><span class="sxs-lookup"><span data-stu-id="92732-127">type</span></span> | <span data-ttu-id="92732-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="92732-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="92732-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="92732-129">typeHandlerVersion</span></span> | <span data-ttu-id="92732-130">1.4</span><span class="sxs-lookup"><span data-stu-id="92732-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="92732-131">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="92732-131">Template deployment</span></span>

<span data-ttu-id="92732-132">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="92732-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="92732-133">Podczas wdrażania szablonu usługi Azure Resource Manager hello toorun szablonu usługi Azure Resource Manager Agent monitora sieci rozszerzenia schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w można.</span><span class="sxs-lookup"><span data-stu-id="92732-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="92732-134">Wdrożenie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="92732-134">PowerShell deployment</span></span>

<span data-ttu-id="92732-135">Witaj `Set-AzureRmVMExtension` polecenie może być używane toodeploy hello Agent monitora sieci maszyny wirtualnej rozszerzenia tooan istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="92732-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="92732-136">Rozwiązywanie problemów i pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="92732-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="92732-137">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="92732-137">Troubleshooting</span></span>

<span data-ttu-id="92732-138">Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="92732-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="92732-139">Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej hello uruchom następujące polecenia przy użyciu hello modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92732-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="92732-140">Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles w hello następującego katalogu:</span><span class="sxs-lookup"><span data-stu-id="92732-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="92732-141">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="92732-141">Support</span></span>

<span data-ttu-id="92732-142">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule można zapoznaj się z dokumentacją Podręcznik użytkownika obserwatora sieciowego toohello lub skontaktuj się z hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="92732-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="92732-143">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92732-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="92732-144">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="92732-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="92732-145">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="92732-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
