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
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Z programu Azure PowerShell, uruchom następujące polecenia cmdlet programu Azure PowerShell hello:

      Get-AzureVMAvailableExtension


To polecenie cmdlet zwraca hello nazwę wydawcy, nazwa rozszerzenia i wersji w następujący sposób:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Te trzy właściwości mapy zbyt "publisher", "type" i "typeHandlerVersion" odpowiednio w hello powyżej fragment szablonu.

> [!NOTE]
> Zawsze jest zalecane toouse hello najnowsze rozszerzenia wersji tooget hello najbardziej zaktualizowane funkcje.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Identyfikowanie hello schematu dla parametrów konfiguracji rozszerzenia hello
następnym krokiem Hello z tworzenia szablonu rozszerzenia jest format hello tooidentify zapewniające parametry konfiguracji. Każde rozszerzenie obsługuje własny zestaw parametrów.

toolook w przykładowych konfiguracji rozszerzeń systemu Windows, temacie [przykładów rozszerzeń Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Zobacz toohello po tooget szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.

[Niestandardowe rozszerzenie skryptu Windows maszyny Wirtualnej](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Po utworzeniu szablonu hello, można wdrożyć przy użyciu programu Azure PowerShell.

