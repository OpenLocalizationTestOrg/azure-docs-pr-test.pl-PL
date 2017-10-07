---
title: "aaaEnable inspekcji i wykrywania zagrożeń SQL bazy danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć inspekcję i wykrywania zagrożeń na baz danych SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a>Włącz inspekcję i wykrywania zagrożeń baz danych SQL w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zostanie zaleca włączenie inspekcji i wykrywania zagrożeń dla wszystkich baz danych SQL, jeśli inspekcja i wykrywanie zagrożeń nie jest jeszcze włączone. Inspekcja i jakie wykrywania pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.

Po włączeniu inspekcji można skonfigurować wykrywanie zagrożeń ustawienia i wiadomości e-mail tooreceive alertów zabezpieczeń. Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych. To pozwala toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania.

To zalecenie dotyczy toohello usługi Azure SQL. nie ma wśród nich SQL uruchomionych na maszynach wirtualnych.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **Włączanie inspekcji i wykrywanie zagrożeń baz danych SQL**.  Spowoduje to otwarcie hello **Włączanie inspekcji i wykrywanie zagrożeń baz danych SQL** bloku.

   ![Włączanie inspekcji dla baz danych SQL][1]
2. Wybierz tooenable bazy danych SQL inspekcji na. Spowoduje to otwarcie hello **Inspekcja i wykrywanie zagrożeń** bloku.

3. Na powitania **Inspekcja i wykrywanie zagrożeń** bloku, wybierz opcję **ON** w obszarze **inspekcji**.

   ![Włączanie inspekcji i wykrywania zagrożeń][2]
4. Wykonaj kroki hello w [wykrywanie zagrożeń bazy danych SQL w portalu Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn na i skonfiguruj wykrywanie zagrożeń i tooconfigure hello listę wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz Inspekcja i wykrywanie zagrożeń baz danych SQL." toolearn więcej informacji na temat zabezpieczania bazy danych SQL, zobacz następujące hello:

* [Zabezpieczanie bazy danych SQL](../sql-database/sql-database-security-overview.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
