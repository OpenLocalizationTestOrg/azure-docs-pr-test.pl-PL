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
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="4bd88-104">Użyj programu Azure PowerShell polecenie toocreate kontener usługi chmury pusty</span><span class="sxs-lookup"><span data-stu-id="4bd88-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="4bd88-105">W tym artykule opisano, jak tooquickly utworzyć kontener usługi w chmurze przy użyciu poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4bd88-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4bd88-106">Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4bd88-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="4bd88-107">Zainstaluj polecenia cmdlet programu PowerShell usługi Microsoft Azure hello z hello [programu Azure PowerShell pobierze](http://aka.ms/webpi-azps) strony.</span><span class="sxs-lookup"><span data-stu-id="4bd88-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="4bd88-108">Otwórz wiersz polecenia programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="4bd88-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="4bd88-109">Użyj hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign w.</span><span class="sxs-lookup"><span data-stu-id="4bd88-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4bd88-110">Dodatkowe instrukcje dotyczące instalowania polecenia cmdlet programu Azure PowerShell hello i łączenie tooyour subskrypcji platformy Azure, można znaleźć zbyt[jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bd88-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="4bd88-111">Użyj hello **New-AzureService** toocreate polecenia cmdlet kontener usługi chmury Azure puste.</span><span class="sxs-lookup"><span data-stu-id="4bd88-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="4bd88-112">Wykonaj to polecenie cmdlet hello tooinvoke przykład:</span><span class="sxs-lookup"><span data-stu-id="4bd88-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="4bd88-113">Aby uzyskać więcej informacji o tworzeniu hello usługi w chmurze Azure Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="4bd88-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="4bd88-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4bd88-114">Next steps</span></span>
* <span data-ttu-id="4bd88-115">Witaj toomanage wdrażania usługi w chmurze, można znaleźć toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), i [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) poleceń.</span><span class="sxs-lookup"><span data-stu-id="4bd88-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="4bd88-116">Można również znaleźć zbyt[jak usługi w chmurze tooconfigure](cloud-services-how-to-configure.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="4bd88-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="4bd88-117">toopublish usługi w chmurze projektu tooAzure, zapoznaj się toohello **PublishCloudService.ps1** przykładowy kod z [ciągłego dostarczania dla usługi w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="4bd88-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
