---
title: wprowadzenie do inspekcji bazy danych Azure SQL aaaGet | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="0e6d9-103">Rozpoczynanie pracy z inspekcją bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="0e6d9-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="0e6d9-104">Usługa Azure SQL database auditing śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="0e6d9-105">Inspekcja również:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-105">Auditing also:</span></span>

* <span data-ttu-id="0e6d9-106">Pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="0e6d9-107">Włącza i ułatwia przestrzeganie standardów toocompliance, chociaż nie gwarantuje zgodności.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="0e6d9-108">Aby uzyskać więcej informacji na temat usługi Azure programy tego zgodność ze standardami pomocy technicznej, zobacz hello [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="0e6d9-109"><a id="subheading-1"></a>Omówienie inspekcji Azure bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="0e6d9-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="0e6d9-110">Program SQL inspekcji bazy danych:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="0e6d9-111">**Zachowaj** dziennik inspekcji wybranych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="0e6d9-112">Można zdefiniować rodzaje toobe działania bazy danych inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="0e6d9-113">**Raport** na działanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-113">**Report** on database activity.</span></span> <span data-ttu-id="0e6d9-114">Można użyć wstępnie skonfigurowane raporty i tooget pulpitu nawigacyjnego, szybkie wprowadzenie aktywności i raportowanie zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="0e6d9-115">**Analizowanie** raportów.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-115">**Analyze** reports.</span></span> <span data-ttu-id="0e6d9-116">Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="0e6d9-117">Inspekcję można skonfigurować dla różnych kategorii, zgodnie z objaśnieniem w hello [inspekcja bazy danych](#subheading-2) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="0e6d9-118">Dzienniki inspekcji są zapisywane tooAzure magazynu obiektów Blob w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="0e6d9-119"><a id="subheading-8"></a>Zdefiniuj na poziomie serwera, a zasady inspekcji na poziomie bazy danych</span><span class="sxs-lookup"><span data-stu-id="0e6d9-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="0e6d9-120">Zasady inspekcji mogą być definiowane dla określonej bazy danych lub jako domyślne zasady serwera:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="0e6d9-121">Zasady serwera stosuje tooall istniejących i nowo utworzone bazy danych na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="0e6d9-122">Jeśli *Inspekcja obiektów blob serwera jest włączone*, on *stosowana jest zawsze toohello bazy danych* (to znaczy hello bazy danych zostanie przeprowadzona), niezależnie od bazy danych hello ustawienia inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="0e6d9-123">Włączenie inspekcji na powitania bazy danych, w tooenabling dodanie go na powitania serwera, obiektów blob będzie *nie* zastąpić lub zmienić dowolne z ustawień hello powitania serwera obiektu blob inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="0e6d9-124">Zarówno inspekcji będą istniały obok siebie.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-124">Both audits will exist side by side.</span></span> <span data-ttu-id="0e6d9-125">Innymi słowy hello bazy danych zostanie dwukrotnie równolegle inspekcji (raz zasadom powitania serwera i raz zasadom hello bazy danych).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0e6d9-126">Należy unikać włączania inspekcji obiektu blob serwera i inspekcja obiektów blob dla bazy danych, chyba że:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="0e6d9-127">Ma inną toouse *konta magazynu* lub *okres przechowywania* dla określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="0e6d9-128">Dla określonej bazy danych różnią się od typów zdarzeń lub kategorie, które są są poddawane inspekcji dla hello reszty baz danych hello na powitania serwera ma typy zdarzeń tooaudit lub kategorii.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="0e6d9-129">Na przykład może być wstawia tabeli, wymagające toobe inspekcji tylko dla określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="0e6d9-130">W przeciwnym razie zalecane jest włączenie inspekcji tylko poziom serwera, obiektów blob i pozostaw hello poziom bazy danych inspekcji wyłączona dla wszystkich baz danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="0e6d9-131"><a id="subheading-2"></a>Inspekcja bazy danych</span><span class="sxs-lookup"><span data-stu-id="0e6d9-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="0e6d9-132">Witaj poniższej sekcji opisano konfigurację hello inspekcji przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="0e6d9-133">Przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0e6d9-134">Przejdź toohello **ustawienia** bloku powitania serwera bazy danych/SQL SQL ma tooaudit.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="0e6d9-135">W hello **ustawienia** bloku, wybierz opcję **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="0e6d9-136"><a id="auditing-screenshot"></a>![Okienka nawigacji][1]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="0e6d9-137">Jeśli wolisz tooset się zasady inspekcji serwera (która zostanie zastosowana tooall istniejących i nowo utworzone bazy danych na tym serwerze), można wybrać hello **wyświetlić ustawienia serwera** łącze w bloku inspekcji hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="0e6d9-138">Można następnie wyświetlić lub zmodyfikować ustawienia inspekcji serwera hello.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-138">You can then view or modify hello server auditing settings.</span></span>

    ![Okienko nawigacji][2]
4. <span data-ttu-id="0e6d9-140">Jeśli wolisz tooenable Inspekcja obiektów blob na poziomie bazy danych hello (w tooor dodanie zamiast inspekcję na poziomie serwera), aby uzyskać **inspekcji**, wybierz pozycję **ON**oraz **inspekcji typu** , wybierz **obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="0e6d9-141">Po włączeniu inspekcji obiektu blob serwera hello skonfigurowane bazy danych inspekcji będą istniały równolegle powitania serwera obiektu blob inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Okienko nawigacji][3]
5. <span data-ttu-id="0e6d9-143">Witaj tooopen **magazyn dzienników inspekcji** bloku, wybierz opcję **szczegóły magazynu**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="0e6d9-144">Wybierz konto magazynu Azure hello, gdzie zostaną zapisane dzienniki, a następnie wybierz okres przechowywania hello, po którym hello będą usuwane stare dzienniki.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="0e6d9-145">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="0e6d9-146">Witaj tooget maksymalne wykorzystanie możliwości inspekcji hello raporty szablony, użyj hello tego samego konta magazynu dla wszystkich baz danych inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="0e6d9-147"><a id="storage-screenshot"></a>![Okienka nawigacji][4]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="0e6d9-148">Jeśli chcesz toocustomize hello inspekcji zdarzeń, możesz to zrobić za pomocą programu PowerShell lub hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="0e6d9-149">Aby uzyskać więcej informacji, zobacz hello [automatyzacji (interfejsu API programu PowerShell/REST)](#subheading-7) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="0e6d9-150">Po skonfigurowaniu ustawień inspekcji można włączyć hello nowych funkcji wykrywania zagrożeń i skonfigurować alerty zabezpieczeń tooreceive wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="0e6d9-151">Gdy używasz wykrywanie zagrożeń, pojawi się aktywne alerty w przypadku nietypowe działania bazy danych, które mogą wskazywać możliwe zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="0e6d9-152">Aby uzyskać więcej informacji, zobacz [wprowadzenie wykrywanie zagrożeń](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="0e6d9-153">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-153">Click **Save**.</span></span>





## <span data-ttu-id="0e6d9-154"><a id="subheading-3"></a>Analizowanie dzienników inspekcji i raportów</span><span class="sxs-lookup"><span data-stu-id="0e6d9-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="0e6d9-155">Dzienniki inspekcji są agregowane w hello kontem magazynu platformy Azure, wybrana podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="0e6d9-156">Dzienniki inspekcji można sprawdzić za pomocą narzędzia, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="0e6d9-157">Dzienniki inspekcji obiektów blob są zapisywane jako kolekcja plików obiektów blob w kontenerze o nazwie **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="0e6d9-158">Aby uzyskać szczegółowe informacje o hierarchii hello folderu przechowywania dzienników inspekcji obiektu blob hello, konwencje nazewnictwa obiektów blob i format dziennika, zobacz hello [odwołanie obiektu Blob inspekcji dziennika formatu (do pobrania plik .docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="0e6d9-159">Istnieje kilka metod, można użyć obiektu blob tooview dzienniki inspekcji:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="0e6d9-160">Użyj hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="0e6d9-161">Otwórz hello odpowiednie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-161">Open hello relevant database.</span></span> <span data-ttu-id="0e6d9-162">Witaj AT na początku hello bazy danych **Inspekcja i wykrywanie zagrożeń** bloku, kliknij przycisk **Przeglądanie dzienników inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Okienko nawigacji][7]

    <span data-ttu-id="0e6d9-164">**Rekordów inspekcji** zostanie otwarty blok, z których będziesz w stanie tooview hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="0e6d9-165">Konkretne daty można wyświetlić, klikając **filtru** u góry hello hello **rekordów inspekcji** bloku.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="0e6d9-166">Można przełączać się między rekordów inspekcji, które zostały utworzone przez serwer zasad lub bazy danych zasad kontroli.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Okienko nawigacji][8]

