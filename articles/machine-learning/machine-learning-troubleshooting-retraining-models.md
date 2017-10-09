---
title: "Usługa sieci web aaaTroubleshoot ponownego trenowania klasycznego Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Zidentyfikować i rozwiązać typowe problemy napotkano, gdy są ponownego trenowania hello modelu dla usługi sieci Web Azure Machine Learning."
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="268e5-103">Rozwiązywanie problemów z hello ponownego trenowania usługi sieci Web Azure Machine Learning klasycznego</span><span class="sxs-lookup"><span data-stu-id="268e5-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="268e5-104">Ponownego trenowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="268e5-104">Retraining overview</span></span>
<span data-ttu-id="268e5-105">Podczas wdrażania eksperyment predykcyjny jako usługę sieci web oceniania jest statyczny modelu.</span><span class="sxs-lookup"><span data-stu-id="268e5-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="268e5-106">Wraz ze wzrostem dostępności nowych danych lub w przypadku hello konsumenta hello interfejsu API ma własne dane modelu hello musi toobe retrained.</span><span class="sxs-lookup"><span data-stu-id="268e5-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="268e5-107">Aby uzyskać pełny przewodnik hello ponownego trenowania procesu usługi sieci Web klasycznego, zobacz [Retrain Machine Learning modeli programowo](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="268e5-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="268e5-108">Proces ponownego trenowania</span><span class="sxs-lookup"><span data-stu-id="268e5-108">Retraining process</span></span>
<span data-ttu-id="268e5-109">Jeśli potrzebujesz hello tooretrain usługi sieci Web, należy dodać niektóre dodatkowe elementy:</span><span class="sxs-lookup"><span data-stu-id="268e5-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="268e5-110">Wdrożone z hello eksperyment uczenia usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="268e5-111">musi mieć eksperymentu Hello **wyjście usługi sieci Web** toohello dane wyjściowe hello podłączony moduł **Train Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="268e5-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Dołącz modelu train toohello dane wyjściowe hello usług sieci web.][image1]
* <span data-ttu-id="268e5-113">Nowy punkt końcowy dodać tooyour oceniania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="268e5-114">Można dodać punktu końcowego hello programowo przy użyciu hello przykładowego kodu, do którego odwołuje się hello Retrain Machine Learning modeli tematu lub za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="268e5-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="268e5-115">Następnie można użyć hello próbki kodu C# z modelu tooretrain strony pomocy interfejsu API usługi hello szkolenia sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="268e5-116">Po zostały obliczone wyniki hello i uzyskaniu je, należy zaktualizować hello uczonego modelu oceniania usługi sieci web przy użyciu hello nowy punkt końcowy, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="268e5-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="268e5-117">Z wszystkich elementów hello w miejscu hello główne kroki należy wykonać tooretrain hello modelu są następujące:</span><span class="sxs-lookup"><span data-stu-id="268e5-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="268e5-118">Wywołanie usługi sieci Web szkolenia hello: wywołanie hello jest toohello usługi wykonywania wsadowego (BES), nie hello żądanie odpowiedzi usługi (RR).</span><span class="sxs-lookup"><span data-stu-id="268e5-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="268e5-119">Można użyć hello próbki C# kodu na powitania interfejsu API pomocy strony toomake hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="268e5-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="268e5-120">Znajdź hello wartości dla hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken*: te wartości są zwracane w danych wyjściowych hello z toohello Twojego wywołania szkoleń w sieci Web Usługa.</span><span class="sxs-lookup"><span data-stu-id="268e5-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="268e5-121">![Wyświetlanie danych wyjściowych hello hello ponownego trenowania próbki i hello BaseLocation, RelativeLocation i SasBlobToken wartości.][image6]</span><span class="sxs-lookup"><span data-stu-id="268e5-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="268e5-122">Hello aktualizacji dodano punkt końcowy z hello nowych oceniania usługi sieci web z hello uczenia modelu: przy użyciu hello przykładowy kod podany w hello Retrain Machine Learning modeli programowo, zaktualizuj nowy punkt końcowy hello dodane toohello nowo oceniania modelu z hello uczonego modelu z hello usługi sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="268e5-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="268e5-123">Typowych wąskich gardeł</span><span class="sxs-lookup"><span data-stu-id="268e5-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="268e5-124">Sprawdź toosee, jeśli masz hello Popraw poprawki</span><span class="sxs-lookup"><span data-stu-id="268e5-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="268e5-125">Hello poprawka używasz adres URL musi być hello, co skojarzony z hello nowego punktu końcowego oceniania dodaniu toohello oceniania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="268e5-126">Istnieje wiele sposobów tooobtain hello poprawka adresu URL:</span><span class="sxs-lookup"><span data-stu-id="268e5-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="268e5-127">**Opcja 1: programowo**</span><span class="sxs-lookup"><span data-stu-id="268e5-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="268e5-128">Witaj tooget Popraw poprawki:</span><span class="sxs-lookup"><span data-stu-id="268e5-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="268e5-129">Uruchom hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="268e5-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="268e5-130">Z danych wyjściowych hello AddEndpoint, Znajdź hello *HelpLocation* wartość i skopiuj adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="268e5-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation w danych wyjściowych hello hello addEndpoint próbki.][image2]
3. <span data-ttu-id="268e5-132">Wklej adres URL hello na stronę tooa toonavigate przeglądarki łącza pomocy hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="268e5-133">Kliknij przycisk hello **aktualizacji zasobów** strona pomocy poprawki hello tooopen łącza.</span><span class="sxs-lookup"><span data-stu-id="268e5-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="268e5-134">**Opcja 2: Hello Użyj klasycznego portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="268e5-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="268e5-135">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="268e5-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="268e5-136">Hello Otwórz kartę uczenia maszynowego. ![Karta oparcie maszyny.][image4]</span><span class="sxs-lookup"><span data-stu-id="268e5-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="268e5-137">Następnie kliknij nazwę obszaru roboczego **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="268e5-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="268e5-138">Kliknij przycisk hello oceniania usługi sieci Web, którą użytkownik pracuje z.</span><span class="sxs-lookup"><span data-stu-id="268e5-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="268e5-139">(Jeśli nie jest zmodyfikowała hello domyślnej nazwy usługi sieci web hello, będą kończyć się [Exp oceniania.]).</span><span class="sxs-lookup"><span data-stu-id="268e5-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="268e5-140">Kliknij przycisk **dodać punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="268e5-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="268e5-141">Po dodaniu punktu końcowego powitania kliknij nazwę punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="268e5-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="268e5-142">Następnie kliknij przycisk **aktualizacji zasobów** tooopen hello stosowania poprawek strony pomocy.</span><span class="sxs-lookup"><span data-stu-id="268e5-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="268e5-143">Jeśli dodano hello toohello punkt końcowy usługi sieci Web szkolenia zamiast hello predykcyjnej usługi sieci Web, zostanie wyświetlony następujący błąd, po kliknięciu hello hello **aktualizacji zasobów** łącza: Niestety, ale ta funkcja nie jest obsługiwana lub niedostępne w tym kontekście.</span><span class="sxs-lookup"><span data-stu-id="268e5-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="268e5-144">Ta usługa sieci Web ma nie nadaje się do aktualizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="268e5-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="268e5-145">Firma Microsoft Przepraszamy za niedogodności hello i działają na ułatwieniu ten przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="268e5-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Nowy punkt końcowy pulpitu nawigacyjnego.][image3]

