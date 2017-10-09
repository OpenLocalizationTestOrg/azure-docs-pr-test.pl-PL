---
title: "usługi sieci web aaaRetrain istniejące predykcyjnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aktualizacja i tooretrain modelu hello sieci web usługi toouse hello nowo uczonego modelu w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="e49e0-103">Ponownie ucz istniejącej usługi sieci web predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="e49e0-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="e49e0-104">W tym dokumencie opisano hello ponownego trenowania proces hello następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="e49e0-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="e49e0-105">Masz eksperyment uczenia i eksperyment predykcyjny, która została wdrożona jako usługi sieci web operationalized.</span><span class="sxs-lookup"><span data-stu-id="e49e0-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="e49e0-106">Masz nowe dane, które mają tooperform toouse usługi sieci web predykcyjnej jego oceniania.</span><span class="sxs-lookup"><span data-stu-id="e49e0-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="e49e0-107">toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="e49e0-108">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e49e0-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="e49e0-109">Począwszy od istniejącej usługi sieci web, a eksperymentów, należy toofollow następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e49e0-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="e49e0-110">Model hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e49e0-110">Update hello model.</span></span>
   1. <span data-ttu-id="e49e0-111">Modyfikowanie użytkownika tooallow eksperymentu uczenia dla sieci web usługi wejścia i wyjścia.</span><span class="sxs-lookup"><span data-stu-id="e49e0-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="e49e0-112">Wdróż eksperyment uczenia hello jako usługę sieci web ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="e49e0-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="e49e0-113">Użyj eksperyment uczenia hello usługi wykonywania wsadowego (BES) tooretrain hello modelu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="e49e0-114">Użyj hello Azure Machine Learning PowerShell polecenia cmdlet tooupdate hello predykcyjnej eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="e49e0-115">Zaloguj się tooyour konta usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e49e0-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="e49e0-116">Pobierz definicję usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="e49e0-117">Eksportowanie definicji usługi sieci web hello formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="e49e0-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="e49e0-118">Aktualizacja hello toohello ilearner obiekt blob odwołania w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e49e0-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="e49e0-119">Zaimportuj hello JSON do definicji usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e49e0-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="e49e0-120">Zaktualizuj usługę sieci web hello z nowej definicji usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e49e0-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="e49e0-121">Wdrażanie eksperyment uczenia hello</span><span class="sxs-lookup"><span data-stu-id="e49e0-121">Deploy hello training experiment</span></span>
<span data-ttu-id="e49e0-122">toodeploy hello eksperyment uczenia ponownego trenowania Usługa sieci web, należy dodać modelu usług sieci web wejściami i wyjściami toohello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="e49e0-123">Łącząc *wyjście usługi sieci Web* modułu toohello eksperymentu  *[Train Model] [ train-model]*  moduł, możesz włączyć hello szkolenia eksperymentu tooproduce nową uczenia modelu używanego w eksperymencie predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="e49e0-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="e49e0-124">Jeśli masz *Evaluate Model* moduł, możesz również dołączyć wyniki oceny hello tooget wyjście usługi sieci web jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="e49e0-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="e49e0-125">tooupdate eksperymentu uczenia:</span><span class="sxs-lookup"><span data-stu-id="e49e0-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="e49e0-126">Połącz *wejściowego usługi sieci Web* modułu tooyour danych wejściowych (na przykład *Clean Missing Data* modułu).</span><span class="sxs-lookup"><span data-stu-id="e49e0-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="e49e0-127">Zazwyczaj mają tooensure przetwarzanego w danych wejściowych hello takie same jak oryginalne dane szkolenia.</span><span class="sxs-lookup"><span data-stu-id="e49e0-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="e49e0-128">Połącz *wyjście usługi sieci Web* dane wyjściowe toohello modułu z *Train Model* modułu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="e49e0-129">Jeśli masz *Evaluate Model* modułu, a wyniki oceny hello toooutput, Połącz *wyjście usługi sieci Web* dane wyjściowe toohello modułu z *Evaluate Model* Moduł.</span><span class="sxs-lookup"><span data-stu-id="e49e0-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="e49e0-130">Uruchamianie eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-130">Run your experiment.</span></span>

