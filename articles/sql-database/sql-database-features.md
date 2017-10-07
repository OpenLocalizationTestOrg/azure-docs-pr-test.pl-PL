---
title: "Omówienie funkcji bazy danych SQL aaaAzure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie hello bazy danych SQL Azure logicznej serwerów i baz danych i obejmuje macierz obsługi funkcji, wraz z łączami w każdej z wymienionych funkcji."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d1a46fa4-53d2-4d25-a0a7-92e8f9d70828
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/25/2017
ms.author: carlrab
ms.openlocfilehash: 463c88edcd38eabbc768cfb701bc74461836aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-features"></a>Funkcje usługi Azure SQL Database

Baza danych SQL Azure udostępnia typowe bazy kodu z programem SQL Server i na poziomie bazy danych hello, obsługuje większość hello te same funkcje. Hello najważniejsze różnice między bazą danych SQL Azure i SQL Server są na poziomie wystąpienia hello. 

W dalszym ciągu tooadd tooAzure funkcje bazy danych SQL. Dlatego firma Microsoft zachęca możesz toovisit naszej usługi aktualizacji strony sieci Web platformy Azure i toouse filtrów:

* Filtrowane toohello [usługi baza danych SQL](https://azure.microsoft.com/updates/?service=sql-database).
* Filtrowane tooGeneral dostępności [anonsów (GA)](http://azure.microsoft.com/updates/?service=sql-database&update-type=general-availability) funkcji bazy danych SQL.

## <a name="sql-server-and-sql-database-feature-support"></a>Obsługa funkcji programu SQL Server i bazy danych SQL

Witaj poniższej tabeli wymieniono hello głównych funkcji programu SQL Server oraz zawiera informacje o czy obsługa każdej z funkcji oraz łącza toomore informacji na temat funkcji hello. Aby tooconsider różnice języka Transact-SQL podczas migracji istniejącego rozwiązania bazy danych, zobacz [różnice języka Transact-SQL rozpoznawania podczas migracji tooSQL bazy danych](sql-database-transact-sql-information.md).


| **Funkcja serwera SQL** | **Obsługiwane w bazie danych Azure SQL** | 
| --- | --- |  
| [Zawsze zaszyfrowane](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) | Tak — zobacz [magazynu certyfikatów](sql-database-always-encrypted.md) i [magazyn kluczy](sql-database-always-encrypted-azure-key-vault.md)|
| [Zawsze włączone grupy dostępności](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) | Nie — zobacz [trybu Failover grupy i aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) |
| [Dołączanie bazy danych](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) | Nie |
| [Role aplikacji](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/application-roles) | Tak |
| [Plik pliku BACPAC (Eksportuj)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) | Tak — zobacz [eksportu bazy danych SQL](sql-database-export.md) |
| [Plik pliku BACPAC (Importuj)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database) | Tak — zobacz [importu bazy danych SQL](sql-database-import.md) |
| [Polecenie tworzenia kopii zapasowej](https://docs.microsoft.com/sql/t-sql/statements/backup-transact-sql) | Nie — zobacz [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md) |
| [Funkcje wbudowane](https://docs.microsoft.com/sql/t-sql/functions/functions) | Większość — Zobacz poszczególnych funkcji |
| [Przechwytywania zmian danych](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-data-capture-sql-server) | Nie |
| [Śledzenie zmian](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server) | Tak |
| [Instrukcje sortowania](https://docs.microsoft.com/sql/t-sql/statements/collations) | Tak |
| [Indeksy magazynu kolumn](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) | Tak — [tylko w wersji Premium](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) |
| [Środowisko uruchomieniowe języka wspólnego (CLR)](https://docs.microsoft.com/sql/relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts) | Nie |
| [Zawartych baz danych](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) | Tak |
| [Zawartych użytkowników](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) | Tak |
| [Formant słów kluczowych języka przepływu](https://docs.microsoft.com/sql/t-sql/language-elements/control-of-flow) | Tak |
| [Zapytania między bazami danych](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/cross-database-queries) | Częściowe — zobacz [Zapytania elastyczne](sql-database-elastic-query-overview.md) |
| [Kursory](https://docs.microsoft.com/sql/t-sql/language-elements/cursors-transact-sql) | Tak | 
| [Kompresja danych](https://docs.microsoft.com/sql/relational-databases/data-compression/data-compression) | Tak |
| [Poczta bazy danych](https://docs.microsoft.com/sql/relational-databases/database-mail/database-mail) | Nie |
| [Funkcja dublowania baz danych](https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server) | Nie |
| [Ustawienia konfiguracji bazy danych](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) | Tak |
| [Usług Data Quality Services (DQS)](https://docs.microsoft.com/sql/data-quality-services/data-quality-services) | Nie |
| [Migawki baz danych](https://docs.microsoft.com/sql/relational-databases/databases/database-snapshots-sql-server) | Nie |
| [Typy danych](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql) | Tak |  
| [Instrukcji DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) | Większość — zobacz instrukcje poszczególnych |
| [Instrukcji DDL](https://docs.microsoft.com/sql/t-sql/statements/statements) | Większość — zobacz instrukcje poszczególnych
| [Wyzwalaczy DDL](https://docs.microsoft.com/sql/relational-databases/triggers/ddl-triggers) | Tylko bazy danych |
| [Transakcje rozproszone - MS DTC](https://docs.microsoft.com/sql/relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions) | Nie — zobacz [elastycznej transakcji](sql-database-elastic-transactions-overview.md) |
| [Instrukcje DML](https://docs.microsoft.com/sql/t-sql/queries/queries) | Większość — zobacz instrukcje poszczególnych |
| [Wyzwalacze DML](https://docs.microsoft.com/sql/relational-databases/triggers/dml-triggers) |
| [Dynamiczne widoki zarządzania](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) | Niektóre — Zobacz poszczególnych widoków DMV |
| [Powiadomienia o zdarzeniach](https://docs.microsoft.com/sql/relational-databases/service-broker/event-notifications) | Nie — zobacz [alertów](sql-database-insights-alerts-portal.md) |
| [Wyrażenia](https://docs.microsoft.com/sql/t-sql/language-elements/expressions-transact-sql) |Tak |
| [Zdarzenia rozszerzone](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events) | Niektóre — Zobacz poszczególne zdarzenia |
| [Rozszerzone procedury składowane](https://docs.microsoft.com/sql/relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures) | Nie |
| [Pliki i grup plików](https://docs.microsoft.com/sql/relational-databases/databases/database-files-and-filegroups) | Tylko grupy plik podstawowy |
| [FILESTREAM](https://docs.microsoft.com/sql/relational-databases/blob/filestream-sql-server) | Nie |
| [Wyszukiwanie pełnotekstowe](https://docs.microsoft.com/sql/relational-databases/search/full-text-search) | Moduły dzielenia wyrazów innej firmy nie są obsługiwane. |
| [Funkcje](https://docs.microsoft.com/sql/t-sql/functions/functions) | Większość — Zobacz poszczególnych funkcji |
| [Przetwarzanie wykresu](/sql/relational-databases/graphs/sql-graph-overview) | Tak |
| [Optymalizacja w pamięci](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization) | Tak — [tylko w wersji Premium](sql-database-in-memory.md) |
| [Obsługa danych JSON](https://docs.microsoft.com/sql/relational-databases/json/json-data-sql-server) | Tak |
| [Elementy języka](https://docs.microsoft.com/sql/t-sql/language-elements/language-elements-transact-sql) | Większość — Zobacz poszczególne elementy |  
| [Połączonych serwerów](https://docs.microsoft.com/sql/relational-databases/linked-servers/linked-servers-database-engine) | Nie — zobacz [elastycznej zapytania](sql-database-elastic-query-horizontal-partitioning.md) |
| [Wysyłanie dziennika](https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server) | Nie — zobacz [trybu Failover grupy i aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) |
| [Usług Master Data Services (MDS)](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds) | Nie |
| [Minimalny logowania za pomocą importowania zbiorczego](https://docs.microsoft.com/sql/relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import) | Nie |
| [Modyfikowanie danych systemowych](https://docs.microsoft.com/sql/relational-databases/databases/system-databases) | Nie |
| [Operacje indeksu w trybie online](https://docs.microsoft.com/sql/relational-databases/indexes/perform-index-operations-online) | Jest obsługiwana — rozmiar transakcji ograniczony przez warstwy usług |
| [Operatory](https://docs.microsoft.com/sql/t-sql/language-elements/operators-transact-sql) | Większość — Zobacz poszczególnych operatorów |
| [Punktu w czasie przywracania bazy danych](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model) | Tak — zobacz [odzyskiwanie bazy danych SQL](sql-database-recovery-using-backups.md#point-in-time-restore) |
| [Program Polybase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) | Nie |
| [Zarządzanie oparte na zasadach](https://docs.microsoft.com/sql/relational-databases/policy-based-management/administer-servers-by-using-policy-based-management) | Nie |
| [Predykaty](https://docs.microsoft.com/sql/t-sql/queries/predicates) | Większość — Zobacz poszczególnych predykatów |
| [Usługi języka R](https://docs.microsoft.com/sql/advanced-analytics/r-services/sql-server-r-services) | Nie |
| [Zarządcy zasobów](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) | Nie |
| [Przywróć — instrukcje](https://docs.microsoft.com/sql/t-sql/statements/restore-statements-for-restoring-recovering-and-managing-backups-transact-sql) | Nie | 
| [Przywróć bazę danych z kopii zapasowej](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases#restore-data-backups) | Wbudowane kopie zapasowe tylko — zobacz [odzyskiwanie bazy danych SQL](sql-database-recovery-using-backups.md) |
| [Zabezpieczenia na poziomie wiersza](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) | Tak |
| [Semantycznego wyszukiwania](https://docs.microsoft.com/sql/relational-databases/search/semantic-search-sql-server) | Nie |
| [Numerów sekwencji.](https://docs.microsoft.com/sql/relational-databases/sequence-numbers/sequence-numbers) | Tak |
| [Usługa Service Broker](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-service-broker) | Nie |
| [Ustawienia konfiguracji serwera](https://docs.microsoft.com/sql/database-engine/configure-windows/server-configuration-options-sql-server) | Nie |
| [Set — instrukcje](https://docs.microsoft.com/sql/t-sql/statements/set-statements-transact-sql) | Większość — zobacz instrukcje poszczególnych 
| [Spatial](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-sql-server) | Tak |
| [Program SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) | Zobacz nr [zadania elastyczne](sql-database-elastic-jobs-getting-started.md) |
| [SQL Server Analysis Services (SSAS)](https://docs.microsoft.com/sql/analysis-services/analysis-services) | Nie — zobacz [usług Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) |
| [Inspekcja programu SQL Server](https://docs.microsoft.com/sql/relational-databases/security/auditing/sql-server-audit-database-engine) | Nie — zobacz [inspekcji bazy danych SQL](sql-database-auditing.md) |
| [SQL Server Integration Services (SSIS)](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services) | Nie — zobacz [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) |
| [SQL Server w programie PowerShell](https://docs.microsoft.com/sql/relational-databases/scripting/sql-server-powershell) | Tak |
| Narzędzie SQL Server Profiler | [Obsługiwane](https://docs.microsoft.com/sql/tools/sql-server-profiler/sql-server-profiler) | Nie — zobacz [rozszerzone zdarzenia](sql-database-xevent-db-diff-from-svr.md) |
| [Replikacja programu SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication) | [Tylko dla subskrybentów replikacji transakcyjnej i replikacji migawki](sql-database-cloud-migrate.md) |
| [SQL Server Reporting Services (SSRS)](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports) | Nie |
| [Procedury składowane](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) | Tak |
| [Funkcje przechowywana w systemie](https://docs.microsoft.com/sql/relational-databases/system-functions/system-functions-for-transact-sql) | Niektóre — Zobacz poszczególne funkcje |
| [Procedury składowane w systemie](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql) | Niektóre — Zobacz poszczególnych procedury składowane |
| [Tabele systemowe](https://docs.microsoft.com/sql/relational-databases/system-tables/system-tables-transact-sql) | Niektóre — Zobacz poszczególnych tabel |
| [Widoków wykazu systemu](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/catalog-views-transact-sql) | Niektóre — Zobacz poszczególnych widoków |
| [Partycjonowanie tabel](https://docs.microsoft.com/sql/relational-databases/partitions/partitioned-tables-and-indexes) | Tak — tylko podstawowej grupy plików |
| [Tabele tymczasowe](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql#temporary-tables) | Lokalne i o zakresie bazy danych globalnych tabele tymczasowe tylko |
| [Tabele danych czasowych](https://docs.microsoft.com/sql/relational-databases/tables/temporal-tables) | Tak |
| [Transakcje](https://docs.microsoft.com/sql/t-sql/language-elements/transactions-transact-sql) | Nie |
| [Zmienne](https://docs.microsoft.com/sql/t-sql/language-elements/variables-transact-sql) | Tak | 
| [Przezroczystego szyfrowania danych (funkcji TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) | Tak |
| [Klaster trybu Failover serwera systemu Windows](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server) | Nie — zobacz [trybu Failover grupy i aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) |
| [Indeksów XML](https://docs.microsoft.com/sql/t-sql/statements/create-xml-index-transact-sql) | Tak |

## <a name="next-steps"></a>Następne kroki

- Informacje o hello usługi baza danych SQL Azure, zobacz [co to jest baza danych SQL?](sql-database-technical-overview.md)
- Informacje o obsługę języka Transact-SQL i różnice, zobacz [różnice języka Transact-SQL rozpoznawania podczas migracji tooSQL bazy danych](sql-database-transact-sql-information.md).
