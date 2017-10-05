---
title: "Tworzenie szablonów z rozszerzeniami maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 338668df33783d8ef62c6710f4d96ce805296fe5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="1d73d-103">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1d73d-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="1d73d-104">Z programu Azure PowerShell uruchom następujące polecenie cmdlet programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1d73d-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="1d73d-105">To polecenie cmdlet zwraca nazwę wydawcy, nazwa rozszerzenia i wersji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d73d-105">This cmdlet returns the publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="1d73d-106">Te trzy właściwości są mapowane na "publisher", "type" i "typeHandlerVersion" odpowiednio w powyższym fragment szablonu.</span><span class="sxs-lookup"><span data-stu-id="1d73d-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="1d73d-107">Zalecane jest zawsze używać najnowszej wersji rozszerzenia, aby korzystać z najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="1d73d-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="1d73d-108">Identyfikowanie schematu dla parametrów konfiguracji rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="1d73d-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="1d73d-109">Następnym krokiem z tworzenia szablonu rozszerzenia jest do identyfikowania format zapewniające parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1d73d-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="1d73d-110">Każde rozszerzenie obsługuje własny zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="1d73d-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="1d73d-111">Aby przyjrzeć się przykładowych konfiguracji rozszerzeń systemu Windows, zobacz [przykładów rozszerzeń Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d73d-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1d73d-112">Zapoznaj się z następujących czynności, aby uzyskać szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d73d-112">Please refer to the following to get a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="1d73d-113">Niestandardowe rozszerzenie skryptu Windows maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1d73d-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="1d73d-114">Po utworzeniu szablonu, można wdrożyć przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d73d-114">After authoring the template, you can deploy it using Azure PowerShell.</span></span>

