---
title: "aaaMonitoring usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor funkcji platformy Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Monitorowanie usługi Azure Functions

## <a name="overview"></a>Omówienie 


Witaj **Monitor** karcie dla każdej funkcji umożliwia tooreview wykonanie każdej funkcji.

![Karta monitor funkcje platformy Azure](./media/functions-monitoring/monitor-tab.png) 

Kliknięcie wykonywania umożliwia możesz tooreview hello duration, danych wejściowych, błędy i skojarzone pliki dziennika. Jest to przydatne debugowania i dostrajania funkcji wydajności.


> [!IMPORTANT]
> Korzystając z hello [zużycie plan hostingu](functions-overview.md#pricing) dla usługi Azure Functions hello **monitorowanie** kafelka w bloku Przegląd funkcji aplikacji hello nie wyświetli żadnych danych. Jest to spowodowane platformy hello dynamicznie skaluje i zarządza wystąpienia obliczeniowe, więc te metryki nie są przydatne w planie zużycia. Użycie hello toomonitor aplikacji funkcji, wskazówki hello należy zamiast tego użyć w tym artykule.
> 
> powitania po zrzut ekranu przedstawia przykład:
> 
> ![Monitorowanie na powitania bloku zasobów głównego](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Monitorowanie w czasie rzeczywistym

Monitorowanie w czasie rzeczywistym będą dostępne po kliknięciu **strumień na żywo zdarzeń** jak pokazano poniżej. 

![Opcja strumienia zdarzeń na karcie monitorowanie hello na żywo](./media/functions-monitoring/monitor-tab-live-event-stream.png)

strumień na żywo zdarzeń Hello zostaną wyświetlone na wykresie na nowej karcie przeglądarki w sposób przedstawiony poniżej. 

![Przykład strumienia wydarzenia na żywo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Jest to znany problem, który może powodować Twojej toobe toofail danych wypełnione. Jeśli wystąpią, może być konieczne tooclose hello przeglądarki kartę zawierającego hello na żywo strumienia zdarzeń, a następnie kliknij przycisk **strumień na żywo zdarzeń** tooallow ponownie go tooproperly wypełnić danych strumienia zdarzeń. 

strumień na żywo zdarzeń Hello będzie wykres hello następujące statystyki dla funkcji:

* Wykonaniami uruchomione na sekundę
* Wykonaniami wykonywanych na sekundę
* Wykonaniami zakończone niepowodzeniami na sekundę
* Średni czas wykonania (w milisekundach).

Te statystyki są w czasie rzeczywistym, ale hello rzeczywiste Tworzenie wykresów hello wykonywania danych mogą mieć około 10 sekund opóźnienia.






## <a name="monitoring-log-files-from-a-command-line"></a>Monitorowanie plików dziennika z wiersza polecenia


Można przesłać strumieniowo sesji wiersza polecenia tooa pliki dziennika na lokalnej stacji roboczej za pomocą hello Azure interfejsu wiersza polecenia (CLI) lub programu PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Pliki dziennika aplikacji funkcji monitorowania z hello wiersza polecenia platformy Azure

tooget pracę, [zainstalować hello wiersza polecenia platformy Azure](../cli-install-nodejs.md)

Zaloguj się do konta platformy Azure przy użyciu następujących hello polecenia ani żadnych innych opcji, których dotyczy, hello [Zaloguj tooAzure z hello Azure CLI](../xplat-cli-connect.md).

    azure login

Użyj hello następujące polecenie trybie Azure CLI usługi zarządzania (ASM) tooenable:.

    azure config mode asm

Jeśli masz wiele subskrypcji, użyj następującego polecenia toolist hello Twojej subskrypcji i zestaw hello bieżącej subskrypcji toohello subskrypcji, która zawiera aplikację funkcji.

    azure account list
    azure account set <subscriptionNameOrId>

Witaj następujące polecenie będą przesyłane strumieniowo pliki dziennika hello linii polecenia toohello aplikacji funkcji:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Pliki dziennika aplikacji funkcji monitorowania przy użyciu programu PowerShell

Rozpoczęto, tooget [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Dodaj konto platformy Azure, uruchamiając następujące polecenie hello:

    PS C:\> Add-AzureAccount

Jeśli masz wiele subskrypcji, możesz podać je według nazwy z powitania po toosee polecenia hello prawidłowa subskrypcja jest hello aktualnie wybrany na podstawie `IsCurrent` właściwości:

    PS C:\> Get-AzureSubscription

Tooset hello aktywną subskrypcją toohello zawierający aplikację funkcji, należy użyć hello następujące polecenie:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Strumień hello rejestruje tooyour sesji programu PowerShell z hello następujące polecenie:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Aby uzyskać więcej informacji można znaleźć zbyt[porady: strumienia dzienników aplikacji sieci web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Testowanie funkcji](functions-test-a-function.md)
* [Skalowanie funkcji](functions-scale.md)

