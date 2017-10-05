---
title: "Zarządzanie aplikacji sieci web w usłudze Azure App Service"
description: "Linki do zasobów związanych z zarządzaniem aplikacji sieci web w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Zarządzanie aplikacji sieci web w usłudze Azure App Service
Ten temat zawiera linki do zasobów związanych z zarządzaniem aplikacji sieci web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Zarządzanie obejmuje wszystkie zadania zachowujących sprawnego działania aplikacji sieci web. 

W okresie istnienia aplikacji sieci web będzie wykonywać różnymi zadaniami zarządzania, w przypadku przejścia od pierwszego wdrożenia do normalnego działania, konserwacji i aktualizacji.

Wiele zadań zarządzania aplikacji sieci web można wykonać w portalu Azure.

## <a name="before-you-deploy-your-web-app-to-production"></a>Przed wdrożeniem aplikacji sieci web w środowisku produkcyjnym
### <a name="choose-a-tier"></a>Wybierz warstwę
Usługa aplikacji Azure jest oferowany pięciu warstw: Zwolnij udostępnione, podstawowa, standardowa i Premium. Informacje o funkcjach i ceny dla każdej warstwy, zobacz [szczegóły cennika](https://azure.microsoft.com/pricing/details/app-service/). 

* [Planów usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pozwalają na grupowanie wielu aplikacji sieci web w tej samej warstwie.
* Możesz zawsze [przełącznik warstwy](web-sites-scale.md) po utworzeniu aplikacji sieci web.

### <a name="configuration"></a>Konfiguracja
Użyj [Azure Portal](https://portal.azure.com/) można ustawić różne opcje konfiguracji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service](web-sites-configure.md). Poniżej przedstawiono szybki Lista kontrolna:

* Wybierz **wersji środowiska uruchomieniowego** dla platformy .NET, PHP, Java lub Python, jeśli to konieczne.
* Włącz **Websocket** Jeśli aplikacja sieci web używa protokołu WebSocket. (Dotyczy to aplikacji, które używają [ASP.NET SignalR](http://www.asp.net/signalr) lub [użyciu biblioteki socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Używasz ciągłego web zadania? Jeśli tak, Włącz **zawsze na**.
* Ustaw **dokument domyślny**, takich jak index.html.

Oprócz tych ustawień konfiguracji podstawowej można skonfigurować następujące ustawienia:

* **Secure Socket Layer (SSL)** szyfrowania. Używanie protokołu SSL z niestandardowej nazwy domeny, należy uzyskać certyfikat SSL i skonfigurować aplikację sieci web w celu używania go. Zobacz [Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service](app-service-web-tutorial-custom-ssl.md).
* **Nazwa domeny niestandardowej.** Aplikacja sieci web ma automatycznie poddomeny w obszarze azurewebsites.net. Możesz skojarzyć niestandardowej nazwy domeny, np. contoso.com. Zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md).

Konfiguracja specyficzny dla języka:

* **PHP**: [skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure](web-sites-php-configure.md).
* **Python**: [Konfigurowanie Python z usługi aplikacji Azure Web Apps](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Aplikacja sieci web jest uruchomiona
Po uruchomieniu aplikacji sieci web ma upewnij się, że jest dostępny i że może spełniać ruchu użytkowników. Może być również konieczne rozwiązywania problemów.

### <a name="monitoring"></a>Monitorowanie
* Za pośrednictwem portalu Azure, możesz [dodać metryki wydajności](web-sites-monitor.md) użycia procesora CPU i liczby żądań klientów.
* [Skalowanie aplikacji sieci web](web-sites-scale.md) w odpowiedzi na ruch. W zależności od warstwę można skalować liczbę maszyn wirtualnych i/lub rozmiaru wystąpień maszyn wirtualnych. W warstwy standardowa i Premium można również skonfigurować Skalowanie automatyczne, więc aplikacji sieci web skaluje automatycznie, zgodnie z ustalonym harmonogramem lub w odpowiedzi na obciążenia.  

### <a name="backups"></a>Tworzenie kopii zapasowych
* Ustaw [automatycznego tworzenia kopii zapasowych](web-sites-backup.md) aplikacji sieci web. Dowiedz się więcej na temat tworzenia kopii zapasowych w [ten film](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Więcej informacji na temat opcji [odzyskiwanie bazy danych](../sql-database/sql-database-business-continuity.md) w bazie danych SQL Azure.

### <a name="troubleshooting"></a>Rozwiązywanie problemów
* Jeśli jakaś nieprawidłowość, możesz [Rozwiązywanie problemów w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), przy użyciu dzienników diagnostycznych i na żywo debugowania w chmurze. 
* Poza Visual Studio istnieją różne sposoby zbierania dzienników diagnostycznych. Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md).
* Dla aplikacji programu Node.js [debugowanie aplikacji sieci web Node.js w usłudze Azure App Service](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Przywracanie danych
* [Przywróć](web-sites-restore.md) aplikacji sieci web, która została wcześniej utworzona kopia zapasowa.

## <a name="when-you-update-your-web-app"></a>Podczas aktualizacji aplikacji sieci web
Jeśli nie włączono automatycznego tworzenia kopii zapasowych, możesz utworzyć [ręcznego wykonywania kopii zapasowej](web-sites-backup.md).

Należy rozważyć użycie [przemieszczane wdrożenia](web-sites-staged-publishing.md). Ta opcja umożliwia publikowanie aktualizacji do tymczasowej wdrożenia, które uruchamia side-by-side z wdrożeniem w środowisku produkcyjnym. 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


