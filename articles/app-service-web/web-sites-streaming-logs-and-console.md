---
title: "Dzienniki przesyłania strumieniowego i konsoli"
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a>Dzienniki przesyłania strumieniowego i konsoli
## <a name="streaming-logs"></a>Dzienniki przesyłania strumieniowego
**Portalu Azure** zapewnia zintegrowane przesyłania strumieniowego przeglądarka dzienników, który umożliwia wyświetlanie zdarzenia śledzenia z Twojej **usługi aplikacji** aplikacji w czasie rzeczywistym.  

Konfigurowanie tej funkcji wymaga kilku prostych kroków:

* Zapisuj śledzenia w kodzie
* Włączanie aplikacji **dzienników diagnostycznych** dla aplikacji
* Wyświetl strumienia z wbudowanych **dzienniki przesyłania strumieniowego** interfejsu użytkownika w **portalu Azure**.

### <a name="how-to-write-traces-in-your-code"></a>Jak można zapisywać dane śledzenia w kodzie
Zapisywanie danych śledzenia w kodzie jest bardzo proste.  W języku C# jest tak proste, jak zapisywania następujący kod:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Klasa śledzenia znajduje się w przestrzeni nazw System.Diagnostics.

W aplikacji node.js można napisać ten kod, aby osiągnąć ten sam rezultat:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a>Jak włączyć i wyświetlić przesyłanie strumieniowe dzienniki
![][BrowseSitesScreenshot]Diagnostyka są włączone na podstawie poszczególnych aplikacji. Rozpocznij od przejrzenia do lokacji, aby włączyć tę funkcję na.  

![][DiagnosticsLogs]Z menu Ustawienia, przewiń w dół do **monitorowanie** sekcji, a następnie kliknij pozycję **(1) dzienników diagnostycznych**. Następnie **(2) Włącz** **rejestrowania aplikacji (systemu plików)** lub **rejestrowania aplikacji (blob)** **poziom** opcja pozwala zmienić poziom ważności śladów do przechwycenia. Jeśli próbujesz po prostu zapoznać się z funkcją, ustawić poziom na **pełne** zapewnienie wszystkie Twoje instrukcji śledzenia są zbierane.

Kliknij przycisk **ZAPISAĆ** w górnej części bloku i jest gotowe do wyświetlania dzienników.

> [!NOTE]
> Wyższe **poziom ważności** więcej zasobów są używane do logowania i więcej dane śledzenia są tworzone. Upewnij się, że **poziom ważności** skonfigurowano poprawne szczegółowości do produkcji lub witryn o dużym ruchu. 
> 
> 

![][StreamingLogsScreenshot]Aby wyświetlić **Podgląd dzienników przesyłanych strumieniowo** w portalu Azure kliknij na **(1) strumienia dziennika** również w **monitorowanie** części menu Ustawienia. Jeśli aplikacja jest aktywnie pisanie instrukcji śledzenia, a następnie powinny być widoczne w w **(2) przesyłania strumieniowego dzienników interfejsu użytkownika** w najbliższym czasie rzeczywistym.

## <a name="console"></a>Konsola
**Portalu Azure** zapewnia dostęp do aplikacji konsoli. Można eksplorować aplikacji w systemie plików i uruchamiać skrypty programu powershell/poleceń. Użytkownik, są powiązane przez te same uprawnienia, Ustaw jako uruchomione kodu aplikacji, podczas wykonywania polecenia konsoli. Dostęp do chronionych katalogów lub uruchamianie skryptów, które wymagają uprawnień z podwyższonym poziomem uprawnień jest zablokowany.  

![][ConsoleScreenshot]Z menu Ustawienia, przewiń w dół do **narzędzi programistycznych** sekcji, a następnie kliknij pozycję **konsoli (1)** i **(2) konsoli** interfejsu użytkownika zostanie otwarty po prawej stronie.

Aby zapoznać się z **konsoli**, spróbuj podstawowych poleceń, takich jak:

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
