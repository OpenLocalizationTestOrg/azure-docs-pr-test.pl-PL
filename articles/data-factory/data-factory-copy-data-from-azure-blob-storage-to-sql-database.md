---
title: "aaaCopy danych z magazynu obiektów Blob tooSQL bazy danych - Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toouse działanie kopiowania w fabryce danych Azure potoku toocopy danych z bazy danych tooSQL magazynu obiektów Blob."
keywords: "Obiekt blob sql magazynu obiektów blob, kopiowanie danych"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="ca151-104">Samouczek: Kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych przy użyciu fabryki danych</span><span class="sxs-lookup"><span data-stu-id="ca151-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca151-105">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca151-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="ca151-106">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="ca151-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="ca151-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ca151-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="ca151-108">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca151-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="ca151-109">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca151-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="ca151-110">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ca151-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="ca151-111">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="ca151-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="ca151-112">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="ca151-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="ca151-113">W tym samouczku utworzysz fabryki danych danymi toocopy potoku z bazy danych tooSQL magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="ca151-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="ca151-114">Witaj działanie kopiowania wykonuje hello przenoszenia danych w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="ca151-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="ca151-115">Jest obsługiwane przez globalnie dostępną usługę, która może kopiować dane między różnymi magazynami danych w sposób bezpieczny, niezawodny i skalowalny.</span><span class="sxs-lookup"><span data-stu-id="ca151-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="ca151-116">Zobacz [działań przepływu danych](data-factory-data-movement-activities.md) artykułu szczegółowe informacje o hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="ca151-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="ca151-117">Szczegółowe omówienie hello usługi fabryka danych, zobacz hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ca151-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="ca151-118">Wymagania wstępne dotyczące samouczka hello</span><span class="sxs-lookup"><span data-stu-id="ca151-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="ca151-119">Przed rozpoczęciem tego samouczka, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="ca151-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="ca151-120">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="ca151-120">**Azure subscription**.</span></span>  <span data-ttu-id="ca151-121">Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ca151-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ca151-122">Zobacz hello [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="ca151-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="ca151-123">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="ca151-123">**Azure Storage Account**.</span></span> <span data-ttu-id="ca151-124">Użyj magazynu obiektów blob hello **źródła** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca151-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="ca151-125">Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykuł, aby toocreate kroki, jeden.</span><span class="sxs-lookup"><span data-stu-id="ca151-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="ca151-126">**Usługa Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ca151-126">**Azure SQL Database**.</span></span> <span data-ttu-id="ca151-127">Użyj bazy danych Azure SQL jako **docelowego** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca151-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="ca151-128">Jeśli nie masz bazy danych Azure SQL można używać w samouczku hello, zobacz [jak toocreate i skonfiguruj bazę danych SQL Azure](../sql-database/sql-database-get-started.md) toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="ca151-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="ca151-129">**2014 programu SQL Server 2012 lub Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="ca151-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="ca151-130">Używasz programu SQL Server Management Studio lub Visual Studio toocreate przykładowej bazy danych i dane wynikowe hello tooview hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ca151-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="ca151-131">Zbierać nazwy konta magazynu obiektów blob i kluczy</span><span class="sxs-lookup"><span data-stu-id="ca151-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="ca151-132">Musisz mieć konto hello toodo konta nazwy i klucza konta magazynu Azure, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca151-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="ca151-133">Należy zanotować **nazwa konta** i **klucz konta** dla konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="ca151-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="ca151-134">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ca151-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ca151-135">Kliknij przycisk **więcej usług** na powitania lewego menu i wybierz **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ca151-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Przeglądaj - kont magazynu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="ca151-137">W hello **kont magazynu** bloku, wybierz hello **konto magazynu Azure** mają toouse w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca151-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="ca151-138">Wybierz **klucze dostępu** łącze w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ca151-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="ca151-139">Kliknij przycisk **kopiowania** (obraz) obok przycisku zbyt**nazwy konta magazynu** tekst pola i Zapisz/wklej go innym (na przykład: w pliku tekstowym).</span><span class="sxs-lookup"><span data-stu-id="ca151-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="ca151-140">Powtórz poprzednie toocopy krok hello lub zanotuj hello **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="ca151-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Klucz dostępu do magazynu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="ca151-142">Zamknij wszystkie bloki hello klikając **X**.</span><span class="sxs-lookup"><span data-stu-id="ca151-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="ca151-143">Zbieraj programu SQL server, bazy danych, nazwy użytkowników</span><span class="sxs-lookup"><span data-stu-id="ca151-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="ca151-144">Należy hello nazwy serwera Azure SQL, bazy danych i toodo użytkownika w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca151-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="ca151-145">Zanotuj nazwy **serwera**, **bazy danych**, i **użytkownika** bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ca151-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="ca151-146">W hello **portalu Azure**, kliknij przycisk **więcej usług** na powitania po lewej stronie i wybierz pozycję **baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="ca151-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="ca151-147">W hello **bloku bazy danych SQL**, wybierz pozycję hello **bazy danych** mają toouse w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca151-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="ca151-148">Zanotuj hello **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="ca151-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="ca151-149">W hello **bazy danych SQL** bloku, kliknij przycisk **właściwości** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ca151-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="ca151-150">Zanotuj wartości hello **nazwy serwera** i **identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="ca151-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="ca151-151">Zamknij wszystkie bloki hello klikając **X**.</span><span class="sxs-lookup"><span data-stu-id="ca151-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="ca151-152">Zezwalaj usługom platformy Azure tooaccess programu SQL server</span><span class="sxs-lookup"><span data-stu-id="ca151-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="ca151-153">Upewnij się, że **dostęp do usług tooAzure** ustawienie włączenia **ON** serwera Azure SQL, że hello usługi fabryka danych można uzyskiwać dostęp do serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ca151-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="ca151-154">tooverify i włącz to ustawienie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ca151-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="ca151-155">Kliknij przycisk **więcej usług** koncentratora na powitania po lewej i kliknij przycisk **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="ca151-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="ca151-156">Wybierz swój serwer, a następnie kliknij przycisk **Zapora** w obszarze **USTAWIENIA**.</span><span class="sxs-lookup"><span data-stu-id="ca151-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="ca151-157">W hello **ustawienia zapory** bloku, kliknij przycisk **ON** dla **dostęp do usług tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="ca151-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="ca151-158">Zamknij wszystkie bloki hello klikając **X**.</span><span class="sxs-lookup"><span data-stu-id="ca151-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="ca151-159">Przygotowanie magazynu obiektów Blob i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="ca151-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="ca151-160">Teraz Przygotuj magazyn obiektów blob platformy Azure i bazy danych Azure SQL hello samouczek, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ca151-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="ca151-161">Uruchom program Notatnik.</span><span class="sxs-lookup"><span data-stu-id="ca151-161">Launch Notepad.</span></span> <span data-ttu-id="ca151-162">Skopiuj następujące tekst hello i zapisz go jako **emp.txt** za**C:\ADFGetStarted** folderu na dysku twardym.</span><span class="sxs-lookup"><span data-stu-id="ca151-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="ca151-163">Użyj narzędzia takiego jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) toocreate hello **adftutorial** hello kontenera i tooupload **emp.txt** kontenera toohello plików.</span><span class="sxs-lookup"><span data-stu-id="ca151-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Eksplorator usługi Storage platformy Azure.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="ca151-166">Użyj powitania po hello toocreate skryptu SQL **pustych elementów** tabeli w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ca151-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="ca151-167">**Jeśli masz programu SQL Server 2012/2014 zainstalowanej na komputerze:** postępuj zgodnie z instrukcjami [Zarządzanie bazą danych SQL Azure przy użyciu programu SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooyour tooconnect Azure SQL server i uruchom hello skryptu SQL.</span><span class="sxs-lookup"><span data-stu-id="ca151-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="ca151-168">W tym artykule wykorzystano hello [klasycznego portalu Azure](http://manage.windowsazure.com), nie hello [nowego portalu Azure](https://portal.azure.com), tooconfigure zapory dla serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ca151-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="ca151-169">Jeśli klient nie jest dozwolona tooaccess hello Azure SQL server, należy tooconfigure zapory dla programu access tooallow serwera Azure SQL z komputera (adres IP).</span><span class="sxs-lookup"><span data-stu-id="ca151-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="ca151-170">Zobacz [w tym artykule](../sql-database/sql-database-configure-firewall-settings.md) kroki tooconfigure hello zapory serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ca151-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="ca151-171">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="ca151-171">Create a data factory</span></span>
<span data-ttu-id="ca151-172">Witaj wymagań wstępnych została ukończona.</span><span class="sxs-lookup"><span data-stu-id="ca151-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="ca151-173">Można utworzyć fabryki danych przy użyciu jednej z hello następujące sposoby.</span><span class="sxs-lookup"><span data-stu-id="ca151-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="ca151-174">Kliknij jedną z opcji hello na liście rozwijanej hello góry hello lub hello samouczka hello tooperform łącza.</span><span class="sxs-lookup"><span data-stu-id="ca151-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="ca151-175">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="ca151-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="ca151-176">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ca151-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="ca151-177">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca151-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="ca151-178">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca151-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="ca151-179">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ca151-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="ca151-180">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="ca151-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="ca151-181">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="ca151-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="ca151-182">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="ca151-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="ca151-183">Przekształca dane wyjściowe tooproduce danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="ca151-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="ca151-184">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie pierwszego potoku dane tootransform przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ca151-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="ca151-185">Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="ca151-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="ca151-186">Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ca151-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
