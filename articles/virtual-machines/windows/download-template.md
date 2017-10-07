---
title: Szablon hello aaaDownload dla maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Pobierz templatefor hello toohelp maszyny Wirtualnej, automatyzacji wdrażania modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Pobierz hello szablon maszyny wirtualnej
Podczas tworzenia maszyny Wirtualnej na platformie Azure za pomocą portalu hello lub programu PowerShell, Menedżer zasobów szablonu jest utworzony automatycznie. Można użyć tego duplikat tooquickly szablonu wdrożenia. Szablon Hello zawiera informacje na temat wszystkich zasobów hello w grupie zasobów. Dla maszyny wirtualnej oznacza to, że szablon hello zawiera wszystko, co jest tworzony w związku z hello maszyny Wirtualnej w tej grupie zasobów, w tym hello zasobów sieciowych.

## <a name="download-hello-template-using-hello-portal"></a>Pobierz szablon hello przy użyciu portalu hello
1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Hello jednego koncentratora menu, wybierz opcję **maszyn wirtualnych**.
3. Wybierz maszynę wirtualną hello z listy hello.
4. Wybierz **skryptu automatyzacji**.
5. Wybierz **Pobierz** i Zapisz komputer lokalny plik tooyour hello zip.
6. Otwórz plik zip hello i wyodrębnienia hello pliki tooa folder. plik zip Hello będzie zawierać:
   
   * Deploy.ps1
   * Deploy.sh 
   * deployer.RB
   * DeploymentHelper.cs
   * parameters.JSON następującym kodem
   * Template.JSON

Plik template.json Hello jest hello szablonu.

## <a name="download-hello-template-using-powershell"></a>Pobierz szablon hello przy użyciu programu PowerShell
Możesz również pobrać plik szablonu JSON hello przy użyciu hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) polecenia cmdlet. Można użyć hello `-path` parametru tooprovide hello nazwę i ścieżkę do pliku JSON hello. W tym przykładzie pokazano, jak szablon hello toodownload hello grupy zasobów o nazwie **myResourceGroup** toohello **C:\users\public\downloads** folderu na komputerze lokalnym.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat wdrażania zasobów przy użyciu szablonów, zobacz [Przewodnik po szablonie usługi Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

