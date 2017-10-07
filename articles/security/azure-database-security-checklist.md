---
title: "Lista kontrolna zabezpieczeń bazy danych aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw Lista kontrolna zabezpieczeń bazy danych platformy Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Lista kontrolna zabezpieczeń bazy danych platformy Azure

toohelp zwiększyć bezpieczeństwo, baza danych Azure zawiera szereg kontroli zabezpieczeń można użyć toolimit i kontroli dostępu.

Należą do nich:

-   Zaporą, która umożliwia toocreate [reguły zapory](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) ograniczenie łączności za pomocą adresu IP
-   Dostępna z portalu Azure hello zapory poziomu serwera
-   Reguły zapory poziomu bazy danych dostępne w programie SSMS
-   Bazy danych tooyour bezpieczne połączenie za pomocą bezpiecznego połączenia ciągów
-   Użyj zarządzania dostępem
-   Szyfrowanie danych
-   Inspekcja bazy danych SQL
-   Wykrywanie zagrożeń bazy danych SQL

## <a name="introduction"></a>Wprowadzenie
Chmura obliczeniowa wymaga nowej wzorcami zabezpieczeń będących toomany doświadczenia w pracy aplikacji użytkowników, administratorów bazy danych i programistów. W związku z tym niektóre organizacje są tooimplement wątpliwości infrastruktury chmury w celu zarządzania danymi powodu tooperceived zagrożenia bezpieczeństwa. Jednak większość tego problemu mogą być złagodzone do lepszego zrozumienia hello funkcji wbudowanych w Microsoft Azure i bazy danych SQL Azure firmy Microsoft.

## <a name="checklist"></a>Lista kontrolna
Zalecamy przeczytanie hello [najlepsze rozwiązania zabezpieczeń bazy danych Azure](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) artykuł wcześniejsze tooreviewing ta lista kontrolna. Po zidentyfikowaniu hello najlepszych rozwiązań, będzie hello tooget mogli korzystać z tej listy kontrolnej. Następnie można użyć tej listy kontrolnej toomake się upewnić, że uwzględniono hello istotne problemy w zabezpieczeń bazy danych Azure.


|Lista kontrolna kategorii| Opis|
| ------------ | -------- |
|**Ochrona danych**||
| <br> Szyfrowanie podczas przesyłania/ruchu| <ul><li>[Transport Layer Security](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), do szyfrowania danych, gdy dane są przenoszone toohello sieci.</li><li>Baza danych wymaga zapewnienia bezpiecznej komunikacji z klientami oparte na powitania [TDS (strumienia danych tabelarycznych)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) na protokole TLS (Transport Layer Security).</li></ul> |
|<br>Szyfrowanie w spoczynku| <ul><li>[Funkcja przezroczystego szyfrowania danych](http://go.microsoft.com/fwlink/?LinkId=526242), gdy nieaktywne dane są przechowywane w fizycznie w jakimkolwiek formularzu cyfrowego.</li></ul>|
|**Kontrola dostępu**||  
|<br> Dostęp do bazy danych | <ul><li>[Uwierzytelnianie](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Azure Active Directory Authentication) AD uwierzytelniania przy użyciu tożsamości zarządzanych przez usługę Azure Active Directory.</li><li>[Autoryzacji](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) przyznania użytkownikom hello co najmniej uprawnienia niezbędne.</li></ul> |
|<br>Dostęp do aplikacji| <ul><li>[Poziom zabezpieczeń wiersz](https://msdn.microsoft.com/library/dn765131) (przy użyciu zasad zabezpieczeń na powitania jednocześnie ograniczając dostęp na poziomie wiersza na podstawie użytkownika tożsamości, roli lub wykonywania kontekstu).</li><li>[Dynamiczne maskowanie danych](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (przy użyciu uprawnień i zasady, limity ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników)</li></ul>|
|**Aktywne monitorowanie**||  
| <br>Śledzenie & wykrywania| <ul><li>[Inspekcja](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) śledzi zdarzenia bazy danych i zapisuje je w dzienniku inspekcji tooan / log działania sieci [konta magazynu Azure](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Przy użyciu kondycji bazy danych Azure Śledź [Dzienniki aktywności monitora Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Wykrywanie zagrożeń](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych. </li></ul> |
|<br>Azure Security Center| <ul><li>[Monitorowanie danych](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) korzystanie z Centrum zabezpieczeń Azure jako scentralizowanych zabezpieczeń rozwiązanie monitorujące, SQL i innymi usługami Azure.</li></ul>|     

## <a name="conclusion"></a>Podsumowanie
Bazy danych platformy Azure to platforma niezawodne bazy danych, z pełnym zakresem funkcji zabezpieczeń, które spełniają wymagania organizacyjne i przepisami zgodności wiele. Kontrolowanie hello dostęp fizyczny tooyour danych, a za pomocą różnych opcji zabezpieczeń danych na powitania pliku, kolumny lub poziomie wiersza niewidocznego szyfrowania danych, szyfrowanie na poziomie komórki lub zabezpieczenia na poziomie wiersza może łatwo chronić dane. Zawsze zaszyfrowane umożliwia również operacji względem zaszyfrowane dane, co upraszcza proces aktualizacji aplikacji hello. Z kolei dostępu tooauditing Dzienniki aktywności bazy danych SQL pozwala hello potrzebne informacje, dzięki czemu tooknow, jak i kiedy jest uzyskiwany dostęp do danych.

## <a name="next-steps"></a>Następne kroki
Można zwiększyć hello ochrony bazy danych przed złośliwymi użytkownikami lub nieautoryzowanego dostępu, wystarczy kilka prostych kroków. W tym samouczku dowiesz się:

- Konfigurowanie [reguły zapory](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) serwera i lub bazy danych.
- Ochrona danych za pomocą [szyfrowania](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Włącz [inspekcji bazy danych SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

