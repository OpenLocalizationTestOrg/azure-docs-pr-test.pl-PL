---
title: "Zła brama aaaFix 502, 503 obsługi błędów niedostępności | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z 502 Niewłaściwa brama i 503 błędów niedostępności usługi w aplikacji sieci web hostowanych w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "Zła brama 502, 503 usługi niedostępne, błąd 503, błąd 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>Rozwiązywanie błędów HTTP "502 Niewłaściwa brama" i "503 Usługa niedostępna" w aplikacjach sieci web platformy Azure
"brama zły 502" i "503 Usługa niedostępna" są typowe błędy w aplikacji sieci web hostowanych w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Ten artykuł pomoże w rozwiązaniu tych błędów.

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz polecenie **Get Support**.

## <a name="symptom"></a>Objaw
Podczas przeglądania aplikacji sieci web toohello zwraca HTTP HTTP lub błąd "502 Niewłaściwa brama" błąd "503 Usługa niedostępna".

## <a name="cause"></a>Przyczyna
Ten problem jest często spowodowane przez problemy z poziomu aplikacji, takich jak:

* żądania zbyt długo
* aplikacji przy użyciu pamięci wysokiej/procesora CPU
* Aplikacja awarii z powodu wyjątku tooan.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Rozwiązywanie problemów z kroki toosolve "502 Niewłaściwa brama" i "503 Usługa niedostępna" błędy
Rozwiązywanie problemów, można podzielić na trzy różne zadania, w kolejności sekwencyjnej:

