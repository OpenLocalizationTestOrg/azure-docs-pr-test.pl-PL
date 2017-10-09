---
title: "aaaTroubleshooting z śledzenie zdarzeń | Dokumentacja firmy Microsoft"
description: "Witaj najczęściej występujących problemów podczas wdrażania usługi na usługi sieć szkieletowa usług Microsoft Azure."
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
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Rozwiązywanie typowych problemów podczas wdrażania usługi w sieci szkieletowej usług Azure
Jeśli korzystasz z usług na komputerze dewelopera, jest łatwe toouse [narzędzia do debugowania programu Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). W przypadku klastrów zdalnego [raportów o kondycji](service-fabric-view-entities-aggregated-health.md) są zawsze toostart dobrym miejscem. Witaj najprostszym tooaccess sposoby te raporty są za pomocą programu PowerShell lub [SFX](service-fabric-visualizing-your-cluster.md). W tym artykule założono, że debugowania zdalnego klastra i mieć podstawową wiedzę na temat tego, jak toouse jednego z tych narzędzi.

## <a name="application-crash"></a>Awarii aplikacji
Witaj "partycji jest poniżej docelowa liczba repliki lub wystąpienie" raport jest wskazuje, że usługa uległa awarii. toofind się, gdy awarii usługi ma nieco więcej dochodzenia. Kiedy usługa jest uruchomiona na dużą skalę, Twój najlepszy przyjaciel zostanie zestaw dobrze przemyślany śladów.  Zalecamy wypróbowanie [diagnostyki Azure](service-fabric-diagnostics-how-to-setup-wad.md) zbierania tych danych śledzenia i przy użyciu rozwiązania, takie jak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) do przeglądania i wyszukiwanie hello śladów.

![SFX partycji kondycji](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Podczas inicjowania usługi lub aktora
Wszelkie wyjątki przed zainicjowaniem hello typ usługi spowoduje, że hello toocrash procesu. Dla tego typu awarii (Crash) w dzienniku zdarzeń aplikacji hello wyświetli błąd hello z usługi.
Są to najczęściej toosee wyjątki hello przed zainicjowaniem hello usługi.

***System.IO.FileNotFoundException***

Ten błąd jest często powodu toomissing zależności zestawu. Sprawdź właściwość CopyLocal hello w Visual Studio lub hello Globalna pamięć podręczna zestawów hello węzła.

***System.Runtime.InteropServices.COMException*** *w System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Oznacza to, że nazwa typu usługi zarejestrowanych hello jest niezgodna z hello manifestu usługi.

[Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md) mogą być automatycznie dziennik zdarzeń aplikacji hello tooupload skonfigurowanych dla wszystkich węzłów.

### <a name="runasync-or-onactivateasync"></a>RunAsync() lub OnActivateAsync()
W przypadku awarii hello odbywa się podczas inicjowania hello lub systemem typu zarejestrowanej usługi lub aktora, hello wyjątek zostanie przechwycony przez sieć szkieletowa usług Azure. Możesz wyświetlić te od dostawców EventSource hello szczegółowo opisane w sekcji "Następne kroki" hello.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o istniejące dane diagnostyczne udostępniane przez usługi sieć szkieletowa usług:

* [Niezawodne diagnostyki złośliwych użytkowników](service-fabric-reliable-actors-diagnostics.md)
* [Niezawodne usługi diagnostyki](service-fabric-reliable-services-diagnostics.md)

