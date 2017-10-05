---
title: "Domyślny rozmiar folderu tymczasowego jest za mały dla roli | Dokumentacja firmy Microsoft"
description: "Rola usługi chmury ma ograniczoną ilość miejsca do folderu tymczasowego. Ten artykuł zawiera wskazówki dotyczące zapobiegania wyczerpaniu miejsca."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="7a75b-104">Domyślny rozmiar folderu tymczasowego jest za mały dla roli sieć web/proces roboczy usługi chmury</span><span class="sxs-lookup"><span data-stu-id="7a75b-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="7a75b-105">Domyślny katalog tymczasowy roli procesu roboczego lub sieci web usługi chmury ma maksymalny rozmiar 100 MB, co może stać się pełna w pewnym momencie.</span><span class="sxs-lookup"><span data-stu-id="7a75b-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="7a75b-106">W tym artykule opisano sposób zapobiega wyczerpaniu się miejsce dla katalogu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="7a75b-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="7a75b-107">Dlaczego zabraknie miejsca?</span><span class="sxs-lookup"><span data-stu-id="7a75b-107">Why do I run out of space?</span></span>
<span data-ttu-id="7a75b-108">Standardowa zmiennych środowiskowych systemu Windows TEMP i TMP są dostępne dla kodu uruchamianego w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a75b-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="7a75b-109">Zarówno TEMP i TMP wskaż jeden katalog, który zawiera maksymalny rozmiar 100 MB.</span><span class="sxs-lookup"><span data-stu-id="7a75b-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="7a75b-110">Wszystkie dane są przechowywane w tym katalogu nie jest zachowywany po cyklem życia usługi w chmurze; Jeśli wystąpień roli w usłudze w chmurze są odzyskiwane, katalog jest czyszczona.</span><span class="sxs-lookup"><span data-stu-id="7a75b-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="7a75b-111">Aby rozwiązać ten problem</span><span class="sxs-lookup"><span data-stu-id="7a75b-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="7a75b-112">Implementować jeden z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="7a75b-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="7a75b-113">Konfigurowanie zasobów magazynu lokalnego, a dostęp do niego bezpośrednio zamiast TEMP lub TMP.</span><span class="sxs-lookup"><span data-stu-id="7a75b-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="7a75b-114">Aby uzyskać dostęp do zasobów magazynu lokalnego z kodu uruchamianego w aplikacji, należy wywołać [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="7a75b-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="7a75b-115">Konfigurowanie zasobów magazynu lokalnego, a punkt katalogów TEMP i TMP wskaż ścieżkę do zasobu magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="7a75b-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="7a75b-116">Ta modyfikacja powinny być wykonywane w ramach [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="7a75b-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="7a75b-117">Następujący przykładowy kod przedstawia sposób modyfikowania katalogów docelowych TEMP i TMP z wewnątrz metody OnStart:</span><span class="sxs-lookup"><span data-stu-id="7a75b-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7a75b-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a75b-118">Next steps</span></span>
<span data-ttu-id="7a75b-119">Przeczytaj blog, który opisuje [jak zwiększyć rozmiar folderu Azure Web roli ASP.NET tymczasowego](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a75b-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="7a75b-120">Wyświetl więcej [Rozwiązywanie problemów z artykułów](/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7a75b-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="7a75b-121">Aby dowiedzieć się, jak rozwiązywać problemy roli usługi w chmurze przy użyciu danych diagnostycznych Azure PaaS komputera, Wyświetl [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a75b-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