<span data-ttu-id="268e5-147">Strona pomocy poprawki Hello zawiera hello PATCH musi używać adresu URL i udostępnia przykładowy kod, można użyć toocall go.</span><span class="sxs-lookup"><span data-stu-id="268e5-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![Adres URL poprawki.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="268e5-149">Aktualizacja punktu końcowego oceniania poprawne hello toosee wyboru</span><span class="sxs-lookup"><span data-stu-id="268e5-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="268e5-150">Nie poprawka hello usługi sieci Web szkolenia: hello poprawki operacja musi zostać wykonana na powitania oceniania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="268e5-151">Nie poprawka hello domyślny punkt końcowy usługi sieci Web: hello poprawki operacja musi zostać wykonana na powitania oceniania nowy punkt końcowy usługi sieci Web, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="268e5-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="268e5-152">Możesz sprawdzić, które hello końcowy usługi sieci Web jest włączone zaproszonych hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="268e5-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="268e5-153">Upewnij się, że w przypadku dodawania hello toohello punkt końcowy usługi sieci Web predykcyjnych, hello usługi sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="268e5-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="268e5-154">Jeśli zostały poprawnie wdrożone zarówno szkolenia, jak i usługi sieci Web predykcyjnej, powinny pojawić się dwa oddzielne usług sieci Web na liście.</span><span class="sxs-lookup"><span data-stu-id="268e5-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="268e5-155">Hello predykcyjnej usługi sieci Web powinien kończyć się "[exp predykcyjnych.]".</span><span class="sxs-lookup"><span data-stu-id="268e5-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="268e5-156">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="268e5-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="268e5-157">Hello Otwórz kartę uczenia maszynowego. ![Obszaru roboczego uczenia maszyny interfejsu użytkownika.][image4]</span><span class="sxs-lookup"><span data-stu-id="268e5-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="268e5-158">Wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="268e5-158">Select your workspace.</span></span>
4. <span data-ttu-id="268e5-159">Kliknij przycisk **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="268e5-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="268e5-160">Wybierz usługę sieci Web predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="268e5-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="268e5-161">Sprawdź, czy nowy punkt końcowy został dodany toohello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="268e5-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="268e5-162">Sprawdź hello roboczy usługi sieci web w tooensure jest poprawny region hello</span><span class="sxs-lookup"><span data-stu-id="268e5-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="268e5-163">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="268e5-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="268e5-164">Wybierz hello menu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="268e5-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="268e5-165">![Machine learning region interfejsu użytkownika.][image4]</span><span class="sxs-lookup"><span data-stu-id="268e5-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="268e5-166">Sprawdź lokalizację hello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="268e5-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
