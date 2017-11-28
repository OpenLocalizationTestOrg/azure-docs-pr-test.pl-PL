---
title: "Tworzenie punktów końcowych usługi sieci Web usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Tworzenie punktów końcowych usługi sieci Web w usłudze Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="893e7-103">Tworzenie punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="893e7-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="893e7-104">W tym temacie opisano techniki dotyczy **klasycznego** usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="893e7-105">Podczas tworzenia usług sieci Web, które sprzedaży do przodu do klientów, należy podać przeszkolone modeli do każdego klienta, nadal połączonych z doświadczenia, z którego utworzono usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="893e7-106">Ponadto wszelkie aktualizacje eksperymentu powinny być stosowane selektywnie punkt końcowy bez zastępowania dostosowania.</span><span class="sxs-lookup"><span data-stu-id="893e7-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="893e7-107">W tym celu uczenia maszynowego Azure umożliwia tworzenie wielu punktów końcowych dla wdrożonej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="893e7-108">Każdy punkt końcowy usługi sieci Web jest niezależnie skierowana, ograniczenie i zarządzany.</span><span class="sxs-lookup"><span data-stu-id="893e7-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="893e7-109">Każdy punkt końcowy jest unikatowy adres URL i klucza autoryzacji, którą można dystrybuować do klientów.</span><span class="sxs-lookup"><span data-stu-id="893e7-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="893e7-110">Dodawanie punktów końcowych usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="893e7-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="893e7-111">Istnieją trzy sposoby dodawania punktu końcowego usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="893e7-112">Programistycznie</span><span class="sxs-lookup"><span data-stu-id="893e7-112">Programmatically</span></span>
* <span data-ttu-id="893e7-113">Za pomocą portalu usługi sieci Web systemu Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="893e7-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="893e7-114">Chociaż klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="893e7-114">Though the Azure classic portal</span></span>

<span data-ttu-id="893e7-115">Po utworzeniu punktu końcowego, możesz pobrać go za pośrednictwem interfejsów API synchroniczne, partii interfejsów API i arkusze programu excel.</span><span class="sxs-lookup"><span data-stu-id="893e7-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="893e7-116">Oprócz dodania punktów końcowych za pośrednictwem tego interfejsu użytkownika, umożliwia także interfejsów API Management punktu końcowego do programowego dodawania punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="893e7-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="893e7-117">Po dodaniu dodatkowe punkty końcowe z usługą sieci Web, nie można usunąć domyślnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="893e7-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="893e7-118">Programowe Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="893e7-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="893e7-119">Możesz dodać punkt końcowy do usługi sieci Web, programowo przy użyciu [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="893e7-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="893e7-120">Dodawanie punktu końcowego za pomocą portalu usługi sieci Web systemu Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="893e7-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="893e7-121">W usłudze Machine Learning Studio w kolumnie nawigacji po lewej stronie kliknij usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="893e7-122">W dolnej części pulpitu nawigacyjnego usługi sieci Web, kliknij przycisk **zarządzanie punktami końcowymi**.</span><span class="sxs-lookup"><span data-stu-id="893e7-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="893e7-123">Portal usługi sieci Web systemu Azure Machine Learning zostanie otwarta strona punkty końcowe usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="893e7-124">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="893e7-124">Click **New**.</span></span>
4. <span data-ttu-id="893e7-125">Wpisz nazwę i opis dla nowego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="893e7-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="893e7-126">Nazwy punktu końcowego musi być 24 znaków lub mniej długości i musi składać się z małych małych liter i cyfr.</span><span class="sxs-lookup"><span data-stu-id="893e7-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="893e7-127">Wybierz poziom rejestrowania i czy jest włączone przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="893e7-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="893e7-128">Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi Machine Learning Web](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="893e7-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="893e7-129">Dodawanie punktu końcowego przy użyciu klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="893e7-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="893e7-130">Zaloguj się do [klasycznego portalu Azure](http://manage.windowsazure.com), kliknij przycisk **uczenia maszynowego** w lewej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="893e7-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="893e7-131">Kliknij obszar roboczy, który zawiera usługę sieci Web, w której jesteś zainteresowany.</span><span class="sxs-lookup"><span data-stu-id="893e7-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Przejdź do obszaru roboczego](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="893e7-133">Kliknij przycisk **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="893e7-133">Click **Web Services**.</span></span>
   
    ![Przejdź do usługi sieci Web](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="893e7-135">Kliknij usługę sieci Web, który chcesz wyświetlić listę dostępnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="893e7-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Przejdź do punktu końcowego](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="893e7-137">W dolnej części strony kliknij **Dodawanie punktu końcowego**.</span><span class="sxs-lookup"><span data-stu-id="893e7-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="893e7-138">Wpisz nazwę i opis, upewnij się, że nie ma żadnych innych punktów końcowych o takiej samej nazwie w tej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="893e7-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="893e7-139">W przypadku braku specjalnych wymagań pozostaw wartość domyślną poziom ograniczania.</span><span class="sxs-lookup"><span data-stu-id="893e7-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="893e7-140">Aby dowiedzieć się więcej o ograniczaniu przepustowości, zobacz [skalowanie punkty końcowe interfejsu API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="893e7-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Tworzenie punktu końcowego](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="893e7-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="893e7-142">Next Steps</span></span>
<span data-ttu-id="893e7-143">[Jak korzystać z usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="893e7-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

