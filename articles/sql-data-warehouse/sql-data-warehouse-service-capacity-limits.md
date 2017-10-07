---
title: "limity pojemności magazynu danych aaaSQL | Dokumentacja firmy Microsoft"
description: "Maksymalne wartości dla połączeń, baz danych, tabel i zapytań dotyczących usługi SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>Limity pojemności magazynu danych SQL
Witaj poniższe tabele zawierają hello wartości maksymalne dozwolone dla poszczególnych składników usługi Azure SQL Data Warehouse.

## <a name="workload-management"></a>Zarządzanie obciążeniami
| Kategoria | Opis | Maksymalna |
|:--- |:--- |:--- |
| [Jednostki magazynu danych (DWU)][Data Warehouse Units (DWU)] |Jednostka DWU Max jednego magazynu danych SQL |6000 |
| [Jednostki magazynu danych (DWU)][Data Warehouse Units (DWU)] |Jednostka DWU Max dla pojedynczego serwera SQL |6000 domyślnie<br/><br/> Domyślnie każdy serwer SQL (np. myserver.database.windows.net) ma przydziału jednostek dtu w warstwie 45,000, dzięki czemu zapasowej too6000 DWU. Ten limit przydziału jest po prostu limitem bezpieczeństwa. Może spowodować zwiększenie limitu przydziału przez [tworzenie biletu pomocy technicznej] [ creating a support ticket] i wybierając *przydziału* jako hello typ żądania.  toocalculate, które wymaga należy pomnożyć z jednostek dtu w warstwie hello 7.5 przez hello potrzebne DWU. Twoje bieżące użycie jednostek DTU z bloku serwera SQL hello można wyświetlić w portalu hello. Zarówno wstrzymana i cofanie wstrzymania bazy danych są wliczane do limitu przydziału jednostek dtu w warstwie hello. |
| Połączenie z bazą danych |Otwieranie sesji jednoczesnych |1024<br/><br/>Firma Microsoft obsługuje maksymalnie 1024 aktywnych połączeń, z których każdy przesyłania żądań bazy danych SQL Data Warehouse tooa na powitania tym samym czasie. Należy pamiętać, że istnieją ograniczenia dotyczące hello liczba zapytań, które faktycznie mogą być wykonywane jednocześnie. Po przekroczeniu limitu współbieżności hello żądania hello przechodzi w stan kolejki wewnętrznej gdzie oczekuje toobe przetworzone. |
| Połączenie z bazą danych |Maksymalna ilość pamięci dla przygotowanych instrukcji |20 MB |
| [Zarządzanie obciążenia][Workload management] |Maksymalna liczba jednoczesnych kwerend |32<br/><br/> Domyślnie usługi SQL Data Warehouse można wykonywać maksymalnie 32 zapytania jednoczesne i kolejek pozostałych zapytań.<br/><br/>poziom współbieżności Hello mogą się zmniejszyć, gdy użytkownicy są dodawani tooa wyższej klasy zasobów lub SQL Data Warehouse jest skonfigurowany z DWU niski. Niektóre kwerendy, takie jak zapytania DMV mogą zawsze toorun. |
| [Bazy danych tempdb][Tempdb] |Maksymalny rozmiar bazy danych Tempdb |399 GB na DW100. W związku z tym w bazie danych Tempdb DWU1000 jest TB too3.99 o określonym rozmiarze |

## <a name="database-objects"></a>Obiekty bazy danych
| Kategoria | Opis | Maksymalna |
|:--- |:--- |:--- |
| Database (Baza danych) |Maksymalny rozmiar |240 TB skompresowane na dysku<br/><br/>Ten obszar jest niezależna od miejsca w bazie danych tempdb lub dziennika, i dlatego ta przestrzeń dedykowanych toopermanent tabel.  Kompresja klastrowanego magazynu kolumn szacuje się na 5 X.  Kompresja ta umożliwia hello bazy danych toogrow tooapproximately 1 PB, gdy wszystkie tabele są klastrowanego magazynu kolumn (hello domyślny typ tabeli). |
| Tabela |Maksymalny rozmiar |60 TB skompresowane na dysku |
| Tabela |Tabel na bazę danych |2 miliardów |
| Tabela |Kolumn w tabeli |1024 kolumn |
| Tabela |Liczba bajtów na kolumny |Zależne od kolumny [— typ danych][data type].  Limit wynosi 8000 dla typów danych char, 4000 dla nvarchar lub 2 GB dla typów danych MAX. |
| Tabela |Liczba bajtów na wiersz, zdefiniowanego rozmiaru |8060 bajtów<br/><br/>Witaj liczbę bajtów na wiersz jest obliczane w hello jest taki sam jak dla programu SQL Server kompresji strony. Jak SQL Server magazynu danych SQL obsługuje magazynowanie przepełnienia wierszy, co umożliwia **kolumn o zmiennej długości** toobe przesunięcie poza wiersz. Jeśli wierszy o zmiennej długości są przenoszone poza wiersz, tylko bajtów 24 główny jest przechowywany w głównym rekordzie hello. Aby uzyskać więcej informacji, zobacz hello [przepełnienia wiersza danych przekraczających 8 KB] [ Row-Overflow Data Exceeding 8 KB] artykuł w witrynie MSDN. |
| Tabela |Partycje tabeli |15,000<br/><br/>O wysokiej wydajności, firma Microsoft zaleca, minimalizując liczbę hello partycji muszą podczas przerywania obsługi wymagań biznesowych. Jako hello liczby partycji rozwoju, narzut na powitania dla języka definicji danych (DDL) i manipulowania języka DML (Data) operacji rozwoju i powoduje, że niższej wydajności. |
| Tabela |Liczba znaków na wartość graniczna partycji. |4000 |
| Indeks |Indeksy klastrowane nie na tabelę. |999<br/><br/>Dotyczy tylko tabele toorowstore. |
| Indeks |Indeksy klastrowane na tabelę. |1<br><br/>Stosuje tooboth magazynu wierszy i magazynu kolumn tabeli. |
| Indeks |Rozmiar klucza indeksu. |900 bajtów.<br/><br/>Dotyczy tylko toorowstore indeksów.<br/><br/>Jeśli po utworzeniu indeksu hello hello istniejące dane w kolumnach hello nie przekracza 900 bajtów można utworzyć indeksy w kolumnach varchar o maksymalnym rozmiarze więcej niż 900 bajtów. Jednak później WSTAWIĆ lub zaktualizować działania hello kolumn, które powodują tooexceed całkowity rozmiar hello, zakończą się 900 bajtów. |
| Indeks |Kolumny klucza w indeksie. |16<br/><br/>Dotyczy tylko toorowstore indeksów. Klastrowane indeksy magazynu kolumn zawiera wszystkich kolumn. |
| Statystyki |Rozmiar hello łączyć wartości w kolumnie. |900 bajtów. |
| Statystyki |Kolumny dla każdego obiektu statystyk. |32 |
| Statystyki |Statystyki tworzone dla kolumn w tabeli. |30,000 |
| Procedury składowane |Maksymalnej liczby poziomów zagnieżdżenia. |8 |
| Widok |Kolumn w widoku |1,024 |

