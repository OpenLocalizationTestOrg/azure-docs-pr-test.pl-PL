---
title: "aktualizacje systemu aaaApply w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zaleceń Centrum zabezpieczeń Azure ** zastosować aktualizacje systemu ** i ** ponowny rozruch po aktualizacji systemu **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure codziennie monitoruje systemu Windows i Linux maszynach wirtualnych (VM) brakujących aktualizacji systemu operacyjnego. Centrum zabezpieczeń pobiera listę dostępnych zabezpieczeń i krytycznych aktualizacji z witryny Windows Update lub Windows Server Update Services (WSUS), w zależności od tego, który usługa jest skonfigurowana na maszynie Wirtualnej systemu Windows.  Centrum zabezpieczeń sprawdza również hello najnowsze aktualizacje w systemach Linux. Jeśli maszyna wirtualna jest Brak aktualizacji systemu, Centrum zabezpieczeń zaleca się zastosowanie aktualizacji systemu

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **stosowanie aktualizacji systemu**.

   ![Zastosuj aktualizacje systemu][1]
2. Witaj **stosowanie aktualizacji systemu** zostanie otwarty blok zawierający listę maszyn wirtualnych Brak aktualizacji systemu. Wybierz maszynę Wirtualną.

   ![Wybierz maszynę Wirtualną][2]
3. Zostanie otwarty blok zawierający listę brakujących aktualizacji dla tej maszyny Wirtualnej. Wybierz aktualizację systemu. W tym przykładzie załóżmy wybierz KB3156016.

   ![Brakujące aktualizacje zabezpieczeń][3]

4. Wykonaj kroki hello hello **aktualizacji zabezpieczeń** tooapply bloku hello brakujących aktualizacji.

   ![Aktualizacja zabezpieczeń][4]

## <a name="reboot-after-system-updates"></a>Uruchom ponownie po zaktualizowaniu systemu
1. Zwraca toohello **zalecenia** bloku. Wygenerowano nowy wpis, po zastosowaniu aktualizacji systemu, o nazwie **ponowny rozruch po aktualizacji systemu**. Ten wpis informuje o tym, że należy tooreboot hello wirtualna toocomplete hello proces stosowania aktualizacji systemu.

   ![Uruchom ponownie po zaktualizowaniu systemu][5]
2. Wybierz **ponowny rozruch po aktualizacji systemu**. Spowoduje to otwarcie **toocomplete oczekujące aktualizacje systemu jest ponowne uruchomienie** blok zawierający listę maszyn wirtualnych konieczność toorestart toocomplete hello zastosowania procesu aktualizacji systemu.

   ![Oczekiwanie na ponowne uruchomienie][6]

Uruchom ponownie hello maszyny Wirtualnej z platformy Azure toocomplete hello procesu.

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
