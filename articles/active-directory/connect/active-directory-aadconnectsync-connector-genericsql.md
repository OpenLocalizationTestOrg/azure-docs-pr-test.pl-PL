---
title: "Łącznik usług SQL aaaGeneric | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooconfigure Microsoft ogólny Łącznik usług SQL."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Ogólne informacje techniczne Łącznik usług SQL
W tym artykule opisano hello ogólny Łącznik usług SQL. Witaj artykuł dotyczy toohello następujące produkty:

* Program Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Należy użyć poprawki 4.1.3671.0 lub nowszym [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 i FIM2010R2 hello łącznika jest dostępna do pobrania z hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee ten łącznik akcji, zobacz hello [ogólny łącznik SQL krok](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) artykułu.

## <a name="overview-of-hello-generic-sql-connector"></a>Omówienie hello ogólny Łącznik usług SQL
Witaj ogólny Łącznik usług SQL umożliwia usługi synchronizacji hello toointegrate z systemem bazy danych, który zapewnia łączność ODBC.  

Z punktu widzenia wysokiego poziomu hello następujące funkcje są obsługiwane przez hello bieżącej wersji łącznika hello:

| Funkcja | Pomoc techniczna |
| --- | --- |
| Połączonego źródła danych |Witaj łącznika jest obsługiwana przez wszystkie 64-bitowe sterowniki ODBC. Był testowany z następujących hello: <li>Program Microsoft SQL Server i SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 i 11 g</li><li>MySQL 5.x</li> |
| Scenariusze |<li>Zarządzanie cyklem życia obiektów</li><li>Zarządzanie hasłami</li> |
| Operacje |<li>Pełny Import i różnicowe importu, eksportu</li><li>Eksportu: Dodawanie, usuwanie, aktualizacji i Zastąp</li><li>Ustawianie hasła, Zmień hasło</li> |
| Schemat |<li>Dynamiczne odnajdowanie obiektów i atrybutów</li> |

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem hello łącznika, upewnij się, że masz następujące hello na powitania serwera synchronizacji:

* Framework Microsoft .NET 4.5.2 lub nowszej
* 64-bitowych klienta ODBC — sterowniki

### <a name="permissions-in-connected-data-source"></a>Uprawnienia w połączonego źródła danych
toocreate lub wykonywania zadań hello obsługiwane w SQL ogólny łącznik, musi mieć:

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Porty i protokoły
Hello portów wymaganych do toowork sterownika ODBC hello zapoznaj się dokumentacją hello bazy danych dostawcy.

## <a name="create-a-new-connector"></a>Utwórz nowy łącznik
tooCreate łącznik SQL ogólnego w **usługi synchronizacji** wybierz **agenta zarządzania** i **Utwórz**. Wybierz hello **ogólnego SQL (Microsoft)** łącznika.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Łączność
Hello łącznik używa pliku ODBC DSN dla połączenia. Tworzenie przy użyciu pliku DSN hello **źródeł danych ODBC** w menu start hello w obszarze **narzędzia administracyjne**. Narzędzia administracyjnego hello, Utwórz **pliku DSN** , może zostać dostarczona toohello łącznika.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

ekran łączności Hello hello jest najpierw podczas tworzenia nowego łącznika SQL ogólnego. Należy najpierw hello tooprovide następujących informacji:

* Ścieżka pliku DSN
* Authentication
  * Nazwa użytkownika
  * Hasło

Witaj bazy danych powinna obsługiwać jedną z następujących metod uwierzytelniania:

* **Uwierzytelnianie systemu Windows**: hello uwierzytelniania bazy danych używa hello Windows poświadczenia tooverify hello użytkownika. Hello określona nazwa użytkownika/hasło jest używane tooauthenticate z hello bazy danych. To konto wymaga uprawnienia toohello w bazie danych.
* **Uwierzytelnianie SQL**: hello uwierzytelniania bazy danych używa hello nazwę użytkownika/hasło zdefiniowane jednej hello łączności ekranu tooconnect toohello bazy danych. Jeśli przechowujesz hello, nazwę użytkownika/hasło w pliku DSN hello hello poświadczenia podane na ekranie łączności hello mają pierwszeństwo.
* **Uwierzytelnianie bazy danych SQL Azure**: Aby uzyskać więcej informacji, zobacz [tooSQL bazy danych przy użyciu usługi Azure uwierzytelnianie usługi Active Directory Connect](../../sql-database/sql-database-aad-authentication.md).

**Nazwa Wyróżniająca jest zakotwiczenia**: Jeśli wybierzesz tę opcję, nazwa Wyróżniająca hello jest również używany jako atrybut zakotwiczenia hello. Może służyć do prostych implementacji, ale ma także hello następujące ograniczenia:

* Łącznik obsługuje tylko jeden typ obiektu. W związku z tym wszystkich odwołań, które atrybutów może odwoływać się tylko hello tego samego typu obiektu.

**Typ eksportu: Obiekt Zamień**: podczas eksportu, gdy tylko niektóre atrybuty, które zostały zmienione, hello całego obiektu ze wszystkich atrybutów są eksportowane i zamienia hello istniejący obiekt.

### <a name="schema-1-detect-object-types"></a>Schemat 1 (Wykryj typy obiektów)
Na tej stronie będą tooconfigure jak hello łącznika jest będzie toofind hello różne typy obiektów w bazie danych hello.

Każdy typ obiektu jest przedstawiony jako partycja i skonfigurowane dodatkowe na **Konfiguruj partycje i hierarchie**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Obiekt metody wykrywania typu**: hello łącznik obsługuje te metody wykrywania typu obiektu.

* **Stała wartość**: zawierają hello listę typów obiektu z listy rozdzielanej przecinkami. Na przykład: `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Procedury przechowywanej-tabeli/widoku**: Podaj nazwę hello hello tabeli/widoku/przechowywane procedury, a następnie hello nazwa kolumny, która umożliwia hello listy typów obiektów. Użycie procedury składowanej, określ również parametry dla niego w formacie hello **[Name]: [kierunek]: [wartość]**. Podaj każdego parametru w osobnym wierszu (Użyj klawiszy Ctrl + Enter tooget znakiem nowego wiersza).  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **Zapytanie SQL**: Ta opcja umożliwia tooprovide zapytanie SQL, która zwraca pojedynczą kolumnę o typów obiektów, na przykład `SELECT [Column Name] FROM TABLENAME`. Witaj zwracany kolumna musi być typu String (varchar).

### <a name="schema-2-detect-attribute-types"></a>Schemat 2 (typy atrybutów Wykryj)
Na tej stronie będą tooconfigure jak hello atrybutu nazwy i typy będą toobe wykryte. Opcje konfiguracji Hello są wyświetlane dla każdego typu obiektu na poprzedniej stronie powitania wykryte.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Atrybut metody wykrywania typu**: hello łącznik obsługuje te metody wykrywania typu atrybutu z każdym typem obiektu wykrytych na ekranie 1 schematu.

* **Procedury przechowywanej-tabeli/widoku**: Podaj hello nazwę tabeli/widoku/przechowywane procedury hello, która powinna być używana toofind hello atrybutu nazwy. Użycie procedury składowanej, określ również parametry dla niego w formacie hello **[Name]: [kierunek]: [wartość]**. Podaj każdego parametru w osobnym wierszu (Użyj klawiszy Ctrl + Enter tooget znakiem nowego wiersza). nazwy atrybutów hello toodetect atrybutu wielowartościowego, podaj rozdzielaną przecinkami listę tabel lub widoków. Wielowartościowy scenariusze nie są obsługiwane podczas ma tej samej nazwy kolumn w tabeli nadrzędnej i podrzędnej.
* **Zapytanie SQL**: Ta opcja umożliwia tooprovide zapytanie SQL, która zwraca pojedynczą kolumnę o nazwach atrybutów, na przykład `SELECT [Column Name] FROM TABLENAME`. Witaj zwracany kolumna musi być typu String (varchar).

### <a name="schema-3-define-anchor-and-dn"></a>Schemat 3 (zdefiniuj zakotwiczenia i DN)
Ta strona umożliwia zakotwiczenia tooconfigure i atrybut nazwy domeny dla każdego typu obiektu wykryte. Możesz wybrać wiele atrybutów toomake hello zakotwiczenia unikatowy.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* Atrybuty wielowartościowe i logiczna nie są wyświetlane.
* Tego samego atrybutu nie można użyć nazwy domeny i zakotwiczenia, chyba że **nazwa Wyróżniająca jest zakotwiczenia** jest zaznaczona na stronie łączności hello.
* Jeśli **nazwa Wyróżniająca jest zakotwiczenia** jest zaznaczona na stronie łączności hello, ta strona wymaga atrybutu tylko nazwa Wyróżniająca hello. Ten atrybut będzie również służyć jako hello atrybutu zakotwiczenia.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Schemat 4 (Zdefiniuj typ atrybutu, odwołania i kierunek)
Ta strona umożliwia tooconfigure hello atrybut typu, na przykład liczba całkowita, binary, lub wartość logiczną i kierunek dla każdego atrybutu. Wszystkie atrybuty ze strony **schematu 2** są wymienione w tym atrybutów wielowartościowych.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Typ danych**: używanymi toomap hello atrybutu typu toothose znane hello aparatu synchronizacji. Domyślnie Hello jest hello toouse tego samego typu jak wykryto w schemacie SQL hello, ale nie są łatwo odwołanie i DateTime. Dla osób, należy toospecify **DateTime** lub **odwołania**.
* **Kierunek**: hello atrybut kierunku tooImport, eksportu lub ImportExport można ustawić. ImportExport jest domyślnym.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Uwagi:

* Jeśli typem atrybutu nie jest wykrywalny przez hello łącznika, używa hello String — typ danych.
* **Zagnieżdżone tabele** można uznać za tabel bazy danych z jednej kolumny. Oracle przechowuje hello wierszy zagnieżdżonej tabeli w określonej kolejności. Jednak po pobraniu hello zagnieżdżonej tabeli w zmiennej PL/SQL wierszy hello podano kolejnych indeksy dolne rozpoczyna się od 1. Która zapewnia dostęp tablicy tooindividual wierszy.
* **VARRYS** nie są obsługiwane w łączniku hello.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Schemat 5 (zdefiniuj partycja dla atrybutów odwołania)
Na tej stronie można skonfigurować dla wszystkich atrybutów odwołania, które partycji (typ obiektu) odwołuje się atrybut do.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Jeśli używasz **nazwa Wyróżniająca jest zakotwiczenia**, należy użyć hello hello jedną odwołujesz się z sam typ obiektu. Nie można odwołać obiektu innego typu.

>[!NOTE]
Począwszy od aktualizacji 2017 marca hello jest teraz opcję "*", kiedy ta opcja jest wybrana, a następnie wszystkie typy elementów członkowskich możliwe zostanie zaimportowane.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 Począwszy od 2017 maja hello "*" alias **każda opcja** zmieniono toosupport importowanie i eksportowanie przepływu. Jeśli chcesz toouse tej opcji wielowartościowe tabeli/widoku ma atrybut, który zawiera typ obiektu hello.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> Jeśli "*" jest zaznaczona, a następnie również należy określić nazwę hello hello kolumny z typem obiektu hello.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

Po zaimportowaniu zobaczysz coś podobnego toohello obraz poniżej:

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Parametry globalne
Witaj parametry globalne strona jest używane tooconfigure Import zmian, format daty i godziny i metody hasła.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Witaj ogólny Łącznik usług SQL obsługuje hello czynności metod Import zmian:

* **Wyzwalacz**: zobacz [generowania widoków zmian za pomocą wyzwalaczy](https://technet.microsoft.com/library/cc708665.aspx).
* **Znak wodny**: ogólne podejście, które mogą być używane z dowolną bazą danych. Zapytanie znaku wodnego Hello jest wstępne wypełnianie oparte na powitania bazy danych dostawcy. Kolumna znaku wodnego musi być obecny na każdym tabelę lub widok używane. Ta kolumna musi śledzić INSERT i Update tabele toohello jako i jego zależne od (wielowartościowe lub podrzędnej) tabel. należy zsynchronizować zegary Hello między usługą synchronizacji i powitania serwera bazy danych. W przeciwnym razie niektóre wpisy hello import zmian może zostać pominięte.  
  Ograniczenie:
  * Znak wodny strategii nie nie obiekty usunięte pomocy technicznej.
* **Migawki**: (działa tylko z programem Microsoft SQL Server) [generowanie widoków zmian przy użyciu migawek](https://technet.microsoft.com/library/cc720640.aspx)
* **Śledzenie zmian**: (działa tylko z programem Microsoft SQL Server) [o śledzenie zmian](https://msdn.microsoft.com/library/bb933875.aspx)  
  Ograniczenia:
  * Zakotwiczenia & Nazwa Wyróżniająca atrybutu musi być częścią klucza podstawowego dla wybranego obiektu hello hello tabeli.
  * Zapytania SQL nie jest obsługiwane podczas importowania i eksportowania z śledzenia zmian.

**Dodatkowe parametry**: Określ hello strefy czasowej serwera bazy danych wskazujące, gdzie znajduje się serwer bazy danych. Ta wartość jest używana toosupport hello różnych formatach atrybutów daty i godziny.

Witaj łącznik zawsze przechowuje Data i godzina data w formacie UTC. toobe toocorrectly można przekonwertować hello daty i godziny, należy określić strefę czasową hello powitania serwera bazy danych i format hello używany. Hello format powinien zostać przedstawiony w formacie .net.

Podczas eksportowania każdego atrybutu czasu daty należy podać toohello łącznika w formacie czasu UTC.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Hasło konfiguracji**: hello łącznika zawiera funkcje synchronizacji hasła i obsługuje ustawić i zmienić hasło.

Witaj łącznika udostępnia dwie metody synchronizacji haseł toosupport:

* **Procedura składowana**: Ta metoda wymaga dwóch procedur składowanych toosupport zestawu i Zmień hasło. Wszystkie parametry dla Dodaj typu i zmień hello operacji hasła w **ustawić hasło SP** i **zmienić hasło SP** parametrów odpowiednio jak na poniższym przykładzie.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Rozszerzenie hasło**: Ta metoda wymaga hasła rozszerzenia DLL (należy hello tooprovide nazwa biblioteki DLL rozszerzenia, która implementuje hello [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interfejs). Hasło zestawu rozszerzenia muszą znajdować się w folderze rozszerzenia, dzięki czemu hello łącznika można załadować hello biblioteki DLL w czasie wykonywania.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

Masz również tooenable hello zarządzania hasłami na powitania **skonfigurować rozszerzenia** strony.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Konfiguruj partycje i hierarchie
Na stronie partycje i hierarchie hello wybierz wszystkie typy obiektów. Każdy typ obiektu jest jego własnej partycji.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

Możesz też przesłonić wartości hello zdefiniowanych w hello **łączności** lub **parametry globalne** strony.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Konfiguruj zakotwiczenia
Ta strona jest tylko do odczytu, ponieważ zakotwiczenia hello został już zdefiniowany. Witaj zakotwiczenia wybranego atrybutu jest zawsze dołączany z tooensure typu obiektu hello pozostaje unikatowy różnych typów obiektów.

![punkty kontrolne](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Konfigurowanie parametrów kroku wykonywania
Te kroki są konfigurowane na powitania profilów uruchamiania na powitania łącznika. Te konfiguracje hello faktyczną pracę importowania i eksportowania danych.

### <a name="full-and-delta-import"></a>Pełne i różnicowe importu
Ogólny Łącznik usług SQL wsparcie pełne i Import zmian za pomocą następujących metod:

* Tabela
* Widok
* Procedura składowana
* Zapytanie SQL

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Tabela/Widok**  
atrybuty wielowartościowe tooimport dla obiekt ma nazwę tabeli/widoku przecinkami hello tooprovide w **widoków tabel nazwy z wieloma wartościami** i warunki sprzężenia odpowiednich w hello **waruneksprzężenia**z tabelą nadrzędną hello.

Przykład: Chcesz tooimport hello pracownika obiekt i jego atrybuty wielowartościowe. Istnieją dwie tabele, o nazwie pracownika (główna tabela) i działu (wielowartościowe).
Witaj, po:

* Typ **pracownika** w **tabeli/widoku/SP**.
* Dział typu **widoków tabel nazwy z wieloma wartościami**.
* Wpisz hello warunek sprzężenia między pracownika & działu w **warunek sprzężenia**, na przykład `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Procedury składowane**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Jeśli masz dużą ilość danych, zaleca się tooimplement podział na strony z własnych procedur przechowywanych.
* Z procedury składowanej toosupport podział na strony należy tooprovide indeksu Start i End indeksu. Zobacz: [wydajnie stronicowania z dużą ilością danych](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndexi @EndIndex zastąpione w czasie wykonywania wartość rozmiaru strony odpowiednich skonfigurowanych na **kroku skonfigurować** strony. Na przykład, gdy łącznik hello pobiera pierwszej strony i rozmiar strony hello ma wartość 500, w takiej sytuacji @StartIndex 1 i @EndIndex 500. Te wartości zwiększenie, gdy łącznik pobiera kolejnych stronach i zmień hello @StartIndex & @EndIndex wartość.
* tooexecute sparametryzowana procedury składowanej, podaj parametry hello w `[Name]:[Direction]:[Value]` format. Wprowadź każdy parametr w osobnym wierszu (Użyj klawiszy Ctrl + Enter tooget znakiem nowego wiersza).
* Ogólny Łącznik usług SQL obsługuje również operacji importu z połączonych serwerów w programie Microsoft SQL Server. Jeśli mają być pobrane informacje z tabeli w połączonej serwera, tabeli, powinny być podawane w formacie hello:`[ServerName].[Database].[Schema].[TableName]`
* Ogólny łącznik SQL obsługuje tylko te obiekty, które mają podobną strukturę (zarówno alias nazwę i typ danych) między wykonanie kroków wykrywania informacji i schematu. Zaznaczenie hello różni się obiektów ze schematu oraz informacje podane podczas wykonywania czynności, a następnie Łącznik usług SQL jest toosupport tego typu scenariuszy.

**Zapytanie SQL**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* Kwerend nieobsługiwana zestawy wielu wyników.
* Zapytanie SQL obsługuje hello podział na strony i podaj początkowy indeks zakończenia jako dzielenia toosupport zmiennej i.

### <a name="delta-import"></a>Import zmian
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

Konfiguracja importu zmian wymaga pewnych dodatkowych czynności konfiguracyjnych w porównaniu z pełny Import.

* Jeśli wybierzesz podejścia wyzwalacza lub migawki hello tootrack zmiany różnicowe, należy podać tabeli historii lub migawki bazy danych w **nazwę bazy danych lub tabeli historii migawki** pole.
* Należy również tooprovide warunek sprzężenia między tabelą historii i tabelą nadrzędną, na przykład`Employee.ID=History.EmployeeID`
* tootrack hello transakcji w tabeli nadrzędnej hello z tabeli historii hello, musisz podać nazwę kolumny hello, który zawiera informacje o operacji hello (Dodaj/aktualizowania/usuwania).
* Jeśli wybierzesz tootrack znaku wodnego zmiany różnicowe, podaj nazwę kolumny hello, który zawiera informacje o operacji hello w **nazwa kolumny znacznik limitu górnego**.
* Witaj **zmienić atrybut typu** kolumny jest wymagana dla typu zmiany hello. W tej kolumnie mapuje zmiany, która występuje w tabeli podstawowej hello lub typu w widoku delta hello zmienić tooa Tabela wielu wartości. Ta kolumna może zawierać hello Modify_Attribute Zmień typ, zmień poziom atrybutu lub dodawanie, modyfikowanie, lub usuń zmienić typu dla typu zmiany na poziomie obiektu. Jeśli jest inny niż wartość domyślna hello dodawania, modyfikowania, lub przycisk Usuń, a następnie można zdefiniować te wartości przy użyciu tej opcji.

### <a name="export"></a>Eksportowanie
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

Ogólny łącznik SQL obsługuje eksportu przy użyciu czterech obsługiwanych metod, takich jak:

* Tabela
* Widok
* Procedura składowana
* Zapytanie SQL

**Tabela/Widok**  
Jeśli wybierzesz hello opcja tabelę lub widok, łącznik hello generuje hello odpowiednich zapytań toodo hello eksportu.

**Procedury składowane**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Jeśli wybierzesz opcję procedury składowanej hello eksportu wymaga trzech różnych przechowywane procedury tooperform wstawiania/aktualizacji/usuwania operacji.

* **Dodaj nazwę SP**: SP ten jest uruchamiany, jeśli dowolny obiekt pochodzi tooconnector przez operację wstawiania w tabeli odpowiednich hello.
* **Aktualizacja nazwy SP**: SP ten jest uruchamiany, jeśli dowolny obiekt pochodzi tooconnector aktualizacji w odpowiedniej tabeli hello.
* **Usuń nazwę SP**: SP ten jest uruchamiany, jeśli dowolny obiekt pochodzi tooconnector do usunięcia w odpowiedniej tabeli hello.
* Atrybut wybrane ze schematu hello używane jako procedura przechowywana toohello wartość parametru. Na przykład `EmployeeName: INPUT: @EmployeeName` (EmployeeName jest zaznaczona w schemacie łącznika hello i łącznika hello zastępuje hello odpowiednią wartość. podczas wykonywania eksportu)
* toorun sparametryzowana procedury składowanej, podaj parametry w `[Name]:[Direction]:[Value]` format. Wprowadź każdy parametr w osobnym wierszu (Użyj klawiszy Ctrl + Enter tooget znakiem nowego wiersza).

**Zapytanie SQL**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Jeśli wybierzesz opcję zapytania SQL hello eksportu wymaga trzech różnych zapytań tooperform operacji wstawiania/aktualizacji/usuwania.

* **Wstaw kwerendę**: to zapytanie jest uruchamiany, jeśli dowolny obiekt pochodzi tooconnector przez operację wstawiania w tabeli odpowiednich hello.
* **Zaktualizuj zapytanie**: to zapytanie jest uruchamiany, jeśli dowolny obiekt pochodzi tooconnector aktualizacji w odpowiedniej tabeli hello.
* **Usuń kwerendę**: to zapytanie jest uruchamiany, jeśli dowolny obiekt pochodzi tooconnector do usunięcia w odpowiedniej tabeli hello.
* Atrybut wybrane ze schematu hello używane jako parametru wartość toohello kwerendy, na przykład`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* Aby informacji na temat sposobu rejestrowania tooenable tootroubleshoot hello łącznika, zobacz hello [jak tooEnable ETW Tracing łączników](http://go.microsoft.com/fwlink/?LinkId=335731).
