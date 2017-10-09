---
title: Szablony aaaAuthoring rozszerzenia maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="b29ad-103">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b29ad-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="b29ad-104">Z wiersza polecenia platformy Azure uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b29ad-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="b29ad-105">To polecenie zwraca hello nazwę wydawcy, nazwa rozszerzenia i wersji w następujący:</span><span class="sxs-lookup"><span data-stu-id="b29ad-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="b29ad-106">Te trzy właściwości mapy zbyt "publisher", "type" i "typeHandlerVersion" odpowiednio w hello powyżej fragment szablonu.</span><span class="sxs-lookup"><span data-stu-id="b29ad-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="b29ad-107">Zawsze jest zalecane toouse hello najnowsze rozszerzenia wersji tooget hello najbardziej zaktualizowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="b29ad-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="b29ad-108">Identyfikowanie hello schematu dla parametrów konfiguracji rozszerzenia hello</span><span class="sxs-lookup"><span data-stu-id="b29ad-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="b29ad-109">następnym krokiem Hello z tworzenia szablonu rozszerzenia jest format hello tooidentify zapewniające parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b29ad-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="b29ad-110">Każde rozszerzenie obsługuje własny zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="b29ad-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="b29ad-111">toolook w przykładowych konfiguracji rozszerzeń systemu Linux kliknij można znaleźć w dokumentacji hello [przykłady eExtensions Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b29ad-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b29ad-112">Zobacz toohello po tooget szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b29ad-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="b29ad-113">Niestandardowe rozszerzenie skryptu na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b29ad-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="b29ad-114">Po utworzeniu szablonu hello, można wdrożyć przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b29ad-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

