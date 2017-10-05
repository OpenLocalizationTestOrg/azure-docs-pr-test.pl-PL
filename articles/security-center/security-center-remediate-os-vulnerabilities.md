---
title: "Korygowanie luk w zabezpieczeniach systemu operacyjnego w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** luk w zabezpieczeniach ** skorygować systemu operacyjnego."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Korygowanie luk w zabezpieczeniach systemu operacyjnego w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure codziennie analizuje systemu operacyjnego maszyny wirtualnej (VM) (system operacyjny) dla konfiguracji, które można utworzyć maszyny Wirtualnej bardziej narażony na ataki i zaleca zmiany konfiguracji, aby rozwiązać te luki w zabezpieczeniach. Centrum zabezpieczeń zaleca się, Usuń luk w zabezpieczeniach, gdy konfiguracja systemu operacyjnego maszyny Wirtualnej jest niezgodna z reguł zalecanych konfiguracji.

> [!NOTE]
> Aby uzyskać więcej informacji o określonych monitorowanych konfiguracji, zobacz [lista reguł zalecanych konfiguracji](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-the-recommendation"></a>Wykonania zalecenia

> [!NOTE]
> Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

1. W **zalecenia** bloku, wybierz opcję **luk w zabezpieczeniach skorygować OS**.
   ![Koryguj luki w zabezpieczeniach systemu operacyjnego][1]

    **Luk w zabezpieczeniach skorygować OS** bloku otwiera i listy maszyn wirtualnych z konfiguracji systemu operacyjnego, które nie są zgodne z reguł zalecanych konfiguracji.  Dla każdej maszyny Wirtualnej identyfikuje bloku:

   * **REGUŁY nie powiodło się** — liczba reguł, których konfiguracja systemu operacyjnego maszyny Wirtualnej nie powiodła się.
   * **Czas ostatniego skanowania** — Data i godzina Centrum zabezpieczeń będzie ostatniego skanowania Konfiguracja systemu operacyjnego maszyny Wirtualnej.
   * **Stan** — bieżący stan luki w zabezpieczeniach:

     * Otwórz: Lukę w zabezpieczeniach nie rozpoczęto jeszcze
     * W toku: Jest aktualnie stosowane lukę w zabezpieczeniach, jest wymagana żadna akcja ze strony
     * Rozpoznać: Usterka została już omówiona (gdy problem został rozwiązany, pozycja jest wyszarzona)
   * **WAŻNOŚĆ** — wszystkie luki w zabezpieczeniach są ustawione na ważność niski, co oznacza powinny być kierowane luka w zabezpieczeniach, ale nie wymaga natychmiastowej uwagi.

2. Wybierz maszynę Wirtualną. Bloku dla tej maszyny Wirtualnej zostanie otwarty i wyświetla reguł, które nie powiodły.
   ![Reguły konfiguracji, które nie powiodło się][2]

3. Wybierz regułę. W tym przykładzie pozwala wybrać **hasło musi spełniać wymagania co do złożoności**. Zostanie otwarty blok opisujące reguły nie powiodło się i wpływu. Przejrzyj szczegóły i należy wziąć pod uwagę sposób stosowania konfiguracji systemu operacyjnego.
  ![Opis reguły nie powiodło się][3]

  Centrum zabezpieczeń używane typowych konfiguracji wyliczenie CCE () do przypisywania unikatowych identyfikatorów dla reguły konfiguracji. Poniższe informacje są przekazywane w tym bloku:

  - Nazwa — Nazwa reguły
  - WAŻNOŚĆ — Wartości ważności CCE krytyczna ważne i ostrzeżenia
  - CCIED — CCE Unikatowy identyfikator reguły
  - OPIS — Opis reguły
  - Luki w zabezpieczeniach — Opis usterki lub ryzyko, gdy nie jest stosowana reguła
  - WPŁYW — Wpływ na prowadzoną działalność po zastosowaniu reguły
  - OCZEKIWANA wartość — Wartość oczekiwana w przypadku Centrum zabezpieczeń analizuje względem reguły konfiguracji systemu operacyjnego maszyny Wirtualnej
  - — Reguła zasada operacji używane przez Centrum zabezpieczeń podczas analizy konfiguracji systemu operacyjnego maszyny Wirtualnej względem reguły
  - RZECZYWISTA wartość--Zwracana wartość po analizie względem reguły konfiguracji systemu operacyjnego maszyny Wirtualnej
  - WYNIK oceny —-wynik analizy: przekazywania błędów

## <a name="see-also"></a>Zobacz też
W tym artykule przedstawiono sposób wykonania zalecenia Centrum zabezpieczeń "Luk Skoryguj systemu operacyjnego". Możesz przejrzeć zestaw reguł konfiguracji [tutaj](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Centrum zabezpieczeń używane CCE (typowych konfiguracji wyliczenie) do przypisywania unikatowych identyfikatorów dla reguły konfiguracji. Odwiedź stronę [CCE](https://nvd.nist.gov/cce/index.cfm) witryny, aby uzyskać więcej informacji.

Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące zasoby:

* [Obsługiwane platformy w Centrum zabezpieczeń Azure](security-center-os-coverage.md) — zawiera listę obsługiwanych systemu Windows i maszyn wirtualnych systemu Linux.
* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.
* [Reagowanie na alerty zabezpieczeń w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje o sposobie monitorowania stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi wyszukiwania.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
