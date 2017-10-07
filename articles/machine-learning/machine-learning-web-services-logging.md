---
title: "aaaLogging usług sieci web usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak jest rejestrowanie tooenable uczenia maszynowego usługi sieci web. Rejestrowanie udostępnia dodatkowe informacje toohelp Rozwiązywanie problemów z hello interfejsów API."
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
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="fa425-104">Włączanie rejestrowania usług sieci Web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fa425-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="fa425-105">Ten dokument zawiera informacje na powitania rejestrowania możliwości usługi sieci web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fa425-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="fa425-106">Rejestrowanie udostępnia dodatkowe informacje, poza tylko liczbą błędów i komunikatów, które mogą pomóc w rozwiązaniu toohello Twojego wywołania Machine Learning API.</span><span class="sxs-lookup"><span data-stu-id="fa425-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="fa425-107">Sposób rejestrowania tooenable usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="fa425-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="fa425-108">Włączanie rejestrowania z hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu.</span><span class="sxs-lookup"><span data-stu-id="fa425-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="fa425-109">Zaloguj się w portalu usługi sieci Web systemu Azure Machine Learning toohello [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="fa425-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="fa425-110">Usługi sieci web klasycznego portalu toohello można także uzyskać, klikając **nowego środowiska usług sieci Web** na stronie usługi sieci Web usługi Machine Learning hello w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fa425-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nowe łącze środowisko usługi sieci Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="fa425-112">Na pasku menu u góry hello kliknij **usług sieci Web** dla nowej usługi sieci web, lub kliknij przycisk **usług sieci Web klasycznego** dla klasyczny usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="fa425-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Wybierz nowy lub Classic usługi sieci web](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="fa425-114">Aby uzyskać nową usługę sieci web kliknij nazwę usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="fa425-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="fa425-115">Usługi sieci web klasycznego kliknij nazwę usługi sieci web hello, a następnie na następnej stronie powitania kliknij przycisk hello odpowiedniego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="fa425-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="fa425-116">Na pasku menu u góry hello kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="fa425-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="fa425-117">Zestaw hello **Włącz rejestrowanie** opcję zbyt*błąd* (toolog tylko błędy) lub *wszystkie* (Aby uzyskać pełne rejestrowanie).</span><span class="sxs-lookup"><span data-stu-id="fa425-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Wybierz poziom rejestrowania](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="fa425-119">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fa425-119">Click **Save**.</span></span>

7. <span data-ttu-id="fa425-120">Dla usług sieci web klasycznego, należy utworzyć hello **diagnostyki ml** kontenera.</span><span class="sxs-lookup"><span data-stu-id="fa425-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="fa425-121">Wszystkie dzienniki usługi sieci web są przechowywane w kontenerze obiektu blob o nazwie **diagnostyki ml** na koncie magazynu hello skojarzony z usługą sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="fa425-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="fa425-122">Dla nowej usługi sieci web ten kontener jest tworzony powitania po raz pierwszy uzyskać dostępu do usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="fa425-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="fa425-123">Dla usług sieci web klasycznego należy toocreate hello kontenera Jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="fa425-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="fa425-124">W hello [portalu Azure](https://portal.azure.com), przejdź do pozycji toohello konta magazynu skojarzone z usługą sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="fa425-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="fa425-125">W obszarze **usługa Blob**, kliknij przycisk **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="fa425-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="fa425-126">Jeśli kontener hello **diagnostyki ml** nie istnieje, kliknij przycisk **+ kontener**, nadaj hello kontenera hello nazwy "ml Diagnostyka" i wybierz hello **dostęp typu** jako "Blob".</span><span class="sxs-lookup"><span data-stu-id="fa425-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="fa425-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa425-127">Click **OK**.</span></span>

      ![Wybierz poziom rejestrowania](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="fa425-129">Usługi sieci web klasycznego hello pulpitu nawigacyjnego usług sieci Web w usłudze Machine Learning Studio zawiera rejestrowania tooenable przełącznika.</span><span class="sxs-lookup"><span data-stu-id="fa425-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="fa425-130">Ponieważ rejestrowanie jest teraz zarządzane za pośrednictwem hello usług sieci Web portalu, jednak tooenable rejestrowanie za pośrednictwem portalu hello zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="fa425-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="fa425-131">Jeśli już włączone rejestrowanie w Studio, w hello Portal usługi sieci Web, należy wyłączyć rejestrowanie i włącz ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="fa425-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="fa425-132">efekty Hello Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="fa425-132">hello effects of enabling logging</span></span>
<span data-ttu-id="fa425-133">Po włączeniu rejestrowania diagnostyki hello i błędów z punktem końcowym usługi sieci web hello są rejestrowane w hello **diagnostyki ml** kontenera obiektów blob w hello konta magazynu Azure połączone z obszarem roboczym hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa425-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="fa425-134">Ten kontener zawiera wszystkie informacje diagnostyczne powitania dla wszystkich hello usługi punktów końcowych sieci web dla wszystkich hello obszary robocze skojarzone z tym kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="fa425-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="fa425-135">Hello dzienniki można wyświetlać przy użyciu dowolnego hello kilku dostępnych narzędzi tooexplore konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa425-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="fa425-136">Najprostszym Hello może być toonavigate toohello magazynu konta w portalu Azure hello, kliknij przycisk **kontenery**, a następnie kliknij przycisk kontenera hello **diagnostyki ml**.</span><span class="sxs-lookup"><span data-stu-id="fa425-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="fa425-137">Dziennik blob szczegółowych informacji</span><span class="sxs-lookup"><span data-stu-id="fa425-137">Log blob detail information</span></span>
<span data-ttu-id="fa425-138">Każdy obiekt blob w kontenerze hello przechowuje informacje diagnostyczne hello dokładnie jednego hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="fa425-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="fa425-139">Wykonywanie metody hello wykonywania wsadowego usługi</span><span class="sxs-lookup"><span data-stu-id="fa425-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="fa425-140">Wykonywanie metody hello żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fa425-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="fa425-141">Inicjowanie kontenera żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fa425-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="fa425-142">Nazwa Hello każdy obiekt blob ma prefiks hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="fa425-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="fa425-143">Gdzie _typ dziennika_ jest jednym z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="fa425-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="fa425-144">Wsadowe</span><span class="sxs-lookup"><span data-stu-id="fa425-144">batch</span></span>  
* <span data-ttu-id="fa425-145">wynik/żądań</span><span class="sxs-lookup"><span data-stu-id="fa425-145">score/requests</span></span>  
* <span data-ttu-id="fa425-146">wynik/init</span><span class="sxs-lookup"><span data-stu-id="fa425-146">score/init</span></span>  

