---
title: "aaaCreate kontener usługi chmury przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate chmurę usługi kontenera przy użyciu programu PowerShell. kontener Hello obsługuje role sieci web i proces roboczy."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Użyj programu Azure PowerShell polecenie toocreate kontener usługi chmury pusty
W tym artykule opisano, jak tooquickly utworzyć kontener usługi w chmurze przy użyciu poleceń cmdlet programu Azure PowerShell. Wykonaj poniższe kroki hello:

1. Zainstaluj polecenia cmdlet programu PowerShell usługi Microsoft Azure hello z hello [programu Azure PowerShell pobierze](http://aka.ms/webpi-azps) strony.
2. Otwórz wiersz polecenia programu PowerShell hello.
3. Użyj hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign w.

   > [!NOTE]
   > Dodatkowe instrukcje dotyczące instalowania polecenia cmdlet programu Azure PowerShell hello i łączenie tooyour subskrypcji platformy Azure, można znaleźć zbyt[jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Użyj hello **New-AzureService** toocreate polecenia cmdlet kontener usługi chmury Azure puste.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Wykonaj to polecenie cmdlet hello tooinvoke przykład:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Aby uzyskać więcej informacji o tworzeniu hello usługi w chmurze Azure Uruchom polecenie:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Następne kroki
* Witaj toomanage wdrażania usługi w chmurze, można znaleźć toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), i [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) poleceń. Można również znaleźć zbyt[jak usługi w chmurze tooconfigure](cloud-services-how-to-configure.md) Aby uzyskać więcej informacji.
* toopublish usługi w chmurze projektu tooAzure, zapoznaj się toohello **PublishCloudService.ps1** przykładowy kod z [ciągłego dostarczania dla usługi w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).
