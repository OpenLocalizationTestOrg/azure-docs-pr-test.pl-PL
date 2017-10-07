---
title: "Szyfrowanie bazy danych magazynowanych: bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bazy danych rozwiązania Cosmos Azure udostępnia domyślne szyfrowanie wszystkich danych."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Azure DB rozwiązania Cosmos szyfrowania bazy danych w stanie spoczynku

Szyfrowanie rest jest frazę, która oznacza najczęściej toohello szyfrowania danych na urządzeniach nieulotnej pamięci masowej, takich jak półprzewodnikowe dyski (SSD) i dysków twardych (HDD). Rozwiązania cosmos bazy danych są przechowywane jego głównej bazy danych na dyskach SSD. Jego załączniki nośników i kopii zapasowych są przechowywane w magazynie obiektów Blob platformy Azure, które zazwyczaj została skopiowana przez użycie dysków twardych. Witaj wersji z szyfrowania magazynowane rozwiązania Cosmos bazy danych wszystkie bazy danych, załączniki nośników i kopii zapasowych są szyfrowane. Dane są teraz szyfrowane podczas przesyłania (za pośrednictwem sieci hello) i w stanie spoczynku (nieulotnej pamięci masowej), umożliwiając szyfrowanie na całej trasie.

Jak usługa PaaS, rozwiązania Cosmos bazy danych jest bardzo proste toouse. Ponieważ wszystkie dane użytkownika przechowywane w bazie danych rozwiązania Cosmos są szyfrowane podczas przechowywania i podczas transportu, nie masz tootake żadnych działań. Inny sposób tooput jest tym szyfrowanie rest jest "na" domyślnie. Nie ma żadnych tooturn formantów go lub wyłączyć. Firma Microsoft udostępnia tę funkcję, będziemy nadal toomeet naszych [SLA dostępności i wydajności](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Wdrożenia szyfrowania magazynowane

Szyfrowanie magazynowane jest implementowane za pomocą wielu technologii zabezpieczeń, takich jak systemy bezpiecznego magazynu kluczy, zaszyfrowanych sieci i interfejsów API usług kryptograficznych. Systemy odszyfrować i przetwarza dane mają toocommunicate z systemów, które zarządzania kluczami. Hello diagram pokazuje, jak magazynu zaszyfrowanych danych i hello zarządzanie kluczami jest oddzielona. 

![Diagram projektu](./media/database-encryption-at-rest/design-diagram.png)

podstawowy przepływ Hello żądania użytkownika jest następujący:
- konto bazy danych użytkownika Hello jest gotów i magazynu kluczy są pobierane za pomocą żądania toohello dostawcy zasobów usługi zarządzania.
- Użytkownik tworzy tooCosmos połączenia bazy danych za pośrednictwem protokołu HTTPS/secure transportu. (szczegóły abstrakcyjny hello zestawów SDK hello).
- Witaj użytkownik wysyła toobe dokumentów JSON przechowywanych przez hello wcześniej utworzony bezpiecznego połączenia.
- dokument JSON Hello jest indeksowana nie hello użytkownik wyłączył indeksowania.
- Zarówno hello dokument JSON i dane indeksu są zapisywane toosecure magazynu.
- Okresowo dane są odczytywane hello bezpiecznego magazynu i kopii zapasowej toohello magazynu obiektów Blob zaszyfrowane Azure.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>Pytanie: jak bardziej usługi Azure Storage koszt Jeśli włączono szyfrowanie usługi Magazyn?
Odpowiedź: nie istnieje bez dodatkowych kosztów.

### <a name="q-who-manages-hello-encryption-keys"></a>Pytanie: zarządzająca hello klucze szyfrowania?
A: Witaj klucze są zarządzane przez firmę Microsoft.

### <a name="q-how-often-are-encryption-keys-rotated"></a>Pytanie: jak często są obracane klucze szyfrowania?
Odpowiedź: Microsoft ma zestaw wewnętrzne wytyczne dotyczące obrotu klucza szyfrowania, następującego rozwiązania Cosmos bazy danych. szczegółowe wytyczne Hello nie są publikowane. Microsoft publikowania hello [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), który jest traktowany jako podzbiór wewnętrzny wskazówki i ma przydatne wskazówki dla deweloperów.

### <a name="q-can-i-use-my-own-encryption-keys"></a>Pytanie: czy można użyć własnych kluczy szyfrowania?
A: rozwiązania cosmos bazy danych jest usługą PaaS i firma Microsoft pracuje toouse łatwe tookeep twardym powitania usługi. Zauważyliśmy, że to pytanie jest często zadawane jako serwer proxy pytanie najlepiej spełniającej wymagania zgodności, takie jak PCI-DSS. W ramach tworzenia tej funkcji firma Microsoft we współpracy z tooensure o obrachunkowego zgodności klienci korzystający z rozwiązania Cosmos DB spełniania wymagań bez hello potrzeby toomanage samych kluczy.
W związku z tym obecnie nie oferujemy tooburden opcji hello użytkownicy sami z zarządzania kluczami.

### <a name="q-what-regions-have-encryption-turned-on"></a>Pytanie: jakie regiony z włączonym szyfrowaniem?
Odpowiedź: rozwiązania Cosmos Azure DB regiony z szyfrowania włączona dla wszystkich danych użytkownika.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>Pyt.: szyfrowanie wpływa na powitania opóźnienia wydajności i przepływności umów SLA?
Odpowiedź: jest nie wpływu zmiany toohello wydajności lub umów SLA teraz szyfrowanie magazynowanych jest włączona dla wszystkich istniejących i nowych kont. Więcej na powitania [umowy SLA dla rozwiązania Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) strony toosee hello najnowsze gwarancji.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>Pytanie: czy emulator lokalne powitania obsługuje szyfrowanie magazynowane?
A: hello emulator jest to samodzielne narzędzie i testowania i nie używa hello usług zarządzania kluczami, które hello zarządzanych używa usługi DB rozwiązania Cosmos. Nasze zalecenie jest tooenable funkcji BitLocker na dyskach, w której są przechowywane emulatora poufnych danych testowych. Witaj [emulatora obsługuje zmieniania hello domyślny katalog danych](local-emulator.md) oraz przy użyciu dobrze znanej lokalizacji.

## <a name="next-steps"></a>Następne kroki

Omówienie rozwiązania Cosmos DB zabezpieczeń i hello najnowszych ulepszeń, zobacz [zabezpieczeń bazy danych Azure DB rozwiązania Cosmos](database-security.md).
Aby uzyskać więcej informacji o certyfikatach firmy Microsoft, zobacz hello [Centrum zaufania Azure](https://azure.microsoft.com/en-us/support/trust-center/).
