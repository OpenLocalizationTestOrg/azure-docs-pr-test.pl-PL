---
title: "aaaAzure rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Wdróż hello Agent monitora sieci na maszynie wirtualnej systemu Linux przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="e103c-103">Rozszerzenie maszyny wirtualnej obserwatorów agenta sieciowe dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="e103c-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="e103c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e103c-104">Overview</span></span>

<span data-ttu-id="e103c-105">[Azure obserwatora sieciowego](https://review.docs.microsoft.com/en-us/azure/network-watcher/) jest sieci performance monitoring, Diagnostyka i analiza usługa, która umożliwia monitorowanie sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e103c-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="e103c-106">Hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta jest wymagane dla niektórych funkcji obserwatora sieciowego hello na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="e103c-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="e103c-107">Dotyczy to również Przechwytywanie ruchu sieciowego na żądanie i inne zaawansowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="e103c-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="e103c-108">Hello szczegóły tego dokumentu obsługiwane platformy i opcje wdrażania dla hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="e103c-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e103c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e103c-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="e103c-110">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="e103c-110">Operating system</span></span>

<span data-ttu-id="e103c-111">Hello rozszerzenia Agent monitora sieci mogą być uruchamiane na tych dystrybucje systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="e103c-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="e103c-112">Dystrybucja</span><span class="sxs-lookup"><span data-stu-id="e103c-112">Distribution</span></span> | <span data-ttu-id="e103c-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="e103c-113">Version</span></span> |
|---|---|
| <span data-ttu-id="e103c-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e103c-114">Ubuntu</span></span> | <span data-ttu-id="e103c-115">16.04 LTS, 14.04 LTS i 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="e103c-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="e103c-116">Debian</span><span class="sxs-lookup"><span data-stu-id="e103c-116">Debian</span></span> | <span data-ttu-id="e103c-117">7 i 8</span><span class="sxs-lookup"><span data-stu-id="e103c-117">7 and 8</span></span> |
| <span data-ttu-id="e103c-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="e103c-118">RedHat</span></span> | <span data-ttu-id="e103c-119">6.x i 7.x</span><span class="sxs-lookup"><span data-stu-id="e103c-119">6.x and 7.x</span></span> |
| <span data-ttu-id="e103c-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="e103c-120">Oracle Linux</span></span> | <span data-ttu-id="e103c-121">7 x</span><span class="sxs-lookup"><span data-stu-id="e103c-121">7x</span></span> |
| <span data-ttu-id="e103c-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="e103c-122">Suse</span></span> | <span data-ttu-id="e103c-123">11 i 12</span><span class="sxs-lookup"><span data-stu-id="e103c-123">11 and 12</span></span> |
| <span data-ttu-id="e103c-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="e103c-124">OpenSuse</span></span> | <span data-ttu-id="e103c-125">7.0</span><span class="sxs-lookup"><span data-stu-id="e103c-125">7.0</span></span> |
| <span data-ttu-id="e103c-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="e103c-126">CentOS</span></span> | <span data-ttu-id="e103c-127">7.0</span><span class="sxs-lookup"><span data-stu-id="e103c-127">7.0</span></span> |

<span data-ttu-id="e103c-128">Należy pamiętać, że CoreOS nie jest obsługiwana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="e103c-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="e103c-129">Łączność z Internetem</span><span class="sxs-lookup"><span data-stu-id="e103c-129">Internet connectivity</span></span>

<span data-ttu-id="e103c-130">Niektóre hello funkcji Agent monitora sieci wymaga tego hello docelowej maszyny wirtualnej toohello połączenia internetowego.</span><span class="sxs-lookup"><span data-stu-id="e103c-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="e103c-131">Bez połączeń wychodzących hello możliwości tooestablish niektóre funkcje sieciowe obserwatorów agenta hello nieprawidłowe działanie lub stała się niedostępna.</span><span class="sxs-lookup"><span data-stu-id="e103c-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="e103c-132">Aby uzyskać więcej informacji, zobacz hello [dokumentacji obserwatora sieciowego](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="e103c-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="e103c-133">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="e103c-133">Extension schema</span></span>

<span data-ttu-id="e103c-134">Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent monitora sieci.</span><span class="sxs-lookup"><span data-stu-id="e103c-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="e103c-135">rozszerzenie Hello ani wymaga nie obsługuje ustawienia dostarczone przez użytkownika w tej chwili i zależy od konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="e103c-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="e103c-136">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="e103c-136">Property values</span></span>

| <span data-ttu-id="e103c-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e103c-137">Name</span></span> | <span data-ttu-id="e103c-138">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="e103c-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="e103c-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e103c-139">apiVersion</span></span> | <span data-ttu-id="e103c-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="e103c-140">2015-06-15</span></span> |
| <span data-ttu-id="e103c-141">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="e103c-141">publisher</span></span> | <span data-ttu-id="e103c-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="e103c-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="e103c-143">type</span><span class="sxs-lookup"><span data-stu-id="e103c-143">type</span></span> | <span data-ttu-id="e103c-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="e103c-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="e103c-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="e103c-145">typeHandlerVersion</span></span> | <span data-ttu-id="e103c-146">1.4</span><span class="sxs-lookup"><span data-stu-id="e103c-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="e103c-147">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="e103c-147">Template deployment</span></span>

<span data-ttu-id="e103c-148">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e103c-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="e103c-149">Podczas wdrażania szablonu usługi Azure Resource Manager hello toorun szablonu usługi Azure Resource Manager Agent monitora sieci rozszerzenia schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w można.</span><span class="sxs-lookup"><span data-stu-id="e103c-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="e103c-150">Wdrożenia usługi Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e103c-150">Azure CLI deployment</span></span>

<span data-ttu-id="e103c-151">Hello Azure CLI może być używane toodeploy hello VM Agent monitora sieci rozszerzenia tooan istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e103c-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="e103c-152">Rozwiązywanie problemów i pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="e103c-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="e103c-153">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e103c-153">Troubleshooting</span></span>

<span data-ttu-id="e103c-154">Z hello portalu Azure i przy użyciu interfejsu wiersza polecenia Azure hello można pobrać danych o stanie hello wdrożeń rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="e103c-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="e103c-155">Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom powitania po użyciu polecenia hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e103c-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="e103c-156">Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles w hello następującego katalogu:</span><span class="sxs-lookup"><span data-stu-id="e103c-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="e103c-157">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="e103c-157">Support</span></span>

<span data-ttu-id="e103c-158">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule można zapoznaj się z dokumentacją obserwatora sieciowego toohello lub skontaktuj się z hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e103c-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="e103c-159">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e103c-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e103c-160">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="e103c-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="e103c-161">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="e103c-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
