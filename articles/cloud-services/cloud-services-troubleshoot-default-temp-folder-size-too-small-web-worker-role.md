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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>Domyślny rozmiar folderu tymczasowego jest za mały dla roli sieć web/proces roboczy usługi chmury
Witaj domyślny katalog tymczasowy roli procesu roboczego lub sieci web usługi chmury ma maksymalny rozmiar 100 MB, co może stać się pełnej w pewnym momencie. W tym artykule opisano sposób tooavoid kończy się wolne miejsce na powitania katalogu tymczasowego.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Dlaczego zabraknie miejsca?
Hello standardowe zmiennych środowiskowych systemu Windows TEMP i TMP są dostępne toocode, działającej w aplikacji. Zarówno TEMP i TMP punktu tooa jeden katalog, który zawiera maksymalny rozmiar 100 MB. Wszystkie dane są przechowywane w tym katalogu nie jest zachowywany po cyklu życia hello hello usługi w chmurze; w przypadku odtwarzania hello wystąpień roli w usłudze w chmurze katalogu hello jest czyszczona.

## <a name="suggestion-toofix-hello-problem"></a>Sugestia toofix hello problem
Implementować jeden z następujących alternatyw hello:

* Konfigurowanie zasobów magazynu lokalnego, a dostęp do niego bezpośrednio zamiast TEMP lub TMP. tooaccess zasobu lokalnego magazynu z kodu uruchamianego w aplikacji, wywołanie hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metody.
* Konfigurowanie zasobów magazynu lokalnego, a punkt hello TEMP i TMP katalogów toopoint toohello ścieżka hello zasobu magazynu lokalnego. Ta modyfikacja powinny być wykonywane w ramach hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metody.

Witaj Poniższy przykładowy kod przedstawia sposób toomodify hello katalogów docelowy dla TEMP i TMP z wewnątrz metody OnStart hello:

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

## <a name="next-steps"></a>Następne kroki
Przeczytaj blog, który opisuje [jak tooincrease hello rozmiar hello folderu tymczasowego ASP.NET roli sieci Web Azure](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Wyświetl więcej [Rozwiązywanie problemów z artykułów](/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.

toolearn jak roli usługi w chmurze tootroubleshoot problemów przy użyciu danych diagnostyki Azure PaaS komputera, Wyświetl [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
