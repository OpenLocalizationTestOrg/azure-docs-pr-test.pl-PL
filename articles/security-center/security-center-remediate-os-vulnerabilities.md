---
title: "luki w zabezpieczeniach aaaRemediate systemu operacyjnego w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** luk w zabezpieczeniach ** skorygować systemu operacyjnego."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Korygowanie luk w zabezpieczeniach systemu operacyjnego w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure codziennie analizuje systemu operacyjnego maszyny wirtualnej (VM) (system operacyjny) dla maszyny Wirtualnej hello konfiguracje, które można utworzyć bardziej narażony konfiguracji tooattack i zaleca zmiany tooaddress te luki w zabezpieczeniach. Centrum zabezpieczeń zaleca się, Usuń luk w zabezpieczeniach, gdy konfiguracja systemu operacyjnego maszyny Wirtualnej jest niezgodna z hello zalecane reguły konfiguracji.

> [!NOTE]
> Aby uzyskać więcej informacji na powitania określonych monitorowanych konfiguracji, zobacz hello [lista reguł zalecanych konfiguracji](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

1. W hello **zalecenia** bloku, wybierz opcję **luk w zabezpieczeniach skorygować OS**.
   ![Koryguj luki w zabezpieczeniach systemu operacyjnego][1]

    Witaj **luk w zabezpieczeniach skorygować OS** bloku otwiera i listy maszyn wirtualnych z konfiguracji systemu operacyjnego, które nie odpowiadają hello zalecane reguły konfiguracji.  Dla każdej maszyny Wirtualnej identyfikuje bloku hello:

   * **REGUŁY nie powiodło się** — hello liczbę reguł, które hello Konfiguracja systemu operacyjnego maszyny Wirtualnej nie powiodło się.
   * **Czas ostatniego skanowania** — Witaj Data i czas ostatniego skanowania hello wirtualna Konfiguracja systemu operacyjnego czy Centrum zabezpieczeń.
   * **Stan** — Witaj bieżący stan hello luki w zabezpieczeniach:

     * Otwórz: Luka w zabezpieczeniach hello nie rozpoczęto jeszcze
     * W toku: Luka w zabezpieczeniach hello jest aktualnie stosowane, jest wymagana żadna akcja ze strony
     * Rozpoznać: Luka w zabezpieczeniach hello został objęty (gdy hello problem został rozwiązany, hello pozycja jest wyszarzona)
   * **WAŻNOŚĆ** — wszystkie luki w zabezpieczeniach są ustawione tooa ważność niski, co oznacza powinny być kierowane luka w zabezpieczeniach, ale nie wymaga natychmiastowej uwagi.

2. Wybierz maszynę Wirtualną. Bloku dla tej maszyny Wirtualnej zostanie otwarty i wyświetla hello reguł, które nie powiodły.
   ![Reguły konfiguracji, które nie powiodło się][2]

3. Wybierz regułę. W tym przykładzie pozwala wybrać **hasło musi spełniać wymagania co do złożoności**. Zostanie otwarty blok zawierająca opis wpływu reguły i hello hello nie powiodło się. Przejrzyj szczegóły hello i należy wziąć pod uwagę sposób stosowania konfiguracji systemu operacyjnego.
  ![Opis hello reguły nie powiodło się][3]

  Centrum zabezpieczeń używa typowych konfiguracji wyliczenie CCE () tooassign unikatowych identyfikatorów dla reguły konfiguracji. w tym bloku znajduje się Hello następujących informacji:

  - Nazwa — Nazwa reguły
  - WAŻNOŚĆ — Wartości ważności CCE krytyczna ważne i ostrzeżenia
  - CCIED — Unikatowy identyfikator CCE Witaj reguły
  - OPIS — Opis reguły
  - Luki w zabezpieczeniach — Opis usterki lub ryzyko, gdy nie jest stosowana reguła
  - WPŁYW — Wpływ na prowadzoną działalność po zastosowaniu reguły
  - OCZEKIWANA wartość — Wartość oczekiwana w przypadku Centrum zabezpieczeń analizuje względem hello reguły konfiguracji systemu operacyjnego maszyny Wirtualnej
  - — Reguła zasada operacji używane przez Centrum zabezpieczeń podczas analizy konfiguracji systemu operacyjnego maszyny Wirtualnej względem reguły hello
  - RZECZYWISTA wartość--Zwracana wartość po analizie względem hello reguły konfiguracji systemu operacyjnego maszyny Wirtualnej
  - WYNIK oceny —-wynik analizy: przekazywania błędów

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Skoryguj systemu operacyjnego luk w zabezpieczeniach." Możesz przejrzeć hello zbiór reguł konfiguracji [tutaj](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Centrum zabezpieczeń używa CCE (typowych konfiguracji wyliczenie) tooassign unikatowych identyfikatorów dla reguły konfiguracji. Odwiedź hello [CCE](https://nvd.nist.gov/cce/index.cfm) witryny, aby uzyskać więcej informacji.

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące zasoby hello:

* [Obsługiwane platformy w Centrum zabezpieczeń Azure](security-center-os-coverage.md) — zawiera listę obsługiwanych systemu Windows i maszyn wirtualnych systemu Linux.
* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
