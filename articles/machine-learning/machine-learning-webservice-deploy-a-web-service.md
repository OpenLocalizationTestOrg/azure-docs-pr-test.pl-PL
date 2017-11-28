---
title: "aaaDeploying nową usługę sieci web w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Usługa sieci web na podstawie Hello przepływ pracy wdrażania ARM"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="539ad-103">Wdrażanie nowej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="539ad-103">Deploy a new web service</span></span>
<span data-ttu-id="539ad-104">Microsoft Azure Machine learning teraz udostępnia usługi sieci web, które są oparte na [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) zezwala na nowe opcje planu rozliczeń i wdrażanie regionów toomultiple usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="539ad-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="539ad-105">Witaj toodeploy ogólny przepływ pracy z usługą sieci web przy użyciu usługi sieci Web Microsoft Azure Machine Learning to:</span><span class="sxs-lookup"><span data-stu-id="539ad-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="539ad-106">Utworzyć eksperyment predykcyjny</span><span class="sxs-lookup"><span data-stu-id="539ad-106">Create a predictive experiment</span></span>
* <span data-ttu-id="539ad-107">Wdróż go</span><span class="sxs-lookup"><span data-stu-id="539ad-107">deploy it</span></span>
* <span data-ttu-id="539ad-108">Konfigurowanie nazwy</span><span class="sxs-lookup"><span data-stu-id="539ad-108">configure its name</span></span>
* <span data-ttu-id="539ad-109">plan rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="539ad-109">billing plan</span></span>
* <span data-ttu-id="539ad-110">należy przeprowadzić test</span><span class="sxs-lookup"><span data-stu-id="539ad-110">test it</span></span>
* <span data-ttu-id="539ad-111">go używać.</span><span class="sxs-lookup"><span data-stu-id="539ad-111">consume it.</span></span>

<span data-ttu-id="539ad-112">powitania po ilustracja przedstawia przepływ pracy dotyczący hello.</span><span class="sxs-lookup"><span data-stu-id="539ad-112">hello following graphic illustrates hello workflow.</span></span>

