---
title: "aaaEnable zbierania danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: " Dowiedz się, jak tooenable zbierania danych w Centrum zabezpieczeń Azure. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Włącz zbieranie danych w Centrum zabezpieczeń Azure

> [!NOTE]
> Począwszy od początku czerwca 2017, Centrum zabezpieczeń użyj toocollect Microsoft Monitoring Agent hello i przechowywania danych. toolearn więcej, zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md). Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>
>

Centrum zabezpieczeń zbiera dane z Twojego tooassess maszynach wirtualnych (VM) stanu zabezpieczeń, podaj zalecenia dotyczące zabezpieczeń i alertów toothreats. Najpierw przejść do Centrum zabezpieczeń ma hello opcja tooenable danych kolekcji dla wszystkich maszyn wirtualnych w ramach subskrypcji. Jeśli zbieranie danych nie jest włączone, Centrum zabezpieczeń zaleca się włączenie funkcji zbierania danych w zasadach zabezpieczeń powitania dla tej subskrypcji.

Po włączeniu funkcji zbierania danych Centrum zabezpieczeń przepisy hello Microsoft Monitoring Agent na wszystkich istniejących obsługiwanych maszyn wirtualnych platformy Azure i nowe pliki, które są tworzone. Witaj Microsoft Monitoring Agent skanowania pod kątem różnych konfiguracji związanych z zabezpieczeniami. Ponadto system operacyjny hello zgłasza zdarzenia z dziennika zdarzeń. Przykłady takich danych to typ systemu operacyjnego i jego wersja, dzienniki systemu operacyjnego (dzienniki zdarzeń systemu Windows), uruchomione procesy, nazwa maszyny, adresy IP, zalogowany użytkownik i identyfikator dzierżawy. Hello Microsoft Monitoring Agent odczytuje wpisy dziennika zdarzeń i konfiguracje i kopiuje hello obszaru roboczego tooyour danych do analizy. Microsoft Monitoring Agent Hello kopiuje roboczym tooyour pliki zrzutu awaryjnego.

Jeśli używasz hello warstwę bezpłatna Centrum zabezpieczeń można wyłączyć zbieranie danych z maszyn wirtualnych przez wyłączenie zbierania danych w zasadach zabezpieczeń hello. Wyłączanie zbierania danych ogranicza ocenę zabezpieczeń dla maszyn wirtualnych. toolearn więcej, zobacz [wyłączanie zbierania danych](#disabling-data-collection). Migawki dysków maszyny Wirtualnej i kolekcji artefaktu są włączone, nawet jeśli zbieranie danych zostało wyłączone. Zbieranie danych jest wymagane dla subskrypcji w warstwie standardowa hello Centrum zabezpieczeń.

> [!NOTE]
> Dowiedz się więcej o wolnym Centrum zabezpieczeń i Standard [warstw cenowych](security-center-pricing.md).
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia. Ten dokument nie jest przewodnik krok po kroku.
>
>

1. W hello **zalecenia** bloku, wybierz opcję **Włączanie zbierania danych dla subskrypcji**.  Spowoduje to otwarcie hello **włączyć funkcję zbierania danych** bloku.
   ![Bloku zalecenia][2]
2. Na powitania **włączyć funkcję zbierania danych** bloku, wybierz subskrypcję. Witaj **zasady zabezpieczeń** zostanie otwarty blok dla tej subskrypcji.
3. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **na** w obszarze **zbierania danych** tooautomatically zbierania dzienników. Włączanie hello przepisy zbierania danych monitorowania rozszerzenie na wszystkie bieżące oraz nowe maszyny wirtualne są obsługiwane w hello subskrypcji.
4. Wybierz pozycję **Zapisz**.
5. Kliknij przycisk **OK**.

## <a name="disabling-data-collection"></a>Wyłączanie zbierania danych
Jeśli używasz hello warstwę bezpłatna Centrum zabezpieczeń można wyłączyć zbieranie danych z maszyn wirtualnych w dowolnym momencie przez wyłączenie zbierania danych w zasadach zabezpieczeń hello. Zbieranie danych jest wymagane dla subskrypcji w warstwie standardowa hello Centrum zabezpieczeń.

1. Zwraca toohello **Centrum zabezpieczeń** bloku i wybierz hello **zasad** kafelka. Spowoduje to otwarcie hello **zasady zabezpieczeń — Zdefiniuj zasady dla subskrypcji** bloku.
   ![Wybierz Kafelek zasad hello][5]
2. Na powitania **zasady zabezpieczeń — Zdefiniuj zasady dla subskrypcji** bloku, wybierz hello subskrypcji, że chcesz toodisable zbierania danych.
3. Witaj **zasady zabezpieczeń** zostanie otwarty blok dla tej subskrypcji.  Wybierz **poza** w obszarze zbierania danych.
4. Wybierz **zapisać** hello wstążce top.

## <a name="next-steps"></a>Następne kroki
W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz zbieranie danych." toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md)— Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md)— Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
- [Bezpieczeństwo danych w Centrum zabezpieczeń Azure](security-center-data-security.md) — Dowiedz się, jak dane są zarządzane i w Centrum zabezpieczeń.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
