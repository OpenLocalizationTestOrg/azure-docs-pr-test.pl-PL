---
title: Dzienniki aaaStreaming i konsoli
description: "Omówienie konsoli i dzienniki przesyłania strumieniowego"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>Dzienniki przesyłania strumieniowego i hello konsoli
## <a name="streaming-logs"></a>Dzienniki przesyłania strumieniowego
Witaj **portalu Azure** zapewnia zintegrowane przesyłania strumieniowego przeglądarka dzienników, który umożliwia wyświetlanie zdarzenia śledzenia z Twojej **usługi aplikacji** aplikacji w czasie rzeczywistym.  

Konfigurowanie tej funkcji wymaga kilku prostych kroków:

* Zapisuj śledzenia w kodzie
* Włączanie aplikacji **dzienników diagnostycznych** dla aplikacji
* Widok hello strumienia z wbudowanych hello **dzienniki przesyłania strumieniowego** interfejsu użytkownika w hello **portalu Azure**.

### <a name="how-toowrite-traces-in-your-code"></a>Jak toowrite służy do śledzenia w kodzie
Zapisywanie danych śledzenia w kodzie jest bardzo proste.  W języku C# jest tak proste, jak zapisywania hello następującego kodu:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Witaj klasy śledzenia znajduje się w przestrzeni nazw System.Diagnostics hello.

W aplikacji node.js można napisać ten kod tooachieve hello takiego samego wyniku:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Jak tooenable i widoku hello dzienniki przesyłania strumieniowego
![][BrowseSitesScreenshot]Diagnostyka są włączone na podstawie poszczególnych aplikacji. Rozpocznij od przejrzenia lokacji toohello chcesz tooenable tej funkcji na.  

![][DiagnosticsLogs]Z menu Ustawienia, przewiń w dół toohello **monitorowanie** sekcji, a następnie kliknij pozycję **(1) dzienników diagnostycznych**. Następnie **(2) Włącz** **rejestrowania aplikacji (systemu plików)** lub **rejestrowania aplikacji (blob)** hello **poziom** opcja pozwala zmienić hello poziom ważności toocapture śladów. Jeśli próbujesz po prostu zapoznać się z funkcją hello tooget, ustawić poziom hello zbyt**pełne** tooensure wszystkie Twoje instrukcji śledzenia są zbierane.

Kliknij przycisk **ZAPISAĆ** u góry bloku hello i hello jest gotowy tooview dzienniki.

> [!NOTE]
> Witaj Witaj wyższej **poziom ważności** hello więcej zasobów są wykorzystanych toolog i hello są produkowane więcej danych śledzenia. Upewnij się, że **poziom ważności** jest poprawne szczegółowości toohello skonfigurowanego do produkcji lub witryn o dużym ruchu. 
> 
> 

![][StreamingLogsScreenshot]tooview hello **Podgląd dzienników przesyłanych strumieniowo** w hello portalu Azure, kliknij na **strumienia dziennika (1)** również w hello **monitorowanie** część hello ustawień menu. Jeśli aplikacja jest aktywnie pisanie instrukcji śledzenia, a następnie powinny być widoczne w hello **(2) przesyłania strumieniowego dzienników interfejsu użytkownika** w najbliższym czasie rzeczywistym.

## <a name="console"></a>Konsola
Witaj **portalu Azure** zapewnia aplikacji tooyour dostępu do konsoli. Można eksplorować aplikacji w systemie plików i uruchamiać skrypty programu powershell/poleceń. Są związani hello tych samych uprawnień ustawionych jako uruchomione kodu aplikacji, podczas wykonywania polecenia konsoli. Katalogi tooprotected dostępu lub uruchamianie skryptów, które wymagają uprawnień z podwyższonym poziomem uprawnień jest zablokowany.  

![][ConsoleScreenshot]Z menu Ustawienia, przewiń w dół za**narzędzi programistycznych** sekcji, a następnie kliknij pozycję **konsoli (1)** i hello **konsoli (2)** prawo toohello otwiera interfejsu użytkownika.

znasz hello tooget **konsoli**, spróbuj podstawowych poleceń, takich jak:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
