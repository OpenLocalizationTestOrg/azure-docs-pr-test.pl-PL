---
title: aaaTroubleshooting Azure SQL Data Warehouse | Dokumentacja firmy Microsoft
description: "Rozwiązywanie problemów z usługą Magazyn danych Azure SQL."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Rozwiązywanie problemów z usługą Magazyn danych Azure SQL
Ten temat zawiera listę hello niektóre z najczęściej pytania dotyczące rozwiązywania problemów, które Otrzymaliśmy od klientów.

## <a name="connecting"></a>Łączenie
| Problem | Rozwiązanie |
|:--- |:--- |
| Logowanie użytkownika "NT\LOGOWANIE" nie powiodło się. (Program Microsoft SQL Server, błąd: 18456) |Ten błąd występuje, gdy użytkownik usługi AAD próbuje tooconnect toohello głównej bazy danych, ale nie ma użytkownika głównego.  toocorrect tego problemu Podaj hello SQL Data Warehouse ma tooconnect tooat połączenia czas lub Dodaj hello użytkownika toohello głównej bazy danych.  Zobacz [Omówienie zabezpieczeń] [ Security overview] artykułu, aby uzyskać więcej informacji. |
| Serwer Hello podmiotu zabezpieczeń "MyUserName" nie jest możliwe tooaccess hello bazy danych "master" w bieżącym kontekście zabezpieczeń hello. Nie można otworzyć domyślnej bazy danych użytkownika. Logowanie nie powiodło się. Logowanie użytkownika "MyUserName" nie powiodło się. (Program Microsoft SQL Server, błąd: 916) |Ten błąd występuje, gdy użytkownik usługi AAD próbuje tooconnect toohello głównej bazy danych, ale nie ma użytkownika głównego.  toocorrect tego problemu Podaj hello SQL Data Warehouse ma tooconnect tooat połączenia czas lub Dodaj hello użytkownika toohello głównej bazy danych.  Zobacz [Omówienie zabezpieczeń] [ Security overview] artykułu, aby uzyskać więcej informacji. |
| Błąd CTAIP |Ten błąd może wystąpić po utworzeniu identyfikatora logowania na powitania wzorca bazy danych SQL, ale nie w bazie danych usługi SQL Data Warehouse hello.  Jeśli ten błąd wystąpi, Przyjrzyjmy się hello [Omówienie zabezpieczeń] [ Security overview] artykułu.  W tym artykule opisano sposób toocreate Utwórz nazwę logowania i użytkownika na wzorcu, a następnie jak toocreate przez użytkownika w hello bazy danych magazynu danych SQL. |
| Blokowane przez zaporę |Bazy danych SQL Azure są chronione przez tooensure zapory poziomu serwera i bazy danych, tylko znane adresy IP, które mają tooa dostępu do bazy danych. zapory Hello są zabezpieczone przez domyślną, co oznacza, że musisz jawnie włączyć oraz adres IP lub zakres adresów, zanim będzie można połączyć.  tooconfigure zapory dla programu access, wykonaj kroki hello w [konfigurowania serwera zapory dostępu do sieci IP klienta] [ Configure server firewall access for your client IP] w hello [inicjowania obsługi administracyjnej instrukcje] [Provisioning instructions]. |
| Nie można połączyć z narzędziem lub sterownika |Usługa SQL Data Warehouse zaleca użycie [SSMS][SSMS], [narzędzi SSDT dla programu Visual Studio][SSDT for Visual Studio], lub [sqlcmd] [ sqlcmd] tooquery danych. Więcej szczegółów na sterowniki i łączenia tooSQL hurtowni danych, zobacz [sterowniki dla usługi Azure SQL Data Warehouse] [ Drivers for Azure SQL Data Warehouse] i [połączyć tooAzure SQL Data Warehouse] [ Connect tooAzure SQL Data Warehouse] artykułów. |

