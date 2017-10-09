---
title: "Omówienie tworzenia aplikacji bazy danych aaaSQL | Dokumentacja firmy Microsoft"
description: "Informacje o łączności dostępnych bibliotek i najlepsze rozwiązania dotyczące łączenia tooSQL bazy danych aplikacji."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>Omówienie tworzenia aplikacji bazy danych SQL
W tym artykule przedstawiono hello podstawowe kwestie, które dewelopera należy zwrócić uwagę podczas pisania kodu tooconnect tooAzure bazy danych SQL.

> [!TIP]
> Samouczek przedstawiający należy jak toocreate serwera, utworzenie zapory na serwerze, Widok właściwości serwera, łączyć się przy użyciu programu SQL Server Management Studio kwerendy bazy danych master hello, tworzenie przykładowej bazy danych i pustą bazę danych, zapytań właściwości bazy danych, można połączyć za pomocą programu SQL Server Management Studio i zapytania hello przykładowej bazy danych, zobacz [Pobierz Samouczek wprowadzający](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Język i platforma
Dostępne są przykłady kodu dla różnych języków programowania i platform programistycznych. Można znaleźć przykłady kodu toohello łącza na: 

* Więcej informacji: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md) (Biblioteki połączeń dla usługi SQL Database i programu SQL Server)

## <a name="tools"></a>Narzędzia 
Możesz skorzystać z narzędzi open source, takich jak [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/). Ponadto usługa Azure SQL Database współpracuje z narzędziami firmy Microsoft, takimi jak [Visual Studio](https://www.visualstudio.com/downloads/) i [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  Umożliwia także hello portalu zarządzania Azure, programu PowerShell i interfejsów API REST pomóc zwiększyć wydajność, dodatkowe.

## <a name="resource-limitations"></a>Ograniczenia zasobów
Baza danych SQL Azure zarządza hello zasoby dostępne tooa bazy danych przy użyciu dwóch różnych mechanizmów: Zarządzanie zasobami i wymuszania ograniczeń.

* Więcej informacji: [Azure SQL Database resource limits](sql-database-resource-limits.md) (Limity zasobów usługi Azure SQL Database)

## <a name="security"></a>Bezpieczeństwo
Usługa Azure SQL Database udostępnia zasoby na potrzeby ograniczania dostępu, ochrony danych i monitorowania działań w bazie danych SQL Database.

* Więcej informacji: [Securing your SQL Database](sql-database-security-overview.md) (Zabezpieczanie bazy danych SQL Database)

## <a name="authentication"></a>Authentication
* Usługa Azure SQL Database obsługuje użytkowników i logowania korzystające zarówno z uwierzytelniania programu SQL Server, jak i z [uwierzytelniania za pomocą usługi Azure Active Directory](sql-database-aad-authentication.md).
* Należy określona baza danych, zamiast domyślne przyjmowanie toohello toospecify *wzorca* bazy danych.
* Nie można użyć hello języka Transact-SQL **myDatabaseName UŻYJ;** instrukcji w bazie danych tooanother tooswitch bazy danych SQL.
* Więcej informacji: [SQL Database security: Manage database access and login security](sql-database-manage-logins.md) (Zabezpieczenia usługi SQL Database: zarządzanie zabezpieczeniami dostępu i logowania do bazy danych)

## <a name="resiliency"></a>Odporność
Po wystąpieniu błędu przejściowego podczas łączenia tooSQL bazy danych, kod powinien ponów wywołanie hello.  Zaleca się, że Logika ponawiania Użyj logiki wycofywania, dlatego, że nie przeciąży hello bazy danych SQL z wielu klientów jednocześnie ponawianie próby.

* Przykłady kodu: Logika ponawiania próby przykłady kodu, które ilustrują temacie Przykłady dla języka hello wybranym w: [biblioteki połączeń dla bazy danych SQL i programu SQL Server](sql-database-libraries.md)
* Więcej informacji: [Komunikaty o błędach dotyczących programów klienckich usługi SQL Database](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Zarządzanie połączeniami
* W logice połączenia klienta musi zostać zastąpiona hello domyślny limit czasu toobe 30 sekund.  Domyślnie Hello 15 sekund jest zbyt krótka dla połączeń, które są zależne od hello internet.
* Jeśli używasz [puli połączeń](http://msdn.microsoft.com/library/8xx3tyca.aspx), czy tooclose hello połączenia hello błyskawicznych, program nie jest aktywnie używa go, a nie przygotowuje tooreuse go.

## <a name="network-considerations"></a>Zagadnienia dotyczące sieci
* Na komputerze hello, który hostuje program kliencki upewnij się, że Zapora hello zezwala wychodzących komunikacji TCP na porcie 1433.  Więcej informacji: [Konfigurowanie zapory usługi Azure SQL Database](sql-database-configure-firewall-settings.md)
* Jeśli program kliencki łączy tooSQL bazy danych, gdy klient działa na maszynie wirtualnej platformy Azure (VM), należy otworzyć określone zakresy portów na powitania maszyny Wirtualnej. Więcej informacji: [porty inne niż 1433 ADO.NET 4.5 i bazy danych SQL](sql-database-develop-direct-route-ports-adonet-v12.md)
* Czasami tooAzure połączeń klienckich bazy danych SQL używaj serwera proxy hello i bezpośrednią interakcję z hello bazy danych. Porty inne niż 1433 nabierają znaczenia. Aby uzyskać więcej informacji [architektury połączenia bazy danych SQL Azure](sql-database-connectivity-architecture.md) i [porty inne niż 1433 ADO.NET 4.5 i bazy danych SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Dzielenia na fragmenty danych o elastycznej skali
Elastyczne skalowanie upraszcza proces hello skalowanie limit (oraz w). 

* [Wzorce projektowe dla wielodostępnych aplikacji SaaS wykorzystujących usługę Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Routing zależny od danych](sql-database-elastic-scale-data-dependent-routing.md)
* [Wprowadzenie do funkcji Elastyczne skalowanie w wersji zapoznawczej dla usługi Azure SQL Database](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Następne kroki
Eksploruj wszystkich hello [możliwości bazy danych SQL](sql-database-technical-overview.md)
