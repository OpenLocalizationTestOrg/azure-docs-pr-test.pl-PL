---
title: "Rozwiązywanie problemów z ponownego trenowania usługi sieci web Azure Machine Learning klasycznego | Dokumentacja firmy Microsoft"
description: "Zidentyfikować i rozwiązać typowe problemy napotkano, gdy są ponownego trenowania modelu dla usługi sieci Web Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="2adea-103">Rozwiązywanie problemów z ponownego trenowania usługi sieci Web Azure Machine Learning klasycznego</span><span class="sxs-lookup"><span data-stu-id="2adea-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="2adea-104">Ponownego trenowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="2adea-104">Retraining overview</span></span>
<span data-ttu-id="2adea-105">Podczas wdrażania eksperyment predykcyjny jako usługę sieci web oceniania jest statyczny modelu.</span><span class="sxs-lookup"><span data-stu-id="2adea-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="2adea-106">Wraz ze wzrostem dostępności nowych danych lub w przypadku interfejsu API klienta ma własne dane modelu musi być retrained.</span><span class="sxs-lookup"><span data-stu-id="2adea-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="2adea-107">Aby uzyskać pełny przewodnik ponownego trenowania proces usługi sieci Web klasycznego, zobacz [Retrain Machine Learning modeli programowo](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="2adea-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="2adea-108">Proces ponownego trenowania</span><span class="sxs-lookup"><span data-stu-id="2adea-108">Retraining process</span></span>
<span data-ttu-id="2adea-109">Musisz ponownie ucz usługi sieci Web, należy dodać niektóre dodatkowe elementy:</span><span class="sxs-lookup"><span data-stu-id="2adea-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="2adea-110">Usługa sieci Web wdrożone z eksperymentów szkolenia.</span><span class="sxs-lookup"><span data-stu-id="2adea-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="2adea-111">Eksperyment musi mieć **wyjście usługi sieci Web** modułu dołączony do danych wyjściowych **Train Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="2adea-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Wyjście usługi sieci web należy dołączyć do modelu pociągu.][image1]
* <span data-ttu-id="2adea-113">Nowy punkt końcowy dodane do oceniania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2adea-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="2adea-114">Można dodać punktu końcowego, programowo przy użyciu przykładowy kod odwołuje się do modeli Retrain Machine Learning programowo tematu lub za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2adea-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="2adea-115">Następnie można przykładowy kod C# z strona pomocy interfejsu API usługi sieci Web szkolenia retrain modelu.</span><span class="sxs-lookup"><span data-stu-id="2adea-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="2adea-116">Po zostały obliczone wyniki i uzyskaniu je, należy zaktualizować trenowanego modelu oceniania usługi sieci web przy użyciu nowego punktu końcowego, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="2adea-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="2adea-117">Wszystkie elementy w miejscu główne kroki, które należy wykonać, aby ponownie ucz modelu są w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2adea-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="2adea-118">Wywoływanie usługi sieci Web szkolenia: wywołanie jest do wsadowe wykonywanie usługi (BES), nie żądanie odpowiedzi usługi (RR).</span><span class="sxs-lookup"><span data-stu-id="2adea-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="2adea-119">Przykładowy kod C# na stronie pomocy interfejsu API służy do wywoływania.</span><span class="sxs-lookup"><span data-stu-id="2adea-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="2adea-120">Znajdź wartości dla *BaseLocation*, *RelativeLocation*, i *SasBlobToken*: te wartości są zwracane w danych wyjściowych z połączenia z usługą sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="2adea-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="2adea-121">![Wyświetlanie danych wyjściowych ponownego trenowania próbki i wartości BaseLocation, RelativeLocation i SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="2adea-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="2adea-122">Zaktualizuj dodano punkt końcowy usługi sieci web oceniania za pomocą nowego trenowanego modelu: przy użyciu przykładowy kod podany w modelach Retrain Machine Learning programowo, zaktualizuj nowy punkt końcowy, dodane do oceniania modelu z nowo trenowanego modelu z Usługa sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="2adea-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="2adea-123">Typowych wąskich gardeł</span><span class="sxs-lookup"><span data-stu-id="2adea-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="2adea-124">Sprawdź, czy masz poprawny adres URL poprawki</span><span class="sxs-lookup"><span data-stu-id="2adea-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="2adea-125">POPRAWKA adres URL, którego używasz, musi być skojarzony z nowego oceniania punktu końcowego, dodane do oceniania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2adea-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="2adea-126">Istnieje wiele sposobów, aby uzyskać adres URL poprawki:</span><span class="sxs-lookup"><span data-stu-id="2adea-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="2adea-127">**Opcja 1: programowo**</span><span class="sxs-lookup"><span data-stu-id="2adea-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="2adea-128">Aby uzyskać poprawny adres URL poprawki:</span><span class="sxs-lookup"><span data-stu-id="2adea-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="2adea-129">Uruchom [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="2adea-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="2adea-130">Z danych wyjściowych AddEndpoint znaleźć *HelpLocation* wartości i skopiuj adres URL.</span><span class="sxs-lookup"><span data-stu-id="2adea-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation w danych wyjściowych próbki addEndpoint.][image2]
3. <span data-ttu-id="2adea-132">Wklej adres URL do przeglądarki, aby przejść do strony, która zawiera łącza pomocy dla usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2adea-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="2adea-133">Kliknij przycisk **aktualizacji zasobów** łącze, aby otworzyć stronę pomocy poprawki.</span><span class="sxs-lookup"><span data-stu-id="2adea-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="2adea-134">**Opcja 2: Użyj klasycznego portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="2adea-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="2adea-135">Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2adea-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2adea-136">Otwórz kartę uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="2adea-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="2adea-137">![Karta oparcie maszyny.][image4]</span><span class="sxs-lookup"><span data-stu-id="2adea-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="2adea-138">Następnie kliknij nazwę obszaru roboczego **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="2adea-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="2adea-139">Kliknij przycisk oceniania usługi sieci Web, którą użytkownik pracuje z.</span><span class="sxs-lookup"><span data-stu-id="2adea-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="2adea-140">(Jeśli nie zmienił domyślnej nazwy usługi sieci web, będą kończyć się [Exp oceniania.]).</span><span class="sxs-lookup"><span data-stu-id="2adea-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="2adea-141">Kliknij przycisk **dodać punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="2adea-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="2adea-142">Po dodaniu punktu końcowego, kliknij nazwę punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="2adea-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="2adea-143">Następnie kliknij przycisk **aktualizacji zasobów** otworzyć stosowania poprawek strony pomocy.</span><span class="sxs-lookup"><span data-stu-id="2adea-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="2adea-144">Jeśli dodano punkt końcowy z usługą sieci Web szkolenia zamiast predykcyjnej usługi sieci Web, zostanie wyświetlony następujący błąd, po kliknięciu **aktualizacji zasobów** łącza: Niestety, ale ta funkcja nie jest obsługiwana lub dostępna w tym kontekst.</span><span class="sxs-lookup"><span data-stu-id="2adea-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="2adea-145">Ta usługa sieci Web ma nie nadaje się do aktualizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="2adea-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="2adea-146">Firma Microsoft Przepraszamy za utrudnienia i działają na ułatwieniu ten przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="2adea-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Nowy punkt końcowy pulpitu nawigacyjnego.][image3]

