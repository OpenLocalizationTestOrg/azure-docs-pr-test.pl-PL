---
title: "aaaCreating punktów końcowych usługi sieci Web w uczeniu maszynowym | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="e531f-103">Tworzenie punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="e531f-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="e531f-104">W tym temacie opisano techniki stosowane tooa **klasycznego** usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e531f-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="e531f-105">Podczas tworzenia usług sieci Web, które sprzedawać klientów do przodu tooyour należy tooprovide przeszkolone modele tooeach klienta, który jest nadal połączony toohello eksperymentu, za pomocą których hello sieci Web została utworzona usługa.</span><span class="sxs-lookup"><span data-stu-id="e531f-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="e531f-106">Ponadto wszelkie aktualizacje, które eksperymentu toohello powinny być stosowane selektywnie tooan punktu końcowego bez zastępowania hello dostosowania.</span><span class="sxs-lookup"><span data-stu-id="e531f-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="e531f-107">tooaccomplish, uczenie maszynowe Azure umożliwia toocreate wiele punktów końcowych dla wdrożonej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e531f-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="e531f-108">Każdy punkt końcowy w hello usługi sieci Web jest niezależnie skierowana, ograniczenie i zarządzany.</span><span class="sxs-lookup"><span data-stu-id="e531f-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="e531f-109">Każdy punkt końcowy jest unikatowy klucz adresu URL i autoryzacji rozpowszechniania tooyour klientów.</span><span class="sxs-lookup"><span data-stu-id="e531f-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="e531f-110">Dodawanie usługi sieci Web tooa punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="e531f-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="e531f-111">Istnieją trzy sposoby tooadd tooa punkt końcowy usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e531f-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="e531f-112">Programistycznie</span><span class="sxs-lookup"><span data-stu-id="e531f-112">Programmatically</span></span>
* <span data-ttu-id="e531f-113">Za pomocą portalu usługi sieci Web systemu Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="e531f-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="e531f-114">Mimo że hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e531f-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="e531f-115">Po utworzeniu punktu końcowego hello, możesz pobrać go za pośrednictwem interfejsów API synchroniczne, partii interfejsów API i arkusze programu excel.</span><span class="sxs-lookup"><span data-stu-id="e531f-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="e531f-116">Ponadto punkty końcowe tooadding za pośrednictwem tego interfejsu użytkownika, umożliwia także tooprogrammatically interfejsów API Management punktu końcowego hello Dodawanie punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e531f-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="e531f-117">Jeśli dodano toohello dodatkowe punkty końcowe usługi sieci Web, nie można usunąć hello domyślnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="e531f-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="e531f-118">Programowe Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e531f-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="e531f-119">Można dodać punkt końcowy usługi sieci Web tooyour programowo przy użyciu hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="e531f-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="e531f-120">Dodawanie punktu końcowego za pomocą portalu usługi sieci Web systemu Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="e531f-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="e531f-121">W usłudze Machine Learning Studio kolumny nawigacji po lewej stronie powitania kliknij usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e531f-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="e531f-122">U dołu hello hello pulpit nawigacyjny z usługi sieci Web, kliknij przycisk **zarządzanie punktami końcowymi**.</span><span class="sxs-lookup"><span data-stu-id="e531f-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="e531f-123">portal usługi sieci Web systemu Azure Machine Learning Hello otwiera stronę punkty końcowe toohello hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e531f-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="e531f-124">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="e531f-124">Click **New**.</span></span>
4. <span data-ttu-id="e531f-125">Wpisz nazwę i opis dla nowego punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="e531f-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="e531f-126">Nazwy punktu końcowego musi być 24 znaków lub mniej długości i musi składać się z małych małych liter i cyfr.</span><span class="sxs-lookup"><span data-stu-id="e531f-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="e531f-127">Wybierz poziom rejestrowania hello i czy jest włączone przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="e531f-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="e531f-128">Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi Machine Learning Web](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="e531f-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="e531f-129">Dodawanie punktu końcowego za pomocą hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e531f-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="e531f-130">Zaloguj się toohello [klasycznego portalu Azure](http://manage.windowsazure.com), kliknij przycisk **uczenia maszynowego** w lewej kolumnie hello.</span><span class="sxs-lookup"><span data-stu-id="e531f-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="e531f-131">Kliknij obszar roboczy hello, który zawiera hello usługi sieci Web, w której jesteś zainteresowany.</span><span class="sxs-lookup"><span data-stu-id="e531f-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Przejdź tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="e531f-133">Kliknij przycisk **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e531f-133">Click **Web Services**.</span></span>
   
    ![Przejdź do usługi tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="e531f-135">Kliknij usługę sieci Web hello interesują Cię toosee hello listę dostępnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e531f-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Przejdź tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="e531f-137">U dołu hello hello strony, kliknij przycisk **Dodawanie punktu końcowego**.</span><span class="sxs-lookup"><span data-stu-id="e531f-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="e531f-138">Wpisz nazwę i opis, upewnij się, że nie ma żadnych innych punktów końcowych z hello takie same nazwy tej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e531f-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="e531f-139">Pozostaw hello ograniczania poziom jego wartość domyślna w przypadku braku specjalnych wymagań.</span><span class="sxs-lookup"><span data-stu-id="e531f-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="e531f-140">Zobacz toolearn więcej informacji na temat ograniczania [skalowanie punkty końcowe interfejsu API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e531f-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Tworzenie punktu końcowego](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="e531f-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e531f-142">Next Steps</span></span>
<span data-ttu-id="e531f-143">[Jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e531f-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