## <a name="loads"></a>Obciążenia
| Kategoria | Opis | Maksymalna |
|:--- |:--- |:--- |
| Program Polybase obciążenia |MB na wiersz |1<br/><br/>Aparat Polybase obciążenia są ograniczone tooloading wierszy zarówno mniejszy niż 1MB i nie można załadować tooVARCHR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX).<br/><br/> |

## <a name="queries"></a>Zapytania
| Kategoria | Opis | Maksymalna |
|:--- |:--- |:--- |
| Zapytanie |W kolejce kwerend w tabelach użytkownika. |1000 |
| Zapytanie |Zapytania jednoczesne na widoki systemu. |100 |
| Zapytanie |Zapytania w kolejce na widoki systemu |1000 |
| Zapytanie |Maksymalna parametrów |2098 |
| Batch |Maksymalny rozmiar |65,536*4096 |
| Wybierz wyniki |Kolumn w wierszu |4096<br/><br/>Nigdy nie może mieć więcej niż 4096 kolumn na wiersz w hello Wybierz wynik. Nie ma żadnej gwarancji, że zawsze może mieć 4096. Jeśli plan zapytania hello wymaga tabeli tymczasowej, mogą być stosowane hello 1024 kolumn dla tabeli maksymalną. |
| WYBIERZ |Podzapytania zagnieżdżonych |32<br/><br/>Program może nigdy nie więcej niż 32 zagnieżdżonych podzapytań w instrukcji SELECT. Nie ma żadnej gwarancji, że zawsze może mieć 32. Na przykład sprzężenia można wprowadzać podzapytania do hello planu zapytania. Liczba Hello podzapytania ograniczeniem również dostępnej pamięci. |
| WYBIERZ |Kolumn w SPRZĘŻENIU |1024 kolumn<br/><br/>Nigdy nie może zawierać więcej niż 1024 kolumny hello sprzężenia. Nie ma żadnej gwarancji, że zawsze może mieć 1024. Jeśli plan sprzężenia hello wymaga tabeli tymczasowej o więcej kolumn niż wynik sprzężenia hello, hello 1024 limit ma zastosowanie toohello tabeli tymczasowej. |
| WYBIERZ |Bajty na grupy według kolumn. |8060<br/><br/>Witaj kolumn w klauzuli GROUP BY hello może mieć co najwyżej 8060 bajtów. |
| WYBIERZ |Bajtów w kolejności według kolumn |8060 bajtów.<br/><br/>Witaj kolumn w klauzuli ORDER BY hello może mieć co najwyżej 8060 bajtów. |
| Identyfikatory i stałych na instrukcję |Liczba identyfikatorów przywoływany i stałe. |65,535<br/><br/>Usługa SQL Data Warehouse ogranicza liczbę hello identyfikatorów i stałe, które mogą znajdować się w jednym wyrażeniu zapytania. Ten limit wynosi 65 535. Przekraczające ten numer powoduje błąd programu SQL Server 8632. Aby uzyskać więcej informacji, zobacz [błąd wewnętrzny: Osiągnięto limit usług wyrażeń][Internal error: An expression services limit has been reached]. |

## <a name="metadata"></a>Metadane
| Widok systemu | Maksymalna liczba wierszy |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10 000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |Całkowita liczba pracowników DMS dla hello najnowszych 1000 żądań SQL. |
| sys.dm_pdw_errors |10 000 |
| sys.dm_pdw_exec_requests |10 000 |
| sys.dm_pdw_exec_sessions |10 000 |
| sys.dm_pdw_request_steps |Całkowita liczba kroki hello najnowszych 1000 żądań SQL, które są przechowywane w sys.dm_pdw_exec_requests. |
| sys.dm_pdw_os_event_logs |10 000 |
| sys.dm_pdw_sql_requests |Witaj najnowszych 1000 SQL żądania, które są przechowywane w sys.dm_pdw_exec_requests. |

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacje, zobacz [Omówienie usługi SQL Data Warehouse][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