<span data-ttu-id="2adea-148">Strona pomocy poprawki zawiera adres URL poprawka, należy użyć i udostępnia przykładowy kod, którego można użyć w celu wywołania go.</span><span class="sxs-lookup"><span data-stu-id="2adea-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![Adres URL poprawki.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="2adea-150">Sprawdź, czy aktualizujesz właściwego punktu końcowego oceniania</span><span class="sxs-lookup"><span data-stu-id="2adea-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="2adea-151">Nie poprawka usługę sieci Web szkolenia: operacja poprawki musi zostać wykonana na oceniania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2adea-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="2adea-152">Poprawka nie jest domyślny punkt końcowy usługi sieci Web: operacja poprawki musi zostać wykonana na nowe oceniania końcowy usługi sieci Web dodany.</span><span class="sxs-lookup"><span data-stu-id="2adea-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="2adea-153">Możesz sprawdzić, które usługi sieci Web punktu końcowego jest w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2adea-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="2adea-154">Upewnij się, że punkt końcowy jest dodawany do predykcyjnej usługi sieci Web nie usługę sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="2adea-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="2adea-155">Jeśli zostały poprawnie wdrożone zarówno szkolenia, jak i usługi sieci Web predykcyjnej, powinny pojawić się dwa oddzielne usług sieci Web na liście.</span><span class="sxs-lookup"><span data-stu-id="2adea-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="2adea-156">Predykcyjnej usługi sieci Web powinien kończyć się "[exp predykcyjnych.]".</span><span class="sxs-lookup"><span data-stu-id="2adea-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="2adea-157">Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2adea-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2adea-158">Otwórz kartę uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="2adea-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="2adea-159">![Obszaru roboczego uczenia maszyny interfejsu użytkownika.][image4]</span><span class="sxs-lookup"><span data-stu-id="2adea-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="2adea-160">Wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="2adea-160">Select your workspace.</span></span>
4. <span data-ttu-id="2adea-161">Kliknij przycisk **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="2adea-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="2adea-162">Wybierz usługę sieci Web predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="2adea-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="2adea-163">Sprawdź, czy nowy punkt końcowy został dodany do usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2adea-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="2adea-164">Sprawdź obszar roboczy usługi sieci web jest w celu zapewnienia, że jest poprawny region</span><span class="sxs-lookup"><span data-stu-id="2adea-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="2adea-165">Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2adea-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2adea-166">Uczenie maszynowe, wybierz z menu.</span><span class="sxs-lookup"><span data-stu-id="2adea-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="2adea-167">![Machine learning region interfejsu użytkownika.][image4]</span><span class="sxs-lookup"><span data-stu-id="2adea-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="2adea-168">Sprawdź lokalizację swojego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="2adea-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
