---
title: "Jak zwiększyć współbieżność usługi sieci web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zwiększyć współbieżność usługi sieci web Azure Machine Learning, dodając dodatkowe punkty końcowe."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "Azure uczenia maszynowego, usług sieci web operationalization skalowania, punkt końcowy, współbieżności"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="301c7-104">Skalowanie usługi sieci web Azure Machine Learning, dodając dodatkowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="301c7-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="301c7-105">W tym temacie opisano techniki dotyczy **klasycznego** usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="301c7-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="301c7-106">Domyślnie każdy opublikowane usługi sieci Web jest skonfigurowany do obsługi 20 równoczesnych żądań i może być możliwie jak 200 równoczesnych żądań.</span><span class="sxs-lookup"><span data-stu-id="301c7-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="301c7-107">Klasyczny portal Azure udostępnia sposób Ustaw tę wartość, uczenie maszynowe Azure automatycznie optymalizuje ustawienie, aby osiągnąć optymalną wydajność dla usługi sieci web i portalu wartość jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="301c7-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="301c7-108">Jeśli planujesz do wywołania interfejsu API z obciążeniem wyższa niż wartość maksymalnej liczby równoczesnych wywołań 200 będzie obsługiwać, należy utworzyć wiele punktów końcowych na tej samej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="301c7-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="301c7-109">Następnie można losowo dystrybucji obciążenia we wszystkich z nich.</span><span class="sxs-lookup"><span data-stu-id="301c7-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="301c7-110">Skalowanie usługi sieci Web jest typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="301c7-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="301c7-111">Niektóre przyczyny skalowania mają obsługuje więcej niż 200 równoczesnych żądań, Zwiększ dostępność za pośrednictwem wiele punktów końcowych lub podaj oddzielne punkty końcowe usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="301c7-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="301c7-112">Skali można zwiększyć przez dodanie dodatkowych punktów końcowych usługi sieci Web za pośrednictwem [klasycznego portalu Azure](https://manage.windowsazure.com/) lub [Usługa sieci Web systemu Azure Machine Learning](https://services.azureml.net/) portalu.</span><span class="sxs-lookup"><span data-stu-id="301c7-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="301c7-113">Aby uzyskać więcej informacji na temat dodawania nowych punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="301c7-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="301c7-114">Należy zwrócić uwagę przy użyciu liczba wysokiej współbieżności mogą być szkodliwe, jeśli nie jest wywołanie interfejsu API z odpowiednio wysoki współczynnik.</span><span class="sxs-lookup"><span data-stu-id="301c7-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="301c7-115">Sporadyczne przekroczeń limitu czasu i/lub nagłego mogą zobaczyć w opóźnienie umieszczenie stosunkowo niska obciążenia na interfejs API skonfigurowane dla wysokie obciążenie.</span><span class="sxs-lookup"><span data-stu-id="301c7-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="301c7-116">Synchroniczne interfejsy API są zazwyczaj używane w sytuacjach, w których jest potrzebne małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="301c7-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="301c7-117">W tym miejscu opóźnienia oznacza czas przyjmuje dla jednego żądania interfejsu API, a nie konto do wszelkich opóźnień sieci.</span><span class="sxs-lookup"><span data-stu-id="301c7-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="301c7-118">Załóżmy, że masz interfejsu API z opóźnieniem 50 ms.</span><span class="sxs-lookup"><span data-stu-id="301c7-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="301c7-119">Pełni korzystać z dostępnej pojemności z poziomu ograniczania wysokiej i maksymalnej liczby równoczesnych wywołań = 20, należy wywołać tego interfejsu API 20 * 1000 / 50 = 400 razy na sekundę.</span><span class="sxs-lookup"><span data-stu-id="301c7-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="301c7-120">Dodatkowo to rozszerzenie, maksymalnej liczby równoczesnych wywołań 200 pozwala wywoływać razy 4000 interfejsu API na sekundę, przy założeniu opóźnienia 50 ms.</span><span class="sxs-lookup"><span data-stu-id="301c7-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