## <a name="tools"></a>Narzędzia
| Problem | Rozwiązanie |
|:--- |:--- |
| Eksplorator obiektów programu Visual Studio nie ma użytkowników usługi AAD |Jest to znany problem.  Jako obejście, Wyświetl użytkowników hello w [sys.database_principals][sys.database_principals].  Zobacz [tooAzure uwierzytelniania SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn więcej o korzystaniu z usługi Azure Active Directory z usługą Magazyn danych SQL. |
|Podręcznik obsługi skryptów, za pomocą Kreatora skryptów hello lub łączących się za pomocą narzędzia SSMS jest powolne, zawieszone lub tworzenie błędów| Upewnij się, że użytkownicy zostały utworzone w bazie danych master hello. W obszarze Opcje obsługi skryptów upewnij się również czy wersji aparatu hello jest ustawiana jako "Microsoft Azure SQL Data magazynu Edition" i "Baza danych SQL Microsoft Azure" jest typ aparatu.|

## <a name="performance"></a>Wydajność
| Problem | Rozwiązanie |
|:--- |:--- |
| Rozwiązywanie problemów z wydajnością zapytania |Jeśli próbujesz tootroubleshoot określonego zapytania, Rozpocznij od [uczenia jak toomonitor zapytań][Learning how toomonitor your queries]. |
| Zapytanie niską wydajność i planów często wynika ma statystyk |Najczęstszą przyczyną niskiej wydajności Hello jest brak statystyk dotyczących tabel.  Zobacz [utrzymania statystyk tabeli] [ Statistics] szczegółowe informacje na temat statystyki toocreate i do czego są krytyczne tooyour wydajności. |
| Współbieżność niski / zapytań w kolejce |Opis [zarządzania obciążenia] [ Workload management] jest ważne w kolejności toounderstand jak toobalance alokacji pamięci z współbieżności. |
| Jak tooimplement najlepsze rozwiązania |Witaj najlepszą wydajność zapytań serwera miejsce toostart toolearn sposobów tooimprove jest [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse] [ SQL Data Warehouse best practices] artykułu. |
| Jak tooimprove wydajność i skalowanie |Czasami wydajność tooimproving rozwiązania hello jest toosimply dodać więcej obliczeniowe zasilania tooyour zapytań przez [skalowania SQL Data Warehouse][Scaling your SQL Data Warehouse]. |
| Wydajność zapytań niską wyniku indeksu słabą jakość |Sytuacje zapytania można spowolnienie z powodu [jakości indeksu magazynu kolumn niską][Poor columnstore index quality].  Zobacz ten artykuł, aby uzyskać więcej informacji i sposobu zbyt[Odbuduj indeksy tooimprove segmentu jakości][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Zarządzanie systemem
| Problem | Rozwiązanie |
|:--- |:--- |
| Msg 40847: Nie można wykonać operacji hello, ponieważ serwer przekroczyłby dozwolony przydział jednostki transakcji bazy danych z 45000 hello. |Obniż hello [DWU] [ DWU] hello bazy danych chcesz toocreate lub [zażądać zwiększenia limitu przydziału][request a quota increase]. |
| Badanie wykorzystania miejsca |Zobacz [tabeli rozmiary] [ Table sizes] wykorzystanie miejsca hello toounderstand systemu. |
| Pomóc w zarządzaniu tabel |Zobacz hello [omówienie tabeli] [ Overview] artykułu, aby uzyskać pomoc dotyczącą zarządzania tabel.  Ten artykuł zawiera także linki do bardziej szczegółowych tematów, takich jak [typów danych tabeli][Data types], [Dystrybucja tabeli][Distribute], [Indeksowania tabeli][Index], [partycjonowania tabeli][Partition], [utrzymania statystyk tabeli] [ Statistics] i [tabel tymczasowych][Temporary]. |
|Pasek postępu danych przezroczystego szyfrowania (funkcji TDE) nie jest aktualizowana w hello portalu Azure|Możesz wyświetlić stan hello funkcji TDE za pośrednictwem [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>Program Polybase
| Problem | Rozwiązanie |
|:--- |:--- |
| Obciążenia zakończy się niepowodzeniem z powodu dużych wierszy |Obsługa dużych wiersza nie jest obecnie dostępna dla programu Polybase.  Oznacza to, że jeśli tabela zawiera VARCHAR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX), tabel zewnętrznych nie może być tooload używanych danych.  Obciążenia dla dużych wierszy jest obecnie obsługiwane tylko za pośrednictwem usługi fabryka danych Azure (za pomocą narzędzia BCP), usługi Azure Stream Analytics, SSIS, BCP lub hello klasy .NET SQLBulkCopy. Obsługa PolyBase dla dużych wierszy zostanie dodana w przyszłej wersji. |
| obciążenia BCP tabeli z typem danych MAX kończy się niepowodzeniem |Jest to znany problem, który wymaga VARCHAR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX) można umieścić na końcu hello hello tabeli w niektórych scenariuszach.  Spróbuj przenieść Twojej maksymalna liczba kolumn toohello końca hello tabeli. |

## <a name="differences-from-sql-database"></a>Różnice z bazy danych SQL
| Problem | Rozwiązanie |
|:--- |:--- |
| Nieobsługiwane funkcje bazy danych SQL |Zobacz [nieobsługiwane funkcje tabeli][Unsupported table features]. |
| Nieobsługiwane typy danych bazy danych SQL |Zobacz [nieobsługiwane typy danych][Unsupported data types]. |
| Usuń i ograniczenia aktualizacji |Zobacz [obejścia aktualizacji][UPDATE workarounds], [obejścia DELETE] [ DELETE workarounds] i [toowork przy użyciu CTAS wokół nieobsługiwany aktualizacji i Usuń składni][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| Instrukcji MERGE nie jest obsługiwane. |Zobacz [obejścia scalania][MERGE workarounds]. |
| Procedura składowana ograniczenia |Zobacz [przechowywane procedury ograniczenia] [ Stored procedure limitations] toounderstand niektóre ograniczenia hello procedur składowanych. |
| Funkcje UDF nie obsługują instrukcji "SELECT" |Jest to aktualne ograniczenie naszych funkcji UDF.  Zobacz [CREATE FUNCTION] [ CREATE FUNCTION] składni hello obsługujemy. |

## <a name="next-steps"></a>Następne kroki
Jeśli jesteś zostały toofind problem tooyour rozwiązania powyżej, poniżej przedstawiono inne zasoby, możesz spróbować.

* [Blogi]
* [Żądania funkcji]
* [Filmy wideo]
* [Blogi zespołu CAT]
* [Tworzenie biletu pomocy technicznej]
* [Forum MSDN]
* [Forum Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Tworzenie biletu pomocy technicznej]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blogi]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogi zespołu CAT]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Żądania funkcji]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Forum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Filmy wideo]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
