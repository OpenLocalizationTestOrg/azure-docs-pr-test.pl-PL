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
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="131e8-103">Przepływ hello śledzenia aplikacji usługi w chmurze Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="131e8-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="131e8-104">Śledzenie jest sposób możesz toomonitor hello wykonanie aplikacji jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="131e8-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="131e8-105">Można użyć hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), i [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) klasy toorecord informacje o błędach i wykonanie aplikacji w dzienniki, pliki tekstowe lub innych urządzeń w celu późniejszej analizy.</span><span class="sxs-lookup"><span data-stu-id="131e8-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="131e8-106">Aby uzyskać więcej informacji dotyczących śledzenia, zobacz [śledzenie i Instrumentacja aplikacji](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="131e8-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="131e8-107">Użyj instrukcji śledzenia i przełączniki śledzenia</span><span class="sxs-lookup"><span data-stu-id="131e8-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="131e8-108">Implementowanie śledzenia w aplikacji usługi w chmurze, dodając hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello konfigurację aplikacji i podejmowania wywołuje tooSystem.Diagnostics.Trace lub System.Diagnostics.Debug w sieci Kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="131e8-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="131e8-109">Użyj pliku konfiguracji hello *app.config* dla roli proces roboczy i hello *web.config* ról sieci web.</span><span class="sxs-lookup"><span data-stu-id="131e8-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="131e8-110">Jeśli utworzysz nową usługę hostowaną przy użyciu szablonu programu Visual Studio, diagnostyki Azure zostanie automatycznie dodany projekt toohello i hello DiagnosticMonitorTraceListener zostanie dodany plik odpowiednia konfiguracja toohello hello ról, które można dodać.</span><span class="sxs-lookup"><span data-stu-id="131e8-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="131e8-111">Aby uzyskać informacje na umieszczenie instrukcji śledzenia, zobacz [porady: Dodawanie instrukcji śledzenia tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="131e8-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="131e8-112">Przez umieszczenie [przełączniki śledzenia](https://msdn.microsoft.com/library/3at424ac.aspx) w kodzie, można kontrolować czy występuje śledzenia i jest ich zakresu.</span><span class="sxs-lookup"><span data-stu-id="131e8-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="131e8-113">Dzięki temu można monitorować stan hello aplikacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="131e8-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="131e8-114">Jest to szczególnie ważne w aplikacji biznesowych, która używa wielu składniki działające na wielu komputerach.</span><span class="sxs-lookup"><span data-stu-id="131e8-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="131e8-115">Aby uzyskać więcej informacji, zobacz [porady: Konfigurowanie przełączników śledzenia](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="131e8-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="131e8-116">Skonfiguruj odbiornik śledzenia hello w aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="131e8-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="131e8-117">Śledzenie debugowania i TraceSource, wymagają ustawić toocollect "odbiorników" i wiadomości powitania rekordów, które są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="131e8-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="131e8-118">Odbiorniki zbierania, przechowywania i wiadomości śledzenia trasy.</span><span class="sxs-lookup"><span data-stu-id="131e8-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="131e8-119">Bezpośrednie one hello śledzenie wyjściowego tooan odpowiednie miejsca docelowego, takich jak dziennika, okna lub plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="131e8-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="131e8-120">Diagnostyka Azure używa hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="131e8-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="131e8-121">Przed wykonaniem procedury hello należy zainicjować hello Azure monitora diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="131e8-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="131e8-122">toodo tego, zobacz [Włączanie diagnostyki w Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="131e8-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="131e8-123">Zauważ, że jeśli używasz hello szablonów, które są dostarczane przez program Visual Studio hello konfiguracji odbiornika hello jest dodawane automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="131e8-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="131e8-124">Dodać obiektu nasłuchującego śledzenia</span><span class="sxs-lookup"><span data-stu-id="131e8-124">Add a trace listener</span></span>
1. <span data-ttu-id="131e8-125">Otwórz plik web.config lub app.config powitania dla roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="131e8-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="131e8-126">Dodaj hello następującego pliku toohello kodu.</span><span class="sxs-lookup"><span data-stu-id="131e8-126">Add hello following code toohello file.</span></span> <span data-ttu-id="131e8-127">Zmienić hello atrybutu toouse hello wersji numer wersji zestawu hello, do którego się odwołujesz.</span><span class="sxs-lookup"><span data-stu-id="131e8-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="131e8-128">Wersja zestawu Hello nie musi zmienia się w każdej wersji zestawu Azure SDK, chyba, że istnieją aktualizacje tooit.</span><span class="sxs-lookup"><span data-stu-id="131e8-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
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
   > <span data-ttu-id="131e8-129">Upewnij się, że masz toohello odwołania projektu Microsoft.WindowsAzure.Diagnostics zestawu.</span><span class="sxs-lookup"><span data-stu-id="131e8-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="131e8-130">Numer wersji hello aktualizacja w kodzie xml hello powyżej toomatch wersji hello hello odwołuje się do zestawu Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="131e8-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="131e8-131">Zapisz plik konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="131e8-131">Save hello config file.</span></span>

<span data-ttu-id="131e8-132">Aby uzyskać więcej informacji na temat odbiorników, zobacz [obiektów nasłuchujących śledzenia](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="131e8-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="131e8-133">Po ukończeniu hello kroki tooadd hello odbiornika, można dodać kod tooyour instrukcji śledzenia.</span><span class="sxs-lookup"><span data-stu-id="131e8-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="131e8-134">Kod tooyour instrukcji śledzenia tooadd</span><span class="sxs-lookup"><span data-stu-id="131e8-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="131e8-135">Otwórz plik źródłowy dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="131e8-135">Open a source file for your application.</span></span> <span data-ttu-id="131e8-136">Na przykład Witaj <RoleName>plik CS roli procesu roboczego hello lub roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="131e8-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="131e8-137">Dodaj następujące hello za pomocą instrukcji, jeśli nie został już dodany:</span><span class="sxs-lookup"><span data-stu-id="131e8-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="131e8-138">Dodawanie instrukcji śledzenia, w których mają toocapture informacje o stanie hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="131e8-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="131e8-139">Można użyć różnych metod tooformat hello dane wyjściowe hello instrukcja śledzenia.</span><span class="sxs-lookup"><span data-stu-id="131e8-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="131e8-140">Aby uzyskać więcej informacji, zobacz [porady: Dodawanie instrukcji śledzenia tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="131e8-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="131e8-141">Zapisz plik źródłowy hello.</span><span class="sxs-lookup"><span data-stu-id="131e8-141">Save hello source file.</span></span>

