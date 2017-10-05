---
title: "Utwórz kontener usługi chmury przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak utworzyć kontener usługi chmury przy użyciu programu PowerShell. Kontener obsługuje role sieci web i proces roboczy."
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
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="4bdfb-104">Użyj polecenia programu Azure PowerShell, aby utworzyć kontener usługi chmury pusty</span><span class="sxs-lookup"><span data-stu-id="4bdfb-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="4bdfb-105">W tym artykule wyjaśniono, jak szybko utworzyć kontener usługi w chmurze przy użyciu poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4bdfb-106">Wykonaj poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="4bdfb-107">Zainstaluj polecenia cmdlet programu PowerShell usługi Microsoft Azure z [programu Azure PowerShell pobierze](http://aka.ms/webpi-azps) strony.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="4bdfb-108">Otwórz wiersz polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="4bdfb-109">Użyj [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) do logowania.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4bdfb-110">Dodatkowe instrukcje dotyczące instalowania polecenia cmdlet programu Azure PowerShell i nawiązywania połączenia z subskrypcją platformy Azure można znaleźć w temacie [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="4bdfb-111">Użyj **New-AzureService** , aby utworzyć kontener usługi chmury Azure puste.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="4bdfb-112">Wykonaj w tym przykładzie do wywołania polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="4bdfb-113">Aby uzyskać więcej informacji na temat tworzenia usługi w chmurze Azure Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="4bdfb-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4bdfb-114">Next steps</span></span>
* <span data-ttu-id="4bdfb-115">Aby zarządzać wdrażaniem usługi chmury, zapoznaj się [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), i [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) poleceń.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="4bdfb-116">Mogą również dotyczyć [sposób konfigurowania usługi w chmurze](cloud-services-how-to-configure.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="4bdfb-117">Aby opublikować projekt usługi w chmurze na platformie Azure, zobacz **PublishCloudService.ps1** przykładowy kod z [ciągłego dostarczania dla usługi w chmurze na platformie Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
