---
title: "Zadania Webjob w usłudze aplikacji Azure"
description: "Dowiedz się, jak utworzyć zadania Webjob do uruchomienia testów tła, interakcji z usług takich jak magazyn i usługi Service Bus i tworzenia zaplanowanych zadań."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="0ff52-103">Użycie zadań WebJobs w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0ff52-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="0ff52-104">Ten artykuł zawiera łącza do dokumentacji zasoby o sposobie używania zadań Webjob Azure i zestawu Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="0ff52-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="0ff52-105">Zadań Webjob Azure umożliwiają łatwe do uruchamiania skryptów lub programów procesów w tle [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="0ff52-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="0ff52-106">Możesz przekazać i uruchom plik wykonywalny, takich jak jako cmd, bat, exe (.NET), ps1, sh, php, py, js i jar.</span><span class="sxs-lookup"><span data-stu-id="0ff52-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="0ff52-107">Te programy uruchamiane jako zadań Webjob, zgodnie z harmonogramem (cron) lub w sposób ciągły.</span><span class="sxs-lookup"><span data-stu-id="0ff52-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="0ff52-108">Zestaw SDK zadań Webjob ułatwia użyć usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ff52-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="0ff52-109">Zestaw SDK zadań Webjob ma powiązanie i system wyzwalacz, który współpracuje z obiektów blob Microsoft Azure magazynu, kolejek i tabel, a także kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0ff52-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="0ff52-110">Tworzenie, wdrażanie i zarządzanie zadań Webjob jest bezproblemowe z narzędziami zintegrowane w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ff52-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="0ff52-111">Można utworzyć zadania Webjob na podstawie szablonów, publikowanie i zarządzanie (Uruchom/stop/monitor/debug) je.</span><span class="sxs-lookup"><span data-stu-id="0ff52-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="0ff52-112">Pulpitu nawigacyjnego zadań Webjob w portalu Azure zapewnia funkcji zaawansowanego zarządzania, które zapewniają pełną kontrolę nad wykonywanie zadań Webjob, w tym możliwość wywołania poszczególnych funkcji w ramach zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="0ff52-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="0ff52-113">Pulpit nawigacyjny jest również wyświetlana funkcja środowisk uruchomieniowych i dane wyjściowe rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="0ff52-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

