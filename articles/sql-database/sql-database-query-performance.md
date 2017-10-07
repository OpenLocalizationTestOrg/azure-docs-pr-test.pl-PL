---
title: "szczegółowe informacje o wydajności aaaQuery bazy danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności kwerendy identyfikuje hello większości używające Procesora zapytań dla bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Wgląd wydajności kwerendy bazy danych Azure SQL
Zarządzanie i dostrajania wydajności hello relacyjnych baz danych jest trudne zadanie, które wymaga znaczących wiedzę i czas inwestycji. Szczegółowe informacje o wydajności zapytań pozwala toospend mniej czasu Rozwiązywanie problemów z wydajnością bazy danych podając następujące hello:

* Bardziej szczegółowe informacje na temat użycia zasobów (bazy danych DTU) bazy danych. 
* Witaj najważniejszych zapytań przez Procesor/czas trwania/wykonywania licznik, który może potencjalnie dostroić zwiększonej wydajności.
* Witaj toodrill możliwości w dół do szczegółów hello zapytania, Wyświetl tekst i historii wykorzystania zasobów. 
* Adnotacje, które zawierają akcje wykonywane przez dostrajania wydajności [doradcy bazy danych SQL Azure](sql-database-advisor.md)  



## <a name="prerequisites"></a>Wymagania wstępne
* Szczegółowe informacje o wydajności wymaga, aby zapytania [magazyn zapytań](https://msdn.microsoft.com/library/dn817826.aspx) jest aktywny w bazie danych. Jeśli Magazyn zapytań nie jest uruchomiona, hello portal monit tooturn go.

## <a name="permissions"></a>Uprawnienia
następujące Hello [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) uprawnienia są wymagane toouse szczegółowe informacje o wydajności zapytań: 

* **Czytnik**, **właściciela**, **współautora**, **Współautor bazy danych SQL**, lub **programu SQL Server współautora** uprawnienia są Wymagany zasób najwyższego hello tooview wykorzystywanie kwerend i wykresy. 
* **Właściciel**, **współautora**, **Współautor bazy danych SQL**, lub **programu SQL Server współautora** tekst zapytania tooview wymagane są uprawnienia.

## <a name="using-query-performance-insight"></a>Przy użyciu szczegółowe informacje o wydajności zapytań
Szczegółowe informacje o wydajności zapytań jest łatwe toouse:

* Otwórz [portalu Azure](https://portal.azure.com/) i Znajdź bazy danych, które mają tooexamine. 
  * Z menu po lewej stronie, w ramach pomocy technicznej i rozwiązywania problemów wybierz opcję "Szybkie szczegółowe informacje o wydajności zapytań".
* Na pierwszej karcie hello Przejrzyj listę hello najważniejszych zapytań korzystanie z zasobów.
* Wybierz tooview określone zapytanie jego szczegóły.
* Otwórz [doradcy bazy danych SQL Azure](sql-database-advisor.md) i sprawdź, czy wszystkie zalecenia są dostępne.
* Za pomocą suwaków lub powiększenie toochange ikony obserwowanych interwału.
  
    ![pulpit nawigacyjny wydajności](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Po kilku godzinach danych musi toobe przechwycone przez Magazyn zapytań dla zapytania SQL Database tooprovide szczegółowe informacje o wydajności. Jeśli hello bazy danych nie ma aktywności lub magazyn zapytań był nieaktywny w przedziale czasu, wykresy hello będzie pusta podczas wyświetlania tego okresu. Mogą włączyć magazyn zapytań w dowolnym momencie, jeśli nie jest uruchomiona.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Przejrzyj górny Procesora korzystanie z zapytań
W hello [portal](http://portal.azure.com) hello następujące:

1. Przeglądaj tooa bazy danych SQL, a następnie kliknij przycisk **wszystkie ustawienia** > **pomocy technicznej i rozwiązywania problemów** > **szczegółowe informacje o wydajności zapytań**. 
   
    ![Szczegółowe informacje o wydajności zapytań][1]
   
    Otwiera widok najważniejszych zapytań Hello i hello najważniejszych Procesora zapytań odbierająca komunikaty są wyświetlane.
2. Kliknij przycisk wokół hello wykresu, aby uzyskać szczegółowe informacje.<br>Hello pierwszego wiersza wyświetlane ogólnej % jednostek dtu w warstwie hello bazy danych, podczas gdy paski hello Pokaż używane przez zapytania hello wybrane interwale wybranego hello procent użycia procesora CPU (na przykład, jeśli **ostatni tydzień** wybrano każdy pasek reprezentuje jeden dzień).
   
    ![najważniejszych zapytań][2]
   
    Siatka dolnej Hello reprezentuje zagregowane informacje hello widoczne zapytań.
   
   * Identyfikator zapytania — Unikatowy identyfikator zapytania w bazie danych.
   * Procesor zapytań interwale zauważalne (zależy od funkcji agregacji tabeli).
   * Czas trwania jednego zapytania (zależy od funkcji agregacji tabeli).
   * Całkowita liczba wykonaniami dla określonego zapytania.
     
     Wybierz lub wyczyść tooinclude poszczególnych kwerend lub wykluczyć je z wykresu hello przy użyciu pola wyboru.
3. W przypadku danych starych, kliknij przycisk hello **Odśwież** przycisku.
4. Za pomocą suwaków i przedziałach obserwacji toochange przycisków powiększenia i zbadaj nagłego: ![ustawienia](./media/sql-database-query-performance/zoom.png)
5. Opcjonalnie, jeśli chcesz inny widok, możesz zaznaczyć **niestandardowy** kartę i ustawić:
   
   * Metryka (CPU, czas trwania, liczba wykonań)
   * Interwał czasu (ostatni tydzień ostatni miesiąc ostatnich 24 godzin). 
   * Liczba zapytań.
   * Funkcją agregacji.
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Wyświetlanie szczegółów pojedynczych zapytań
Szczegóły kwerendy tooview:

1. Kliknij każde zapytanie operacji hello listę najważniejszych zapytań.
   
    ![Szczegóły](./media/sql-database-query-performance/details.png)
2. Otwiera widok szczegółów Hello i liczba zużycie/czas trwania/wykonania Procesora kwerend hello dzieli się wraz z upływem czasu.
3. Kliknij przycisk wokół hello wykresu, aby uzyskać szczegółowe informacje.
   
   * Górny wykres pokazuje wiersza z ogólną % jednostek dtu w warstwie bazy danych i paski hello są używane przez wybrane zapytanie hello procent użycia procesora CPU.
   * Drugi wykres przedstawia całkowity czas trwania przez wybrane zapytanie hello.
   * Wykres dolnej pokazuje łączna liczba wykonań przez wybrane zapytanie hello.
     
     ![Szczegóły kwerendy][3]
4. Opcjonalnie, za pomocą suwaków, przyciski powiększania lub kliknij przycisk **ustawienia** toocustomize sposób wyświetlania danych zapytania lub toopick w innym czasie.

## <a name="review-top-queries-per-duration"></a>Przejrzyj najważniejszych zapytań na czas trwania
Witaj najnowszych aktualizacji szczegółowe informacje o wydajności zapytań, wprowadzono dwie nowe metryki, które mogą ułatwić identyfikację wąskich gardeł: liczba czas trwania i wykonywanie.<br>

Kwerend mają potencjalnie największy hello blokowanie zasobów dłużej, blokowania innych użytkowników i ograniczanie skalowalności. Są one również hello najbardziej odpowiednich do optymalizacji.<br>

tooidentify długo działające kwerendy:

1. Otwórz **niestandardowy** karcie szczegółowe informacje o wydajności zapytań dla wybranej bazy danych
2. Zmień toobe metryki **czas trwania**
3. Wybierz liczbę zapytań i przedziałach obserwacji
4. Wybierz funkcję agregacji
   
   * **Suma** dodaje wszystkie czasu wykonywania zapytania interwału obserwacji całego.
   * **Maksymalna liczba** znajduje zapytań, które czas wykonywania był maksymalna w przedziałach obserwacji całego.
   * **Średni** znajduje Średni czas wykonania wszystkich zapytań wykonaniami i wyświetlić hello top poza te wartości. 
     
     ![czas trwania kwerendy][4]

## <a name="review-top-queries-per-execution-count"></a>Przejrzyj najważniejszych zapytań na liczba wykonania
Wysoka liczba wykonań nie może mieć wpływ sama baza danych i użycia zasobów może być niski, ale może spowodować, że aplikacja ogólna powolne.

W niektórych przypadkach wykonanie bardzo dużej liczby może prowadzić tooincrease sieci rund. Rund znacznie wpłynąć na wydajność. Są one podmiotu toonetwork opóźnienia i toodownstream opóźnienia serwera. 

Wiele witryn sieci Web opartych na danych dostęp silnie hello bazy danych, dla każdego żądania użytkownika. Podczas buforowania pomaga, hello połączeń zwiększenie ruchu sieciowego i obciążenie przetwarzaniem na powitania serwera bazy danych może niekorzystnie wpłynąć na wydajność.  Ogólne porady jest tookeep round rund tooan absolutne minimum.

tooidentify często wykonywane zapytania zapytań ("chatty"):

1. Otwórz **niestandardowy** karcie szczegółowe informacje o wydajności zapytań dla wybranej bazy danych
2. Zmień toobe metryki **liczba wykonania**
3. Wybierz liczbę zapytań i przedziałach obserwacji
   
    ![Liczba wykonania zapytania][5]

## <a name="understanding-performance-tuning-annotations"></a>Opis adnotacje dostrajania wydajności
Podczas eksploracji obciążenie w szczegółowe informacje o wydajności zapytań, można zauważyć ikon z pionowym wierszem na powitania wykresu.<br>

Te ikony są adnotacje; reprezentują wydajności wpływających na akcje wykonywane przez [doradcy bazy danych SQL Azure](sql-database-advisor.md). Dzięki aktywowania adnotacji możesz uzyskać podstawowe informacje o akcji hello:

![Adnotacja zapytania][6]

Jeśli chcesz tooknow więcej lub zastosować zalecenia usługi advisor, kliknij ikonę hello. Zostanie otwarty szczegóły akcji. Jeśli jest aktywny zalecenia można zastosować razu za pomocą polecenia.

![Szczegóły adnotacji kwerendy][7]

### <a name="multiple-annotations"></a>Wiele adnotacji.
Jest to możliwe, że z powodu poziomu powiększenia adnotacje tooeach Zamknij inne będzie pobrać zwinięte do jednego. To będą reprezentowane przez specjalnej ikony, klikając go zostanie otwarty nowy blok, gdy lista pogrupowanych adnotacje będą wyświetlane.
Korelowanie zapytań i akcji dostrajania wydajności mogą pomóc toobetter zrozumieć obciążenie. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Optymalizowanie konfiguracji magazynu zapytań hello, aby uzyskać szczegółowe informacje o wydajności zapytań
Podczas korzystania z szczegółowe informacje o wydajności zapytań mogą wystąpić następujące magazynu zapytań wiadomości powitania:

* "Magazyn zapytań nie jest prawidłowo skonfigurowany na tę bazę danych. Kliknij tutaj toolearn więcej".
* "Magazyn zapytań nie jest prawidłowo skonfigurowany na tę bazę danych. Kliknij tutaj ustawienia toochange". 

Komunikaty te są zwykle widoczne, gdy magazyn zapytań nie jest możliwe toocollect nowych danych. 

Pierwszym przypadku się stanie, jeśli magazyn zapytań jest w stanie tylko do odczytu i parametry zostały ustawione optymalnie. Można temu zaradzić przez zwiększenie rozmiaru magazynu zapytań lub wyczyszczenie magazynu zapytań.

![przycisk qds][8]

Drugim przypadku się stanie, jeśli magazyn zapytań jest wyłączony lub parametry nie są ustawione optymalnie. <br>Witaj przechowywania i przechwytywania zasad i Włącz magazyn zapytań można zmienić, wykonując poniższe polecenia lub bezpośrednio z portalu:

![przycisk qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Zalecane zasady przechowywania i przechwytywania
Istnieją dwa typy zasad przechowywania:

* Na podstawie rozmiaru — po osiągnięciu tooAUTO zestaw zostanie czyszczenia automatycznie prawie maksymalny rozmiar danych.
* Czas na podstawie — domyślnie możemy zostanie ustawiony too30 dni, co oznacza, że, jeśli magazyn zapytań zabraknie miejsca, spowoduje to usunięcie zapytania o informacje o starsze niż 30 dni

Przechwyć można ustawić zasady:

* **Wszystkie** -przechwytuje wszystkie zapytania.
* **Automatycznie** -rzadkim zapytania i zapytania z nieznaczne czas trwania kompilacji i wykonywanie zostaną zignorowane. Wewnętrznie zależą progi czas wykonywania liczby, kompilacji i środowiska wykonawczego. Jest to opcja domyślna hello.
* **Brak** — magazyn zapytań zatrzymuje przechwytywanie nowego zapytania, jednak Statystyka środowiska uruchomieniowego już przechwyconych zapytania są nadal zbierane.

Firma Microsoft zaleca ustawienie wszystkich tooAUTO zasad i wyczyść zasad too30 dni:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Zwiększ rozmiar magazynu zapytań. Może to być wykonywane przez łączącego tooa bazę danych i wystawiających następujące zapytania:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Stosowanie tych ustawień spowoduje ostatecznie magazynu zapytań zbieranie nowego zapytania, jednak jeśli nie chcesz toowait można wyczyścić magazyn zapytań. 

> [!NOTE]
> Wykonywanie zapytania następujące spowoduje usunięcie wszystkich bieżących informacji w hello magazynu zapytań. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Podsumowanie
Szczegółowe informacje o wydajności zapytań ułatwia zrozumienie wpływu hello obciążenia zapytania i jego powiązań toodatabase zużycia zasobów. W przypadku tej funkcji będzie informacje o hello zapytania zużywające najwięcej zasobów i łatwo zidentyfikować toofix hello z nich, zanim staną się problem.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać dodatkowe zalecenia dotyczące poprawy wydajności hello bazy danych SQL, kliknij [zalecenia](sql-database-advisor.md) na powitania **szczegółowe informacje o wydajności zapytań** bloku.

![Doradca wydajności](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

