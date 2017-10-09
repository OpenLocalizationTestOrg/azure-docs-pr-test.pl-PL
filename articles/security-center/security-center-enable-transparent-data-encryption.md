---
title: "aaaEnable przezroczystego szyfrowania danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć przezroczysty danych szyfrowania **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Włącz przezroczystego szyfrowania danych w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca Włącz funkcji przezroczystego szyfrowania danych (TDE) baz danych SQL, jeśli nie jest już włączona funkcji TDE. Funkcji TDE chroni dane i pomaga spełnić wymagania zgodności przez zaszyfrowanie bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku, bez konieczności wprowadzania zmian tooyour aplikacji. więcej Zobacz toolearn [przezroczystego szyfrowania danych z bazy danych SQL Azure](https://msdn.microsoft.com/library/dn948096).

To zalecenie dotyczy toohello usługi Azure SQL. nie zawiera SQL uruchomionych na maszynach wirtualnych.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **włączyć przezroczystego szyfrowania danych**.
   ![Włączanie technologii Transparent Data Encryption][1]
2. Spowoduje to otwarcie hello **włączyć przezroczystego szyfrowania danych w bazach danych SQL** bloku. Wybierz tooenable bazy danych SQL funkcji TDE.
   ![Wybierz bazy danych SQL tooenable funkcji TDE na][2]
3. Na powitania **przezroczystego szyfrowania danych** bloku, wybierz opcję **ON** szyfrowania danych i wybierz **zapisać** hello wstążce top hello bloku.
   ![Włączanie funkcji TDE][3]

   Po włączeniu funkcji TDE hello wybrana baza danych SQL, hello **stanu szyfrowania** zmieni się zbyt**zaszyfrowane**.    

   ![Stan szyfrowania][4]

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Włącz przezroczystego szyfrowania danych." toolearn więcej informacji na temat funkcji SQL TDE znaleźć hello w następujących tematach:

* [Przezroczystego szyfrowania danych z bazy danych Azure SQL](https://msdn.microsoft.com/library/dn948096)
* [Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
