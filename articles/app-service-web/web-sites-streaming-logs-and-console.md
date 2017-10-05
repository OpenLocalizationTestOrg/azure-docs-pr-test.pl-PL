---
title: "Dzienniki przesyłania strumieniowego i konsoli"
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="f871e-103">Dzienniki przesyłania strumieniowego i konsoli</span><span class="sxs-lookup"><span data-stu-id="f871e-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="f871e-104">Dzienniki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="f871e-104">Streaming Logs</span></span>
<span data-ttu-id="f871e-105">**Portalu Azure** zapewnia zintegrowane przesyłania strumieniowego przeglądarka dzienników, który umożliwia wyświetlanie zdarzenia śledzenia z Twojej **usługi aplikacji** aplikacji w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="f871e-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="f871e-106">Konfigurowanie tej funkcji wymaga kilku prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="f871e-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="f871e-107">Zapisuj śledzenia w kodzie</span><span class="sxs-lookup"><span data-stu-id="f871e-107">Write traces in your code</span></span>
* <span data-ttu-id="f871e-108">Włączanie aplikacji **dzienników diagnostycznych** dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="f871e-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="f871e-109">Wyświetl strumienia z wbudowanych **dzienniki przesyłania strumieniowego** interfejsu użytkownika w **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="f871e-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="f871e-110">Jak można zapisywać dane śledzenia w kodzie</span><span class="sxs-lookup"><span data-stu-id="f871e-110">How to write traces in your code</span></span>
<span data-ttu-id="f871e-111">Zapisywanie danych śledzenia w kodzie jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="f871e-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="f871e-112">W języku C# jest tak proste, jak zapisywania następujący kod:</span><span class="sxs-lookup"><span data-stu-id="f871e-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="f871e-113">Klasa śledzenia znajduje się w przestrzeni nazw System.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f871e-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="f871e-114">W aplikacji node.js można napisać ten kod, aby osiągnąć ten sam rezultat:</span><span class="sxs-lookup"><span data-stu-id="f871e-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="f871e-115">Jak włączyć i wyświetlić przesyłanie strumieniowe dzienniki</span><span class="sxs-lookup"><span data-stu-id="f871e-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="f871e-116">![][BrowseSitesScreenshot]Diagnostyka są włączone na podstawie poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f871e-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="f871e-117">Rozpocznij od przejrzenia do lokacji, aby włączyć tę funkcję na.</span><span class="sxs-lookup"><span data-stu-id="f871e-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="f871e-118">![][DiagnosticsLogs]Z menu Ustawienia, przewiń w dół do **monitorowanie** sekcji, a następnie kliknij pozycję **(1) dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="f871e-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="f871e-119">Następnie **(2) Włącz** **rejestrowania aplikacji (systemu plików)** lub **rejestrowania aplikacji (blob)** **poziom** opcja pozwala zmienić poziom ważności śladów do przechwycenia.</span><span class="sxs-lookup"><span data-stu-id="f871e-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="f871e-120">Jeśli próbujesz po prostu zapoznać się z funkcją, ustawić poziom na **pełne** zapewnienie wszystkie Twoje instrukcji śledzenia są zbierane.</span><span class="sxs-lookup"><span data-stu-id="f871e-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="f871e-121">Kliknij przycisk **ZAPISAĆ** w górnej części bloku i jest gotowe do wyświetlania dzienników.</span><span class="sxs-lookup"><span data-stu-id="f871e-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="f871e-122">Wyższe **poziom ważności** więcej zasobów są używane do logowania i więcej dane śledzenia są tworzone.</span><span class="sxs-lookup"><span data-stu-id="f871e-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="f871e-123">Upewnij się, że **poziom ważności** skonfigurowano poprawne szczegółowości do produkcji lub witryn o dużym ruchu.</span><span class="sxs-lookup"><span data-stu-id="f871e-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="f871e-124">![][StreamingLogsScreenshot]Aby wyświetlić **Podgląd dzienników przesyłanych strumieniowo** w portalu Azure kliknij na **(1) strumienia dziennika** również w **monitorowanie** części menu Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="f871e-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="f871e-125">Jeśli aplikacja jest aktywnie pisanie instrukcji śledzenia, a następnie powinny być widoczne w w **(2) przesyłania strumieniowego dzienników interfejsu użytkownika** w najbliższym czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="f871e-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="f871e-126">Konsola</span><span class="sxs-lookup"><span data-stu-id="f871e-126">Console</span></span>
<span data-ttu-id="f871e-127">**Portalu Azure** zapewnia dostęp do aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="f871e-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="f871e-128">Można eksplorować aplikacji w systemie plików i uruchamiać skrypty programu powershell/poleceń.</span><span class="sxs-lookup"><span data-stu-id="f871e-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="f871e-129">Użytkownik, są powiązane przez te same uprawnienia, Ustaw jako uruchomione kodu aplikacji, podczas wykonywania polecenia konsoli.</span><span class="sxs-lookup"><span data-stu-id="f871e-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="f871e-130">Dostęp do chronionych katalogów lub uruchamianie skryptów, które wymagają uprawnień z podwyższonym poziomem uprawnień jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="f871e-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="f871e-131">![][ConsoleScreenshot]Z menu Ustawienia, przewiń w dół do **narzędzi programistycznych** sekcji, a następnie kliknij pozycję **konsoli (1)** i **(2) konsoli** interfejsu użytkownika zostanie otwarty po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="f871e-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="f871e-132">Aby zapoznać się z **konsoli**, spróbuj podstawowych poleceń, takich jak:</span><span class="sxs-lookup"><span data-stu-id="f871e-132">To get familiar with the **console**, try basic commands like:</span></span>

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
