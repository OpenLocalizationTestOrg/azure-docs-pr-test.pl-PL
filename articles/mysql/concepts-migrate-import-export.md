---
title: aaaImport i eksportowanie w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano typowe sposoby tooimport i eksportowanie bazy danych w bazie danych Azure dla programu MySQL, za pomocą narzędzi, takich jak MySQL Workbench."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>Migrowanie bazy danych MySQL za pomocą importowania i eksportowania
W tym artykule opisano dwie typowe tooimporting podejścia i eksportowanie danych tooan Azure bazy danych MySQL serwera przy użyciu narzędzia MySQL Workbench. 

## <a name="before-you-begin"></a>Przed rozpoczęciem
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- Bazy danych Azure dla serwera MySQL, wykonując [utworzenia bazy danych Azure dla serwera MySQL przy użyciu portalu Azure](quickstart-create-mysql-server-database-using-azure-portal.md).
- MySQL Workbench [pobrane](https://dev.mysql.com/downloads/workbench/), lub inny tooimport narzędzie MySQL i eksportu.

## <a name="use-common-tools"></a>Użyj standardowych narzędzi
Użyj standardowych narzędzi, takich jak MySQL Workbench, Toad lub Navicat tooremotely Połącz się i Importuj lub Eksportuj dane do bazy danych Azure dla programu MySQL. 

Użycie tych narzędzi na komputerze klienckim z tooAzure tooconnect połączenia internetowego bazy danych MySQL. Użyj połączenia z protokołem szyfrowania SSL dla najlepsze rozwiązania w zakresie zabezpieczeń, zgodnie z opisem w [łączności Konfigurowanie protokołu SSL w bazie danych Azure dla programu MySQL](concepts-ssl-connection-security.md).

Nie należy toomove importowanie i eksportowanie lokalizacji specjalne chmury tooany plików, podczas migracji tooAzure bazy danych dla programu MySQL. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Utwórz bazę danych na hello Azure bazy danych MySQL serwera
Utwórz pustą bazę danych na hello Azure bazy danych dla serwera MySQL, gdzie chcesz toomigrate hello dane. Za pomocą narzędzia, takie jak bazy danych hello toocreate MySQL Workbench, Toad lub Navicat. Witaj baza danych może mieć hello sama nazwa jak hello baza danych zawiera dane utworzyć zrzutu hello, lub można utworzyć bazę danych pod inną nazwą.

tooget podłączony, Znajdź informacje o połączeniu hello na powitania **właściwości** okienko w bazie danych Azure dla programu MySQL.

![Informacje dotyczące połączenia hello w hello portalu Azure](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Dodaj hello połączenia informacji tooMySQL Workbench.

![Parametry połączenia MySQL Workbench](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Określania, kiedy toouse importowania i eksportowania techniki zamiast zrzutu i przywracania
Użyj tooimport narzędzia MySQL i eksportowanie bazy danych do bazy danych MySQL Azure w hello następujące scenariusze. W innych sytuacjach mogą korzystać z hello [zrzutu i przywrócić](concepts-migrate-dump-restore.md) zamiast tego podejścia. 

- Gdy potrzebne są tooselectively wybrać kilka tooimport tabel z istniejącej bazy danych MySQL do bazy danych MySQL Azure, jego najlepszych toouse hello importu i eksportu techniki.  W ten sposób można pominąć wszystkie zbędne tabele z hello migracji toosave czasu i zasobów. Na przykład użyć hello `--include-tables` lub `--exclude-tables` przełącznik z [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) i hello `--tables` przełącznik z [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Podczas przenoszenia hello obiektów bazy danych innej niż tabele, jawnie utwórz je. Obejmują ograniczenia (klucz podstawowy, klucz obcy, indeksy), widoki, funkcje, procedur, wyzwalaczy i inne bazy danych obiektów, które mają toomigrate.
- Podczas migracji danych z zewnętrznych źródeł danych innego niż bazy danych MySQL, tworzenia plików prostych i zaimportuj je za pomocą [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Upewnij się, że wszystkie tabele w bazie danych hello używać aparatu magazynu InnoDB hello podczas ładowania danych do bazy danych Azure dla programu MySQL. Bazy danych platformy Azure dla programu MySQL obsługuje tylko hello InnoDB aparatu magazynu, więc nie obsługuje aparaty alternatywnych magazynu. Jeśli tabele wymagają magazynu alternatywnych aparatów, tooconvert się, że można je toouse hello InnoDB aparat formatu przed hello tooAzure migracji bazy danych dla programu MySQL. 

Na przykład jeśli WordPress lub sieci web aplikacji, który używa aparatu MyISAM hello, najpierw przekonwertuj tabele hello przez migrację danych hello na InnoDB tabel. Następnie należy przywrócić tooAzure bazy danych dla programu MySQL. Użycie klauzuli hello `ENGINE=INNODB` tooset hello aparatu tworzenia spisu, a następnie transfer danych hello do tabeli zgodne hello przed migracją hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>Zalecenia dotyczące wydajności importowania i eksportowania
-   Przed załadowaniem danych, należy utworzyć indeksy klastrowane i klucze podstawowe. Ładowanie danych w kolejności klucza podstawowego. 
-   Opóźnienie tworzenia indeksów pomocniczych dopiero po danych została załadowana. Tworzenie wszystkich indeksów pomocniczych po załadowaniu. 
-   Wyłącz ograniczeń klucza obcego przed załadowaniem. Wyłączenie sprawdzania klucza obcego zapewnia znaczący wzrost wydajności. Włącz ograniczenia hello i zweryfikować danych na powitania po hello integralności referencyjnej tooensure obciążenia.
-   Ładowanie danych równolegle. Należy unikać zbyt dużo równoległości, które mogłyby spowodować toohit limit zasobów i monitorowanie zasobów przy użyciu metryk hello dostępne w portalu Azure hello. 
-   Użyj podzielonych tabel, gdy jest to konieczne.

## <a name="import-and-export-by-using-mysql-workbench"></a>Importowanie i eksportowanie przy użyciu narzędzia MySQL Workbench
Istnieją dwa sposoby tooexport, a następnie zaimportuj dane w MySQL Workbench. Każdy służy do innych celów. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Dane tabeli eksportować i importować kreatorów z menu kontekstowego przeglądarki obiektów hello
![Kreatorzy MySQL Workbench w menu kontekstowym przeglądarki obiektów hello](./media/concepts-migrate-import-export/p1.png)

Kreatorzy Hello dla tabeli danych obsługuje importowania i eksportowania operacje przy użyciu plików CSV i JSON. Obejmują one kilka opcji konfiguracji, takich jak separatorów, wybór kolumn i wybór kodowania. Można wykonywać każdego kreatora względem lokalne lub zdalne połączonych serwerów MySQL. Akcja importu Hello obejmuje tabeli, kolumny i mapowania typu. 

Dostępne z tych kreatorów z menu kontekstowego przeglądarki obiektów hello, klikając prawym przyciskiem myszy tabelę. Następnie wybierz opcję **Kreatora eksportu danych tabeli** lub **Kreatora importu danych tabeli**. 

#### <a name="table-data-export-wizard"></a>Kreator eksportu danych tabeli
Witaj poniższy przykład eksportuje plik CSV tooa tabeli hello: 
1. Kliknij prawym przyciskiem myszy hello spis toobe bazy danych hello wyeksportowane. 
2. Wybierz **tabeli Kreator eksportu danych**. Wybierz hello kolumn toobe wyeksportowane, przesunięcie wiersza (jeśli istnieje) i count (jeśli istnieje). 
3. Na powitania **wybierz dane do wyeksportowania** kliknij przycisk **dalej**. Wybierz ścieżkę pliku hello, CSV lub JSON typu pliku. Wybierz również hello linii separatora, metody otaczającej ciągów i separator pola. 
4. Na powitania **lokalizacja pliku wyjściowego wybierz** kliknij przycisk **dalej**. 
5. Na powitania **eksportować dane** kliknij przycisk **dalej**.

#### <a name="table-data-import-wizard"></a>Kreator importu tabeli danych
Witaj poniższy przykład importuje hello tabeli z pliku CSV:
1. Kliknij prawym przyciskiem myszy hello spis toobe bazy danych hello zaimportowane. 
2. Wybierz tooand przeglądania hello zaimportowane toobe pliku CSV, a następnie kliknij **dalej**. 
3. Wybierz tabelę docelową hello (nowego lub istniejącego) i hello zaznacz lub usuń zaznaczenie **Truncate table przed rozpoczęciem importowania** pole wyboru. Kliknij przycisk **Dalej**.
4. Wybierz kodowanie i hello toobe kolumn zaimportowane, a następnie kliknij przycisk **dalej**. 
5. Na powitania **importowania danych** kliknij przycisk **dalej**. Kreator Hello odpowiednio importuje hello danych.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>Danych SQL eksportować i importować kreatorów z okienka Navigator hello
Użyj tooexport kreatora lub zaimportować SQL generowane na podstawie MySQL Workbench lub wygenerować hello mysqldump polecenia. Dostęp do tych kreatorów z hello **Nawigator** okienku lub wybierając **serwera** z hello menu głównego. Następnie wybierz **eksportu danych** lub **importowania danych**. 

#### <a name="data-export"></a>Eksportowanie danych
![Eksportowanie danych MySQL Workbench za pomocą okienka Navigator hello](./media/concepts-migrate-import-export/p2.png)

Można użyć hello **eksportu danych** karcie tooexport danych MySQL. 
1. Wybierz każdego schematu, że mają tooexport, opcjonalnie wybierz schematu obiektów/tabel z każdym ze schematów, a Generowanie hello eksportu. Opcje konfiguracji obejmują niezależne SQL pliku lub folderu projektu tooa eksportu, zrzutu procedury składowane i zdarzenia lub pominąć danych tabeli. 
 
   Można również użyć **wyeksportować zestawu wyników** tooexport wynik określonego zestawu w hello SQL Edytor tooanother formacie, na przykład woluminów CSV, JSON, HTML i XML. 
3. Wybierz tooexport obiektów bazy danych hello i skonfiguruj hello powiązane opcje.
4. Kliknij przycisk **Odśwież** tooload hello obiekty.
5. Opcjonalnie można otworzyć hello **zaawansowane opcje** karcie operacji eksportowania hello toorefine. Na przykład dodać blokady tabeli, Zastąp Użyj zamiast instrukcji insert i identyfikatory oferty backtick znaków.
6. Kliknij przycisk **Uruchom eksportowanie** toobegin hello Eksport.


#### <a name="data-import"></a>Importowanie danych
![Importowanie danych Workbench MySQL przy użyciu nawigatora zarządzania](./media/concepts-migrate-import-export/p3.png)

Można użyć hello **importowania danych** karcie tooimport lub Przywróć wyeksportowanych danych z operacji eksportowania danych hello lub hello mysqldump polecenia. 
1. Wybierz folder projektu hello lub niezależnym pliku SQL, wybierz hello tooimport schematu do lub **nowy** toodefine nowego schematu. 
2. Kliknij przycisk **Start zaimportować** procesu importowania hello toobegin.

## <a name="next-steps"></a>Następne kroki
Jako innego sposobu migracji, należy przeczytać [migracji, używając bazy danych MySQL zrzutu i przywrócić w bazie danych Azure dla programu MySQL](concepts-migrate-dump-restore.md). 
