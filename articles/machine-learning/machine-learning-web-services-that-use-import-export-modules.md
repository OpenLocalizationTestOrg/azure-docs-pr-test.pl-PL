---
title: "aaaUsing importowania i eksportowania danych w usługach sieci web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello toosend moduły danych importowanie i eksportowanie danych i odbierać dane z usługi sieci web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="5ae9f-103">Wdrażanie usług sieci Web Azure ML używających modułów importu i eksportu danych</span><span class="sxs-lookup"><span data-stu-id="5ae9f-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="5ae9f-104">Po utworzeniu eksperyment predykcyjny zazwyczaj są dodawane usługi sieci web w danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="5ae9f-105">Podczas wdrażania eksperymentu hello konsumentów może wysyłać i odbierać dane z usługi sieci web hello za pośrednictwem hello wejścia i wyjścia.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="5ae9f-106">Dla pewnych aplikacji danych klientów mogą być dostępne ze strumieniowego źródła danych lub już znajdują się w źródle danych zewnętrznych, takie jak magazyn obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="5ae9f-107">W takich przypadkach nie potrzebują oni odczytywanie i zapisywanie danych przy użyciu sieci web usługi wejścia i wyjścia.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="5ae9f-108">Mogą, zamiast tego użyj hello usługi wykonywania wsadowego (BES) tooread danych ze źródła danych hello za pomocą modułu i zaimportuj dane i zapisać hello oceniania wyników tooa różnych danych lokalizacji za pomocą modułu eksportu danych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="5ae9f-109">Hello importowanie danych i moduły danych eksportu, można odczytywać i zapisać dane toovarious, na przykład adres URL sieci Web za pośrednictwem protokołu HTTP, zapytanie Hive, bazy danych Azure SQL, Magazyn tabel Azure, magazynu obiektów Blob platformy Azure, strumieniowego źródła danych zawierają lub lokalną bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="5ae9f-110">W tym temacie używa hello "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" przykładowe i zakłada hello zestaw danych został już załadowany do tabeli Azure SQL o nazwie censusdata.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="5ae9f-111">Tworzenie eksperymentu uczenia hello</span><span class="sxs-lookup"><span data-stu-id="5ae9f-111">Create hello training experiment</span></span>
<span data-ttu-id="5ae9f-112">Po otwarciu hello "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" Przykładowe go używa hello próbki dla dorosłych klasyfikacji binarnej dochodu spisu w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="5ae9f-113">I eksperymentu hello kanwie hello będzie wyglądać podobnie toohello po obrazu:</span><span class="sxs-lookup"><span data-stu-id="5ae9f-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Wstępna konfiguracja hello eksperymentu.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="5ae9f-115">tooread hello danych z tabeli Azure SQL hello:</span><span class="sxs-lookup"><span data-stu-id="5ae9f-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="5ae9f-116">Usuń hello modułu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="5ae9f-117">W polu wyszukiwania składników hello wpisz importu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="5ae9f-118">Z listy wyników hello, Dodaj *i zaimportuj dane* kanwy eksperymentu toohello modułu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="5ae9f-119">Połącz dane wyjściowe hello *i zaimportuj dane* danych wejściowych hello modułu hello *Clean Missing Data* modułu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="5ae9f-120">W okienku właściwości, wybierz **bazy danych SQL Azure** w hello **źródła danych** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="5ae9f-121">W hello **nazwę serwera bazy danych**, **Nazwa bazy danych**, **nazwy użytkownika**, i **hasło** wprowadź odpowiednie informacje powitalnych dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="5ae9f-122">W polu kwerendy bazy danych hello wprowadzić hello następującego zapytania.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="5ae9f-123">Wybierz [wieku]</span><span class="sxs-lookup"><span data-stu-id="5ae9f-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="5ae9f-124">z dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="5ae9f-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="5ae9f-125">U dołu hello hello roboczego eksperymentu, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="5ae9f-126">Utworzyć eksperyment predykcyjny hello</span><span class="sxs-lookup"><span data-stu-id="5ae9f-126">Create hello predictive experiment</span></span>
<span data-ttu-id="5ae9f-127">Następnie możesz skonfigurować eksperyment predykcyjny hello, z którego można wdrożyć usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="5ae9f-128">U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **predykcyjnej usługi sieci Web [zalecane]**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="5ae9f-129">Usuń hello *wprowadzania usługi sieci Web* i *modułów wyjście usługi sieci Web* z eksperyment predykcyjny hello.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="5ae9f-130">W polu wyszukiwania składników hello wpisz eksportu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="5ae9f-131">Z listy wyników hello, Dodaj *eksportowanie danych* kanwy eksperymentu toohello modułu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="5ae9f-132">Połącz dane wyjściowe hello *Score Model* danych wejściowych hello modułu hello *eksportowanie danych* modułu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="5ae9f-133">W okienku właściwości, wybierz **bazy danych SQL Azure** w hello dane miejsce docelowe z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="5ae9f-134">W hello **nazwę serwera bazy danych**, **Nazwa bazy danych**, **nazwę konta użytkownika serwera**, i **hasło konta użytkownika serwera** wprowadź Witaj odpowiednie informacje dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="5ae9f-135">W hello **rozdzielana przecinkami lista kolumn toobe zapisane** wpisz oceniane etykiety.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="5ae9f-136">W hello **pole Nazwa tabeli danych**, wpisz dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="5ae9f-137">Jeśli nie istnieje tabela hello, utworzeniu po uruchomieniu eksperymentu hello lub usługi sieci web hello jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="5ae9f-138">W hello **rozdzielana przecinkami lista kolumn datatable** wpisz ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="5ae9f-139">Podczas pisania aplikacji czy wywołania hello usługi końcowego sieci web, możesz toospecify innej wejściowe tabeli zapytania lub docelowego w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="5ae9f-140">tooconfigure te wejściach i wyjściach, użyj hello parametry usługi sieci Web funkcji tooset hello *i zaimportuj dane* modułu *źródła danych* właściwości i hello *eksportowanie danych* tryb Właściwość docelowego danych.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="5ae9f-141">Aby uzyskać więcej informacji o parametry usługi sieci Web, zobacz hello [wpis parametry usługi sieci Web uczenie maszynowe Azure](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) na powitania Cortana Intelligence i Machine Learning blogu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="5ae9f-142">Witaj tooconfigure parametry usługi sieci Web hello importu zapytania i tabela docelowa hello:</span><span class="sxs-lookup"><span data-stu-id="5ae9f-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="5ae9f-143">W okienku właściwości hello hello *i zaimportuj dane* modułu, kliknij ikonę hello na powitania górnego prawego hello **zapytanie bazy danych** i wybierz pozycję **ustawić jako parametr usługi sieci web**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="5ae9f-144">W okienku właściwości hello hello *eksportowanie danych* modułu, kliknij ikonę hello na powitania górnego prawego hello **Nazwa tabeli danych** i wybierz pozycję **ustawić jako parametr usługi sieci web**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="5ae9f-145">U dołu hello hello *eksportowanie danych* okienka właściwości modułu, w hello **parametry usługi sieci Web** sekcji, kliknij przycisk zapytanie bazy danych i zmień jego nazwę zapytania.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="5ae9f-146">Kliknij przycisk **Nazwa tabeli danych** i zmień jego nazwę **tabeli**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="5ae9f-147">Gdy wszystko będzie gotowe, eksperymentu powinien wyglądać podobnie toohello po obrazu:</span><span class="sxs-lookup"><span data-stu-id="5ae9f-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Końcowe wygląd eksperymentu.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="5ae9f-149">Teraz można wdrożyć hello eksperymentu jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="5ae9f-150">Wdrażanie usługi sieci web hello</span><span class="sxs-lookup"><span data-stu-id="5ae9f-150">Deploy hello web service</span></span>
<span data-ttu-id="5ae9f-151">Można wdrożyć tooeither Classic lub Nowa usługa sieci web.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="5ae9f-152">Wdrażanie usługi sieci Web klasycznego</span><span class="sxs-lookup"><span data-stu-id="5ae9f-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="5ae9f-153">toodeploy w trybie klasycznym usługi sieci Web i utworzyć tooconsume aplikacji go:</span><span class="sxs-lookup"><span data-stu-id="5ae9f-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="5ae9f-154">U dołu hello hello roboczego eksperymentu kliknij przycisk Uruchom.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="5ae9f-155">Po zakończeniu uruchom powitania kliknij **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="5ae9f-156">Na pulpicie nawigacyjnym usługi sieci web hello zlokalizuj klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="5ae9f-157">Skopiuj i zapisz go toouse później.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="5ae9f-158">W hello **domyślny punkt końcowy** tabeli, kliknij przycisk hello **Batch Execution** łącze tooopen hello strona pomocy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="5ae9f-159">W programie Visual Studio Utwórz aplikację konsoli języka C#: **nowy** > **projektu** > **Visual C#** > **systemu Windows Klasyczny pulpit** > **konsoli aplikacji (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="5ae9f-160">Na powitania strona pomocy interfejsu API, Znajdź hello **przykładowy kod** sekcji u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="5ae9f-161">Skopiuj i Wklej hello C# przykładowy kod do pliku Program.cs i usunąć wszystkie odwołania toohello obiektu blob magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="5ae9f-162">Zaktualizuj wartość hello hello *apiKey* kluczem interfejsu API hello zapisany wcześniej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="5ae9f-163">Zlokalizuj hello żądania deklaracji i aktualizacji hello wartości parametry usługi sieci Web, które są przekazywane toohello *i zaimportuj dane* i *eksportowanie danych* modułów.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="5ae9f-164">W takim przypadku używać hello oryginalne zapytanie, ale definiuje nowej nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="5ae9f-165">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-165">Run hello application.</span></span> 

