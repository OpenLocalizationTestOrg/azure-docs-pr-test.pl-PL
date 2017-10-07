---
title: "aaaTroubleshoot połączenia typowe problemy tooAzure bazy danych SQL"
description: "Kroki tooidentify i rozwiązywanie typowych błędów połączenia bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Rozwiązywanie problemów z tooAzure problemów połączenia bazy danych SQL
Gdy hello tooAzure połączenia bazy danych SQL nie powiodło się, zostanie wyświetlony [komunikaty o błędach](sql-database-develop-error-messages.md). W tym artykule jest scentralizowane temat, który pomaga w rozwiązywaniu problemów z połączeniem bazy danych SQL Azure. Podaj [hello typowych przyczyn](#cause) problemów połączenie zaleca [rozwiązywania problemów](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) pomaga problem hello tożsamości i zawiera toosolve kroki rozwiązywania problemów [ błędów przejściowych](#troubleshoot-transient-errors) i [trwałe lub nieprzejściowego błędów](#troubleshoot-persistent-errors). 

Jeśli wystąpią problemy z połączeniem hello, spróbuj hello Rozwiązywanie problemów z kroków opisanych w tym artykule.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Przyczyna
Problemy z połączeniem może być spowodowane jedną z następujących przyczyn hello:

* Błąd tooapply najlepsze rozwiązania i wskazówki dotyczące projektowania podczas procesu projektowania aplikacji hello.  Zobacz [omówienie tworzenia bazy danych SQL](sql-database-develop-overview.md) tooget uruchomiona.
* Rekonfiguracji bazy danych SQL Azure
* Ustawienia zapory
* Limit czasu połączenia
* Informacje logowania niepoprawne
* Osiągnięto maksymalny limit dla niektórych zasobów bazy danych SQL Azure

Ogólnie rzecz biorąc tooAzure problemów połączenia bazy danych SQL mogą być klasyfikowane w następujący sposób:

* [Błędów przejściowych (krótkim okresie lub sporadyczne)](#troubleshoot-transient-errors)
* [Trwałe lub nieprzejściowego błędów (błędy, które regularnie powtarzać)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Spróbuj hello rozwiązywania problemów łączności bazy danych SQL Azure
W razie wystąpienia błędu określonego połączenia spróbować [to narzędzie](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), który będzie pomagają w szybkim tożsamości i rozwiązania problemu.

## <a name="troubleshoot-transient-errors"></a>Rozwiązywanie błędów przejściowych

Aplikacja nawiązuje połączenie z bazą danych Azure SQL tooan, pojawi się następujący komunikat o błędzie hello:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Ten komunikat o błędzie jest zwykle charakter przejściowy (krótkim okresie).
> 
> 

Ten błąd występuje, gdy hello Azure bazy danych są przenoszone (lub ponownie skonfigurować) i jego połączenia bazy danych SQL toohello utraci aplikacji. Występują zdarzenia ponownej konfiguracji bazy danych SQL z powodu planowanych zdarzeń (na przykład uaktualnienie oprogramowania) lub nieplanowanego zdarzenia (na przykład awaria procesu lub równoważenia obciążenia). Większość zdarzeń zmiany konfiguracji są zazwyczaj w krótkim okresie i należy wykonać w mniej niż 60 sekund co najwyżej. Jednak te zdarzenia czasami może potrwać dłużej toofinish, takie jak kiedy dużych transakcji powoduje odzyskiwania długotrwałe.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Kroki tooresolve łączności przejściowych problemów

1. Sprawdź hello [pulpicie nawigacyjnym usługi systemu Microsoft Azure](https://azure.microsoft.com/status) dla znanych wystąpienia awarii, które wystąpiły w czasie hello, podczas których hello aplikacji hello zgłoszenia błędów.
2. Aplikacje łączące tooa usługi w chmurze, takich jak bazy danych SQL Azure należy oczekiwać zdarzenia okresowe ponowna konfiguracja i wdrożenie ponów toohandle logiki te błędy, zamiast udostępniając je jako toousers błędów aplikacji. Przejrzyj hello [błędów przejściowych](sql-database-connectivity-issues.md) sekcji hello najlepsze rozwiązania i projektu wytyczne [omówienie tworzenia bazy danych SQL](sql-database-develop-overview.md) uzyskać więcej informacji oraz ogólne ponów strategii. Następnie, zobacz przykłady kodu w [biblioteki połączeń dla bazy danych SQL i programu SQL Server](sql-database-libraries.md) dla szczegółowych informacji.
3. Jako bazę danych zbliża się limit zasobów, może wydawać się toobe to problem przejściowy łączności. Zobacz [Rozwiązywanie problemów z wydajnością](sql-database-troubleshoot-performance.md).
4. Jeśli nadal występują problemy z łącznością lub jeśli hello czas trwania, dla których aplikacja napotka błąd hello przekracza 60 sekund lub jeśli w danym dniu wielu wystąpień błędu hello pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać obsługuje** na powitania [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options) lokacji.

## <a name="troubleshoot-persistent-errors"></a>Rozwiązywanie problemów trwałych
Jeśli aplikacja hello nie trwale tooAzure tooconnect bazy danych SQL, zwykle wskazuje problem z jedną z następujących hello:

* Konfiguracja zapory. Hello Azure SQL bazy danych lub po stronie klienta Zapora blokuje tooAzure połączenia bazy danych SQL.
* Ponowna konfiguracja po stronie klienta hello sieci: na przykład nowy adres IP lub serwer proxy.
* Błąd użytkownika: na przykład parametry połączenia, takie jak nazwa serwera hello w parametrach połączenia hello wpisana z błędem.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Kroki tooresolve trwałe połączenie problemów
1. Konfigurowanie [reguły zapory](sql-database-configure-firewall-settings.md) adres IP klienta hello tooallow. Dla tymczasowych do celów testowych Skonfiguruj regułę zapory przy użyciu 0.0.0.0 jako hello uruchamianie zakres adresów IP i przy użyciu 255.255.255.255 jako hello końcowa zakresu adresów IP. Spowoduje to otwarcie hello adresy IP tooall. Jeśli to rozwiązuje problem z łącznością, należy usunąć tę regułę i utworzyć regułę zapory odpowiednio ograniczone adres IP lub zakres adresów. 
2. Upewnij się, że port 1433 jest otwarty dla połączeń wychodzących na wszystkie zapory między powitania klienta i hello Internet. Przegląd [skonfigurować tooAllow zapory systemu Windows hello dostęp do programu SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) i [hybrydowego tożsamości wymagane porty i protokoły](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) dodatkowe wskaźniki związanych z tooadditional porty, które należy tooopen dla Uwierzytelnianie usługi Active Directory systemu Azure.
3. Sprawdź ciąg połączenia i inne ustawienia połączenia. Zobacz hello sekcji Parametry połączenia w hello [tematu problemy z łącznością](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Sprawdź kondycję usług hello w pulpicie nawigacyjnym. Jeśli uważasz, że istnieje regionalnej awarii, zobacz [odzyskiwanie po awarii](sql-database-disaster-recovery.md) dla czynności toorecover tooa nowego obszaru.

## <a name="next-steps"></a>Następne kroki
* [Rozwiązywanie problemów z wydajnością bazy danych SQL Azure](sql-database-troubleshoot-performance.md)
* [Dokumentacja hello wyszukiwania w systemie Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Widok hello najnowszych aktualizacji toohello usługi baza danych SQL Azure](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Omówienie tworzenia bazy danych SQL](sql-database-develop-overview.md)
* [Ogólne wskazówki obsługi błędów przejściowych](../best-practices-retry-general.md)
* [Biblioteki połączeń dla bazy danych SQL i programu SQL Server](sql-database-libraries.md)

