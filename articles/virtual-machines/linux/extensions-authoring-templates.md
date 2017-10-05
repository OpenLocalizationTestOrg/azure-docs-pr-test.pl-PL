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
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Z wiersza polecenia platformy Azure uruchom następujące polecenie:

      Azure VM extension list

To polecenie zwraca nazwę wydawcy, nazwa rozszerzenia i wersji, jak następujące:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Te trzy właściwości są mapowane na "publisher", "type" i "typeHandlerVersion" odpowiednio w powyższym fragment szablonu.

> [!NOTE]
> Zalecane jest zawsze używać najnowszej wersji rozszerzenia, aby korzystać z najnowszych funkcji.
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a>Identyfikowanie schematu dla parametrów konfiguracji rozszerzenia
Następnym krokiem z tworzenia szablonu rozszerzenia jest do identyfikowania format zapewniające parametry konfiguracji. Każde rozszerzenie obsługuje własny zestaw parametrów.

Aby przyjrzeć się przykładowych konfiguracji rozszerzeń systemu Linux, kliknij przycisk można znaleźć w dokumentacji [przykłady eExtensions Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Zapoznaj się z następujących czynności, aby uzyskać szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.

[Niestandardowe rozszerzenie skryptu na maszynie Wirtualnej systemu Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Po utworzeniu szablonu, można wdrożyć przy użyciu wiersza polecenia platformy Azure.

