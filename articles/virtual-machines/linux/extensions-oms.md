---
title: aaaOMS rozszerzenia maszyny wirtualnej platformy Azure dla systemu Linux | Dokumentacja firmy Microsoft
description: "Wdróż agenta pakietu OMS hello na maszynie wirtualnej systemu Linux przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="bec12-103">Rozszerzenie maszyny wirtualnej OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="bec12-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="bec12-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bec12-104">Overview</span></span>

<span data-ttu-id="bec12-105">Operations Management Suite (OMS) zapewnia możliwości korygowania monitorowania, alertów i alertów w chmurze i lokalnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="bec12-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="bec12-106">Witaj Agent pakietu OMS rozszerzenie maszyny wirtualnej dla systemu Linux publikowania i obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bec12-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="bec12-107">rozszerzenie Hello instaluje agenta pakietu OMS hello na maszynach wirtualnych platformy Azure i rejestrowania maszyn wirtualnych w istniejącym obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="bec12-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="bec12-108">Hello szczegóły tego dokumentu obsługuje platform, konfiguracji i opcji wdrażania hello OMS rozszerzenie maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="bec12-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bec12-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bec12-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="bec12-110">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="bec12-110">Operating system</span></span>

<span data-ttu-id="bec12-111">Witaj Agent pakietu OMS rozszerzenia mogą być uruchamiane na tych dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="bec12-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="bec12-112">Dystrybucja</span><span class="sxs-lookup"><span data-stu-id="bec12-112">Distribution</span></span> | <span data-ttu-id="bec12-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="bec12-113">Version</span></span> |
|---|---|
| <span data-ttu-id="bec12-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="bec12-114">CentOS Linux</span></span> | <span data-ttu-id="bec12-115">5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="bec12-115">5, 6, and 7</span></span> |
| <span data-ttu-id="bec12-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="bec12-116">Oracle Linux</span></span> | <span data-ttu-id="bec12-117">5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="bec12-117">5, 6, and 7</span></span> |
| <span data-ttu-id="bec12-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="bec12-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="bec12-119">5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="bec12-119">5, 6 and 7</span></span> |
| <span data-ttu-id="bec12-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="bec12-120">Debian GNU/Linux</span></span> | <span data-ttu-id="bec12-121">6, 7 i 8</span><span class="sxs-lookup"><span data-stu-id="bec12-121">6, 7, and 8</span></span> |
| <span data-ttu-id="bec12-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="bec12-122">Ubuntu</span></span> | <span data-ttu-id="bec12-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="bec12-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="bec12-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="bec12-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="bec12-125">11 i 12</span><span class="sxs-lookup"><span data-stu-id="bec12-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="bec12-126">Łączność z Internetem</span><span class="sxs-lookup"><span data-stu-id="bec12-126">Internet connectivity</span></span>

<span data-ttu-id="bec12-127">Hello Agent pakietu OMS rozszerzenia dla systemu Linux wymaga tego hello docelowej maszyny wirtualnej jest połączonych toohello internet.</span><span class="sxs-lookup"><span data-stu-id="bec12-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="bec12-128">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="bec12-128">Extension schema</span></span>

<span data-ttu-id="bec12-129">Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="bec12-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="bec12-130">rozszerzenie Hello wymaga hello klucz identyfikator i obszaru roboczego obszaru roboczego z hello docelowym obszarem roboczym pakietu OMS; te wartości można znaleźć w portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="bec12-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="bec12-131">Ponieważ klucz obszaru roboczego hello powinny być traktowane jako poufne dane, powinny być przechowywane w chronionej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bec12-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="bec12-132">Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bec12-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="bec12-133">Należy pamiętać, że **workspaceId** i **workspaceKey** jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bec12-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="bec12-134">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="bec12-134">Property values</span></span>

| <span data-ttu-id="bec12-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bec12-135">Name</span></span> | <span data-ttu-id="bec12-136">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="bec12-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="bec12-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="bec12-137">apiVersion</span></span> | <span data-ttu-id="bec12-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="bec12-138">2015-06-15</span></span> |
| <span data-ttu-id="bec12-139">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="bec12-139">publisher</span></span> | <span data-ttu-id="bec12-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="bec12-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="bec12-141">type</span><span class="sxs-lookup"><span data-stu-id="bec12-141">type</span></span> | <span data-ttu-id="bec12-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="bec12-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="bec12-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="bec12-143">typeHandlerVersion</span></span> | <span data-ttu-id="bec12-144">1.4</span><span class="sxs-lookup"><span data-stu-id="bec12-144">1.4</span></span> |
| <span data-ttu-id="bec12-145">workspaceId (np.)</span><span class="sxs-lookup"><span data-stu-id="bec12-145">workspaceId (e.g)</span></span> | <span data-ttu-id="bec12-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="bec12-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="bec12-147">workspaceKey (np.)</span><span class="sxs-lookup"><span data-stu-id="bec12-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="bec12-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="bec12-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="bec12-149">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="bec12-149">Template deployment</span></span>

