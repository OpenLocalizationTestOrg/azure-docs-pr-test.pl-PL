---
title: aaaManage baz danych Azure SQL Data Warehouse | Dokumentacja firmy Microsoft
description: "Omówienie zarządzania bazami danych magazynu danych SQL. Obejmuje narzędzia do zarządzania, jednostek dwu i wydajność skalowania w poziomie, rozwiązywanie problemów z wydajność zapytań, ustanawiania zasad zabezpieczeń dobrej i przywracanie bazy danych z uszkodzenie danych lub regionalnej awarii."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Zarządzanie bazami danych w magazynie danych SQL Azure
Usługa SQL Data Warehouse automatyzuje wiele aspektów Zarządzanie bazami danych. Na przykład wydajności tooscale tylko muszą tooadjust i opłacać hello prawo poziom zasoby obliczeniowe, a następnie umożliwił SQL Data Warehouse pracy wszystkie hello skalowanie w poziomie oraz skalowanie kopii.

Bez wątpienia można toomonitor Twojego tooidentify obciążenie wydajności musi, a także rozwiązywanie problemów z kwerendami długotrwałe. Należy również tooperform kilka zadań uprawnienia toomanage dla użytkowników i nazwy logowania.

To omówienie dotyczy aspektami zarządzania magazynu danych SQL.

* Narzędzia do zarządzania
* Skalowanie możliwości obliczeniowych
* Wstrzymywanie i wznawianie
* Najlepsze rozwiązania w zakresie wydajności
* Monitorowanie zapytania
* Bezpieczeństwo
* Tworzenie kopii zapasowej i przywracanie

## <a name="management-tools"></a>Narzędzia do zarządzania
Można użyć różnych baz danych toomanage narzędzia w usłudze SQL Data Warehouse. W przypadku zarządzania bazami danych, użytkownik opracuje preferencji narzędzia dla poszczególnych typów zadań należy tooperform.

### <a name="azure-portal"></a>Azure Portal
Witaj [portalu Azure] [ Azure portal] jest oparte na sieci web portalu, gdzie możesz tworzenie, aktualizowanie i usuwanie baz danych i monitorowania zasobów bazy danych. To narzędzie jest doskonałym rozwiązaniem jest po prostu rozpoczniesz pracę z platformą Azure, zarządzanie niewielkiej liczby baz danych magazynu danych, czy należy tooquickly czymś.

tooget wprowadzenie hello portalu Azure, zobacz [Utwórz magazyn danych SQL (Azure portal)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools w programie Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) w programie Visual Studio pozwala tooconnect do zarządzania i tworzenie baz danych. Jeśli jesteś deweloperem zapoznać się z programu Visual Studio lub innych środowisk zintegrowanego rozwoju (IDE), spróbuj użyć narzędzia SSDT w programie Visual Studio.

Program SSDT zawiera hello Eksplorator obiektów programu SQL Server, co pozwala toovisualize, połączenie i wykonywanie skryptów SQL Data Warehouse w przypadku baz danych. tooquickly połączenia tooSQL hurtowni danych, wystarczy kliknąć hello **Otwórz w programie Visual Studio** przycisku w pasku poleceń hello podczas wyświetlania szczegółowych informacji bazy danych hello w hello klasycznego portalu Azure.  

