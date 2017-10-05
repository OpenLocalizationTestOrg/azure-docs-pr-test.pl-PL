---
title: "Monitorowanie usługę Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak monitorować funkcji platformy Azure."
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
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a>Monitorowanie usługi Azure Functions

## <a name="overview"></a>Omówienie 


**Monitor** karcie dla każdej funkcji umożliwia przeglądanie wykonanie każdej funkcji.

![Karta monitor funkcje platformy Azure](./media/functions-monitoring/monitor-tab.png) 

Kliknięcie przycisku wykonywania umożliwia przeglądanie czas trwania, danych wejściowych, błędy i skojarzone pliki dziennika. Jest to przydatne debugowania i dostrajania funkcji wydajności.


> [!IMPORTANT]
> Korzystając z [zużycie plan hostingu](functions-overview.md#pricing) dla usługi Azure Functions **monitorowanie** kafelka w bloku Przegląd funkcji aplikacji nie wyświetli żadnych danych. Jest to spowodowane platformę dynamicznie skaluje i zarządza wystąpienia obliczeniowe, więc te metryki nie są przydatne w planie zużycia. Do monitorowania użycia aplikacji funkcji, należy zamiast tego użyj wskazówek w tym artykule.
> 
> Poniższy zrzut ekranu przedstawia przykład:
> 
> ![Monitorowanie w bloku zasobów głównego](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Monitorowanie w czasie rzeczywistym

Monitorowanie w czasie rzeczywistym będą dostępne po kliknięciu **strumień na żywo zdarzeń** jak pokazano poniżej. 

![Opcja strumień wydarzenia na żywo na karcie monitor](./media/functions-monitoring/monitor-tab-live-event-stream.png)

Strumień na żywo zdarzeń zostaną wyświetlone na wykresie na nowej karcie przeglądarki w sposób przedstawiony poniżej. 

![Przykład strumienia wydarzenia na żywo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Jest to znany problem, który może powodować danych nie można wypełnić. Jeśli wystąpią, konieczne może być zamknąć kartę przeglądarki zawierająca strumień wydarzenia na żywo, a następnie kliknij przycisk **strumień na żywo zdarzeń** ponownie, aby zezwalała na poprawnie wypełnić danych strumienia zdarzeń. 

Strumień na żywo zdarzeń będzie wykres następujące statystyki dla funkcji:

* Wykonaniami uruchomione na sekundę
* Wykonaniami wykonywanych na sekundę
* Wykonaniami zakończone niepowodzeniami na sekundę
* Średni czas wykonania (w milisekundach).

Te statystyki są w czasie rzeczywistym, ale rzeczywisty Tworzenie wykresów danych wykonawczych mogą mieć około 10 sekund opóźnienia.






## <a name="monitoring-log-files-from-a-command-line"></a>Monitorowanie plików dziennika z wiersza polecenia


Można przesłać strumieniowo pliki dziennika do sesji wiersza polecenia na lokalnej stacji roboczej za pomocą usługi Azure interfejsu wiersza polecenia (CLI) lub programu PowerShell.

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a>Pliki dziennika aplikacji funkcji monitorowania z wiersza polecenia platformy Azure

Aby rozpocząć, [zainstaluj interfejs wiersza polecenia platformy Azure](../cli-install-nodejs.md)

Zaloguj się do konta platformy Azure przy użyciu następującego polecenia lub inne opcje objęte, [logowanie do platformy Azure z wiersza polecenia platformy Azure](../xplat-cli-connect.md).

    azure login

Użyj następującego polecenia, aby włączyć tryb Azure CLI usługi zarządzania (ASM):.

    azure config mode asm

Jeśli masz wiele subskrypcji, użyj następujących poleceń listy subskrypcji i ustawić bieżącej subskrypcji na subskrypcję, która zawiera aplikację funkcji.

    azure account list
    azure account set <subscriptionNameOrId>

Polecenie będą przesyłane strumieniowo pliki dziennika aplikacji funkcji w wierszu polecenia:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Pliki dziennika aplikacji funkcji monitorowania przy użyciu programu PowerShell

Aby rozpocząć, [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Dodaj konto platformy Azure, uruchamiając następujące polecenie:

    PS C:\> Add-AzureAccount

Jeśli masz wiele subskrypcji, możesz podać je według nazwy przy użyciu następującego polecenia, aby sprawdzić, czy prawidłowa subskrypcja jest aktualnie wybrany na podstawie `IsCurrent` właściwości:

    PS C:\> Get-AzureSubscription

Jeśli musisz ustawić aktywną subskrypcją dysk zawierający aplikację funkcji, użyj następującego polecenia:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Strumienia dzienników do sesji programu PowerShell przy użyciu następującego polecenia:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Więcej informacji można znaleźć w [porady: strumienia dzienników aplikacji sieci web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Następne kroki
Więcej informacji zawierają następujące zasoby:

* [Testowanie funkcji](functions-test-a-function.md)
* [Skalowanie funkcji](functions-scale.md)

