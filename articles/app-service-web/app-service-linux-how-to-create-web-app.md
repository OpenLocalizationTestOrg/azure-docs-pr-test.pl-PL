---
title: aaaCreate platformy Azure w sieci web aplikacji uruchomionej w systemie Linux | Dokumentacja firmy Microsoft
description: "Przepływ tworzenia aplikacji sieci Web dla aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Utwórz aplikację sieci web platformy Azure z systemem Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Użyj aplikacji sieci web hello toocreate portalu Azure
Można utworzyć aplikacji sieci web w systemie Linux z hello [portalu Azure](https://portal.azure.com) pokazane na powitania po obrazu:

![Rozpocznij tworzenie aplikacji sieci web na powitania portalu Azure][1]

Następnie hello **bloku Utwórz** otwiera pokazane na powitania po obrazu:

![bloku Utwórz Hello][2]

1. Nadaj nazwę aplikacji sieci web.
2. Wybierz istniejącą grupę zasobów lub Utwórz nową. (Zobacz dostępnych regionów w hello [sekcji ograniczenia](app-service-linux-intro.md).)
3. Wybierz istniejący plan usługi aplikacji Azure lub Utwórz nową. (Zobacz uwagi planu usługi aplikacji w hello [sekcji ograniczenia](app-service-linux-intro.md).)
4. Wybierz aplikację hello stosu, który ma toouse. Można wybrać różne wersje programu Node.js, PHP, .net Core i Ruby.

Po utworzeniu aplikacji hello pokazane na powitania po obrazu można zmienić stosu aplikacji hello z ustawień aplikacji hello:

![Ustawienia aplikacji][3]

## <a name="deploy-your-web-app"></a>Wdrażanie aplikacji sieci web
Wybieranie **opcje wdrażania** z zapewnia portalu zarządzania hello hello opcja toouse lokalnego Git i GitHub repozytorium toodeploy aplikacji. rest Hello instrukcji hello są podobne toothose dla aplikacji sieci web z systemem innym niż Linux. Możesz wykonać instrukcje hello [lokalnego wdrożenia Git](app-service-deploy-local-git.md) lub [ciągłe wdrażanie](app-service-continuous-deployment.md) toodeploy aplikacji.

Umożliwia także FTP tooupload w witrynie tooyour aplikacji. Można pobrać punktu końcowego FTP powitania dla aplikacji sieci web z diagnostyki hello sekcji dzienniki pokazane na powitania po obrazu:

![Dzienniki diagnostyczne][4]

## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](app-service-linux-intro.md)
* [Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-nodejs-pm2.md)
* [W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby](app-service-linux-ruby-get-started.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
