---
title: "Dodatek aaaExcel dla usługi Machine Learning Web | Dokumentacja firmy Microsoft"
description: "Jak toouse Azure Machine Learning w sieci Web usług bezpośrednio w programie Excel bez pisania żadnego kodu."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="aa99e-103">Dodatki programu Excel do usług sieci Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa99e-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="aa99e-104">Excel umożliwia łatwe toocall usług sieci web bezpośrednio bez hello muszą toowrite żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="aa99e-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="aa99e-105">Kroki tooUse usługi sieci web istniejące w hello skoroszytu</span><span class="sxs-lookup"><span data-stu-id="aa99e-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="aa99e-106">Otwórz hello [przykładowy plik programu Excel](http://aka.ms/amlexcel-sample-2), który zawiera hello dodatek programu Excel i dane dotyczące osób na hello Titanic.</span><span class="sxs-lookup"><span data-stu-id="aa99e-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="aa99e-107">Wybierz usługę sieci web hello kliknięciem — "Titanic predykcyjne renty (przykład dodatku Excel) [Wynik]" w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="aa99e-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Wybierz usługę sieci Web][01]
3. <span data-ttu-id="aa99e-109">Powoduje to przejście toohello **Predict** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aa99e-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="aa99e-110">Ten skoroszyt zawiera już dane przykładowe, ale dla pustego skoroszytu można zaznaczyć komórkę w programie Excel i kliknij przycisk **użyj przykładowych danych**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="aa99e-111">Wybierz dane hello z nagłówkami i kliknij ikonę zakres danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="aa99e-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="aa99e-112">Upewnij się, że zaznaczone jest pole "dane ma nagłówki" hello.</span><span class="sxs-lookup"><span data-stu-id="aa99e-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="aa99e-113">W obszarze **dane wyjściowe**, wprowadź numer komórki hello, w której mają hello toobe danych wyjściowych, na przykład "H1" w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="aa99e-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="aa99e-114">Kliknij przycisk **prognozowania**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-114">Click **Predict**.</span></span>
   
    ![Przewidywanie sekcji][02]

<span data-ttu-id="aa99e-116">Wdrażanie usługi sieci web, lub użyj istniejącej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="aa99e-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="aa99e-117">Aby uzyskać więcej informacji na temat wdrażania usługi sieci web, zobacz [wskazówki krok 5: Wdrażanie usługi sieci Web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="aa99e-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="aa99e-118">Pobierz hello klucza interfejsu API usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="aa99e-118">Get hello API key for your web service.</span></span> <span data-ttu-id="aa99e-119">Miejsce można wykonać tej akcji zależy czy opublikowane usługi sieci web klasycznego uczenia maszynowego usługi sieci web uczenie maszynowe nowe.</span><span class="sxs-lookup"><span data-stu-id="aa99e-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="aa99e-120">**Użyj usługi sieci web klasycznego**</span><span class="sxs-lookup"><span data-stu-id="aa99e-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="aa99e-121">W usłudze Machine Learning Studio, kliknij przycisk hello **usług sieci WEB** sekcji w okienku po lewej stronie powitania, a następnie wybierz hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="aa99e-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Wybierz Studio usługi sieci Web][04]
2. <span data-ttu-id="aa99e-123">Skopiuj klucz interfejsu API hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="aa99e-123">Copy hello API key for hello web service.</span></span>
   
    ![Klucz interfejsu API Studio][05]
3. <span data-ttu-id="aa99e-125">Na powitania **pulpitu NAWIGACYJNEGO** hello usługi sieci web, kliknij pozycję hello **żądanie/odpowiedź** łącza.</span><span class="sxs-lookup"><span data-stu-id="aa99e-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="aa99e-126">Wyszukaj hello **przez identyfikator URI żądania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aa99e-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="aa99e-127">Skopiuj i Zapisz adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="aa99e-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="aa99e-128">Teraz jest możliwe toosign do hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu tooobtain klucza hello interfejsu API usługi sieci web uczenie maszynowe klasycznego.</span><span class="sxs-lookup"><span data-stu-id="aa99e-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="aa99e-129">**Użyj nowej usługi sieci web**</span><span class="sxs-lookup"><span data-stu-id="aa99e-129">**Use a New web service**</span></span>

1. <span data-ttu-id="aa99e-130">W hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu, kliknij przycisk **usług sieci Web**, wybierz opcję usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="aa99e-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="aa99e-131">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-131">Click **Consume**.</span></span>
3. <span data-ttu-id="aa99e-132">Wyszukaj hello **zużycie podstawowe informacje o** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aa99e-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="aa99e-133">Skopiuj i Zapisz hello **klucza podstawowego** i hello **żądań i odpowiedzi** adresu URL.</span><span class="sxs-lookup"><span data-stu-id="aa99e-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="aa99e-134">Kroki tooAdd nową usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="aa99e-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="aa99e-135">Wdrażanie usługi sieci web, lub użyj istniejącej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="aa99e-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="aa99e-136">Aby uzyskać więcej informacji na temat wdrażania usługi sieci web, zobacz [wskazówki krok 5: Wdrażanie usługi sieci Web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="aa99e-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="aa99e-137">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-137">Click **Consume**.</span></span>
3. <span data-ttu-id="aa99e-138">Wyszukaj hello **zużycie podstawowe informacje o** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aa99e-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="aa99e-139">Skopiuj i Zapisz hello **klucza podstawowego** i hello **żądań i odpowiedzi** adresu URL.</span><span class="sxs-lookup"><span data-stu-id="aa99e-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="aa99e-140">W programie Excel Przejdź toohello **usług sieci Web** sekcji (w hello **Predict** kliknij hello strzałkę Wstecz toogo toohello listę usług sieci web).</span><span class="sxs-lookup"><span data-stu-id="aa99e-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Przejdź tooWeb wybór usługi][03]
5. <span data-ttu-id="aa99e-142">Kliknij przycisk **Dodaj usługę sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="aa99e-143">Wklej adres URL hello do hello etykietą pole tekstowe dodatek programu Excel **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="aa99e-144">Wklej klucz interfejsu API/podstawowy hello hello pole tekstowe z etykietą **klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="aa99e-145">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="aa99e-145">Click **Add**.</span></span>
   
    ![Adres URL i klucz API usługi sieci Web klasycznego.][06]
9. <span data-ttu-id="aa99e-147">usługi sieci web hello toouse, wykonaj hello poprzedzających kierunków, "Kroki tooUse istniejące sieci web usługi."</span><span class="sxs-lookup"><span data-stu-id="aa99e-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="aa99e-148">Udostępnianie skoroszytu</span><span class="sxs-lookup"><span data-stu-id="aa99e-148">Sharing Your Workbook</span></span>
<span data-ttu-id="aa99e-149">Czy zapisać skoroszyt, klucz interfejsu API/podstawowy hello hello usług sieci web, które zostały dodane również jest zapisywane.</span><span class="sxs-lookup"><span data-stu-id="aa99e-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="aa99e-150">Oznacza to, że skoroszytu hello powinien udostępniać tylko dla osób zaufanych.</span><span class="sxs-lookup"><span data-stu-id="aa99e-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="aa99e-151">Pytania w hello następujących sekcji komentarza lub na naszych [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="aa99e-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
