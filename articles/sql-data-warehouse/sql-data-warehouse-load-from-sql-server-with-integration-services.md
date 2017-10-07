---
title: aaaLoad danych z programu SQL Server do magazynu danych SQL Azure (SSIS) | Dokumentacja firmy Microsoft
description: "Pokazuje, jak toocreate danych toomove pakietu SQL Server Integration Services (SSIS) z różnych typów danych źródła tooSQL hurtowni danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Ładowanie danych z programu SQL Server do magazynu danych SQL Azure (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Utwórz danych programu SQL Server Integration Services (SSIS) tooload pakietu z programu SQL Server do usługi Azure SQL Data Warehouse. Można opcjonalnie restrukturyzacji, przekształcanie i czyszczenia danych hello, kiedy przechodzi on przez przepływ danych usług SSIS hello.

W tym samouczku zostaną wykonane następujące czynności:

* Utwórz nowy projekt usług integracji w programie Visual Studio.
* Połącz toodata źródeł, takich jak SQL Server (jako źródło) i usługi SQL Data Warehouse (jako miejsce docelowe).
* Projekt pakietu SSIS, który ładuje dane ze źródła hello do docelowego hello.
* Uruchom hello SSIS pakietu tooload hello danych.

Ten samouczek używa programu SQL Server jako hello źródła danych. SQL Server może działać lokalnie lub w maszynie wirtualnej platformy Azure.

## <a name="basic-concepts"></a>Podstawowe pojęcia
Pakiet HELLO jest hello jednostka pracy w SSIS. Pakiety powiązane są pogrupowane w projektach. W programie Visual Studio z programu SQL Server Data Tools jest tworzenie projektów i pakietów projektów. Projekt Hello się, że proces jest procesem visual, w którym przeciągania i upuszczania składniki z przybornika hello toohello powierzchnię, podłącz je i ustawiania ich właściwości. Po zakończeniu pakietu, można opcjonalnie ją wdrożyć tooSQL serwera kompleksowego zarządzania, monitorowania i zabezpieczeń.

## <a name="options-for-loading-data-with-ssis"></a>Opcje dotyczące ładowania danych z usług SSIS
SQL Server Integration Services (SSIS) to elastyczne zestaw narzędzi, która zapewnia różne opcje połączenie i ładowania danych do usługi SQL Data Warehouse.

