---
title: "Kopiowanie danych z magazynu obiektów Blob do bazy danych SQL — Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia sposób użycia działanie kopiowania w potoku fabryki danych Azure, aby skopiować dane z magazynu obiektów Blob do bazy danych SQL."
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
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="9c486-104">Samouczek: Kopiowanie danych z magazynu obiektów Blob do bazy danych SQL przy użyciu fabryki danych</span><span class="sxs-lookup"><span data-stu-id="9c486-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c486-105">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c486-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9c486-106">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="9c486-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9c486-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9c486-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9c486-108">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c486-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9c486-109">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c486-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9c486-110">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9c486-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9c486-111">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="9c486-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9c486-112">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="9c486-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="9c486-113">W tym samouczku utworzysz fabryki danych z potoku, aby skopiować dane z magazynu obiektów Blob do bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9c486-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="9c486-114">Działanie kopiowania wykonuje operację przenoszenia danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9c486-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="9c486-115">Jest obsługiwane przez globalnie dostępną usługę, która może kopiować dane między różnymi magazynami danych w sposób bezpieczny, niezawodny i skalowalny.</span><span class="sxs-lookup"><span data-stu-id="9c486-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="9c486-116">Szczegółowe informacje dotyczące działania kopiowania znajdują się w artykule [Data Movement Activities](data-factory-data-movement-activities.md) (Działania przenoszenia danych).</span><span class="sxs-lookup"><span data-stu-id="9c486-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="9c486-117">Szczegółowe omówienie usługi fabryka danych, zobacz [wprowadzenie do fabryki danych Azure](data-factory-introduction.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="9c486-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="9c486-118">Wymagania wstępne dotyczące samouczka</span><span class="sxs-lookup"><span data-stu-id="9c486-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="9c486-119">Przed rozpoczęciem tego samouczka wymagane są następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="9c486-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="9c486-120">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c486-120">**Azure subscription**.</span></span>  <span data-ttu-id="9c486-121">Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9c486-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9c486-122">Zobacz [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="9c486-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="9c486-123">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c486-123">**Azure Storage Account**.</span></span> <span data-ttu-id="9c486-124">Użyj magazynu obiektów blob jako **źródła** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c486-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="9c486-125">Jeśli nie masz konta magazynu platformy Azure, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu kroki go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9c486-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="9c486-126">**Baza danych Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="9c486-126">**Azure SQL Database**.</span></span> <span data-ttu-id="9c486-127">Użyj bazy danych Azure SQL jako **docelowego** magazynu danych, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c486-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="9c486-128">Jeśli nie masz bazy danych Azure SQL można użyć w instrukcji, zobacz [sposobu tworzenia i konfigurowania bazy danych SQL Azure](../sql-database/sql-database-get-started.md) go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9c486-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="9c486-129">**2014 programu SQL Server 2012 lub Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="9c486-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="9c486-130">Użyj programu SQL Server Management Studio lub Visual Studio do tworzenia przykładowej bazy danych i wyświetlać dane wynikowe w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9c486-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="9c486-131">Zbierać nazwy konta magazynu obiektów blob i kluczy</span><span class="sxs-lookup"><span data-stu-id="9c486-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="9c486-132">Należy nazwę konta i klucz konta magazynu Azure w celu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="9c486-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="9c486-133">Należy zanotować **nazwa konta** i **klucz konta** dla konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c486-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="9c486-134">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c486-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9c486-135">Kliknij przycisk **więcej usług** w menu po lewej stronie i wybierz **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="9c486-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Przeglądaj - kont magazynu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="9c486-137">W **kont magazynu** bloku, wybierz opcję **konto magazynu Azure** , które mają być używane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c486-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="9c486-138">Wybierz **klucze dostępu** łącze w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="9c486-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="9c486-139">Kliknij przycisk **kopiowania** (obraz) przycisk Dalej, aby **nazwy konta magazynu** tekst pola i Zapisz/wklej go innym (na przykład: w pliku tekstowym).</span><span class="sxs-lookup"><span data-stu-id="9c486-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="9c486-140">Powtórz poprzedni krok, aby skopiować lub notowanie niezbędnych **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="9c486-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Klucz dostępu do magazynu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="9c486-142">Zamknij wszystkie bloki, klikając **X**.</span><span class="sxs-lookup"><span data-stu-id="9c486-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="9c486-143">Zbieraj programu SQL server, bazy danych, nazwy użytkowników</span><span class="sxs-lookup"><span data-stu-id="9c486-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="9c486-144">Należy nazwy serwera Azure SQL, bazy danych i wykonywać w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c486-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="9c486-145">Zanotuj nazwy **serwera**, **bazy danych**, i **użytkownika** bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9c486-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="9c486-146">W **portalu Azure**, kliknij przycisk **więcej usług** po lewej i wybierz **baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="9c486-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="9c486-147">W **bloku bazy danych SQL**, wybierz pozycję **bazy danych** , które mają być używane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c486-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="9c486-148">Należy zanotować **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="9c486-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="9c486-149">W **bazy danych SQL** bloku, kliknij przycisk **właściwości** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="9c486-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="9c486-150">Zanotuj wartości **nazwy serwera** i **identyfikator logowania administratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="9c486-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="9c486-151">Zamknij wszystkie bloki, klikając **X**.</span><span class="sxs-lookup"><span data-stu-id="9c486-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="9c486-152">Zezwalaj usługom platformy Azure na dostęp do serwera SQL</span><span class="sxs-lookup"><span data-stu-id="9c486-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="9c486-153">Upewnij się, że **zezwolić na dostęp do usług platformy Azure** ustawienie włączenia **ON** serwera Azure SQL, aby usługi fabryka danych można uzyskać dostępu do serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9c486-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="9c486-154">Aby sprawdzić, a następnie włącz to ustawienie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c486-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="9c486-155">Kliknij przycisk **więcej usług** koncentratora po lewej i kliknij przycisk **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="9c486-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="9c486-156">Wybierz serwer, a następnie kliknij przycisk **zapory** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="9c486-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="9c486-157">W bloku **Ustawienia zapory** kliknij pozycję **WŁĄCZ** dla ustawienia **Zezwalaj na dostęp do usług Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c486-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="9c486-158">Zamknij wszystkie bloki, klikając **X**.</span><span class="sxs-lookup"><span data-stu-id="9c486-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="9c486-159">Przygotowanie magazynu obiektów Blob i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="9c486-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="9c486-160">Teraz Przygotuj magazyn obiektów blob platformy Azure i bazy danych Azure SQL dla tego samouczka, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c486-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="9c486-161">Uruchom program Notatnik.</span><span class="sxs-lookup"><span data-stu-id="9c486-161">Launch Notepad.</span></span> <span data-ttu-id="9c486-162">Skopiuj poniższy tekst i zapisz go jako **emp.txt** do **C:\ADFGetStarted** folderu na dysku twardym.</span><span class="sxs-lookup"><span data-stu-id="9c486-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="9c486-163">Użyj narzędzi takich jak [Eksplorator magazynu Azure](http://storageexplorer.com/) do utworzenia kontenera **adftutorial** i przekazania pliku **emp.txt** do kontenera.</span><span class="sxs-lookup"><span data-stu-id="9c486-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Eksplorator usługi Storage platformy Azure.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="9c486-166">Poniższy skrypt SQL umożliwia utworzenie tabeli **emp** w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9c486-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="9c486-167">**Jeśli masz programu SQL Server 2012/2014 zainstalowanej na komputerze:** postępuj zgodnie z instrukcjami [Zarządzanie bazą danych SQL Azure przy użyciu programu SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) do połączenia się z serwerem Azure SQL, a następnie uruchom skrypt SQL.</span><span class="sxs-lookup"><span data-stu-id="9c486-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="9c486-168">W tym artykule wykorzystano [klasycznego portalu Azure](http://manage.windowsazure.com), a nie [nowego portalu Azure](https://portal.azure.com), aby skonfigurować zaporę na serwerze Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9c486-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="9c486-169">Jeśli klient nie ma dostępu do serwera SQL Azure, musisz skonfigurować zaporę serwera SQL Azure tak, aby dostęp z Twojego komputera (adresu IP) był dozwolony.</span><span class="sxs-lookup"><span data-stu-id="9c486-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="9c486-170">W [tym artykule](../sql-database/sql-database-configure-firewall-settings.md) opisano kroki konfigurowania zapory dla serwera SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9c486-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="9c486-171">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="9c486-171">Create a data factory</span></span>
<span data-ttu-id="9c486-172">Sprawdzanie wymagań wstępnych została ukończona.</span><span class="sxs-lookup"><span data-stu-id="9c486-172">You have completed the prerequisites.</span></span> <span data-ttu-id="9c486-173">Można utworzyć fabryki danych przy użyciu jednej z następujących sposobów.</span><span class="sxs-lookup"><span data-stu-id="9c486-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="9c486-174">Kliknij jedną z opcji na liście rozwijanej na górze lub poniższe linki do wykonania w samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c486-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="9c486-175">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="9c486-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="9c486-176">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9c486-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="9c486-177">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c486-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="9c486-178">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c486-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="9c486-179">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9c486-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="9c486-180">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="9c486-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="9c486-181">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="9c486-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="9c486-182">Potok danych przedstawiony w tym samouczku kopiuje dane ze źródłowego do docelowego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="9c486-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="9c486-183">Nie przekształca on danych wejściowych w celu wygenerowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9c486-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="9c486-184">Aby zapoznać się z samouczkiem dotyczącym przekształcania danych za pomocą usługi Azure Data Factory, zobacz [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Samouczek: Tworzenie pierwszego potoku przekształcającego dane przy użyciu klastra Hadoop).</span><span class="sxs-lookup"><span data-stu-id="9c486-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="9c486-185">Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego.</span><span class="sxs-lookup"><span data-stu-id="9c486-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="9c486-186">Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory).</span><span class="sxs-lookup"><span data-stu-id="9c486-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