![Przepływ pracy wdrożenia usługi sieci Web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="539ad-114">Wdrażanie usługi sieci web w Studio</span><span class="sxs-lookup"><span data-stu-id="539ad-114">Deploy web service from Studio</span></span>
<span data-ttu-id="539ad-115">toodeploy eksperymentu jako nową usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="539ad-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="539ad-116">Zaloguj się do hello Machine Learning Studio i utworzyć nową usługę sieci web predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="539ad-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="539ad-117">**Uwaga**: Jeśli zostały już wdrożone eksperymentu jako usługę sieci web klasycznego nie można wdrożyć go jako nową usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="539ad-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="539ad-118">Kliknij przycisk **Uruchom** u dołu hello hello eksperymentu kanwy, a następnie kliknij przycisk **wdrażanie usługi sieci Web** i **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="539ad-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="539ad-119">zostanie otwarta strona wdrożenia Hello hello Menedżera Usługa sieci Web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="539ad-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="539ad-120">Strona eksperymentu wdrażanie Machine Learning Web Service Manager</span><span class="sxs-lookup"><span data-stu-id="539ad-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="539ad-121">Na stronie eksperymentu wdrażanie hello wprowadź nazwę usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="539ad-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="539ad-122">Wybrać planu cenowego.</span><span class="sxs-lookup"><span data-stu-id="539ad-122">Select a pricing plan.</span></span> <span data-ttu-id="539ad-123">Jeśli masz istniejące planu cenowego, że zostanie ona wybrana, w przeciwnym razie należy utworzyć nowy plan cen hello usługi.</span><span class="sxs-lookup"><span data-stu-id="539ad-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="539ad-124">W hello **planu cen** listy rozwijanej, wybierz istniejący plan lub hello **wybierz nowy plan** opcji.</span><span class="sxs-lookup"><span data-stu-id="539ad-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="539ad-125">W **Nazwa planu**, wpisz nazwę identyfikującą planu hello na rachunku.</span><span class="sxs-lookup"><span data-stu-id="539ad-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="539ad-126">Wybierz jedną z hello **miesięcznych poziomów Planowanie**.</span><span class="sxs-lookup"><span data-stu-id="539ad-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="539ad-127">Zauważ, że warstw planu hello domyślne plany toohello w Twoim regionie domyślne i usługi sieci web jest wdrożone toothat regionu.</span><span class="sxs-lookup"><span data-stu-id="539ad-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="539ad-128">Kliknij przycisk **Wdróż** i otwiera hello strony Szybki Start dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="539ad-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="539ad-129">Strona Szybki Start</span><span class="sxs-lookup"><span data-stu-id="539ad-129">Quickstart page</span></span>
<span data-ttu-id="539ad-130">strony Szybki Start usługi sieci web Hello zapewnia dostęp i wskazówki na powitania najbardziej typowych zadań, które ma zostać wykonane po utworzeniu nowej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="539ad-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="539ad-131">W tym miejscu można łatwo dostęp zarówno hello **testu** strony i **Consume** strony.</span><span class="sxs-lookup"><span data-stu-id="539ad-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="539ad-132">Testowanie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="539ad-132">Testing your web service</span></span>
<span data-ttu-id="539ad-133">Ze strony szybkiego startu hello kliknij przycisk Test sieci web usługi w obszarze zadań.</span><span class="sxs-lookup"><span data-stu-id="539ad-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="539ad-134">Usługa sieci web hello tootest jako usługa żądań i odpowiedzi (RR):</span><span class="sxs-lookup"><span data-stu-id="539ad-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="539ad-135">Kliknij przycisk **testu** hello paska menu.</span><span class="sxs-lookup"><span data-stu-id="539ad-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="539ad-136">Kliknij przycisk **żądań i odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="539ad-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="539ad-137">Wprowadź odpowiednie wartości dla kolumny wejściowe hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="539ad-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="539ad-138">Kliknij przycisk Testuj **żądań i odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="539ad-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="539ad-139">Możesz wyniki będą wyświetlane na powitania po prawej stronie powitania strony.</span><span class="sxs-lookup"><span data-stu-id="539ad-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="539ad-140">tootest usługi sieci web usługi wykonywania wsadowego (BES), którego użyjesz pliku CSV:</span><span class="sxs-lookup"><span data-stu-id="539ad-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="539ad-141">Kliknij przycisk **testu** hello paska menu.</span><span class="sxs-lookup"><span data-stu-id="539ad-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="539ad-142">Kliknij przycisk **partii**.</span><span class="sxs-lookup"><span data-stu-id="539ad-142">Click **Batch**.</span></span>
* <span data-ttu-id="539ad-143">W obszarze dane wejściowe kliknij przycisk Przeglądaj i przejdź tooyour przykładowy plik danych.</span><span class="sxs-lookup"><span data-stu-id="539ad-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="539ad-144">Kliknij przycisk **testu**.</span><span class="sxs-lookup"><span data-stu-id="539ad-144">Click **Test**.</span></span>

<span data-ttu-id="539ad-145">Stan Hello testu jest wyświetlany w obszarze **Test zadań wsadowych**.</span><span class="sxs-lookup"><span data-stu-id="539ad-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="539ad-146">Korzystanie z usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="539ad-146">Consuming your Web Service</span></span>
<span data-ttu-id="539ad-147">Po wdrożeniu jako usługę sieci web Azure Machine Learning eksperymenty Podaj interfejsu API REST, które mogą być używane przez szeroki zakres urządzeń i platform.</span><span class="sxs-lookup"><span data-stu-id="539ad-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="539ad-148">Jest to spowodowane komunikatów w formacie hello prosty interfejs API REST akceptuje i odpowiada JSON.</span><span class="sxs-lookup"><span data-stu-id="539ad-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="539ad-149">Witaj portalu usługi Azure Machine Learning zawiera kod, który może służyć usługi sieci web hello toocall R, C# i Python.</span><span class="sxs-lookup"><span data-stu-id="539ad-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="539ad-150">Na stronie Consuming hello można znaleźć:</span><span class="sxs-lookup"><span data-stu-id="539ad-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="539ad-151">klucz interfejsu API Hello i URI służący do konsumowania usługi sieci web w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="539ad-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="539ad-152">Tookick szablonów aplikacji sieci web i Excel uruchomić procesu zużycia.</span><span class="sxs-lookup"><span data-stu-id="539ad-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="539ad-153">Przykładowy kod w języku C#, python i R tooget rozpoczęty.</span><span class="sxs-lookup"><span data-stu-id="539ad-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="539ad-154">Aby uzyskać więcej informacji dotyczących używania usług sieci web, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="539ad-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="539ad-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="539ad-155">Next Steps</span></span>
<span data-ttu-id="539ad-156">Aby uzyskać więcej informacji dotyczących używania usług sieci web zobacz:</span><span class="sxs-lookup"><span data-stu-id="539ad-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="539ad-157">Jak tooconsume usługi sieci Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="539ad-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="539ad-158">Usługi sieci Web uczenie Azure maszyny: Wdrażanie i zużycia</span><span class="sxs-lookup"><span data-stu-id="539ad-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
