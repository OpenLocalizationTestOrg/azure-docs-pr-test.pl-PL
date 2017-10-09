---
title: "aaaMonitor hello kondycji zasobów Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure CDN przy użyciu kondycja zasobów Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Monitorowanie kondycji hello zasobów Azure CDN
  
Kondycja zasobów sieci CDN w warstwie Azure jest podzbiorem [kondycji zasobów platformy Azure](../resource-health/resource-health-overview.md).  Można używać zasobów platformy Azure kondycji toomonitor hello kondycji zasobów w sieci CDN i odbierać wskazówki można wykonać tootroubleshoot problemów.

>[!IMPORTANT] 
>Kondycja zasobów usługi Azure CDN tylko aktualnie kont kondycji hello globalne dostarczania CDN i funkcje interfejsu API.  Kondycja zasobów usługi Azure CDN nie weryfikuje poszczególnych punktów końcowych usługi CDN.
>
>Witaj sygnalizuje, że źródła danych usługi Azure CDN kondycja zasobów może być aktywne minut too15 opóźnione.

## <a name="how-toofind-azure-cdn-resource-health"></a>Jak toofind kondycja zasobów Azure CDN

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj tooyour profilu CDN.

2. Kliknij przycisk hello **ustawienia** przycisku.

    ![Przycisk ustawień](./media/cdn-resource-health/cdn-profile-settings.png)

3. W obszarze *pomocy technicznej i rozwiązywania problemów*, kliknij przycisk **kondycja zasobów**.

    ![Kondycja zasobów w sieci CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>Możesz również znaleźć CDN zasobów wymienionych w hello *kondycja zasobów* kafelka w hello *Pomoc i obsługa techniczna* bloku.  Szybki dostęp zbyt*Pomoc i obsługa techniczna* klikając hello kółku **?** w hello prawym górnym rogu portalu hello.
>
> ![Pomoc i obsługa techniczna](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Azure CDN specyficzne wiadomości

Kondycja zasobów w sieci CDN tooAzure powiązane stany znajdują się poniżej.

|Komunikat | Zalecane działanie |
|---|---|
|Użytkownik może mieć zatrzymana, usunięte lub błędnie skonfigurowane co najmniej jednego z punktami końcowymi CDN | Użytkownik może mieć zatrzymana, usunięte lub błędnie skonfigurowane co najmniej jednego z punktami końcowymi CDN.|
|Niestety, hello CDN Usługa zarządzania jest obecnie niedostępna | Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną.|
|Niestety, punktami końcowymi CDN może mieć wpływ bieżących problemów niektóre z naszych dostawców usługi CDN | Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jak używać hello rozwiązywanie narzędzie toolearn tootest Twojego punkt początkowy i punkt końcowy CDN; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną. |
|Niestety, zmiany w konfiguracji punktu końcowego CDN występują opóźnienia w przepłynie | Zaglądaj tu, aby zobaczyć aktualizacje stanu; Zmiany w konfiguracji nie są w pełni propagowane w hello oczekiwany czas, należy się z pomocą techniczną.|
|Niestety, wystąpiły problemy podczas ładowania portalu dodatkowym hello | Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną.|
Niestety, wystąpiły problemy z niektórych naszych dostawców sieci CDN | Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną. |

## <a name="next-steps"></a>Następne kroki

- [Zapoznanie się z informacjami o kondycji zasobów platformy Azure](../resource-health/resource-health-overview.md)
- [Rozwiązywanie problemów z sieci CDN kompresji](./cdn-troubleshoot-compression.md)
- [Rozwiązywanie problemów z błędami 404](./cdn-troubleshoot-endpoint.md)