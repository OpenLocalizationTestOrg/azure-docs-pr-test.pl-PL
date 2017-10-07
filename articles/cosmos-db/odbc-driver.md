---
title: "tooAzure aaaConnect rozwiązania Cosmos DB przy użyciu narzędzi do analizy Biznesowej analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Azure rozwiązania Cosmos bazy danych ODBC sterownika toocreate tabele i widoki, tak, aby znormalizowane danych mogą być wyświetlane w oprogramowania analizy danych i analizy Biznesowej."
keywords: ODBC i sterownik odbc
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Połącz tooAzure rozwiązania Cosmos DB przy użyciu narzędzia do analizy BI ze sterownikiem ODBC hello

Umożliwia sterownika ODBC DB rozwiązania Cosmos Azure Hello tooconnect tooAzure rozwiązania Cosmos bazy danych przy użyciu analizy BI narzędzi takich jak SQL Server Integration Services, Power BI Desktop i Tableau tak, aby można było analizować i tworzenie wizualizacji danych bazy danych Azure rozwiązania Cosmos w tych rozwiązania.

Sterownik ODBC DB rozwiązania Cosmos Azure Hello jest 3.8 ODBC zgodne i obsługuje składni ANSI SQL-92. Witaj toohelp rozbudowane funkcje oferty sterownika renormalize danych w usłudze Azure DB rozwiązania Cosmos. Sterownik hello może reprezentować danych w usłudze Azure DB rozwiązania Cosmos jako tabele i widoki. Sterownik Hello umożliwia tooperform operacji SQL przed hello tabel i widoków, w tym Grupuj według zapytania, wstawiania, aktualizacji i usunięć.

## <a name="why-do-i-need-toonormalize-my-data"></a>Dlaczego należy toonormalize danych?
Azure DB rozwiązania Cosmos jest bezschematową bazą danych, włączając tooiterate aplikacji umożliwia szybkie opracowywanie aplikacji swoje dane modelu na bieżąco hello i nie ograniczają ich tooa strict schematu. Pojedyncza baza danych bazy danych Azure rozwiązania Cosmos może zawierać dokumentów JSON różnych struktur. Jest to doskonałe rozwiązanie dla szybkie programowanie aplikacji, ale po mają tooanalyze i tworzenie raportów danych z użyciem analizy danych i narzędzi do analizy Biznesowej hello danych często musi toobe jako spłaszczone i tooa schematu jest zgodna.

Jest to, gdzie hello sterownik ODBC jest dostarczany. Za pomocą sterownika ODBC hello, użytkownik może teraz renormalized danych w usłudze Azure DB rozwiązania Cosmos w tabelach i widokach dopasowanie tooyour dane analityczne i raportowania musi. schematy Hello renormalized nie mają wpływu na powitania podstawowych danych i nie ograniczają toothem tooadhere deweloperów, po prostu umożliwiają one możesz tooleverage standardem ODBC narzędzia tooaccess hello danych. Dlatego teraz bazy danych Azure DB rozwiązania Cosmos nie tylko będzie element ulubiony dla zespołu deweloperów, ale analityków danych będzie pokochasz je za.

Teraz umożliwia wprowadzenie hello sterownik ODBC.

## <a id="install"></a>Krok 1: Instalowanie sterownika ODBC DB rozwiązania Cosmos Azure hello