<span data-ttu-id="e49e0-131">Następnie należy wdrożyć eksperyment uczenia hello jako usługę sieci web, który spowoduje utworzenie uczonego modelu i wyniki oceny modelu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="e49e0-132">U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web**, a następnie wybierz **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="e49e0-133">portal usługi sieci Web systemu Azure Machine Learning Hello otwiera toohello **wdrażanie usługi sieci Web** strony.</span><span class="sxs-lookup"><span data-stu-id="e49e0-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="e49e0-134">Wpisz nazwę usługi sieci web, wybierz plan płatności, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="e49e0-135">Metody wykonywania wsadowego usługi hello można używać tylko do tworzenia modeli przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="e49e0-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="e49e0-136">Ponownie ucz modelu hello nowymi danymi za pomocą usługi BES</span><span class="sxs-lookup"><span data-stu-id="e49e0-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="e49e0-137">W tym przykładzie używamy C# hello toocreate ponownego trenowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e49e0-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="e49e0-138">Umożliwia także Python lub R tooaccomplish kod przykładowy tego zadania.</span><span class="sxs-lookup"><span data-stu-id="e49e0-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="e49e0-139">Witaj toocall ponownego trenowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="e49e0-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="e49e0-140">Tworzenie aplikacji konsolowej C# w programie Visual Studio: **nowy** > **projektu** > **Visual C#** > **Windows Desktop klasycznego** > **aplikacji konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="e49e0-141">Zaloguj się toohello portal usługi sieci Web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e49e0-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="e49e0-142">Kliknij opcję usługi sieci web hello, z którymi pracujesz.</span><span class="sxs-lookup"><span data-stu-id="e49e0-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="e49e0-143">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-143">Click **Consume**.</span></span>
5. <span data-ttu-id="e49e0-144">U dołu hello hello **Consume** strony w hello **przykładowy kod** kliknij **partii**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="e49e0-145">Skopiuj hello próbki kodu C# dla wykonywania wsadowego i wklej go do pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="e49e0-146">Upewnij się, że w tej przestrzeni nazw hello pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="e49e0-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="e49e0-147">Dodaj hello pakiet NuGet Microsoft.AspNet.WebApi.Client, jak określono w komentarzach hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="e49e0-148">tooadd tooMicrosoft.WindowsAzure.Storage.dll odwołania hello, być może konieczne tooinstall hello [biblioteki klienta usługi Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="e49e0-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="e49e0-149">Witaj Poniższy zrzut ekranu przedstawia hello **Consume** w portalu usługi sieci Web systemu Azure Machine Learning hello na stronie.</span><span class="sxs-lookup"><span data-stu-id="e49e0-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Korzystanie ze strony][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="e49e0-151">Zaktualizuj hello apikey deklaracji</span><span class="sxs-lookup"><span data-stu-id="e49e0-151">Update hello apikey declaration</span></span>
<span data-ttu-id="e49e0-152">Zlokalizuj hello **apikey** deklaracji:</span><span class="sxs-lookup"><span data-stu-id="e49e0-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="e49e0-153">W hello **zużycie podstawowe informacje o** sekcji hello **Consume** strony Znajdź klucz podstawowy hello i skopiuj go toohello **apikey** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="e49e0-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="e49e0-154">Zaktualizuj informacje magazynie Azure hello</span><span class="sxs-lookup"><span data-stu-id="e49e0-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="e49e0-155">Hello BES przykładowy kod operacji przekazywania plików z tooAzure dysk lokalny (na przykład "C:\temp\CensusIpnput.csv"), magazynu, procesy i zapisuje hello wyników wstecz tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="e49e0-156">tooupdate hello Azure Storage informacji, należy pobrać hello konta magazynu, że nazwa, klucz i kontenera informacji dla konta magazynu z hello klasycznego portalu Azure, a następnie correspondi hello aktualizacji po uruchomieniu eksperymentu, Witaj, co przepływ pracy powinny być podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e49e0-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Wynikowa przepływu pracy po uruchomieniu][4]<span data-ttu-id="e49e0-158">wartości ng w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-158">ng values in hello code.</span></span>

