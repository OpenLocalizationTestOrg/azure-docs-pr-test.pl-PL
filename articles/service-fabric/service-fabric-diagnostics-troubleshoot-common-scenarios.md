---
title: "Rozwiązywanie problemów z śledzenie zdarzeń | Dokumentacja firmy Microsoft"
description: "Najczęściej występujących problemów podczas wdrażania usługi na usługi sieć szkieletowa usług Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Rozwiązywanie typowych problemów podczas wdrażania usługi w sieci szkieletowej usług Azure
Jeśli korzystasz z usług na komputerze dewelopera, jest łatwy w użyciu [narzędzia do debugowania programu Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). W przypadku klastrów zdalnego [raportów o kondycji](service-fabric-view-entities-aggregated-health.md) zawsze są dobrym miejscem do rozpoczęcia. Najprostszym sposobem dostęp do tych raportów jest za pomocą programu PowerShell lub [SFX](service-fabric-visualizing-your-cluster.md). W tym artykule założono, że debugowania zdalnego klastra i mieć podstawową wiedzę na temat sposobów użycia jednej z tych narzędzi.

## <a name="application-crash"></a>Awarii aplikacji
"Partycji jest poniżej docelowa liczba repliki lub wystąpienie" raport jest wskazuje, że usługa uległa awarii. Aby dowiedzieć się, gdy awarii usługi ma nieco więcej dochodzenia. Kiedy usługa jest uruchomiona na dużą skalę, Twój najlepszy przyjaciel zostanie zestaw dobrze przemyślany śladów.  Zalecamy wypróbowanie [diagnostyki Azure](service-fabric-diagnostics-how-to-setup-wad.md) zbierania tych danych śledzenia i przy użyciu rozwiązania, takie jak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) do przeglądania i wyszukiwanie dane śledzenia.

![SFX partycji kondycji](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Podczas inicjowania usługi lub aktora
Wszelkie wyjątki przed zainicjowaniem typu usługi spowoduje, że proces awarii. W przypadku tych typów awarii w dzienniku zdarzeń aplikacji zostaną wyświetlone błędu z usługi.
Są to najczęściej wyjątki, aby zobaczyć przed zainicjowaniem usługi.

***System.IO.FileNotFoundException***

Ten błąd jest często z powodu braku zależności zestawu. Sprawdź właściwość CopyLocal w Visual Studio lub w globalnej pamięci podręcznej zestawów dla węzła.

***System.Runtime.InteropServices.COMException*** *w System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Oznacza to, że nazwa typu zarejestrowanej usługi nie jest zgodna manifestu usługi.

[Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md) można skonfigurować, aby automatycznie przekazać wszystkie węzły w dzienniku zdarzeń aplikacji.

### <a name="runasync-or-onactivateasync"></a>RunAsync() lub OnActivateAsync()
W przypadku awarii podczas inicjowania lub systemem typu zarejestrowanej usługi lub aktora, wyjątek zostanie przechwycony przez sieć szkieletowa usług Azure. Możesz wyświetlić te od dostawców EventSource szczegółowo opisane w sekcji "Następne kroki".

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o istniejące dane diagnostyczne udostępniane przez usługi sieć szkieletowa usług:

* [Niezawodne diagnostyki złośliwych użytkowników](service-fabric-reliable-actors-diagnostics.md)
* [Niezawodne usługi diagnostyki](service-fabric-reliable-services-diagnostics.md)

