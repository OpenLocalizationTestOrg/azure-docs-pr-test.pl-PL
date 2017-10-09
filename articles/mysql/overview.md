---
title: "aaaOverview bazy danych Azure dla usługa relacyjnej bazy danych MySQL | Dokumentacja firmy Microsoft"
description: "Przegląd hello Azure bazy danych dla usługa relacyjnej bazy danych MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Co to jest Azure bazy danych MySQL? Wprowadzenie do usługi
Bazy danych platformy Azure dla programu MySQL to usługa relacyjnej bazy danych w hello firmy Microsoft w chmurze na podstawie [MySQL Community Edition](https://www.mysql.com/products/community/) aparatu bazy danych.  Bazy danych platformy Azure dla programu MySQL zapewnia:

- Przewidywalna wydajność na różnych poziomach usługi
- Dynamiczne skalowalność bez przestojów aplikacji
- Wbudowaną wysoką dostępność
- Ochrona danych

Te możliwości wymagają prawie nie administracji, a wszystkie są dostarczane bez ponoszenia dodatkowych kosztów. Umożliwiają one toofocus na tworzenie aplikacji szybki i przyspieszając toomarket Twojego czasu, zamiast przydzielania cenny czas i maszyn wirtualnych toomanaging zasobów i infrastruktury. Ponadto możesz kontynuować toodevelop do aplikacji z hello otworzyć narzędzia źródła i platform wybranych przez użytkownika i dostarczanie z hello szybkości i wydajności firmy wymaga bez konieczności toolearn nowe umiejętności.

![Azure bazy danych MySQL diagram koncepcyjny](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Ten artykuł obejmuje wprowadzenie tooAzure bazy danych MySQL podstawowe koncepcje i tooperformance powiązanych funkcji, skalowalności i możliwości zarządzania przy użyciu łącza tooexplore szczegółów. Zobacz, czy te szybkiego uruchamiania tooget rozpoczętej:
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Tworzenie serwera usługi Azure Database for MySQL za pomocą interfejsu wiersza polecenia platformy Azure](quickstart-create-mysql-server-database-using-azure-cli.md)

Zestaw przykładów wiersza polecenia platformy Azure zobacz:
- [Przykładów dla interfejsu wiersza polecenia platformy Azure dla bazy danych Azure dla programu MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Dostosowanie wydajności i skalowanie bez przestojów
Bazy danych platformy Azure dla usługi MySQL oferuje dwie warstwy usług: Basic i Standard. Każda warstwa oferuje różne wydajności i możliwości toosupport lekkie tooheavyweight bazy danych obciążeń. Można utworzyć pierwszą aplikację na małej bazie danych dla kilku dolarów, miesiąc, a następnie zmień Twoje tooscale warstwy usługi z potrzebuje rozwiązania bez przestojów. Skalowalność dynamiczne umożliwia Twojej bazy danych toorapidly odpowiedź tootransparently zmiany wymagań dotyczących zasobów. Płacisz tylko za hello potrzebne zasoby, gdy są potrzebne.

## <a name="monitoring-and-alerting"></a>Monitorowanie i zgłaszanie alertów
Skąd wiadomo, powitania kliknij prawym przyciskiem myszy, aby zatrzymać podczas wybierania w górę i w dół? Użyj hello wbudowanych wydajności monitorowania oraz alertów funkcji, z ocen wydajności hello opartego na jednostce obliczeniowe. Korzystanie z tych funkcji, można szybko ocenić wpływ hello skalowanie w górę lub w dół na bieżącym podstawie lub projektu na potrzeby w zakresie wydajności. Zobacz [pojęcia: warstwy usług](concepts-service-tiers.md) szczegółowe informacje.

## <a name="keep-your-app-and-business-running"></a>Zapewnienie działania aplikacji i firmy
Azure w branży 99,99% dostępności Umowa dotycząca poziomu usług (SLA), obsługiwane przez usługę globalnej sieci centrów danych zarządzany przez firmę Microsoft, pomaga zapewnić działanie aplikacji 24/7. Z każdym Azure bazy danych MySQL serwera możesz korzystać z zabezpieczeń, odporność na uszkodzenia i ochrony danych, w przeciwnym razie trzeba będzie toobuy lub projektowanie, tworzenie i zarządzanie nimi. Z bazy danych Azure dla programu MySQL, można użyć w momencie przywracania toorecover tooan serwera wcześniej stanu, nawet sprzed 35 dni.

## <a name="secure-your-data"></a>Zabezpieczanie danych
Usługi Azure bazy danych ma tradycję bezpieczeństwa danych, czy baza danych Azure dla programu MySQL podtrzymuje dzięki funkcjom ograniczania dostępu, ochrony danych na rest i w ruchu i monitorowania aktywności. Odwiedź hello [Centrum zaufania Azure](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) informacji o zabezpieczeniach platformy Azure.

Hello Azure bazy danych dla usługi MySQL używa szyfrowania magazynu dla danych na rest. Dane w tym kopie zapasowe, są szyfrowane na dysku (z wyjątkiem hello plików tymczasowych utworzonych przez aparat hello podczas uruchamiania zapytań). Usługa Hello używa szyfrowania AES 256-bitowy, należący do szyfrowania magazynu Azure, a klucze hello jest kontrolowany przez system. Szyfrowanie magazynu jest zawsze włączone i nie można wyłączyć.

Domyślnie hello Azure bazy danych dla usługi MySQL jest skonfigurowany toorequire [zabezpieczeń połączenia SSL](./concepts-ssl-connection-security.md) dla danych w ruchu w sieci hello. Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.  Opcjonalnie możesz wyłączyć wymaganie protokołu SSL dla połączenia tooyour usługi bazy danych, jeśli aplikacja kliencka nie obsługuje łączności SSL.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy zostały odczytane tooAzure wprowadzenie bazy danych MySQL i odpowiedzi na pytanie hello "Nowości bazy danych platformy Azure dla programu MySQL", wszystko jest gotowe do:
- Zobacz hello cennikiem koszt porównania i kalkulatory. [Cennik](https://azure.microsoft.com/pricing/details/mysql/)
- Rozpoczynanie pracy przez utworzenie pierwszego serwera. [Tworzenie serwera usługi Azure Database for MySQL za pomocą witryny Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- Tworzenie pierwszej aplikacji w języku Python, PHP, Ruby, C\#, Java, Node.js: [bibliotek łączności używane tooAzure tooconnect bazy danych dla programu MySQL](concepts-connection-libraries.md)
