---
title: "(przestarzałe) Publikowanie usługi machine learning web service w portalu Azure Marketplace | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Jak opublikować usługi sieci Web Azure Machine Learning w portalu Azure Marketplace"
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
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="d09ac-103">(przestarzałe) Publikowanie usługi sieci Web Azure Machine Learning w portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="d09ac-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="d09ac-104">DataMarket i usług danych jest wycofana i istniejące subskrypcje zostaną wycofane i anulowane uruchamianie 3/31/2017 r.</span><span class="sxs-lookup"><span data-stu-id="d09ac-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="d09ac-105">W związku z tym w tym artykule jest przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="d09ac-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="d09ac-106">Alternatywnie, można opublikować eksperymentów uczenia maszynowego do [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) dla społeczności analizy danych.</span><span class="sxs-lookup"><span data-stu-id="d09ac-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="d09ac-107">Aby uzyskać więcej informacji, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="d09ac-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="d09ac-108">W portalu Azure Marketplace pozwala, aby opublikować usługi sieci web Azure Machine Learning płatnej, lub zwolnij usługi do użycia przez klientów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="d09ac-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="d09ac-109">Ten artykuł zawiera omówienie procesu z łącza do wskazówki ułatwiające rozpoczęcie pracy.</span><span class="sxs-lookup"><span data-stu-id="d09ac-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="d09ac-110">Za pomocą tego procesu, można udostępnić swoje usługi sieci web innych deweloperom korzystanie w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="d09ac-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="d09ac-111">Omówienie procesu publikowania</span><span class="sxs-lookup"><span data-stu-id="d09ac-111">Overview of the publishing process</span></span>
<span data-ttu-id="d09ac-112">Poniżej przedstawiono kroki publikowania usługi sieci web uczenie maszynowe Azure w portalu Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="d09ac-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="d09ac-113">Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)</span><span class="sxs-lookup"><span data-stu-id="d09ac-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="d09ac-114">Wdrażanie usługi do środowiska produkcyjnego i uzyskiwania informacji punktu końcowego klucz interfejsu API i OData.</span><span class="sxs-lookup"><span data-stu-id="d09ac-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="d09ac-115">Użyj adresu URL usługi sieci web opublikowane do publikowania [portalu Azure Marketplace (rynku danych)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="d09ac-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="d09ac-116">Po przesłane, przejrzeć Twoją ofertę i wymaga zatwierdzenia przed klientów można uruchomić jej zakup.</span><span class="sxs-lookup"><span data-stu-id="d09ac-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="d09ac-117">Publikowanie proces może potrwać kilka dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="d09ac-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="d09ac-118">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="d09ac-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="d09ac-119">Krok 1: Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)</span><span class="sxs-lookup"><span data-stu-id="d09ac-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="d09ac-120">Jeśli nie zostało zrobione to już, należy spojrzeć na to [przeprowadzenie](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="d09ac-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="d09ac-121">Krok 2: Wdrażanie usługi do środowiska produkcyjnego i uzyskać klucz interfejsu API i informacje o punkcie końcowym OData</span><span class="sxs-lookup"><span data-stu-id="d09ac-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="d09ac-122">Z [klasycznego portalu Azure](http://manage.windowsazure.com), wybierz pozycję **UCZENIA MASZYNOWEGO** opcji na pasku nawigacyjnym po lewej stronie, a następnie wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="d09ac-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="d09ac-123">Polecenie **usług sieci WEB** , a następnie wybierz usługę sieci web ma zostać publikowanie w portalu marketplace.</span><span class="sxs-lookup"><span data-stu-id="d09ac-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="d09ac-125">Wybierz punkt końcowy chcesz korzystać z portalu marketplace.</span><span class="sxs-lookup"><span data-stu-id="d09ac-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="d09ac-126">Jeśli nie utworzono żadnych dodatkowych punktów końcowych, możesz wybrać **domyślne** punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d09ac-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="d09ac-127">Po kliknięciu przycisku w punkcie końcowym, będzie mógł wyświetlić **klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="d09ac-128">Należy ten element informacji później w kroku 3, dlatego należy kopii.</span><span class="sxs-lookup"><span data-stu-id="d09ac-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="d09ac-130">Polecenie **żądanie/odpowiedź** metody, w tym punkcie publikowania usługi wykonywania wsadowego w portalu Marketplace nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="d09ac-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="d09ac-131">Spowoduje to do strona pomocy interfejsu API dla metody żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d09ac-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="d09ac-132">Kopiuj **adres punktu końcowego OData**, należy te informacje później w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="d09ac-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="d09ac-134">Wdrażanie usługi do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d09ac-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="d09ac-135">Krok 3: Użyj adresu URL usługi sieci web opublikowane do publikowania w portalu Azure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="d09ac-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="d09ac-136">Przejdź do [witrynę Azure Marketplace (rynku danych)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="d09ac-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="d09ac-137">Polecenie **publikowania** łącze w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="d09ac-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="d09ac-138">Spowoduje to przejście do [publikowania portalu usługi Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="d09ac-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="d09ac-139">Polecenie **wydawców** sekcji, aby zarejestrować jako wydawca.</span><span class="sxs-lookup"><span data-stu-id="d09ac-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="d09ac-140">Podczas tworzenia nowej oferty, wybierz **usług danych**, następnie kliknij przycisk **Utwórz nową usługę danych**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="d09ac-142">W obszarze **plany** zawierają informacje na Twojej oferty, w tym planu cenowego.</span><span class="sxs-lookup"><span data-stu-id="d09ac-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="d09ac-143">Zdecyduj, jeśli będą oferować usługę wolne lub płatną.</span><span class="sxs-lookup"><span data-stu-id="d09ac-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="d09ac-144">Aby uzyskać płatną, podaj informacje dotyczące płatności, takich jak informacji bankowych i podatek.</span><span class="sxs-lookup"><span data-stu-id="d09ac-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="d09ac-145">W obszarze **Marketing** zawierają informacje o Twojej oferty, takie jak tytuł i opis dla danej oferty.</span><span class="sxs-lookup"><span data-stu-id="d09ac-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="d09ac-146">W obszarze **cennik** można ustawić ceny dla planów dla określonych krajów lub Niech system "autoprice" ofertę.</span><span class="sxs-lookup"><span data-stu-id="d09ac-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="d09ac-147">Na **Usługa danych** , kliknij pozycję **usługi sieci Web** jako **źródła danych**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="d09ac-149">Pobierz klucz adresu URL i interfejsu API usługi sieci web z klasycznego portalu Azure, zgodnie z objaśnieniem w kroku 2. powyżej.</span><span class="sxs-lookup"><span data-stu-id="d09ac-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="d09ac-150">W oknie dialogowym Instalator usługi danych portalu Marketplace, wklej adres punktu końcowego OData do **adres URL usługi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d09ac-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="d09ac-151">Aby uzyskać **uwierzytelniania**, wybierz **nagłówka** jako **schemat uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="d09ac-152">Wprowadź "Autoryzacji" **nazwa nagłówka**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="d09ac-153">Dla **wartość nagłówka**wpisz "Bearer" (bez cudzysłowów), kliknij przycisk **miejsca** pasek, a następnie wklej klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d09ac-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="d09ac-154">Wybierz **ta usługa jest OData** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="d09ac-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="d09ac-155">Kliknij przycisk **Testuj połączenie** testowania połączenia.</span><span class="sxs-lookup"><span data-stu-id="d09ac-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="d09ac-156">W obszarze **kategorii**, upewnij się, **uczenia maszynowego** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="d09ac-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="d09ac-157">Po zakończeniu wprowadzania wszystkie metadane dotyczące Twojej oferty, kliknij **publikowania**, a następnie **wypychania do przemieszczania**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="d09ac-158">W tym momencie dowiesz się wszelkie pozostałe problemy, które trzeba naprawić.</span><span class="sxs-lookup"><span data-stu-id="d09ac-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="d09ac-159">Po zapewnieniu ukończenia nierozwiązane problemy, kliknij polecenie **zażądać zatwierdzenia do produkcji**.</span><span class="sxs-lookup"><span data-stu-id="d09ac-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="d09ac-160">Publikowanie proces może potrwać kilka dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="d09ac-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