tooget pracę z narzędziami SSDT w programie Visual Studio, zobacz [zapytania magazyn danych SQL Azure z programem Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Narzędzia wiersza polecenia
Narzędzia wiersza polecenia idealnie nadają się do automatyzowania obciążeń.  Środowiska PowerShell i sqlcmd znajdują się dwie tooautomate świetnych sposobów procesów.  Firma Microsoft zaleca tych narzędzi do zarządzania dużą liczbę serwerów logicznych i wdrażanie zmiany zasobów w środowisku produkcyjnym, jak hello zadań niezbędnych mogą być uwzględnione w skryptach i następnie automatycznego.

### <a name="dynamic-management-views"></a>Dynamicznych widoków zarządzania
Widoków DMV są hello chleb i masła zarządzania magazynu danych SQL. Prawie wszystkie informacje, które udostępnia w portalu hello zależy od widoków DMV. toosee listę widoków DMV magazynu danych SQL, zobacz [widoków systemowych SQL Data Warehouse][SQL Data Warehouse system views].

Zobacz tooget pracę, [Connect i zapytania przy użyciu narzędzia sqlcmd][Connect and query with sqlcmd], i [Utwórz bazę danych (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Skalowanie możliwości obliczeniowych
W usłudze SQL Data Warehouse można szybko skalować wydajności lub ponownie według zwiększenie lub zmniejszenie zasoby obliczeniowe procesora CPU, pamięci i przepustowość we/wy. wydajność tooscale toodo wystarczy Dostosuj liczbę hello jednostki magazynu danych (dwu) czy usługi SQL Data Warehouse przydziela tooyour bazy danych. Usługa SQL Data Warehouse szybko ułatwia hello zmienić i obsługuje wszystkie hello podstawowej zmiany toohardware lub oprogramowania.

toolearn więcej informacji na temat skalowania jednostek dwu, zobacz [skalowanie wydajności].

## <a name="pause-and-resume"></a>Wstrzymywanie i wznawianie
koszty toosave w przypadku wstrzymania i wznowienia obliczeniowe zasobów na żądanie. Na przykład jeśli nie będzie używać hello bazy danych podczas hello nocy i w weekendy, można wstrzymywać go w tych godzinach i wznawiać jej w ciągu dnia hello. Użytkownik nie zostanie obciążona dla jednostek dwu, podczas hello bazy danych zostało wstrzymane.

Aby uzyskać więcej informacji, zobacz [wstrzymać obliczeń][Pause compute], i [wznowić operacje obliczeniowe][Resume compute].

## <a name="performance-best-practices"></a>Najlepsze rozwiązania w zakresie wydajności
Wprowadzenie do korzystania z nowej technologii, odnajdywanie hello porady i wskazówki, które działają najlepiej prawo od początku hello można zapisać można bardzo długo.  Najlepsze rozwiązania w całym wiele nasze tematy będą dostępne.

toosee wiele podsumowanie najważniejszych zagadnień hello podczas opracowywania obciążenie, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Monitorowanie zapytania
Czasami kwerendy działa zbyt długo, ale nie ma pewności co hello culprit jest. Magazyn danych SQL ma dynamicznych widoków zarządzania (widoków DMV), których można używać toofigure się, których kwerendy trwa zbyt długo.

toofind długotrwałe zapytań, zobacz [monitorowania obciążenia przy użyciu widoków DMV][Monitor your workload using DMVs].

## <a name="security"></a>Bezpieczeństwo
toomaintain bezpieczny system musi być na powitania alert i chronią przed nieautoryzowanym dostępem dowolnego typu. System zabezpieczeń musi toomake się, że reguły zapory są stosowane tylko autoryzowane adresy IP mogą się łączyć. Musi on odpowiedniego uwierzytelnienia poświadczeń użytkownika. Po podłączeniu toohello bazy danych użytkownika hello użytkownik powinien mieć tylko tooperform uprawnienia minimalnej liczbie czynności. toosecure danych, należy używać szyfrowania. Jest również ważne toohave inspekcji i śledzenia, więc można odtwarzanie zdarzenia, jeśli istnieje wszelkich podejrzanych działań.

toolearn dotyczących zarządzania zabezpieczeniami, head za pośrednictwem toohello [Omówienie zabezpieczeń][Security overview].

## <a name="backup-and-restore"></a>Tworzenie kopii zapasowej i przywracanie
Posiadanie niezawodnej backps danych jest integralną część żadnych produkcyjną bazę danych. Usługa SQL Data Warehouse chroni dane przez automatyczne tworzenie kopii zapasowej active baz danych w regularnych odstępach czasu. Te kopie zapasowe pozwalają toorecover z scenariuszy, w którym uszkodzone dane lub przypadkowo usunięty, danych lub bazy danych.  Witaj harmonogramu tworzenia kopii zapasowej danych, zasad przechowywania i toorestore bazy danych, zobacz temat [Przywracanie z migawki][Restore from snapshot].

## <a name="next-steps"></a>Następne kroki
Za pomocą zasady projektowania dobrej bazy danych, spowoduje to łatwiejsze toomanage baz danych w usłudze SQL Data Warehouse. toolearn więcej, head za pośrednictwem toohello [omówienie tworzenia][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[skalowanie wydajności]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
