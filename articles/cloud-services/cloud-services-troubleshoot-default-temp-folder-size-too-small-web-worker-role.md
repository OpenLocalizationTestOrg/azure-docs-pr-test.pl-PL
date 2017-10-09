---
title: "rozmiar folderu tymczasowego aaaDefault jest za mały dla roli | Dokumentacja firmy Microsoft"
description: "Rola usługi chmury ma ograniczoną ilość miejsca na hello TEMP folder. Ten artykuł zawiera wskazówki dotyczące tooavoid kończy się wolne miejsce."
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
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="967c9-104">Domyślny rozmiar folderu tymczasowego jest za mały dla roli sieć web/proces roboczy usługi chmury</span><span class="sxs-lookup"><span data-stu-id="967c9-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="967c9-105">Witaj domyślny katalog tymczasowy roli procesu roboczego lub sieci web usługi chmury ma maksymalny rozmiar 100 MB, co może stać się pełnej w pewnym momencie.</span><span class="sxs-lookup"><span data-stu-id="967c9-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="967c9-106">W tym artykule opisano sposób tooavoid kończy się wolne miejsce na powitania katalogu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="967c9-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="967c9-107">Dlaczego zabraknie miejsca?</span><span class="sxs-lookup"><span data-stu-id="967c9-107">Why do I run out of space?</span></span>
<span data-ttu-id="967c9-108">Hello standardowe zmiennych środowiskowych systemu Windows TEMP i TMP są dostępne toocode, działającej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="967c9-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="967c9-109">Zarówno TEMP i TMP punktu tooa jeden katalog, który zawiera maksymalny rozmiar 100 MB.</span><span class="sxs-lookup"><span data-stu-id="967c9-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="967c9-110">Wszystkie dane są przechowywane w tym katalogu nie jest zachowywany po cyklu życia hello hello usługi w chmurze; w przypadku odtwarzania hello wystąpień roli w usłudze w chmurze katalogu hello jest czyszczona.</span><span class="sxs-lookup"><span data-stu-id="967c9-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="967c9-111">Sugestia toofix hello problem</span><span class="sxs-lookup"><span data-stu-id="967c9-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="967c9-112">Implementować jeden z następujących alternatyw hello:</span><span class="sxs-lookup"><span data-stu-id="967c9-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="967c9-113">Konfigurowanie zasobów magazynu lokalnego, a dostęp do niego bezpośrednio zamiast TEMP lub TMP.</span><span class="sxs-lookup"><span data-stu-id="967c9-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="967c9-114">tooaccess zasobu lokalnego magazynu z kodu uruchamianego w aplikacji, wywołanie hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="967c9-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="967c9-115">Konfigurowanie zasobów magazynu lokalnego, a punkt hello TEMP i TMP katalogów toopoint toohello ścieżka hello zasobu magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="967c9-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="967c9-116">Ta modyfikacja powinny być wykonywane w ramach hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="967c9-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="967c9-117">Witaj Poniższy przykładowy kod przedstawia sposób toomodify hello katalogów docelowy dla TEMP i TMP z wewnątrz metody OnStart hello:</span><span class="sxs-lookup"><span data-stu-id="967c9-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
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

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="967c9-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="967c9-118">Next steps</span></span>
<span data-ttu-id="967c9-119">Przeczytaj blog, który opisuje [jak tooincrease hello rozmiar hello folderu tymczasowego ASP.NET roli sieci Web Azure](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="967c9-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="967c9-120">Wyświetl więcej [Rozwiązywanie problemów z artykułów](/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="967c9-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="967c9-121">toolearn jak roli usługi w chmurze tootroubleshoot problemów przy użyciu danych diagnostyki Azure PaaS komputera, Wyświetl [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="967c9-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
