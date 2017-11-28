---
title: "Tworzenie szablonów z rozszerzeniami maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat tworzenia szablonów usługi Azure Resource Manager z rozszerzeniami dla maszyn wirtualnych systemu Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="ce105-103">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="ce105-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="ce105-104">Z wiersza polecenia platformy Azure uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ce105-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="ce105-105">To polecenie zwraca nazwę wydawcy, nazwa rozszerzenia i wersji, jak następujące:</span><span class="sxs-lookup"><span data-stu-id="ce105-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="ce105-106">Te trzy właściwości są mapowane na "publisher", "type" i "typeHandlerVersion" odpowiednio w powyższym fragment szablonu.</span><span class="sxs-lookup"><span data-stu-id="ce105-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="ce105-107">Zalecane jest zawsze używać najnowszej wersji rozszerzenia, aby korzystać z najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="ce105-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="ce105-108">Identyfikowanie schematu dla parametrów konfiguracji rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="ce105-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="ce105-109">Następnym krokiem z tworzenia szablonu rozszerzenia jest do identyfikowania format zapewniające parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ce105-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="ce105-110">Każde rozszerzenie obsługuje własny zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="ce105-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="ce105-111">Aby przyjrzeć się przykładowych konfiguracji rozszerzeń systemu Linux, kliknij przycisk można znaleźć w dokumentacji [przykłady eExtensions Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce105-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ce105-112">Zapoznaj się z następujących czynności, aby uzyskać szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ce105-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="ce105-113">Niestandardowe rozszerzenie skryptu na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="ce105-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="ce105-114">Po utworzeniu szablonu, można wdrożyć przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce105-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

