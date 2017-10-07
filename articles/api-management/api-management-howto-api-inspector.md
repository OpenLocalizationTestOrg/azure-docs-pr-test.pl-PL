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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Jak wywołuje hello toouse tootrace inspektora interfejsu API w usłudze Azure API Management
Zarządzanie interfejsami API udostępnia inspektora interfejsu API narzędzia toohelp z debugowania i rozwiązywania problemów z interfejsów API. Witaj interfejsu API można programowo i Inspektora można również bezpośrednio z portalu dla deweloperów hello. 

Ponadto operacji tootracing inspektora interfejsu API również śledzi [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx) oceny. Aby demonstracyjne, zobacz [177 epizodu obejmują chmury: więcej funkcji interfejsu API zarządzania](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too21:00.

Ten przewodnik zawiera omówienie Inspektor interfejsu API.

> [!NOTE]
> Ślady inspektora interfejsu API tylko były generowane i dostępne dla żądań zawierających klucze subskrypcji, które należą toohello [administratora](api-management-howto-create-groups.md) konta.
> 
> 

## <a name="trace-call"></a> Tootrace Użyj interfejsu API inspektora wywołania
Dodaj toouse inspektora interfejsu API **ocp apim śledzenia: true** żądania wywołania operacji tooyour nagłówek, a następnie Pobierz i sprawdzić hello śledzenia przy użyciu adresu URL hello wskazywanym przez hello **ocp-apim śledzenia lokalizacji** Nagłówek odpowiedzi. Można wykonać programowo i można również wykonać bezpośrednio z portalu dla deweloperów hello.

Ten samouczek pokazuje, jak toouse hello interfejsu API inspektora tootrace operacji za pomocą hello podstawowe API Kalkulator skonfigurowanego w hello [pierwszy interfejs API zarządzania](api-management-get-started.md) Wprowadzenie — samouczek. Nie ukończono ten samouczek zajmuje tylko kilka chwil hello tooimport podstawowe Kalkulator interfejsu API, czy można użyć innego interfejsu API Wybieranie takich jak hello Echo interfejsu API. Każde wystąpienie usługi API Management jest wstępnie skonfigurowany z użyciem interfejsu API Echo, które można tooexperiment używanych z i więcej informacji na temat interfejsu API zarządzania. Hello Echo API zwraca Wstecz, niezależnie od dane wejściowe są wysyłane tooit. toouse, można wywołać żadnych zlecenie HTTP, a wartość zwrotna hello po prostu będą zostały wysłane. 

tooget pracę, kliknij przycisk **portalu dla deweloperów** w hello portalu Azure usługi Zarządzanie interfejsami API. Operacje mogą być wywoływane bezpośrednio z portalu dla deweloperów hello oferujący tooview wygodny sposób i przetestować hello operacje interfejsu API.

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

![Zarządzanie interfejsami API portalu dla deweloperów][api-management-developer-portal-menu]

Kliknij przycisk **interfejsów API** z hello menu u góry, a następnie kliknij przycisk **podstawowe Kalkulator**.

![Interfejs Echo API][api-management-api]

Kliknij przycisk **wypróbuj** tootry hello **Dodaj dwie liczb całkowitych** operacji.

![Wypróbuj][api-management-open-console]

Zachowaj hello domyślne wartości parametrów i wybierz hello subskrypcji klucza produktu hello ma toouse z hello **klucza subskrypcji** listy rozwijanej.

Domyślnie w portalu hello developer hello **Ocp Apim śledzenia** nagłówka jest już ustawiona zbyt**true**. Ten nagłówek Określa, czy śledzenie jest generowany.

![Send][api-management-http-get]

Kliknij przycisk **wysyłania** tooinvoke hello operacji.

![Send][api-management-send-results]

W odpowiedzi hello nagłówki zostaną **ocp-apim śledzenia lokalizacji** z wartości toohello podobne, poniższy przykład.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

Witaj śledzenia można pobrać z hello określonej lokalizacji i sprawdzić, jak pokazano w następnym krokiem hello. Zauważ, że tylko hello ostatnich 100 wpisy dziennika są przechowywane i lokalizacje dziennika są ponownie używane w obrotu. Dlatego w przypadku wywołań więcej niż 100 z włączonym śledzeniem po pewnym czasie rozpoczęcia zastępowanie hello pierwsze dane śledzenia w miejscu.

## <a name="inspect-trace"></a>Sprawdzić hello śledzenia
wartości hello tooreview hello śledzenia, Pobierz plik śledzenia hello z hello **ocp-apim śledzenia lokalizacji** adresu URL. Jest to plik tekstowy w formacie JSON i zawiera wpisy toohello podobnie poniższy przykład.

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

## <a name="next-steps"> </a>Następne kroki
* Obejrzyj pokaz śledzenia wyrażenie zasad w [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Pokaz hello toosee too21:00 szybkie przewijanie do przodu.

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




