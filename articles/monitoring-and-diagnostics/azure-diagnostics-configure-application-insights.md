---
title: aaaConfigure diagnostyki Azure toosend danych tooApplication Insights | Dokumentacja firmy Microsoft
description: "Zaktualizuj hello Azure Diagnostics publicznej konfiguracji toosend danych tooApplication szczegółowych informacji."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Usługi w chmurze maszyny wirtualnej i sieci szkieletowej usług danych diagnostycznych tooApplication Insights wysyłania
Usługi w chmurze, maszyn wirtualnych, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług wszystkich Użyj hello Azure Diagnostics rozszerzenia toocollect danych.  Diagnostyka Azure wysyła tooAzure danych magazynu tabel.  Można jednak również potoku wszystkie lub podzbiór lokalizacje tooother danych hello przy użyciu rozszerzenia diagnostyki Azure w wersji 1.5 lub nowszego.

W tym artykule opisano, jak dane toosend z hello Azure Diagnostics rozszerzenia tooApplication szczegółowych informacji.

## <a name="diagnostics-configuration-explained"></a>Wyjaśniono konfiguracji diagnostyki
wychwytywanie rozszerzenia 1.5 wprowadzone diagnostyki Azure Hello, które są dodatkowe lokalizacje, w którym może wysyłać dane diagnostyczne.

Przykład konfiguracji zbiorniku dla usługi Application Insights:

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- Witaj **zbiornika** *nazwa* atrybut jest wartość ciągu, który unikatowo identyfikuje zbiornika hello.

- Witaj **ApplicationInsights** element określa klucz Instrumentacji hello zasobu usługi Application insights wysyłania hello dane diagnostyczne platformy Azure.
    - Jeśli nie masz istniejący zasób usługi Application Insights, zobacz [utworzyć nowy zasób usługi Application Insights](../application-insights/app-insights-create-new-resource.md) Aby uzyskać więcej informacji na temat tworzenia zasobu i pobierania klucza Instrumentacji hello.
    - Jeśli tworzysz usługi w chmurze z Azure SDK 2.8 i nowsze, ten klucz Instrumentacji jest wypełniane automatycznie. wartość Hello jest oparta na powitania **APPINSIGHTS_INSTRUMENTATIONKEY** ustawienie konfiguracyjne usługi podczas pakowania hello projektu usługi w chmurze. Zobacz [wystawia usługi w chmurze Użyj usługi Application Insights z diagnostyki Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Witaj **kanałów** elementu zawiera jeden lub więcej **kanału** elementów.
    - Witaj *nazwa* jednoznacznie odnosi się toothat kanału.
    - Witaj *loglevel* atrybutu pozwala określić umożliwia hello poziom dziennika, który hello kanału. poziomy rejestrowania dostępne Hello w kolejności większość informacji tooleast są:
        - Pełne
        - Informacje
        - Ostrzeżenie
        - Błąd
        - Krytyczne

Kanał działa jak filtr i pozwala określonego dziennika tooselect poziomy toohello toosend docelowej obiekt sink. Można na przykład zbierania pełnych dzienników i wysyłać je toostorage, ale wysłać tylko błędy toohello ujścia.

Witaj poniższy rysunek przedstawia tę relację.

![Publiczna Konfiguracja diagnostyki](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

powitania po grafiki znajduje się podsumowanie wartości konfiguracji hello i jak działają. W konfiguracji hello na różnych poziomach hierarchii hello może zawierać wiele wychwytywanie. zbiornik Hello na najwyższym poziomie hello działa jako ustawienie globalne i hello jeden określony w poszczególnych hello element działa jak ustawienie globalne toothat do zastąpienia.

![Diagnostyka wychwytywanie konfiguracji z usługą Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Przykład konfiguracji zbiornika ukończone
W tym miejscu jest kompletnym przykładem hello publicznej konfiguracji pliku
1. wysyła wszystkie błędy tooApplication Insights (określone na powitania **DiagnosticMonitorConfiguration** węzła)
2. wysyła również pełne poziomu dzienniki hello Dzienniki aplikacji (określone na powitania **dzienniki** węzła).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
W poprzedniej konfiguracji hello hello następujące wiersze mają następujące znaczenie hello:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Wyślij wszystkie dane hello, które jest zbieranych przez Diagnostyka Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Wyślij tylko błąd dzienniki toohello usługi Application Insights odbioru

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Wyślij dzienniki pełne application tooApplication Insights

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Ograniczenia

- **Kanały zalogować się wyłącznie liczniki wydajności nie i typu.** Jeśli określisz kanał z elementem licznika wydajności jest ignorowana.
- **poziom dziennika Hello kanału nie może przekraczać hello poziom dziennika co zbieranych przez diagnostycznych platformy Azure.** Na przykład nie można gromadzić błędy w dzienniku aplikacji w elemencie dzienniki hello i spróbuj toosend pełne dzienniki toohello szczegółowe informacje o aplikacji ujścia. Witaj *scheduledTransferLogLevelFilter* atrybutów zawsze należy zebrać takie same lub więcej dzienników niż hello loguje użytkownika próbujesz toosend tooa ujścia.
- **Nie można wysłać obiektu blob danych zbieranych przez tooApplication rozszerzenia diagnostyki Azure szczegółowych informacji.** Na przykład niczego określone w obszarze hello *katalogów* węzła. Zrzuty awaryjne zrzutu awaryjnego rzeczywiste hello są wysyłane tooblob magazynu i został wygenerowany tylko powiadomienie, które hello zrzutu awaryjnego są wysyłane tooApplication szczegółowych informacji.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[wyświetlania informacji diagnostycznych platformy Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) w usłudze Application Insights.
* Użyj [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello rozszerzenia diagnostyki Azure dla aplikacji.
* Użyj [programu Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello rozszerzenia diagnostyki Azure dla aplikacji
