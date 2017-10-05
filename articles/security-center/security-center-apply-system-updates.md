---
title: "Stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera implementowania zaleceń Centrum zabezpieczeń Azure ** zastosować aktualizacje systemu ** i ** ponowny rozruch po aktualizacji systemu **."
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure codziennie monitoruje systemu Windows i Linux maszynach wirtualnych (VM) brakujących aktualizacji systemu operacyjnego. Centrum zabezpieczeń pobiera listę dostępnych zabezpieczeń i krytycznych aktualizacji z witryny Windows Update lub Windows Server Update Services (WSUS), w zależności od tego, który usługa jest skonfigurowana na maszynie Wirtualnej systemu Windows.  Centrum zabezpieczeń sprawdza także najnowsze aktualizacje w systemach Linux. Jeśli maszyna wirtualna jest Brak aktualizacji systemu, Centrum zabezpieczeń zaleca się zastosowanie aktualizacji systemu

> [!NOTE]
> Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-the-recommendation"></a>Wykonania zalecenia
1. W **zalecenia** bloku, wybierz opcję **stosowanie aktualizacji systemu**.

   ![Zastosuj aktualizacje systemu][1]
2. **Stosowanie aktualizacji systemu** zostanie otwarty blok zawierający listę maszyn wirtualnych Brak aktualizacji systemu. Wybierz maszynę Wirtualną.

   ![Wybierz maszynę Wirtualną][2]
3. Zostanie otwarty blok zawierający listę brakujących aktualizacji dla tej maszyny Wirtualnej. Wybierz aktualizację systemu. W tym przykładzie załóżmy wybierz KB3156016.

   ![Brakujące aktualizacje zabezpieczeń][3]

4. Postępuj zgodnie z instrukcjami **aktualizacji zabezpieczeń** bloku, aby zastosować brakujących aktualizacji.

   ![Aktualizacja zabezpieczeń][4]

## <a name="reboot-after-system-updates"></a>Uruchom ponownie po zaktualizowaniu systemu
1. Wróć do **zalecenia** bloku. Wygenerowano nowy wpis, po zastosowaniu aktualizacji systemu, o nazwie **ponowny rozruch po aktualizacji systemu**. Ten wpis informuje o tym, że należy przeprowadzić ponowny rozruch maszyny Wirtualnej, aby ukończyć proces stosowania aktualizacji systemu.

   ![Uruchom ponownie po zaktualizowaniu systemu][5]
2. Wybierz **ponowny rozruch po aktualizacji systemu**. Spowoduje to otwarcie **oczekuje na ponowne uruchomienie do ukończenia aktualizacji systemu** blok zawierający listę maszyn wirtualnych, które należy ponownie przeprowadzić systemu Zastosuj aktualizacje procesu.

   ![Oczekiwanie na ponowne uruchomienie][6]

Uruchom ponownie maszynę Wirtualną z platformy Azure, aby ukończyć proces.

## <a name="see-also"></a>Zobacz też
Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

* [Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
