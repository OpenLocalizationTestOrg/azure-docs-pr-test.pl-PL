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
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Z wiersza polecenia platformy Azure uruchom następujące polecenie hello:

      Azure VM extension list

To polecenie zwraca hello nazwę wydawcy, nazwa rozszerzenia i wersji w następujący:

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

toolook w przykładowych konfiguracji rozszerzeń systemu Linux kliknij można znaleźć w dokumentacji hello [przykłady eExtensions Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Zobacz toohello po tooget szablon pełni ukończone z rozszerzeń maszyny Wirtualnej.

[Niestandardowe rozszerzenie skryptu na maszynie Wirtualnej systemu Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Po utworzeniu szablonu hello, można wdrożyć przy użyciu hello wiersza polecenia platformy Azure.

