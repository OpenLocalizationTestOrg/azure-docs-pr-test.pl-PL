---
title: "Przepływ hello aaaTrace w aplikacji usługi w chmurze z diagnostyki Azure | Dokumentacja firmy Microsoft"
description: "Dodaj śledzenie wiadomości tooan aplikacji Azure toohelp debugowania, pomiaru wydajności, monitorowania, analizy ruchu i innych."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Przepływ hello śledzenia aplikacji usługi w chmurze Diagnostyka Azure
Śledzenie jest sposób możesz toomonitor hello wykonanie aplikacji jest uruchomiona. Można użyć hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), i [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) klasy toorecord informacje o błędach i wykonanie aplikacji w dzienniki, pliki tekstowe lub innych urządzeń w celu późniejszej analizy. Aby uzyskać więcej informacji dotyczących śledzenia, zobacz [śledzenie i Instrumentacja aplikacji](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>Użyj instrukcji śledzenia i przełączniki śledzenia
Implementowanie śledzenia w aplikacji usługi w chmurze, dodając hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello konfigurację aplikacji i podejmowania wywołuje tooSystem.Diagnostics.Trace lub System.Diagnostics.Debug w sieci Kod aplikacji. Użyj pliku konfiguracji hello *app.config* dla roli proces roboczy i hello *web.config* ról sieci web. Jeśli utworzysz nową usługę hostowaną przy użyciu szablonu programu Visual Studio, diagnostyki Azure zostanie automatycznie dodany projekt toohello i hello DiagnosticMonitorTraceListener zostanie dodany plik odpowiednia konfiguracja toohello hello ról, które można dodać.

Aby uzyskać informacje na umieszczenie instrukcji śledzenia, zobacz [porady: Dodawanie instrukcji śledzenia tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).

Przez umieszczenie [przełączniki śledzenia](https://msdn.microsoft.com/library/3at424ac.aspx) w kodzie, można kontrolować czy występuje śledzenia i jest ich zakresu. Dzięki temu można monitorować stan hello aplikacji w środowisku produkcyjnym. Jest to szczególnie ważne w aplikacji biznesowych, która używa wielu składniki działające na wielu komputerach. Aby uzyskać więcej informacji, zobacz [porady: Konfigurowanie przełączników śledzenia](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Skonfiguruj odbiornik śledzenia hello w aplikacji Azure
Śledzenie debugowania i TraceSource, wymagają ustawić toocollect "odbiorników" i wiadomości powitania rekordów, które są wysyłane. Odbiorniki zbierania, przechowywania i wiadomości śledzenia trasy. Bezpośrednie one hello śledzenie wyjściowego tooan odpowiednie miejsca docelowego, takich jak dziennika, okna lub plik tekstowy. Diagnostyka Azure używa hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) klasy.

Przed wykonaniem procedury hello należy zainicjować hello Azure monitora diagnostycznego. toodo tego, zobacz [Włączanie diagnostyki w Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Zauważ, że jeśli używasz hello szablonów, które są dostarczane przez program Visual Studio hello konfiguracji odbiornika hello jest dodawane automatycznie dla Ciebie.

### <a name="add-a-trace-listener"></a>Dodać obiektu nasłuchującego śledzenia
1. Otwórz plik web.config lub app.config powitania dla roli użytkownika.
2. Dodaj hello następującego pliku toohello kodu. Zmienić hello atrybutu toouse hello wersji numer wersji zestawu hello, do którego się odwołujesz. Wersja zestawu Hello nie musi zmienia się w każdej wersji zestawu Azure SDK, chyba, że istnieją aktualizacje tooit.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Upewnij się, że masz toohello odwołania projektu Microsoft.WindowsAzure.Diagnostics zestawu. Numer wersji hello aktualizacja w kodzie xml hello powyżej toomatch wersji hello hello odwołuje się do zestawu Microsoft.WindowsAzure.Diagnostics.
   > 
   > 
3. Zapisz plik konfiguracji hello.

Aby uzyskać więcej informacji na temat odbiorników, zobacz [obiektów nasłuchujących śledzenia](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Po ukończeniu hello kroki tooadd hello odbiornika, można dodać kod tooyour instrukcji śledzenia.

### <a name="tooadd-trace-statement-tooyour-code"></a>Kod tooyour instrukcji śledzenia tooadd
1. Otwórz plik źródłowy dla aplikacji. Na przykład Witaj <RoleName>plik CS roli procesu roboczego hello lub roli sieci web.
2. Dodaj następujące hello za pomocą instrukcji, jeśli nie został już dodany:
    ```
        using System.Diagnostics;
    ```
3. Dodawanie instrukcji śledzenia, w których mają toocapture informacje o stanie hello aplikacji. Można użyć różnych metod tooformat hello dane wyjściowe hello instrukcja śledzenia. Aby uzyskać więcej informacji, zobacz [porady: Dodawanie instrukcji śledzenia tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Zapisz plik źródłowy hello.

