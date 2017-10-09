
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
koszty toosave w przypadku wstrzymania i wznowienia obliczeniowe zasobów na żądanie. Na przykład jeśli nie będzie używać hello bazy danych podczas hello nocy i w weekendy, można wstrzymywać go w tych godzinach i wznawiać jej w ciągu dnia hello. Użytkownik nie zostanie obciążona dla jednostek dwu, podczas hello bazy danych zostało wstrzymane.

Po zatrzymaniu bazy danych:

* Zasoby obliczeniowe i pamięci są zwracane toohello puli zasobów dostępnych w centrum danych hello
* Jednostka DWU koszty są zerowe hello czas trwania pauzy hello.
* Nie wpływa na magazyn danych i danych pozostaje niezmieniona. 
* Usługa SQL Data Warehouse anuluje wszystkie uruchomione lub umieszczonych w kolejce operacji.

