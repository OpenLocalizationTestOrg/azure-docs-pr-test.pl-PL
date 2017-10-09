---
title: "aaaWebJobs w usłudze Azure App Service"
description: "Dowiedz się, jak testy toobuild tła toorun zadań Webjob, interakcji z usług takich jak magazyn i usługi Service Bus i tworzenia zaplanowanych zadań."
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
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="746b4-103">Użycie zadań WebJobs w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="746b4-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="746b4-104">W tym artykule łączy toodocumentation zasoby dotyczące toouse zadań Webjob Azure i hello Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="746b4-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="746b4-105">Zadań Webjob Azure zapewniają prosty sposób toorun skrypty lub programy jako procesy w tle na [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="746b4-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="746b4-106">Możesz przekazać i uruchom plik wykonywalny, takich jak jako cmd, bat, exe (.NET), ps1, sh, php, py, js i jar.</span><span class="sxs-lookup"><span data-stu-id="746b4-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="746b4-107">Te programy uruchamiane jako zadań Webjob, zgodnie z harmonogramem (cron) lub w sposób ciągły.</span><span class="sxs-lookup"><span data-stu-id="746b4-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="746b4-108">Witaj zestaw SDK zadań Webjob ułatwia łatwiejsze toouse usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="746b4-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="746b4-109">zestaw SDK zadań Webjob Hello ma powiązanie i system wyzwalacz, który współpracuje z obiektów blob Microsoft Azure magazynu, kolejek i tabel, a także kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="746b4-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="746b4-110">Tworzenie, wdrażanie i zarządzanie zadań Webjob jest bezproblemowe z narzędziami zintegrowane w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="746b4-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="746b4-111">Można utworzyć zadania Webjob na podstawie szablonów, publikowanie i zarządzanie (Uruchom/stop/monitor/debug) je.</span><span class="sxs-lookup"><span data-stu-id="746b4-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="746b4-112">pulpitu nawigacyjnego zadań Webjob Hello w hello Azure portal udostępnia funkcji zaawansowanego zarządzania, które zapewniają pełną kontrolę nad hello wykonywanie zadań Webjob, w tym hello możliwości tooinvoke poszczególnych funkcji w ramach zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="746b4-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="746b4-113">pulpit nawigacyjny Hello są również wyświetlane funkcja środowisk uruchomieniowych i dane wyjściowe rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="746b4-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

