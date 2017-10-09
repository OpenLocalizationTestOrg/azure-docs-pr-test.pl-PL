---
title: "aaaAll tematów dotyczących usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Spis wszystkich tematów dotyczących hello Azure usługa o nazwie SQL Data Warehouse, która istnieje na http://azure.microsoft.com/documentation/articles/, tytuł i opis."
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Wszystkie tematy dotyczące usługi Azure SQL Data Warehouse
W tym temacie wymieniono co temat, który bezpośrednio dotyczy toohello **SQL Data Warehouse** usługi platformy Azure. Ta strona sieci Web dla słów kluczowych można wyszukiwać za pomocą **Ctrl + F**, tematów hello bieżącego toofind.

## <a name="new"></a>Nowy
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 1 |[Tworzenie kopii zapasowych SQL Data Warehouse](sql-data-warehouse-backups.md) |Więcej informacji na temat kopii zapasowych wbudowaną bazą danych SQL Data Warehouse, umożliwiających toorestore punkt przywracania tooa magazyn danych SQL Azure lub inny region geograficzny. |

## <a name="updated-articles-sql-data-warehouse"></a>Zaktualizowano artykuły, Magazyn danych SQL
Ta sekcja zawiera artykuły, które zostały ostatnio aktualizowany, gdy aktualizacja hello był duży lub znaczących. Dla każdego artykułu zaktualizowane nierównej fragment hello dodać markdown tekst jest wyświetlany. artykuły Hello zostały zaktualizowane w zakresie hello danych **2016-08-22** za**2016-10-05**.

