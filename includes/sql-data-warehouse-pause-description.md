
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="394df-101">koszty toosave w przypadku wstrzymania i wznowienia obliczeniowe zasobów na żądanie.</span><span class="sxs-lookup"><span data-stu-id="394df-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="394df-102">Na przykład jeśli nie będzie używać hello bazy danych podczas hello nocy i w weekendy, można wstrzymywać go w tych godzinach i wznawiać jej w ciągu dnia hello.</span><span class="sxs-lookup"><span data-stu-id="394df-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="394df-103">Użytkownik nie zostanie obciążona dla jednostek dwu, podczas hello bazy danych zostało wstrzymane.</span><span class="sxs-lookup"><span data-stu-id="394df-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="394df-104">Po zatrzymaniu bazy danych:</span><span class="sxs-lookup"><span data-stu-id="394df-104">When you pause a database:</span></span>

* <span data-ttu-id="394df-105">Zasoby obliczeniowe i pamięci są zwracane toohello puli zasobów dostępnych w centrum danych hello</span><span class="sxs-lookup"><span data-stu-id="394df-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="394df-106">Jednostka DWU koszty są zerowe hello czas trwania pauzy hello.</span><span class="sxs-lookup"><span data-stu-id="394df-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="394df-107">Nie wpływa na magazyn danych i danych pozostaje niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="394df-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="394df-108">Usługa SQL Data Warehouse anuluje wszystkie uruchomione lub umieszczonych w kolejce operacji.</span><span class="sxs-lookup"><span data-stu-id="394df-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

