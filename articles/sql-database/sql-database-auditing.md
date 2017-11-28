---
title: Rozpoczynanie pracy z inspekcji bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: Rozpoczynanie pracy z inspekcji bazy danych Azure SQL
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="78842-103">Rozpoczynanie pracy z inspekcją bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="78842-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="78842-104">Usługa Azure SQL database auditing śledzi zdarzenia bazy danych i zapisuje je inspekcji logowania na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="78842-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="78842-105">Inspekcja również:</span><span class="sxs-lookup"><span data-stu-id="78842-105">Auditing also:</span></span>

* <span data-ttu-id="78842-106">Pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="78842-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="78842-107">Włącza i ułatwia przestrzeganie standardów zgodności, mimo że nie gwarantuje zgodności.</span><span class="sxs-lookup"><span data-stu-id="78842-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="78842-108">Aby uzyskać więcej informacji na temat usługi Azure programy tego zgodność ze standardami pomocy technicznej, zobacz [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="78842-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="78842-109"><a id="subheading-1"></a>Omówienie inspekcji Azure bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="78842-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="78842-110">Program SQL inspekcji bazy danych:</span><span class="sxs-lookup"><span data-stu-id="78842-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="78842-111">**Zachowaj** dziennik inspekcji wybranych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="78842-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="78842-112">Można zdefiniować kategorie działań przeprowadzać inspekcję bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78842-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="78842-113">**Raport** na działanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78842-113">**Report** on database activity.</span></span> <span data-ttu-id="78842-114">Wstępnie skonfigurowane raporty i pulpit nawigacyjny umożliwia szybkie rozpoczęcie pracy z aktywności i raportowanie zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="78842-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="78842-115">**Analizowanie** raportów.</span><span class="sxs-lookup"><span data-stu-id="78842-115">**Analyze** reports.</span></span> <span data-ttu-id="78842-116">Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.</span><span class="sxs-lookup"><span data-stu-id="78842-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="78842-117">Inspekcję można skonfigurować dla różnych kategorii, zgodnie z objaśnieniem w [inspekcja bazy danych](#subheading-2) sekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="78842-118">Dzienniki inspekcji są zapisywane do magazynu obiektów Blob platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78842-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="78842-119"><a id="subheading-8"></a>Zdefiniuj na poziomie serwera, a zasady inspekcji na poziomie bazy danych</span><span class="sxs-lookup"><span data-stu-id="78842-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="78842-120">Zasady inspekcji mogą być definiowane dla określonej bazy danych lub jako domyślne zasady serwera:</span><span class="sxs-lookup"><span data-stu-id="78842-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="78842-121">Zasady serwera ma zastosowanie do wszystkich istniejących i nowo utworzone bazy danych na serwerze.</span><span class="sxs-lookup"><span data-stu-id="78842-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="78842-122">Jeśli *Inspekcja obiektów blob serwera jest włączone*, on *zawsze ma zastosowanie do bazy danych* (to znaczy bazy danych zostanie przeprowadzona), niezależnie od tego, w bazie danych ustawienia inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="78842-123">Włączanie Inspekcja obiektów blob w bazie danych, oprócz włączenia go na serwerze, będzie *nie* zastąpić lub zmienić dowolne z ustawień inspekcji serwera obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="78842-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="78842-124">Zarówno inspekcji będą istniały obok siebie.</span><span class="sxs-lookup"><span data-stu-id="78842-124">Both audits will exist side by side.</span></span> <span data-ttu-id="78842-125">Innymi słowy bazy danych zostanie dwukrotnie równolegle inspekcji (raz przez zasady serwera i raz przez zasady bazy danych).</span><span class="sxs-lookup"><span data-stu-id="78842-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="78842-126">Należy unikać włączania inspekcji obiektu blob serwera i inspekcja obiektów blob dla bazy danych, chyba że:</span><span class="sxs-lookup"><span data-stu-id="78842-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="78842-127">Aby użyć innego *konta magazynu* lub *okres przechowywania* dla określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78842-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="78842-128">Chcesz inspekcji typów zdarzeń lub kategorii dla określonej bazy danych, które różnią się od typów zdarzeń lub kategorie, które są są poddawane inspekcji dla pozostałych baz danych na serwerze.</span><span class="sxs-lookup"><span data-stu-id="78842-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="78842-129">Na przykład może być wstawia tabeli, które muszą być sprawdzona tylko dla określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78842-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="78842-130">W przeciwnym razie zaleca się włączania inspekcji obiektu blob tylko poziom serwera i pozostaw inspekcji bazy danych na poziomie wyłączona dla wszystkich baz danych.</span><span class="sxs-lookup"><span data-stu-id="78842-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="78842-131"><a id="subheading-2"></a>Inspekcja bazy danych</span><span class="sxs-lookup"><span data-stu-id="78842-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="78842-132">W poniższej sekcji opisano konfigurację inspekcji przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="78842-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="78842-133">Przejdź do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78842-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78842-134">Przejdź do **ustawienia** bloku programu SQL server bazy danych/SQL chcesz inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="78842-135">W **ustawienia** bloku, wybierz opcję **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="78842-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="78842-136"><a id="auditing-screenshot"></a>![Okienka nawigacji][1]</span><span class="sxs-lookup"><span data-stu-id="78842-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="78842-137">Jeśli wolisz skonfigurować zasady inspekcji serwera (która zostanie zastosowana do wszystkich istniejących i nowo utworzone bazy danych na tym serwerze), możesz wybrać **wyświetlić ustawienia serwera** łącze w bloku inspekcji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78842-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="78842-138">Można następnie wyświetlić lub zmodyfikować ustawienia inspekcji serwera.</span><span class="sxs-lookup"><span data-stu-id="78842-138">You can then view or modify the server auditing settings.</span></span>

    ![Okienko nawigacji][2]
4. <span data-ttu-id="78842-140">Jeśli wolisz włączyć inspekcję obiektu blob na poziomie bazy danych (oprócz lub zamiast inspekcję na poziomie serwera), dla **inspekcji**, wybierz pozycję **ON**oraz **inspekcji typu**, Wybierz **obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="78842-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="78842-141">Jeśli inspekcja obiektów blob serwera jest włączone, skonfigurować bazy danych inspekcji będą istniały równolegle z obiektu blob inspekcji serwera.</span><span class="sxs-lookup"><span data-stu-id="78842-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Okienko nawigacji][3]
5. <span data-ttu-id="78842-143">Aby otworzyć **magazyn dzienników inspekcji** bloku, wybierz opcję **szczegóły magazynu**.</span><span class="sxs-lookup"><span data-stu-id="78842-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="78842-144">Wybierz konto magazynu Azure, w którym zostaną zapisane dzienniki, a następnie wybierz okres przechowywania, po upływie którego będzie można usunąć stare dzienniki.</span><span class="sxs-lookup"><span data-stu-id="78842-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="78842-145">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78842-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="78842-146">Aby uzyskać maksymalne wykorzystanie inspekcji szablonów raportów, należy użyć tego samego konta magazynu dla wszystkich baz danych inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="78842-147"><a id="storage-screenshot"></a>![Okienka nawigacji][4]</span><span class="sxs-lookup"><span data-stu-id="78842-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="78842-148">Jeśli chcesz dostosować zdarzeń inspekcji, można to zrobić za pomocą programu PowerShell lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="78842-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="78842-149">Aby uzyskać więcej informacji, zobacz [automatyzacji (interfejsu API programu PowerShell/REST)](#subheading-7) sekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="78842-150">Po skonfigurowaniu ustawień inspekcji można włączyć funkcji wykrywania zagrożeń i skonfigurować wiadomości e-mail w celu otrzymywania alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="78842-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="78842-151">Gdy używasz wykrywanie zagrożeń, pojawi się aktywne alerty w przypadku nietypowe działania bazy danych, które mogą wskazywać możliwe zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="78842-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="78842-152">Aby uzyskać więcej informacji, zobacz [wprowadzenie wykrywanie zagrożeń](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="78842-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="78842-153">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="78842-153">Click **Save**.</span></span>





## <span data-ttu-id="78842-154"><a id="subheading-3"></a>Analizowanie dzienników inspekcji i raportów</span><span class="sxs-lookup"><span data-stu-id="78842-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="78842-155">Dzienniki inspekcji są agregowane w wybranym podczas instalacji konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="78842-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="78842-156">Dzienniki inspekcji można sprawdzić za pomocą narzędzia, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="78842-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="78842-157">Dzienniki inspekcji obiektów blob są zapisywane jako kolekcja plików obiektów blob w kontenerze o nazwie **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="78842-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="78842-158">Aby uzyskać więcej szczegółowych informacji o hierarchii folderu przechowywania dzienników inspekcji obiektu blob, konwencje nazewnictwa obiektów blob i format dziennika, zobacz [odwołanie obiektu Blob inspekcji dziennika formatu (do pobrania plik .docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="78842-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="78842-159">Istnieje kilka metod, których można użyć do wyświetlenia obiektu blob, dzienniki inspekcji:</span><span class="sxs-lookup"><span data-stu-id="78842-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="78842-160">Użyj [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78842-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="78842-161">Otwórz odpowiednie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78842-161">Open the relevant database.</span></span> <span data-ttu-id="78842-162">W górnej części bazy danych **Inspekcja i wykrywanie zagrożeń** bloku, kliknij przycisk **Przeglądanie dzienników inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="78842-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Okienko nawigacji][7]

    <span data-ttu-id="78842-164">**Rekordów inspekcji** zostanie otwarty blok, z których będziesz mieć możliwość wyświetlania w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="78842-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="78842-165">Konkretne daty można wyświetlić, klikając **filtru** w górnej części **rekordów inspekcji** bloku.</span><span class="sxs-lookup"><span data-stu-id="78842-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="78842-166">Można przełączać się między rekordów inspekcji, które zostały utworzone przez serwer zasad lub bazy danych zasad kontroli.</span><span class="sxs-lookup"><span data-stu-id="78842-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Okienko nawigacji][8]

* <span data-ttu-id="78842-168">Użyj funkcji systemowej **sys.fn_get_audit_file** (T-SQL), aby przywrócić dane z dziennika inspekcji w formacie tabelarycznym.</span><span class="sxs-lookup"><span data-stu-id="78842-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="78842-169">Aby uzyskać więcej informacji na temat używania tej funkcji, zobacz [dokumentacji sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="78842-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="78842-170">Użyj **scalania plików inspekcji** w programu SQL Server Management Studio (począwszy od SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="78842-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="78842-171">Wybierz z menu Narzędzia SSMS **pliku** > **Otwórz** > **scalania plików inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="78842-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Okienko nawigacji][9]
    2. <span data-ttu-id="78842-173">**Dodaj pliki inspekcji** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="78842-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="78842-174">Wybierz jedną z **Dodaj** opcji, aby zdecydować się na scalanie plików inspekcji na dysku lokalnym lub zaimportować je z usługi Azure Storage (będzie trzeba podać szczegóły magazynu Azure i klucza konta).</span><span class="sxs-lookup"><span data-stu-id="78842-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="78842-175">Po dodaniu wszystkich plików do scalenia kliknij **OK** można ukończyć operacji scalania.</span><span class="sxs-lookup"><span data-stu-id="78842-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="78842-176">Scalony plik zostanie otwarty w programie SSMS, gdzie możesz można wyświetlać i analizować je, a także go wyeksportować do pliku w pliku XEL lub CSV lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="78842-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="78842-177">Użyj [synchronizacji aplikacji](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="78842-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="78842-178">Działa na platformie Azure, a używa Operations Management Suite (OMS) analizy dzienników publiczne interfejsy API, aby wypchnąć dzienników inspekcji SQL do OMS.</span><span class="sxs-lookup"><span data-stu-id="78842-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="78842-179">Synchronizowanie aplikacji wypchnięcia dzienników inspekcji SQL do analizy dzienników OMS zużycia za pośrednictwem pulpitu nawigacyjnego Analytics dziennika OMS.</span><span class="sxs-lookup"><span data-stu-id="78842-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="78842-180">Przy użyciu usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="78842-180">Use Power BI.</span></span> <span data-ttu-id="78842-181">Można wyświetlać i analizować dane dzienników inspekcji w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="78842-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="78842-182">Dowiedz się więcej o [usługi Power BI i dostęp do pobrania szablonu](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="78842-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="78842-183">Pobierz pliki dziennika z kontenera obiektów blob magazynu Azure w portalu lub przy użyciu narzędzia, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="78842-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="78842-184">Po pobraniu pliku dziennika, który jest lokalnie, możesz kliknąć dwukrotnie plik, który będzie otwierać, przeglądać i analizować dzienniki w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="78842-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="78842-185">Możesz również pobrać wielu plików jednocześnie za pomocą Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78842-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="78842-186">Kliknij prawym przyciskiem myszy określony podfolder (na przykład podfolder, który zawiera wszystkie pliki dziennika dotyczące określonej daty) i wybierz **Zapisz jako** można zapisać w folderze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="78842-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="78842-187">Dodatkowe metody:</span><span class="sxs-lookup"><span data-stu-id="78842-187">Additional methods:</span></span>
   * <span data-ttu-id="78842-188">Po pobraniu kilka plików (lub podfolder, który zawiera pliki dziennika dla całego dnia, zgodnie z opisem w poprzedniej pozycji na tej liście), można połączyć je lokalnie zgodnie z opisem w instrukcjach plików inspekcji scalania SSMS opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="78842-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="78842-189">Inspekcja obiektów blob widoku programowo dzienników:</span><span class="sxs-lookup"><span data-stu-id="78842-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="78842-190">Użyj [czytnika zdarzeń rozszerzonych](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteki C#.</span><span class="sxs-lookup"><span data-stu-id="78842-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="78842-191">[Zapytanie rozszerzonych plików zdarzenia](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78842-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="78842-192"><a id="subheading-5"></a>Wskazówki produkcji</span><span class="sxs-lookup"><span data-stu-id="78842-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="78842-193"><a id="subheading-6">Inspekcja bazy danych z replikacją geograficzną</a></span><span class="sxs-lookup"><span data-stu-id="78842-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="78842-194">Korzystając z bazy danych z replikacją geograficzną, istnieje możliwość ustawiania inspekcji dla podstawowej bazy danych, dodatkowej bazy danych lub obu w zależności od typu inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="78842-195">Wykonaj te instrukcje (należy pamiętać, że inspekcja obiektów blob można włączyć lub wyłączyć tylko z podstawowej bazy danych, ustawienia inspekcji):</span><span class="sxs-lookup"><span data-stu-id="78842-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="78842-196">**Podstawowa baza danych**.</span><span class="sxs-lookup"><span data-stu-id="78842-196">**Primary database**.</span></span> <span data-ttu-id="78842-197">Włącz Inspekcja obiektów blob, na serwerze lub w bazie danych, zgodnie z opisem w [inspekcja bazy danych](#subheading-2) sekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="78842-198">**Dodatkowej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="78842-198">**Secondary database**.</span></span> <span data-ttu-id="78842-199">Włącz Inspekcja obiektów blob w podstawowej bazie danych, zgodnie z opisem w [inspekcja bazy danych](#subheading-2) sekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="78842-200">Inspekcja obiektów blob musi być włączona na *podstawowa baza danych sam*, nie na serwerze.</span><span class="sxs-lookup"><span data-stu-id="78842-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="78842-201">Po włączeniu inspekcji obiektu blob na podstawowej bazy danych, również będą stają się włączone w pomocniczej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="78842-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="78842-202">Domyślnie ustawienia magazynu dla pomocniczej bazy danych będzie identyczne z podstawowej bazy danych, powodując ruchu między regionalne.</span><span class="sxs-lookup"><span data-stu-id="78842-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="78842-203">Można tego uniknąć, włączając Inspekcja obiektów blob na serwerze pomocniczym i konfigurowania magazynu lokalnego w ustawieniach magazynu serwera pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="78842-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="78842-204">Spowoduje to zmianę lokalizacji magazynu dla pomocniczej bazy danych i wyników w każdej bazie danych, zapisanie jej dzienników inspekcji do lokalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="78842-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="78842-205"><a id="subheading-6">Ponowne generowanie klucza magazynu</a></span><span class="sxs-lookup"><span data-stu-id="78842-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="78842-206">W środowisku produkcyjnym najprawdopodobniej będzie okresowo Odśwież kluczy magazynu.</span><span class="sxs-lookup"><span data-stu-id="78842-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="78842-207">Podczas odświeżania klucze, należy ponownie zapisać zasady inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="78842-208">Proces przebiega w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="78842-208">The process is as follows:</span></span>

1. <span data-ttu-id="78842-209">Otwórz **szczegóły magazynu** bloku.</span><span class="sxs-lookup"><span data-stu-id="78842-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="78842-210">W **klucz dostępu do magazynu** wybierz opcję **dodatkowej**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78842-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="78842-211">Następnie kliknij przycisk **zapisać** w górnej części bloku konfiguracji inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Okienko nawigacji][5]
2. <span data-ttu-id="78842-213">Przejdź do bloku konfiguracji magazynu i ponownie wygenerować podstawowy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="78842-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Okienko nawigacji][6]
3. <span data-ttu-id="78842-215">Przejdź wstecz do inspekcji bloku konfiguracji przełącznika klucz dostępu do magazynu z podstawowym dodatkowej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78842-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="78842-216">Następnie kliknij przycisk **zapisać** w górnej części bloku konfiguracji inspekcji.</span><span class="sxs-lookup"><span data-stu-id="78842-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="78842-217">Wróć do bloku konfiguracji magazynu, a następnie ponownie wygenerować pomocniczy klucz dostępu (w ramach przygotowania do klucza następnego cyklu odświeżania).</span><span class="sxs-lookup"><span data-stu-id="78842-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="78842-218"><a id="subheading-7"></a>Automatyzacja (programu PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="78842-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="78842-219">Można również skonfigurować inspekcji w bazie danych SQL Azure za pomocą następujących narzędzi automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="78842-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="78842-220">**Polecenia cmdlet programu PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="78842-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="78842-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="78842-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="78842-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="78842-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="78842-223">[Usuń AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="78842-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="78842-224">[Usuń AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="78842-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="78842-225">[Zestaw AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="78842-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="78842-226">[Zestaw AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="78842-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="78842-227">[Użyj AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="78842-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="78842-228">Na przykład skryptu, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="78842-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="78842-229">**Interfejs API REST - Inspekcja obiektów Blob**:</span><span class="sxs-lookup"><span data-stu-id="78842-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="78842-230">Utwórz lub zaktualizuj bazę danych obiektów Blob zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="78842-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="78842-231">Utwórz lub zaktualizuj Blob serwera zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="78842-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="78842-232">Pobierz bazy danych obiektów Blob zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="78842-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="78842-233">Pobierz obiekt Blob serwera zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="78842-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="78842-234">Pobierz Blob serwera inspekcji wynik operacji</span><span class="sxs-lookup"><span data-stu-id="78842-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
