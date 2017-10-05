---
title: "Utwórz aplikację sieci web platformy Azure z systemem Linux | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Utwórz aplikację sieci web platformy Azure z systemem Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a>Użyj portalu Azure, aby utworzyć aplikację sieci web
Można utworzyć aplikacji sieci web w systemie Linux z [portalu Azure](https://portal.azure.com) jak pokazano na poniższej ilustracji:

![Rozpocznij tworzenie aplikacji sieci web w portalu Azure][1]

Następnie **bloku Utwórz** otwiera, jak pokazano na poniższej ilustracji:

![Tworzenie bloku][2]

1. Nadaj nazwę aplikacji sieci web.
2. Wybierz istniejącą grupę zasobów lub Utwórz nową. (Zobacz dostępnych regionów w [sekcji ograniczenia](app-service-linux-intro.md).)
3. Wybierz istniejący plan usługi aplikacji Azure lub Utwórz nową. (Zobacz uwagi planu usługi aplikacji w [sekcji ograniczenia](app-service-linux-intro.md).)
4. Wybierz stosu aplikacji, które będą używane. Można wybrać różne wersje programu Node.js, PHP, .net Core i Ruby.

Po utworzeniu aplikacji można zmienić stosu aplikacji z ustawień aplikacji, jak pokazano na poniższej ilustracji:

![Ustawienia aplikacji][3]

## <a name="deploy-your-web-app"></a>Wdrażanie aplikacji sieci web
Wybieranie **opcje wdrażania** z zarządzania portalu daje możliwość użycia lokalnego repozytorium Git i GitHub do wdrożenia aplikacji. Pozostałe instrukcje są podobne do tych aplikacji sieci web z systemem innym niż Linux. Można postępuj zgodnie z instrukcjami [lokalnego wdrożenia Git](app-service-deploy-local-git.md) lub [ciągłe wdrażanie](app-service-continuous-deployment.md) do wdrożenia aplikacji.

Umożliwia także FTP do przekazywania aplikacji do witryny. Można uzyskać punktu końcowego FTP dla aplikacji sieci web, z sekcji dzienników diagnostyki, jak pokazano na poniższej ilustracji:

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
