---
title: "aaaManage aplikacji sieci web w usłudze Azure App Service"
description: "Tooresources łącza do zarządzania aplikacji sieci web w usłudze Azure App Service."
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
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Zarządzanie aplikacji sieci web w usłudze Azure App Service
Ten temat zawiera tooresources łącza do zarządzania aplikacji sieci web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Zarządzanie obejmuje wszystkie zadania hello, zachowujących sprawnego działania aplikacji sieci web. 

Hello okresu istnienia aplikacji sieci web będzie wykonywać różnymi zadaniami zarządzania, jak przenieść z operacji toonormal początkowe wdrożenie, obsługi i aktualizacje.

Wiele zadań zarządzania aplikacji sieci web można wykonać w hello portalu Azure.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Przed wdrożeniem tooproduction aplikacji sieci web
### <a name="choose-a-tier"></a>Wybierz warstwę
Usługa aplikacji Azure jest oferowany pięciu warstw: Zwolnij udostępnione, podstawowa, standardowa i Premium. Aby uzyskać informacje o funkcjach hello i ceny dla każdej warstwy, zobacz [szczegóły cennika](https://azure.microsoft.com/pricing/details/app-service/). 

* [Planów usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pozwalają na grupowanie wielu aplikacji sieci web w obszarze hello tej samej warstwie.
* Możesz zawsze [przełącznik warstwy](web-sites-scale.md) po utworzeniu aplikacji sieci web.

### <a name="configuration"></a>Konfiguracja
Użyj hello [Azure Portal](https://portal.azure.com/) tooset różne opcje konfiguracji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service](web-sites-configure.md). Poniżej przedstawiono szybki Lista kontrolna:

* Wybierz **wersji środowiska uruchomieniowego** dla platformy .NET, PHP, Java lub Python, jeśli to konieczne.
* Włącz **Websocket** Jeśli protokół WebSocket hello korzysta z aplikacji sieci web. (Dotyczy to aplikacji, które używają [ASP.NET SignalR](http://www.asp.net/signalr) lub [użyciu biblioteki socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Używasz ciągłego web zadania? Jeśli tak, Włącz **zawsze na**.
* Zestaw hello **dokument domyślny**, takich jak index.html.

W ustawieniach konfiguracji podstawowej toothese dodanie może być tooconfigure hello poniżej:

* **Secure Socket Layer (SSL)** szyfrowania. toouse SSL z niestandardowej nazwy domeny, należy uzyskać SSL certyfikatów i skonfigurować toouse aplikacji sieci web go. Zobacz [Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service](app-service-web-tutorial-custom-ssl.md).
* **Nazwa domeny niestandardowej.** Aplikacja sieci web ma automatycznie poddomeny w obszarze azurewebsites.net. Możesz skojarzyć niestandardowej nazwy domeny, np. contoso.com. Zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md).

Konfiguracja specyficzny dla języka:

* **PHP**: [skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure](web-sites-php-configure.md).
* **Python**: [Konfigurowanie Python z usługi aplikacji Azure Web Apps](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Aplikacja sieci web jest uruchomiona
Po uruchomieniu aplikacji sieci web ma toomake się, że jest dostępny i że skaluje się toomeet ruchu użytkowników. Możesz także tootroubleshoot błędy.

### <a name="monitoring"></a>Monitorowanie
* Za pomocą hello portalu Azure, możesz [dodać metryki wydajności](web-sites-monitor.md) użycia procesora CPU i liczby żądań klientów.
* [Skalowanie aplikacji sieci web](web-sites-scale.md) w tootraffic odpowiedzi. W zależności od warstwę można skalować hello liczbę maszyn wirtualnych i/lub rozmiaru hello hello wystąpień maszyn wirtualnych. W hello Standard i Premium warstw można również skonfigurować Skalowanie automatyczne, dzięki aplikacji sieci web skaluje automatycznie, zgodnie z ustalonym harmonogramem lub w tooload odpowiedzi.  

### <a name="backups"></a>Tworzenie kopii zapasowych
* Ustaw [automatycznego tworzenia kopii zapasowych](web-sites-backup.md) aplikacji sieci web. Dowiedz się więcej na temat tworzenia kopii zapasowych w [ten film](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Dowiedz się więcej o opcjach hello [odzyskiwanie bazy danych](../sql-database/sql-database-business-continuity.md) w bazie danych SQL Azure.

### <a name="troubleshooting"></a>Rozwiązywanie problemów
* Jeśli jakaś nieprawidłowość, możesz [Rozwiązywanie problemów w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), przy użyciu dzienników diagnostycznych i debugowania w chmurze hello na żywo. 
* Poza Visual Studio istnieją różne sposoby toocollect diagnostycznych dzienników. Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md).
* Dla aplikacji programu Node.js [jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Przywracanie danych
* [Przywróć](web-sites-restore.md) aplikacji sieci web, która została wcześniej utworzona kopia zapasowa.

## <a name="when-you-update-your-web-app"></a>Podczas aktualizacji aplikacji sieci web
Jeśli nie włączono automatycznego tworzenia kopii zapasowych, możesz utworzyć [ręcznego wykonywania kopii zapasowej](web-sites-backup.md).

Należy rozważyć użycie [przemieszczane wdrożenia](web-sites-staged-publishing.md). Ta opcja umożliwia publikowanie przemieszczania wdrożenia, który uruchamia side-by-side tooa aktualizacje z wdrożeniem w środowisku produkcyjnym. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


