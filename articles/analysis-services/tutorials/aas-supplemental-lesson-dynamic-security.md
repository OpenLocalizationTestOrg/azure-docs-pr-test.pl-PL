---
title: aaa "samouczek lekcji dodatkowych usług Azure Analysis Services: dynamiczne zabezpieczeń | Opis elementu Microsoft Docs": w tym artykule opisano, jak filtry toouse dynamiczne zabezpieczeń przy użyciu wiersza hello samouczka usług Azure Analysis Services.
usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Lekcja uzupełniająca — zabezpieczenia dynamiczne

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji uzupełniającej utworzysz dodatkową rolę w celu zaimplementowania zabezpieczeń dynamicznych. Dynamiczne zabezpieczeń zapewnia oparte na powitania identyfikator użytkownika, nazwę lub nazwy logowania aktualnie zalogowanego użytkownika hello zabezpieczeń na poziomie wiersza. 
  
tooimplement dynamiczne zabezpieczeń, możesz dodać modelu tooyour tabeli zawierającej nazwy użytkowników hello tych użytkowników, które można połączyć modelu toohello i Przeglądaj modelu obiektów i danych. model Hello, utworzone za pomocą tego samouczka jest w kontekście hello Adventure Works; jednak toocomplete to lekcja, należy dodać tabelę zawierającą użytkowników z własnej domeny. Nie trzeba hello hasła dla hello nazwy użytkowników, które są dodawane. toocreate tabelę EmployeeSecurity z małej przykładowej użytkowników z własnej domeny, funkcja hello wklejania, wklejanie danych pracowników z arkusz kalkulacyjny programu Excel. W przypadku rzeczywistych hello tabeli zawierającej nazwy użytkowników będzie zazwyczaj tabelę z istniejącej bazy danych jako źródła danych; na przykład rzeczywistej DimEmployee tabeli.  
  
