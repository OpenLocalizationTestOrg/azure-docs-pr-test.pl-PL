---
title: "Współbieżność tooincrease aaaHow usługi sieci web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooincrease współbieżności usługi Azure Machine Learning usługi sieci web przez dodanie dodatkowych punktów końcowych."
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
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="9d094-104">Skalowanie usługi sieci web Azure Machine Learning, dodając dodatkowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="9d094-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="9d094-105">W tym temacie opisano techniki stosowane tooa **klasycznego** usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9d094-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="9d094-106">Domyślnie poszczególnych opublikowanych usług sieci Web jest skonfigurowana toosupport 20 równoczesnych żądań i może być możliwie jak 200 równoczesnych żądań.</span><span class="sxs-lookup"><span data-stu-id="9d094-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="9d094-107">Witaj klasyczny portal Azure udostępnia tooset sposób tę wartość, uczenie maszynowe Azure automatycznie optymalizuje hello ustawienie tooprovide hello najlepszą wydajność usługi sieci web i hello portalu wartość jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="9d094-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="9d094-108">Jeśli planujesz API hello toocall z obciążeniem wyższa niż wartość maksymalnej liczby równoczesnych wywołań 200 będzie obsługiwać, należy utworzyć wiele punktów końcowych na powitania tej samej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9d094-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="9d094-109">Następnie można losowo dystrybucji obciążenia we wszystkich z nich.</span><span class="sxs-lookup"><span data-stu-id="9d094-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="9d094-110">Witaj skalowanie usługi sieci Web jest typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="9d094-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="9d094-111">Niektóre przyczyny tooscale są toosupport ponad 200 równoczesnych żądań, zwiększyć dostępność za pośrednictwem wiele punktów końcowych lub podaj oddzielne punkty końcowe dla usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="9d094-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="9d094-112">Skala hello można zwiększyć przez dodanie dodatkowych punktów końcowych dla hello tej samej usługi sieci Web za pośrednictwem [klasycznego portalu Azure](https://manage.windowsazure.com/) lub hello [Usługa sieci Web systemu Azure Machine Learning](https://services.azureml.net/) portalu.</span><span class="sxs-lookup"><span data-stu-id="9d094-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="9d094-113">Aby uzyskać więcej informacji na temat dodawania nowych punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9d094-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="9d094-114">Należy zwrócić uwagę przy użyciu liczba wysokiej współbieżności mogą być szkodliwe, jeśli nie jest wywoływany hello interfejsu API z odpowiednio wysoki współczynnik.</span><span class="sxs-lookup"><span data-stu-id="9d094-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="9d094-115">Sporadyczne przekroczeń limitu czasu i/lub nagłego mogą zobaczyć w opóźnienia hello umieszczenie stosunkowo niska obciążenia na interfejs API skonfigurowane dla wysokie obciążenie.</span><span class="sxs-lookup"><span data-stu-id="9d094-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="9d094-116">powitalne synchroniczne interfejsy API są zazwyczaj używane w sytuacjach, w których jest potrzebne małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="9d094-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="9d094-117">W tym miejscu opóźnienia oznacza czas hello przyjmuje dla jednego żądania toocomplete hello interfejsu API, a nie konto do wszelkich opóźnień sieci.</span><span class="sxs-lookup"><span data-stu-id="9d094-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="9d094-118">Załóżmy, że masz interfejsu API z opóźnieniem 50 ms.</span><span class="sxs-lookup"><span data-stu-id="9d094-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="9d094-119">toofully stosowanie hello dostępnej pojemności z poziomu ograniczania wysokiej i maksymalnej liczby równoczesnych wywołań = 20, należy toocall ten interfejs API 20 * 1000 / 50 = 400 razy na sekundę.</span><span class="sxs-lookup"><span data-stu-id="9d094-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="9d094-120">Dalsze to rozszerzenie, maksymalnej liczby równoczesnych wywołań 200 umożliwia możesz toocall hello 4000 interfejsu API razy na sekundę, przy założeniu opóźnienia 50 ms.</span><span class="sxs-lookup"><span data-stu-id="9d094-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
