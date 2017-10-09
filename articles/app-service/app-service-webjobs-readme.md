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
# <a name="using-webjobs-in-azure-app-service"></a>Użycie zadań WebJobs w usłudze Azure App Service
W tym artykule łączy toodocumentation zasoby dotyczące toouse zadań Webjob Azure i hello Azure WebJobs SDK. Zadań Webjob Azure zapewniają prosty sposób toorun skrypty lub programy jako procesy w tle na [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). Możesz przekazać i uruchom plik wykonywalny, takich jak jako cmd, bat, exe (.NET), ps1, sh, php, py, js i jar. Te programy uruchamiane jako zadań Webjob, zgodnie z harmonogramem (cron) lub w sposób ciągły.

Witaj zestaw SDK zadań Webjob ułatwia łatwiejsze toouse usługi Azure Storage. zestaw SDK zadań Webjob Hello ma powiązanie i system wyzwalacz, który współpracuje z obiektów blob Microsoft Azure magazynu, kolejek i tabel, a także kolejek usługi Service Bus.

Tworzenie, wdrażanie i zarządzanie zadań Webjob jest bezproblemowe z narzędziami zintegrowane w programie Visual Studio. Można utworzyć zadania Webjob na podstawie szablonów, publikowanie i zarządzanie (Uruchom/stop/monitor/debug) je.

pulpitu nawigacyjnego zadań Webjob Hello w hello Azure portal udostępnia funkcji zaawansowanego zarządzania, które zapewniają pełną kontrolę nad hello wykonywanie zadań Webjob, w tym hello możliwości tooinvoke poszczególnych funkcji w ramach zadań Webjob. pulpit nawigacyjny Hello są również wyświetlane funkcja środowisk uruchomieniowych i dane wyjściowe rejestrowania.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

