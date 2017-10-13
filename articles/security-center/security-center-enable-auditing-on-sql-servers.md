---
title: "Włącz inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Włącz inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zostanie zaleca włączenie inspekcji i wykrywanie zagrożeń dla wszystkich baz danych na serwerach Azure SQL, jeśli inspekcji nie jest jeszcze włączone. Inspekcja i jakie wykrywania pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.

Po włączeniu inspekcji można skonfigurować ustawienia wykrywanie zagrożeń i wiadomości e-mail, aby otrzymywać alerty zabezpieczeń. Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazują możliwe zagrożenia bezpieczeństwa w bazie danych. Umożliwia to wykrywanie i odpowiadanie na potencjalne zagrożenia w miarę ich występowania.

To zalecenie stosuje się do usługi Azure SQL. nie ma wśród nich programu SQL Server uruchomionego na maszynach wirtualnych w usługi infrastruktury platformy Azure (IaaS platformy Azure).

> [!NOTE]
> Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-the-recommendation"></a>Wykonania zalecenia
1. W **zalecenia** bloku, wybierz opcję **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL**.  Spowoduje to otwarcie **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL** bloku.

   ![Włączanie inspekcji dla serwerów SQL][1]
2. Wybierz serwer SQL, Włącz inspekcję i wykrywania zagrożeń. Spowoduje to otwarcie **Inspekcja i wykrywanie zagrożeń** bloku.

3. Na **Inspekcja i wykrywanie zagrożeń** bloku, wybierz opcję **ON** w obszarze **inspekcji**.

   ![Włączanie ustawień inspekcji][2]
4. Postępuj zgodnie z instrukcjami [inspekcja bazy danych SQL w portalu Azure](../sql-database/sql-database-auditing-portal.md) skonfigurować Magazyn przechowywania dzienników inspekcji. Konto magazynu subskrypcji na potrzeby zbierania danych jest domyślne konto magazynu.
5. Postępuj zgodnie z instrukcjami [wprowadzenie wykrywanie zagrożeń bazy danych SQL](../sql-database/sql-database-threat-detection.md) włączać i konfigurować wykrywanie zagrożeń i skonfigurować listę wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.

## <a name="see-also"></a>Zobacz też
W tym artykule przedstawiono sposób wdrożenia Centrum zabezpieczeń zalecenie "włączania inspekcji i wykrywania zagrożeń na serwerach SQL." Aby dowiedzieć się więcej na temat zabezpieczania bazy danych SQL, zobacz następujące tematy:

* [Zabezpieczanie bazy danych SQL](../sql-database/sql-database-security-overview.md)

Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

* [Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Uzyskaj najnowsze informacje zabezpieczeń platformy Azure i informacje.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
