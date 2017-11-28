---
title: "aaaTrace wywołania z interfejsu API inspektora - Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą wywołania tootrace hello inspektora interfejsu API w usłudze Azure API Management."
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
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="897c1-103">Jak wywołuje hello toouse tootrace inspektora interfejsu API w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="897c1-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="897c1-104">Zarządzanie interfejsami API udostępnia inspektora interfejsu API narzędzia toohelp z debugowania i rozwiązywania problemów z interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="897c1-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="897c1-105">Witaj interfejsu API można programowo i Inspektora można również bezpośrednio z portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="897c1-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="897c1-106">Ponadto operacji tootracing inspektora interfejsu API również śledzi [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx) oceny.</span><span class="sxs-lookup"><span data-stu-id="897c1-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="897c1-107">Aby demonstracyjne, zobacz [177 epizodu obejmują chmury: więcej funkcji interfejsu API zarządzania](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too21:00.</span><span class="sxs-lookup"><span data-stu-id="897c1-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="897c1-108">Ten przewodnik zawiera omówienie Inspektor interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="897c1-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="897c1-109">Ślady inspektora interfejsu API tylko były generowane i dostępne dla żądań zawierających klucze subskrypcji, które należą toohello [administratora](api-management-howto-create-groups.md) konta.</span><span class="sxs-lookup"><span data-stu-id="897c1-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="897c1-110"><a name="trace-call"></a> Tootrace Użyj interfejsu API inspektora wywołania</span><span class="sxs-lookup"><span data-stu-id="897c1-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="897c1-111">Dodaj toouse inspektora interfejsu API **ocp apim śledzenia: true** żądania wywołania operacji tooyour nagłówek, a następnie Pobierz i sprawdzić hello śledzenia przy użyciu adresu URL hello wskazywanym przez hello **ocp-apim śledzenia lokalizacji** Nagłówek odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="897c1-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="897c1-112">Można wykonać programowo i można również wykonać bezpośrednio z portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="897c1-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="897c1-113">Ten samouczek pokazuje, jak toouse hello interfejsu API inspektora tootrace operacji za pomocą hello podstawowe API Kalkulator skonfigurowanego w hello [pierwszy interfejs API zarządzania](api-management-get-started.md) Wprowadzenie — samouczek.</span><span class="sxs-lookup"><span data-stu-id="897c1-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="897c1-114">Nie ukończono ten samouczek zajmuje tylko kilka chwil hello tooimport podstawowe Kalkulator interfejsu API, czy można użyć innego interfejsu API Wybieranie takich jak hello Echo interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="897c1-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="897c1-115">Każde wystąpienie usługi API Management jest wstępnie skonfigurowany z użyciem interfejsu API Echo, które można tooexperiment używanych z i więcej informacji na temat interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="897c1-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="897c1-116">Hello Echo API zwraca Wstecz, niezależnie od dane wejściowe są wysyłane tooit.</span><span class="sxs-lookup"><span data-stu-id="897c1-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="897c1-117">toouse, można wywołać żadnych zlecenie HTTP, a wartość zwrotna hello po prostu będą zostały wysłane.</span><span class="sxs-lookup"><span data-stu-id="897c1-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="897c1-118">tooget pracę, kliknij przycisk **portalu dla deweloperów** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="897c1-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="897c1-119">Operacje mogą być wywoływane bezpośrednio z portalu dla deweloperów hello oferujący tooview wygodny sposób i przetestować hello operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="897c1-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="897c1-120">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="897c1-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Zarządzanie interfejsami API portalu dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="897c1-122">Kliknij przycisk **interfejsów API** z hello menu u góry, a następnie kliknij przycisk **podstawowe Kalkulator**.</span><span class="sxs-lookup"><span data-stu-id="897c1-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![Interfejs Echo API][api-management-api]

<span data-ttu-id="897c1-124">Kliknij przycisk **wypróbuj** tootry hello **Dodaj dwie liczb całkowitych** operacji.</span><span class="sxs-lookup"><span data-stu-id="897c1-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Wypróbuj][api-management-open-console]

<span data-ttu-id="897c1-126">Zachowaj hello domyślne wartości parametrów i wybierz hello subskrypcji klucza produktu hello ma toouse z hello **klucza subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="897c1-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="897c1-127">Domyślnie w portalu hello developer hello **Ocp Apim śledzenia** nagłówka jest już ustawiona zbyt**true**.</span><span class="sxs-lookup"><span data-stu-id="897c1-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="897c1-128">Ten nagłówek Określa, czy śledzenie jest generowany.</span><span class="sxs-lookup"><span data-stu-id="897c1-128">This header configures whether or not a trace is generated.</span></span>

![Send][api-management-http-get]

<span data-ttu-id="897c1-130">Kliknij przycisk **wysyłania** tooinvoke hello operacji.</span><span class="sxs-lookup"><span data-stu-id="897c1-130">Click **Send** tooinvoke hello operation.</span></span>

![Send][api-management-send-results]

<span data-ttu-id="897c1-132">W odpowiedzi hello nagłówki zostaną **ocp-apim śledzenia lokalizacji** z wartości toohello podobne, poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="897c1-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="897c1-133">Witaj śledzenia można pobrać z hello określonej lokalizacji i sprawdzić, jak pokazano w następnym krokiem hello.</span><span class="sxs-lookup"><span data-stu-id="897c1-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="897c1-134">Zauważ, że tylko hello ostatnich 100 wpisy dziennika są przechowywane i lokalizacje dziennika są ponownie używane w obrotu.</span><span class="sxs-lookup"><span data-stu-id="897c1-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="897c1-135">Dlatego w przypadku wywołań więcej niż 100 z włączonym śledzeniem po pewnym czasie rozpoczęcia zastępowanie hello pierwsze dane śledzenia w miejscu.</span><span class="sxs-lookup"><span data-stu-id="897c1-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="897c1-136"><a name="inspect-trace"></a>Sprawdzić hello śledzenia</span><span class="sxs-lookup"><span data-stu-id="897c1-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="897c1-137">wartości hello tooreview hello śledzenia, Pobierz plik śledzenia hello z hello **ocp-apim śledzenia lokalizacji** adresu URL.</span><span class="sxs-lookup"><span data-stu-id="897c1-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="897c1-138">Jest to plik tekstowy w formacie JSON i zawiera wpisy toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="897c1-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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
                    "message": "Request is being forwarded toohello backend service.",
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
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="897c1-139"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="897c1-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="897c1-140">Obejrzyj pokaz śledzenia wyrażenie zasad w [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="897c1-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="897c1-141">Pokaz hello toosee too21:00 szybkie przewijanie do przodu.</span><span class="sxs-lookup"><span data-stu-id="897c1-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
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




