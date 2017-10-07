---
title: "aaaOverview bazy danych Azure dla usługa relacyjnej bazy danych PostgreSQL | Dokumentacja firmy Microsoft"
description: "Omówienie bazy danych Azure dla PostgreSQL usługa relacyjnej bazy danych."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>Co to jest Azure bazy danych PostgreSQL?

Bazy danych PostgreSQL Azure to usługa relacyjnej bazy danych w hello firmy Microsoft w chmurze skompilowana dla deweloperów na podstawie wersji społeczności hello typu open source [PostgreSQL](https://www.postgresql.org/) aparatu bazy danych. Ta usługa jest w wersji zapoznawczej. Bazy danych platformy Azure dla PostgreSQL zapewnia:
- Przewidywalna wydajność na różnych poziomach usługi
- Dynamiczne skalowalność bez przestojów aplikacji
- Wbudowaną wysoką dostępność
- Ochrona danych

Wszystkie te funkcje wymagają prawie nie administracji, a wszystkie znajdują się bez ponoszenia dodatkowych kosztów. Te funkcje umożliwiają toofocus szybkie programowanie aplikacji i przyspieszając toomarket Twojego czasu, zamiast przydzielania cenny czas i maszyn wirtualnych toomanaging zasobów i infrastruktury. Ponadto możesz kontynuować toodevelop do aplikacji z hello otworzyć narzędzia źródła i platform wybranych przez użytkownika i dostarczanie z hello szybkości i wydajności firmy wymaga bez konieczności toolearn nowe umiejętności. 

Ten artykuł obejmuje wprowadzenie tooAzure bazy danych PostgreSQL podstawowe koncepcje i tooperformance powiązanych funkcji, skalowalności i możliwości zarządzania. Zobacz, czy te szybkiego uruchamiania tooget rozpoczętej:

- [Tworzenie bazy danych Azure dla PostgreSQL przy użyciu portalu Azure](quickstart-create-server-database-portal.md)
- [Tworzenie bazy danych Azure dla PostgreSQL przy użyciu hello wiersza polecenia platformy Azure](quickstart-create-server-database-azure-cli.md)

Aby uzyskać zestaw przykładów interfejsu wiersza polecenia platformy Azure i programu PowerShell, zobacz:

- [Przykładów dla interfejsu wiersza polecenia platformy Azure dla bazy danych Azure dla PostgreSQL](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Dostosowanie wydajności i skalowanie bez przestojów

Bazy danych platformy Azure dla usługi PostgreSQL obecnie oferuje dwie warstwy usług: Basic i Standard. Każda warstwa usług oferuje [różne poziomy wydajności, gwarancji IOPS i możliwości](concepts-service-tiers.md) toosupport tooheavyweight lekkie bazy danych obciążeń. Można utworzyć pierwszą aplikację na serwerze małych za niewielką sumę miesięcznie, a następnie [zmienić poziom wydajności hello](scripts/sample-scale-server-up-or-down.md) w ramach usługi warstwy ręcznie lub programowo w dowolnej potrzeb hello toomeet czas rozwiązania. Można to zrobić bez przestojów tooyour aplikacji lub tooyour klientów. Umożliwia dynamiczne skalowalność tootransparently Twojej bazy danych odpowiada toorapidly zmiany wymagań dotyczących zasobów i umożliwia tooonly można płacić za zasoby hello należy najodpowiedniejszym czasie.

## <a name="monitoring-and-alerting"></a>Monitorowanie i zgłaszanie alertów
Jak można określić podczas toodial w górę i w dół? Możesz użyć hello wbudowanych wydajności monitorowania oraz alertów funkcji, z hello oceny wydajności na podstawie obliczeniowe jednostek. Za pomocą tych narzędzi, może szybko ocenić wpływ hello skalowania obliczeniowe jednostki lub w dół na podstawie potrzeb bieżącego lub planowane wydajności. Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla PostgreSQL opcje i wydajność: Poznaj, co jest dostępne w poszczególnych warstwach usług](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Zapewnienie działania aplikacji i firmy
Azure w branży 99,99% dostępności (niedostępne w wersji zapoznawczej) umowę dotyczącą poziomu usług (SLA), obsługiwane przez usługę globalnej sieci centrów danych zarządzany przez firmę Microsoft, pomaga zapewnić działanie aplikacji 24/7. Z każdym Azure bazy danych PostgreSQL serwera możesz korzystać z zabezpieczeń, odporność na uszkodzenia i ochrony danych, w przeciwnym razie trzeba będzie toobuy lub projektowanie, tworzenie i zarządzanie nimi. Z bazy danych Azure PostgreSQL każda warstwa usług oferuje kompleksowe zbiór funkcjach ciągłości biznesowej i opcje, które można korzystać z tooget i kontynuować w ten sposób. Można użyć [w momencie przywracania](howto-restore-server-portal.md) tooreturn tooan bazy danych wcześniej stanu, nawet sprzed 35 dni. Ponadto jeśli hello centrum danych hostujące bazy danych ulegnie awarii, można przywrócić bazy danych z geograficznie nadmiarowego kopie ostatnie kopie zapasowe.

## <a name="secure-your-data"></a>Zabezpieczanie danych
Usługi Azure bazy danych ma tradycję bezpieczeństwa danych, czy baza danych Azure dla PostgreSQL podtrzymuje dzięki funkcjom ograniczania dostępu, ochrony danych na rest i w ruchu i monitorowania aktywności. Odwiedź hello [Centrum zaufania Azure](https://www.microsoft.com/TrustCenter/Security/default.aspx) informacji o zabezpieczeniach platformy Azure.

Hello Azure bazy danych dla usługi PostgreSQL używa szyfrowania magazynu dla danych na rest. W tym kopie zapasowe danych są szyfrowane na dysku (z wyjątkiem hello plików tymczasowych utworzonych przez aparat hello podczas uruchamiania zapytań). Usługa Hello używa szyfrowania AES 256-bitowy, należący do szyfrowania magazynu Azure, a klucze hello jest kontrolowany przez system. Szyfrowanie magazynu jest zawsze włączone i nie można wyłączyć.

Domyślnie hello Azure bazy danych dla usługi PostgreSQL jest skonfigurowany toorequire [zabezpieczeń połączenia SSL](./concepts-ssl-connection-security.md) dla danych w ruchu w sieci hello. Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.  Opcjonalnie możesz wyłączyć wymaganie protokołu SSL dla połączenia tooyour usługi bazy danych, jeśli aplikacja kliencka nie obsługuje łączności SSL.

## <a name="next-steps"></a>Następne kroki
- Zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/postgresql/) koszt porównania i kalkulatory.
- Rozpoczynanie pracy przez [tworzenie pierwszej bazy danych Azure dla PostgreSQL](./quickstart-create-server-database-portal.md).
- Tworzenie pierwszej aplikacji w języku Python, PHP, Ruby, C\#, Java, Node.js: [biblioteki połączeń](./concepts-connection-libraries.md)
