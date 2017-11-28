---
title: "Co się stało z projektu programu ASP.NET 5 (Visual Studio połączenia usług) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co się stanie po połączeniu z kontem magazynu platformy Azure w projekcie programu Visual Studio ASP.NET 5 za pomocą programu Visual Studio połączenia usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2a25c24fd7625374d269622a805f386fcd52bb5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="855ea-103">Co się stało z projektu programu ASP.NET 5 (Visual Studio usługi Azure Storage połączenia usług)?</span><span class="sxs-lookup"><span data-stu-id="855ea-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="855ea-104">Odwołania dodane</span><span class="sxs-lookup"><span data-stu-id="855ea-104">References added</span></span>
<span data-ttu-id="855ea-105">Pakiet NuGet magazynu Azure został dodany do projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="855ea-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="855ea-106">Ten pakiet zawiera następujące odwołania .NET:</span><span class="sxs-lookup"><span data-stu-id="855ea-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="855ea-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="855ea-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="855ea-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="855ea-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="855ea-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="855ea-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="855ea-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="855ea-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="855ea-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="855ea-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="855ea-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="855ea-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="855ea-113">**Dane systemowe**</span><span class="sxs-lookup"><span data-stu-id="855ea-113">**System.Data**</span></span>
* <span data-ttu-id="855ea-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="855ea-114">**System.Spatial**</span></span>

<span data-ttu-id="855ea-115">Ponadto pakiet NuGet **Microsoft.Framework.Configuration.Json** został dodany.</span><span class="sxs-lookup"><span data-stu-id="855ea-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="855ea-116">Parametry połączenia dla usługi Azure Storage dodane</span><span class="sxs-lookup"><span data-stu-id="855ea-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="855ea-117">W pliku config.json projektu element został utworzony z parametrów połączenia i kluczem konta magazynu wybranego.</span><span class="sxs-lookup"><span data-stu-id="855ea-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="855ea-118">Aby uzyskać więcej informacji, zobacz [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="855ea-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

