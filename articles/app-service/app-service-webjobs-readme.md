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
# <a name="using-webjobs-in-azure-app-service"></a>Użycie zadań WebJobs w usłudze Azure App Service
Ten artykuł zawiera łącza do dokumentacji zasoby o sposobie używania zadań Webjob Azure i zestawu Azure WebJobs SDK. Zadań Webjob Azure umożliwiają łatwe do uruchamiania skryptów lub programów procesów w tle [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). Możesz przekazać i uruchom plik wykonywalny, takich jak jako cmd, bat, exe (.NET), ps1, sh, php, py, js i jar. Te programy uruchamiane jako zadań Webjob, zgodnie z harmonogramem (cron) lub w sposób ciągły.

Zestaw SDK zadań Webjob ułatwia użyć usługi Azure Storage. Zestaw SDK zadań Webjob ma powiązanie i system wyzwalacz, który współpracuje z obiektów blob Microsoft Azure magazynu, kolejek i tabel, a także kolejek usługi Service Bus.

Tworzenie, wdrażanie i zarządzanie zadań Webjob jest bezproblemowe z narzędziami zintegrowane w programie Visual Studio. Można utworzyć zadania Webjob na podstawie szablonów, publikowanie i zarządzanie (Uruchom/stop/monitor/debug) je.

Pulpitu nawigacyjnego zadań Webjob w portalu Azure zapewnia funkcji zaawansowanego zarządzania, które zapewniają pełną kontrolę nad wykonywanie zadań Webjob, w tym możliwość wywołania poszczególnych funkcji w ramach zadań Webjob. Pulpit nawigacyjny jest również wyświetlana funkcja środowisk uruchomieniowych i dane wyjściowe rejestrowania.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

