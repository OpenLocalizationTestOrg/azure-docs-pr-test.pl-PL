---
title: "aaaUnderstand Centrum IoT Azure bezpośrednie metody | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — użyj metody bezpośredniego tooinvoke kodu na urządzeniach z usługi aplikacji."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="77fc7-103">Informacje o funkcji i wywołanie metody bezpośrednio z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="77fc7-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="77fc7-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="77fc7-104">Overview</span></span>
<span data-ttu-id="77fc7-105">Centrum IoT umożliwia bezpośrednie metody tooinvoke możliwości na urządzeniach z hello chmury.</span><span class="sxs-lookup"><span data-stu-id="77fc7-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="77fc7-106">Bezpośrednie metody reprezentują interakcji żądanie odpowiedź z urządzenia tooan podobne, wywołaj HTTP, w tym ich powodzenie lub niepowodzenie natychmiast (po limitu określonego przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="77fc7-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="77fc7-107">Jest to przydatne w scenariuszach, w którym hello przebiegu natychmiastowego działania różni się w zależności od tego, czy urządzenie hello było możliwe toorespond, takie jak wysyłanie SMS tooa wznawiania urządzenia, jeśli urządzenie jest w trybie offline (SMS są droższe niż wywołania metody).</span><span class="sxs-lookup"><span data-stu-id="77fc7-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="77fc7-108">Każda metoda urządzenia jest przeznaczony dla jednego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77fc7-108">Each device method targets a single device.</span></span> <span data-ttu-id="77fc7-109">[Zadania] [ lnk-devguide-jobs] podania tooinvoke sposób bezpośredniego metod na wielu urządzeniach i Zaplanuj wywołania metody odłączone urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77fc7-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="77fc7-110">Każda osoba mająca **usługa połączyć** uprawnień w Centrum IoT mogą wywołać metodę na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="77fc7-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="77fc7-111">Gdy toouse</span><span class="sxs-lookup"><span data-stu-id="77fc7-111">When toouse</span></span>
<span data-ttu-id="77fc7-112">Bezpośrednie metody wykonaj wzorzec żądań i odpowiedzi i są przeznaczone do komunikacji, które wymagają natychmiastowego potwierdzenia ich wyniku sterowania zwykle interaktywnego hello urządzenia, na przykład tooturn na wentylatora.</span><span class="sxs-lookup"><span data-stu-id="77fc7-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="77fc7-113">Odwołuje się zbyt[wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] w razie wątpliwości między przy użyciu żądanej właściwości, bezpośrednie metod lub komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77fc7-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="77fc7-114">Cykl życia — metoda</span><span class="sxs-lookup"><span data-stu-id="77fc7-114">Method lifecycle</span></span>
<span data-ttu-id="77fc7-115">Bezpośrednie metody są wdrożone na urządzeniu hello i może wymagać zero lub więcej danych wejściowych w toocorrectly ładunku metody hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="77fc7-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="77fc7-116">Wywołaj metodę bezpośrednio za pomocą identyfikatora URI usługi połączonej (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="77fc7-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="77fc7-117">Urządzenie odbiera metody bezpośredniego za pośrednictwem tematu MQTT specyficzne dla urządzenia (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="77fc7-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="77fc7-118">Firma Microsoft może obsługiwać bezpośredniego metody na dodatkowych protokołów sieciowych po stronie urządzenia w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="77fc7-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="77fc7-119">Po wywołaniu metody bezpośrednio na urządzeniu, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych w hello następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="77fc7-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="77fc7-120">Bezpośrednie metody są synchroniczne i albo pomyślnie lub niepowodzeniem hello limit czasu, po (domyślne: 30 sekund, można ustawić w górę too3600 sekund).</span><span class="sxs-lookup"><span data-stu-id="77fc7-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="77fc7-121">Bezpośrednie metody są przydatne w scenariuszach interakcyjne miejscu tooact urządzenia tylko wtedy, gdy urządzenie hello jest online i odbierania poleceń, jak włączenie światła przez telefon.</span><span class="sxs-lookup"><span data-stu-id="77fc7-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="77fc7-122">W tych scenariuszach ma toosee natychmiastowego powodzenie lub niepowodzenie, usługa w chmurze hello może działać na powitania wyniku tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="77fc7-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="77fc7-123">Hello urządzenie może zwrócić niektóre treści wiadomości wyniku metody hello, ale nie jest wymagane dla toodo metody hello tak.</span><span class="sxs-lookup"><span data-stu-id="77fc7-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="77fc7-124">Brak żadnej gwarancji, w kolejności lub dowolnego semantyki współbieżności na wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="77fc7-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="77fc7-125">Metoda bezpośrednia są tylko po stronie chmury hello HTTP i MQTT tylko z hello urządzenia strony.</span><span class="sxs-lookup"><span data-stu-id="77fc7-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="77fc7-126">ładunek Hello metod żądań i odpowiedzi jest too8KB dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="77fc7-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="77fc7-127">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="77fc7-127">Reference topics:</span></span>
<span data-ttu-id="77fc7-128">Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat przy użyciu metod bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="77fc7-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="77fc7-129">Wywoływanie metody bezpośrednio z aplikacji zaplecza</span><span class="sxs-lookup"><span data-stu-id="77fc7-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="77fc7-130">Wywołanie metody</span><span class="sxs-lookup"><span data-stu-id="77fc7-130">Method invocation</span></span>
<span data-ttu-id="77fc7-131">Bezpośrednie wywołania metod na urządzeniu są połączenia HTTP, które obejmują:</span><span class="sxs-lookup"><span data-stu-id="77fc7-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="77fc7-132">Witaj *URI* toohello określonego urządzenia (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="77fc7-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="77fc7-133">Witaj POST *— metoda*</span><span class="sxs-lookup"><span data-stu-id="77fc7-133">hello POST *method*</span></span>
* <span data-ttu-id="77fc7-134">*Nagłówki* które zawiera hello autoryzacji, żądania Identyfikatora, typu zawartości i kodowania zawartości</span><span class="sxs-lookup"><span data-stu-id="77fc7-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="77fc7-135">Przezroczysty JSON *treści* w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="77fc7-135">A transparent JSON *body* in hello following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="77fc7-136">Jest limit czasu w sekundach.</span><span class="sxs-lookup"><span data-stu-id="77fc7-136">Timeout is in seconds.</span></span> <span data-ttu-id="77fc7-137">Jeśli nie ustawiono limit czasu, domyślnie przyjmowana too30 sekund.</span><span class="sxs-lookup"><span data-stu-id="77fc7-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="77fc7-138">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="77fc7-138">Response</span></span>
<span data-ttu-id="77fc7-139">Witaj zaplecza aplikacji otrzymuje odpowiedzi, która obejmuje:</span><span class="sxs-lookup"><span data-stu-id="77fc7-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="77fc7-140">*Kod stanu HTTP*, używany błędy pochodzące z hello Centrum IoT, łącznie z błędem 404 dla urządzeń nie jest obecnie połączony</span><span class="sxs-lookup"><span data-stu-id="77fc7-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="77fc7-141">*Nagłówki* które zawierają hello ETag, żądania Identyfikatora, typu zawartości i kodowania zawartości</span><span class="sxs-lookup"><span data-stu-id="77fc7-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="77fc7-142">JSON *treści* w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="77fc7-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="77fc7-143">Zarówno `status` i `body` są dostarczane przez hello urządzenie i użyć toorespond z kodem stanu dla urządzenia hello i/lub opis.</span><span class="sxs-lookup"><span data-stu-id="77fc7-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="77fc7-144">Dojście metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="77fc7-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="77fc7-145">Wywołanie metody</span><span class="sxs-lookup"><span data-stu-id="77fc7-145">Method invocation</span></span>
<span data-ttu-id="77fc7-146">Urządzenia odbierania żądań metoda bezpośrednia na temat MQTT hello:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="77fc7-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="77fc7-147">urządzenia, które hello odbiera treści Hello znajduje się w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="77fc7-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="77fc7-148">Metoda żądania są QoS 0.</span><span class="sxs-lookup"><span data-stu-id="77fc7-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="77fc7-149">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="77fc7-149">Response</span></span>
<span data-ttu-id="77fc7-150">urządzenie Hello wysyła odpowiedzi zbyt`$iothub/methods/res/{status}/?$rid={request id}`, gdzie:</span><span class="sxs-lookup"><span data-stu-id="77fc7-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="77fc7-151">Witaj `status` właściwość jest hello dostarczone przez urządzenie stan wykonywania metody.</span><span class="sxs-lookup"><span data-stu-id="77fc7-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="77fc7-152">Witaj `$rid` właściwość jest identyfikator żądania powitania od wywołania metody hello odebranych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="77fc7-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="77fc7-153">Treść Hello jest ustawiana przez urządzenie hello i może być dowolnym stanie.</span><span class="sxs-lookup"><span data-stu-id="77fc7-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="77fc7-154">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="77fc7-154">Additional reference material</span></span>
<span data-ttu-id="77fc7-155">Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:</span><span class="sxs-lookup"><span data-stu-id="77fc7-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="77fc7-156">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="77fc7-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="77fc7-157">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello, stosowane toohello usługi IoT Hub, które hello ograniczania tooexpect zachowanie, gdy używasz usługi hello.</span><span class="sxs-lookup"><span data-stu-id="77fc7-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="77fc7-158">[Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="77fc7-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="77fc7-159">[Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje hello tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="77fc7-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="77fc7-160">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.</span><span class="sxs-lookup"><span data-stu-id="77fc7-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77fc7-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77fc7-161">Next steps</span></span>
<span data-ttu-id="77fc7-162">Teraz wiesz już, jak toouse metody bezpośredniego, może Cię zainteresować hello kolejny temat przewodnik dewelopera Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="77fc7-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="77fc7-163">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="77fc7-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="77fc7-164">Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="77fc7-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="77fc7-165">[Użyj metody bezpośredniego][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="77fc7-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