1. [Sprawdź i monitorowanie zachowania aplikacji](#observe)
2. [Zbieranie danych](#collect)
3. [Ograniczenia hello problem](#mitigate)

[Aplikacje sieci Web usługi aplikacji](/services/app-service/web/) zapewnia różne opcje w każdym kroku.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Sprawdź i monitorowanie zachowania aplikacji
#### <a name="track-service-health"></a>Śledź usługę kondycji
Microsoft Azure publicizes każdym razem, gdy istnieje degradacji przerw i wydajności usługi. Kondycja hello hello usługi można śledzić na powitania [Azure Portal](https://portal.azure.com/). Aby uzyskać więcej informacji, zobacz [śledzić kondycja usługi](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Monitorowanie aplikacji sieci web
Ta opcja umożliwia toofind wychodzących, jeśli masz problemy w aplikacji. W bloku aplikacja sieci web, kliknij hello **żądań i błędów** kafelka. Witaj **Metryka** bloku wyświetli wszystkie metryki hello można dodać.

Niektóre hello metryki dla aplikacji sieci web można toomonitor

* Pamięć średni zestaw roboczy
* Średni czas odpowiedzi
* Czas procesora CPU
* Zestaw roboczy pamięci
* Żądania

![monitorowanie aplikacji sieci web do rozwiązania błędów HTTP 502 Niewłaściwa brama i 503 Usługa jest niedostępna](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Aby uzyskać więcej informacji, zobacz:

* [Monitorowanie aplikacji sieci Web w usłudze aplikacji Azure](web-sites-monitor.md)
* [Otrzymywanie powiadomień o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Zbieranie danych
#### <a name="use-hello-azure-app-service-support-portal"></a>Użyj hello portalu pomocy technicznej usługi aplikacji Azure
Aplikacje sieci Web udostępnia aplikacji sieci web hello możliwości tootroubleshoot problemów powiązanych tooyour analizując HTTP dzienniki, dzienniki zdarzeń, zrzuty procesu i inne. Można uzyskać dostępu do tych informacji za pomocą portalu pomocy technicznej w **http://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/Support**

Hello portalu pomocy technicznej usługi aplikacji Azure udostępnia trzy oddzielne karty toosupport hello trzy kroki typowego scenariusza rozwiązywania problemów:

1. Sprawdź bieżące zachowanie
2. Analizowanie zbierania informacji diagnostycznych i uruchamiając hello analizatorów wbudowane
3. Ograniczenia

Problem hello jest przeprowadzana od razu, kliknij przycisk **Analizuj** > **diagnostyki** > **diagnozowanie teraz** toocreate sesję diagnostyki, który będzie zbierać HTTP dzienniki, dzienniki Podglądu zdarzeń, pamięci zrzuty, dzienniki błędów PHP i PHP przetwarzania raportu.

Po pobraniu danych hello, zostanie również przeprowadzanie analizy na powitania danych oraz zapewnić mu raport HTML.

W przypadku, gdy chcesz toodownload hello dane, domyślnie, powinny być przechowywane w folderze D:\home\data\DaaS hello.

Aby uzyskać więcej informacji na powitania portalu pomocy technicznej usługi aplikacji Azure, zobacz [tooSupport nowe aktualizacje lokacji rozszerzenie dla witryny sieci Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Użyj hello Kudu Debug Console
Aplikacje sieci Web jest dostarczany z konsoli debugowania, która służy do debugowania, eksploracji, przekazywania plików, a także pobieranie informacji na temat środowiska punktów końcowych JSON. Ta metoda jest wywoływana hello *konsoli Kudu* lub hello *pulpitu nawigacyjnego SCM* dla aplikacji sieci web.

Uzyskać dostęp do tego pulpitu nawigacyjnego, przechodząc łącze toohello **https://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/**.

Program Kudu udostępnia zagadnienia hello należą:

* ustawienia środowiska aplikacji
* strumień dziennika
* diagnostycznych zrzutu
* Konsola, w którym można uruchomić poleceń cmdlet programu Powershell i podstawowe polecenia systemu DOS debugowania.

Inny przydatną cechą Kudu jest, że w przypadku, gdy aplikacja jest zgłaszanie wyjątków pierwszej szansy, można użyć Kudu i zrzuty hello SysInternals narzędzie Procdump toocreate pamięci. Te zrzuty pamięci są migawki procesu hello i często ułatwiają rozwiązywanie problemów z bardziej skomplikowanych problemów z aplikacją sieci web.

Aby uzyskać więcej informacji o funkcjach dostępnych w Kudu, zobacz [narzędzia online witryny sieci Web Azure należy wiedzieć o](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Ograniczenia hello problem
#### <a name="scale-hello-web-app"></a>Aplikacja sieci web hello skali
W usłudze Azure App Service Aby zwiększyć wydajność i przepływność, można dostosować hello skali, w którym są uruchomione aplikacji. Skalowanie w górę aplikacji sieci web obejmuje dwie akcje powiązane: zmiana z wyższej warstwy cenowej i konfigurowanie niektórych ustawień po przełączeniu toohello wyższej warstwy cenowej tooa planu usługi aplikacji.

Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie aplikacji sieci web w usłudze Azure App Service](web-sites-scale.md).

Ponadto można wybrać toorun aplikacji na więcej niż jedno wystąpienie. To nie tylko zapewnia więcej możliwości przetwarzania, ale umożliwia także niektóre ilość odporność na uszkodzenia. Jeśli hello procesu przestanie działać w jednym wystąpieniu, hello inne wystąpienie będzie nadal obsługiwać żądania dostępu.

Można ustawić hello skalowanie toobe ręczne lub automatyczne.

#### <a name="use-autoheal"></a>Funkcja AutoHeal użycia
Funkcja AutoHeal odtwarzania procesu roboczego hello aplikacji na podstawie ustawień wybranego (np. zmiany konfiguracji, żądania, limity pamięci lub czasu hello wymagane tooexecute żądania). W większości przypadków hello odtworzenia procesu hello jest hello najszybszy sposób toorecover z problem. Chociaż można zawsze uruchomić ponownie hello aplikacji sieci web z bezpośrednio z poziomu portalu Azure hello, funkcja AutoHeal będzie robi to automatycznie. Toodo wystarczy dodać niektóre wyzwalacze w hello głównym pliku web.config dla aplikacji sieci web. Należy pamiętać, że te ustawienia będą działać w hello sam sposób, nawet jeśli w aplikacji nie jest jedną .net.

Aby uzyskać więcej informacji, zobacz [automatyczne naprawianie Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Ponowne uruchomienie aplikacji sieci web hello
Jest to często hello najprostszy sposób toorecover jednorazowo występujące problemy. Na powitania [Azure Portal](https://portal.azure.com/), w bloku aplikacja sieci web, masz toostop opcje hello lub uruchom ponownie aplikację.

 ![ponowne uruchomienie aplikacji toosolve HTTP błędy 502 Niewłaściwa brama i 503 Usługa jest niedostępna](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

Można również zarządzać aplikacji sieci web przy użyciu programu Azure Powershell. Aby uzyskać więcej informacji, zobacz temat [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Azure PowerShell z usługą Azure Resource Manager).

