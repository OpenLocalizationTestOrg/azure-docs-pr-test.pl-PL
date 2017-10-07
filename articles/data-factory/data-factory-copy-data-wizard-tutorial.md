---
title: "Samouczek: Tworzenie potoku przy użyciu Kreatora kopiowania | Microsoft Docs"
description: "W tym samouczku utworzysz potok fabryki danych Azure z działaniem kopiowania za pomocą hello obsługiwane przez fabrykę danych Kreatora kopiowania"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="c186b-103">Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu Kreatora kopiowania usługi Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="c186b-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c186b-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c186b-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c186b-105">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="c186b-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c186b-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c186b-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c186b-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c186b-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c186b-108">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="c186b-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c186b-109">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c186b-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c186b-110">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="c186b-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c186b-111">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="c186b-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="c186b-112">W tym samouczku przedstawiono sposób toouse hello **kreatora kopiowania** toocopy dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c186b-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="c186b-113">Witaj fabryki danych Azure **kreatora kopiowania** pozwala tooquickly utworzyć potok danych, które kopiuje dane z magazynu danych obsługiwane źródła danych magazynu tooa obsługiwane docelowego.</span><span class="sxs-lookup"><span data-stu-id="c186b-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="c186b-114">Dlatego zaleca się, użyj Kreatora hello jako pierwszy toocreate krok potoku próbki dla danego scenariusza przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="c186b-115">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i lokalizacje docelowe, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c186b-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="c186b-116">Ten samouczek pokazuje, jak toocreate fabryki danych Azure, hello uruchamiania kreatora kopiowania, przejdź na kolejnych kroków tooprovide szczegóły danego scenariusza wprowadzanie/przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="c186b-117">Po zakończeniu czynności w Kreatorze hello hello Kreator automatycznie tworzy potoku z toocopy działanie kopiowania danych z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c186b-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="c186b-118">Więcej informacji o Działaniu kopiowania znajduje się w temacie [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c186b-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c186b-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c186b-119">Prerequisites</span></span>
<span data-ttu-id="c186b-120">Wymagania wstępne wymienione w hello ukończyć [— samouczek Przegląd](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykuł przed wykonaniem tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c186b-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="c186b-121">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="c186b-121">Create data factory</span></span>
<span data-ttu-id="c186b-122">W tym kroku użyjesz hello Azure toocreate portalu fabryki danych Azure o nazwie **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="c186b-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="c186b-123">Zaloguj się za[portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c186b-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c186b-124">Kliknij przycisk **+ nowy** hello lewym górnym rogu kliknij **dane i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="c186b-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Nowy-> Fabryka danych](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="c186b-126">W hello **nowa fabryka danych** bloku:</span><span class="sxs-lookup"><span data-stu-id="c186b-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="c186b-127">Wprowadź **ADFTutorialDataFactory** dla hello **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="c186b-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="c186b-128">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="c186b-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c186b-129">Jeśli wystąpi błąd hello: `Data factory name “ADFTutorialDataFactory” is not available`, Zmień nazwę hello hello fabryki danych (na przykład yournameADFTutorialDataFactoryYYYYMMDD) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="c186b-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="c186b-130">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Nazwa fabryki danych jest niedostępna](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="c186b-132">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c186b-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="c186b-133">Dla grupy zasobów wykonaj jedną z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c186b-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="c186b-134">Wybierz **Użyj istniejącego** tooselect istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="c186b-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="c186b-135">Wybierz **Utwórz nowy** tooenter nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c186b-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="c186b-136">Niektóre kroki hello w tym samouczku Załóżmy, że nazwa hello: **ADFTutorialResourceGroup** hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c186b-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="c186b-137">toolearn temat grup zasobów, zobacz [toomanage przy użyciu zasobów grup zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c186b-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="c186b-138">Wybierz **lokalizacji** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="c186b-139">Wybierz **toodashboard numeru Pin** pole wyboru u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="c186b-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="c186b-140">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c186b-140">Click **Create**.</span></span>
      
       ![Blok Nowa fabryka danych](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="c186b-142">Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="c186b-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![Strona główna fabryki danych](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="c186b-144">Uruchamianie Kreatora kopiowania</span><span class="sxs-lookup"><span data-stu-id="c186b-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="c186b-145">W bloku fabryki danych hello, kliknij **kopiowanie danych [Podgląd]** toolaunch hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="c186b-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c186b-146">Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** w ustawieniach przeglądarki hello (lub) Zachowaj ona włączona i utworzyć wyjątek  **Login.microsoftonline.com** , a następnie spróbuj ponownie uruchomić Kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="c186b-147">W hello **właściwości** strony:</span><span class="sxs-lookup"><span data-stu-id="c186b-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="c186b-148">Wprowadź wartość **CopyFromBlobToAzureSql** w polu **Nazwa zadania**</span><span class="sxs-lookup"><span data-stu-id="c186b-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="c186b-149">Wprowadź **opis** (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="c186b-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="c186b-150">Zmień hello **Data i godzina rozpoczęcia** i hello **Data i godzina zakończenia** tak, aby data zakończenia hello jest ustawić tootoday i uruchomić Data toofive dni wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c186b-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="c186b-151">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-151">Click **Next**.</span></span>  
      
      ![Narzędzie kopiowania — strona Właściwości](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="c186b-153">Na powitania **magazynu danych źródła** kliknij przycisk **magazyn obiektów Blob Azure** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c186b-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="c186b-154">Zadanie kopiowania hello są używane magazynu tej strony toospecify hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![Narzędzie kopiowania — strona magazynu danych źródłowych](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="c186b-156">Na powitania **Określ konto magazynu obiektów Blob platformy Azure hello** strony:</span><span class="sxs-lookup"><span data-stu-id="c186b-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="c186b-157">Wprowadź wartość **AzureStorageLinkedService** w polu **Nazwa połączonej usługi**.</span><span class="sxs-lookup"><span data-stu-id="c186b-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="c186b-158">Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.</span><span class="sxs-lookup"><span data-stu-id="c186b-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="c186b-159">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c186b-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="c186b-160">Wybierz **konto magazynu Azure** z hello konta dostępne w ramach subskrypcji hello wybrane listy magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c186b-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="c186b-161">Można także tooenter ustawienia konta magazynu ręcznie, wybierając **ręcznie wprowadzić** opcję hello **konta metodę wyboru**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![Skopiuj narzędzie — Określ konto magazynu obiektów Blob platformy Azure hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="c186b-163">Na **wybierz hello wejściowy plik lub folder** strony:</span><span class="sxs-lookup"><span data-stu-id="c186b-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="c186b-164">Kliknij dwukrotnie pozycję **adftutorial** (folder).</span><span class="sxs-lookup"><span data-stu-id="c186b-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="c186b-165">Zaznacz plik **emp.txt** i kliknij przycisk **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="c186b-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="c186b-167">Na powitania **wybierz hello wejściowy plik lub folder** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="c186b-168">Nie wybieraj opcji **Kopia binarna**.</span><span class="sxs-lookup"><span data-stu-id="c186b-168">Do not select **Binary copy**.</span></span> 
   
    ![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="c186b-170">Na powitania **ustawienia formatu pliku** strony, zobacz ograniczniki hello i hello schemat, który jest automatycznie wykrywane przez kreatora hello podczas analizowania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="c186b-171">Możesz też wprowadzić ograniczniki hello ręcznie hello kopiowania kreatora toostop auto wykrywania lub toooverride.</span><span class="sxs-lookup"><span data-stu-id="c186b-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="c186b-172">Kliknij przycisk **dalej** po Przejrzyj ograniczniki hello i wyświetlić podgląd danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![Narzędzie kopiowania — ustawienia formatu pliku](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="c186b-174">Na powitania docelowego dane przechowywane strony, wybierz **bazy danych SQL Azure**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Narzędzie kopiowania — wybieranie magazynu docelowego](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="c186b-176">Na **bazy danych Azure SQL hello określ** strony:</span><span class="sxs-lookup"><span data-stu-id="c186b-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="c186b-177">Wprowadź **AzureSqlLinkedService** dla hello **nazwa połączenia** pola.</span><span class="sxs-lookup"><span data-stu-id="c186b-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="c186b-178">Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru serwera/bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="c186b-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="c186b-179">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c186b-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="c186b-180">Wybierz opcje **Nazwa serwera** i **Baza danych**.</span><span class="sxs-lookup"><span data-stu-id="c186b-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="c186b-181">Wypełnij pola **Nazwa użytkownika** i **Hasło**.</span><span class="sxs-lookup"><span data-stu-id="c186b-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="c186b-182">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-182">Click **Next**.</span></span>  
      
      ![Narzędzie kopiowania — określanie bazy danych Azure SQL Database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="c186b-184">Na powitania **mapowania tabeli** wybierz pozycję **pustych elementów** dla hello **docelowego** pola z listy rozwijanej hello, kliknij przycisk **Strzałka w dół** (opcjonalnie) toosee hello schematu i toopreview hello danych.</span><span class="sxs-lookup"><span data-stu-id="c186b-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![Narzędzie kopiowania — mapowanie tabeli](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="c186b-186">Na powitania **mapowanie schematu** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![Narzędzie kopiowania — mapowanie schematu](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="c186b-188">Na powitania **ustawienia wydajności** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c186b-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![Narzędzie kopiowania — ustawienia wydajności](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="c186b-190">Przejrzyj informacje w hello **Podsumowanie** , a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="c186b-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="c186b-191">Kreator Hello tworzy dwa połączone usługi, dwóch zestawów danych (dane wejściowe i wyjściowe) i jeden potok w fabryce danych hello (z którego uruchamiana jest hello kreatora kopiowania).</span><span class="sxs-lookup"><span data-stu-id="c186b-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![Narzędzie kopiowania — ustawienia wydajności](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="c186b-193">Uruchamianie aplikacji do monitorowania i zarządzania</span><span class="sxs-lookup"><span data-stu-id="c186b-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="c186b-194">Na powitania **wdrożenia** strony, kliknij łącze hello: `Click here toomonitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="c186b-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![Narzędzie kopiowania — wdrażanie zakończyło się pomyślnie](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="c186b-196">monitorowanie aplikacji Hello jest uruchamiana w osobnej karcie w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="c186b-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Aplikacja do monitorowania](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="c186b-198">toosee hello najnowszy stan wycinków co godzinę, kliknij przycisk **Odśwież** przycisku na powitania **okien działania** listy u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="c186b-199">Pięć okien działania zostanie wyświetlony przez pięć dni od czasu rozpoczęcia i zakończenia dla potoku hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="c186b-200">listy Hello nie zostanie automatycznie odświeżony, więc możesz muszą tooclick Odśwież kilka razy, zanim zostaną wyświetlone wszystkie okna działania hello w stanie gotowe hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="c186b-201">Wybierz okno działania hello listy.</span><span class="sxs-lookup"><span data-stu-id="c186b-201">Select an activity window in hello list.</span></span> <span data-ttu-id="c186b-202">Zobacz szczegóły hello o nim w hello **działania okna Eksploratora** na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="c186b-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![Szczegóły okna działania](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="c186b-204">Należy zauważyć, że są daty hello 11, 12, 13, 14 do 15 w kolorze zielonym, co oznacza, że już zostały wyprodukowane hello dzienne dane wyjściowe wycinków tymi datami.</span><span class="sxs-lookup"><span data-stu-id="c186b-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="c186b-205">Również Zobacz kolor kodowania na powitania potoku i hello wyjściowy zestaw danych w widoku diagramu hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="c186b-206">W poprzednim kroku hello Zwróć uwagę, wycinków dwóch zostały już utworzone, jeden wycinek jest obecnie przetwarzana i hello pozostałe dwa oczekują toobe przetworzone (w oparciu kodowanie kolorami hello).</span><span class="sxs-lookup"><span data-stu-id="c186b-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="c186b-207">Aby uzyskać więcej informacji na temat używania tej aplikacji, zobacz artykuł [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) (Monitorowanie potoku i zarządzanie nim przy użyciu aplikacji do monitorowania).</span><span class="sxs-lookup"><span data-stu-id="c186b-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c186b-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c186b-208">Next steps</span></span>
<span data-ttu-id="c186b-209">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c186b-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c186b-210">Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello:</span><span class="sxs-lookup"><span data-stu-id="c186b-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c186b-211">Aby uzyskać więcej informacji o pola/właściwości, które widać w kreatorze kopiowania hello magazynu danych kliknij łącze hello hello magazynu danych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="c186b-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
