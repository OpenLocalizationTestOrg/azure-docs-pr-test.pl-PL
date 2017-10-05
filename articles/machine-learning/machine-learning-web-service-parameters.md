---
title: "Użyj Azure Machine Learning parametry usługi sieci Web | Dokumentacja firmy Microsoft"
description: "Jak używać parametry usługi sieci Web Azure Machine Learning, aby zmodyfikować zachowanie modelu podczas uzyskiwania dostępu do usługi sieci web."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 482726c1dae5385964e08b720e529817d5907537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="53073-103">Używanie parametrów usługi sieci Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="53073-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="53073-104">Usługi sieci web Azure Machine Learning jest tworzony przez publikowanie eksperymentu, która zawiera moduły można skonfigurować parametrów.</span><span class="sxs-lookup"><span data-stu-id="53073-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="53073-105">W niektórych przypadkach możesz zmienić to zachowanie modułu jest uruchomiona usługa sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="53073-106">*Parametry usługi sieci Web* umożliwiają wykonywanie tego zadania.</span><span class="sxs-lookup"><span data-stu-id="53073-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="53073-107">Typowym przykładem jest konfigurowanie [i zaimportuj dane] [ reader] modułu, aby użytkownik usługi opublikowana w sieci web można określić innego źródła danych podczas uzyskiwania dostępu do usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="53073-108">Lub konfigurowania [eksportowanie danych] [ writer] modułu, dzięki czemu można określić inną lokalizację docelową.</span><span class="sxs-lookup"><span data-stu-id="53073-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="53073-109">Inne przykłady zmiana liczby bitów dla [Tworzenie skrótu funkcji] [ feature-hashing] modułu lub liczbę potrzebne funkcje [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu.</span><span class="sxs-lookup"><span data-stu-id="53073-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="53073-110">Można ustawić parametry usługi sieci Web i skojarz je z jednego lub więcej parametrów modułu w eksperymencie i czy są one wymagane lub opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="53073-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="53073-111">Użytkownik usługi sieci web mogą udzielić im wartości dla tych parametrów, gdy wywołują usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="53073-112">Jak ustawić i skorzystać parametry usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="53073-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="53073-113">Należy zdefiniować parametr usługi sieci Web, klikając ikonę obok parametru modułu i wybierając "Ustaw jako parametr usługi sieci web".</span><span class="sxs-lookup"><span data-stu-id="53073-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="53073-114">Tworzy nowy parametr usługi sieci Web i łączy go do tego parametru modułu.</span><span class="sxs-lookup"><span data-stu-id="53073-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="53073-115">Następnie podczas uzyskiwania dostępu do usługi sieci web użytkownika można określić wartość dla parametru usługi sieci Web i jest stosowane do parametru modułu.</span><span class="sxs-lookup"><span data-stu-id="53073-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="53073-116">Po zdefiniowaniu parametr usługi sieci Web jest dostępne dla innych parametrów modułu w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="53073-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="53073-117">Po zdefiniowaniu parametr usługi sieci Web skojarzony z parametrem dla jednego modułu można użyć tego samego parametru usługi sieci Web dla inny moduł, tak długo, jak parametr oczekuje wartości tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="53073-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="53073-118">Na przykład jeśli parametr usługi sieci Web jest wartość liczbowa, następnie tylko umożliwia dla modułu parametrów, które oczekują wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="53073-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="53073-119">Gdy użytkownik ustawia wartość dla parametru usługi sieci Web, będą dotyczyć wszystkich parametrów skojarzonych modułu.</span><span class="sxs-lookup"><span data-stu-id="53073-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="53073-120">Można zdecydować, czy można podać wartości domyślnej dla parametru usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="53073-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="53073-121">Jeśli to zrobisz, parametr jest opcjonalny dla użytkownika usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="53073-122">Jeśli nie podasz wartość domyślną, użytkownika jest wymagane wprowadzenie wartości podczas uzyskiwania dostępu do usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="53073-123">Dokumentacja interfejsu API usługi sieci web zawiera informacje o użytkowniku usługi sieci web na temat sposobu programowo określić parametr usługi sieci Web podczas uzyskiwania dostępu do usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="53073-124">Dokumentacja interfejsu API dla usługi sieci web klasycznego jest zapewniana za pomocą **strona pomocy interfejsu API** łącze usługi sieci web **pulpitu NAWIGACYJNEGO** w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="53073-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="53073-125">Dokumentacja interfejsu API dla nowej usługi sieci web jest zapewniana za pomocą [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net/Quickstart) portal **Consume** i **interfejsu API programu Swagger** stron dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="53073-126">Przykład</span><span class="sxs-lookup"><span data-stu-id="53073-126">Example</span></span>
<span data-ttu-id="53073-127">Na przykład załóżmy, że mamy doświadczenia z [eksportowanie danych] [ writer] moduł, który wysyła informacje do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53073-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="53073-128">Zdefiniujemy parametr usługi sieci Web o nazwie "Ścieżka obiektu Blob" umożliwiająca użytkownika usługi sieci web zmienić ścieżkę do magazynu obiektów blob podczas uzyskiwania dostępu do usługi.</span><span class="sxs-lookup"><span data-stu-id="53073-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="53073-129">W usłudze Machine Learning Studio, kliknij przycisk [eksportowanie danych] [ writer] modułu, aby go wybrać.</span><span class="sxs-lookup"><span data-stu-id="53073-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="53073-130">Jego właściwości są wyświetlane w okienku właściwości z prawej strony obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="53073-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="53073-131">Określ typ magazynu:</span><span class="sxs-lookup"><span data-stu-id="53073-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="53073-132">W obszarze **określ miejsce docelowe danych**, wybierz pozycję "Magazyn obiektów Blob Azure".</span><span class="sxs-lookup"><span data-stu-id="53073-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="53073-133">W obszarze **Określ typ uwierzytelniania**, wybierz "Konto".</span><span class="sxs-lookup"><span data-stu-id="53073-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="53073-134">Wprowadź informacje o koncie magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53073-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="53073-135">
3.Kliknij ikonę z prawej strony **ścieżki do obiektu blob, począwszy od parametru kontenera**.</span><span class="sxs-lookup"><span data-stu-id="53073-135">
3. Click the icon to the right of the **Path to blob beginning with container parameter**.</span></span> <span data-ttu-id="53073-136">Wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="53073-136">It looks like this:</span></span>
   
   ![Ikona parametr usługi sieci Web][icon]
   
   <span data-ttu-id="53073-138">Wybierz "Ustaw jako parametr usługi sieci web".</span><span class="sxs-lookup"><span data-stu-id="53073-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="53073-139">Wpis zostanie dodany w obszarze **parametry usługi sieci Web** w dolnej części okienka właściwości o nazwie "Ścieżki do obiektu blob kontenera, począwszy od".</span><span class="sxs-lookup"><span data-stu-id="53073-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="53073-140">Jest to parametr usługi sieci Web, która jest teraz skojarzony z tym [eksportowanie danych] [ writer] parametru modułu.</span><span class="sxs-lookup"><span data-stu-id="53073-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="53073-141">Zmień nazwę parametru usługi sieci Web, kliknij nazwę, wprowadź "Ścieżka obiektu Blob" i naciśnij klawisz **Enter** klucza.</span><span class="sxs-lookup"><span data-stu-id="53073-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="53073-142">Aby podać wartości domyślnej dla parametru usługi sieci Web, kliknij ikonę z prawej strony nazwy wybierz "Podać wartości domyślnej", wprowadź wartość (na przykład "container1/output1.csv") i naciśnij klawisz **Enter** klucza.</span><span class="sxs-lookup"><span data-stu-id="53073-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![Parametr usługi sieci Web][parameter]
6. <span data-ttu-id="53073-144">Kliknij pozycję **Run** (Uruchom).</span><span class="sxs-lookup"><span data-stu-id="53073-144">Click **Run**.</span></span> 
7. <span data-ttu-id="53073-145">Kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]** wdrożenie usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="53073-146">Aby wdrożyć nową usługę sieci web musi masz wystarczające uprawnienia do subskrypcji, do którego należy wdrożyć usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="53073-147">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="53073-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="53073-148">Użytkownik usługi sieci web można teraz określić nową lokalizację docelową dla [eksportowanie danych] [ writer] modułu podczas uzyskiwania dostępu do usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53073-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="53073-149">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="53073-149">More information</span></span>
<span data-ttu-id="53073-150">Aby uzyskać bardziej szczegółowy przykład zobacz [parametry usługi sieci Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) wpis w [Machine Learning blogu](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="53073-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="53073-151">Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do usługi sieci web uczenie maszynowe, zobacz [jak korzystać z usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="53073-151">For more information on accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

