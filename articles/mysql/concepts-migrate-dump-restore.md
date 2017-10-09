---
title: "aaaMigrate użyciu bazy danych MySQL zrzutu i przywrócić w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano dwie typowe sposoby tooback zapasowej i przywracania bazy danych, w bazie danych Azure dla programu MySQL, za pomocą narzędzi, takich jak mysqldump, MySQL Workbench i PHPMyAdmin."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>Migrowanie tooAzure bazy danych programu MySQL bazy danych dla programu MySQL przy użyciu zrzutu i przywracania
W tym artykule opisano dwa tooback typowe sposoby zapasowej i przywracanie baz danych w bazie danych Azure dla programu MySQL
- Zrzut i przywrócenie z hello wiersza polecenia, (przy użyciu mysqldump) 
- Zrzut i przywracania przy użyciu PHPMyAdmin 

## <a name="before-you-begin"></a>Przed rozpoczęciem
toostep za pośrednictwem tego jak tooguide, należy toohave:
- [Tworzenie bazy danych platformy Azure dla serwera MySQL - portalu Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html) na komputerze zainstalowano narzędzia wiersza polecenia.
- MySQL Workbench [Pobierz Workbench MySQL](https://dev.mysql.com/downloads/workbench/), Toad, Navicat lub innych firm MySQL narzędzia toodo zrzutu i przywrócić polecenia.

## <a name="use-common-tools"></a>Użyj standardowych narzędzi
Użyj typowych narzędzi i narzędzi, takich jak MySQL Workbench, mysqldump, Toad lub Navicat tooremotely połączenia i przywracania danych do bazy danych Azure dla programu MySQL. Narzędzia takie na komputerze klienckim z toohello tooconnect połączenia internetowego bazy danych platformy Azure dla programu MySQL. Połączenie SSL zaszyfrowane za pomocą najlepsze rozwiązania w zakresie zabezpieczeń, zobacz też [łączności Konfigurowanie protokołu SSL w bazie danych Azure dla programu MySQL](concepts-ssl-connection-security.md). Nie trzeba toomove hello zrzutu pliki tooany specjalne chmury lokalizacji podczas migracji tooAzure bazy danych dla programu MySQL. 

## <a name="common-uses-for-dump-and-restore"></a>Typowe zastosowania zrzutu i przywracania
Możesz użyć narzędzia MySQL przykład mysqldump i mysqlpump toodump i obciążenia bazy danych do bazy danych MySQL na platformie Azure w kilka typowych scenariuszy. W innych sytuacjach może używać hello [importowanie i eksportowanie](concepts-migrate-import-export.md) zamiast tego podejścia.

- Użyj bazy danych zrzuty podczas migrowania hello całej bazy danych. To zalecenie posiada podczas przenoszenia dużych ilości danych MySQL, gdy ma być toominimize przerw w witrynach lub aplikacjach. 
-  Upewnij się, że wszystkie tabele w bazie danych hello użyć aparatu magazynu InnoDB hello podczas ładowania danych do bazy danych platformy Azure dla programu MySQL. Bazy danych platformy Azure dla programu MySQL obsługuje tylko aparatu magazynu InnoDB i dlatego nie obsługuje aparaty alternatywnych magazynu. Skonfigurowanie tabel z innych aparatów magazynu przekonwertować je na format aparatu InnoDB hello przed tooAzure migracji bazy danych dla programu MySQL.
   Na przykład jeśli masz WordPress lub aplikacji sieci Web przy użyciu tabel MyISAM hello, najpierw przekonwertuj te tabele przy użyciu funkcji migracji do formatu InnoDB przed przywróceniem tooAzure bazy danych dla programu MySQL. Użycie klauzuli hello `ENGINE=InnoDB` tooset hello aparat używany podczas tworzenia nowej tabeli, a następnie przenieść hello dane do tabeli zgodne hello przed przywróceniem hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- tooavoid zgodności wszelkie problemy, upewnij się, hello tę samą wersję programu MySQL jest używany w systemach źródłowych i docelowych hello, gdy zrzucanie baz danych. Na przykład jeśli istniejący serwer MySQL jest w wersji 5.7, następnie należy zmigrować tooAzure bazy danych MySQL skonfigurowane toorun wersji 5.7. Witaj `mysql_upgrade` polecenie nie działa w bazie danych Azure MySQL serwera i nie jest obsługiwany. Jeśli potrzebujesz tooupgrade między wersjami MySQL, najpierw zrzutu lub wyeksportować niższe wersji bazy danych do nowszej wersji programu MySQL we własnym środowisku. Następnie uruchom `mysql_upgrade`, przed podjęciem próby wykonania migracji w bazie danych programu Azure dla programu MySQL.

## <a name="performance-considerations"></a>Zagadnienia dotyczące wydajności
wydajność toooptimize, odbioru powiadomienia o te zagadnienia dotyczące zrzucanie dużych baz danych:
-   Użyj hello `exclude-triggers` opcji w mysqldump podczas zrzucanie baz danych. Wyklucz wyzwalaczy wyzwalania podczas przywracania danych hello zrzutu pliki tooavoid hello wyzwalacza poleceń. 
-   Unikaj hello `single-transaction` opcji w mysqldump podczas zrzucanie bardzo dużych baz danych. Zrzucanie wiele tabel w ramach jednej transakcji powoduje dodatkowe miejsce do magazynowania i toobe zasoby pamięci używane podczas przywracania i może powodować opóźnienia wydajności lub ograniczenia zasobów.
-   Wstawia wielowartościowych używany podczas ładowania z koszty wykonywania instrukcji SQL w toominimize, gdy zrzucanie baz danych. Podczas korzystania z plików zrzutu wygenerowany przez narzędzie mysqldump, wstawia wielowartościowe są domyślnie włączone. 
-  Użyj hello `order-by-primary` opcji w mysqldump podczas zrzucanie baz danych, dzięki czemu dane hello jest tworzone w kolejności klucza podstawowego.
-   Użyj hello `disable-keys` opcji w mysqldump podczas zrzucanie danych, toodisable ograniczeń klucza obcego przed obciążenia. Wyłączenie sprawdzania klucza obcego umożliwia zwiększenie wydajności. Włącz ograniczenia hello i zweryfikować danych na powitania po hello integralności referencyjnej tooensure obciążenia.
-   Użyj podzielonych tabel, gdy jest to konieczne.
-   Ładowanie danych równolegle. Należy unikać zbyt dużo równoległości, które mogłyby spowodować toohit limit zasobów i monitorowanie zasobów przy użyciu metryk hello dostępne w portalu Azure hello. 
-   Użyj hello `defer-table-indexes` opcji w mysqlpump podczas zrzucanie baz danych, dzięki temu tworzenie indeksów odbywa się po załadowaniu danych tabel.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Utworzenie pliku kopii zapasowej z hello wiersza polecenia przy użyciu mysqldump
tooback zapasową istniejącej bazy danych MySQL na lokalne powitania serwera lokalnego lub na maszynie wirtualnej, uruchom następujące polecenia hello: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

tooprovide parametry Hello są:
- [uname] Nazwa użytkownika bazy danych 
- [hasło] hello hasło dla bazy danych (należy pamiętać, nie bez spacji między -p i hello hasła) 
- [dbname] hello Nazwa bazy danych 
- [backupfile.sql] hello nazwę pliku kopii zapasowej bazy danych 
- [--opt] hello mysqldump opcji 

Na przykład tooback bazę danych o nazwie "programu testdb" na serwerze MySQL z hello username "testuser" i nie testdb_backup.sql pliku tooa hasła, użyj następującego polecenia hello. Hello polecenie tworzy kopię zapasową hello `testdb` bazy danych w pliku o nazwie `testdb_backup.sql`, który zawiera wszystkie instrukcje SQL hello potrzebne toore — tworzenie hello bazy danych. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect określonych tabel w Twojej tooback bazy danych w górę, nazwy tabeli hello listy rozdzielone spacjami. Na przykład tooback tylko tabel table1 i table2 z hello "programu testdb", należy wykonać w tym przykładzie: 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

Przełącz się tooback więcej niż jednej bazy danych jednocześnie, użyj hello — bazy danych i nazwy bazy danych hello listy rozdzielone spacjami. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback zapasową wszystkich baz danych hello powitania serwera w tym samym czasie, należy użyć hello — bazy danych wszystkich opcji.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>Utwórz bazę danych w celu hello Azure bazy danych MySQL serwera
Utwórz pustą bazę danych w celu hello Azure bazy danych dla serwera MySQL, gdzie chcesz toomigrate hello dane. Za pomocą narzędzia, takie jak bazy danych hello toocreate MySQL Workbench, Toad lub Navicat. Witaj baza danych może mieć takie same nazwy co baza danych hello, ilości danych zawartych w niej hello utworzyć zrzutu hello lub utworzysz bazę danych pod inną nazwą.

połączone tooget, Znajdź informacje o połączeniu hello na stronie właściwości hello w bazie danych Azure dla programu MySQL.
![Informacje dotyczące połączenia hello w hello portalu Azure](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

Dodaj informacje o połączeniu hello do środowiska roboczego programu MySQL.
![Parametry połączenia MySQL Workbench](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>Przywracanie bazy danych MySQL przy użyciu wiersza polecenia lub MySQL Workbench
Po utworzeniu hello docelowej bazy danych, można użyć polecenia mysql hello lub MySQL Workbench toorestore hello danych do określonych hello nowo utworzone bazy danych na podstawie pliku zrzutu hello.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
W tym przykładzie należy przywrócić dane hello na powitania nowo utworzone bazy danych w celu hello Azure bazy danych dla serwera MySQL.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>Eksportowanie przy użyciu PHPMyAdmin
tooexport, możesz użyć typowych phpMyAdmin narzędzie hello, które mogą już zainstalowano lokalnie w danym środowisku. tooexport bazy danych MySQL przy użyciu PHPMyAdmin:
- Otwórz phpMyAdmin.
- Wybierz bazę danych. Kliknij nazwę bazy danych hello liście hello powitania po lewej stronie. 
- Kliknij przycisk hello **wyeksportować** łącza. Nowa strona zostanie wyświetlona zrzutu hello tooview bazy danych.
- W hello obszaru eksportu kliknij hello **Zaznacz wszystko** toochoose hello tabele w bazie danych. 
- W hello obszaru Opcje SQL kliknij odpowiednie opcje hello. 
- Kliknij przycisk hello **zapisać jako plik** opcja i odpowiedniej kompresji hello opcji, a następnie kliknij przycisk hello **Przejdź** przycisku. Okno dialogowe powinna zostać wyświetlona sygnalizowania możesz toosave hello plik lokalnie.

## <a name="import-using-phpmyadmin"></a>Import za pomocą PHPMyAdmin
Importowanie bazy danych jest tooexporting podobne. Witaj następujących czynności:
- Otwórz phpMyAdmin. 
- Na stronie Ustawienia phpMyAdmin powitania kliknij **Dodaj** tooadd MySQL serwera bazy danych platformy Azure. Podaj szczegóły połączenia hello i informacji o logowaniu.
- Utwórz bazę danych o odpowiedniej nazwie i zaznacz go po lewej stronie powitania hello ekranu. toorewrite hello istniejącej bazy danych, kliknij nazwę bazy danych hello, wybierz wszystkie hello pola wyboru obok nazwy tabel hello i wybierz **porzucić** toodelete hello istniejące tabele. 
- Kliknij przycisk hello **SQL** łącze tooshow hello strony gdzie można wpisać w poleceniach SQL, lub Przekaż plik programu SQL. 
- Użyj hello **Przeglądaj** pliku bazy danych hello toofind przycisku. 
- Kliknij przycisk hello **Przejdź** przycisk tooexport hello tworzenia kopii zapasowej, wykonania polecenia SQL hello i ponownie utworzyć bazę danych.

## <a name="next-steps"></a>Następne kroki
[Łączenie aplikacji tooAzure bazy danych dla programu MySQL](./howto-connection-string.md)