<span data-ttu-id="5ae9f-166">Po zakończeniu uruchom hello nowej tabeli jest dodawany toohello bazy danych zawierające hello oceniania wyników.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="5ae9f-167">Wdrożenie nowej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="5ae9f-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="5ae9f-168">toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="5ae9f-169">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="5ae9f-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="5ae9f-170">toodeploy jako nową usługę sieci Web i utworzyć tooconsume aplikacji go:</span><span class="sxs-lookup"><span data-stu-id="5ae9f-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="5ae9f-171">U dołu hello hello roboczego eksperymentu, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="5ae9f-172">Po zakończeniu uruchom powitania kliknij **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="5ae9f-173">Na stronie eksperymentu wdrażanie hello, wprowadź nazwę usługi sieci web i wybrać planu cenowego, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="5ae9f-174">Na powitania **szybkiego startu** kliknij przycisk **Consume**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="5ae9f-175">W hello **przykładowy kod** kliknij **partii**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="5ae9f-176">W programie Visual Studio Utwórz aplikację konsoli języka C#: **nowy** > **projektu** > **Visual C#** > **systemu Windows Klasyczny pulpit** > **konsoli aplikacji (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="5ae9f-177">Skopiuj i Wklej hello C# przykładowy kod w pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="5ae9f-178">Zaktualizuj wartość hello hello *apiKey* zmiennej z hello **klucza podstawowego** znajduje się w hello **zużycie podstawowe informacje o** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="5ae9f-179">Zlokalizuj hello *scoreRequest* deklaracji i aktualizacji wartości hello parametry usługi sieci Web, które są przekazywane toohello *i zaimportuj dane* i *eksportowanie danych* modułów.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="5ae9f-180">W takim przypadku używać hello oryginalne zapytanie, ale definiuje nowej nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="5ae9f-181">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5ae9f-181">Run hello application.</span></span> 

