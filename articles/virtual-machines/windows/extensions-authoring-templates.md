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
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Z programu Azure PowerShell uruchom następujące polecenie cmdlet programu Azure PowerShell:

      Get-AzureVMAvailableExtension


To polecenie cmdlet zwraca nazwę wydawcy, nazwa rozszerzenia i wersji w następujący sposób:

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

Aby przyjrzeć się przykładowych konfiguracji rozszerzeń systemu Windows, zobacz [przykładów rozszerzeń Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Zapoznaj się z następujących czynności, aby uzyskać szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.

[Niestandardowe rozszerzenie skryptu Windows maszyny Wirtualnej](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Po utworzeniu szablonu, można wdrożyć przy użyciu programu Azure PowerShell.