1. <span data-ttu-id="e49e0-159">Zaloguj się toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e49e0-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="e49e0-160">W kolumnie nawigacji po lewej stronie powitania kliknij **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="e49e0-161">Z listy hello kont magazynu wybierz jeden toostore hello retrained modelu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="e49e0-162">U dołu hello hello strony, kliknij przycisk **Zarządzaj kluczami dostępu**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="e49e0-163">Skopiuj i Zapisz hello **podstawowy klucz dostępu** hello Zamknij okno dialogowe i.</span><span class="sxs-lookup"><span data-stu-id="e49e0-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="e49e0-164">U góry hello hello strony, kliknij przycisk **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="e49e0-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="e49e0-165">Wybierz istniejącego kontenera, lub Utwórz nową i Zapisz nazwę hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="e49e0-166">Zlokalizuj hello *StorageAccountName*, *StorageAccountKey*, i *StorageContainerName* deklaracje i Aktualizuj hello wartości zapisane w portalu klasycznym hello .</span><span class="sxs-lookup"><span data-stu-id="e49e0-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="e49e0-167">Ponadto musisz zapewnić, że tego pliku wejściowego hello jest dostępna w lokalizacji hello w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="e49e0-168">Określ lokalizację danych wyjściowych hello</span><span class="sxs-lookup"><span data-stu-id="e49e0-168">Specify hello output location</span></span>
<span data-ttu-id="e49e0-169">Po określeniu lokalizacji wyjściowej hello w ładunku żądania hello hello rozszerzenie pliku hello, który jest określony w *RelativeLocation* muszą być określone jako `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="e49e0-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="e49e0-170">Zobacz poniższy przykład hello:</span><span class="sxs-lookup"><span data-stu-id="e49e0-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="e49e0-171">Witaj poniżej przedstawiono przykład ponownego trenowania dane wyjściowe: ![ponownego trenowania danych wyjściowych][6]</span><span class="sxs-lookup"><span data-stu-id="e49e0-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="e49e0-172">Witaj ponownego trenowania wyników oceny</span><span class="sxs-lookup"><span data-stu-id="e49e0-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="e49e0-173">Po uruchomieniu aplikacji hello hello danych wyjściowych zawiera adres URL hello i tokenu sygnatury dostępu współdzielonego, który wyniki oceny hello tooaccess niezbędne są.</span><span class="sxs-lookup"><span data-stu-id="e49e0-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="e49e0-174">Można wyświetlić wyniki wydajności hello modelu hello retrained łącząc hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik Aby uzyskać *output2* (jak pokazano w poprzednim ponownego trenowania obrazu wyjściowego hello) i wklejanie hello pełny adres URL do hello na pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="e49e0-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="e49e0-175">Witaj toodetermine wyników należy sprawdzić, czy nowo uczonego modelu hello wykonuje również za mało hello tooreplace jedną istniejącą.</span><span class="sxs-lookup"><span data-stu-id="e49e0-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="e49e0-176">Kopiuj hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik.</span><span class="sxs-lookup"><span data-stu-id="e49e0-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="e49e0-177">Ponownie ucz hello usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="e49e0-177">Retrain hello web service</span></span>
<span data-ttu-id="e49e0-178">Gdy retrain nową usługę sieci web, należy zaktualizować hello predykcyjnego modelu usług sieci web definicji tooreference hello nowe przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="e49e0-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="e49e0-179">definicji usługi sieci web Hello jest wewnętrznej reprezentacji hello uczonego modelu hello usługi sieci web i nie można bezpośrednio modyfikować.</span><span class="sxs-lookup"><span data-stu-id="e49e0-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="e49e0-180">Upewnij się, czy są pobierania definicji usługi sieci web hello predykcyjnej eksperymentu, a nie eksperyment uczenia.</span><span class="sxs-lookup"><span data-stu-id="e49e0-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="e49e0-181">Zaloguj się tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e49e0-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="e49e0-182">Konto platformy Azure w środowisku PowerShell hello tooyour musi pierwszy raz logujesz się przy użyciu hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49e0-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="e49e0-183">Pobierz obiekt definicji usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="e49e0-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="e49e0-184">Następnie Pobierz obiekt definicji usługi sieci Web hello przez wywołanie hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49e0-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="e49e0-185">toodetermine hello Nazwa grupy zasobów z istniejącej usługi sieci web, uruchom polecenie cmdlet Get-AzureRmMlWebService hello bez żadnych parametrów toodisplay hello sieci web usług w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e49e0-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="e49e0-186">Zlokalizuj hello usługi sieci web, a następnie sprawdź jej identyfikatora usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="e49e0-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="e49e0-187">Witaj Nazwa grupy zasobów hello jest czwartym elementem hello w identyfikatorze hello zaraz po hello *resourceGroups* elementu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="e49e0-188">W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="e49e0-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="e49e0-189">Alternatywnie toodetermine hello Nazwa grupy zasobów istniejącej usługi sieci web, należy się zalogować w portalu usługi sieci Web systemu Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="e49e0-190">Wybierz usługę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-190">Select hello web service.</span></span> <span data-ttu-id="e49e0-191">Nazwa grupy zasobów Hello jest hello elementu piątym powitania adres URL usługi sieci web hello, zaraz po hello *resourceGroups* elementu.</span><span class="sxs-lookup"><span data-stu-id="e49e0-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="e49e0-192">W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="e49e0-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="e49e0-193">Eksport obiektu definicji usługi sieci Web hello w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="e49e0-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="e49e0-194">Definicja hello toomodify hello uczonego modelu toouse hello nowo uczenia modelu, należy najpierw użyć hello [AzureRmMlWebService eksportu](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport polecenia cmdlet go plik tooa formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="e49e0-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="e49e0-195">Obiekt blob ilearner toohello odwołania hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="e49e0-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="e49e0-196">Zasoby hello odszukaj hello [uczonego modelu] hello aktualizacji *uri* wartość hello *locationInfo* węzeł z identyfikatora URI obiektu hello ilearner blob hello.</span><span class="sxs-lookup"><span data-stu-id="e49e0-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="e49e0-197">Witaj identyfikatora URI jest generowany przez połączenie hello *BaseLocation* i hello *RelativeLocation* z wyników hello hello BES Wywołanie ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="e49e0-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="e49e0-198">Importowanie hello JSON do obiektu definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e49e0-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="e49e0-199">Należy użyć hello [AzureRmMlWebService importu](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert polecenia cmdlet zmodyfikowany plik JSON do obiektu definicji usługi sieci Web z użyciem eksperymentu predicative hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e49e0-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="e49e0-200">Usługi sieci web hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="e49e0-200">Update hello web service</span></span>
<span data-ttu-id="e49e0-201">Na koniec użyj hello [AzureRmMlWebService aktualizacji](https://msdn.microsoft.com/library/azure/mt767922.aspx) eksperyment predykcyjny hello tooupdate polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e49e0-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
