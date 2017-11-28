---
title: "aaaAuditing w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="8ecbf-103">Inspekcja w magazynie danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="8ecbf-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ecbf-104">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="8ecbf-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="8ecbf-105">Wykrywanie zagrożeń</span><span class="sxs-lookup"><span data-stu-id="8ecbf-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="8ecbf-106">Inspekcja SQL Data Warehouse pozwala toorecord zdarzenia w dzienniku inspekcji tooan bazy danych na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="8ecbf-107">Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="8ecbf-108">Inspekcja SQL Data Warehouse integruje się również z usługi Microsoft Power BI do przechodzenia raportowania i analiz.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="8ecbf-109">Narzędzia inspekcji Włącz i ułatwienia standardów toocompliance zgodność, ale nie zagwarantuje zgodności.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="8ecbf-110">Aby uzyskać więcej informacji na temat usługi Azure programy tego zgodność ze standardami pomocy technicznej, zobacz hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centrum zaufania Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="8ecbf-111">[Podstawowe informacje dotyczące bazy danych inspekcji]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="8ecbf-112">[Inspekcja bazy danych]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="8ecbf-113">[Analizowanie dzienników inspekcji i raportów]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="8ecbf-114"><a id="subheading-1"></a>Podstawy inspekcja bazy danych magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8ecbf-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="8ecbf-115">Inspekcja bazy danych SQL Data Warehouse umożliwia:</span><span class="sxs-lookup"><span data-stu-id="8ecbf-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="8ecbf-116">**Zachowaj** dziennik inspekcji wybranych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="8ecbf-117">Można zdefiniować rodzaje toobe działania bazy danych inspekcji.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="8ecbf-118">**Raport** na działanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-118">**Report** on database activity.</span></span> <span data-ttu-id="8ecbf-119">Można użyć wstępnie skonfigurowane raporty i tooget pulpitu nawigacyjnego, szybkie wprowadzenie aktywności i raportowanie zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="8ecbf-120">**Analizowanie** raportów.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-120">**Analyze** reports.</span></span> <span data-ttu-id="8ecbf-121">Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="8ecbf-122">Można skonfigurować inspekcję hello następujących kategorii:</span><span class="sxs-lookup"><span data-stu-id="8ecbf-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="8ecbf-123">**Zwykły SQL** i **sparametryzowana SQL** dla których hello dzienników inspekcji zbierane są sklasyfikowane jako</span><span class="sxs-lookup"><span data-stu-id="8ecbf-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="8ecbf-124">**Toodata dostępu**</span><span class="sxs-lookup"><span data-stu-id="8ecbf-124">**Access toodata**</span></span>
* <span data-ttu-id="8ecbf-125">**Zmiany schematu (DDL)**</span><span class="sxs-lookup"><span data-stu-id="8ecbf-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="8ecbf-126">**Zmiany danych (DML)**</span><span class="sxs-lookup"><span data-stu-id="8ecbf-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="8ecbf-127">**Konta, role i uprawnienia (DCL)**</span><span class="sxs-lookup"><span data-stu-id="8ecbf-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="8ecbf-128">**Procedura składowana**, **logowania** i **zarządzania transakcji**.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="8ecbf-129">Dla każdej kategorii zdarzenia inspekcji z **Powodzenie** i **błąd** operacje nie zostały skonfigurowane osobno.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="8ecbf-130">Aby uzyskać więcej informacji na temat hello działań i zdarzeń inspekcji, zobacz hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">odwołanie do formatu dziennika inspekcji (Pobieranie pliku doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="8ecbf-131">Dzienniki inspekcji są przechowywane na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="8ecbf-132">Można zdefiniować okres przechowywania dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="8ecbf-133">Zasady inspekcji mogą być definiowane dla określonej bazy danych lub jako domyślne zasady serwera.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="8ecbf-134">Domyślne zasady inspekcji serwera stosuje tooall baz danych na serwerze, które nie mają określonej bazy danych inspekcji zasad zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="8ecbf-135">Przed przystąpieniem do ustawiania inspekcji inspekcji wyboru, jeśli używasz ["Klientów niższych poziomów."](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="8ecbf-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="8ecbf-136"><a id="subheading-2"></a>Inspekcja bazy danych</span><span class="sxs-lookup"><span data-stu-id="8ecbf-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="8ecbf-137">Uruchamianie hello <a href="https://portal.azure.com" target="_blank">portalu Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="8ecbf-138">Przejdź toohello **ustawienia** bloku hello ma tooaudit usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="8ecbf-139">W hello **ustawienia** bloku, wybierz opcję **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="8ecbf-140">Należy również włączyć inspekcję, klikając hello **ON** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="8ecbf-141">Hello inspekcji blok konfiguracji, wybierz **szczegóły MAGAZYNU** tooopen hello magazynu dzienniki inspekcji bloku.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="8ecbf-142">Wybierz hello kontem magazynu platformy Azure, w którym zostanie zapisany dzienniki i hello okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="8ecbf-143">Witaj Użyj tego samego konta magazynu dla wszystkich baz danych inspekcji hello tooget wykorzystanie hello wstępnie skonfigurowane raporty szablonów.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="8ecbf-144">Kliknij przycisk hello **OK** przycisk toosave hello magazynu szczegóły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="8ecbf-145">W obszarze **rejestrowanie przez zdarzenie**, kliknij przycisk **Powodzenie** i **błąd** toolog wszystkie zdarzenia, lub wybierz kategorie poszczególnych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="8ecbf-146">W przypadku konfigurowania inspekcji bazy danych, może być konieczne parametry połączenia hello tooalter Twojego tooensure klienta, który prawidłowo przechwycone dane inspekcji.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="8ecbf-147">Sprawdź hello [zmodyfikować FDQN serwera w parametrach połączenia hello](sql-data-warehouse-auditing-downlevel-clients.md) tematu dla połączeń klientów niższych poziomów.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="8ecbf-148">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-148">Click **OK**.</span></span>

## <span data-ttu-id="8ecbf-149"><a id="subheading-3"></a>Analizowanie dzienników inspekcji i raportów</span><span class="sxs-lookup"><span data-stu-id="8ecbf-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="8ecbf-150">Dzienniki inspekcji są agregowane w zbiorze magazynu tabel z **SQLDBAuditLogs** prefiks w hello wybrana w Instalatorze kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="8ecbf-151">Można wyświetlić przy użyciu narzędzia, takie jak pliki dziennika <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Eksploratora usługi Storage Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="8ecbf-152">Szablon raportu dotyczącego wstępnie skonfigurowane pulpit nawigacyjny jest dostępny jako <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">arkusz kalkulacyjny programu Excel do pobrania</a> toohelp szybko analizować dane dzienników.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="8ecbf-153">toouse hello szablonu w dziennikach inspekcji, potrzebujesz programu Excel 2013 lub nowszy i dodatku Power Query, który można pobrać <a href="http://www.microsoft.com/download/details.aspx?id=39379">tutaj</a>.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="8ecbf-154">Witaj szablonu w nim fikcyjnej przykładowych danych, i służą do tworzenia dodatku Power Query tooimport dziennik inspekcji bezpośrednio z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="8ecbf-155"><a id="subheading-4"></a>Ponowne generowanie klucza magazynu</span><span class="sxs-lookup"><span data-stu-id="8ecbf-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="8ecbf-156">W środowisku produkcyjnym jest prawdopodobnie toorefresh Twojego magazynu kluczy okresowo.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="8ecbf-157">Podczas odświeżania kluczy, należy toosave hello zasad.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="8ecbf-158">Witaj proces przebiega następująco:</span><span class="sxs-lookup"><span data-stu-id="8ecbf-158">hello process is as follows:</span></span>

1. <span data-ttu-id="8ecbf-159">W hello inspekcji blok konfiguracji (opisane powyżej w Instalatorze hello inspekcji sekcji) Przełącz hello **klucz dostępu do magazynu** z *głównej* za*dodatkowej* i  **ZAPISZ**.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="8ecbf-160">Blok konfiguracji magazynu Przejdź toohello i **ponownie wygenerować** hello *podstawowy klucz dostępu*.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="8ecbf-161">Przejdź wstecz toohello inspekcji bloku konfiguracji przełącznika hello **klucz dostępu do magazynu** z *dodatkowej* za*głównej* i naciśnij klawisz **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="8ecbf-162">Przejdź wstecz magazynu toohello interfejsu użytkownika i **ponownie wygenerować** hello *pomocniczy klucz dostępu* (jako przygotowanie hello klucze następnego odświeżenia cyklu.</span><span class="sxs-lookup"><span data-stu-id="8ecbf-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="8ecbf-163"><a id="subheading-5"></a>Automatyzacja (programu PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="8ecbf-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="8ecbf-164">Można również skonfigurować inspekcji w usłudze Azure SQL Data Warehouse przy użyciu powitania po narzędziami automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="8ecbf-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="8ecbf-165">**Polecenia cmdlet programu PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="8ecbf-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="8ecbf-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="8ecbf-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="8ecbf-168">[Usuń AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="8ecbf-169">[Usuń AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="8ecbf-170">[Zestaw AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="8ecbf-171">[Zestaw AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="8ecbf-172">[Użyj AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="8ecbf-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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