| &nbsp; | Artykuł | Zaktualizowany tekst, fragment kodu | Zaktualizowane |
| ---:|:--- |:--- |:--- |
| 2 |[Ładowanie danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Bajty/tootrack i plików, wybierz r.command, s.request_id, r.status, count (różne input_name) jako nbr_files, Suma (s.bytes_processed) / 1024/1024 jako gb_processed z sys.dm_pdw_exec_requests r sprzężenia wewnętrznego sys.dm_pdw_dms_external_work s na r.request_id = s.request_id WHERE r. Etykieta = "CTAS: cso obciążenia. DimProduct "lub r. Etykieta = "CTAS: cso obciążenia. FactOnlineSales GROUP BY r.command, s.request_id, r.status ORDER BY nbr_files desc, gb_processed desc; |2016-09-07 |
| 3 |[Przywrócenie magazynu danych SQL](sql-data-warehouse-restore-database-overview.md) |** Można przywrócić hurtowni danych wstrzymania? ** toorestore hurtowni danych, która jest wstrzymana, należy toofirst przełączenie klastra w tryb online. Po powrocie do trybu online hurtowni danych hello masz siedem dni toochoose punktów przywracania z. ** Przywrócić tooa geograficznie nadmiarowego region ** Jeśli korzystasz z magazynu geograficznie nadmiarowego hello, można przywrócić hello centrum danych sparowanego tooyour magazynu danych w innym regionie geograficznym. Magazyn danych Hello został przywrócony z hello ostatniego tworzenia codziennej kopii zapasowej. ** Przywrócić osi czasu ** tooany punkt przywracania bazy danych w ramach hello można przywrócić w ostatnich siedmiu dni. Migawki Uruchom co cztery godziny tooeight i są dostępne na siedem dni. Gdy migawka jest starsza niż siedmiu dni, wygaśnie i jego punktu przywracania nie jest już dostępny. ** Przywrócić kosztów ** hello magazynu opłat dla magazynu danych hello przywrócić jest on rozliczany szybkością hello Azure Premium Storage. Jeśli magazynu przywróconych danych zostanie wstrzymana, są naliczane opłaty za magazyn szybkością hello Azure Premium Storage. Zaletą Hello wstrzymanie jest się, że nie jesteś opłat |2016-09-29 |

## <a name="get-started"></a>Rozpoczęcie pracy
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 4 |[TooAzure uwierzytelniania SQL Data Warehouse](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) i SQL Server authentication tooAzure SQL Data Warehouse. |
| 5 |[Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse](sql-data-warehouse-best-practices.md) |Zalecenia i najlepsze praktyki, których stosowanie zaleca się podczas tworzenia rozwiązań dla usługi Azure SQL Data Warehouse. Dzięki nim łatwiej jest odnieść sukces. |
| 6 |[Sterowniki dla magazynu danych Azure SQL](sql-data-warehouse-connection-strings.md) |Parametry połączenia i sterowniki dla magazynu danych SQL |
| 7 |[Połącz tooAzure SQL Data Warehouse](sql-data-warehouse-connect-overview.md) |Jak ciąg połączenia i nazwę serwera na powitania toofind dla Twojego tooAzure SQL Data Warehouse |
| 8 |[Analizowanie danych przy użyciu usługi Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Użyj usługi Azure Machine Learning toobuild predykcyjnej maszyny uczenie modelu, w oparciu o dane przechowywane w magazynie danych SQL Azure. |
| 9 |[Zapytanie usługi Azure SQL Data Warehouse (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Kwerenda usługi Azure SQL Data Warehouse przy użyciu narzędzia sqlcmd hello jest narzędzie wiersza polecenia. |
| 10 |[Utwórz bazę danych SQL Data Warehouse przy użyciu języka Transact-SQL (TSQL)](sql-data-warehouse-get-started-create-database-tsql.md) |Dowiedz się, jak toocreate Azure SQL Data Warehouse przy użyciu języka TSQL |
| 11 |[Jak toocreate obsługi biletu usługi SQL Data Warehouse](sql-data-warehouse-get-started-create-support-ticket.md) |Jak toocreate obsługi biletu w usłudze Azure SQL Data Warehouse. |
| 12 |[Ładowanie danych przy użyciu fabryki danych Azure](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Dowiedz się tooload dane z fabryką danych Azure |
| 13 |[Ładowanie danych przy użyciu programu PolyBase w usłudze SQL Data Warehouse](sql-data-warehouse-get-started-load-with-polybase.md) |Dowiedz się, co to jest aparat PolyBase i jak toouse go w scenariuszach dotyczących magazynów danych. |
| 14 |[Utwórz magazyn danych Azure SQL](sql-data-warehouse-get-started-provision.md) |Dowiedz się, jak hello przez toocreate usługi Azure SQL Data Warehouse w portalu Azure |
| 15 |[Tworzenie usługi SQL Data Warehouse przy użyciu programu PowerShell](sql-data-warehouse-get-started-provision-powershell.md) |Tworzenie bazy danych w usłudze SQL Data Warehouse za pomocą programu PowerShell |
| 16 |[Wizualizacja danych przy użyciu usługi Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Wizualizacja danych usługi SQL Data Warehouse przy użyciu usługi Power BI |
| 17 |[Tworzenie zapytań względem usługi Azure SQL Data Warehouse (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Tworzenie zapytań względem usługi SQL Data Warehouse przy użyciu programu Visual Studio. |

## <a name="develop"></a>Programowanie
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 18 |[Optymalizacja transakcji dla magazynu danych SQL](sql-data-warehouse-develop-best-practices-transactions.md) |Najlepszych rozwiązań o pisaniu aktualizacje wydajne transakcji w magazynie danych SQL Azure |
| 19 |[Zarządzanie współbieżności i obciążenia w usłudze SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md) |Zrozumienie zarządzania współbieżności i obciążenia w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 20 |[Utwórz tabelę jako Select (CTAS) w magazynie danych SQL](sql-data-warehouse-develop-ctas.md) |Porady dotyczące programowania z hello Utwórz tabelę jako select — instrukcja (CTAS) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 21 |[Dynamiczne SQL w usłudze SQL Data Warehouse](sql-data-warehouse-develop-dynamic-sql.md) |Porady dotyczące używania dynamicznych SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 22 |[Grupuj według opcje w usłudze SQL Data Warehouse](sql-data-warehouse-develop-group-by-options.md) |Wskazówki dotyczące implementowania grupy Opcje w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 23 |[Użyj etykiety tooinstrument zapytania w usłudze SQL Data Warehouse](sql-data-warehouse-develop-label.md) |Porady dotyczące korzystania z etykiet tooinstrument zapytania w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 24 |[W przypadku usługi SQL Data Warehouse pętle](sql-data-warehouse-develop-loops.md) |Porady dotyczące języka Transact-SQL pętli i zastąpienie kursory w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 25 |[Procedury składowane w usłudze SQL Data Warehouse](sql-data-warehouse-develop-stored-procedures.md) |Wskazówki dotyczące implementowania procedur przechowywanych w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 26 |[Transakcje w usłudze SQL Data Warehouse](sql-data-warehouse-develop-transactions.md) |Wskazówki dotyczące implementowania transakcji w magazynie danych SQL Azure związane z opracowywaniem rozwiązań. |
| 27 |[Schematy zdefiniowane przez użytkownika w usłudze SQL Data Warehouse](sql-data-warehouse-develop-user-defined-schemas.md) |Porady dotyczące używania schematów języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 28 |[Przypisz zmiennych w usłudze SQL Data Warehouse](sql-data-warehouse-develop-variable-assignment.md) |Porady dotyczące przypisywania zmienne języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 29 |[Widoki w usłudze SQL Data Warehouse](sql-data-warehouse-develop-views.md) |Porady dotyczące korzystania z widoków języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 30 |[Decyzje dotyczące projektu i technik programowania dla usługi SQL Data Warehouse](sql-data-warehouse-overview-develop.md) |Pojęcia dotyczące programowania, decyzji projektowych i zalecenia dotyczące technik programowania dla usługi SQL Data Warehouse. |

## <a name="manage"></a>Zarządzanie
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 31 |[Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (omówienie)](sql-data-warehouse-manage-compute-overview.md) |Wydajność skalowania możliwości w usłudze Azure SQL Data Warehouse. Skalowanie w poziomie przez dostosowanie wartości dwu lub wstrzymywać i wznawiać koszty toosave zasobów obliczeniowych. |
| 32 |[Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (Azure portal)](sql-data-warehouse-manage-compute-portal.md) |Mocy obliczeniowej toomanage zadania portalu Azure. Zasoby obliczeniowe skali przez dostosowanie wartości dwu. Lub wstrzymywanie i wznawianie koszty toosave zasoby obliczeniowe. |
| 33 |[Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |Mocy obliczeniowej toomanage zadania programu PowerShell. Zasoby obliczeniowe skali przez dostosowanie wartości dwu. Lub wstrzymywanie i wznawianie koszty toosave zasoby obliczeniowe. |
| 34 |[Zarządzanie energią obliczeniowych w magazynie danych SQL Azure (REST)](sql-data-warehouse-manage-compute-rest-api.md) |Mocy obliczeniowej toomanage zadania programu PowerShell. Zasoby obliczeniowe skali przez dostosowanie wartości dwu. Lub wstrzymywanie i wznawianie koszty toosave zasoby obliczeniowe. |
| 35 |[Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Transact-SQL (T-SQL) zadań poza tooscale wydajności przez dostosowanie wartości dwu. Zmniejszyć koszty przez skalowanie w trakcie godziny poza szczytem. |
| 36 |[Monitorowanie obciążenia przy użyciu widoków DMV](sql-data-warehouse-manage-monitor.md) |Dowiedz się, jak toomonitor obciążenia przy użyciu widoków DMV. |
| 37 |[Zarządzanie bazami danych w magazynie danych SQL Azure](sql-data-warehouse-overview-manage.md) |Omówienie zarządzania bazami danych magazynu danych SQL. Obejmuje narzędzia do zarządzania, jednostek dwu i wydajność skalowania w poziomie, rozwiązywanie problemów z wydajność zapytań, ustanawiania zasad zabezpieczeń dobrej i przywracanie bazy danych z uszkodzenie danych lub regionalnej awarii. |
| 38 |[Monitor kwerend użytkowników w usłudze Azure SQL Data Warehouse](sql-data-warehouse-overview-manage-user-queries.md) |Omówienie zagadnień hello, najlepszych rozwiązań i zadania monitorowania kwerend użytkowników w usłudze Azure SQL Data Warehouse |
| 39 |[Przywrócenie magazynu danych SQL](sql-data-warehouse-restore-database-overview.md) |Przegląd hello opcje przywracania bazy danych do przywrócenia bazy danych w magazynie danych SQL Azure. |
| 40 |[Przywróć magazyn danych Azure SQL (Portal)](sql-data-warehouse-restore-database-portal.md) |Azure portalu zadania przywracania usługi Azure SQL Data Warehouse. |
| 41 |[Przywróć magazyn danych Azure SQL (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Zadania programu PowerShell dla usługi Azure SQL Data Warehouse przywracania. |
| 42 |[Przywróć magazyn danych Azure SQL (interfejsu API REST)](sql-data-warehouse-restore-database-rest-api.md) |Interfejs API REST zadania przywracania usługi Azure SQL Data Warehouse. |

## <a name="tables-and-indexes"></a>Tabele i indeksy
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 43 |[Typy danych w przypadku tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-data-types.md) |Wprowadzenie do typów danych w przypadku tabel Azure SQL Data Warehouse. |
| 44 |[Dystrybucja tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-distribute.md) |Wprowadzenie do korzystania z dystrybucji tabel w usłudze Azure SQL Data Warehouse. |
| 45 |[Indeksowanie tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-index.md) |Wprowadzenie do korzystania z tabeli indeksowanie w usłudze Azure SQL Data Warehouse. |
| 46 |[Przegląd tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-overview.md) |Wprowadzenie do tabel magazynu danych SQL Azure. |
| 47 |[Partycjonowanie tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-partition.md) |Wprowadzenie do partycjonowania tabeli w magazynie danych SQL Azure. |
| 48 |[Zarządzanie statystyk dotyczących tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-statistics.md) |Wprowadzenie do korzystania z statystyk dotyczących tabel w usłudze Azure SQL Data Warehouse. |
| 49 |[Tabele tymczasowe w usłudze SQL Data Warehouse](sql-data-warehouse-tables-temporary.md) |Wprowadzenie do tabel tymczasowych w usłudze Azure SQL Data Warehouse. |

## <a name="integrate"></a>Integracja
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 50 |[Użyj fabryki danych Azure z usługą Magazyn danych SQL](sql-data-warehouse-integrate-azure-data-factory.md) |Porady dotyczące przy użyciu fabryki danych Azure (ADF) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 51 |[Użyj usługi Azure Machine Learning z usługą Magazyn danych SQL](sql-data-warehouse-integrate-azure-machine-learning.md) |Samouczek korzystania z usługi Azure Machine Learning z usługą Azure SQL Data Warehouse w celu opracowywania rozwiązań. |
| 52 |[Użyj usługi Azure Stream Analytics z usługą Magazyn danych SQL](sql-data-warehouse-integrate-azure-stream-analytics.md) |Porady dotyczące korzystania z usługi Azure Stream Analytics z usługą Magazyn danych SQL Azure związane z opracowywaniem rozwiązań. |
| 53 |[Użyj usługi Power BI z usługą Magazyn danych SQL](sql-data-warehouse-integrate-power-bi.md) |Porady dotyczące korzystania z usługi Power BI z usługą Magazyn danych SQL Azure związane z opracowywaniem rozwiązań. |
| 54 |[Korzystać z innych usług z usługą Magazyn danych SQL](sql-data-warehouse-overview-integrate.md) |Narzędzia i partnerom rozwiązania, które integrują się z usługą Magazyn danych SQL. |

## <a name="load"></a>Ładowanie
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 55 |[Ładowanie danych z magazynu obiektów blob platformy Azure do usługi Azure SQL Data Warehouse (fabryka danych Azure)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Dowiedz się tooload dane z fabryką danych Azure |
| 56 |[Ładowanie danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Dowiedz się, jak toouse PolyBase tooload dane platformy Azure z magazynu obiektów blob do magazynu danych SQL. Ładowanie kilku tabel z danych publicznej do schematu magazynu danych sprzedaży detalicznej Contoso hello. |
| 57 |[Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Używa bcp tooexport danych z plików tooflat programu SQL Server, magazynu obiektów blob tooAzure danych tooimport AZCopy i PolyBase tooingest hello danych do usługi Azure SQL Data Warehouse. |
| 58 |[Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (pliki proste)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Rozmiar danych w małych używa bcp tooexport danych z plików tooflat programu SQL Server i zaimportuj dane hello bezpośrednio do usługi Azure SQL Data Warehouse. |
| 59 |[Ładowanie danych z programu SQL Server do magazynu danych SQL Azure (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Pokazuje, jak toocreate danych toomove pakietu SQL Server Integration Services (SSIS) z różnych typów danych źródła tooSQL hurtowni danych. |
| 60 |[Ładowanie danych przy użyciu programu PolyBase w usłudze SQL Data Warehouse](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Używa bcp tooexport danych z plików tooflat programu SQL Server, magazynu obiektów blob tooAzure danych tooimport AZCopy i PolyBase tooingest hello danych do usługi Azure SQL Data Warehouse. |
| 61 |[Przewodnik dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse](sql-data-warehouse-load-polybase-guide.md) |Wskazówki i zalecenia dotyczące przy użyciu programu PolyBase w scenariuszach SQL Data Warehouse. |
| 62 |[Ładowanie przykładowych danych do usługi SQL Data Warehouse](sql-data-warehouse-load-sample-databases.md) |Ładowanie przykładowych danych do usługi SQL Data Warehouse |
| 63 |[Ładowanie danych za pomocą narzędzia BCP](sql-data-warehouse-load-with-bcp.md) |Dowiedz się, czym jest program bcp i jak toouse go w scenariuszach dotyczących magazynów danych. |
| 64 |[Ładowanie danych do usługi Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) |Dowiedz się hello typowe scenariusze dotyczące danych ładowania do usługi SQL Data Warehouse. Obejmują one przy użyciu programu PolyBase, magazynu obiektów blob platformy Azure, plików prostych i wysyłania dysku. Można także użyć narzędzi innych firm. |

## <a name="migrate"></a>Migrate (Migracja)
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 65 |[Migracja z tooSQL kodu SQL magazynu danych](sql-data-warehouse-migrate-code.md) |Wskazówki dotyczące migrowania związane z opracowywaniem rozwiązań programu SQL tooAzure kodu SQL Data Warehouse. |
| 66 |[Migrowanie danych](sql-data-warehouse-migrate-data.md) |Wskazówki dotyczące migrowania tooAzure Twojego danych usługi SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 67 |[Narzędzie migracji magazynu danych (wersja zapoznawcza)](sql-data-warehouse-migrate-migration-utility.md) |Przeprowadź migrację tooSQL hurtowni danych. |
| 68 |[Migrowanie tooSQL Twojego schematu magazynu danych](sql-data-warehouse-migrate-schema.md) |Wskazówki dotyczące migrowania tooAzure Twojego schematu SQL Data Warehouse związane z opracowywaniem rozwiązań. |
| 69 |[Migrowanie tooSQL Twojego rozwiązania magazynu danych](sql-data-warehouse-overview-migrate.md) |Wskazówki dotyczące migracji za platformy SQL Data Warehouse tooAzure rozwiązania. |

## <a name="partners"></a>Partnerzy
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 70 |[Partnerów analizy biznesowej usługi SQL Data Warehouse](sql-data-warehouse-partner-business-intelligence.md) |Lista partnerów analizy biznesowej innych firm z rozwiązaniami, które obsługują usługi SQL Data Warehouse. |
| 71 |[Partnerzy Integracja danych magazynu danych SQL](sql-data-warehouse-partner-data-integration.md) |Listę innych firm partnerom rozwiązań integracji danych, które obsługują usługi Azure SQL Data Warehouse. |
| 72 |[Partnerzy zarządzania danych magazynu danych SQL](sql-data-warehouse-partner-data-management.md) |Lista partnerów zarządzania innych producentów danych z rozwiązaniami, które obsługują usługi SQL Data Warehouse. |

## <a name="reference"></a>Dokumentacja
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 73 |[Tematy odwołań dla usługi SQL Data Warehouse](sql-data-warehouse-overview-reference.md) |Odwołanie łączy zawartości dla usługi SQL Data Warehouse. |
| 74 |[Polecenia cmdlet programu PowerShell i interfejsów API REST dla usługi SQL Data Warehouse](sql-data-warehouse-reference-powershell-cmdlets.md) |Znajdź hello top poleceń cmdlet programu PowerShell dla usługi Azure SQL Data Warehouse w tym jak toopause i wznowić bazy danych. |
| 75 |[Elementy języka](sql-data-warehouse-reference-tsql-language-elements.md) |Lista łączy tooreference zawartości dla elementów języka Transact-SQL hello używane dla usługi SQL Data Warehouse. |
| 76 |[Tematy dotyczące języka Transact-SQL](sql-data-warehouse-reference-tsql-statements.md) |Zawartość tooreference łącza hello tematy języka Transact-SQL używane przez usługi SQL Data Warehouse. |
| 77 |[Widoki systemowe](sql-data-warehouse-reference-tsql-system-views.md) |Zawartość widoków toosystem łącza dla usługi SQL Data Warehouse. |

## <a name="security"></a>Bezpieczeństwo
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 78 |[Obsługa klientów niższych poziomów usługi SQL Data Warehouse — inspekcji i dynamicznego maskowania danych](sql-data-warehouse-auditing-downlevel-clients.md) |Więcej informacji na temat obsługi klientów niższych poziomów usługi SQL Data Warehouse danych inspekcji |
| 79 |[Inspekcja w magazynie danych Azure SQL](sql-data-warehouse-auditing-overview.md) |Wprowadzenie do inspekcji w usłudze Azure SQL Data Warehouse |
| 80 |[Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE) w magazynie danych SQL](sql-data-warehouse-encryption-tde.md) |Przezroczystego szyfrowania danych (funkcji TDE) w magazynie danych SQL |
| 81 |[Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE)](sql-data-warehouse-encryption-tde-tsql.md) |Przezroczystego szyfrowania danych (funkcji TDE) w magazynie danych SQL (T-SQL) |
| 82 |[Zabezpieczanie bazy danych w usłudze SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md) |Porady dotyczące zabezpieczenia bazy danych w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań. |

## <a name="miscellaneous"></a>Różne postanowienia
| &nbsp; | Tytuł | Opis |
| ---:|:--- |:--- |
| 83 |[Instalacja programu Visual Studio i narzędzi SSDT dla usługi SQL Data Warehouse](sql-data-warehouse-install-visual-studio.md) |Instalacja programu Visual Studio i narzędzi SQL Server Data Tools (SSDT) dla usługi Azure SQL Data Warehouse |
| 84 |[Migracja tooPremium szczegóły magazynu](sql-data-warehouse-migrate-to-premium-storage.md) |Instrukcje dotyczące migracji istniejącego magazynu toopremium SQL Data Warehouse |
| 85 |[Rozpoczynanie pracy z wykrywanie zagrożeń](sql-data-warehouse-security-threat-detection.md) |Jak tooget pracę z wykrywanie zagrożeń |
| 86 |[Limity pojemności magazynu danych SQL](sql-data-warehouse-service-capacity-limits.md) |Maksymalne wartości dla połączeń, baz danych, tabel i zapytań dotyczących usługi SQL Data Warehouse. |
| 87 |[Rozwiązywanie problemów z usługą Magazyn danych Azure SQL](sql-data-warehouse-troubleshoot.md) |Rozwiązywanie problemów z usługą Magazyn danych Azure SQL. |

