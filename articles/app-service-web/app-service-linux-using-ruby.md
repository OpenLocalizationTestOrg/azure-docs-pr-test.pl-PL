---
title: "W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby | Dokumentacja firmy Microsoft"
description: "Używanie Ruby w aplikacji sieci Web usługi aplikacji Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, często zadawane pytania, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>W aplikacji sieci Web w systemie Linux przy użyciu Ruby #

Przy użyciu najnowszych aktualizacji do naszej wewnętrznej bazy danych wprowadzono obsługę v.2.3 dopisków fonetycznych. Przez ustawienie konfiguracji aplikacji sieci web systemu Linux, można zmienić stosu aplikacji.

## <a name="using-the-azure-portal"></a>Korzystanie z witryny Azure Portal ##

W menu Nowy [portalu Azure](https://portal.azure.com), można wybrać do utworzenia aplikacji sieci Web w systemie Linux z sieci Web i opcji mobilnych, jak pokazano na poniższej ilustracji:

![Rozpocznij tworzenie aplikacji sieci web w portalu Azure][1]

Następnie **bloku Utwórz** otwiera, jak pokazano na poniższej ilustracji:

![Tworzenie bloku][2]

1. Nadaj nazwę aplikacji sieci web.
2. Wybierz istniejącą grupę zasobów lub Utwórz nową. (Zobacz dostępnych regionów w [sekcji ograniczenia](app-service-linux-intro.md).)
3. Wybierz istniejący plan usługi aplikacji Azure lub Utwórz nową. (Zobacz uwagi planu usługi aplikacji w [sekcji ograniczenia](app-service-linux-intro.md).)
4. Wybierz Ruby z stosów wbudowanych środowiska wykonawczego.

Po utworzeniu aplikacji sieci web dopisków fonetycznych pobiera można wdrożyć do niej przy użyciu narzędzia Git i FTP.

Aby dowiedzieć się więcej o tworzeniu aplikacji dopisków fonetycznych, sprawdź [przewodnika get](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web w systemie Linux?](app-service-linux-intro.md)
* [Wdrażanie lokalnej usługi Git w usłudze Azure App Service](app-service-deploy-local-git.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](app-service-linux-faq.md)
* [Tworzenie aplikacji dopisków fonetycznych w aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png