---
title: aaaAuthoring szablony z rozszerzeniami maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat tworzenia szablonów usługi Azure Resource Manager z rozszerzeniami dla maszyn wirtualnych systemu Windows"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="4fa1e-103">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="4fa1e-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="4fa1e-104">Z programu Azure PowerShell, uruchom następujące polecenia cmdlet programu Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="4fa1e-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="4fa1e-105">To polecenie cmdlet zwraca hello nazwę wydawcy, nazwa rozszerzenia i wersji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4fa1e-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="4fa1e-106">Te trzy właściwości mapy zbyt "publisher", "type" i "typeHandlerVersion" odpowiednio w hello powyżej fragment szablonu.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="4fa1e-107">Zawsze jest zalecane toouse hello najnowsze rozszerzenia wersji tooget hello najbardziej zaktualizowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="4fa1e-108">Identyfikowanie hello schematu dla parametrów konfiguracji rozszerzenia hello</span><span class="sxs-lookup"><span data-stu-id="4fa1e-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="4fa1e-109">następnym krokiem Hello z tworzenia szablonu rozszerzenia jest format hello tooidentify zapewniające parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="4fa1e-110">Każde rozszerzenie obsługuje własny zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="4fa1e-111">toolook w przykładowych konfiguracji rozszerzeń systemu Windows, temacie [przykładów rozszerzeń Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fa1e-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4fa1e-112">Zobacz toohello po tooget szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="4fa1e-113">Niestandardowe rozszerzenie skryptu Windows maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4fa1e-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="4fa1e-114">Po utworzeniu szablonu hello, można wdrożyć przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

