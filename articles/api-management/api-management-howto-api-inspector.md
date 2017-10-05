---
title: "Śledzenia wywołań z interfejsu API inspektora - Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak śledzić wywołania Inspektor interfejsu API w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="091c4-103">Sposób użycia interfejsu API inspektora śledzenia wywołań w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="091c4-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="091c4-104">Zarządzanie interfejsami API zawiera narzędzie inspektora interfejsu API, które zapewniają pomoc podczas debugowania i rozwiązywania problemów z interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="091c4-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="091c4-105">Kontroler interfejsu API można programowo i można również bezpośrednio z portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="091c4-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="091c4-106">Oprócz operacji śledzenia śledzi także inspektora interfejsu API [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx) oceny.</span><span class="sxs-lookup"><span data-stu-id="091c4-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="091c4-107">Aby demonstracyjne, zobacz [177 epizodu obejmują chmury: więcej funkcji interfejsu API zarządzania](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 21:00.</span><span class="sxs-lookup"><span data-stu-id="091c4-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="091c4-108">Ten przewodnik zawiera omówienie Inspektor interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="091c4-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="091c4-109">Ślady inspektora interfejsu API tylko były generowane i dostępne dla żądań zawierających klucze subskrypcji, które należą do [administratora](api-management-howto-create-groups.md) konta.</span><span class="sxs-lookup"><span data-stu-id="091c4-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="091c4-110"><a name="trace-call"></a> Użyj interfejsu API inspektora śledzenie wywołania</span><span class="sxs-lookup"><span data-stu-id="091c4-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="091c4-111">Aby używać interfejsu API inspektora, Dodaj **ocp apim śledzenia: true** żądania nagłówka do wywołania operacji, a następnie Pobierz i sprawdzić śledzenia przy użyciu adresu URL, wskazane przez **ocp-apim śledzenia lokalizacji** nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="091c4-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="091c4-112">Można wykonać programowo i można również wykonać bezpośrednio z portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="091c4-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="091c4-113">Ten samouczek przedstawia sposób użycia inspektora interfejsu API przy użyciu interfejsu API podstawowe Kalkulator, skonfigurowanego w operacji śledzenia [pierwszy interfejs API zarządzania](api-management-get-started.md) Wprowadzenie — samouczek.</span><span class="sxs-lookup"><span data-stu-id="091c4-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="091c4-114">Nie ukończono ten samouczek zajmuje tylko kilka minut zaimportować podstawowy interfejs API Kalkulator, czy można użyć innego interfejsu API Wybieranie np. interfejsu API Echo.</span><span class="sxs-lookup"><span data-stu-id="091c4-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="091c4-115">Każde wystąpienie usługi API Management ma wstępnie skonfigurowany interfejs Echo API, którego można używać do eksperymentów oraz poznawania usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="091c4-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="091c4-116">Interfejs API Echo zwraca wstecz niezależnie od danych wejściowych jest wysyłane do niego.</span><span class="sxs-lookup"><span data-stu-id="091c4-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="091c4-117">Aby go użyć, może wywołać żadnych zlecenie HTTP, a wartość zwracana jest zostały wysłane.</span><span class="sxs-lookup"><span data-stu-id="091c4-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="091c4-118">Aby rozpocząć, kliknij przycisk **portalu dla deweloperów** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="091c4-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="091c4-119">Operacje można wywołać bezpośrednio z portalu dla deweloperów, które oferują wygodny sposób, aby wyświetlić i przetestować operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="091c4-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="091c4-120">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="091c4-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Zarządzanie interfejsami API portalu dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="091c4-122">Kliknij przycisk **interfejsów API** z menu u góry, a następnie kliknij przycisk **podstawowe Kalkulator**.</span><span class="sxs-lookup"><span data-stu-id="091c4-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![Interfejs Echo API][api-management-api]

<span data-ttu-id="091c4-124">Kliknij przycisk **wypróbuj** próby **Dodaj dwie liczb całkowitych** operacji.</span><span class="sxs-lookup"><span data-stu-id="091c4-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Wypróbuj][api-management-open-console]

<span data-ttu-id="091c4-126">Zachowaj ustawienie domyślne wartości parametrów, a następnie wybierz subskrypcję klucz produktu ma być używany z **klucza subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="091c4-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="091c4-127">Domyślnie w portalu dla deweloperów **Ocp Apim śledzenia** nagłówka są już ustawione na **true**.</span><span class="sxs-lookup"><span data-stu-id="091c4-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="091c4-128">Ten nagłówek Określa, czy śledzenie jest generowany.</span><span class="sxs-lookup"><span data-stu-id="091c4-128">This header configures whether or not a trace is generated.</span></span>

![Send][api-management-http-get]

<span data-ttu-id="091c4-130">Kliknij przycisk **wysyłania** do wywołania operacji.</span><span class="sxs-lookup"><span data-stu-id="091c4-130">Click **Send** to invoke the operation.</span></span>

![Send][api-management-send-results]

<span data-ttu-id="091c4-132">W odpowiedzi będzie nagłówki **ocp-apim śledzenia lokalizacji** o wartości podobnie do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="091c4-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="091c4-133">Śledzenie można pobrać z określonej lokalizacji i sprawdzić, jak pokazano w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="091c4-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="091c4-134">Zauważ, że są przechowywane tylko ostatnich wpisów dziennika 100 i lokalizacje dziennika są ponownie używane w obrotu.</span><span class="sxs-lookup"><span data-stu-id="091c4-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="091c4-135">Dlatego w przypadku wywołań więcej niż 100 z włączonym śledzeniem po pewnym czasie rozpoczęcia zastępowanie pierwsze dane śledzenia w miejscu.</span><span class="sxs-lookup"><span data-stu-id="091c4-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="091c4-136"><a name="inspect-trace"></a>Sprawdź dane śledzenia</span><span class="sxs-lookup"><span data-stu-id="091c4-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="091c4-137">Aby zapoznać się z wartości w śledzeniu, Pobierz plik śledzenia z **ocp-apim śledzenia lokalizacji** adresu URL.</span><span class="sxs-lookup"><span data-stu-id="091c4-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="091c4-138">Jest to plik tekstowy w formacie JSON i zawiera wpisy podobne do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="091c4-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded to the backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="091c4-139"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="091c4-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="091c4-140">Obejrzyj pokaz śledzenia wyrażenie zasad w [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="091c4-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="091c4-141">Szybko przewinąć do 21:00, aby wyświetlić pokaz.</span><span class="sxs-lookup"><span data-stu-id="091c4-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




