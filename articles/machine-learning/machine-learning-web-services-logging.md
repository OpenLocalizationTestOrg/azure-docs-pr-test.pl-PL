---
title: "Rejestrowanie dla usługi sieci web usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć rejestrowanie dla usługi sieci web usługi Machine Learning. Rejestrowanie udostępnia dodatkowe informacje ułatwiające rozwiązywanie problemów z interfejsów API."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="61be2-104">Włączanie rejestrowania usług sieci Web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="61be2-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="61be2-105">Ten dokument zawiera informacje o możliwości rejestrowania usług sieci web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="61be2-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="61be2-106">Rejestrowanie udostępnia dodatkowe informacje, poza tylko numer błędu i wiadomości, które ułatwiają rozwiązywanie problemów z wywołaniami interfejsy API Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="61be2-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="61be2-107">Jak włączyć rejestrowanie dla usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="61be2-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="61be2-108">Włączanie rejestrowania z [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu.</span><span class="sxs-lookup"><span data-stu-id="61be2-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="61be2-109">Zaloguj się do portalu usługi sieci Web systemu Azure Machine Learning pod adresem [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="61be2-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="61be2-110">Usługi sieci web klasycznego, można także uzyskać portalu, klikając **nowego środowiska usług sieci Web** na stronie usługi sieci Web usługi Machine Learning w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="61be2-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nowe łącze środowisko usługi sieci Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="61be2-112">Na pasku menu u góry kliknij **usług sieci Web** dla nowej usługi sieci web, lub kliknij przycisk **usług sieci Web klasycznego** dla klasyczny usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="61be2-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Wybierz nowy lub Classic usługi sieci web](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="61be2-114">Aby uzyskać nową usługę sieci web kliknij nazwę usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="61be2-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="61be2-115">Usługi sieci web klasycznego kliknij nazwę usługi sieci web, a następnie w na następnej stronie kliknij odpowiednie punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="61be2-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="61be2-116">Na pasku menu u góry kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="61be2-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="61be2-117">Ustaw **Włącz rejestrowanie** opcji w celu *błąd* (aby rejestruje tylko błędy) lub *wszystkie* (Aby uzyskać pełne rejestrowanie).</span><span class="sxs-lookup"><span data-stu-id="61be2-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Wybierz poziom rejestrowania](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="61be2-119">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="61be2-119">Click **Save**.</span></span>

7. <span data-ttu-id="61be2-120">Dla usług sieci web klasycznego, należy utworzyć **diagnostyki ml** kontenera.</span><span class="sxs-lookup"><span data-stu-id="61be2-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="61be2-121">Wszystkie dzienniki usługi sieci web są przechowywane w kontenerze obiektu blob o nazwie **diagnostyki ml** w ramach konta magazynu skojarzone z usługą sieci web.</span><span class="sxs-lookup"><span data-stu-id="61be2-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="61be2-122">Dla nowej usługi sieci web ten kontener jest tworzony po raz pierwszy dostęp do usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="61be2-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="61be2-123">Dla usług sieci web klasycznego należy utworzyć kontener, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="61be2-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="61be2-124">W [portalu Azure](https://portal.azure.com), przejdź do konta magazynu skojarzone z usługą sieci web.</span><span class="sxs-lookup"><span data-stu-id="61be2-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="61be2-125">W obszarze **usługa Blob**, kliknij przycisk **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="61be2-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="61be2-126">Jeśli kontener **diagnostyki ml** nie istnieje, kliknij przycisk **+ kontener**, nadaj nazwę "ml diagnostyki" kontenera i wybierz **dostęp typu** jako "Blob".</span><span class="sxs-lookup"><span data-stu-id="61be2-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="61be2-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="61be2-127">Click **OK**.</span></span>

      ![Wybierz poziom rejestrowania](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="61be2-129">Usługi sieci web klasycznego pulpitu nawigacyjnego usług sieci Web w usłudze Machine Learning Studio ma przełącznik, aby włączyć rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="61be2-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="61be2-130">Jednak ponieważ rejestrowania będzie teraz zarządzana za pośrednictwem portalu usługi sieci Web, należy włączyć rejestrowanie za pośrednictwem portalu, zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="61be2-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="61be2-131">Jeśli już włączone rejestrowanie w Studio, w portalu usługi sieci Web, należy wyłączyć rejestrowanie i włącz ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="61be2-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="61be2-132">Efekty Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="61be2-132">The effects of enabling logging</span></span>
<span data-ttu-id="61be2-133">Po włączeniu rejestrowania diagnostyki i błędów z punktem końcowym usługi sieci web są rejestrowane w **diagnostyki ml** kontenera obiektów blob na koncie magazynu Azure połączone z obszarem roboczym użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61be2-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="61be2-134">Ten kontener zawiera wszystkie informacje diagnostyczne dla wszystkich sieci web usługi punkty końcowe dla wszystkich obszarów roboczych skojarzonych z tym kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="61be2-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="61be2-135">Dzienniki można wyświetlać przy użyciu dowolnego narzędzia kilka dostępne zapoznać się z konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="61be2-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="61be2-136">Najprostsza może być przejdź do konta magazynu w portalu Azure, kliknij przycisk **kontenery**, a następnie kliknij przycisk kontenera **diagnostyki ml**.</span><span class="sxs-lookup"><span data-stu-id="61be2-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="61be2-137">Dziennik blob szczegółowych informacji</span><span class="sxs-lookup"><span data-stu-id="61be2-137">Log blob detail information</span></span>
<span data-ttu-id="61be2-138">Każdy obiekt blob w kontenerze przechowuje informacje diagnostyczne dla dokładnie jeden z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="61be2-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="61be2-139">Wykonywanie metody wykonywania wsadowego usługi</span><span class="sxs-lookup"><span data-stu-id="61be2-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="61be2-140">Wykonywanie metody żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="61be2-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="61be2-141">Inicjowanie kontenera żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="61be2-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="61be2-142">Nazwa każdego obiektu blob ma prefiks następującą postać:</span><span class="sxs-lookup"><span data-stu-id="61be2-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="61be2-143">Gdzie _typ dziennika_ jest jednym z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="61be2-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="61be2-144">Wsadowe</span><span class="sxs-lookup"><span data-stu-id="61be2-144">batch</span></span>  
* <span data-ttu-id="61be2-145">wynik/żądań</span><span class="sxs-lookup"><span data-stu-id="61be2-145">score/requests</span></span>  
* <span data-ttu-id="61be2-146">wynik/init</span><span class="sxs-lookup"><span data-stu-id="61be2-146">score/init</span></span>  