1. Użyj tooSQL tooconnect ADO NET docelowym magazynu danych. W tym samouczku używa docelowego NET ADO ponieważ ma ona hello najmniejszej opcji konfiguracji.
2. Użyj tooSQL tooconnect OLE DB miejsce docelowe magazynu danych. Ta opcja może udostępnić nieco większą wydajność niż hello ADO sieci docelowej.
3. Użyj hello zadań przekazania obiektu Blob Azure toostage hello danych w magazynie obiektów Blob Azure. Następnie użyj toolaunch zadania SSIS wykonaj instrukcję SQL hello skrypt programu Polybase, który ładuje hello danych do usługi SQL Data Warehouse. Ta opcja zapewnia najlepszą wydajność hello hello trzy opcje wymienione w tym miejscu. tooget hello przekazania obiektu Blob Azure zadania Pobierz hello [Microsoft SQL Server 2016 integracji usług Feature Pack dla systemu Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. Zobacz toolearn więcej informacji na temat programu Polybase [Przewodnik po programie PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Przed rozpoczęciem
toostep opisanych w tym samouczku, potrzebne są:

1. **SQL Server Integration Services (SSIS)**. SSIS jest składnikiem programu SQL Server i wymaga wersji próbnej lub licencjonowanej wersji programu SQL Server. tooget wersji ewaluacyjnej programu SQL Server 2016 Preview, zobacz [programu SQL Server ocen][SQL Server Evaluations].
2. Program **Visual Studio**. tooget hello bezpłatna wersja Community programu Visual Studio, zobacz [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools dla programu Visual Studio (SSDT)**. tooget programu SQL Server Data Tools dla programu Visual Studio, zobacz [Pobierz programu SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Przykładowe dane**. Ten samouczek używa przykładowe dane przechowywane w programie SQL Server w przykładowej bazy danych AdventureWorks hello jako hello źródła danych toobe ładowane do usługi SQL Data Warehouse. Witaj tooget przykładową bazę danych AdventureWorks, zobacz [AdventureWorks 2014 przykładowe bazy danych][AdventureWorks 2014 Sample Databases].
5. **Baza danych SQL Data Warehouse i uprawnienia**. W tym samouczku łączy tooa wystąpienie usługi SQL Data Warehouse i ładuje dane do niego. Masz toocreate uprawnienia toohave tabeli i tooload danych.
6. **Reguły zapory**. Masz toocreate reguły zapory na magazyn danych SQL z hello adres IP komputera lokalnego przed możesz przekazać dane toohello SQL Data Warehouse.

## <a name="step-1-create-a-new-integration-services-project"></a>Krok 1: Utwórz nowy projekt usług Integration Services
1. Uruchom program Visual Studio.
2. Na powitania **pliku** menu, wybierz opcję **nowy | Projekt**.
3. Przejdź toohello **zainstalowana | Szablony | Analiza biznesowa | Usługi integracji** typy projektów.
4. Wybierz **projektu usług integracji**. Podaj wartości dla **nazwa** i **lokalizacji**, a następnie wybierz **OK**.

Visual Studio otwierania i tworzenia nowego projektu Integration Services (SSIS). Następnie Visual Studio otworzy hello Projektant hello jednego nowego pakietu SSIS (Package.dtsx) w projekcie hello. Zostaną wyświetlone następujące obszary ekranu hello:

* Po lewej stronie powitania, hello **przybornika** składników usług SSIS.
* W środku hello hello powierzchni projektu z wieloma kartami. Używane zwykle co najmniej hello **przepływ sterowania** i hello **przepływu danych** karty.
* Na powitania prawo, hello **Eksploratora rozwiązań** i hello **właściwości** okienka.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Krok 2: Tworzenie przepływu danych podstawowych hello
1. Przeciągnij z przybornika hello toohello środek powierzchni projektowej hello zadania przepływu danych (na powitania **przepływ sterowania** kartę).
   
    ![][02]
2. Kliknij dwukrotnie kartę hello zadania przepływu danych tooswitch toohello przepływu danych.
3. Z listy źródeł inne hello w hello przybornika przeciągnij powierzchnię toohello źródła ADO.NET. Z nadal wybrana karta źródła hello, zmień jego nazwę za**źródła SQL Server** w hello **właściwości** okienka.
4. Z listy innych miejsc docelowych hello w przyborniku hello przeciągnij powierzchnię toohello docelowego ADO.NET w obszarze hello ADO.NET źródła. Z hello nadal wybrana karta docelowego, zmień jego nazwę za**docelowego SQL DW** w hello **właściwości** okienka.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Krok 3: Konfigurowanie hello źródła karty
1. Kliknij dwukrotnie hello źródła karty tooopen hello **Edytor źródła ADO.NET**.
   
    ![][03]
2. Na powitania **Menedżera połączeń** kartę hello **Edytor źródła ADO.NET**, kliknij przycisk hello **nowy** przycisku Dalej toohello **Menedżera połączeń ADO.NET**hello tooopen listy **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe i utworzyć ustawienia połączenia dla bazy danych programu SQL Server hello z którego ten samouczek ładuje dane.
   
    ![][04]
3. W hello **Konfigurowanie Menedżera połączeń ADO.NET** okna dialogowego kliknij hello **nowy** hello tooopen przycisk **Menedżera połączeń** okno dialogowe i utworzyć nowe połączenie danych.
   
    ![][05]
4. W hello **Menedżera połączeń** okna dialogowego pozycję hello następujące czynności.
   
   1. Aby uzyskać **dostawcy**, wybierz hello dostawcy danych SqlClient.
   2. Aby uzyskać **nazwy serwera**, wprowadź nazwę serwera SQL hello.
   3. W hello **Zaloguj się na serwerze toohello** wybierz lub wprowadź informacje dotyczące uwierzytelniania.
   4. W hello **bazy danych tooa Connect** Wybierz przykładową bazę danych AdventureWorks hello.
   5. Kliknij przycisk **połączenie testowe**.
      
       ![][06]
   6. Okno dialogowe hello hello wyniki testu połączenia hello raporty, kliknij przycisk **OK** tooreturn toohello **Menedżera połączeń** okno dialogowe.
   7. W hello **Menedżera połączeń** okno dialogowe, kliknij przycisk **OK** tooreturn toohello **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe.
5. W hello **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe, kliknij przycisk **OK** tooreturn toohello **Edytor źródła ADO.NET**.
6. W hello **Edytor źródła ADO.NET**, w hello **nazwa hello tabeli lub widoku hello** listy, wybierz opcję hello **Sales.SalesOrderDetail** tabeli.
   
    ![][07]
7. Kliknij przycisk **Podgląd** toosee hello pierwszych 200 wierszy danych w tabeli źródłowej hello w hello **Podgląd wyników zapytania** okno dialogowe.
   
    ![][08]
8. W hello **Podgląd wyników zapytania** okno dialogowe, kliknij przycisk **Zamknij** tooreturn toohello **Edytor źródła ADO.NET**.
9. W hello **Edytor źródła ADO.NET**, kliknij przycisk **OK** toofinish konfigurowania hello źródła danych.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Krok 4: Łączenie hello źródła karty toohello docelowy adapter
1. Wybierz kartę źródła hello na powierzchni projektowej hello.
2. Wybierz strzałkę hello niebieski, która rozciąga się od karty źródła hello i przeciągnij go toohello docelowego edytora, dopóki nie zostanie zablokowany na miejscu.
   
    ![][10]
   
    W typowych pakietów SSIS używa wielu innych składników z hello przybornika SSIS Between hello źródłowego i hello docelowego toorestructure, przekształcania i czyszczenia danych, ponieważ przechodzi ona przez przepływ danych usług SSIS hello. tookeep w tym przykładzie, wystarczy możemy tworzone jest połączenie hello źródła bezpośrednio toohello docelowego.

## <a name="step-5-configure-hello-destination-adapter"></a>Krok 5: Konfigurowanie hello adapter miejsca docelowego
1. Kliknij dwukrotnie hello docelowy adapter tooopen hello **ADO.NET docelowego edytora**.
   
    ![][11]
2. Na powitania **Menedżera połączeń** kartę hello **ADO.NET docelowego edytora**, kliknij przycisk hello **nowy** przycisku Dalej toohello **Menedżera połączeń**hello tooopen listy **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe i utworzyć ustawienia połączenia dla bazy danych Azure SQL Data Warehouse hello w którym w tym samouczku ładuje dane.
3. W hello **Konfigurowanie Menedżera połączeń ADO.NET** okna dialogowego kliknij hello **nowy** hello tooopen przycisk **Menedżera połączeń** okno dialogowe i utworzyć nowe połączenie danych.
4. W hello **Menedżera połączeń** okna dialogowego pozycję hello następujące czynności.
   1. Aby uzyskać **dostawcy**, wybierz hello dostawcy danych SqlClient.
   2. Aby uzyskać **nazwy serwera**, wprowadź nazwę usługi SQL Data Warehouse hello.
   3. W hello **Zaloguj się na serwerze toohello** zaznacz **uwierzytelniania programu SQL Server używana** , a następnie wprowadź informacje dotyczące uwierzytelniania.
   4. W hello **bazy danych tooa Connect** wybierz istniejącą bazę danych usługi SQL Data Warehouse.
   5. Kliknij przycisk **połączenie testowe**.
   6. Okno dialogowe hello hello wyniki testu połączenia hello raporty, kliknij przycisk **OK** tooreturn toohello **Menedżera połączeń** okno dialogowe.
   7. W hello **Menedżera połączeń** okno dialogowe, kliknij przycisk **OK** tooreturn toohello **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe.
5. W hello **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe, kliknij przycisk **OK** tooreturn toohello **ADO.NET docelowego edytora**.
6. W hello **ADO.NET docelowego edytora**, kliknij przycisk **nowy** dalej toohello **za pomocą tabeli lub widoku** hello tooopen listy **Create Table** — okno dialogowe toocreate tabelę docelową z listy kolumn, który odpowiada hello tabeli źródłowej.
   
    ![][12a]
7. W hello **Create Table** okna dialogowego pozycję hello następujące czynności.
   
   1. Zmień nazwę hello tabeli docelowej hello zbyt**szczegóły zamówienia sprzedaży**.
   2. Usuń hello **rowguid** kolumny. Witaj **uniqueidentifier** — typ danych nie jest obsługiwana w usłudze SQL Data Warehouse.
   3. Zmień typ danych hello hello **LineTotal** kolumny zbyt**pieniędzy**. Witaj **dziesiętną** — typ danych nie jest obsługiwana w usłudze SQL Data Warehouse. Informacje o obsługiwane typy danych, zobacz [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Kliknij przycisk **OK** toocreate hello tabeli i przywracać toohello **ADO.NET docelowego edytora**.
8. W hello **ADO.NET docelowego edytora**, wybierz pozycję hello **mapowania** karcie toosee jak kolumny w źródle hello są mapowane toocolumns hello miejsca docelowego.
   
    ![][13]
9. Kliknij przycisk **OK** toofinish konfigurowania hello źródła danych.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Krok 6: Uruchamianie hello pakietu tooload hello danych
Uruchom hello pakietu przez kliknięcie hello **Start** przycisk na pasku narzędzi hello lub wybierając jedną z hello **Uruchom** opcji na powitania **debugowania** menu.

Pakiet powitania po rozpoczęciu toorun, zobacz żółty koła Obracająca tooindicate działania, a także liczbę hello wykonanej do tej pory przetworzonych wierszy.

![][14]

Po zakończeniu uruchamiania pakietów hello możesz Zobacz zielone znaczniki wyboru tooindicate Powodzenie jak również hello całkowitej liczby wierszy danych załadowanych z docelowym toohello źródła hello.

![][15]

Gratulacje! Pomyślnie zastosowano SQL Server Integration Services tooload danych do usługi Azure SQL Data Warehouse.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat przepływu danych usług SSIS hello. Zacznij tutaj: [przepływu danych][Data Flow].
* Dowiedz się, jak toodebug i rozwiązywanie problemów w środowisku projektowania hello uprawnienie pakietów. Zacznij tutaj: [Rozwiązywanie problemów z narzędzia do tworzenia pakietu][Troubleshooting Tools for Package Development].
* Dowiedz się, jak toodeploy Twojego SSIS projektów, a następnie umieszcza tooIntegration serwera usług lub tooanother lokalizacji magazynu. Zacznij tutaj: [projekty wdrożeń i pakietów][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