<span data-ttu-id="bec12-150">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bec12-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="bec12-151">Szablony są idealne w przypadku wdrażania maszyn wirtualnych, które wymagają konfiguracji wdrożenia post, takich jak tooOMS dołączania.</span><span class="sxs-lookup"><span data-stu-id="bec12-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="bec12-152">Przykładowy szablon usługi Resource Manager zawierający rozszerzenia maszyny Wirtualnej agenta pakietu OMS hello znajduje się na powitania [Azure Szybki Start galerii](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="bec12-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="bec12-153">Hello JSON konfiguracji dla rozszerzenia maszyny wirtualnej można zagnieżdżona hello zasobu maszyny wirtualnej lub umieszczane na główny hello lub najwyższego poziomu szablonu usługi Resource Manager JSON.</span><span class="sxs-lookup"><span data-stu-id="bec12-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="bec12-154">umieszczanie Hello hello JSON konfiguracji dotyczy wartości hello hello nazwy zasobów i typu.</span><span class="sxs-lookup"><span data-stu-id="bec12-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="bec12-155">Aby uzyskać więcej informacji, zobacz [Ustaw nazwę i typ zasoby podrzędne](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bec12-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="bec12-156">Witaj poniższym przykładzie przyjęto założenie, że rozszerzenie OMS hello jest zagnieżdżona hello zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bec12-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="bec12-157">Podczas zagnieżdżania hello rozszerzenia zasobu, hello JSON jest umieszczany w hello `"resources": []` obiektu hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bec12-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="bec12-158">Podczas umieszczania hello rozszerzenia JSON w głównym hello hello szablonu, hello Nazwa zasobu zawiera maszynę wirtualną nadrzędnej toohello odwołania, a typ hello odzwierciedla hello zagnieżdżonych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bec12-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="bec12-159">Wdrożenia usługi Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bec12-159">Azure CLI deployment</span></span>

<span data-ttu-id="bec12-160">Hello wiersza polecenia platformy Azure mogą być używane toodeploy hello VM Agent pakietu OMS rozszerzenia tooan istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bec12-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="bec12-161">Zamień na powitania OMS klucz i identyfikator pakietu OMS od obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="bec12-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="bec12-162">Rozwiązywanie problemów i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="bec12-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="bec12-163">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="bec12-163">Troubleshoot</span></span>

<span data-ttu-id="bec12-164">Z hello portalu Azure i przy użyciu interfejsu wiersza polecenia Azure hello można pobrać danych o stanie hello wdrożeń rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="bec12-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="bec12-165">Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom powitania po użyciu polecenia hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bec12-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="bec12-166">Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toohello następującego pliku:</span><span class="sxs-lookup"><span data-stu-id="bec12-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="bec12-167">Kody błędów i ich znaczenie</span><span class="sxs-lookup"><span data-stu-id="bec12-167">Error codes and their meanings</span></span>

| <span data-ttu-id="bec12-168">Kod błędu:</span><span class="sxs-lookup"><span data-stu-id="bec12-168">Error Code</span></span> | <span data-ttu-id="bec12-169">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="bec12-169">Meaning</span></span> | <span data-ttu-id="bec12-170">Możliwe działania</span><span class="sxs-lookup"><span data-stu-id="bec12-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="bec12-171">10</span><span class="sxs-lookup"><span data-stu-id="bec12-171">10</span></span> | <span data-ttu-id="bec12-172">Maszyna wirtualna jest już połączony tooan obszarem roboczym pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="bec12-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="bec12-173">tooconnect hello wirtualna toohello roboczym określonej w schemacie rozszerzenia hello, ustaw stopOnMultipleConnections toofalse w ustawieniach publiczny lub Usuń tę właściwość.</span><span class="sxs-lookup"><span data-stu-id="bec12-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="bec12-174">Tej maszyny Wirtualnej pobiera rozliczane po dla każdego obszaru roboczego jest połączony.</span><span class="sxs-lookup"><span data-stu-id="bec12-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="bec12-175">11</span><span class="sxs-lookup"><span data-stu-id="bec12-175">11</span></span> | <span data-ttu-id="bec12-176">Nieprawidłowy konfiguracji podano toohello rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="bec12-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="bec12-177">Wykonaj hello poprzedzających tooset przykłady wszystkich wartości właściwości niezbędne do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="bec12-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="bec12-178">12</span><span class="sxs-lookup"><span data-stu-id="bec12-178">12</span></span> | <span data-ttu-id="bec12-179">Menedżer pakietów dpkg Hello jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="bec12-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="bec12-180">Upewnij się, wszystkie dpkg operacje aktualizacji na komputerze hello zostało ukończone, a następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="bec12-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="bec12-181">20</span><span class="sxs-lookup"><span data-stu-id="bec12-181">20</span></span> | <span data-ttu-id="bec12-182">Włącz o nazwie przedwcześnie</span><span class="sxs-lookup"><span data-stu-id="bec12-182">Enable called prematurely</span></span> | <span data-ttu-id="bec12-183">[Witaj aktualizacji agenta systemu Linux Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="bec12-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="bec12-184">51</span><span class="sxs-lookup"><span data-stu-id="bec12-184">51</span></span> | <span data-ttu-id="bec12-185">To rozszerzenie nie jest obsługiwany w systemie operacji hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bec12-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="bec12-186">55</span><span class="sxs-lookup"><span data-stu-id="bec12-186">55</span></span> | <span data-ttu-id="bec12-187">Nie można połączyć z usługą Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="bec12-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="bec12-188">Sprawdź, czy hello system ma dostęp do Internetu lub że podano prawidłowy serwer proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="bec12-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="bec12-189">Ponadto sprawdź poprawność hello identyfikator hello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="bec12-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="bec12-190">Dodatkowe informacje dotyczące rozwiązywania problemów można znaleźć na powitania [przewodnik rozwiązywania problemów OMS agenta dla Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="bec12-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="bec12-191">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="bec12-191">Support</span></span>

<span data-ttu-id="bec12-192">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="bec12-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="bec12-193">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bec12-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="bec12-194">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="bec12-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="bec12-195">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="bec12-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
