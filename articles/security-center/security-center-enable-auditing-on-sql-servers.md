---
title: "aaaEnable inspekcji i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL **."
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
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Włącz inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zostanie zaleca włączenie inspekcji i wykrywanie zagrożeń dla wszystkich baz danych na serwerach Azure SQL, jeśli inspekcji nie jest jeszcze włączone. Inspekcja i jakie wykrywania pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.

Po włączeniu inspekcji można skonfigurować wykrywanie zagrożeń ustawienia i wiadomości e-mail tooreceive alertów zabezpieczeń. Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych. To pozwala toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania.

To zalecenie dotyczy toohello usługi Azure SQL. nie ma wśród nich programu SQL Server uruchomionego na maszynach wirtualnych w usługi infrastruktury platformy Azure (IaaS platformy Azure).

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL**.  Spowoduje to otwarcie hello **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL** bloku.

   ![Włączanie inspekcji dla serwerów SQL][1]
2. Wybierz program SQL server tooenable inspekcji i wykrywania zagrożeń. Spowoduje to otwarcie hello **Inspekcja i wykrywanie zagrożeń** bloku.

3. Na powitania **Inspekcja i wykrywanie zagrożeń** bloku, wybierz opcję **ON** w obszarze **inspekcji**.

   ![Włączanie ustawień inspekcji][2]
4. Wykonaj kroki hello w [inspekcja bazy danych SQL w hello portalu Azure](../sql-database/sql-database-auditing-portal.md) magazynu tooconfigure przechowywania dzienników inspekcji. Witaj konta magazynu dla tej subskrypcji do zbierania danych jest hello domyślne konto magazynu.
5. Wykonaj kroki hello w [wprowadzenie wykrywanie zagrożeń bazy danych SQL](../sql-database/sql-database-threat-detection.md) tooturn na i skonfiguruj wykrywanie zagrożeń i tooconfigure hello listę wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Włączania inspekcji i wykrywanie na serwerach SQL zagrożeń". toolearn więcej informacji na temat zabezpieczania bazy danych SQL, zobacz następujące hello:

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
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
