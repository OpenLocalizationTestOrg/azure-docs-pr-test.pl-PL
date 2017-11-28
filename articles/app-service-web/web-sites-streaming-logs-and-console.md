---
title: Dzienniki aaaStreaming i konsoli
description: "Omówienie konsoli i dzienniki przesyłania strumieniowego"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="def9a-103">Dzienniki przesyłania strumieniowego i hello konsoli</span><span class="sxs-lookup"><span data-stu-id="def9a-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="def9a-104">Dzienniki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="def9a-104">Streaming Logs</span></span>
<span data-ttu-id="def9a-105">Witaj **portalu Azure** zapewnia zintegrowane przesyłania strumieniowego przeglądarka dzienników, który umożliwia wyświetlanie zdarzenia śledzenia z Twojej **usługi aplikacji** aplikacji w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="def9a-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="def9a-106">Konfigurowanie tej funkcji wymaga kilku prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="def9a-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="def9a-107">Zapisuj śledzenia w kodzie</span><span class="sxs-lookup"><span data-stu-id="def9a-107">Write traces in your code</span></span>
* <span data-ttu-id="def9a-108">Włączanie aplikacji **dzienników diagnostycznych** dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="def9a-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="def9a-109">Widok hello strumienia z wbudowanych hello **dzienniki przesyłania strumieniowego** interfejsu użytkownika w hello **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="def9a-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="def9a-110">Jak toowrite służy do śledzenia w kodzie</span><span class="sxs-lookup"><span data-stu-id="def9a-110">How toowrite traces in your code</span></span>
<span data-ttu-id="def9a-111">Zapisywanie danych śledzenia w kodzie jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="def9a-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="def9a-112">W języku C# jest tak proste, jak zapisywania hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="def9a-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="def9a-113">Witaj klasy śledzenia znajduje się w przestrzeni nazw System.Diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="def9a-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="def9a-114">W aplikacji node.js można napisać ten kod tooachieve hello takiego samego wyniku:</span><span class="sxs-lookup"><span data-stu-id="def9a-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="def9a-115">Jak tooenable i widoku hello dzienniki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="def9a-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="def9a-116">![][BrowseSitesScreenshot]Diagnostyka są włączone na podstawie poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="def9a-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="def9a-117">Rozpocznij od przejrzenia lokacji toohello chcesz tooenable tej funkcji na.</span><span class="sxs-lookup"><span data-stu-id="def9a-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="def9a-118">![][DiagnosticsLogs]Z menu Ustawienia, przewiń w dół toohello **monitorowanie** sekcji, a następnie kliknij pozycję **(1) dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="def9a-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="def9a-119">Następnie **(2) Włącz** **rejestrowania aplikacji (systemu plików)** lub **rejestrowania aplikacji (blob)** hello **poziom** opcja pozwala zmienić hello poziom ważności toocapture śladów.</span><span class="sxs-lookup"><span data-stu-id="def9a-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="def9a-120">Jeśli próbujesz po prostu zapoznać się z funkcją hello tooget, ustawić poziom hello zbyt**pełne** tooensure wszystkie Twoje instrukcji śledzenia są zbierane.</span><span class="sxs-lookup"><span data-stu-id="def9a-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="def9a-121">Kliknij przycisk **ZAPISAĆ** u góry bloku hello i hello jest gotowy tooview dzienniki.</span><span class="sxs-lookup"><span data-stu-id="def9a-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="def9a-122">Witaj Witaj wyższej **poziom ważności** hello więcej zasobów są wykorzystanych toolog i hello są produkowane więcej danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="def9a-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="def9a-123">Upewnij się, że **poziom ważności** jest poprawne szczegółowości toohello skonfigurowanego do produkcji lub witryn o dużym ruchu.</span><span class="sxs-lookup"><span data-stu-id="def9a-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="def9a-124">![][StreamingLogsScreenshot]tooview hello **Podgląd dzienników przesyłanych strumieniowo** w hello portalu Azure, kliknij na **strumienia dziennika (1)** również w hello **monitorowanie** część hello ustawień menu.</span><span class="sxs-lookup"><span data-stu-id="def9a-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="def9a-125">Jeśli aplikacja jest aktywnie pisanie instrukcji śledzenia, a następnie powinny być widoczne w hello **(2) przesyłania strumieniowego dzienników interfejsu użytkownika** w najbliższym czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="def9a-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="def9a-126">Konsola</span><span class="sxs-lookup"><span data-stu-id="def9a-126">Console</span></span>
<span data-ttu-id="def9a-127">Witaj **portalu Azure** zapewnia aplikacji tooyour dostępu do konsoli.</span><span class="sxs-lookup"><span data-stu-id="def9a-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="def9a-128">Można eksplorować aplikacji w systemie plików i uruchamiać skrypty programu powershell/poleceń.</span><span class="sxs-lookup"><span data-stu-id="def9a-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="def9a-129">Są związani hello tych samych uprawnień ustawionych jako uruchomione kodu aplikacji, podczas wykonywania polecenia konsoli.</span><span class="sxs-lookup"><span data-stu-id="def9a-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="def9a-130">Katalogi tooprotected dostępu lub uruchamianie skryptów, które wymagają uprawnień z podwyższonym poziomem uprawnień jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="def9a-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="def9a-131">![][ConsoleScreenshot]Z menu Ustawienia, przewiń w dół za**narzędzi programistycznych** sekcji, a następnie kliknij pozycję **konsoli (1)** i hello **konsoli (2)** prawo toohello otwiera interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="def9a-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="def9a-132">znasz hello tooget **konsoli**, spróbuj podstawowych poleceń, takich jak:</span><span class="sxs-lookup"><span data-stu-id="def9a-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
