---
title: "Zrozumienie metod bezpośredniego Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — użyj bezpośredniego metody do wywołania kodu na urządzeniach z usługi aplikacji."
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
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="47f77-103">Informacje o funkcji i wywołanie metody bezpośrednio z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="47f77-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="47f77-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="47f77-104">Overview</span></span>
<span data-ttu-id="47f77-105">Centrum IoT daje możliwość wywołania metod bezpośrednio na urządzeniach z chmury.</span><span class="sxs-lookup"><span data-stu-id="47f77-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="47f77-106">Bezpośrednie metody reprezentują żądanie odpowiedź interakcji z urządzeniem podobna do wywołania HTTP w tym ich powodzenie lub niepowodzenie natychmiast (po limitu określonego przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="47f77-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="47f77-107">Jest to przydatne w scenariuszach, w którym kursu natychmiastowego działania różni się w zależności od tego, czy urządzenie mógł odpowiedzieć, takie jak wysyłanie SMS wake-up na urządzeniu, jeśli urządzenie jest w trybie offline (SMS są droższe niż wywołania metody).</span><span class="sxs-lookup"><span data-stu-id="47f77-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="47f77-108">Każda metoda urządzenia jest przeznaczony dla jednego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="47f77-108">Each device method targets a single device.</span></span> <span data-ttu-id="47f77-109">[Zadania] [ lnk-devguide-jobs] umożliwiają wywołania metod bezpośrednio na wielu urządzeniach i Zaplanuj wywołania metody odłączone urządzenia.</span><span class="sxs-lookup"><span data-stu-id="47f77-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="47f77-110">Każda osoba mająca **usługa połączyć** uprawnień w Centrum IoT mogą wywołać metodę na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="47f77-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="47f77-111">Kiedy stosować</span><span class="sxs-lookup"><span data-stu-id="47f77-111">When to use</span></span>
<span data-ttu-id="47f77-112">Bezpośrednie metody wykonaj wzorzec żądań i odpowiedzi i są przeznaczone do komunikacji, które wymagają natychmiastowego potwierdzenia ich wyniku sterowania zwykle interaktywnego urządzenia, na przykład aby włączyć wentylatora.</span><span class="sxs-lookup"><span data-stu-id="47f77-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="47f77-113">Zapoznaj się [wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] w razie wątpliwości między przy użyciu żądanej właściwości, bezpośrednie metod lub komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="47f77-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="47f77-114">Cykl życia — metoda</span><span class="sxs-lookup"><span data-stu-id="47f77-114">Method lifecycle</span></span>
<span data-ttu-id="47f77-115">Bezpośrednie metody są wdrożone na urządzeniu i może wymagać zero lub więcej danych wejściowych w ładunku metody, aby poprawnie utworzyć wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="47f77-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="47f77-116">Wywołaj metodę bezpośrednio za pomocą identyfikatora URI usługi połączonej (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="47f77-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="47f77-117">Urządzenie odbiera metody bezpośredniego za pośrednictwem tematu MQTT specyficzne dla urządzenia (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="47f77-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="47f77-118">Firma Microsoft może obsługiwać bezpośredniego metod na dodatkowych protokołów sieciowych po stronie urządzenia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="47f77-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="47f77-119">Po wywołaniu metody bezpośrednio na urządzeniu, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych z następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="47f77-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="47f77-120">Bezpośrednie metody są synchroniczne i albo pomyślnie lub zakończyć się niepowodzeniem po upływie limitu czasu (domyślne: 30 sekund, można ustawić się do 3600 sekund).</span><span class="sxs-lookup"><span data-stu-id="47f77-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="47f77-121">Bezpośrednie metody są przydatne w scenariuszach interakcyjne miejsce na urządzeniu działa tylko wtedy, gdy urządzenie jest online i odbierania poleceń, jak włączenie światła przez telefon.</span><span class="sxs-lookup"><span data-stu-id="47f77-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="47f77-122">W tych scenariuszach chcesz wyświetlić natychmiastowego powodzenie lub niepowodzenie, dlatego usługa w chmurze może działać na wynik tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="47f77-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="47f77-123">Urządzenie może zwrócić niektóre treści wiadomości wyniku metody, ale nie jest wymagane dla metody to zrobić.</span><span class="sxs-lookup"><span data-stu-id="47f77-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="47f77-124">Brak żadnej gwarancji, w kolejności lub dowolnego semantyki współbieżności na wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="47f77-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="47f77-125">Metoda bezpośrednia są tylko po stronie chmury HTTP i MQTT tylko po stronie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="47f77-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="47f77-126">Ładunek dla metod żądań i odpowiedzi jest maksymalnie 8KB dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="47f77-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="47f77-127">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="47f77-127">Reference topics:</span></span>
<span data-ttu-id="47f77-128">Następujące tematy dokumentacji dostarczają więcej informacji na temat przy użyciu metod bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="47f77-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="47f77-129">Wywoływanie metody bezpośrednio z aplikacji zaplecza</span><span class="sxs-lookup"><span data-stu-id="47f77-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="47f77-130">Wywołanie metody</span><span class="sxs-lookup"><span data-stu-id="47f77-130">Method invocation</span></span>
<span data-ttu-id="47f77-131">Bezpośrednie wywołania metod na urządzeniu są połączenia HTTP, które obejmują:</span><span class="sxs-lookup"><span data-stu-id="47f77-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="47f77-132">*URI* specyficzne dla urządzenia (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="47f77-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="47f77-133">WPIS *— metoda*</span><span class="sxs-lookup"><span data-stu-id="47f77-133">The POST *method*</span></span>
* <span data-ttu-id="47f77-134">*Nagłówki* które zawiera autoryzacji, żądania Identyfikatora, typu zawartości i kodowania zawartości</span><span class="sxs-lookup"><span data-stu-id="47f77-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="47f77-135">Przezroczysty JSON *treści* w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="47f77-135">A transparent JSON *body* in the following format:</span></span>

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

<span data-ttu-id="47f77-136">Jest limit czasu w sekundach.</span><span class="sxs-lookup"><span data-stu-id="47f77-136">Timeout is in seconds.</span></span> <span data-ttu-id="47f77-137">Jeśli nie ustawiono limit czasu, domyślnie 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="47f77-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="47f77-138">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="47f77-138">Response</span></span>
<span data-ttu-id="47f77-139">Aplikacja zaplecza odbiera odpowiedzi, która obejmuje:</span><span class="sxs-lookup"><span data-stu-id="47f77-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="47f77-140">*Kod stanu HTTP*, używany dla błędów pochodzących z Centrum IoT, łącznie z błędem 404 dla urządzeń nie jest obecnie połączony</span><span class="sxs-lookup"><span data-stu-id="47f77-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="47f77-141">*Nagłówki* który zawiera element ETag, żądania Identyfikatora, typu zawartości i kodowania zawartości</span><span class="sxs-lookup"><span data-stu-id="47f77-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="47f77-142">JSON *treści* w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="47f77-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="47f77-143">Zarówno `status` i `body` udostępnianym przez urządzenie i używane do odpowiedzi z kodem stanu własnych urządzeń i/lub opis.</span><span class="sxs-lookup"><span data-stu-id="47f77-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="47f77-144">Dojście metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="47f77-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="47f77-145">Wywołanie metody</span><span class="sxs-lookup"><span data-stu-id="47f77-145">Method invocation</span></span>
<span data-ttu-id="47f77-146">Urządzenia odbierania żądań metoda bezpośrednia na temat MQTT:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="47f77-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="47f77-147">Treści, który odbiera urządzenie znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="47f77-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="47f77-148">Metoda żądania są QoS 0.</span><span class="sxs-lookup"><span data-stu-id="47f77-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="47f77-149">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="47f77-149">Response</span></span>
<span data-ttu-id="47f77-150">Urządzenie wysyła odpowiedzi `$iothub/methods/res/{status}/?$rid={request id}`, gdzie:</span><span class="sxs-lookup"><span data-stu-id="47f77-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="47f77-151">`status` Właściwość jest stan wykonanie metody dostarczone przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="47f77-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="47f77-152">`$rid` Właściwość jest identyfikator żądania z wywołania metody odebranych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="47f77-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="47f77-153">Treść jest ustawiana przez urządzenia i może być dowolnym stanie.</span><span class="sxs-lookup"><span data-stu-id="47f77-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="47f77-154">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="47f77-154">Additional reference material</span></span>
<span data-ttu-id="47f77-155">Inne tematy referencyjne w Podręczniku dewelopera Centrum IoT obejmują:</span><span class="sxs-lookup"><span data-stu-id="47f77-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="47f77-156">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="47f77-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="47f77-157">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziałów, które dotyczą usługi IoT Hub i ograniczania przepustowości zachowania można oczekiwać podczas korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="47f77-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="47f77-158">[Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] wymieniono języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="47f77-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="47f77-159">[Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje język zapytań Centrum IoT można pobrać z Centrum IoT informacji o twins urządzenia i zadania.</span><span class="sxs-lookup"><span data-stu-id="47f77-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="47f77-160">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zapewnia więcej informacji na temat Centrum IoT obsługi protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="47f77-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47f77-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47f77-161">Next steps</span></span>
<span data-ttu-id="47f77-162">Po zapoznaniu bezpośredniego metod, mogą być zainteresowane w następującym temacie przewodnika deweloperów Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="47f77-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="47f77-163">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="47f77-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="47f77-164">Jeśli chcesz wypróbować niektóre pojęcia opisane w tym artykule, mogą być zainteresowane w następujących instrukcji Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="47f77-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="47f77-165">[Użyj metody bezpośredniego][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="47f77-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