1. Pobieranie sterowników hello w danym środowisku:

    * [Microsoft Azure rozwiązania Cosmos bazy danych ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64) dla 64-bitowego systemu Windows
    * [Microsoft Azure rozwiązania Cosmos bazy danych ODBC 32 x 64-bit.msi](https://aka.ms/documentdb-odbc-32x64) dla 32-bitowych na 64-bitowego systemu Windows
    * [Microsoft Azure rozwiązania Cosmos bazy danych ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32) dla 32-bitowego systemu Windows

    Msi hello wykonywania pliku lokalnie, które hello uruchamia **Kreatora instalacji sterownika ODBC bazy danych Microsoft Azure rozwiązania Cosmos**. 
2. Ukończ Kreatora instalacji hello za pomocą sterownika ODBC hello hello domyślne tooinstall wejściowego.
3. Otwórz hello **Administrator źródeł danych ODBC** aplikacji na komputerze, można to zrobić wpisanie **źródeł danych ODBC** w systemie Windows hello w polu wyszukiwania. 
    Można potwierdzić, klikając hello został zainstalowany sterownik hello **sterowniki** kartę i zapewnienie **sterownika ODBC usługi Microsoft Azure rozwiązania Cosmos DB** ma na liście.

    ![Administrator źródła danych ODBC Azure rozwiązania Cosmos bazy danych](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>Krok 2: Łączenie tooyour bazy danych z bazy danych Azure rozwiązania Cosmos

1. Po [sterownika ODBC DB rozwiązania Cosmos Azure hello instalowanie](#install), w hello **Administrator źródła danych ODBC** okna, kliknij przycisk **Dodaj**. Można utworzyć użytkownika lub nazwy DSN systemu. W tym przykładzie tworzymy DSN użytkownika.
2. W hello **Utwórz nowe źródło danych** wybierz **sterownika ODBC usługi Microsoft Azure rozwiązania Cosmos DB**, a następnie kliknij przycisk **Zakończ**.
3. W hello **ustawienia SDN sterownika ODBC Azure rozwiązania Cosmos DB** okna, wypełnij następujące hello: 

    ![Azure okno Ustawienia DSN sterownika ODBC DB rozwiązania Cosmos](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Nazwa źródła danych**: przyjazną nazwę dla hello ODBC DSN. Ta nazwa jest konto bazy danych Azure rozwiązania Cosmos tooyour unikatowy, więc nadaj jej nazwę odpowiednio Jeśli masz wiele kont.
    - **Opis elementu**: Krótki opis hello źródła danych.
    - **Host**: identyfikator URI dla Twojego konta bazy danych Azure rozwiązania Cosmos. Można pobrać to z bloku klucze DB rozwiązania Cosmos Azure hello w hello portalu Azure, jak pokazano w powitania po zrzut ekranu. 
    - **Klawisz dostępu**: hello klucz podstawowy lub pomocniczy, Odczyt i zapis lub tylko do odczytu z bloku klucze DB rozwiązania Cosmos Azure hello w hello portalu Azure, jak pokazano w hello następującego zrzutu ekranu. Zaleca się używać klucza hello tylko do odczytu, jeśli hello DSN służy do przetwarzania danych tylko do odczytu i raportowania.
    ![Azure bloku klucze DB rozwiązania Cosmos](./media/odbc-driver/odbc-driver-keys.png)
    - **Szyfrowanie klucza dostępu dla**: wybierz opcję najlepiej hello na podstawie hello użytkowników tego komputera. 
4. Kliknij przycisk hello **testu** się, że możesz połączyć konto bazy danych Azure rozwiązania Cosmos tooyour toomake przycisku. 
5. Kliknij przycisk **zaawansowane opcje** i hello ustaw następujące wartości:
    - **Zapytanie spójności**: Wybierz hello [poziomu spójności](consistency-levels.md) dla operacji. Domyślnie Hello jest sesji.
    - **Liczba ponownych prób**: Wprowadź hello liczba operacji, jeśli nie została zakończona żądania początkowego hello powodu ograniczania tooservice tooretry.
    - **Plik schematu**: w tym miejscu masz kilka opcji.
        - Domyślnie ten wpis jest (pusty), pozostawiając sterownik hello skanuje hello pierwszej strony danych wszystkie kolekcje toodetermine hello schemat każdej kolekcji. Jest to nazywane mapowania kolekcji. Bez pliku schematu zdefiniowane sterownik hello ma tooperform hello skanowania dla każdej sesji sterowników i może skutkować czasu aplikacji przy użyciu hello DSN wyższej uruchamiania. Firma Microsoft zaleca zawsze skojarzenia pliku schematu dla nazwy DSN.
        - Jeśli masz już plik schematu (prawdopodobnie jedną, które zostały utworzone za pomocą hello [Edytor schematów](#schema-editor)), możesz kliknąć **Przeglądaj**Przejdź tooyour pliku, kliknij przycisk **zapisać**, a następnie kliknij przycisk **OK**.
        - Toocreate nowego schematu, kliknij przycisk **OK**, a następnie kliknij przycisk **Edytor schematów** w oknie głównym hello. Aby kontynuować toohello [Edytor schematów](#schema-editor) informacji. Podczas tworzenia nowego pliku schematu hello, należy pamiętać o toohello wstecz toogo **zaawansowane opcje** pliku schematu hello nowo utworzony tooinclude okna.

6. Po zakończeniu i zamknąć hello **ustawienia DSN sterownika ODBC Azure rozwiązania Cosmos DB** okna, hello jest nowy DSN użytkownika dodane toohello karta DSN użytkownika.

    ![Nowe Azure rozwiązania Cosmos DB DSN ODBC na karcie DSN użytkownika hello](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>Krok 3: Tworzenie definicji schematu przy użyciu metody mapowania kolekcji hello

Istnieją dwa typy metod pobierania próbek, których mogą używać: **mapowania kolekcji** lub **ograniczników tabeli**. Obie metody pobierania próbek mogą korzystać z sesji próbkowania, ale każdej kolekcji można używać tylko metody pobierania próbek określonych. Poniższe kroki Hello utworzyć schemat dla danych hello w co najmniej jednej kolekcji przy użyciu metody mapowania kolekcji hello. Ta metoda pobierania próbek pobiera dane hello na stronie powitania struktury hello toodetermine kolekcji hello danych. Go transposes tabeli tooa kolekcji na powitania po stronie ODBC. Ta metoda pobierania próbek jest wydajne i szybkie po jednorodnego hello danych w kolekcji. Jeśli kolekcja zawiera heterogenicznych typu danych, zalecane jest użycie hello [ograniczników tabeli mapowania metody](#table-mapping) jako zapewnia bardziej niezawodna metoda pobierania próbek struktur danych hello toodetermine w kolekcji hello. 

1. Po zakończeniu kroków od 1 do 4 w [połączenia bazy danych z bazy danych Azure rozwiązania Cosmos tooyour](#connect), kliknij przycisk **Edytor schematów** w hello **ustawienia DSN sterownika ODBC Azure rozwiązania Cosmos DB** okna.

    ![Przycisk Edytor schematu w oknie Ustawienia DSN sterownika ODBC Azure rozwiązania Cosmos DB hello](./media/odbc-driver/odbc-driver-schema-editor.png)
2. W hello **Edytor schematów** okna, kliknij przycisk **Utwórz nowy**.
    Witaj **generowania schematu** okno wyświetla wszystkie kolekcje hello w hello konta bazy danych Azure rozwiązania Cosmos. 
3. Wybierz co najmniej jeden toosample kolekcji, a następnie kliknij przycisk **próbki**. 
4. W hello **widoku Projekt** są reprezentowane kartę, bazy danych hello schematu i tabeli. W widoku tabeli hello skanowania hello Wyświetla hello zbiór właściwości skojarzone z nazw kolumn hello (Nazwa SQL, nazwa źródła, itp.).
    Dla każdej kolumny można zmodyfikować hello kolumny SQL nazwę, typ SQL hello, długość SQL (jeśli dotyczy), skali (jeśli dotyczy), Precision (jeśli dotyczy) oraz Nullable.
    - Można ustawić **Ukryj kolumnę** za**true** Jeśli chcesz tooexclude tej kolumny z wyników zapytania. Kolumny oznaczone jako Ukryj kolumnę = true nie są zwracane do wyboru i projekcji, mimo że nadal są częścią hello schematu. Na przykład można ukryć wszystkie właściwości wymagane systemu Azure DB rozwiązania Cosmos hello począwszy od "_".
    - Witaj **identyfikator** hello tylko pola, które nie mogą być ukryte, ponieważ jest używany jako klucz podstawowy hello w schemacie znormalizowane hello jest kolumny. 
5. Po określeniu schematu powitania kliknij **pliku** | **zapisać**, przejdź toohello katalogu toosave hello schematu, a następnie kliknij przycisk **zapisać**.

    Jeśli w przyszłości hello toouse tego schematu o nazwie DSN, Otwórz okno Ustawienia DSN sterownika ODBC Azure rozwiązania Cosmos DB hello (za pośrednictwem hello Administrator źródła danych ODBC), kliknij przycisk Opcje zaawansowane, a następnie w polu pliku schematu hello Przejdź toohello zapisany schemat. Zapisywanie tooan pliku schematu istniejącej nazwy DSN modyfikuje hello DSN połączenia tooscope toohello danych i struktury zdefiniowane przez schemat.

## <a id="table-mapping"></a>Krok 4: Tworzenie definicji schematu przy użyciu hello tabeli — ograniczniki mapowania — metoda

Istnieją dwa typy metod pobierania próbek, których mogą używać: **mapowania kolekcji** lub **ograniczników tabeli**. Obie metody pobierania próbek mogą korzystać z sesji próbkowania, ale każdej kolekcji można używać tylko metody pobierania próbek określonych. 

Hello następujące kroki tworzenia schematu dla danych hello w co najmniej jednej kolekcji przy użyciu hello **ograniczników tabeli** mapowanie metody. Firma Microsoft zaleca, użyj tej metody pobierania próbek, gdy kolekcji zawiera heterogeniczne typu danych. Możesz użyć tego hello tooscope — metoda pobierania próbek tooa zestawu atrybutów i jego odpowiednie wartości. Na przykład jeśli dokument zawiera właściwość "Type", możesz zakresu hello próbkowania toohello wartości tej właściwości. wynik końcowy Hello próbkowania hello byłoby zestawu tabel dla każdej z hello wartości dla typu został określony. Na przykład wpisz = samochodu spowoduje utworzenie tabeli samochodu podczas typu = płaszczyzny dałby w efekcie tabeli płaszczyzny.

1. Po zakończeniu kroków od 1 do 4 w [połączenia bazy danych z bazy danych Azure rozwiązania Cosmos tooyour](#connect), kliknij przycisk **Edytor schematów** w oknie Ustawienia DSN sterownika ODBC Azure rozwiązania Cosmos DB hello.
2. W hello **Edytor schematów** okna, kliknij przycisk **Utwórz nowy**.
    Witaj **generowania schematu** okno wyświetla wszystkie kolekcje hello w hello konta bazy danych Azure rozwiązania Cosmos. 
3. Wybierz kolekcję na powitania **przykładowy widok** na karcie hello **definicji mapowanie** kolumny dla kolekcji powitania kliknij **Edytuj**. Następnie w hello **definicji mapowanie** wybierz **ograniczników tabeli** metody. Następnie hello następujące:

    a. W hello **atrybuty** okno, nazwa typu hello właściwości ogranicznika. Jest to właściwość dokumentu, który ma tooscope hello próbkowania, na przykład miasto, a następnie naciśnij klawisz enter. 

    b. Jeśli chcesz tylko tooscope hello próbkowania toocertain wartości dla atrybutu hello podanej, wybierz atrybut hello hello pole wyboru, a następnie wprowadź wartość w hello **wartość** okno, na przykład Seattle a naciśnij klawisz enter. Możesz kontynuować tooadd wiele wartości atrybutów. Po prostu upewnij się, że hello poprawna, że atrybut jest zaznaczone, gdy wprowadzasz wartości.

    Na przykład, Jeśli dołączysz **atrybuty** wartość miasto i chcesz toolimit Twojego tooonly tabeli Dołącz wiersze z wartością Miasto Warszawa i Dubaj, miasta w polu atrybutów hello i Nowy Jork, a następnie Dubaj wejdzie w hello  **Wartości** pole.
4. Kliknij przycisk **OK**. 
5. Po zakończeniu hello definicji mapowanie dla kolekcji hello ma toosample w hello **Edytor schematów** okna, kliknij przycisk **próbki**.
     Dla każdej kolumny można zmodyfikować hello kolumny SQL nazwę, typ SQL hello, długość SQL (jeśli dotyczy), skali (jeśli dotyczy), Precision (jeśli dotyczy) oraz Nullable.
    - Można ustawić **Ukryj kolumnę** za**true** Jeśli chcesz tooexclude tej kolumny z wyników zapytania. Kolumny oznaczone jako Ukryj kolumnę = true nie są zwracane do wyboru i projekcji, mimo że nadal są częścią hello schematu. Na przykład można ukryć wszystkie właściwości hello Azure DB rozwiązania Cosmos system wymagany, począwszy od "_".
    - Witaj **identyfikator** hello tylko pola, które nie mogą być ukryte, ponieważ jest używany jako klucz podstawowy hello w schemacie znormalizowane hello jest kolumny. 
6. Po określeniu schematu powitania kliknij **pliku** | **zapisać**, przejdź toohello katalogu toosave hello schematu, a następnie kliknij przycisk **zapisać**.
7. Po powrocie do hello **ustawienia DSN sterownika ODBC Azure rozwiązania Cosmos DB** okna, kliknij przycisk ** Zaawansowane opcje **. Następnie w hello **pliku schematu** Przejdź toohello zapisany plik schematu a kliknij przycisk **OK**. Kliknij przycisk **OK** ponownie toosave hello DSN. Ta hello zapisuje schemat utworzony toohello DSN. 

## <a name="optional-creating-views"></a>(Opcjonalnie) Tworzenie widoków
Można zdefiniować i tworzyć widoki w ramach procesu pobierania próbek hello. Widoki te są równoważne tooSQL widoków. Są tylko do odczytu i są opcje hello zakresu i projekcje hello zdefiniowanych Azure rozwiązania Cosmos bazy danych SQL. 

toocreate widoku danych, w hello **Edytor schematów** okna na powitania **definicji widoku** kolumny, kliknij przycisk **Dodaj** w wierszu hello hello toosample kolekcji. Następnie w hello **definicji widoku** oknie hello następujące:
1. Kliknij przycisk **nowy**, wprowadź nazwę dla widoku hello, na przykład EmployeesfromSeattleView, a następnie kliknij przycisk **OK**.
2. W hello **Edytowanie widoku** okna, wprowadź zapytanie bazy danych Azure rozwiązania Cosmos. Musi to być zapytania Azure rozwiązania Cosmos bazy danych SQL, na przykład`SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`, a następnie kliknij przycisk **OK**.

Można utworzyć wiele widoków, według uznania. Po zakończeniu definiującego widoków hello można następnie przykładowe hello danych. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>Krok 5: Zostaną wyświetlone dane narzędzi analizy Biznesowej, takich jak Power BI Desktop

Można użyć nowego tooconnect DSN DocumentADB narzędziami standardem ODBC — ten krok pokazuje, jak tooPower tooconnect BI Desktop i tworzenie wizualizacji usługi Power BI.

1. Otwórz program Power BI Desktop.
2. Kliknij przycisk **Pobierz dane**.
3. W hello **Pobierz dane** okna, kliknij przycisk **innych** | **ODBC** | **Connect**.
4. W hello **z ODBC** okna, wybierz hello nazwa źródła danych utworzone, a następnie kliknij przycisk **OK**. Możesz pozostawić hello **zaawansowane opcje** wpisy puste.
5. W hello **dostęp do źródła danych za pomocą sterownika ODBC** wybierz **domyślnej lub niestandardowej** , a następnie kliknij przycisk **Connect**. Nie trzeba tooinclude hello **poświadczeń właściwości parametrów połączenia**.
6. W hello **Nawigator** oknie w lewym okienku hello, rozwiń węzeł bazy danych hello, hello schematu i tabeli hello a następnie wybierz pozycję. Witaj w okienku wyników zawiera dane hello przy użyciu schematu hello, który został utworzony.
7. toovisualize hello danych w usłudze Power BI desktop, pole hello przed nazwą tabeli hello wyboru, a następnie kliknij **obciążenia**.
8. Power BI Desktop na powitania Maks, zaznacz hello karta dane ![Na karcie dane Power BI Desktop](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm dane zostały zaimportowane.
9. Teraz można utworzyć przy użyciu usługi Power BI, klikając kartę raportu hello elementy wizualne ![raport w programie Power BI Desktop](./media/odbc-driver/odbc-driver-report-tab.png), klikając pozycję **nowe Visual**, a następnie dostosowywania kafelka. Aby uzyskać więcej informacji o tworzeniu wizualizacje w programie Power BI Desktop, zobacz [wizualizację typów w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli zostanie wyświetlony następujący błąd hello, upewnij się, hello **hosta** i **klucz dostępu** wartości skopiowany hello portalu Azure w [krok 2](#connect) są poprawne, a następnie spróbuj ponownie. Użyj hello kopiowanie przycisków toohello rogu hello **hosta** i **klucz dostępu** wartości hello bez błędów wartości hello toocopy portalu Azure.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, zobacz [co to jest Azure DB rozwiązania Cosmos?](introduction.md).
