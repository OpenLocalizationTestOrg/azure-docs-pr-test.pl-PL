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
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="6cecd-104">Zarządzanie bazami danych w magazynie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6cecd-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="6cecd-105">Usługa SQL Data Warehouse automatyzuje wiele aspektów Zarządzanie bazami danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="6cecd-106">Na przykład wydajności tooscale tylko muszą tooadjust i opłacać hello prawo poziom zasoby obliczeniowe, a następnie umożliwił SQL Data Warehouse pracy wszystkie hello skalowanie w poziomie oraz skalowanie kopii.</span><span class="sxs-lookup"><span data-stu-id="6cecd-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="6cecd-107">Bez wątpienia można toomonitor Twojego tooidentify obciążenie wydajności musi, a także rozwiązywanie problemów z kwerendami długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="6cecd-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="6cecd-108">Należy również tooperform kilka zadań uprawnienia toomanage dla użytkowników i nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="6cecd-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="6cecd-109">To omówienie dotyczy aspektami zarządzania magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6cecd-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="6cecd-110">Narzędzia do zarządzania</span><span class="sxs-lookup"><span data-stu-id="6cecd-110">Management tools</span></span>
* <span data-ttu-id="6cecd-111">Skalowanie możliwości obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="6cecd-111">Scale Compute</span></span>
* <span data-ttu-id="6cecd-112">Wstrzymywanie i wznawianie</span><span class="sxs-lookup"><span data-stu-id="6cecd-112">Pause and Resume</span></span>
* <span data-ttu-id="6cecd-113">Najlepsze rozwiązania w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="6cecd-113">Performance Best Practices</span></span>
* <span data-ttu-id="6cecd-114">Monitorowanie zapytania</span><span class="sxs-lookup"><span data-stu-id="6cecd-114">Query Monitoring</span></span>
* <span data-ttu-id="6cecd-115">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="6cecd-115">Security</span></span>
* <span data-ttu-id="6cecd-116">Tworzenie kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="6cecd-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="6cecd-117">Narzędzia do zarządzania</span><span class="sxs-lookup"><span data-stu-id="6cecd-117">Management tools</span></span>
<span data-ttu-id="6cecd-118">Można użyć różnych baz danych toomanage narzędzia w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6cecd-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="6cecd-119">W przypadku zarządzania bazami danych, użytkownik opracuje preferencji narzędzia dla poszczególnych typów zadań należy tooperform.</span><span class="sxs-lookup"><span data-stu-id="6cecd-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6cecd-120">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6cecd-120">Azure portal</span></span>
<span data-ttu-id="6cecd-121">Witaj [portalu Azure] [ Azure portal] jest oparte na sieci web portalu, gdzie możesz tworzenie, aktualizowanie i usuwanie baz danych i monitorowania zasobów bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="6cecd-122">To narzędzie jest doskonałym rozwiązaniem jest po prostu rozpoczniesz pracę z platformą Azure, zarządzanie niewielkiej liczby baz danych magazynu danych, czy należy tooquickly czymś.</span><span class="sxs-lookup"><span data-stu-id="6cecd-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="6cecd-123">tooget wprowadzenie hello portalu Azure, zobacz [Utwórz magazyn danych SQL (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="6cecd-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="6cecd-124">SQL Server Data Tools w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6cecd-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="6cecd-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) w programie Visual Studio pozwala tooconnect do zarządzania i tworzenie baz danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="6cecd-126">Jeśli jesteś deweloperem zapoznać się z programu Visual Studio lub innych środowisk zintegrowanego rozwoju (IDE), spróbuj użyć narzędzia SSDT w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6cecd-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="6cecd-127">Program SSDT zawiera hello Eksplorator obiektów programu SQL Server, co pozwala toovisualize, połączenie i wykonywanie skryptów SQL Data Warehouse w przypadku baz danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="6cecd-128">tooquickly połączenia tooSQL hurtowni danych, wystarczy kliknąć hello **Otwórz w programie Visual Studio** przycisku w pasku poleceń hello podczas wyświetlania szczegółowych informacji bazy danych hello w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6cecd-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="6cecd-129">tooget pracę z narzędziami SSDT w programie Visual Studio, zobacz [zapytania magazyn danych SQL Azure z programem Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6cecd-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="6cecd-130">Narzędzia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="6cecd-130">Command-line tools</span></span>
<span data-ttu-id="6cecd-131">Narzędzia wiersza polecenia idealnie nadają się do automatyzowania obciążeń.</span><span class="sxs-lookup"><span data-stu-id="6cecd-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="6cecd-132">Środowiska PowerShell i sqlcmd znajdują się dwie tooautomate świetnych sposobów procesów.</span><span class="sxs-lookup"><span data-stu-id="6cecd-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="6cecd-133">Firma Microsoft zaleca tych narzędzi do zarządzania dużą liczbę serwerów logicznych i wdrażanie zmiany zasobów w środowisku produkcyjnym, jak hello zadań niezbędnych mogą być uwzględnione w skryptach i następnie automatycznego.</span><span class="sxs-lookup"><span data-stu-id="6cecd-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="6cecd-134">Dynamicznych widoków zarządzania</span><span class="sxs-lookup"><span data-stu-id="6cecd-134">Dynamic management views</span></span>
<span data-ttu-id="6cecd-135">Widoków DMV są hello chleb i masła zarządzania magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6cecd-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="6cecd-136">Prawie wszystkie informacje, które udostępnia w portalu hello zależy od widoków DMV.</span><span class="sxs-lookup"><span data-stu-id="6cecd-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="6cecd-137">toosee listę widoków DMV magazynu danych SQL, zobacz [widoków systemowych SQL Data Warehouse][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="6cecd-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="6cecd-138">Zobacz tooget pracę, [Connect i zapytania przy użyciu narzędzia sqlcmd][Connect and query with sqlcmd], i [Utwórz bazę danych (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="6cecd-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="6cecd-139">Skalowanie możliwości obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="6cecd-139">Scale compute</span></span>
<span data-ttu-id="6cecd-140">W usłudze SQL Data Warehouse można szybko skalować wydajności lub ponownie według zwiększenie lub zmniejszenie zasoby obliczeniowe procesora CPU, pamięci i przepustowość we/wy.</span><span class="sxs-lookup"><span data-stu-id="6cecd-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="6cecd-141">wydajność tooscale toodo wystarczy Dostosuj liczbę hello jednostki magazynu danych (dwu) czy usługi SQL Data Warehouse przydziela tooyour bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="6cecd-142">Usługa SQL Data Warehouse szybko ułatwia hello zmienić i obsługuje wszystkie hello podstawowej zmiany toohardware lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="6cecd-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="6cecd-143">toolearn więcej informacji na temat skalowania jednostek dwu, zobacz [skalowanie wydajności].</span><span class="sxs-lookup"><span data-stu-id="6cecd-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="6cecd-144">Wstrzymywanie i wznawianie</span><span class="sxs-lookup"><span data-stu-id="6cecd-144">Pause and resume</span></span>
<span data-ttu-id="6cecd-145">koszty toosave w przypadku wstrzymania i wznowienia obliczeniowe zasobów na żądanie.</span><span class="sxs-lookup"><span data-stu-id="6cecd-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="6cecd-146">Na przykład jeśli nie będzie używać hello bazy danych podczas hello nocy i w weekendy, można wstrzymywać go w tych godzinach i wznawiać jej w ciągu dnia hello.</span><span class="sxs-lookup"><span data-stu-id="6cecd-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="6cecd-147">Użytkownik nie zostanie obciążona dla jednostek dwu, podczas hello bazy danych zostało wstrzymane.</span><span class="sxs-lookup"><span data-stu-id="6cecd-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="6cecd-148">Aby uzyskać więcej informacji, zobacz [wstrzymać obliczeń][Pause compute], i [wznowić operacje obliczeniowe][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="6cecd-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="6cecd-149">Najlepsze rozwiązania w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="6cecd-149">Performance Best Practices</span></span>
<span data-ttu-id="6cecd-150">Wprowadzenie do korzystania z nowej technologii, odnajdywanie hello porady i wskazówki, które działają najlepiej prawo od początku hello można zapisać można bardzo długo.</span><span class="sxs-lookup"><span data-stu-id="6cecd-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="6cecd-151">Najlepsze rozwiązania w całym wiele nasze tematy będą dostępne.</span><span class="sxs-lookup"><span data-stu-id="6cecd-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="6cecd-152">toosee wiele podsumowanie najważniejszych zagadnień hello podczas opracowywania obciążenie, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="6cecd-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="6cecd-153">Monitorowanie zapytania</span><span class="sxs-lookup"><span data-stu-id="6cecd-153">Query Monitoring</span></span>
<span data-ttu-id="6cecd-154">Czasami kwerendy działa zbyt długo, ale nie ma pewności co hello culprit jest.</span><span class="sxs-lookup"><span data-stu-id="6cecd-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="6cecd-155">Magazyn danych SQL ma dynamicznych widoków zarządzania (widoków DMV), których można używać toofigure się, których kwerendy trwa zbyt długo.</span><span class="sxs-lookup"><span data-stu-id="6cecd-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="6cecd-156">toofind długotrwałe zapytań, zobacz [monitorowania obciążenia przy użyciu widoków DMV][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="6cecd-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="6cecd-157">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="6cecd-157">Security</span></span>
<span data-ttu-id="6cecd-158">toomaintain bezpieczny system musi być na powitania alert i chronią przed nieautoryzowanym dostępem dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="6cecd-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="6cecd-159">System zabezpieczeń musi toomake się, że reguły zapory są stosowane tylko autoryzowane adresy IP mogą się łączyć.</span><span class="sxs-lookup"><span data-stu-id="6cecd-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="6cecd-160">Musi on odpowiedniego uwierzytelnienia poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6cecd-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="6cecd-161">Po podłączeniu toohello bazy danych użytkownika hello użytkownik powinien mieć tylko tooperform uprawnienia minimalnej liczbie czynności.</span><span class="sxs-lookup"><span data-stu-id="6cecd-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="6cecd-162">toosecure danych, należy używać szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="6cecd-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="6cecd-163">Jest również ważne toohave inspekcji i śledzenia, więc można odtwarzanie zdarzenia, jeśli istnieje wszelkich podejrzanych działań.</span><span class="sxs-lookup"><span data-stu-id="6cecd-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="6cecd-164">toolearn dotyczących zarządzania zabezpieczeniami, head za pośrednictwem toohello [Omówienie zabezpieczeń][Security overview].</span><span class="sxs-lookup"><span data-stu-id="6cecd-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="6cecd-165">Tworzenie kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="6cecd-165">Backup and restore</span></span>
<span data-ttu-id="6cecd-166">Posiadanie niezawodnej backps danych jest integralną część żadnych produkcyjną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="6cecd-167">Usługa SQL Data Warehouse chroni dane przez automatyczne tworzenie kopii zapasowej active baz danych w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="6cecd-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="6cecd-168">Te kopie zapasowe pozwalają toorecover z scenariuszy, w którym uszkodzone dane lub przypadkowo usunięty, danych lub bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6cecd-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="6cecd-169">Witaj harmonogramu tworzenia kopii zapasowej danych, zasad przechowywania i toorestore bazy danych, zobacz temat [Przywracanie z migawki][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="6cecd-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cecd-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6cecd-170">Next steps</span></span>
<span data-ttu-id="6cecd-171">Za pomocą zasady projektowania dobrej bazy danych, spowoduje to łatwiejsze toomanage baz danych w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6cecd-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="6cecd-172">toolearn więcej, head za pośrednictwem toohello [omówienie tworzenia][Development overview].</span><span class="sxs-lookup"><span data-stu-id="6cecd-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

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