tooimplement dynamiczne zabezpieczeń, użyj dwóch funkcji języka DAX: [funkcja USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) i [funkcja LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Te funkcje, zastosowane w formule filtra wierszy, są definiowane w nowej roli. Funkcja LOOKUPVALUE hello formuła hello określa wartość z tabeli EmployeeSecurity hello. Formuła Hello następnie przekazuje, że wartość toohello USERNAME funkcji, która określa nazwę użytkownika hello zalogowanego użytkownika hello należy toothis roli. Witaj, użytkownik może następnie przeglądać tylko danych określoną przez rolę hello filtrów wierszy. W tym scenariuszu należy określić, że pracownicy sprzedaży można przeglądać tylko danych sprzedaży w Internecie dla hello terytoriów sprzedaży, w których one należą do.  
  
Te zadania, które są unikatowe toothis scenariusza modelu tabelarycznego Adventure Works, ale nie będą zawsze miały zastosowania tooa rzeczywistych scenariuszy są określone jako takie. Każde zadanie zawiera dodatkowe informacje opisujące cel hello hello zadania.  
  
Szacowany czas toocomplete tej lekcji: **30 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tym uzupełniające lekcji, powinno mieć ukończone wszystkie poprzednie — lekcje.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Dodaj hello DimSalesTerritory tabeli toohello AW Internet sprzedaży tabelarycznym modelu projektu  
tooimplement dynamiczne zabezpieczeń w tym scenariuszu Firma Adventure Works, należy dodać dwa dodatkowe tabele tooyour modelu. Witaj pierwszej tabeli dodawany jest DimSalesTerritory (jako obszar sprzedaży) z hello tej samej bazy danych AdventureWorksDW. Należy zastosować tabeli SalesTerritory toohello filtr wiersza, która definiuje danych hello później można przeglądać hello zalogowanego użytkownika.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tooadd hello DimSalesTerritory tabeli  
  
1.  W Eksploratorze modeli tabelarycznych wybierz pozycję **Źródła danych**, kliknij prawym przyciskiem myszy połączenie, a następnie kliknij pozycję **Importuj nowe tabele**.  

    Jeśli zostanie wyświetlone okno dialogowe poświadczeń personifikacji hello, wpisz poświadczenia personifikacji hello użyte Lekcja 2: Dodawanie danych.
  
2.  W Nawigatorze, wybierz hello **DimSalesTerritory** tabeli, a następnie kliknij przycisk **OK**.    
  
3.  W edytorze zapytań kliknij hello **DimSalesTerritory** zapytania, a następnie usuń **SalesTerritoryAlternateKey** kolumny.  
  
7.  Kliknij przycisk **Importuj**.  
  
    Nowa tabela Hello jest dodawana toohello roboczym modelu. Obiekty i dane z tabeli DimSalesTerritory źródła hello następnie są importowane do modelu tabelarycznego sprzedaży AW Internet.  
  
9. Po tabeli hello został pomyślnie zaimportowany, kliknij przycisk **Zamknij**.  

## <a name="add-a-table-with-user-name-data"></a>Dodawanie tabeli z danymi dotyczącymi nazw użytkowników  
Tabela DimEmployee Hello w przykładowej bazy danych AdventureWorksDW hello zawiera użytkowników z domeny AdventureWorks hello. Te nazwy użytkowników nie istnieją w Twoim własnym środowisku. Należy utworzyć w modelu tabelę zawierającą małą próbkę (co najmniej trzy elementy) rzeczywistych użytkowników z Twojej organizacji. Następnie dodaj tych użytkowników jako elementy członkowskie toohello nową rolę. Nie trzeba hello hasła dla hello przykładowe nazwy użytkownika, ale trzeba rzeczywistej nazwy użytkowników systemu Windows z własnej domeny.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd tabeli EmployeeSecurity  
  
1.  Otwórz program Microsoft Excel i utwórz arkusz.  
  
2.  Hello w poniższej tabeli, w tym wierszu nagłówka hello, skopiuj i wklej go do arkusza hello.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Zamień na powitania imię, nazwisko i domena azwa_użytkownika hello nazwy i identyfikatory logowania trzech użytkowników w organizacji. Umieść hello jednego użytkownika na powitania pierwsze dwa wiersze, dla 1 identyfikator pracownika, przedstawiający toomore niż jeden obszar sprzedaży należy ten użytkownik. Pozostaw pola Identyfikator pracownika i SalesTerritoryId hello są one.  
  
4.  Zapisz skoroszyt hello jako **SampleEmployee**.  
  
5.  W arkuszu hello, wybierz wszystkie komórki hello z danymi pracownika, włącznie z nagłówkami hello, a następnie kliknij prawym przyciskiem myszy hello wybrane dane, a następnie kliknij **kopiowania**.  
  
6.  Programu SSDT, kliknij przycisk hello **Edytuj** menu, a następnie kliknij przycisk **Wklej**.  
  
    Jeśli Wklej jest wyszarzone, kliknij pozycję wszystkie kolumny tabeli w oknie projektowania modelu hello i spróbuj ponownie.  
  
7.  W hello **Podgląd Wklej** okna dialogowego, **nazwy tabeli**, typ **EmployeeSecurity**.  
  
8.  W **toobe danych wkleić**, sprawdź dane hello obejmują wszystkie dane użytkownika hello i nagłówków z hello SampleEmployee arkusza.  
  
9. Sprawdź, czy pole **Użyj pierwszego wiersza jako nagłówków kolumn** jest zaznaczone, a następnie kliknij przycisk **OK**.  
  
    Utworzono nową tabelę z danymi pracowników skopiowane z arkusza SampleEmployee hello o nazwie EmployeeSecurity.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Tworzenie relacji między tabelami FactInternetSales, DimGeography i DimSalesTerritory  
Witaj wszystkich Tabela FactInternetSales, DimGeography i DimSalesTerritory zawierać wspólnej kolumny SalesTerritoryId. Witaj SalesTerritoryId kolumny w tabeli DimSalesTerritory hello zawiera wartości w inny identyfikator dla każdego obszaru sprzedaży.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>toocreate relacje między hello FactInternetSales, DimGeography i hello DimSalesTerritory tabeli  
  
1.  W widoku diagramu, hello **DimGeography** tabeli, kliknij i przytrzymaj hello **SalesTerritoryId** kolumny, a następnie przeciągnij hello kursora toohello **SalesTerritoryId** kolumny w hello **DimSalesTerritory** tabeli, a następnie zwolnij.  
  
2.  W hello **FactInternetSales** tabeli, kliknij i przytrzymaj hello **SalesTerritoryId** kolumny, a następnie przeciągnij hello kursora toohello **SalesTerritoryId** kolumny w hello  **DimSalesTerritory** tabeli, a następnie zwolnij.  
  
    Powiadomienie hello Active właściwości dla tej relacji ma wartość False, co oznacza, że jest nieaktywny. Tabela FactInternetSales Hello jest już aktywna relacja innego.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Ukryj hello tabeli EmployeeSecurity za pośrednictwem aplikacji klienckich  
W tym zadaniu można ukryć hello EmployeeSecurity tabeli uniemożliwienie znajdujących się w aplikacji klienckiej pola listy. Pamiętaj, że ukrycie tabeli nie jest równoważne z jej zabezpieczeniem. Użytkownicy mogą nadal wyszukiwać dane w tabeli EmployeeSecurity, jeśli znają odpowiedni sposób. toosecure hello EmployeeSecurity tabeli danych, uniemożliwia użytkownikom tooquery może być dowolną z jego danych, zastosuj filtr w późniejszym zadań.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>Tabela EmployeeSecurity hello toohide za pośrednictwem aplikacji klienckich  
  
-   W Projektancie modeli hello, w widoku diagramu, kliknij prawym przyciskiem myszy hello **pracownika** nagłówek tabeli, a następnie kliknij przycisk **Ukryj przed narzędziami klienta**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Tworzenie roli użytkownika Sales Employees by Territory  
W tym zadaniu utworzysz rolę użytkownika. Ta rola obejmuje definiujący, które wiersze tabeli DimSalesTerritory hello są widoczne toousers filtr wiersza. Hello jest następnie stosowany filtr w relacji jeden do wielu hello kierunek tooall innych tabelach pokrewnych tooDimSalesTerritory. Należy także zastosować filtr, który zabezpiecza hello całą tabelę EmployeeSecurity przed obsługą zapytań przez dowolnego użytkownika, który jest członkiem roli hello.  
  
> [!NOTE]  
> Witaj sprzedaży pracowników przez rolę terytorium, utworzone w tej lekcji ogranicza członków toobrowse (lub zapytanie) tylko dane dotyczące sprzedaży toowhich obszaru sprzedaży hello, do których należą. Jeśli użytkownik zostanie dodany jako członek toohello sprzedaży pracowników przez rolę terytorium, który również występuje jako element członkowski w rolę utworzone w [lekcji 11: tworzenie ról](../tutorials/aas-lesson-11-create-roles.md), Pobierz kombinacja uprawnień. Gdy użytkownik jest członkiem wielu ról, uprawnienia hello i filtry wiersza zdefiniowane dla każdej roli kumulują się. Oznacza to hello użytkownika ma uprawnienia większa hello ustaleniami hello zestawu ról.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate pracowników sprzedaży, przez terytorium roli użytkownika  
  
1.  Programu SSDT, kliknij przycisk hello **modelu** menu, a następnie kliknij przycisk **ról**.  
  
2.  W **Menedżerze ról** kliknij przycisk **Nowa**.  
  
    Nowa rola z hello brak uprawnienia są dodawane toohello listy.  
  
3.  Kliknij hello nową rolę, a następnie w hello **nazwa** kolumny, Zmień nazwę roli hello zbyt**pracowników sprzedaży według obszaru**.  
  
4.  W hello **uprawnienia** kolumny, kliknij listę rozwijaną hello, a następnie wybierz hello **odczytu** uprawnienia.  
  
5.  Kliknij przycisk hello **członków** , a następnie kliknij pozycję **Dodaj**.  
  
6.  W hello **Wybieranie użytkownika lub grupy** okna dialogowego, **Enter hello obiektu o nazwie tooselect**, typ hello pierwszy Przykładowa nazwa użytkownika używana podczas tworzenia tabeli EmployeeSecurity hello. Kliknij przycisk **Sprawdź nazwy** tooverify hello użytkownika nazwa jest prawidłowa, a następnie kliknij **Ok**.  
  
    Powtórz ten krok, dodawanie hello innych przykładowe nazwy użytkownika użytą podczas tworzenia tabeli EmployeeSecurity hello.  
  
7.  Kliknij przycisk hello **filtrów wierszy** kartę.  
  
8.  Dla hello **EmployeeSecurity** tabeli w hello **filtru DAX** kolumny, hello typu następującej formuły:  
  
    ```
      =FALSE()  
    ```
  
    W tej formule Określa, że wszystkie kolumny rozpoznać toohello false warunek typu Boolean. Brak kolumn dla tabeli EmployeeSecurity hello może przeszukiwać członkiem hello sprzedaży pracowników przez terytorium roli użytkownika.  
  
9. Dla hello **DimSalesTerritory** tabeli, hello typu następującej formuły:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    W tej formule hello funkcja LOOKUPVALUE zwraca wszystkie wartości w kolumnie [SalesTerritoryId] DimEmployeeSecurity hello, gdzie hello EmployeeSecurity [LoginId] jest hello sam jako hello bieżący zalogowany nazwa użytkownika systemu Windows i EmployeeSecurity [ SalesTerritoryId] jest hello taki sam jak hello DimSalesTerritory [SalesTerritoryId].  
  
    Witaj zestaw zwrócony przez LOOKUPVALUE identyfikatory obszaru sprzedaży jest używane toorestrict hello wierszy w tabeli DimSalesTerritory hello. Tylko wiersze, gdzie hello SalesTerritoryID dla wiersza hello jest w zestawie hello identyfikatorów zwracane przez funkcję LOOKUPVALUE hello są wyświetlane.  
  
10. W obszarze Menedżer ról kliknij przycisk **OK**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Testowanie hello sprzedaży pracowników przez terytorium roli użytkownika  
W tym zadaniu hello analizy w programie Excel funkcji programu SSDT tootest hello skuteczności hello sprzedaży pracowników przez rolę użytkownika terytorium. Określ jedną nazw użytkowników hello dodano toohello EmployeeSecurity tabelę i jest członkiem roli hello. Ta nazwa użytkownika jest następnie używany jako hello obowiązująca nazwa użytkownika połączenia hello między programu Excel i hello modelu.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>Witaj tootest sprzedaży pracowników przez terytorium roli użytkownika  
  
1.  Programu SSDT, kliknij przycisk hello **modelu** menu, a następnie kliknij przycisk **analizy w programie Excel**.  
  
2.  W hello **analizy w programie Excel** okna dialogowego, **Określ hello użytkownika nazwę lub rolę toouse tooconnect toohello modelu**, wybierz pozycję **inny użytkownik systemu Windows**, a następnie kliknij przycisk **Przeglądaj**.  
  
3.  W hello **Wybieranie użytkownika lub grupy** okna dialogowego, **wprowadź tooselect nazwa obiektu hello**, wpisz nazwę użytkownika, uwzględnione w tabeli EmployeeSecurity hello, a następnie kliknij przycisk **Sprawdź nazwy**.  
  
4.  Kliknij przycisk **Ok** tooclose hello **Wybieranie użytkownika lub grupy** , a następnie kliknij przycisk **Ok** tooclose hello **analizy w programie Excel** okno dialogowe.  
  
    Zostanie otwarty nowy skoroszyt w programie Excel. Automatycznie utworzona zostanie tabela przestawna. Witaj listy pól tabeli przestawnej zawiera większość hello pól danych jest dostępne w nowym modelu.  
  
    Powiadomienie hello EmployeeSecurity tabeli nie jest widoczny w hello listy pól tabeli przestawnej. Ta tabela została w poprzednim zadaniu ukryta przed narzędziami klienckimi.  
  
5.  W hello **pola** listy w **sprzedaży Internet ∑** (miary), wybierz opcję hello **InternetTotalSales** miary. Miara Hello jest wprowadzany do hello **wartości** pola.  
  
6.  Wybierz hello **SalesTerritoryId** kolumny z hello **DimSalesTerritory** tabeli. Kolumna Hello jest wprowadzany do hello **etykiety wierszy** pola.  
  
    Internet powiadomienia, wyników sprzedaży są wyświetlane tylko w przypadku hello jeden region toowhich hello obowiązująca nazwa użytkownika używanego należy. Jeśli wybierzesz inną kolumnę, takich jak miasto z tabeli DimGeography hello pole wiersza etykiety, miasta tylko w hello obszaru sprzedaży toowhich hello skuteczne użytkownika należy są wyświetlane.  
  
    Tego użytkownika nie może przejrzeć lub wszelkich danych sprzedaży Internet terytoriów innych niż hello jedną należą one do zapytania. Jest to ograniczenie, ponieważ hello filtr wiersza zdefiniowane dla tabeli DimSalesTerritory hello, w hello sprzedaży pracowników przez rolę użytkownika terytorium zabezpiecza dane dla wszystkich danych powiązanych tooother terytoriów sprzedaży.  
  
## <a name="see-also"></a>Zobacz też  
[Funkcja USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Funkcja LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Funkcja CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  