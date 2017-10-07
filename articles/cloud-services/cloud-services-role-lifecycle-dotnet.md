---
title: "zdarzenia cyklu życia usługi w chmurze aaaHandle | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak metod cyklu życia hello roli usługi w chmurze można użyć w .NET"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Dostosowywanie hello cyklu życia roli sieci Web lub procesu roboczego w programie .NET
Podczas tworzenia roli procesu roboczego rozszerzyć hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) klasy, która udostępnia metody dla Ciebie toooverride, które umożliwiają odpowiadać toolifecycle zdarzenia. Dla ról sieć web ta klasa jest opcjonalne, trzeba używać toorespond toolifecycle zdarzenia.

## <a name="extend-hello-roleentrypoint-class"></a>Rozszerzenie klasy RoleEntryPoint hello
Hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) klasa zawiera metody, które są wywoływane przez platformę Azure podczas jego **uruchamia**, **uruchamia**, lub **zatrzymuje** roli sieci web lub procesu roboczego. Opcjonalnie można zastąpić te metody toomanage roli inicjowania, roli zamknięcia sekwencji lub wątku wykonawczego hello hello roli. 

Podczas rozszerzania **RoleEntryPoint**, należy zwrócić uwagę hello następujące zachowania hello metod:

* Witaj [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) i [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) metody zwracać wartość logiczną, dzięki czemu możliwe tooreturn **false** z tych metod.
  
   Jeśli kod zwraca **false**, proces roli hello nagle jest zakończony, bez konieczności uruchamiania żadnych zamykania może być w miejscu. Ogólnie rzecz biorąc, należy unikać zwracanie **false** z hello **OnStart** metody.
* Wszelkie nieprzechwycony wyjątek w obrębie przeciążenia **RoleEntryPoint** metoda jest traktowana jako nieobsługiwany wyjątek.
  
   Jeśli wystąpi wyjątek w jednej z metod cyklu życia hello, Azure zostanie podniesiony hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) zdarzenia, a następnie hello proces jest zakończony. Po roli użytkownika został przełączony w tryb offline, zostanie ono uruchomione na platformie Azure. Gdy wystąpił nieobsługiwany wyjątek wystąpi, hello [zatrzymywanie](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) zdarzenie nie jest wywoływane i hello **OnStop** nie jest wywoływana metoda.

Roli użytkownika nie uruchamia się, czy jest odtwarzania między hello inicjowania stanów zajęty i zatrzymywanie, kod może zgłaszanie nieobsługiwany wyjątek w ramach jednej zdarzenia cyklu życia hello każdej roli hello czasu ponownym uruchomieniem. W takim przypadku należy użyć hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) toodetermine zdarzeń hello przyczyną hello wyjątku i odpowiednią obsługę. Roli użytkownika może być również zwracanie z hello [Uruchom](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodę, która powoduje, że hello toorestart roli. Aby uzyskać więcej informacji na temat stanów wdrożenia, zobacz [tooRecycle typowe problemy z którego przyczyna role](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Jeśli używasz hello **Azure Tools dla programu Microsoft Visual Studio** toodevelop aplikacji, szablony projektu roli hello automatyczne rozszerzanie hello **RoleEntryPoint** klasy, w hello *WebRole.cs* i *WorkerRole.cs* plików.
> 
> 

## <a name="onstart-method"></a>OnStart — metoda
Witaj **OnStart** metoda jest wywoływana, gdy wystąpienie roli w tryb online na platformie Azure. Podczas wykonywania hello kodu OnStart wystąpienia roli hello jest oznaczony jako **zajęty** i nie ruch zewnętrzny zostanie ukierunkowanej tooit przez hello równoważenia obciążenia. Można zastąpić ten — metoda tooperform inicjowania pracy, takich jak wdrażanie programów obsługi zdarzeń i uruchamianie [diagnostyki Azure](cloud-services-how-to-monitor.md).

Jeśli **OnStart** zwraca **true**, pomyślnie zainicjowano wystąpienia hello i wywołuje Azure hello **RoleEntryPoint.Run** metody. Jeśli **OnStart** zwraca **false**, roli hello natychmiast kończy się bez wykonania dowolnego planowanego zamknięcia sekwencji.

Witaj, jak po przedstawia przykładowy kod toooverride hello **OnStart** metody. Ta metoda umożliwia skonfigurowanie i rozpoczyna się monitora diagnostycznego w momencie wystąpienia roli hello uruchamia i konfiguruje transfer rejestrowania konta magazynu tooa danych:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>OnStop — metoda
Witaj **OnStop** metoda jest wywoływana po wystąpienia roli została podjęta w trybie offline przez platformę Azure i przed hello proces kończy się. Można zastąpić ten kod toocall metody wymagane dla Twojego toocleanly wystąpienia roli zamknięta.

> [!IMPORTANT]
> Kodu uruchamianego w hello **OnStop** metoda ma toofinish ograniczony czas, gdy jest wywoływana z powodów innych niż zamknięcia zainicjowanego przez użytkownika. Po upływie tego czasu, hello proces jest zakończony, dlatego należy się upewnić, że kod w hello **OnStop** metody można szybko uruchomić lub zaakceptować toocompletion nie jest uruchomiony. Witaj **OnStop** metoda jest wywoływana po wykonaniu hello **zatrzymywanie** zdarzenia.
> 
> 

## <a name="run-method"></a>Run — metoda
Można zastąpić hello **Uruchom** tooimplement metody wątku długotrwałe dla swojego wystąpienia roli.

Zastępowanie hello **Uruchom** — metoda nie jest wymagana; hello Domyślna implementacja uruchamia wątku, który jest w stanie uśpienia nieskończona. Jeśli zastąpienie hello **Uruchom** metody kodu powinna zablokować nieskończoność. Jeśli hello **Uruchom** metoda zwróci wartość, automatycznie bezpiecznie odtworzeniem roli hello; innymi słowy, zgłasza Azure hello **zatrzymywanie** hello zdarzeń i wywołania **OnStop** metody tak czy sekwencjach zamknięcia mogą być wykonywane przed hello roli do trybu offline.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Implementacja metody cyklu życia ASP.NET hello roli sieci web
Można używać metod cyklu życia ASP.NET hello, oprócz toothose podał hello **RoleEntryPoint** klasy toomanage inicjowania i zamknięcie sekwencji dla roli sieci web. Może to być przydatne do celów zgodności, jeśli są Przenoszenie istniejących tooAzure aplikacji ASP.NET. metody cyklu życia ASP.NET Hello zostaną wywołane wewnątrz hello **RoleEntryPoint** metody. Witaj **aplikacji\_Start** metoda jest wywoływana po wykonaniu hello **RoleEntryPoint.OnStart** zakończeniu działania metody. Witaj **aplikacji\_zakończenia** metoda jest wywoływana przed hello **RoleEntryPoint.OnStop** metoda jest wywoływana.

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[Utwórz pakiet usługi chmury](cloud-services-model-and-package.md).

