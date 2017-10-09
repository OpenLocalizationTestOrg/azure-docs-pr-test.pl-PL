---
title: "AAA(deprecated) publikowania machine learning tooAzure usługi sieci web portalu Marketplace | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Jak toopublish Twojego toohello Usługa sieci Web systemu Azure Machine Learning portalu Azure Marketplace"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="9c661-103">(przestarzałe) Publikowanie toohello Usługa sieci Web systemu Azure Machine Learning portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9c661-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="9c661-104">DataMarket i usług danych jest wycofana i istniejące subskrypcje zostaną wycofane i anulowane uruchamianie 3/31/2017 r.</span><span class="sxs-lookup"><span data-stu-id="9c661-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="9c661-105">W związku z tym w tym artykule jest przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="9c661-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="9c661-106">Alternatywnie, można opublikować toohello eksperymentów z uczenia maszynowego [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) asysty hello hello danych nauki społeczności.</span><span class="sxs-lookup"><span data-stu-id="9c661-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="9c661-107">Aby uzyskać więcej informacji, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="9c661-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="9c661-108">Hello Azure Marketplace udostępnia możliwości hello usług sieci web Azure Machine Learning toopublish płatnej, lub zwolnij usługi do użycia przez klientów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="9c661-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="9c661-109">Ten artykuł zawiera omówienie procesu z łącza tooguidelines tooget, który został uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="9c661-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="9c661-110">Za pomocą tego procesu, można udostępnić swoje usługi sieci web dla innych tooconsume deweloperów w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="9c661-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="9c661-111">Omówienie procesu publikowania hello</span><span class="sxs-lookup"><span data-stu-id="9c661-111">Overview of hello publishing process</span></span>
<span data-ttu-id="9c661-112">Hello poniżej przedstawiono kroki publikowania tooAzure usługi sieci web uczenie maszynowe Azure Marketplace hello:</span><span class="sxs-lookup"><span data-stu-id="9c661-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="9c661-113">Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)</span><span class="sxs-lookup"><span data-stu-id="9c661-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="9c661-114">Wdrażanie hello tooproduction usługi i w zamian hello klucz interfejsu API i OData informacje o punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="9c661-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="9c661-115">Adres URL hello Użyj hello opublikowane za toopublish usługi sieci web[portalu Azure Marketplace (rynku danych)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="9c661-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="9c661-116">Po przesłane, przejrzeć Twoją ofertę i musi toobe zatwierdzona przed klientów można uruchomić jej zakup.</span><span class="sxs-lookup"><span data-stu-id="9c661-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="9c661-117">proces publikowania Hello może potrwać kilka dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="9c661-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="9c661-118">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="9c661-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="9c661-119">Krok 1: Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)</span><span class="sxs-lookup"><span data-stu-id="9c661-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="9c661-120">Jeśli nie zostało zrobione to już, należy spojrzeć na to [przeprowadzenie](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9c661-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="9c661-121">Krok 2: Wdrażanie hello usługi tooproduction i uzyskać informacje o punkcie końcowym klucz interfejsu API i OData hello</span><span class="sxs-lookup"><span data-stu-id="9c661-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="9c661-122">Z hello [klasycznego portalu Azure](http://manage.windowsazure.com), wybierz pozycję hello **UCZENIA MASZYNOWEGO** opcję hello na pasku nawigacyjnym po lewej stronie, a następnie wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="9c661-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="9c661-123">Polecenie hello **usług sieci WEB** kartę i usługi sieci web wybierz hello chcesz toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="9c661-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="9c661-125">Wybierz hello punktu końcowego użytkownik będzie jak toohave hello marketplace używać.</span><span class="sxs-lookup"><span data-stu-id="9c661-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="9c661-126">Jeśli nie utworzono żadnych dodatkowych punktów końcowych, możesz wybrać hello **domyślne** punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="9c661-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="9c661-127">Po kliknięciu przycisku w punkcie końcowym hello, będą mogli toosee hello **klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="9c661-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="9c661-128">Należy ten element informacji później w kroku 3, dlatego należy kopii.</span><span class="sxs-lookup"><span data-stu-id="9c661-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="9c661-130">Polecenie hello **żądanie/odpowiedź** metody, w tym punkcie nie obsługujemy publikowania wykonywania wsadowego usługi toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="9c661-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="9c661-131">Spowoduje to strona pomocy toohello interfejsu API dla hello metoda żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9c661-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="9c661-132">Kopiuj hello **adres punktu końcowego OData**, należy te informacje później w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="9c661-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="9c661-134">Wdrażanie usługi hello w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9c661-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="9c661-135">Krok 3: Adres URL hello Użyj hello opublikowane tooAzure toopublish usługi sieci web witryny Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="9c661-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="9c661-136">Przejdź do zbyt[portalu Azure Marketplace (rynku danych)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="9c661-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="9c661-137">Polecenie hello **publikowania** łącze u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="9c661-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="9c661-138">Spowoduje to przejście toohello [publikowania portalu usługi Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="9c661-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="9c661-139">Polecenie hello **wydawców** tooregister sekcji jako wydawca.</span><span class="sxs-lookup"><span data-stu-id="9c661-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="9c661-140">Podczas tworzenia nowej oferty, wybierz **usług danych**, następnie kliknij przycisk **Utwórz nową usługę danych**.</span><span class="sxs-lookup"><span data-stu-id="9c661-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="9c661-142">W obszarze **plany** zawierają informacje na Twojej oferty, w tym planu cenowego.</span><span class="sxs-lookup"><span data-stu-id="9c661-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="9c661-143">Zdecyduj, jeśli będą oferować usługę wolne lub płatną.</span><span class="sxs-lookup"><span data-stu-id="9c661-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="9c661-144">tooget płatnej, podaj informacje dotyczące płatności, takich jak informacji bankowych i podatku.</span><span class="sxs-lookup"><span data-stu-id="9c661-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="9c661-145">W obszarze **Marketing** zawierają informacje o Twojej oferty, takie jak hello tytuł i opis dla danej oferty.</span><span class="sxs-lookup"><span data-stu-id="9c661-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="9c661-146">W obszarze **cennik** ustawić hello cen dla planów dla określonych krajów lub pozostawić hello "autoprice" ofertę.</span><span class="sxs-lookup"><span data-stu-id="9c661-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="9c661-147">Na powitania **Usługa danych** , kliknij pozycję **usługi sieci Web** jako hello **źródła danych**.</span><span class="sxs-lookup"><span data-stu-id="9c661-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="9c661-149">Pobierz hello klucza usługi sieci web adres URL i interfejsu API z hello klasycznego portalu Azure, zgodnie z objaśnieniem w kroku 2. powyżej.</span><span class="sxs-lookup"><span data-stu-id="9c661-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="9c661-150">W hello okno dialogowe Ustawienia usługi danych portalu Marketplace, wklej adres punktu końcowego OData hello do hello **adres URL usługi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9c661-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="9c661-151">Aby uzyskać **uwierzytelniania**, wybierz **nagłówka** jako hello **schemat uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="9c661-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="9c661-152">Wprowadź "Autoryzacji" hello **nazwa nagłówka**.</span><span class="sxs-lookup"><span data-stu-id="9c661-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="9c661-153">Dla hello **wartość nagłówka**, wprowadź "Bearer" (bez cudzysłowów hello), kliknij przycisk hello **miejsca** paska, a następnie wklej klucz hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9c661-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="9c661-154">Wybierz hello **ta usługa jest OData** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="9c661-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="9c661-155">Kliknij przycisk **Testuj połączenie** tootest hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="9c661-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="9c661-156">W obszarze **kategorii**, upewnij się, **uczenia maszynowego** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="9c661-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="9c661-157">Po zakończeniu wprowadzania wszystkie hello metadanych o ofertę, kliknij **publikowania**, a następnie **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="9c661-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="9c661-158">W tym momencie użytkownik zostanie powiadomiony o pozostałe problemy należy toofix.</span><span class="sxs-lookup"><span data-stu-id="9c661-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="9c661-159">Po zapewnieniu ukończenia wszystkich hello nierozwiązane problemy, kliknij polecenie **żądania zatwierdzenia toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="9c661-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="9c661-160">proces publikowania Hello może potrwać kilka dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="9c661-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