* <span data-ttu-id="0e6d9-168">Użyj funkcji systemowej hello **sys.fn_get_audit_file** (T-SQL) tooreturn hello danych z dziennika inspekcji w formacie tabelarycznym.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="0e6d9-169">Aby uzyskać więcej informacji na temat używania tej funkcji, zobacz hello [dokumentacji sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="0e6d9-170">Użyj **scalania plików inspekcji** w programu SQL Server Management Studio (począwszy od SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="0e6d9-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="0e6d9-171">Wybierz z menu Narzędzia SSMS hello **pliku** > **Otwórz** > **scalania plików inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Okienko nawigacji][9]
    2. <span data-ttu-id="0e6d9-173">Witaj **Dodaj pliki inspekcji** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="0e6d9-174">Wybierz jedną z hello **Dodaj** opcji, aby wybrać, czy inspekcji toomerge pliki z dysku lokalnego na dysku lub zaimportować je z usługi Azure Storage (użytkownik będzie tooprovide wymagane szczegóły usługi Azure Storage, a klucz konta).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="0e6d9-175">Po dodaniu wszystkich plików toomerge kliknij **OK** toocomplete hello: Operacja scalania.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="0e6d9-176">Hello scalony plik zostanie otwarty w programie SSMS, w którym można wyświetlać i analizować je, a także eksportu go tooan pliku XEL lub CSV pliku lub tooa tabeli.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="0e6d9-177">Użyj hello [synchronizacji aplikacji](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="0e6d9-178">Działa na platformie Azure, a używa analizy dzienników Operations Management Suite (OMS) publiczne interfejsy API toopush SQL dzienników inspekcji na OMS.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="0e6d9-179">Hello synchronizacji aplikacji wypchnięcia dzienników inspekcji SQL do analizy dzienników OMS zużycia za pośrednictwem pulpitu nawigacyjnego Analytics dziennika OMS hello.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="0e6d9-180">Przy użyciu usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-180">Use Power BI.</span></span> <span data-ttu-id="0e6d9-181">Można wyświetlać i analizować dane dzienników inspekcji w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="0e6d9-182">Dowiedz się więcej o [usługi Power BI i dostęp do pobrania szablonu](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="0e6d9-183">Pobierz pliki dziennika z kontenera obiektów blob magazynu Azure za pośrednictwem portalu hello lub przy użyciu narzędzia, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="0e6d9-184">Po pobraniu pliku dziennika, który jest lokalnie, możesz kliknąć dwukrotnie tooopen pliku hello, wyświetlać i analizować dzienniki hello w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="0e6d9-185">Możesz również pobrać wielu plików jednocześnie za pomocą Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="0e6d9-186">Kliknij prawym przyciskiem myszy określony podfolder (na przykład podfolder, który zawiera wszystkie pliki dziennika dotyczące określonej daty) i wybierz **Zapisz jako** toosave w folderze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="0e6d9-187">Dodatkowe metody:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-187">Additional methods:</span></span>
   * <span data-ttu-id="0e6d9-188">Po pobraniu kilka plików (lub podfolder, który zawiera pliki dziennika dla całego dnia, zgodnie z opisem w hello poprzedniego elementu na tej liście), można połączyć je lokalnie zgodnie z opisem w instrukcjach plików inspekcji scalania SSMS hello opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="0e6d9-189">Inspekcja obiektów blob widoku programowo dzienników:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="0e6d9-190">Użyj hello [czytnika zdarzeń rozszerzonych](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteki C#.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="0e6d9-191">[Zapytanie rozszerzonych plików zdarzenia](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="0e6d9-192"><a id="subheading-5"></a>Wskazówki produkcji</span><span class="sxs-lookup"><span data-stu-id="0e6d9-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="0e6d9-193"><a id="subheading-6">Inspekcja bazy danych z replikacją geograficzną</a></span><span class="sxs-lookup"><span data-stu-id="0e6d9-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="0e6d9-194">Korzystając z bazy danych z replikacją geograficzną, jest możliwe tooset inspekcja na powitania podstawowej bazy danych, hello pomocniczej bazy danych lub obu w zależności od typu inspekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="0e6d9-195">Wykonaj te instrukcje (należy pamiętać, że inspekcja obiektów blob można włączyć lub wyłączyć tylko z ustawień inspekcji bazy danych podstawowego hello):</span><span class="sxs-lookup"><span data-stu-id="0e6d9-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="0e6d9-196">**Podstawowa baza danych**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-196">**Primary database**.</span></span> <span data-ttu-id="0e6d9-197">Włącz Inspekcja obiektów blob, albo na powitania serwera na powitania bazy danych, zgodnie z opisem w hello [inspekcja bazy danych](#subheading-2) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="0e6d9-198">**Dodatkowej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-198">**Secondary database**.</span></span> <span data-ttu-id="0e6d9-199">Włącz inspekcję obiektów blob na powitania podstawowej bazy danych, zgodnie z opisem w hello [inspekcja bazy danych](#subheading-2) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="0e6d9-200">Inspekcja obiektów blob musi być włączona na powitania *podstawowa baza danych sam*, nie powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="0e6d9-201">Po włączeniu inspekcji obiektu blob na powitania podstawowej bazy danych, również będą stają się włączone na powitania dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="0e6d9-202">Domyślnie hello ustawienia magazynu dla hello pomocniczej bazy danych będzie identyczne toothose hello głównej bazy danych, powodując ruchu między regionalne.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="0e6d9-203">Można tego uniknąć, włączając Inspekcja obiektów blob na powitania serwera pomocniczego i konfigurowania magazynu lokalnego w ustawieniach magazynu pomocniczego serwera hello.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="0e6d9-204">Spowoduje to zmianę lokalizacji magazynu hello hello pomocniczej bazy danych i wyników w każdej bazie danych, zapisanie jej magazynem toolocal dzienniki inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="0e6d9-205"><a id="subheading-6">Ponowne generowanie klucza magazynu</a></span><span class="sxs-lookup"><span data-stu-id="0e6d9-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="0e6d9-206">W środowisku produkcyjnym jest prawdopodobnie toorefresh Twojego magazynu kluczy okresowo.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="0e6d9-207">Podczas odświeżania kluczy, należy zasady inspekcji hello tooresave.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="0e6d9-208">Witaj proces przebiega następująco:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-208">hello process is as follows:</span></span>

1. <span data-ttu-id="0e6d9-209">Otwórz hello **szczegóły magazynu** bloku.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="0e6d9-210">W hello **klucz dostępu do magazynu** wybierz opcję **dodatkowej**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="0e6d9-211">Następnie kliknij przycisk **zapisać** u góry hello hello inspekcji blok konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Okienko nawigacji][5]
2. <span data-ttu-id="0e6d9-213">Przejdź do bloku konfiguracji magazynu toohello i ponowne wygenerowanie hello podstawowy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Okienko nawigacji][6]
3. <span data-ttu-id="0e6d9-215">Przejdź wstecz toohello inspekcji blok konfiguracji, Przełącz hello klucz dostępu do magazynu z tooprimary dodatkowej, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="0e6d9-216">Następnie kliknij przycisk **zapisać** u góry hello hello inspekcji blok konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="0e6d9-217">Blok konfiguracji magazynu toohello i regenerate hello pomocniczy klucz dostępu (w ramach przygotowania do cyklu odświeżania hello klawisza Następna), przejdź wstecz.</span><span class="sxs-lookup"><span data-stu-id="0e6d9-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="0e6d9-218"><a id="subheading-7"></a>Automatyzacja (programu PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="0e6d9-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="0e6d9-219">Można również skonfigurować inspekcji w bazie danych SQL Azure za pomocą powitania po narzędziami automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="0e6d9-220">**Polecenia cmdlet programu PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="0e6d9-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="0e6d9-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="0e6d9-223">[Usuń AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="0e6d9-224">[Usuń AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="0e6d9-225">[Zestaw AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="0e6d9-226">[Zestaw AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="0e6d9-227">[Użyj AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="0e6d9-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="0e6d9-228">Na przykład skryptu, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d9-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="0e6d9-229">**Interfejs API REST - Inspekcja obiektów Blob**:</span><span class="sxs-lookup"><span data-stu-id="0e6d9-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="0e6d9-230">Utwórz lub zaktualizuj bazę danych obiektów Blob zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="0e6d9-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="0e6d9-231">Utwórz lub zaktualizuj Blob serwera zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="0e6d9-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="0e6d9-232">Pobierz bazy danych obiektów Blob zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="0e6d9-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="0e6d9-233">Pobierz obiekt Blob serwera zasady inspekcji</span><span class="sxs-lookup"><span data-stu-id="0e6d9-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="0e6d9-234">Pobierz Blob serwera inspekcji wynik operacji</span><span class="sxs-lookup"><span data-stu-id="0e6d9-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
