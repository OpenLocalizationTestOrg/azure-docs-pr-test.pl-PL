---
title: "aaaApplication wydajności — często zadawane pytania dotyczące aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące dostępności, wydajności i problemy z aplikacji w funkcji Web Apps hello Azure App Service."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Wydajność aplikacji — często zadawane pytania dotyczące aplikacji sieci Web na platformie Azure

Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania (FAQ) o problemy z wydajnością aplikacji dla hello [funkcja Web Apps usługi Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Dlaczego jest Moja aplikacja wolne?

Wiele czynników może przyczynić się tooslow wydajność aplikacji. Aby uzyskać szczegółowe kroki rozwiązywania problemów, zobacz [wydajność aplikacji sieci web powolne rozwiązywanie](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Jak rozwiązywać problemy z scenariusza wysokie użycie procesora CPU

W niektórych scenariuszach wysokie użycie procesora CPU aplikacji naprawdę może wymagać więcej zasobów obliczeniowych. W takim przypadku należy wziąć pod uwagę skalowanie tooa wyższego poziomu usługi, więc aplikacji hello pobiera wszystkie zasoby hello, których potrzebuje. Innych przypadkach może być spowodowany wysokie użycie procesora CPU, zły pętli lub rozwiązaniem w zakresie kodowania. Uzyskiwanie wglądu w co jest przyczyną zwiększone użycie procesora CPU jest procesem dwóch części. Najpierw należy utworzyć zrzutu procesu, a następnie analizować hello zrzutu procesu. Aby uzyskać więcej informacji, zobacz [przechwytywanie i analizowanie plik zrzutu wysokie użycie procesora CPU dla aplikacji sieci Web](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Jak rozwiązywać scenariusza wysokie zużycie pamięci?

W niektórych scenariuszach wysokie zużycie pamięci aplikacji naprawdę może wymagać więcej zasobów obliczeniowych. W takim przypadku należy wziąć pod uwagę skalowanie tooa wyższego poziomu usługi, więc aplikacji hello pobiera wszystkie zasoby hello, których potrzebuje. Innym razem usterki w kodzie hello może spowodować przeciek pamięci. Rozwiązaniem w zakresie kodowania także może zwiększyć wykorzystanie pamięci. Uzyskiwanie wglądu w co jest przyczyną pamięci wysokiej zużycie to proces składający się z dwóch części. Najpierw należy utworzyć zrzutu procesu, a następnie analizować hello zrzutu procesu. Diagnostyki awarii z hello galerii rozszerzeń witryny Azure można efektywnie obsługiwać obu tych czynności. Aby uzyskać więcej informacji, zobacz [przechwytywanie i analizowanie pliku zrzutu pamięci wysokiej sporadyczne dla aplikacji sieci Web](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>Jak zautomatyzować aplikacje sieci web usługi aplikacji przy użyciu programu PowerShell?

Można użyć toomanage poleceń cmdlet programu PowerShell i obsługa aplikacji sieci web usługi aplikacji. W naszym blogu [zautomatyzować aplikacje sieci web hostowanych w usłudze Azure App Service przy użyciu programu PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), opisano sposób toouse na podstawie Menedżera zasobów Azure PowerShell polecenia cmdlet tooautomate typowych zadań. Witaj w blogu ma również przykładowy kod dla różnych zadań zarządzania aplikacji sieci web. Opisy i składnia dla wszystkich poleceń cmdlet aplikacji sieci web usługi aplikacji, zobacz [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>Jak wyświetlać dzienniki zdarzeń aplikacji sieci web?

tooview w dziennikach zdarzeń aplikacji sieci web:

1. Zaloguj się tooyour [Kudu witryny sieci Web](https://*yourwebsitename*.scm.azurewebsites.net).
2. Wybierz hello menu **konsoli debugowania** > **CMD**.
3. Wybierz hello **LogFiles** folderu.
4. dzienniki zdarzeń tooview, wybierz ikonę ołówka hello obok zbyt**eventlog.xml**.
5. Dzienniki hello toodownload, uruchom polecenie cmdlet programu PowerShell hello `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>Jak przechwytywania zrzutu pamięci trybu użytkownika mojej aplikacji sieci web?

toocapture zrzutu pamięci trybu użytkownika aplikacji sieci web:

1. Zaloguj się tooyour [Kudu witryny sieci Web](https://*yourwebsitename*.scm.azurewebsites.net).
2. Wybierz hello **Eksploratora procesów** menu.
3. Kliknij prawym przyciskiem myszy hello **w3wp.exe** procesu lub proces zadania WebJob.
4. Wybierz **Pobierz zrzut pamięci** > **pełne zrzutu**.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Jak wyświetlić informacje o poziomie procesu dla mojej aplikacji sieci web?

Masz dwie opcje wyświetlania informacji o poziomie procesu dla aplikacji sieci web:

*   W portalu Azure hello:
    1. Otwórz hello **Eksploratora procesów** hello aplikacji sieci web.
    2. toosee hello szczegóły, wybierz opcję hello **w3wp.exe** procesu.
*   W konsoli Kudu hello:
    1. Zaloguj się tooyour [Kudu witryny sieci Web](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Wybierz hello **Eksploratora procesów** menu.
    3. Dla hello **w3wp.exe** procesu, wybierz opcję **właściwości**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Przeglądających toomy aplikacji, są widoczne "Błąd 403 - ta aplikacja sieci web została zatrzymana." Jak rozwiązać ten problem?

Trzy warunki mogą być przyczyną tego błędu:

* Hello aplikacji sieci web został osiągnięty limit rozliczeń i witryna została wyłączona.
* w portalu hello Hello aplikacji sieci web została zatrzymana.
* aplikacji sieci web Hello osiągnął limity przydziału zasobów mogą być stosowane tooa wolne lub planu usług udostępnionych skali.

toosee co jest przyczyną błędu hello i tooresolve hello problem, hello wykonaj kroki opisane w temacie [aplikacji sieci Web: "Błąd 403 — ta aplikacja sieci web została zatrzymana"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Gdzie mogą dowiedzieć się więcej na temat przydziały i limity dla różnych planów usługi aplikacji?

Aby uzyskać informacje o przydziały i limity, zobacz [ogranicza usługi aplikacji](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Jak obniżyć hello czas odpowiedzi dla pierwszego żądania powitania po bezczynności?

Domyślnie aplikacje sieci web są usuwane, jeśli są one bezczynności na wybrany okres czasu. Dzięki temu hello system zachować zasoby. Wadą interfejsu Hello jest hello odpowiedzi toohello pierwsze żądanie po hello aplikacji sieci web jest zwalniany jest dłuższy, tooallow hello tooload aplikacji sieci web i uruchomić jednoczesnej obsłudze odpowiedzi. W planie Basic i Standard usługi, możesz włączyć hello **zawsze na** aplikacji hello tookeep ustawienie zawsze ładowany. Eliminuje to dłuższy czas ładowania po aplikacji hello jest w stanie bezczynności. Witaj toochange **zawsze na** ustawienia:

1. W hello portalu Azure Przejdź tooyour aplikacji sieci web.
2. Wybierz **ustawienia aplikacji**.
3. Aby uzyskać **zawsze na**, wybierz pozycję **na**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Jak włączone śledzenie nieudanych żądań?

tooturn na śledzenie nieudanych żądań:

1. W hello portalu Azure Przejdź tooyour aplikacji sieci web.
3. Wybierz **wszystkie ustawienia** > **dzienników diagnostycznych**.
4. Aby uzyskać **śledzenia nieudanych żądań**, wybierz pozycję **na**.
5. Wybierz pozycję **Zapisz**.
6. W bloku aplikacja sieci web hello, wybierz **narzędzia**.
7. Wybierz **Visual Studio Online**.
8. Jeśli ustawienie hello nie **na**, wybierz pozycję **na**.
9. Wybierz **Przejdź**.
10. Wybierz **Web.config**.
11. W system.webServer Dodaj tę konfigurację (toocapture określony adres URL):

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. tootroubleshoot problemów zmniejszyć wydajność, Dodaj tę konfigurację (jeśli hello Przechwytywanie żądania trwa dłużej niż 30 sekund):
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. Witaj toodownload nie powiodło się ślady na żądanie, w hello [portal](https://portal.azure.com), przejdź do pozycji tooyour witryny sieci Web.
15. Wybierz **narzędzia** > **Kudu** > **Przejdź**.
18. Wybierz hello menu **konsoli debugowania** > **CMD**.
19. Wybierz hello **LogFiles** folder, a następnie wybierz hello folder o nazwie, która rozpoczyna się od **W3SVC**.
20. plik XML hello toosee, hello wybierz ikonę ołówka.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Widać wiadomości powitania "proces roboczy zażądał odzyskania termin too'Percent pamięci" limit. " Jak rozwiązać ten problem?

Hello maksymalna dostępna ilość pamięci dla procesu 32-bitowego (nawet na 64-bitowym systemie operacyjnym) wynosi 2 GB. Domyślnie proces roboczy hello ustawiono too32-bitowe w usłudze App Service (dla zachowania zgodności z aplikacjami sieci web w starszej wersji).

Należy rozważyć przełączania too64-bitowych procesów, dzięki czemu można korzystać hello dodatkowych dostępnej pamięci w swojej roli procesu roboczego sieci Web. Powoduje ponowne uruchomienie aplikacji sieci web, więc planowanie odpowiednio.

Należy również zauważyć, że 64-bitowego środowiska wymaga usługi planu Basic lub Standard. Zwolnij i planów udostępnione są zawsze uruchamiane w środowisku 32-bitowym.

Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji sieci web w usłudze App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Dlaczego moja limit czasu żądania 240 sekund?

Moduł równoważenia obciążenia Azure ma domyślne ustawienie limitu czasu bezczynności czterech minut. Zwykle jest to termin uzasadnione odpowiedzi na żądania sieci web. Jeśli aplikacja sieci web wymaga przetwarzania w tle, zalecamy użycie zadań Webjob Azure. Aplikacja sieci web platformy Azure Hello można wywołać zadania Webjob i powiadomienie po zakończeniu przetwarzania w tle. Można wybrać z wielu metod umożliwiających używanie zadań Webjob, łącznie z kolejki i wyzwalaczy.

Zadania Webjob jest przeznaczony do przetwarzania w tle. Możesz to zrobić tyle przetwarzania w tle w zadanie WebJob. Aby uzyskać więcej informacji na temat zadań Webjob, zobacz [wykonywać zadania w tle z zadań Webjob](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>Aplikacji platformy ASP.NET Core, które są obsługiwane w usłudze App Service czasami przestać odpowiadać. Jak rozwiązać ten problem?

Znany problem dotyczący wcześniejszego [wersji Kestrel](https://github.com/aspnet/KestrelHttpServer/issues/1182) może spowodować aplikacji platformy ASP.NET Core 1.0, która znajduje się w aplikacji usługi toointermittently przestaje odpowiadać. Można również zobaczyć ten komunikat: "hello określona aplikacja CGI napotkał błąd i hello procesu powitania serwera zakończone."

Ten problem został rozwiązany w Kestrel wersji 1.0.2. Ta wersja jest dołączona hello platformy ASP.NET Core 1.0.3 aktualizacji. tooresolve ten problem, upewnij się, że aktualizacja Twojej aplikacji zależności toouse Kestrel wersji 1.0.2. Alternatywnie można użyć jednej z dwóch rozwiązania, które zostały opisane w blogu hello [powolne wydajności platformy ASP.NET Core 1.0 problemy w aplikacji sieci web usługi aplikacji](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>Nie można znaleźć pliki dziennika w strukturze plików hello Moja aplikacja sieci web. Jak można je znaleźć?

Jeśli funkcja hello lokalnej pamięci podręcznej usługi App Service, folderów danych dla swojego wystąpienia usługi aplikacji i struktury folderów hello hello LogFiles dotyczy problem. W przypadku lokalnej pamięci podręcznej podfoldery są tworzone w hello magazynu LogFiles i foldery z danymi. Użyj podfoldery Hello hello nazewnictwa wzorzec "Unikatowy identyfikator" + sygnatury czasowej. Każdy podfolder odpowiada tooa wystąpienia maszyny Wirtualnej, w których hello aplikacji sieci web jest uruchomiona lub jest uruchomione.

toodetermine czy korzystasz z lokalnej pamięci podręcznej, sprawdź aplikację usługi **ustawienia aplikacji** kartę. Jeśli używane jest lokalnej pamięci podręcznej, ustawienia aplikacji hello `WEBSITE_LOCAL_CACHE_OPTION` ustawiono zbyt`Always`. Aby uzyskać więcej informacji o lokalnej pamięci podręcznej, zobacz hello [lokalnej pamięci podręcznej usługi aplikacji — omówienie](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Jeśli nie korzystają z lokalnej pamięci podręcznej i występuje ten problem, należy przesłać żądanie obsługi.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Widać wiadomości powitania "próba wprowadzone tooaccess gniazda w sposób zabroniony przez jego uprawnienia dostępu." Jak rozwiązać ten problem?

Ten błąd zazwyczaj występuje podczas wyczerpania Witaj wychodzące połączenia TCP na powitania wystąpienia maszyny Wirtualnej. W usłudze App Service limity są wymuszane hello maksymalnej liczby połączeń wychodzących, które można podjąć dla każdego wystąpienia maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [limity wartości liczbowych maszyny Wirtualnej między](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).

Ten błąd może również wystąpić przy próbie tooaccess adresu lokalnego z aplikacji. Aby uzyskać więcej informacji, zobacz [żądań lokalny adres](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).

Aby uzyskać więcej informacji na temat połączenia wychodzące w aplikacji sieci web, zobacz hello blogu o [wychodzące połączenia tooAzure witryn sieci Web](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Jak używać programu Visual Studio tooremote debugowania Moja aplikacja sieci web usługi aplikacji?

Aby uzyskać szczegółowy przewodnik pokazujący sposób toodebug aplikacji sieci web za pomocą programu Visual Studio, zobacz [zdalne debugowanie aplikacji sieci web usługi aplikacji](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
