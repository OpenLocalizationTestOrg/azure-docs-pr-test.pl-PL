---
title: "Inspekcji w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do inspekcji w usłudze Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="39a69-103">Inspekcja w magazynie danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="39a69-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39a69-104">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="39a69-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="39a69-105">Wykrywanie zagrożeń</span><span class="sxs-lookup"><span data-stu-id="39a69-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="39a69-106">Inspekcja SQL Data Warehouse pozwala do rekordu dziennika zdarzeń w bazie danych inspekcji na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="39a69-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="39a69-107">Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="39a69-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="39a69-108">Inspekcja SQL Data Warehouse integruje się również z usługi Microsoft Power BI do przechodzenia raportowania i analiz.</span><span class="sxs-lookup"><span data-stu-id="39a69-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="39a69-109">Narzędzia inspekcji włączyć i ułatwienia przestrzeganie standardów zgodności, ale nie gwarantuje się zgodności.</span><span class="sxs-lookup"><span data-stu-id="39a69-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="39a69-110">Aby uzyskać więcej informacji na temat usługi Azure programy tego zgodność ze standardami pomocy technicznej, zobacz <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centrum zaufania Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="39a69-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="39a69-111">[Podstawowe informacje dotyczące bazy danych inspekcji]</span><span class="sxs-lookup"><span data-stu-id="39a69-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="39a69-112">[Inspekcja bazy danych]</span><span class="sxs-lookup"><span data-stu-id="39a69-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="39a69-113">[Analizowanie dzienników inspekcji i raportów]</span><span class="sxs-lookup"><span data-stu-id="39a69-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="39a69-114"><a id="subheading-1"></a>Podstawy inspekcja bazy danych magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="39a69-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="39a69-115">Inspekcja bazy danych SQL Data Warehouse umożliwia:</span><span class="sxs-lookup"><span data-stu-id="39a69-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="39a69-116">**Zachowaj** dziennik inspekcji wybranych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="39a69-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="39a69-117">Można zdefiniować kategorie działań przeprowadzać inspekcję bazy danych.</span><span class="sxs-lookup"><span data-stu-id="39a69-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="39a69-118">**Raport** na działanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="39a69-118">**Report** on database activity.</span></span> <span data-ttu-id="39a69-119">Wstępnie skonfigurowane raporty i pulpit nawigacyjny umożliwia szybkie rozpoczęcie pracy z aktywności i raportowanie zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="39a69-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="39a69-120">**Analizowanie** raportów.</span><span class="sxs-lookup"><span data-stu-id="39a69-120">**Analyze** reports.</span></span> <span data-ttu-id="39a69-121">Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.</span><span class="sxs-lookup"><span data-stu-id="39a69-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="39a69-122">Można skonfigurować inspekcji w ramach następujących kategorii zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="39a69-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="39a69-123">**Zwykły SQL** i **sparametryzowana SQL** dla którego dzienników inspekcji zbierane są sklasyfikowane jako</span><span class="sxs-lookup"><span data-stu-id="39a69-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="39a69-124">**Dostęp do danych**</span><span class="sxs-lookup"><span data-stu-id="39a69-124">**Access to data**</span></span>
* <span data-ttu-id="39a69-125">**Zmiany schematu (DDL)**</span><span class="sxs-lookup"><span data-stu-id="39a69-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="39a69-126">**Zmiany danych (DML)**</span><span class="sxs-lookup"><span data-stu-id="39a69-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="39a69-127">**Konta, role i uprawnienia (DCL)**</span><span class="sxs-lookup"><span data-stu-id="39a69-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="39a69-128">**Procedura składowana**, **logowania** i **zarządzania transakcji**.</span><span class="sxs-lookup"><span data-stu-id="39a69-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="39a69-129">Dla każdej kategorii zdarzenia inspekcji z **Powodzenie** i **błąd** operacje nie zostały skonfigurowane osobno.</span><span class="sxs-lookup"><span data-stu-id="39a69-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="39a69-130">Aby uzyskać więcej informacji dotyczących działań i zdarzeń inspekcji, zobacz <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">odwołanie do formatu dziennika inspekcji (Pobieranie pliku doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="39a69-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="39a69-131">Dzienniki inspekcji są przechowywane na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="39a69-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="39a69-132">Można zdefiniować okres przechowywania dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="39a69-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="39a69-133">Zasady inspekcji mogą być definiowane dla określonej bazy danych lub jako domyślne zasady serwera.</span><span class="sxs-lookup"><span data-stu-id="39a69-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="39a69-134">Domyślne zasady inspekcji serwera ma zastosowanie do wszystkich baz danych na serwerze, które nie mają określonej bazy danych inspekcji zasad zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="39a69-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="39a69-135">Przed przystąpieniem do ustawiania inspekcji inspekcji wyboru, jeśli używasz ["Klientów niższych poziomów."](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="39a69-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="39a69-136"><a id="subheading-2"></a>Inspekcja bazy danych</span><span class="sxs-lookup"><span data-stu-id="39a69-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="39a69-137">Uruchom <a href="https://portal.azure.com" target="_blank">portalu Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="39a69-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="39a69-138">Przejdź do **ustawienia** bloku inspekcji ma usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="39a69-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="39a69-139">W **ustawienia** bloku, wybierz opcję **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="39a69-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="39a69-140">Należy również włączyć inspekcję, klikając **ON** przycisku.</span><span class="sxs-lookup"><span data-stu-id="39a69-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="39a69-141">W bloku inspekcji konfiguracji, wybierz **szczegóły MAGAZYNU** aby otworzyć blok magazyn dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="39a69-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="39a69-142">Wybierz konto magazynu Azure, w którym zostanie zapisany dzienniki i okres przechowywania.</span><span class="sxs-lookup"><span data-stu-id="39a69-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="39a69-143">Użyj tego samego konta magazynu dla wszystkich baz danych inspekcji na maksymalne wykorzystanie szablonów wstępnie skonfigurowane raporty.</span><span class="sxs-lookup"><span data-stu-id="39a69-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="39a69-144">Kliknij przycisk **OK** przycisk, aby zapisać konfigurację szczegóły magazynu.</span><span class="sxs-lookup"><span data-stu-id="39a69-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="39a69-145">W obszarze **rejestrowanie przez zdarzenie**, kliknij przycisk **Powodzenie** i **błąd** do rejestrowania wszystkich zdarzeń lub wybierz kategorie poszczególnych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="39a69-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="39a69-146">W przypadku konfigurowania inspekcji bazy danych, może być konieczne zmienić parametry połączenia klientowi upewnij się, że poprawnie przechwycone dane inspekcji.</span><span class="sxs-lookup"><span data-stu-id="39a69-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="39a69-147">Sprawdź [zmodyfikować FDQN serwera w parametrach połączenia](sql-data-warehouse-auditing-downlevel-clients.md) tematu dla połączeń klientów niższych poziomów.</span><span class="sxs-lookup"><span data-stu-id="39a69-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="39a69-148">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="39a69-148">Click **OK**.</span></span>

## <span data-ttu-id="39a69-149"><a id="subheading-3"></a>Analizowanie dzienników inspekcji i raportów</span><span class="sxs-lookup"><span data-stu-id="39a69-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="39a69-150">Dzienniki inspekcji są agregowane w zbiorze magazynu tabel z **SQLDBAuditLogs** prefiks na koncie magazynu Azure wybrana w Instalatorze.</span><span class="sxs-lookup"><span data-stu-id="39a69-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="39a69-151">Można wyświetlić przy użyciu narzędzia, takie jak pliki dziennika <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Eksploratora usługi Storage Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="39a69-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="39a69-152">Szablon raportu dotyczącego wstępnie skonfigurowane pulpit nawigacyjny jest dostępny jako <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">arkusz kalkulacyjny programu Excel do pobrania</a> ułatwiają szybkie analizowanie danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="39a69-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="39a69-153">Aby użyć szablonu w dziennikach inspekcji, należy Excel 2013 lub nowszy i dodatku Power Query, który można pobrać <a href="http://www.microsoft.com/download/details.aspx?id=39379">tutaj</a>.</span><span class="sxs-lookup"><span data-stu-id="39a69-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="39a69-154">Szablon ma fikcyjnej przykładowe dane w nim, a dodatku Power Query można skonfigurować do zaimportowania dziennik inspekcji bezpośrednio z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39a69-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="39a69-155"><a id="subheading-4"></a>Ponowne generowanie klucza magazynu</span><span class="sxs-lookup"><span data-stu-id="39a69-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="39a69-156">W środowisku produkcyjnym najprawdopodobniej będzie okresowo Odśwież kluczy magazynu.</span><span class="sxs-lookup"><span data-stu-id="39a69-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="39a69-157">Podczas odświeżania kluczy, należy zapisać zasady.</span><span class="sxs-lookup"><span data-stu-id="39a69-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="39a69-158">Proces przebiega w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="39a69-158">The process is as follows:</span></span>

1. <span data-ttu-id="39a69-159">W bloku konfiguracji inspekcji (opisany wyżej w ustawieniach inspekcji sekcji) Przełącz **klucz dostępu do magazynu** z *głównej* do *dodatkowej* i **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="39a69-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="39a69-160">Przejdź do bloku konfiguracji magazynu i **ponownie wygenerować** *podstawowy klucz dostępu*.</span><span class="sxs-lookup"><span data-stu-id="39a69-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="39a69-161">Wróć do bloku konfiguracji inspekcji, Przełącz **klucz dostępu do magazynu** z *dodatkowej* do *głównej* i naciśnij klawisz **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="39a69-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="39a69-162">Wróć do magazynu interfejsu użytkownika i **ponownie wygenerować** *pomocniczy klucz dostępu* (jako przygotowania do następnej klucze odświeżania w tle.</span><span class="sxs-lookup"><span data-stu-id="39a69-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="39a69-163"><a id="subheading-5"></a>Automatyzacja (programu PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="39a69-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="39a69-164">Można również skonfigurować inspekcji w usłudze Azure SQL Data Warehouse przy użyciu następujących narzędzi automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="39a69-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="39a69-165">**Polecenia cmdlet programu PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="39a69-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="39a69-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="39a69-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="39a69-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="39a69-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="39a69-168">[Usuń AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="39a69-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="39a69-169">[Usuń AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="39a69-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="39a69-170">[Zestaw AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="39a69-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="39a69-171">[Zestaw AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="39a69-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="39a69-172">[Użyj AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="39a69-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Podstawowe informacje dotyczące bazy danych inspekcji]: #subheading-1
[Inspekcja bazy danych]: #subheading-2
[Analizowanie dzienników inspekcji i raportów]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy